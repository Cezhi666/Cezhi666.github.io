# Cezhi666.github.io
None
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>浪漫文字雨</title>
    <!-- 使用 Inter 字体和中文字体 -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@500;600&family=Noto+Sans+SC:wght@500&display=swap" rel="stylesheet">
    
    <style>
        body {
            /* 北极冰块水汽背景：
              使用多层渐变模拟冰块的质感和水汽的朦胧感。
              - 基础是浅冰蓝色 (#f0f8ff)
              - 叠加一个线性渐变来营造深度
              - 叠加两个径向渐变模拟高光和雾气
            */
            background-color: #f0f8ff;
            background-image: 
                radial-gradient(at 80% 20%, #ffffff 0%, transparent 50%),
                radial-gradient(at 20% 80%, #ffffff 0%, transparent 50%),
                linear-gradient(135deg, #e0f7fa 0%, #f0f8ff 50%, #d4eaf7 100%);
            min-height: 100vh;
            width: 100%;
            /* 关键：隐藏所有超出屏幕的元素 */
            overflow: hidden;
            margin: 0;
            padding: 0;
            /* 优先使用中文字体，然后是 Inter 字体 */
            font-family: "Inter", "Noto Sans SC", "Microsoft YaHei", "SimHei", sans-serif;
            position: relative; /* 为绝对定位的子元素提供锚点 */
        }

        /* 文字框的统一样式 */
        .danmaku-item {
            position: fixed; /* 使用 fixed 定位，使其相对于视口浮动 */
            /* 初始位置 (0,0)，将完全由 transform 控制 */
            top: 0;
            left: 0;
            
            /* 可爱的框样式 */
            padding: 10px 20px;
            border-radius: 50px; /* 药丸形状，非常可爱 */
            font-size: 1.2rem; /* 调整字体大小 */
            font-weight: 600; /* 字体加粗 */
            white-space: nowrap; /* 确保文字不换行 */
            
            /* 视觉效果 */
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1), 0 2px 5px rgba(0, 0, 0, 0.05);
            opacity: 0.95; /* 略微透明，增加层次感 */
            
            /* 性能优化：告诉浏览器这个元素的 transform 会频繁变化 */
            will-change: transform;
            
            /* 边框增加质感 */
            border-width: 2px;
            border-style: solid;
            z-index: 1; /* 设置z-index为1，确保在icon之下 */
        }

        /*
          马卡龙色系主题：
          每种颜色都包含背景色、文字颜色和边框色
        */

        /* 浅粉色 */
        .color-1 { 
            background-color: #FFD1DC; /* 浅粉红 */
            color: #5c3a47; /* 深粉褐 */
            border-color: #FFB6C1; /* 亮粉红 */
        }
        
        /* 淡蓝色 */
        .color-2 { 
            background-color: #BDE0FE; /* 淡天蓝 */
            color: #2a4a6b; /* 深石板蓝 */
            border-color: #A2CFFE; /* 较深的天蓝 */
        }
        
        /* 浅绿色 */
        .color-3 { 
            background-color: #C2F0C2; /* 淡薄荷绿 */
            color: #3b5c3b; /* 深绿 */
            border-color: #AADEAA; /* 较深的绿 */
        }
        
        /* 米黄色 */
        .color-4 { 
            background-color: #FFFACD; /* 柠檬雪纺 */
            color: #6b5a2a; /* 深褐 */
            border-color: #FAEBD7; /* 亚麻色 */
        }
        
        /* 浅紫色 */
        .color-5 { 
            background-color: #E6E6FA; /* 淡紫色 */
            color: #4b4b6b; /* 深石板蓝紫 */
            border-color: #D8BFD8; /* 蓟色 */
        }

        /* 居中的冰块图标 - 尺寸加大，完全不透明 */
        #ice-cube-icon {
            position: fixed;
            top: 50%;
            left: 50%;
            width: 150px; /* 增大尺寸 */
            height: 150px; /* 增大尺寸 */
            transform: translate(-50%, -50%);
            z-index: 100; /* z-index更高，确保在弹幕之上 */
            opacity: 1.0; /* 100% 不透明 */
            pointer-events: none; /* 确保图标不会捕获鼠标事件 */
        }

        /* 居中的开场信息 */
        #intro-message {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 3rem; /* 大字号，冲击力强 */
            font-weight: 800;
            padding: 20px 40px;
            border-radius: 20px;
            background-color: #FFD1DC; /* 浅粉色背景 */
            color: #5c3a47; /* 深粉色文字 */
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            opacity: 1; /* 初始完全可见 */
            /* 渐变过渡效果 */
            transition: opacity 2.5s ease-out; 
            z-index: 200; /* 确保在所有元素的最上层 */
            white-space: nowrap;
        }

        /* 右下角版权文字样式 */
        #copyright-text {
            position: fixed;
            bottom: 10px;
            right: 15px;
            color: #777; /* 柔和的灰色 */
            font-size: 0.9rem;
            font-weight: 500;
            z-index: 5; /* 略高于弹幕，确保可见 */
            opacity: 0.8;
        }
    </style>
</head>
<body>

    <!-- 居中的开场信息 -->
    <div id="intro-message">冰冰的策纸</div>

    <!-- 居中的冰块图标 SVG (更拟真、更具棱角和细节) -->
    <svg id="ice-cube-icon" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
        <!-- 冰块主体 - 底部 -->
        <polygon points="50,85 80,70 80,30 50,15" fill="#BDE0FE" stroke="#A2CFFE" stroke-width="2.5" opacity="0.9"/>
        <!-- 冰块主体 - 左侧 -->
        <polygon points="20,70 50,85 50,15 20,30" fill="#E0F7FA" stroke="#A2CFFE" stroke-width="2.5" opacity="0.9"/>
        <!-- 冰块主体 - 顶部 -->
        <polygon points="20,30 50,15 80,30 50,45" fill="#FFFFFF" stroke="#A2CFFE" stroke-width="2.5" opacity="1.0"/>
        
        <!-- 内部裂纹/高光线 -->
        <line x1="50" y1="15" x2="50" y2="85" stroke="white" stroke-width="1.5" opacity="0.8"/>
        <line x1="20" y1="30" x2="80" y2="30" stroke="white" stroke-width="1.5" opacity="0.5"/>
        <line x1="20" y1="70" x2="80" y2="70" stroke="white" stroke-width="1.5" opacity="0.5"/>
        
        <!-- 中央连接点 -->
        <circle cx="50" cy="45" r="3" fill="#FFFFFF" opacity="0.9"/>
    </svg>

    <!-- 右下角版权文字 -->
    <div id="copyright-text">@策纸</div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {

            // 文字内容库
            const texts = [
                "记得吃水果", "多喝水哦~", "天冷了，多穿衣服", "记得好好护肤",
                "我想你了", "想见面", "要相信自己奥", "你超棒的",
                "金榜题名", "别熬夜", "早点休息", "别太累啦，偶尔偷懒也好",
                "一切都会好起来的", "你是最棒的", "加油！", "爱你~", "MUA!",
                "今天也要开心呀", "好好吃饭", "注意休息", "保护好眼睛",
                "你很优秀", "你是我的光", "晚安，好梦"
            ];

            // 颜色样式库
            const colorClasses = ['color-1', 'color-2', 'color-3', 'color-4', 'color-5'];

            // 存储所有在屏幕上的文字对象
            let particles = [];
            
            // 最大同时存在的文字数量：30
            const MAX_PARTICLES = 30;
            // 冰块的固定尺寸 (必须匹配CSS)
            const ICE_CUBE_SIZE = 150;
            const ICE_HALF_SIZE = ICE_CUBE_SIZE / 2;

            const introMessage = document.getElementById('intro-message');


            // --- 辅助函数 ---
            // 1. 获取范围内的随机数
            function getRandom(min, max) {
                return Math.random() * (max - min) + min;
            }

            // 2. 从数组中随机获取一项
            function getRandomItem(arr) {
                return arr[Math.floor(Math.random() * arr.length)];
            }
            // --- 辅助函数结束 ---


            /**
             * 创建一个新的文字DOM元素并初始化其运动属性
             */
            function createDanmaku() {
                const el = document.createElement('div');
                el.className = 'danmaku-item';
                
                // 随机应用一种颜色
                el.classList.add(getRandomItem(colorClasses));
                
                // 随机选择一段文字
                el.textContent = getRandomItem(texts);
                
                // 添加到 body
                document.body.appendChild(el);

                // --- 初始化运动属性 ---
                const viewWidth = window.innerWidth;
                const viewHeight = window.innerHeight;

                let x, y, dx, dy;
                
                // 随机速度：加快到 (1.3, 2.6)
                const speed = getRandom(1.3, 2.6); 
                
                // 随机一个出发侧（0:上, 1:右, 2:下, 3:左）
                const startSide = Math.floor(Math.random() * 4);

                switch (startSide) {
                    case 0: // 从顶部出发
                        x = getRandom(0, viewWidth);
                        y = -100; // 初始位置在屏幕上方
                        dx = getRandom(-0.3, 0.3); // x轴上轻微漂移
                        dy = 1; // y轴上向下
                        break;
                    case 1: // 从右侧出发
                        x = viewWidth + 100; // 初始位置在屏幕右侧
                        y = getRandom(0, viewHeight);
                        dx = -1; // x轴上向左
                        dy = getRandom(-0.3, 0.3); // y轴上轻微漂移
                        break;
                    case 2: // 从底部出发
                        x = getRandom(0, viewWidth);
                        y = viewHeight + 100; // 初始位置在屏幕下方
                        dx = getRandom(-0.3, 0.3); // x轴上轻微漂移
                        dy = -1; // y轴上向上
                        break;
                    case 3: // 从左侧出发
                        x = -200; // 初始位置在屏幕左侧 (给-200的buffer)
                        y = getRandom(0, viewHeight);
                        dx = 1; // x轴上向右
                        dy = getRandom(-0.3, 0.3); // y轴上轻微漂移
                        break;
                }
                
                // 返回一个“粒子”对象
                return { el, x, y, dx, dy, speed };
            }

            /**
             * 动画循环：更新所有文字的位置
             */
            function animate() {
                const viewWidth = window.innerWidth;
                const viewHeight = window.innerHeight;
                
                // 冰块的碰撞区域中心点
                const iceX = viewWidth / 2;
                const iceY = viewHeight / 2;
                // 冰块的边界
                const iceLeft = iceX - ICE_HALF_SIZE;
                const iceRight = iceX + ICE_HALF_SIZE;
                const iceTop = iceY - ICE_HALF_SIZE;
                const iceBottom = iceY + ICE_HALF_SIZE;


                // 从后向前遍历，方便安全地删除元素
                for (let i = particles.length - 1; i >= 0; i--) {
                    const p = particles[i];

                    // 更新位置
                    p.x += p.dx * p.speed;
                    p.y += p.dy * p.speed;

                    // --- 碰撞检测与反弹 ---
                    const danmakuWidth = p.el.offsetWidth;
                    const danmakuHeight = p.el.offsetHeight;

                    // 弹幕中心坐标
                    const pxCenter = p.x + danmakuWidth / 2;
                    const pyCenter = p.y + danmakuHeight / 2;

                    // 检查碰撞 (矩形相交检测)
                    // 只有当弹幕中心点处于冰块范围内时，才进行反弹
                    const isColliding = pxCenter > iceLeft && pxCenter < iceRight && 
                                        pyCenter > iceTop && pyCenter < iceBottom;

                    if (isColliding) {
                        // 确定反弹方向以防止卡住：检查距离哪个边缘最近
                        const dLeft = Math.abs(pxCenter - iceLeft);
                        const dRight = Math.abs(pxCenter - iceRight);
                        const dTop = Math.abs(pyCenter - iceTop);
                        const dBottom = Math.abs(pyCenter - iceBottom);
                        
                        const minX = Math.min(dLeft, dRight);
                        const minY = Math.min(dTop, dBottom);
                        
                        // 优先反弹撞击最浅的轴（防止对角线穿透）
                        if (minX < minY) {
                            p.dx *= -1; // 水平反弹
                            // 将粒子稍微移出碰撞区，防止下一帧再次触发
                            if (p.dx > 0) p.x = iceRight + 1; 
                            else p.x = iceLeft - danmakuWidth - 1; 
                        } else {
                            p.dy *= -1; // 垂直反弹
                            // 将粒子稍微移出碰撞区
                            if (p.dy > 0) p.y = iceBottom + 1;
                            else p.y = iceTop - danmakuHeight - 1; 
                        }
                    }


                    // 应用 transform 实现平滑动画
                    p.el.style.transform = `translate(${p.x}px, ${p.y}px)`;

                    // --- 检查是否移出屏幕 ---
                    
                    // 检查边界 (增加 400px 的缓冲区)
                    const isOffScreen = p.x < -400 || p.x > viewWidth + 400 ||
                                        p.y < -400 || p.y > viewHeight + 400;

                    if (isOffScreen) {
                        // 1. 从DOM中移除元素
                        p.el.remove();
                        // 2. 从数组中移除对象
                        particles.splice(i, 1);
                    }
                }

                // 请求下一帧动画
                requestAnimationFrame(animate);
            }

            /**
             * 生成循环：定期创建新的文字
             */
            function spawn() {
                // 如果屏幕上的文字小于最大值，则创建新的
                if (particles.length < MAX_PARTICLES) {
                    particles.push(createDanmaku());
                }

                // 随机间隔 500ms 到 1200ms 再次调用 spawn
                setTimeout(spawn, getRandom(500, 1200));
            }

            /**
             * 启动弹幕系统
             */
            function startDanmakuSystem() {
                // 启动动画和生成循环
                animate();
                spawn();
                
                // 窗口大小改变时清空并重置，防止文字卡住
                window.addEventListener('resize', () => {
                    particles.forEach(p => p.el.remove());
                    particles = [];
                });
            }

            // 1. 初始延迟和渐隐
            // 1.5秒可见
            setTimeout(() => {
                // 2. 开始渐隐
                if (introMessage) {
                    introMessage.style.opacity = '0';
                }
            }, 1500); 

            // 1.5秒可见 + 2.5秒渐隐时间 (CSS transition) = 4秒后开始弹幕
            setTimeout(() => {
                // 3. 移除信息并启动弹幕
                if (introMessage) {
                    introMessage.remove();
                }
                startDanmakuSystem();
            }, 4000); 
        });
    </script>
</body>
</html>
