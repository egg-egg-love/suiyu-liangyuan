
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>穗遇良缘</title>
    <!-- 引入优美的中文字体 -->
    <link href="https://fonts.googleapis.com/css2?family=Ma+Shan+Zheng&family=ZCOOL+XiaoWei&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body, html {
            width: 100%;
            height: 100%;
            overflow: hidden;
            background-color: #0d1117;
            font-family: 'ZCOOL XiaoWei', serif;
            color: #fff;
        }

        /* 全屏滚动容器 */
        .container {
            height: 100vh;
            overflow-y: scroll;
            scroll-snap-type: y mandatory;
            scroll-behavior: smooth;
            /* 隐藏滚动条 */
            -ms-overflow-style: none;
            scrollbar-width: none;
        }
        .container::-webkit-scrollbar {
            display: none;
        }

        /* 每一页的区块 */
        .section {
            position: relative;
            width: 100%;
            height: 100vh;
            scroll-snap-align: start;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
        }

        /* 背景图片设置 */
        .bg-img {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            object-fit: cover;
            z-index: -2;
            transition: transform 0.1s linear;
        }

        /* 图片上的暗色遮罩，让文字更清晰 */
        .overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(to bottom, rgba(0,0,0,0.3) 0%, rgba(13,17,23,0.8) 100%);
            z-index: -1;
        }

        /* 诗意文案 */
        .text-content {
            text-align: center;
            opacity: 0;
            transform: translateY(30px);
            transition: all 1s ease;
            padding: 20px;
            z-index: 10;
        }

        .section.active .text-content {
            opacity: 1;
            transform: translateY(0);
        }

        .title {
            font-family: 'Ma Shan Zheng', cursive;
            font-size: 3rem;
            color: #ffd7d7;
            text-shadow: 0 0 10px rgba(255, 255, 255, 0.5), 0 0 20px rgba(200, 0, 0, 0.5);
            letter-spacing: 5px;
            margin-bottom: 20px;
        }

        .subtitle {
            font-size: 1.2rem;
            color: #e0e0e0;
            line-height: 1.8;
            letter-spacing: 2px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.8);
        }

        /* 首页专属大字 */
        .main-title {
            font-size: 4.5rem;
            margin-bottom: 10px;
        }

        /* 提示向下滑动 */
        .scroll-hint {
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            font-size: 1rem;
            color: #ccc;
            animation: bounce 2s infinite;
            z-index: 10;
            letter-spacing: 2px;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0) translateX(-50%); }
            40% { transform: translateY(-15px) translateX(-50%); }
            60% { transform: translateY(-7px) translateX(-50%); }
        }

        /* 音乐播放按钮 */
        .music-btn {
            position: fixed;
            top: 20px;
            right: 20px;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background: rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 215, 215, 0.5);
            color: #ffd7d7;
            display: flex;
            justify-content: center;
            align-items: center;
            cursor: pointer;
            z-index: 100;
            transition: all 0.3s;
        }
        .music-btn:hover {
            background: rgba(200, 0, 0, 0.5);
        }
        .music-btn.playing {
            animation: rotate 3s linear infinite;
        }
        @keyframes rotate {
            from { transform: rotate(0deg); }
            to { transform: rotate(360deg); }
        }

        /* 飘雪/落花特效的Canvas */
        #particle-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events:
