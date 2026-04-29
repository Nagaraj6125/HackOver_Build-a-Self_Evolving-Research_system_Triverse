# 🤖 AI Research Assistant

A smart AI-based learning assistant that helps users understand key concepts in:

- DSA
- Photosynthesis
- Stress-sad, sadness
- Gravity
- Circle
- Statistics
- Engineering
- Machine Learning-ml
- Hello
- 

---

## 🚀 Features

- 💬 Chat mode for explanations  
- 🎯 Quiz mode for testing knowledge  
- 🧠 Visual mode for flowcharts  
- ⚡ Fast and interactive UI  

---

## 🛠️ Technologies Used

- HTML
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Adaptive AI Tutor - Pro Scholar</title>
    <style>
        :root {
            --primary: #4F46E5;
            --bg-dark: #1F2937;
            --bg-panel: #374151;
            --text-light: #F3F4F6;
            --text-dim: #9CA3AF;
            --xp-color: #10B981;
            --accent-gold: #FBBF24;
            --visual-box: #111827;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-dark);
            color: var(--text-light);
            margin: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .container {
            width: 100%;
            max-width: 650px;
            background: var(--bg-panel);
            border-radius: 12px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.5);
            overflow: hidden;
        }

        #login-screen { padding: 40px; text-align: center; }
        #login-screen input {
            width: 80%; padding: 12px; margin: 10px 0;
            border: none; border-radius: 6px;
            background: #4B5563; color: white;
            box-sizing: border-box;
        }

        button {
            background: var(--primary); color: white; border: none;
            padding: 12px 24px; border-radius: 6px;
            cursor: pointer; font-weight: bold; transition: 0.3s;
        }
        button:hover { background: #4338CA; }

        #chat-interface { display: none; flex-direction: column; height: 85vh; }

        .chat-header {
            background: #111827; padding: 15px 20px;
            display: flex; justify-content: space-between; align-items: center;
            border-bottom: 1px solid #4B5563;
        }
        .user-info h3 { margin: 0; font-size: 1.1rem; color: var(--primary); }
        .user-info span { font-size: 0.85rem; font-weight: bold; color: var(--accent-gold); }
        
        .xp-bar-container {
            width: 150px; background: #4B5563; border-radius: 10px;
            height: 8px; margin-top: 5px; overflow: hidden;
        }
        #xp-bar { height: 100%; background: var(--xp-color); width: 0%; transition: width 0.5s ease; }

        .mode-tabs { display: flex; background: #1F2937; }
        .mode-tab {
            flex: 1; padding: 12px; background: transparent;
            color: #9CA3AF; font-size: 0.9rem; border: none; cursor: pointer;
            border-bottom: 3px solid transparent;
        }
        .mode-tab.active { background: var(--bg-panel); color: white; border-bottom: 3px solid var(--primary); }

        #chat-box {
            flex: 1; padding: 20px; overflow-y: auto;
            display: flex; flex-direction: column; gap: 15px;
            background: #1f293780;
        }
        .msg { max-width: 90%; padding: 12px 16px; border-radius: 8px; line-height: 1.5; word-wrap: break-word; }
        .msg.user { background: var(--primary); align-self: flex-end; border-bottom-right-radius: 0; }
        .msg.ai { background: #4B5563; align-self: flex-start; border-bottom-left-radius: 0; border-left: 4px solid var(--primary); white-space: normal; }
        .msg.system { align-self: center; background: transparent; color: var(--accent-gold); font-size: 0.8rem; font-weight: bold; text-transform: uppercase; }

        .quiz-options { display: flex; flex-direction: column; gap: 8px; margin-top: 10px; }
        .quiz-btn {
            background: #374151; border: 1px solid #4B5563; color: white;
            padding: 8px; border-radius: 4px; text-align: left; cursor: pointer;
        }
        .quiz-btn:hover { background: #4B5563; }

        .input-area { display: flex; padding: 15px; background: #111827; gap: 10px; }
        .input-area input { flex: 1; padding: 12px; border: none; border-radius: 6px; background: #374151; color: white; }

        /* =========================================
           VISUALS: MINDMAP & FLOWCHART STYLES
           ========================================= */

        /* Main Mindmap Container */
        .mindmap-wrapper {
            display: flex;
            justify-content: center;
            overflow-x: auto;
            padding: 15px 0;
            width: 100%;
            background: var(--visual-box);
            border-radius: 8px;
            margin-top: 10px;
            border: 1px solid #374151;
        }

        .mindmap {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* Tree Structure using standard ul/li */
        .mindmap ul {
            padding-top: 20px; 
            position: relative;
            transition: all 0.5s;
            display: flex;
            justify-content: center;
            padding-left: 0;
            margin: 0;
        }

        .mindmap li {
            float: left; text-align: center;
            list-style-type: none;
            position: relative;
            padding: 20px 10px 0 10px;
            transition: all 0.5s;
        }

        /* Drawing connecting lines using pseudo-elements */
        .mindmap li::before, .mindmap li::after {
            content: '';
            position: absolute; top: 0; right: 50%;
            border-top: 2px solid var(--text-dim);
            width: 50%; height: 20px;
        }

        .mindmap li::after {
            right: auto; left: 50%;
            border-left: 2px solid var(--text-dim);
        }

        /* Cleanup extra lines for first and last child */
        .mindmap li:only-child::after, .mindmap li:only-child::before { display: none; }
        .mindmap li:only-child { padding-top: 0; }
        .mindmap li:first-child::before, .mindmap li:last-child::after { border: 0 none; }

        /* Connecting line to the bottom of parents */
        .mindmap li:first-child::after { border-radius: 8px 0 0 0; }
        .mindmap li:last-child::before { border-right: 2px solid var(--text-dim); border-radius: 0 8px 0 0; }

        .mindmap ul ul::before {
            content: '';
            position: absolute; top: 0; left: 50%;
            border-left: 2px solid var(--text-dim);
            width: 0; height: 20px;
        }

        /* Node Styling (Circles / Pills) */
        .mindmap-node {
            display: inline-block;
            background: var(--bg-dark);
            border: 2px solid var(--primary);
            color: var(--text-light);
            padding: 10px 15px;
            text-decoration: none;
            border-radius: 30px; 
            font-size: 0.85rem;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 6px rgba(0,0,0,0.3);
            position: relative;
            z-index: 1;
        }

        .mindmap-node:hover {
            background: var(--primary);
            color: white;
            box-shadow: 0 0 15px var(--primary);
            transform: scale(1.05);
        }

        /* Root Node Variation */
        .mindmap-node.root {
            border-color: var(--accent-gold);
            background: rgba(251, 191, 36, 0.1);
        }

        .mindmap-node.root:hover {
            background: var(--accent-gold);
            color: var(--bg-dark);
            box-shadow: 0 0 15px var(--accent-gold);
        }

        /* Linear Flowchart styles (Top to Bottom) */
        .flowchart {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 0;
            padding: 20px;
            background: var(--visual-box);
            border-radius: 8px;
            margin-top: 10px;
            border: 1px solid #374151;
        }

        .flow-arrow {
            width: 2px;
            height: 25px;
            background: var(--text-dim);
            position: relative;
            margin: 5px 0;
        }

        .flow-arrow::after {
            content: '';
            position: absolute;
            bottom: -4px;
            left: -4px;
            border-left: 5px solid transparent;
            border-right: 5px solid transparent;
            border-top: 5px solid var(--text-dim);
        }
    </style>
</head>
<body>

    <div class="container">
        <div id="login-screen">
            <h2>Scholar Alpha v1.0</h2>
            <p>Enter your credentials to access the Knowledge Base.</p>
            <input type="text" id="username" placeholder="Scholar Name" required>
            <input type="password" id="password" placeholder="Passcode">
            <br><br>
            <button onclick="login()">Initialize Session</button>
        </div>

        <div id="chat-interface">
            <div class="chat-header">
                <div class="user-info">
                    <h3 id="display-name">User</h3>
                    <span id="level-display">Lvl 1 Scholar</span>
                </div>
                <div>
                    <div style="font-size: 0.75rem; text-align: right;" id="xp-text">0 / 100 XP</div>
                    <div class="xp-bar-container"><div id="xp-bar"></div></div>
                </div>
            </div>

            <div class="mode-tabs">
                <button class="mode-tab active" onclick="setMode('text', this)">💬 Chat</button>
                <button class="mode-tab" onclick="setMode('quiz', this)">🎯 Quiz</button>
                <button class="mode-tab" onclick="setMode('visual', this)">🧠 Visuals</button>
            </div>

            <div id="chat-box"></div>

            <div class="input-area">
                <input type="text" id="user-input" placeholder="Try 'dsa' or 'web development'..." onkeypress="handleEnter(event)">
                <button onclick="sendMessage()">Send</button>
            </div>
        </div>
    </div>

    <script>
        let currentUser = "";
        let currentMode = "text";
        let userStats = { xp: 0, level: 1, topicCounts: {} };

        const topicDB = {
            "web development": {
                levels: [
                    `🟢 Beginner: Foundation\n- HTML5 Structure\n- CSS3 Styling\n- JS Fundamentals`,
                    `🟡 Intermediate: Logic\n- ES6+, DOM Manipulation\n- React/Vue Frameworks\n- REST APIs`,
                    `🔴 Advanced: Scaling\n- Microservices & Docker\n- Next.js & SEO\n- CI/CD Pipelines`
                ],
                quizzes: [
                    { q: "Which protocol is used for secure transfer?", options: ["HTTP", "HTTPS", "FTP"], correct: 1 }
                ],
                visualHTML: `
                <div class="mindmap-wrapper">
                    <div class="mindmap">
                        <ul>
                            <li>
                                <div class="mindmap-node root">Web Development</div>
                                <ul>
                                    <li>
                                        <div class="mindmap-node">Frontend</div>
                                        <ul>
                                            <li><div class="mindmap-node" style="border-color:#10B981">HTML / CSS</div></li>
                                            <li><div class="mindmap-node" style="border-color:#10B981">React / UI</div></li>
                                        </ul>
                                    </li>
                                    <li>
                                        <div class="mindmap-node">Backend</div>
                                        <ul>
                                            <li><div class="mindmap-node" style="border-color:#3B82F6">Node.js</div></li>
                                            <li>n<div class="mindmap-node" style="border-color:#3B82F6">Database</div></li>
                                        </ul>
                                    </li>
                                </ul>
                            </li>
                        </ul>
                    </div>
                </div>`
            },
            "dsa": {
                levels: [
                    `🟢 Beginner: Linear DS\n- Arrays & Strings\n- Linked Lists\n- Complexity (Big O)`,
                    `🟡 Intermediate: Hierarchical\n- Binary Trees\n- Recursion & Sorting\n- Hash Maps`,
                    `🔴 Advanced: Complex\n- Dynamic Programming\n- Graph Algorithms\n- Tries`
                ],
                quizzes: [
                    { q: "LIFO is associated with which structure?", options: ["Queue", "Stack", "Heap"], correct: 1 }
                ],
                visualHTML: `
                <div class="flowchart">
                    <div class="mindmap-node root">Raw Input Data</div>
                    <div class="flow-arrow"></div>
                    <div class="mindmap-node">Data Structure (Array/Tree)</div>
                    <div class="flow-arrow"></div>
                    <div class="mindmap-node">Algorithm (Sorting/Search)</div>
                    <div class="flow-arrow"></div>
                    <div class="mindmap-node" style="border-color: #10B981; background: rgba(16, 185, 129, 0.1);">Optimized Output</div>
                </div>`
            }
        };

        function login() {
            const user = document.getElementById('username').value.trim();
            if(!user) return alert("Enter Name.");
            currentUser = user;
            document.getElementById('display-name').innerText = currentUser;
            const saved = localStorage.getItem(`stats_${currentUser}`);
            if(saved) userStats = JSON.parse(saved);
            updateUI();
            document.getElementById('login-screen').style.display = 'none';
            document.getElementById('chat-interface').style.display = 'flex';
            addMessage("ai", `Welcome. Enter "DSA" or "Web Development" to begin.`);
        }

        function setMode(mode, btn) {
            currentMode = mode;
            document.querySelectorAll('.mode-tab').forEach(t => t.classList.remove('active'));
            btn.classList.add('active');
            addMessage("system", `Mode: ${mode.toUpperCase()}`);
        }

        function handleEnter(e) { if(e.key === 'Enter') sendMessage(); }

        function sendMessage() {
            const input = document.getElementById('user-input');
            const text = input.value.trim();
            if(!text) return;
            addMessage("user", text);
            input.value = '';
            setTimeout(() => generateAIResponse(text), 500);
        }

        function addMessage(sender, text, isSpecial = false, data = null) {
            const chatBox = document.getElementById('chat-box');
            const m = document.createElement('div');
            m.className = `msg ${sender}`;
            
            if (isSpecial && currentMode === 'visual') {
                m.innerHTML = `<strong style="display:block; margin-bottom: 10px; color: var(--accent-gold);">Architectural Flow:</strong>` + data;
            } else if (isSpecial && currentMode === 'quiz') {
                m.innerText = text;
                const optContainer = document.createElement('div');
                optContainer.className = 'quiz-options';
                data.options.forEach((opt, index) => {
                    const btn = document.createElement('button');
                    btn.className = 'quiz-btn';
                    btn.innerText = opt;
                    btn.onclick = () => checkAnswer(index, data.correct, optContainer);
                    optContainer.appendChild(btn);
                });
                m.appendChild(optContainer);
            } else {
                m.innerText = text;
            }

            chatBox.appendChild(m);
            chatBox.scrollTop = chatBox.scrollHeight;
        }

        function generateAIResponse(input) {
            const topic = input.toLowerCase();
            const data = topicDB[topic];

            if (!data) {
                addMessage("ai", `Topic "${input}" not found in current module. Try "DSA" or "Web Development".`);
                return;
            }

            if (currentMode === 'quiz') {
                const q = data.quizzes[0];
                addMessage("ai", q.q, true, q);
            } else if (currentMode === 'visual') {
                addMessage("ai", "", true, data.visualHTML);
                gainXP(10);
            } else {
                let count = userStats.topicCounts[topic] || 0;
                addMessage("ai", data.levels[Math.min(count, 2)]);
                userStats.topicCounts[topic] = count + 1;
                gainXP(20);
            }
        }

        function checkAnswer(sel, cor, cont) {
            if (sel === cor) {
                addMessage("system", "✅ CORRECT! +50 XP");
                gainXP(50);
            } else {
                addMessage("system", "❌ TRY AGAIN.");
            }
            cont.querySelectorAll('button').forEach(b => b.disabled = true);
        }

        function gainXP(amt) {
            userStats.xp += amt;
            if(userStats.xp >= 100) { userStats.level++; userStats.xp = 0; }
            updateUI();
            save();
        }

        function save() { localStorage.setItem(`stats_${currentUser}`, JSON.stringify(userStats)); }
        function updateUI() {
            document.getElementById('level-display').innerText = `Lvl ${userStats.level} Scholar`;
            document.getElementById('xp-text').innerText = `${userStats.xp} / 100 XP`;
            document.getElementById('xp-bar').style.width = `${userStats.xp}%`;
        }
    </script>
</body>
</html>
- CSS  
:root {
    --bg-dark: #0f172a;
    --panel: #1e293b;
    --accent-blue: #38bdf8;
    --accent-yellow: #fbbf24;
    --text-white: #f8fafc;
    --text-dim: #94a3b8;
}

body {
    background-color: var(--bg-dark);
    color: var(--text-white);
    font-family: 'Inter', system-ui, sans-serif;
    margin: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

.container { width: 100%; max-width: 500px; padding: 20px; }

/* Login Card */
.card {
    background: var(--panel);
    padding: 2rem;
    border-radius: 16px;
    border: 1px solid #334155;
    text-align: center;
    box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}

input {
    width: 100%;
    padding: 12px;
    margin: 10px 0;
    background: #0f172a;
    border: 1px solid #475569;
    color: white;
    border-radius: 8px;
    box-sizing: border-box;
}

button {
    background: var(--accent-blue);
    color: #0f172a;
    border: none;
    padding: 12px 24px;
    border-radius: 8px;
    font-weight: 800;
    cursor: pointer;
    transition: 0.3s;
}

button:hover { opacity: 0.9; transform: translateY(-1px); }

/* Chat Layout */
.chat-wrapper {
    background: var(--panel);
    border-radius: 16px;
    height: 85vh;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    border: 1px solid #334155;
}

header {
    padding: 1rem;
    background: #1e293b;
    border-bottom: 1px solid #334155;
}

.xp-bar {
    width: 100%;
    height: 6px;
    background: #0f172a;
    border-radius: 3px;
    margin: 10px 0;
}

#xp-fill {
    height: 100%;
    background: var(--accent-yellow);
    width: 0%;
    transition: 0.5s;
    box-shadow: 0 0 10px var(--accent-yellow);
}

.mode-tabs { display: flex; gap: 5px; margin-top: 10px; }

.tab {
    flex: 1;
    font-size: 0.75rem;
    background: #334155;
    color: white;
}

.tab.active { background: var(--accent-blue); color: #0f172a; }

.chat-messages {
    flex: 1;
    overflow-y: auto;
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.message { padding: 12px; border-radius: 12px; max-width: 85%; font-size: 0.95rem; line-height: 1.5; }
.ai { background: #334155; align-self: flex-start; border-bottom-left-radius: 2px; }
.user { background: var(--accent-blue); color: #0f172a; align-self: flex-end; border-bottom-right-radius: 2px; }
.system { font-size: 0.8rem; color: var(--accent-yellow); text-align: center; align-self: center; }

.input-group { padding: 1rem; display: flex; gap: 10px; background: #1e293b; }

/* =========================================
   VISUALS: MINDMAP & FLOWCHART STYLES
   ========================================= */

/* Main Mindmap Container */
.mindmap-wrapper {
    display: flex;
    justify-content: center;
    overflow-x: auto;
    padding: 20px 0;
    width: 100%;
}

.mindmap {
    display: flex;
    flex-direction: column;
    align-items: center;
}

/* Tree Structure using standard ul/li */
.mindmap ul {
    padding-top: 20px; 
    position: relative;
    transition: all 0.5s;
    display: flex;
    justify-content: center;
    padding-left: 0;
}

.mindmap li {
    float: left; text-align: center;
    list-style-type: none;
    position: relative;
    padding: 20px 10px 0 10px;
    transition: all 0.5s;
}

/* Drawing connecting lines using pseudo-elements */
.mindmap li::before, .mindmap li::after{
    content: '';
    position: absolute; top: 0; right: 50%;
    border-top: 2px solid var(--text-dim);
    width: 50%; height: 20px;
}

.mindmap li::after{
    right: auto; left: 50%;
    border-left: 2px solid var(--text-dim);
}

/* Cleanup extra lines for first and last child */
.mindmap li:only-child::after, .mindmap li:only-child::before { display: none; }
.mindmap li:only-child { padding-top: 0; }
.mindmap li:first-child::before, .mindmap li:last-child::after { border: 0 none; }

/* Connecting line to the bottom of parents */
.mindmap li:first-child::after{ border-radius: 8px 0 0 0; }
.mindmap li:last-child::before{ border-right: 2px solid var(--text-dim); border-radius: 0 8px 0 0; }

.mindmap ul ul::before{
    content: '';
    position: absolute; top: 0; left: 50%;
    border-left: 2px solid var(--text-dim);
    width: 0; height: 20px;
}

/* Node Styling (Circles / Pills) */
.mindmap-node {
    display: inline-block;
    background: var(--bg-dark);
    border: 2px solid var(--accent-blue);
    color: var(--text-white);
    padding: 10px 15px;
    text-decoration: none;
    border-radius: 30px; /* High radius for pill/circle shape */
    font-size: 0.85rem;
    font-weight: 600;
    transition: all 0.3s ease;
    box-shadow: 0 4px 6px rgba(0,0,0,0.3);
    position: relative;
    z-index: 1;
}

.mindmap-node:hover {
    background: var(--accent-blue);
    color: var(--bg-dark);
    box-shadow: 0 0 15px var(--accent-blue);
    transform: scale(1.05);
}

/* Root Node Variation */
.mindmap-node.root {
    border-color: var(--accent-yellow);
    background: rgba(251, 191, 36, 0.1);
}

.mindmap-node.root:hover {
    background: var(--accent-yellow);
    color: var(--bg-dark);
    box-shadow: 0 0 15px var(--accent-yellow);
}

/* Linear Flowchart styles (Top to Bottom) */
.flowchart {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0;
}

.flow-arrow {
    width: 2px;
    height: 25px;
    background: var(--text-dim);
    position: relative;
    margin: 5px 0;
}

.flow-arrow::after {
    content: '';
    position: absolute;
    bottom: -4px;
    left: -4px;
    border-left: 5px solid transparent;
    border-right: 5px solid transparent;
    border-top: 5px solid var(--text-dim);
}
- JavaScript
- const app = {
    state: {
        username: "",
        xp: 0,
        level: 1,
        history: {}, // Format: { "Topic": level_integer }
        mode: 'text' // 'text', 'quiz', 'visual'
    },

    init: function() {
        // Load existing history if available
        const saved = localStorage.getItem('scholar_data');
        if (saved) this.state = JSON.parse(saved);
    },

    save: function() {
        localStorage.setItem('scholar_data', JSON.stringify(this.state));
    },

    login: function() {
        const userVal = document.getElementById('username').value;
        if (!userVal) return alert("Identify yourself, Scholar.");
        
        this.state.username = userVal;
        document.getElementById('user-display').innerText = userVal;
        document.getElementById('login-container').style.display = 'none';
        document.getElementById('app-container').style.display = 'block';
        this.updateUI();
        this.addMessage("AI", `Welcome back, ${userVal}. What are we researching today?`);
    },

    setMode: function(m) {
        this.state.mode = m;
        document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
        event.target.classList.add('active');
        this.addMessage("System", `Mode switched to: ${m.toUpperCase()}`);
    },

    handleSend: function() {
        const input = document.getElementById('user-input');
        const text = input.value.trim();
        if (!text) return;

        this.addMessage("User", text);
        this.processResponse(text);
        input.value = "";
    },

    processResponse: function(query) {
        // Logic for Adaptive Learning (Example: Machine Learning)
        let topic = query.toLowerCase();
        let currentTopicLevel = this.state.history[topic] || 0;

        let response = "";

        if (this.state.mode === 'quiz') {
            response = `[QUIZ MODE] Based on your history with ${query}, here is a question: What is the primary goal of this concept?`;
        } else if (this.state.mode === 'visual') {
            response = `[VISUAL MODE] Generating a mindmap for ${query}... Imagine a central node branching into Key Components and Use Cases.`;
        } else {
            // Adaptive Text Progression
            if (currentTopicLevel === 0) {
                response = `Let's start with the basics of ${query}. It is defined as... [Beginner Level]`;
                this.state.history[topic] = 1;
                this.gainXP(20);
            } else {
                response = `Since you understand the basics of ${query}, let's dive deeper into the advanced applications... [Intermediate Level]`;
                this.state.history[topic] = 2;
                this.gainXP(50);
            }
        }

        this.addMessage("AI", response);
        this.save();
    },

    gainXP: function(val) {
        this.state.xp += val;
        if (this.state.xp >= 100) {
            this.state.level++;
            this.state.xp = 0;
            this.addMessage("System", "LEVEL UP! You are now a Level " + this.state.level + " Scholar.");
        }
        this.updateUI();
    },

    updateUI: function() {
        document.getElementById('xp-fill').style.width = this.state.xp + "%";
        document.getElementById('level-tag').innerText = `Lvl ${this.state.level} Scholar`;
    },

    addMessage: function(sender, text) {
        const box = document.getElementById('chat-box');
        const m = document.createElement('div');
        m.className = `message ${sender.toLowerCase()}`;
        m.innerHTML = `<strong>${sender}:</strong> ${text}`;
        box.appendChild(m);
        box.scrollTop = box.scrollHeight;
    }
};

app.init(); 

---

## ▶️ How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
