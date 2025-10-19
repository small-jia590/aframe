<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>熊猫馆VR体验</title>
    <script src="https://aframe.io/releases/1.4.0/aframe.min.js"></script>
    <script src="https://unpkg.com/aframe-environment-component@1.3.0/dist/aframe-environment-component.min.js"></script>
    <script src="https://unpkg.com/aframe-extras@6.1.1/dist/aframe-extras.min.js"></script>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            font-family: 'Arial', sans-serif;
        }
        #ui-container {
            position: absolute;
            top: 20px;
            left: 20px;
            z-index: 1000;
            background: rgba(255, 255, 255, 0.8);
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
            max-width: 300px;
        }
        h1 {
            color: #2c5530;
            margin-top: 0;
        }
        .instructions {
            margin: 10px 0;
            line-height: 1.5;
        }
        .controls {
            margin-top: 15px;
            font-size: 14px;
        }
        .btn {
            background: #4CAF50;
            color: white;
            border: none;
            padding: 8px 15px;
            margin: 5px 5px 5px 0;
            border-radius: 4px;
            cursor: pointer;
        }
        .btn:hover {
            background: #45a049;
        }
        .vr-btn {
            background: #2196F3;
        }
        .vr-btn:hover {
            background: #0b7dda;
        }
        .mobile-controls {
            position: absolute;
            bottom: 20px;
            width: 100%;
            display: none;
            justify-content: center;
            z-index: 1000;
        }
        .joystick {
            width: 80px;
            height: 80px;
            background: rgba(255, 255, 255, 0.7);
            border-radius: 50%;
            margin: 0 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            touch-action: none;
        }
        @media (max-width: 768px) {
            #ui-container {
                max-width: 200px;
                font-size: 14px;
            }
            .mobile-controls {
                display: flex;
            }
        }
    </style>
</head>
<body>
    <div id="ui-container">
        <h1>熊猫馆VR体验</h1>
        <div class="instructions">
            <p>欢迎来到虚拟熊猫馆！您可以：</p>
            <ul>
                <li>使用鼠标拖动来环顾四周</li>
                <li>使用WASD键或方向键移动</li>
                <li>点击熊猫与它们互动</li>
                <li>点击竹子听到熊猫的声音</li>
            </ul>
        </div>
        <div class="controls">
            <button class="btn vr-btn" id="enter-vr">进入VR模式</button>
            <button class="btn" id="reset-view">重置视角</button>
        </div>
    </div>

    <div class="mobile-controls">
        <div class="joystick" id="move-joystick">移动</div>
        <div class="joystick" id="look-joystick">视角</div>
    </div>

    <a-scene 
        vr-mode-ui="enterVRButton: #enter-vr"
        cursor="rayOrigin: mouse"
        raycaster="objects: .clickable"
        loading-screen="enabled: false">
        
        <!-- 场景环境 -->
        <a-entity environment="preset: forest; lighting: none; shadow: false"></a-entity>
        
        <!-- 天空 -->
        <a-sky color="#87CEEB"></a-sky>
        
        <!-- 地面 -->
        <a-circle id="ground" position="0 0 0" rotation="-90 0 0" radius="30" color="#7EC850" shadow="receive: true"></a-circle>
        
        <!-- 熊猫馆建筑 -->
        <a-box id="panda-house" position="0 0.5 -5" width="10" height="3" depth="8" color="#F5F5DC" shadow="cast: true; receive: true">
            <a-box position="0 1.5 4" width="8" height="2" depth="0.2" color="#8B4513"></a-box>
            <a-box position="-4.5 1.5 0" width="0.2" height="2" depth="7" color="#8B4513"></a-box>
            <a-box position="4.5 1.5 0" width="0.2" height="2" depth="7" color="#8B4513"></a-box>
            <a-cylinder position="0 3.5 0" radius="5.5" height="0.5" color="#8B4513" open-ended="true"></a-cylinder>
        </a-box>
        
        <!-- 竹林 -->
        <a-entity id="bamboo-forest">
            <!-- 多棵竹子 -->
            <a-cylinder class="bamboo clickable" position="-8 1.5 -8" radius="0.2" height="5" color="#7CFC00" shadow="cast: true">
                <a-cone position="0 2.5 0" radius-bottom="1" radius-top="0" height="2" color="#228B22"></a-cone>
            </a-cylinder>
            <a-cylinder class="bamboo clickable" position="7 1.5 -10" radius="0.2" height="6" color="#7CFC00" shadow="cast: true">
                <a-cone position="0 3 0" radius-bottom="1.2" radius-top="0" height="2.5" color="#228B22"></a-cone>
            </a-cylinder>
            <a-cylinder class="bamboo clickable" position="-10 1.5 5" radius="0.2" height="4" color="#7CFC00" shadow="cast: true">
                <a-cone position="0 2 0" radius-bottom="0.8" radius-top="0" height="1.5" color="#228B22"></a-cone>
            </a-cylinder>
            <a-cylinder class="bamboo clickable" position="9 1.5 7" radius="0.2" height="5.5" color="#7CFC00" shadow="cast: true">
                <a-cone position="0 2.75 0" radius-bottom="1.1" radius-top="0" height="2.2" color="#228B22"></a-cone>
            </a-cylinder>
            <a-cylinder class="bamboo clickable" position="5 1.5 -5" radius="0.2" height="4.5" color="#7CFC00" shadow="cast: true">
                <a-cone position="0 2.25 0" radius-bottom="1" radius-top="0" height="1.8" color="#228B22"></a-cone>
            </a-cylinder>
        </a-entity>
        
        <!-- 熊猫模型1 - 坐着的熊猫 -->
        <a-entity class="panda clickable" id="panda1" position="-3 0.5 0" animation="property: rotation; to: 0 360 0; loop: true; dur: 20000">
            <!-- 身体 -->
            <a-sphere position="0 0.5 0" radius="0.5" color="white" shadow="cast: true"></a-sphere>
            <!-- 头 -->
            <a-sphere position="0 1.2 0.4" radius="0.4" color="white" shadow="cast: true">
                <!-- 耳朵 -->
                <a-sphere position="-0.2 0.3 0.1" radius="0.15" color="black"></a-sphere>
                <a-sphere position="0.2 0.3 0.1" radius="0.15" color="black"></a-sphere>
                <!-- 眼睛 -->
                <a-sphere position="-0.15 0.1 0.3" radius="0.05" color="black"></a-sphere>
                <a-sphere position="0.15 0.1 0.3" radius="0.05" color="black"></a-sphere>
                <!-- 眼斑 -->
                <a-sphere position="-0.15 0.1 0.25" radius="0.08" color="black"></a-sphere>
                <a-sphere position="0.15 0.1 0.25" radius="0.08" color="black"></a-sphere>
                <!-- 鼻子 -->
                <a-sphere position="0 0 0.4" radius="0.06" color="black"></a-sphere>
            </a-sphere>
            <!-- 四肢 -->
            <a-cylinder position="-0.3 0.2 0.2" radius="0.1" height="0.4" color="black" rotation="30 0 0"></a-cylinder>
            <a-cylinder position="0.3 0.2 0.2" radius="0.1" height="0.4" color="black" rotation="30 0 0"></a-cylinder>
            <a-cylinder position="-0.25 -0.1 -0.2" radius="0.1" height="0.4" color="black" rotation="-30 0 0"></a-cylinder>
            <a-cylinder position="0.25 -0.1 -0.2" radius="0.1" height="0.4" color="black" rotation="-30 0 0"></a-cylinder>
        </a-entity>
        
        <!-- 熊猫模型2 - 行走的熊猫 -->
        <a-entity class="panda clickable" id="panda2" position="3 0.5 -3">
            <!-- 身体 -->
            <a-sphere position="0 0.5 0" radius="0.5" color="white" shadow="cast: true"></a-sphere>
            <!-- 头 -->
            <a-sphere position="0 1.2 0.4" radius="0.4" color="white" shadow="cast: true">
                <!-- 耳朵 -->
                <a-sphere position="-0.2 0.3 0.1" radius="0.15" color="black"></a-sphere>
                <a-sphere position="0.2 0.3 0.1" radius="0.15" color="black"></a-sphere>
                <!-- 眼睛 -->
                <a-sphere position="-0.15 0.1 0.3" radius="0.05" color="black"></a-sphere>
                <a-sphere position="0.15 0.1 0.3" radius="0.05" color="black"></a-sphere>
                <!-- 眼斑 -->
                <a-sphere position="-0.15 0.1 0.25" radius="0.08" color="black"></a-sphere>
                <a-sphere position="0.15 0.1 0.25" radius="0.08" color="black"></a-sphere>
                <!-- 鼻子 -->
                <a-sphere position="0 0 0.4" radius="0.06" color="black"></a-sphere>
            </a-sphere>
            <!-- 四肢 -->
            <a-cylinder position="-0.3 0.1 0.2" radius="0.1" height="0.5" color="black" rotation="10 0 0"></a-cylinder>
            <a-cylinder position="0.3 0.3 0.2" radius="0.1" height="0.5" color="black" rotation="-10 0 0"></a-cylinder>
            <a-cylinder position="-0.25 -0.2 -0.2" radius="0.1" height="0.5" color="black" rotation="10 0 0"></a-cylinder>
            <a-cylinder position="0.25 0 -0.2" radius="0.1" height="0.5" color="black" rotation="-10 0 0"></a-cylinder>
        </a-entity>
        
        <!-- 熊猫模型3 - 吃竹子的熊猫 -->
        <a-entity class="panda clickable" id="panda3" position="0 0.5 3">
            <!-- 身体 -->
            <a-sphere position="0 0.5 0" radius="0.5" color="white" shadow="cast: true"></a-sphere>
            <!-- 头 -->
            <a-sphere position="0 1.2 0.4" radius="0.4" color="white" shadow="cast: true">
                <!-- 耳朵 -->
                <a-sphere position="-0.2 0.3 0.1" radius="0.15" color="black"></a-sphere>
                <a-sphere position="0.2 0.3 0.1" radius="0.15" color="black"></a-sphere>
                <!-- 眼睛 -->
                <a-sphere position="-0.15 0.1 0.3" radius="0.05" color="black"></a-sphere>
                <a-sphere position="0.15 0.1 0.3" radius="0.05" color="black"></a-sphere>
                <!-- 眼斑 -->
                <a-sphere position="-0.15 0.1 0.25" radius="0.08" color="black"></a-sphere>
                <a-sphere position="0.15 0.1 0.25" radius="0.08" color="black"></a-sphere>
                <!-- 鼻子 -->
                <a-sphere position="0 0 0.4" radius="0.06" color="black"></a-sphere>
            </a-sphere>
            <!-- 四肢 -->
            <a-cylinder position="-0.3 0.2 0.2" radius="0.1" height="0.4" color="black" rotation="30 0 0"></a-cylinder>
            <a-cylinder position="0.3 0.2 0.2" radius="0.1" height="0.4" color="black" rotation="30 0 0"></a-cylinder>
            <a-cylinder position="-0.25 -0.1 -0.2" radius="0.1" height="0.4" color="black" rotation="-30 0 0"></a-cylinder>
            <a-cylinder position="0.25 -0.1 -0.2" radius="0.1" height="0.4" color="black" rotation="-30 0 0"></a-cylinder>
            <!-- 竹子 -->
            <a-cylinder position="0.2 0.8 0.5" radius="0.03" height="1" color="#7CFC00" rotation="0 0 20"></a-cylinder>
        </a-entity>
        
        <!-- 玩家/相机 -->
        <a-entity id="player" movement-controls="fly: true">
            <a-entity id="camera" camera="active: true" position="0 1.6 0" look-controls wasd-controls="fly: true">
                <a-cursor id="cursor" 
                         animation__click="property: scale; from: 0.1 0.1 0.1; to: 1 1 1; easing: easeInCubic; dur: 150"
                         animation__fusing="property: scale; from: 1 1 1; to: 0.1 0.1 0.1; easing: easeInCubic; dur: 1500"
                         event-set__1="_event: mouseenter; color: springgreen"
                         event-set__2="_event: mouseleave; color: black"
                         fuse="true"
                         raycaster="objects: .clickable">
                </a-cursor>
            </a-entity>
        </a-entity>
        
        <!-- 环境音效 -->
        <a-sound src="https://cdn.aframe.io/basic-guide/audio/backgroundnoise.wav" autoplay="true" loop="true" volume="0.2"></a-sound>
    </a-scene>

    <script>
        // 添加交互功能
        document.addEventListener('DOMContentLoaded', function() {
            // 重置视角按钮
            document.getElementById('reset-view').addEventListener('click', function() {
                const camera = document.querySelector('#camera');
                camera.setAttribute('position', '0 1.6 0');
                camera.setAttribute('rotation', '0 0 0');
            });
            
            // 熊猫点击交互
            const pandas = document.querySelectorAll('.panda');
            pandas.forEach(function(panda) {
                panda.addEventListener('click', function() {
                    // 添加简单的动画效果
                    panda.setAttribute('animation', {
                        property: 'rotation',
                        to: '0 360 0',
                        dur: 2000,
                        easing: 'easeInOutQuad'
                    });
                    
                    // 重置动画
                    setTimeout(function() {
                        panda.removeAttribute('animation');
                    }, 2000);
                });
            });
            
            // 竹子点击交互
            const bamboos = document.querySelectorAll('.bamboo');
            bamboos.forEach(function(bamboo) {
                bamboo.addEventListener('click', function() {
                    // 添加简单的动画效果
                    bamboo.setAttribute('animation', {
                        property: 'scale',
                        from: '1 1 1',
                        to: '1.2 1.2 1.2',
                        dur: 500,
                        easing: 'easeInOutQuad'
                    });
                    
                    // 重置动画
                    setTimeout(function() {
                        bamboo.setAttribute('animation', {
                            property: 'scale',
                            to: '1 1 1',
                            dur: 500,
                            easing: 'easeInOutQuad'
                        });
                    }, 500);
                });
            });
            
            // 移动设备控制
            if (window.innerWidth <= 768) {
                initMobileControls();
            }
        });
        
        // 移动设备控制初始化
        function initMobileControls() {
            const moveJoystick = document.getElementById('move-joystick');
            const lookJoystick = document.getElementById('look-joystick');
            const player = document.getElementById('player');
            
            let moveTouchId = null;
            let lookTouchId = null;
            
            // 移动控制
            moveJoystick.addEventListener('touchstart', function(e) {
                e.preventDefault();
                moveTouchId = e.changedTouches[0].identifier;
            });
            
            moveJoystick.addEventListener('touchmove', function(e) {
                e.preventDefault();
                if (!moveTouchId) return;
                
                for (let i = 0; i < e.changedTouches.length; i++) {
                    const touch = e.changedTouches[i];
                    if (touch.identifier === moveTouchId) {
                        const rect = moveJoystick.getBoundingClientRect();
                        const centerX = rect.left + rect.width / 2;
                        const centerY = rect.top + rect.height / 2;
                        
                        const deltaX = touch.clientX - centerX;
                        const deltaY = touch.clientY - centerY;
                        
                        // 根据触摸位置移动玩家
                        const moveX = deltaX / 50;
                        const moveZ = -deltaY / 50;
                        
                        const position = player.getAttribute('position');
                        player.setAttribute('position', {
                            x: position.x + moveX,
                            y: position.y,
                            z: position.z + moveZ
                        });
                    }
                }
            });
            
            moveJoystick.addEventListener('touchend', function(e) {
                e.preventDefault();
                moveTouchId = null;
            });
            
            // 视角控制
            lookJoystick.addEventListener('touchstart', function(e) {
                e.preventDefault();
                lookTouchId = e.changedTouches[0].identifier;
            });
            
            lookJoystick.addEventListener('touchmove', function(e) {
                e.preventDefault();
                if (!lookTouchId) return;
                
                for (let i = 0; i < e.changedTouches.length; i++) {
                    const touch = e.changedTouches[i];
                    if (touch.identifier === lookTouchId) {
                        const rect = lookJoystick.getBoundingClientRect();
                        const centerX = rect.left + rect.width / 2;
                        const centerY = rect.top + rect.height / 2;
                        
                        const deltaX = touch.clientX - centerX;
                        const deltaY = touch.clientY - centerY;
                        
                        // 根据触摸位置旋转相机
                        const camera = document.querySelector('#camera');
                        const rotation = camera.getAttribute('rotation');
                        
                        camera.setAttribute('rotation', {
                            x: rotation.x - deltaY / 10,
                            y: rotation.y + deltaX / 10,
                            z: rotation.z
                        });
                    }
                }
            });
            
            lookJoystick.addEventListener('touchend', function(e) {
                e.preventDefault();
                lookTouchId = null;
            });
        }
    </script>
</body>
</html>
