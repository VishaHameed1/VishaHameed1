<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Visha Hameed · 3D GitHub Profile</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,600;14..32,700;14..32,800&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: radial-gradient(circle at 20% 30%, #0a0c12, #020308);
            font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
            color: #f0f3fa;
            line-height: 1.5;
            padding: 2rem 1.5rem;
        }

        /* 3D perspective container */
        .perspective-wrapper {
            perspective: 1200px;
            max-width: 1400px;
            margin: 0 auto;
        }

        /* 3D card base */
        .card-3d {
            background: rgba(15, 20, 30, 0.65);
            backdrop-filter: blur(2px);
            border-radius: 2rem;
            border: 1px solid rgba(100, 150, 255, 0.2);
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.6), 0 0 0 1px rgba(255, 255, 255, 0.03) inset;
            transition: transform 0.25s ease, box-shadow 0.3s ease;
            transform-style: preserve-3d;
        }

        .card-3d:hover {
            transform: translateY(-6px) rotateX(1.5deg) rotateY(0.5deg);
            box-shadow: 0 35px 55px -18px black, 0 0 0 1px rgba(90, 180, 255, 0.3) inset;
        }

        /* text with 3D extrusion / depth */
        .text-3d {
            text-shadow: 0 1px 0 rgba(0,0,0,0.4), 0 2px 0 rgba(0,0,0,0.3), 0 4px 8px rgba(0,0,0,0.5);
            font-weight: 600;
            letter-spacing: -0.01em;
        }

        .glow-3d {
            text-shadow: 0 1px 2px black, 0 0 8px rgba(80, 150, 255, 0.4), 0 0 12px rgba(70, 130, 255, 0.2);
        }

        /* inline 3d badges - flat but 3D via box-shadow + subtle transform */
        .badge-3d {
            display: inline-flex;
            align-items: center;
            background: linear-gradient(135deg, #1e2a3a, #0f1722);
            padding: 0.45rem 1rem;
            border-radius: 40px;
            font-weight: 500;
            font-size: 0.85rem;
            letter-spacing: -0.2px;
            transition: all 0.2s;
            box-shadow: 0 8px 14px -8px rgba(0, 0, 0, 0.5), inset 0 1px 0 rgba(255,255,255,0.05);
            border: 0.5px solid rgba(90, 150, 255, 0.3);
        }

        .badge-3d:hover {
            transform: translateY(-2px) scale(1.02);
            box-shadow: 0 12px 20px -10px black;
            border-color: rgba(120, 170, 255, 0.6);
        }

        /* 3D stat cards (GitHub stats) */
        .stat-card-3d {
            background: rgba(12, 18, 28, 0.7);
            backdrop-filter: blur(4px);
            border-radius: 1.5rem;
            padding: 1rem;
            transition: all 0.2s cubic-bezier(0.2, 0.9, 0.4, 1.1);
            border: 1px solid rgba(70, 130, 255, 0.2);
            box-shadow: 0 20px 30px -15px rgba(0, 0, 0, 0.5);
            transform-style: preserve-3d;
        }

        .stat-card-3d:hover {
            transform: translateY(-5px) rotateX(2deg);
            border-color: #3b82f680;
            box-shadow: 0 25px 35px -18px #000000cc;
        }

        /* project row 3d elements */
        .project-item {
            background: linear-gradient(105deg, rgba(20, 28, 40, 0.7), rgba(10, 15, 25, 0.8));
            border-radius: 1.25rem;
            padding: 1rem 1.2rem;
            margin-bottom: 1rem;
            transition: all 0.2s;
            border-left: 3px solid #3b82f6;
            box-shadow: 0 10px 20px -10px rgba(0, 0, 0, 0.4);
            transform: translateZ(5px);
        }

        .project-item:hover {
            transform: translateX(8px) translateZ(8px);
            background: rgba(30, 45, 70, 0.8);
            border-left-width: 6px;
        }

        /* code block 3d */
        .code-block {
            background: #0a0e17;
            border-radius: 1.2rem;
            padding: 1.2rem;
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.85rem;
            box-shadow: 0 12px 22px -12px black, inset 0 0 0 1px #2a3748;
            border-bottom: 2px solid #2c3e66;
        }

        /* typing SVG wrapper (keep original but surround with 3D container) */
        .typing-3d-wrap {
            filter: drop-shadow(0 8px 12px rgba(0, 0, 0, 0.6));
            transform: translateZ(15px);
        }

        hr {
            margin: 2rem 0;
            border: none;
            height: 2px;
            background: linear-gradient(90deg, transparent, #3b82f6, #a855f7, transparent);
            box-shadow: 0 2px 8px #3b82f620;
        }

        /* headers extrude */
        h1, h2, h3 {
            text-shadow: 0 2px 3px rgba(0,0,0,0.5), 0 6px 12px rgba(0,0,0,0.3);
            letter-spacing: -0.02em;
        }

        h2 {
            font-size: 1.9rem;
            margin: 1rem 0 1rem 0;
            display: inline-block;
            background: linear-gradient(135deg, #fff, #b9d0ff);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: none;
        }

        a {
            color: #74b9ff;
            text-decoration: none;
            font-weight: 500;
            transition: all 0.2s;
            text-shadow: 0 1px 1px black;
        }

        a:hover {
            color: white;
            text-shadow: 0 0 4px #3b82f6;
        }

        /* metrics layout */
        .flex-stats {
            display: flex;
            flex-wrap: wrap;
            gap: 1.2rem;
            justify-content: center;
            margin: 1.8rem 0;
        }

        .flex-stats > * {
            flex: 1;
            min-width: 260px;
        }

        .grid-projects {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
            gap: 1.4rem;
            margin-top: 1rem;
        }

        .badge-stack {
            display: flex;
            flex-wrap: wrap;
            gap: 0.7rem;
            justify-content: center;
            margin: 1.5rem 0;
        }

        /* 3D progress-like time distribution */
        .time-bar {
            background: #10141f;
            border-radius: 60px;
            overflow: hidden;
            margin: 8px 0;
            box-shadow: inset 0 1px 3px #00000055, 0 1px 1px #ffffff10;
        }
        .time-fill {
            padding: 0.5rem 0.8rem;
            background: linear-gradient(90deg, #2b5f8a, #3b82f6);
            border-radius: 60px;
            width: 0%;
            font-weight: bold;
            text-shadow: 0 1px 2px black;
            box-shadow: 2px 0 6px rgba(0,0,0,0.3);
        }

        footer {
            text-align: center;
            margin-top: 3rem;
            opacity: 0.85;
        }

        @media (max-width: 700px) {
            body {
                padding: 1rem;
            }
            .badge-3d {
                padding: 0.3rem 0.8rem;
                font-size: 0.7rem;
            }
        }

        .pill-icon {
            display: inline-block;
            margin-right: 6px;
        }

        .glow-text {
            text-shadow: 0 0 5px #3b82f6, 0 2px 6px black;
        }
    </style>
</head>
<body>
<div class="perspective-wrapper">
    <!-- header typing SVG: original image, but wrapped in 3D container for depth -->
    <div class="typing-3d-wrap" style="text-align: center; margin-bottom: 1rem;">
        <img src="https://readme-typing-svg.demolab.com/?lines=🚀+AI/ML+Engineer+🚀;💻+Full+Stack+Developer+💻;🎯+Computer+Vision+Specialist;🤖+Gemini+2.5+Practitioner;✨+25%2B+Projects+Completed;🌟+Code+is+My+Superpower+🌟&center=true&width=700&height=45&vCenter=true&pause=1000&size=22" alt="Typing SVG" style="display: inline-block; max-width: 100%; filter: drop-shadow(0 4px 10px #00000066);">
    </div>

    <!-- profile views & counters with 3D badges -->
    <div style="text-align: center; margin: 15px 0 25px 0;">
        <span class="badge-3d"><span class="pill-icon">👁️</span> <img src="https://komarev.com/ghpvc/?username=VishaHameed1&label=Profile+Views&color=FF6B6B&style=flat-square" style="height:20px; display:inline-block; vertical-align:middle; margin-left:5px;"></span>
        <span class="badge-3d" style="margin-left: 10px;"><span class="pill-icon">👥</span> <img src="https://img.shields.io/github/followers/VishaHameed1?label=Followers&style=flat-square&color=4ECDC4" style="height:20px; display:inline-block; vertical-align:middle;"></span>
        <span class="badge-3d"><span class="pill-icon">⭐</span> <img src="https://img.shields.io/github/stars/VishaHameed1?label=Total+Stars&style=flat-square&color=FFE66D" style="height:20px;"></span>
    </div>

    <!-- About Me section -->
    <div class="card-3d" style="padding: 1.8rem 2rem; margin-bottom: 2rem;">
        <h1 class="text-3d" style="font-size: 2.8rem; background: linear-gradient(135deg, #ffffff, #98b9ff); -webkit-background-clip: text; background-clip: text; color: transparent; display: inline-block;">✨ Hi, I'm Visha Hameed! ✨</h1>
        <div style="margin-top: 1.2rem;">
            <div class="code-block" style="margin-top: 0.8rem;">
                <pre style="color:#b9e6ff; margin:0; font-family: 'JetBrains Mono', monospace; font-size: 0.85rem;">
class VishaHameed:
    def __init__(self):
        self.name = "Visha Hameed"
        self.location = "🌍 Pakistan"
        self.role = "AI/ML Engineer & Full Stack Developer"
        self.experience = "25+ Production Projects"
        self.mission = "Building intelligent solutions that make a difference"
        self.interests = ["🔬 Computer Vision", "🧠 Deep Learning", "💬 NLP", "🤖 LLMs"]
        self.current_focus = "Facial Emotion Recognition & Age Detection"
        self.tech_stack = ["Python", "C#", "PyTorch", "OpenCV", "Gemini 2.5", "React", "MERN"]
    
    def daily_motto(self):
        return "Code. Learn. Build. Repeat."
    
    def say_hi(self):
        return "Thanks for visiting my profile! 🚀"</pre>
            </div>
            <p class="glow-3d" style="margin-top: 1.2rem; font-style: italic; font-size: 1.1rem;">✨ "The best way to predict the future is to build it."</p>
        </div>
    </div>

    <!-- Tech Stack full of badges (original images replaced with 3d-like badges but keep img? I'll keep original img.shields but embed inside 3d containers for depth) -->
    <h2 class="text-3d" style="margin-top: 0.4rem;">🛠️ Tech Stack</h2>
    <div class="badge-stack">
        <span class="badge-3d"><img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" style="height:28px;"></span>
        <span class="badge-3d"><img src="https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white" style="height:28px;"></span>
        <span class="badge-3d"><img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" style="height:28px;"></span>
        <span class="badge-3d"><img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white" style="height:28px;"></span>
        <span class="badge-3d"><img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black" style="height:28px;"></span>
        <span class="badge-3d"><img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" style="height:28px;"></span>
        <span class="badge-3d"><img src="https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white" style="height:28px;"></span>
        <span class="badge-3d"><img src="https://img.shields.io/badge/Gemini-8E75B2?style=for-the-badge&logo=googlebard&logoColor=white" style="height:28px;"></span>
        <span class="badge-3d"><img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white" style="height:28px;"></span>
    </div>

    <!-- Featured projects 3d grid -->
    <h2>🚀 Featured Projects</h2>
    <div class="grid-projects">
        <div class="project-item"><strong>🔍 AiImageDetector</strong> · C#, ML.NET · <span style="color:#7bdff2;">88.67% accuracy</span> — Detecting AI-generated images <br><a href="#">[repo]</a></div>
        <div class="project-item"><strong>🎭 Facial Emotion Recognition</strong> · Python, OpenCV <br>Real-time emotion detection <br><a href="#">[GitHub]</a></div>
        <div class="project-item"><strong>📊 Age & Gender Detection</strong> · Python, OpenCV · Age range & gender prediction <br><a href="#">[code]</a></div>
        <div class="project-item"><strong>💳 Fraud Detection System</strong> · Python, ML · Anomaly detection for transactions <br><a href="#">[HexSoftwares]</a></div>
        <div class="project-item"><strong>🤖 AI Chatbot</strong> · Gemini 2.5, Python · Intelligent conversational AI <br><a href="#">[demo]</a></div>
        <div class="project-item"><strong>🏡 PropTrack-MERN</strong> · MERN Stack · Property tracking platform <br><a href="#">[frontend]</a></div>
    </div>

    <!-- GitHub Analytics section with 3D cards and original stats images but wrapped in 3d containers to give depth -->
    <h2>📊 GitHub Analytics (3D Enhanced)</h2>
    <div class="flex-stats">
        <div class="stat-card-3d"><img src="https://github-readme-stats.vercel.app/api?username=VishaHameed1&show_icons=true&theme=radical&hide_border=true&count_private=true&border_radius=10" width="100%" style="border-radius: 1rem;"></div>
        <div class="stat-card-3d"><img src="https://github-readme-streak-stats.herokuapp.com/?user=VishaHameed1&theme=radical&hide_border=true&border_radius=10" width="100%" style="border-radius: 1rem;"></div>
    </div>
    <div class="flex-stats">
        <div class="stat-card-3d"><img src="https://github-readme-stats.vercel.app/api/top-langs/?username=VishaHameed1&layout=compact&theme=radical&hide_border=true&langs_count=10&border_radius=10" width="100%"></div>
        <div class="stat-card-3d"><img src="https://github-profile-trophy.vercel.app/?username=VishaHameed1&theme=radical&no-frame=true&row=2&column=4&margin-w=15&margin-h=15" width="100%"></div>
    </div>
    <div style="text-align: center; margin-top: 1rem;">
        <div class="stat-card-3d" style="display: inline-block; width: auto; padding: 0.8rem 1.2rem;"><img src="https://github-profile-summary-cards.vercel.app/api/cards/profile-details?username=VishaHameed1&theme=radical" width="100%" style="max-width: 800px;"></div>
    </div>

    <!-- Contribution graph -->
    <h2>📈 Contribution Activity</h2>
    <div class="card-3d" style="padding: 1.2rem; margin: 1rem 0;">
        <img src="https://github-readme-activity-graph.vercel.app/graph?username=VishaHameed1&theme=rogue&hide_border=true&area=true" width="100%" style="border-radius: 1rem;">
    </div>

    <!-- Experience internships etc -->
    <div style="display: flex; flex-wrap: wrap; gap: 1.5rem; margin: 2rem 0;">
        <div class="stat-card-3d" style="flex:1">
            <h3 class="text-3d">🎯 Dual Internship</h3>
            <p><strong>DeveloperHub</strong> · ML Integration 🔄 Active</p>
            <p><strong>Hex Softwares</strong> · Computer Vision + Gemini AI (1 Month)</p>
        </div>
        <div class="stat-card-3d" style="flex:1">
            <h3 class="text-3d">✅ Completed Projects at Hex Softwares</h3>
            <ul style="margin-left: 1.2rem;">
                <li>🤖 AI Chatbot (Gemini 2.5 Flash)</li>
                <li>🎙️ Virtual Assistant</li>
                <li>🔍 Fraud Detection</li>
                <li>🎭 Facial Emotion Recognition</li>
                <li>👤 Face Detection System</li>
                <li>📊 Age & Gender Prediction</li>
                <li>🌟 Personality Prediction (OCEAN)</li>
            </ul>
        </div>
    </div>

    <!-- Time Distribution 3D -->
    <h2>⏰ Time Distribution</h2>
    <div class="card-3d" style="padding: 1.5rem;">
        <div><span>🐍 Python 8h 45m</span> <span style="float:right;">45.2%</span><div class="time-bar"><div class="time-fill" style="width:45.2%">45.2%</div></div></div>
        <div><span>🎯 C# 4h 30m</span> <span style="float:right;">23.1%</span><div class="time-bar"><div class="time-fill" style="width:23.1%">23.1%</div></div></div>
        <div><span>🌐 JavaScript 3h 15m</span> <span style="float:right;">16.8%</span><div class="time-bar"><div class="time-fill" style="width:16.8%">16.8%</div></div></div>
        <div><span>☕ Java 1h 45m</span> <span style="float:right;">9.0%</span><div class="time-bar"><div class="time-fill" style="width:9%">9.0%</div></div></div>
        <div><span>🔧 Other 1h 15m</span> <span style="float:right;">5.9%</span><div class="time-bar"><div class="time-fill" style="width:5.9%">5.9%</div></div></div>
    </div>

    <!-- Goals -->
    <h2>🎯 2026 Goals</h2>
    <div class="card-3d" style="padding: 1rem 1.8rem; margin-bottom: 1.5rem;">
        <ul style="list-style-type: none;">
            <li>🚀 <input type="checkbox" disabled> Contribute to 15+ open source projects</li>
            <li>🤖 <input type="checkbox" disabled> Build a production-grade LLM application</li>
            <li>⭐ <input type="checkbox" disabled> Achieve 500+ GitHub followers</li>
            <li>📜 <input type="checkbox" disabled> Complete Google's Advanced ML certification</li>
            <li>💼 <input type="checkbox" disabled> Launch a SaaS product</li>
            <li>✍️ <input type="checkbox" disabled> Write 25+ technical blog posts</li>
        </ul>
    </div>

    <!-- Connect with 3D badges + social icons -->
    <h2>🤝 Let's Connect</h2>
    <div class="badge-stack">
        <a href="#" class="badge-3d" style="background: #171f2e;">🐙 GitHub</a>
        <a href="#" class="badge-3d" style="background: #0a66c2;">🔗 LinkedIn</a>
        <a href="#" class="badge-3d" style="background: #ea4335;">📧 Gmail</a>
        <a href="#" class="badge-3d" style="background: #1da1f2;">🐦 Twitter</a>
        <a href="#" class="badge-3d" style="background: #20BEFF;">📊 Kaggle</a>
    </div>

    <!-- Recent activity block 3d -->
    <h2>📝 Recent Activity</h2>
    <div class="code-block" style="background: #0b0f18;">
        <ul style="margin-left: 1rem; color: #b8e1ff;">
            <li>🚀 Released <strong>Facial Emotion Recognition</strong> · <a href="#">repo</a></li>
            <li>🔧 Enhanced <strong>Age & Gender Detection</strong> · accuracy improved</li>
            <li>🎯 <strong>AiImageDetector</strong> achieved 88.67% accuracy milestone</li>
            <li>🛡️ Improved security in <strong>PropTrack-MERN</strong></li>
            <li>💬 Deployed <strong>AI Chatbot</strong> with Gemini 2.5</li>
        </ul>
    </div>

    <!-- Quote + footer with 3D typing -->
    <hr>
    <div style="text-align: center;">
        <p class="glow-3d" style="font-size: 1.2rem;">✨ "Code is poetry written in logic. Make every line count." ✨<br><b>- Visha Hameed</b></p>
        <div class="typing-3d-wrap" style="margin-top: 1rem;">
            <img src="https://readme-typing-svg.demolab.com/?lines=Happy+Coding!;Keep+Building!;Stay+Awesome!&center=true&width=400&height=30&size=18" alt="typing footer">
        </div>
        <div style="margin: 2rem 0 1rem;">
            <span class="badge-3d">🌟 Star my repos to support my work 🌟</span>
        </div>
    </div>

    <!-- wave image (capsule) but it's an image, we keep -->
    <div style="text-align: center; margin-top: 2rem;">
        <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=120&section=footer&animation=twinkling" width="100%" style="border-radius: 30px 30px 0 0; opacity: 0.9;">
    </div>
    <footer>✨ Visha Hameed · AI/ML Engineer · 3D Interactive Profile ✨</footer>
</div>
</body>
</html>
