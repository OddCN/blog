---
english_title: draco-guide-3
title: draco教程（三）：draco与three.js相遇
date: 2017-07-26 10:46:16
---

加载.drc，渲染一个可以旋转的3D模型

<!-- more -->

---

索引：

[draco教程（一）：准备工作](http://oddcn.cn/2017/07/11/draco-guide-1/)
[draco教程（二）：3D模型obj压缩](http://oddcn.cn/2017/07/12/draco-guide-2/)
draco教程（三）：draco与Three.js相遇

---

# 简介

[three.js](https://threejs.org/)可以说是非常有名了，它是一个JavaScript库，帮助我们在浏览器中绘制、控制3D场景。官网有很多炫酷的示例项目，还有文档以及例子。

本文对Google的codelabs中的教程做了翻译、整理和扩展，[原教程](https://codelabs.developers.google.com/codelabs/draco-3d/index.html?index=..%2F..%2Fio2017#5)可能需要科学上网。

# 准备

## 成果预览

提前预览 [成果](http://draco3js.oddcn.cn/)
可以更快明白我们要将做什么。

## 工程目录

- dracoWithThreeJs
  - js
    - three.min.js
    - OrbitControls.js
    - draco_decoder.js
    - DRACOLoader.js
  - test.drc
  - index.html

## .js下载和.drc下载

[js.zip](http://draco3js.oddcn.cn/js/js.zip)

|               js | 功能                       |
| ---------------: | ------------------------ |
|     three.min.js | three.js的核心              |
| OrbitControls.js | three.js的相机控制器，用于鼠标拖动、旋转 |
| draco_decoder.js | draco解码                  |
|   DRACOLoader.js | draco加载                  |

[test.drc](http://draco3js.oddcn.cn/test.drc)

# 示例代码

以下代码按顺序依次粘贴至index.html

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>draco with three js</title>
</head>
<script src="js/three.min.js"></script>
<script src="js/DRACOLoader.js"></script>
<script src="js/draco_decoder.js"></script>
<script src="js/OrbitControls.js"></script>
```

初始化three,js的场景、镜头、渲染器等

```javascript
<script>
    'use strict';
    let camera, cameraTarget, scene, renderer;

    function threejsInit() {
        let container = document.createElement('div');
        document.body.appendChild(container);

        //创建镜头
        camera = new THREE.PerspectiveCamera(45, window.innerWidth / window.innerHeight, 0.01, 1000);
        camera.position.set(3, 0.15, 3);

        //指定镜头朝向
        cameraTarget = new THREE.Vector3(0, 0, 0);
        camera.lookAt(cameraTarget);

        //创建场景
        scene = new THREE.Scene();

        //用黑雾充当黑色背景
        scene.fog = new THREE.Fog(0x000000, 2, 15);

        // 添加两个光源，一个黄、一个白
        scene.add(new THREE.HemisphereLight(0x443333, 0x111122));
        addShadowedLight(1, 1, 1, 0xffffff, 1.35);
        addShadowedLight(0.5, 1, -1, 0xffaa00, 1);

        //创建相机控制
        var controls = new THREE.OrbitControls(camera);
        controls.addEventListener('change', render);

        // 创建渲染器renderer
        renderer = new THREE.WebGLRenderer({antialias: true});
        renderer.setClearColor(scene.fog.color);
        renderer.setPixelRatio(window.devicePixelRatio);
        renderer.setSize(window.innerWidth, window.innerHeight);
        container.appendChild(renderer.domElement);
        window.addEventListener('resize', onWindowResize, false);
    }
```

监听

```javascript
    //监听浏览器窗口大小的变化，从而改变绘制区域
    function onWindowResize() {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
    }

    //刷新每一帧
    function threejsAnimate() {
        requestAnimationFrame(threejsAnimate);
        render();
    }

    function render() {
        renderer.render(scene, camera);
    }
```

两个供其他部分调用的方法

```javascript
    //添加光源
    function addShadowedLight(x, y, z, color, intensity) {
        const directionalLight = new THREE.DirectionalLight(color, intensity);
        directionalLight.position.set(x, y, z);
        scene.add(directionalLight);
    }

    //缩放模型至合适大小、移动模型至合适位置
    function resizeGeometry(bufferGeometry, material) {
        let geometry;
        // Point cloud does not have face indices.
        if (bufferGeometry.index == null) {
            geometry = new THREE.Points(bufferGeometry, material);
        } else {
            bufferGeometry.computeVertexNormals();
            geometry = new THREE.Mesh(bufferGeometry, material);
        }
        // Compute range of the geometry coordinates for proper rendering.
        bufferGeometry.computeBoundingBox();
        const sizeX = bufferGeometry.boundingBox.max.x - bufferGeometry.boundingBox.min.x;
        const sizeY = bufferGeometry.boundingBox.max.y - bufferGeometry.boundingBox.min.y;
        const sizeZ = bufferGeometry.boundingBox.max.z - bufferGeometry.boundingBox.min.z;
        const diagonalSize = Math.sqrt(sizeX * sizeX + sizeY * sizeY + sizeZ * sizeZ);
        const scale = 1.0 / diagonalSize;
        const midX =
            (bufferGeometry.boundingBox.min.x + bufferGeometry.boundingBox.max.x) / 2;
        const midY =
            (bufferGeometry.boundingBox.min.y + bufferGeometry.boundingBox.max.y) / 2;
        const midZ =
            (bufferGeometry.boundingBox.min.z + bufferGeometry.boundingBox.max.z) / 2;

        geometry.scale.multiplyScalar(scale);
        geometry.position.x = -midX * scale;
        geometry.position.y = -midY * scale;
        geometry.position.z = -midZ * scale;
        geometry.castShadow = true;
        geometry.receiveShadow = true;
        return geometry;
    }
```

创建draco解码器

```javascript
    // Global Draco decoder type.
    let dracoDecoderType = {};
    let dracoLoader;

    function createDracoDecoder() {
        dracoLoader = new THREE.DRACOLoader();
        dracoLoader.setDracoDecoderType(dracoDecoderType);
    }

    createDracoDecoder();

```

downloadEncodedMesh()用来下载.drc，onDecode()在下载后调用

```javascript
 // bufferGeometry is a geometry decoded by DRACOLoader.js
    function onDecode(bufferGeometry) {
        const material = new THREE.MeshStandardMaterial({vertexColors: THREE.VertexColors});

        const geometry = resizeGeometry(bufferGeometry, material);

        const selectedObject = scene.getObjectByName("my_mesh");
        scene.remove(selectedObject);
        geometry.name = "my_mesh";
        scene.add(geometry);
    }

    // Download and decode the Draco encoded geometry.
    function downloadEncodedMesh(filename) {
        // Download the encoded file.
        const xhr = new XMLHttpRequest();
        xhr.open("GET", filename, true);
        xhr.responseType = "arraybuffer";

        xhr.onload = function (event) {
            const arrayBuffer = xhr.response;
            if (arrayBuffer) {
                dracoLoader.setVerbosity(1);
                dracoLoader.decodeDracoFile(arrayBuffer, onDecode);
            }
        };

        xhr.send(null);
    }
```

整个示例开始工作的入口

```javascript
    window.onload = function () {
        const fileInput = document.getElementById('fileInput');
        fileInput.onclick = function () {
            this.value = '';
        }

        fileInput.addEventListener('change', function (e) {
            const file = fileInput.files[0];
            console.log(file);

            const reader = new FileReader();
            reader.onload = function (e) {
                // Enable logging to console output.
                dracoLoader.setVerbosity(1);
                dracoLoader.decodeDracoFile(reader.result, onDecode);
            }
            reader.readAsArrayBuffer(file);
        });


        threejsInit();
        threejsAnimate();

        //自动加载一个示例模型test.drc
        downloadEncodedMesh('test.drc');
    }
</script>
```

页面

```javascript
<body>
<div id="page-wrapper">
    <h1>Open a draco compressed file (.drc):</h1>
    <div>
        <input type="file" id="fileInput">
    </div>
</div>
</body>
</html>
```