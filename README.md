[index.html.html](https://github.com/user-attachments/files/32705607/index.html.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Linguistic Escape Room: Stative vs. Dynamic Verbs</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@500;700;900&family=Poppins:wght@300;400;600&display=swap');
        
        * { box-sizing: border-box; }
        
        body {
            background-color: #0b0f19;
            color: #e2e8f0;
            font-family: 'Poppins', sans-serif;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-image: 
                radial-gradient(circle at 10% 20%, rgba(59, 130, 246, 0.15) 0%, transparent 40%),
                radial-gradient(circle at 90% 80%, rgba(139, 92, 246, 0.15) 0%, transparent 40%);
        }
        
        .container {
            width: 100%;
            max-width: 900px;
            background: rgba(15, 23, 42, 0.95);
            padding: 35px;
            border-radius: 20px;
            box-shadow: 0 0 35px rgba(59, 130, 246, 0.25);
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
        }
        
        h1 {
            font-family: 'Orbitron', sans-serif;
            color: #38bdf8;
            text-shadow: 0 0 15px rgba(56, 189, 248, 0.5);
            font-size: 2em;
            margin-bottom: 10px;
            text-align: center;
        }
        
        p.subtitle {
            text-align: center;
            color: #94a3b8;
            margin-bottom: 25px;
        }

        .avatar-container {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 20px 0;
            flex-wrap: wrap;
        }

        .avatar-option {
            cursor: pointer;
            width: 100px;
            padding: 15px;
            border-radius: 12px;
            border: 2px solid rgba(255, 255, 255, 0.1);
            background: rgba(30, 41, 59, 0.5);
            text-align: center;
            transition: all 0.3s ease;
        }

        .avatar-icon { font-size: 38px; display: block; margin-bottom: 5px; }

        .avatar-option p {
            margin: 0;
            font-size: 0.85em;
            font-weight: 600;
            color: #cbd5e1;
        }

        .avatar-option:hover, .selected-avatar {
            transform: translateY(-5px);
            border-color: #38bdf8;
            background: rgba(56, 189, 248, 0.15);
            box-shadow: 0 0 15px rgba(56, 189, 248, 0.3);
        }

        .timer {
            font-family: 'Orbitron', monospace;
            font-size: 2.2em;
            color: #ef4444;
            text-shadow: 0 0 10px rgba(239, 68, 68, 0.6);
            margin: 15px 0;
            text-align: center;
        }

        .question-card {
            background: rgba(30, 41, 59, 0.7);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-left: 4px solid #38bdf8;
            border-radius: 10px;
            padding: 16px 20px;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 15px;
            flex-wrap: wrap;
        }

        .question-text {
            flex: 1;
            min-width: 280px;
            font-size: 1.05em;
        }

        .verb-hint {
            color: #38bdf8;
            font-weight: bold;
        }

        .input-group {
            display: flex;
            align-items: center;
            gap: 10px;
        }

        input[type="text"] {
            padding: 10px 14px;
            border-radius: 8px;
            border: 1px solid #475569;
            background: #0f172a;
            color: #f8fafc;
            font-size: 1em;
            width: 220px;
            outline: none;
            text-align: center;
            transition: all 0.2s;
        }

        input[type="text"]:focus {
            border-color: #38bdf8;
            box-shadow: 0 0 8px rgba(56, 189, 248, 0.4);
        }

        .status-indicator {
            font-size: 1.2em;
            width: 25px;
            text-align: center;
        }

        button.primary-btn {
            background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
            color: white;
            border: none;
            padding: 14px 40px;
            font-size: 1.1em;
            font-weight: bold;
            cursor: pointer;
            border-radius: 10px;
            transition: all 0.3s;
            display: block;
            margin: 25px auto 0;
            box-shadow: 0 4px 15px rgba(37, 99, 235, 0.4);
        }

        button.primary-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(37, 99, 235, 0.6);
            background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
        }

        .hud-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-bottom: 15px;
            border-bottom: 1px solid #334155;
            margin-bottom: 20px;
            font-weight: 600;
            color: #38bdf8;
        }

        .progress-bar-container {
            width: 100%;
            background: #1e293b;
            border-radius: 10px;
            height: 12px;
            margin-bottom: 25px;
            overflow: hidden;
            border: 1px solid #334155;
        }

        .progress-bar {
            height: 100%;
            width: 0%;
            background: linear-gradient(90deg, #38bdf8, #818cf8);
            transition: width 0.4s ease;
        }

        .hidden { display: none; }
        
        .stage-title {
            color: #f1f5f9;
            font-family: 'Orbitron', sans-serif;
            font-size: 1.3em;
            margin-bottom: 15px;
            border-bottom: 1px dashed #334155;
            padding-bottom: 8px;
        }
    </style>
</head>
<body>

<!-- Setup Screen -->
<div class="container" id="intro-screen">
    <h1>🔐 MISSION 3: VERB DECODER</h1>
    <p class="subtitle">Same Verb, Different Meaning — Master Stative & Dynamic Forms to Escape!</p>
    
    <div style="text-align: center; margin-bottom: 20px;">
        <input type="text" id="teamName" placeholder="Enter Team Name..." style="width: 80%; max-width: 350px;">
    </div>

    <h3 style="text-align: center; color: #cbd5e1;">Select Team Mascot:</h3>
    <div class="avatar-container">
        <div class="avatar-option" onclick="selectAvatar('Cyber-Fox', this)">
            <span class="avatar-icon">🦊</span>
            <p>Cyber-Fox</p>
        </div>
        <div class="avatar-option" onclick="selectAvatar('Quantum-Owl', this)">
            <span class="avatar-icon">🦉</span>
            <p>Quantum-Owl</p>
        </div>
        <div class="avatar-option" onclick="selectAvatar('Neon-Panther', this)">
            <span class="avatar-icon">🐆</span>
            <p>Neon-Panther</p>
        </div>
        <div class="avatar-option" onclick="selectAvatar('Tech-Falcon', this)">
            <span class="avatar-icon">🦅</span>
            <p>Tech-Falcon</p>
        </div>
    </div>

    <button class="primary-btn" onclick="startGame()">Initiate Escape Sequence ⚡</button>
</div>

<!-- Main Game Screen -->
<div class="container hidden" id="game-screen">
    <div class="hud-bar">
        <span id="display-team">Team: </span>
        <span id="display-avatar">Mascot: </span>
    </div>
    
    <div class="timer" id="timer">45:00</div>

    <div class="progress-bar-container">
        <div class="progress-bar" id="progress-bar"></div>
    </div>

    <div id="stage-container">
        <!-- Questions injected via JavaScript -->
    </div>

    <button class="primary-btn" id="action-btn" onclick="checkCurrentStage()">Validate Submissions 🔓</button>
</div>

<script>
    let timerInterval;
    let timeLeft = 45 * 60;
    let currentStageIndex = 0;
    let selectedAvatarName = "";

    const stages = [
        {
            title: "STAGE 1: VERB PAIRS 1–5",
            questions: [
                { id: 1, text: "1. I __________________________ what you mean.", verb: "(see)", answer: ["see"] },
                { id: 2, text: "2. The chef __________________________ the soup.", verb: "(taste)", answer: ["is tasting", "'s tasting"] },
                { id: 3, text: "3. Tom __________________________ very rude today.", verb: "(be)", answer: ["is being", "'s being"] },
                { id: 4, text: "4. She __________________________ two sisters.", verb: "(have)", answer: ["has"] },
                { id: 5, text: "5. Why __________________________ at me?", verb: "(look)", answer: ["are you looking"], inputType: "single" }
            ]
        },
        {
            title: "STAGE 2: VERB PAIRS 6–10",
            questions: [
                { id: 6, text: "6. I __________________________ about your idea right now.", verb: "(think)", answer: ["am thinking", "'m thinking"] },
                { id: 7, text: "7. The flowers __________________________ wonderful.", verb: "(smell)", answer: ["smell"] },
                { id: 8, text: "8. I __________________________ the fabric to see if it is soft.", verb: "(feel)", answer: ["am feeling", "'m feeling"] },
                { id: 9, text: "9. The students __________________________ on stage tonight.", verb: "(appear)", answer: ["are appearing", "'re appearing"] },
                { id: 10, text: "10. I __________________________ this movie is fantastic.", verb: "(think)", answer: ["think"] }
            ]
        },
        {
            title: "STAGE 3: VERB PAIRS 11–15",
            questions: [
                { id: 11, text: "11. You __________________________ tired today.", verb: "(look)", answer: ["look"] },
                { id: 12, text: "12. I __________________________ my doctor tomorrow.", verb: "(see)", answer: ["am seeing", "'m seeing"] },
                { id: 13, text: "13. The soup __________________________ delicious.", verb: "(taste)", answer: ["tastes"] },
                { id: 14, text: "14. She __________________________ breakfast right now.", verb: "(have)", answer: ["is having", "'s having"] },
                { id: 15, text: "15. I __________________________ that this is the right decision.", verb: "(feel)", answer: ["feel"] }
            ]
        },
        {
            title: "STAGE 4: VERB PAIRS 16–20",
            questions: [
                { id: 16, text: "16. The problem __________________________ to be more difficult than expected.", verb: "(appear)", answer: ["appears"] },
                { id: 17, text: "17. Tom __________________________ very polite.", verb: "(be)", answer: ["is"] },
                { id: 18, text: "18. The girl __________________________ the flowers.", verb: "(smell)", answer: ["is smelling", "'s smelling"] },
                { id: 19, text: "19. Why __________________________ at the new student?", verb: "(look)", answer: ["are you looking"] },
                { id: 20, text: "20. I __________________________ about the answer right now.", verb: "(think)", answer: ["am thinking", "'m thinking"] }
            ]
        }
    ];

    function selectAvatar(name, el) {
        document.querySelectorAll('.avatar-option').forEach(item => item.classList.remove('selected-avatar'));
        el.classList.add('selected-avatar');
        selectedAvatarName = name;
    }

    function startGame() {
        const team = document.getElementById('teamName').value.trim();
        if (!team || !selectedAvatarName) {
            alert("Please provide a Team Name and choose a Team Mascot to proceed!");
            return;
        }

        document.getElementById('display-team').innerText = "Team: " + team;
        document.getElementById('display-avatar').innerText = "Mascot: " + selectedAvatarName;
        document.getElementById('intro-screen').classList.add('hidden');
        document.getElementById('game-screen').classList.remove('hidden');

        renderStage();
        startTimer();
    }

    function startTimer() {
        timerInterval = setInterval(() => {
            let m = Math.floor(timeLeft / 60);
            let s = timeLeft % 60;
            document.getElementById('timer').innerText = `${m < 10 ? '0' : ''}${m}:${s < 10 ? '0' : ''}${s}`;
            
            if (timeLeft-- <= 0) {
                clearInterval(timerInterval);
                alert("SYSTEM BREACH! Time has expired. Lockdown initiated.");
                location.reload();
            }
        }, 1000);
    }

    function renderStage() {
        const currentStage = stages[currentStageIndex];
        const container = document.getElementById('stage-container');
        
        let html = `<div class="stage-title">${currentStage.title}</div>`;
        
        currentStage.questions.forEach(q => {
            html += `
                <div class="question-card">
                    <div class="question-text">
                        ${q.text} <span class="verb-hint">${q.verb}</span>
                    </div>
                    <div class="input-group">
                        <input type="text" id="q-${q.id}" placeholder="Type verb form..." autocomplete="off">
                        <span class="status-indicator" id="status-${q.id}"></span>
                    </div>
                </div>
            `;
        });

        container.innerHTML = html;
        updateProgressBar();
    }

    function updateProgressBar() {
        const percent = (currentStageIndex / stages.length) * 100;
        document.getElementById('progress-bar').style.width = `${percent}%`;
    }

    function sanitizeInput(text) {
        return text.trim().toLowerCase().replace(/\s+/g, ' ');
    }

    function checkCurrentStage() {
        const currentStage = stages[currentStageIndex];
        let allCorrect = true;

        currentStage.questions.forEach(q => {
            const userInput = sanitizeInput(document.getElementById(`q-${q.id}`).value);
            const statusEl = document.getElementById(`status-${q.id}`);
            
            const isCorrect = q.answer.some(validAns => sanitizeInput(validAns) === userInput);

            if (isCorrect) {
                statusEl.innerText = "✅";
                document.getElementById(`q-${q.id}`).style.borderColor = "#22c55e";
            } else {
                statusEl.innerText = "❌";
                document.getElementById(`q-${q.id}`).style.borderColor = "#ef4444";
                allCorrect = false;
            }
        });

        if (allCorrect) {
            if (currentStageIndex < stages.length - 1) {
                alert("Stage Decoded! Sector Unlocked.");
                currentStageIndex++;
                renderStage();
            } else {
                clearInterval(timerInterval);
                document.getElementById('progress-bar').style.width = `100%`;
                document.body.innerHTML = `
                    <div class="container" style="text-align: center;">
                        <h1 style="font-size: 3em; color: #38bdf8;">🏆 ULTIMATE VICTORY!</h1>
                        <p style="font-size: 1.3em; color: #cbd5e1; margin: 20px 0;">
                            Congratulations! Your team successfully decoded all 20 Stative & Dynamic verb patterns and bypassed security!
                        </p>
                        <button class="primary-btn" onclick="location.reload()">Replay Mission 🔄</button>
                    </div>`;
            }
        } else {
            alert("Errors detected! Check red-flagged inputs and correct them.");
        }
    }
</script>
</body>
</html>
