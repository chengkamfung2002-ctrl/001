<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>互动学习中心</title>
    <style>
        :root {
            --primary: #4f46e5;
            --primary-hover: #4338ca;
            --bg: #f8fafc;
            --card-bg: #ffffff;
            --text: #0f172a;
            --text-light: #64748b;
            --success: #10b981;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            display: flex;
            min-height: 100vh;
        }

        /* 侧边导航栏样式 */
        nav {
            width: 280px;
            background-color: var(--card-bg);
            border-right: 1px solid #e2e8f0;
            padding: 2rem;
            display: flex;
            flex-direction: column;
            gap: 2rem;
        }

        .logo {
            font-size: 1.5rem;
            font-weight: 700;
            color: var(--primary);
        }

        .menu-item {
            padding: 0.75rem 1rem;
            border-radius: 0.5rem;
            cursor: pointer;
            color: var(--text-light);
            font-weight: 500;
            transition: all 0.2s;
        }

        .menu-item.active, .menu-item:hover {
            background-color: #f1f5f9;
            color: var(--primary);
        }

        /* 主内容区域 */
        main {
            flex: 1;
            padding: 3rem;
            max-width: 1000px;
        }

        .header {
            margin-bottom: 2rem;
        }

        .header h1 {
            font-size: 2.25rem;
            margin-bottom: 0.5rem;
        }

        /* 进度条 */
        .progress-container {
            background: var(--card-bg);
            padding: 1.5rem;
            border-radius: 1rem;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
            margin-bottom: 2rem;
        }

        .progress-bar-bg {
            background: #e2e8f0;
            height: 10px;
            border-radius: 5px;
            margin-top: 0.75rem;
            overflow: hidden;
        }

        .progress-bar-fill {
            background: var(--success);
            height: 100%;
            width: 0%;
            transition: width 0.4s ease;
        }

        /* 学习卡片 */
        .card {
            background: var(--card-bg);
            padding: 2.5rem;
            border-radius: 1rem;
            box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05);
            margin-bottom: 2rem;
        }

        .content-section {
            display: none;
        }

        .content-section.active {
            display: block;
        }

        .content-section h2 {
            margin-bottom: 1rem;
            color: var(--primary);
        }

        .content-section p {
            line-height: 1.7;
            color: var(--text-light);
            margin-bottom: 1.5rem;
        }

        /* 测验样式 */
        .quiz-option {
            display: block;
            width: 100%;
            padding: 1rem;
            background: #f8fafc;
            border: 2px solid #e2e8f0;
            border-radius: 0.5rem;
            margin-bottom: 0.75rem;
            text-align: left;
            cursor: pointer;
            font-size: 1rem;
            transition: border-color 0.2s;
        }

        .quiz-option:hover {
            border-color: var(--primary);
        }

        .feedback {
            margin-top: 1rem;
            font-weight: 600;
            display: none;
        }

        /* 按钮 */
        .btn {
            background-color: var(--primary);
            color: white;
            border: none;
            padding: 0.75rem 1.5rem;
            border-radius: 0.5rem;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
        }

        .btn:hover {
            background-color: var(--primary-hover);
        }
    </style>
</head>
<body>

    <!-- 侧边导航栏 -->
    <nav>
        <div class="logo">学海无涯 💡</div>
        <div class="menu">
            <div class="menu-item active" onclick="switchTab('lesson1')">1. 认识万维网</div>
            <div class="menu-item" onclick="switchTab('lesson2')">2. 什么是 HTML？</div>
            <div class="menu-item" onclick="switchTab('quiz-time')">3. 知识小测验</div>
        </div>
    </nav>

    <!-- 主内容 -->
    <main>
        <div class="header">
            <h1>欢迎来到学习中心！</h1>
            <p style="color: var(--text-light)">按照你自己的节奏，掌控学习进度。</p>
        </div>

        <!-- 动态进度条 -->
        <div class="progress-container">
            <span style="font-weight: 600;">当前模块学习进度：</span><span id="progress-text">0%</span>
            <div class="progress-bar-bg">
                <div class="progress-bar-fill" id="progress-fill"></div>
            </div>
        </div>

        <!-- 课程内容容器 -->
        <div class="card">
            
            <!-- 第一课 -->
            <div id="lesson1" class="content-section active">
                <h2>第一课：认识万维网 (Web)</h2>
                <p>万维网是一个由全球各地的计算机存储的、相互链接的数字化文件组成的庞大网络。当你打开 Chrome 或 Safari 等浏览器时，你实际上是在使用一种工具来读取这些文件。</p>
                <p>网站通过服务器传输到你的屏幕上，并由你的浏览器实时解析。准备好看看它们是如何构建了吗？</p>
                <button class="btn" onclick="completeStep(1, 'lesson2')">标记为已读并进入下一课</button>
            </div>

            <!-- 第二课 -->
            <div id="lesson2" class="content-section">
                <h2>第二课：什么是 HTML？</h2>
                <p>HTML 的全称是 <strong>HyperText Markup Language</strong>（超文本标记语言）。它是互联网上每一个网页的结构骨架。</p>
                <p>这就像盖房子：HTML 代表了房屋的木质框架和梁柱。没有它，文本、图片和按钮就不知道该在屏幕的什么地方安家！</p>
                <button class="btn" onclick="completeStep(2, 'quiz-time')">标记为已读并开始测验</button>
            </div>

            <!-- 互动测验 -->
            <div id="quiz-time" class="content-section">
                <h2>知识小测验</h2>
                <p>HTML 代表什么意思？</p>
                <button class="quiz-option" onclick="checkAnswer(false, this)">Hyperlinks Text Management Language</button>
                <button class="quiz-option" onclick="checkAnswer(true, this)">HyperText Markup Language</button>
                <button class="quiz-option" onclick="checkAnswer(false, this)">Home Tool Markup Language</button>
                
                <div id="quiz-feedback" class="feedback"></div>
            </div>

        </div>
    </main>

    <script>
        let completedSteps = new Set();
        const totalSteps = 3;

        function switchTab(sectionId) {
            // 隐藏所有内容区块
            document.querySelectorAll('.content-section').forEach(section => {
                section.classList.remove('active');
            });
            // 显示选中的区块
            document.getElementById(sectionId).classList.add('active');

            // 更新侧边栏高亮
            document.querySelectorAll('.menu-item').forEach(item => {
                item.classList.remove('active');
                if(item.getAttribute('onclick').includes(sectionId)) {
                    item.classList.add('active');
                }
            });
        }

        function completeStep(stepNumber, nextSectionId) {
            completedSteps.add(stepNumber);
            updateProgressBar();
            switchTab(nextSectionId);
        }

        function checkAnswer(isCorrect, element) {
            const feedback = document.getElementById('quiz-feedback');
            feedback.style.display = 'block';
            
            // 重置所有选项颜色
            document.querySelectorAll('.quiz-option').forEach(opt => opt.style.borderColor = '#e2e8f0');
            
            if(isCorrect) {
                feedback.innerText = "🎉 太棒了！回答完全正确。";
                feedback.style.color = "var(--success)";
                element.style.borderColor = "var(--success)";
                completedSteps.add(3);
                updateProgressBar();
            } else {
                feedback.innerText = "❌ 差一点点！再试一次吧。";
                feedback.style.color = "#ef4444";
                element.style.borderColor = "#ef4444";
            }
        }

        function updateProgressBar() {
            const percentage = Math.round((completedSteps.size / totalSteps) * 100);
            document.getElementById('progress-fill').style.width = percentage + '%';
            document.getElementById('progress-text').innerText = percentage + '%';
        }
    </script>
</body>
</html>
