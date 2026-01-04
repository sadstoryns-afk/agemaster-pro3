
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    
    <meta name="google-site-verification" content="sQYMF8wNauVN-H3J7u6rwydmqwZ6aSw5QtrshaNevWQ" />

    <title>ToolMaster Pro - Exact Age Calculator & Smart Tools</title>
    <meta name="description" content="ToolMaster Pro: Sabse sateek Age Calculator, Love Matcher aur Password Generator. Muft aur surakshit web tools.">
    <meta name="keywords" content="Age Calculator, Love Matcher, Day Finder, ToolMaster Pro, Exact Age Finder 2026">
    <meta name="author" content="ToolMaster Pro">

    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --primary: #6366f1; --secondary: #a855f7; --accent: #10b981; --bg: #0f172a; --card: #ffffff; --text: #1e293b; }
        .light-mode { --bg: #f1f5f9; --card: #ffffff; --text: #1e293b; }
        
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        body { margin: 0; font-family: 'Poppins', sans-serif; background: var(--bg); color: var(--text); transition: 0.3s; min-height: 100vh; display: flex; flex-direction: column; align-items: center; padding-bottom: 40px; }
        
        .header { width: 100%; max-width: 500px; display: flex; justify-content: space-between; align-items: center; padding: 20px; }
        .nav-btn { background: white; border: none; width: 45px; height: 45px; border-radius: 12px; font-size: 20px; cursor: pointer; box-shadow: 0 5px 15px rgba(0,0,0,0.3); }
        .live-timer { color: white; font-weight: 700; font-size: 14px; background: rgba(255,255,255,0.1); padding: 8px 15px; border-radius: 30px; border: 1px solid rgba(255,255,255,0.2); backdrop-filter: blur(5px); }

        .container { width: 92%; max-width: 450px; }
        .tool-card { background: var(--card); padding: 25px; border-radius: 30px; box-shadow: 0 15px 35px rgba(0,0,0,0.2); margin-bottom: 25px; text-align: center; border: 1px solid rgba(0,0,0,0.05); }
        h2 { background: linear-gradient(to right, #6366f1, #a855f7); -webkit-background-clip: text; -webkit-text-fill-color: transparent; font-weight: 800; margin: 0 0 15px 0; font-size: 20px; }
        
        input, textarea, select { width: 100%; padding: 12px; border: 2px solid #e2e8f0; border-radius: 15px; font-size: 14px; margin-bottom: 10px; outline: none; font-family: inherit; }
        .main-btn { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: white; border: none; width: 100%; padding: 15px; border-radius: 15px; font-size: 15px; font-weight: 700; cursor: pointer; transition: 0.2s; }
        .main-btn:active { transform: scale(0.97); }
        
        .res-box { display: none; background: #f8fafc; padding: 15px; border-radius: 15px; border: 1px solid #ddd; margin-top: 15px; word-break: break-all; }
        
        #side-drawer { position: fixed; top: 0; left: -100%; width: 280px; height: 100%; background: white; z-index: 3000; transition: 0.4s; padding: 40px 20px; box-shadow: 10px 0 30px rgba(0,0,0,0.5); }
        #side-drawer.active { left: 0; }
        .drawer-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); z-index: 2500; }
        .drawer-item { padding: 12px; margin-bottom: 8px; border-radius: 10px; background: #f1f5f9; cursor: pointer; font-weight: 600; color: #333; }
        
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.85); z-index: 5000; align-items: center; justify-content: center; padding: 20px; }
        .modal-content { background: white; width: 100%; max-width: 400px; border-radius: 25px; padding: 25px; position: relative; color: #333; }
    </style>
</head>
<body class="dark-mode">

<div class="header">
    <button class="nav-btn" onclick="toggleDrawer()">☰</button>
    <div class="live-timer" id="clock">00:00:00</div>
</div>

<div class="drawer-overlay" id="overlay" onclick="toggleDrawer()"></div>

<div id="side-drawer">
    <h2 style="background:none; -webkit-text-fill-color:initial; color:var(--primary)">ToolMaster Pro</h2>
    <div class="drawer-item" onclick="toggleTheme()">🌓 Dark/Light Mode</div>
    <div class="drawer-item" onclick="openAbout()">ℹ️ About Us</div>
    <div class="drawer-item" onclick="location.reload()">🔄 Refresh App</div>
</div>

<div class="modal" id="aboutModal">
    <div class="modal-content">
        <span style="position:absolute; top:15px; right:20px; font-size:25px; cursor:pointer;" onclick="closeAbout()">&times;</span>
        <h3 style="color:var(--primary)">About Us</h3>
        <p style="font-size:14px; line-height:1.6;"><b>ToolMaster Pro</b> ek modern web tool hub hai jo aapko sateek Age calculation, Secure Password generation aur Health tools muft mein pradan karta hai. Hum koi data save nahi karte.</p>
    </div>
</div>

<div class="container">
    <div class="tool-card">
        <h2>Age Calculator 🎂</h2>
        <input type="date" id="dob">
        <button onclick="calcAge()" class="main-btn">Check Age ⚡</button>
        <div id="ageRes" class="res-box"><b id="ageOut" style="color:var(--primary); font-size:18px;"></b></div>
    </div>

    <div class="tool-card">
        <h2>Day Finder 🔮</h2>
        <input type="date" id="dayInput">
        <button onclick="calcDay()" class="main-btn" style="background:var(--accent)">Din Jane</button>
        <div id="dayRes" class="res-box"><b id="dayOut" style="font-size:18px;"></b></div>
    </div>

    <div class="tool-card">
        <h2>Password Generator 🔐</h2>
        <button onclick="genPass()" class="main-btn" style="background:var(--secondary)">Secure Password Banayein</button>
        <div id="passRes" class="res-box"><b id="passOut" style="font-family: monospace; letter-spacing: 1px; color:var(--accent);"></b></div>
    </div>

    <div class="tool-card">
        <h2>Word Counter ✍️</h2>
        <textarea id="wordText" placeholder="Yahan type karein..." oninput="countWords()" rows="3"></textarea>
        <p style="font-size:13px; font-weight:600;">Shabd: <span id="wCount">0</span> | Akshar: <span id="cCount">0</span></p>
    </div>

    <div class="tool-card">
        <h2>BMR Health Check ⚖️</h2>
        <input type="number" id="weight" placeholder="Wajan (kg)">
        <input type="number" id="height" placeholder="Lambai (cm)">
        <input type="number" id="ageBmr" placeholder="Umra">
        <select id="gender">
            <option value="male">Purush (Male)</option>
            <option value="female">Mahila (Female)</option>
        </select>
        <button onclick="calcBMR()" class="main-btn" style="background:#f59e0b">BMR Check Karein</button>
        <div id="bmrRes" class="res-box"><b id="bmrOut"></b></div>
    </div>
</div>

<script>
    setInterval(() => { document.getElementById('clock').innerText = new Date().toLocaleTimeString(); }, 1000);

    function toggleDrawer() {
        const d = document.getElementById('side-drawer');
        const o = document.getElementById('overlay');
        d.classList.toggle('active');
        o.style.display = d.classList.contains('active') ? 'block' : 'none';
    }

    function toggleTheme() {
        document.body.classList.toggle('light-mode');
        toggleDrawer();
    }

    function openAbout() { toggleDrawer(); document.getElementById('aboutModal').style.display = 'flex'; }
    function closeAbout() { document.getElementById('aboutModal').style.display = 'none'; }

    function calcAge() {
        const val = document.getElementById('dob').value;
        if(!val) return;
        const dob = new Date(val); const now = new Date();
        let y = now.getFullYear() - dob.getFullYear();
        let m = now.getMonth() - dob.getMonth();
        let d = now.getDate() - dob.getDate();
        if (d < 0) { m--; d += new Date(now.getFullYear(), now.getMonth(), 0).getDate(); }
        if (m < 0) { y--; m += 12; }
        document.getElementById('ageRes').style.display = 'block';
        document.getElementById('ageOut').innerText = `${y} saal, ${m} mahine, ${d} din`;
    }

    function calcDay() {
        const val = document.getElementById('dayInput').value;
        if(!val) return;
        const days = ["Ravivar", "Somvar", "Mangalvar", "Budhvar", "Guruvar", "Shukravar", "Shanivar"];
        document.getElementById('dayRes').style.display = 'block';
        document.getElementById('dayOut').innerText = "Us din " + days[new Date(val).getDay()] + " tha.";
    }

    function genPass() {
        const chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*";
        let pass = "";
        for (let i = 0; i < 14; i++) pass += chars.charAt(Math.floor(Math.random() * chars.length));
        document.getElementById('passRes').style.display = 'block';
        document.getElementById('passOut').innerText = pass;
    }

    function countWords() {
        const text = document.getElementById('wordText').value.trim();
        document.getElementById('wCount').innerText = text ? text.split(/\s+/).length : 0;
        document.getElementById('cCount').innerText = text.length;
    }

    function calcBMR() {
        const w = parseFloat(document.getElementById('weight').value);
        const h = parseFloat(document.getElementById('height').value);
        const a = parseFloat(document.getElementById('ageBmr').value);
        const g = document.getElementById('gender').value;
        if(!w || !h || !a) return alert("Puri jankari bharein!");
        let bmr = (g === 'male') ? (10 * w + 6.25 * h - 5 * a + 5) : (10 * w + 6.25 * h - 5 * a - 161);
        document.getElementById('bmrRes').style.display = 'block';
        document.getElementById('bmrOut').innerText = `Aapka BMR: ${bmr.toFixed(2)} calories/din`;
    }
</script>
</body>
</html>
