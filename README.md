<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>我的AI作品集 | 自主搭建展示平台</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "Microsoft YaHei", sans-serif;
            scroll-behavior: smooth;
        }

        /* 顶部导航（固定，滚动不消失） */
        nav {
            background: #111;
            color: white;
            padding: 15px 30px;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 999;
            box-shadow: 0 2px 10px rgba(0,0,0,0.2);
        }
        .nav-container {
            max-width: 1200px;
            margin: auto;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .nav-logo {
            font-size: 18px;
            font-weight: bold;
            color: #00d1ff;
        }
        .nav-menu a {
            color: white;
            margin-left: 20px;
            text-decoration: none;
            font-size: 16px;
            transition: 0.3s;
        }
        .nav-menu a:hover {
            color: #00d1ff;
            text-decoration: underline;
        }

        /* 页面主体（避开导航栏，适配所有设备） */
        .container {
            max-width: 1200px;
            margin: 100px auto 80px;
            padding: 0 20px;
        }

        /* 标题样式（统一风格，突出层级） */
        .section-title {
            font-size: 28px;
            margin: 60px 0 25px;
            color: #222;
            border-left: 5px solid #00d1ff;
            padding-left: 15px;
            font-weight: bold;
        }
        .section-subtitle {
            font-size: 16px;
            color: #666;
            margin-bottom: 30px;
        }

        /* 个人介绍（突出AI身份） */
        .intro {
            background: #f5fafe;
            padding: 30px;
            border-radius: 12px;
            line-height: 1.8;
            font-size: 17px;
            border-left: 5px solid #0066ff;
            margin-bottom: 20px;
        }
        .intro strong {
            color: #0066ff;
        }

        /* 海报/图片作品（图片墙，hover放大，适配手机） */
        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        .gallery-item {
            position: relative;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            transition: 0.3s;
        }
        .gallery-item:hover {
            transform: scale(1.03);
            box-shadow: 0 5px 15px rgba(0,0,0,0.15);
        }
        .gallery-item img {
            width: 100%;
            height: 250px;
            object-fit: cover;
            display: block;
        }
        .gallery-desc {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            background: rgba(0,0,0,0.6);
            color: white;
            padding: 10px;
            font-size: 14px;
        }

        /* 视频模块（自适应大小，带封面感） */
        .video-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }
        .video-card {
            background: white;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0,0,0,0.1);
            overflow: hidden;
        }
        .video-card video {
            width: 100%;
            height: 200px;
            object-fit: cover;
            border-bottom: 1px solid #eee;
        }
        .video-desc {
            padding: 15px;
            font-size: 15px;
            color: #333;
        }

        /* 文章模块（卡片式，清晰易读） */
        .article-list {
            margin-top: 20px;
        }
        .article-card {
            background: white;
            padding: 25px;
            border-radius: 10px;
            margin-bottom: 20px;
            line-height: 1.7;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
            transition: 0.3s;
        }
        .article-card:hover {
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        .article-card h3 {
            color: #0066ff;
            margin-bottom: 10px;
            font-size: 20px;
        }
        .article-card p {
            color: #444;
            font-size: 16px;
        }

        /* AI能力展示（重点突出，视觉冲击强） */
        .ai-box {
            background: linear-gradient(90deg, #0066ff, #00d1ff);
            color: white;
            padding: 40px;
            border-radius: 12px;
            margin: 30px 0;
            box-shadow: 0 5px 20px rgba(0,102,255,0.3);
        }
        .ai-box h3 {
            font-size: 24px;
            margin-bottom: 20px;
            text-align: center;
        }
        .ai-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
        }
        .ai-item {
            background: rgba(255,255,255,0.1);
            padding: 15px;
            border-radius: 8px;
            font-size: 16px;
        }
        .ai-item:before {
            content: "✅";
            margin-right: 8px;
            color: #fff;
        }

        /* 底部联系方式（简洁明了） */
        .footer {
            background: #111;
            color: white;
            padding: 30px;
            text-align: center;
            margin-top: 50px;
            border-radius: 8px 8px 0 0;
        }
        .footer p {
            margin: 5px 0;
            font-size: 16px;
        }
        .footer a {
            color: #00d1ff;
            text-decoration: none;
        }

        /* 响应式适配（手机端优化） */
        @media (max-width: 768px) {
            .nav-container {
                flex-direction: column;
                gap: 10px;
            }
            .nav-menu a {
                margin: 0 10px;
            }
            .container {
                margin-top: 120px;
            }
            .video-grid {
                grid-template-columns: 1fr;
            }
            .video-card video {
                height: 180px;
            }
            .section-title {
                font-size: 24px;
            }
        }
    </style>
</head>

<body>

<!-- 导航栏（快速跳转各模块） -->
<nav>
    <div class="nav-container">
        <div class="nav-logo">AI作品集 | 自主搭建</div>
        <div class="nav-menu">
            <a href="#intro">个人介绍</a>
            <a href="#poster">海报作品</a>
            <a href="#video">短视频</a>
            <a href="#article">文章作品</a>
            <a href="#ai">AI能力</a>
            <a href="#contact">联系方式</a>
        </div>
    </div>
</nav>

<!-- 主体内容（分块展示，清晰有序） -->
<div class="container">

    <!-- 个人介绍（突出AI搭建能力） -->
    <div id="intro" class="section-title">个人介绍</div>
    <p class="section-subtitle">专注AI创作与前端搭建，自主完成本作品集网页开发</p>
    <div class="intro">
        大家好！我擅长利用AI工具完成海报设计、短视频生成、文案创作，同时具备独立前端搭建能力，本作品集网页全程自主开发、无需第三方模板，完美整合AI创作与前端技术，实现作品分块展示、多设备适配。所有展示作品均为本人原创（含AI辅助创作），欢迎浏览指导，期待与您交流合作。
    </div>

    <!-- 海报/图片作品（分块展示，带描述） -->
    <div id="poster" class="section-title">AI海报 / 设计作品</div>
    <p class="section-subtitle">AI辅助设计，涵盖创意海报、视觉设计等作品</p>
    <div class="gallery">
        <div class="gallery-item">
            <img src="替换为你的海报1地址.jpg" alt="AI创意海报1">
            <div class="gallery-desc">AI创意海报 | 主题：科技简约</div>
        </div>
        <div class="gallery-item">
            <img src="替换为你的海报2地址.jpg" alt="AI创意海报2">
            <div class="gallery-desc">AI创意海报 | 主题：潮流视觉</div>
        </div>
        <div class="gallery-item">
            <img src="替换为你的设计1地址.jpg" alt="AI设计作品1">
            <div class="gallery-desc">AI设计作品 | 主题：品牌视觉</div>
        </div>
        <div class="gallery-item">
            <img src="替换为你的设计2地址.jpg" alt="AI设计作品2">
            <div class="gallery-desc">AI设计作品 | 主题：极简风格</div>
        </div>
        <!-- 可自行添加更多图片：复制上面的div，修改地址和描述即可 -->
    </div>

    <!-- 短视频作品（带描述，支持播放） -->
    <div id="video" class="section-title">AI短视频作品</div>
    <p class="section-subtitle">AI生成+剪辑，涵盖创意短视频、作品演示等内容</p>
    <div class="video-grid">
        <div class="video-card">
            <video controls src="替换为你的视频1地址.mp4" poster="替换为视频1封面地址.jpg"></video>
            <div class="video-desc">AI短视频 | 主题：作品演示（AI生成+自主剪辑）</div>
        </div>
        <div class="video-card">
            <video controls src="替换为你的视频2地址.mp4" poster="替换为视频2封面地址.jpg"></video>
            <div class="video-desc">AI短视频 | 主题：创意展示（AI脚本+AI配音）</div>
        </div>
        <!-- 可自行添加更多视频：复制上面的div，修改地址和描述即可 -->
    </div>

    <!-- 文章作品（卡片式，清晰易读） -->
    <div id="article" class="section-title">文章 / 文案作品</div>
    <p class="section-subtitle">AI辅助创作，涵盖文案、文章、创作心得等内容</p>
    <div class="article-list">
        <div class="article-card">
            <h3>作品标题1：AI设计工具使用心得与技巧</h3>
            <p>替换为你的文章内容，可详细介绍AI设计的思路、工具使用方法、创作过程中的技巧，体现你的AI应用能力。内容可根据实际作品调整，确保真实、有深度，突出AI辅助创作的优势，同时展现个人思考与总结。</p>
        </div>
        <div class="article-card">
            <h3>作品标题2：AI短视频创作全流程解析</h3>
            <p>替换为你的文章内容，可介绍AI短视频的脚本生成、素材制作、剪辑优化等全流程，结合自己的作品案例，分享AI在短视频创作中的应用经验，体现你的AI整合与实践能力。</p>
        </div>
        <!-- 可自行添加更多文章：复制上面的div，修改标题和内容即可 -->
    </div>

    <!-- AI能力展示（核心突出，视觉优先） -->
    <div id="ai" class="section-title">AI搭建与创作能力</div>
    <p class="section-subtitle">核心能力：AI创作 + 前端自主搭建，可独立完成作品创作与展示</p>
    <div class="ai-box">
        <h3>我的AI核心能力</h3>
        <div class="ai-list">
            <div class="ai-item">独立搭建前端网页（本作品集网页全程自主开发，无第三方模板）</div>
            <div class="ai-item">AI辅助海报、视觉设计，可快速生成创意作品并优化细节</div>
            <div class="ai-item">AI短视频创作，涵盖脚本生成、素材制作、配音剪辑全流程</div>
            <div class="ai-item">AI文案、文章创作，结合自身思路优化内容，提升创作效率</div>
            <div class="ai-item">具备AI工具与前端技术的整合能力，可自主完成作品展示系统搭建</div>
            <div class="ai-item">熟练运用各类AI创作工具，可根据需求灵活调整创作风格</div>
        </div>
    </div>

    <!-- 联系方式（方便他人联系） -->
    <div id="contact" class="section-title">联系方式</div>
    <div class="footer">
        <p>感谢浏览我的AI作品集 | 网页自主搭建，作品均为原创</p>
        <p>联系电话：替换为你的联系电话</p>
        <p>邮箱：替换为你的邮箱地址</p>
        <p>微信：替换为你的微信号（可选）</p>
    </div>

</div>

</body>
</html>
