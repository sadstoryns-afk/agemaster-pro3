
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">




<meta name="google-site-verification" content="sQYMF8wNauVN-H3J7u6rwydmqwZ6aSw5QtrshaNevWQ" />


    
    <meta name="google-site-verification" content="sQYMF8wNauVN-H3J7u6rwydmqwZ6aSw5QtrshaNevWQ" />

    <title>ToolMaster Pro - Exact ="ToolMaster Pro: सबसे सटीक Age Calculator, Love card: #ffffff; --text: #1e293b; }
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        body { margin: 0; font-family: 'Poppins', sans-serif; background: var(--bg); color: var(--text); transition: 0.3s; min-height: 100vh; display: flex; flex-direction: column; align-items: center; padding-bottom: 40px; }
        .header { width: 100%; max-width: 500px; display: flex; justify-content: space-between; align-items: center; padding: 20px; }
        .nav-btn { background: white; border: none; width: 45px; height: 45px; border-radius: 12px; font-size: 20px; cursor: pointer; box-shadow: 0 5px 15px rgba(0,0,0,0.3); }
        .live-timer { color: white; font-weight: 700; font-size: 14px; background: rgba(255,255,255,0.1); padding: 8px 15px; border-radius: 30px; border: 1px solid rgba(255,255,255,0.2); backdrop-filter: blur(5px); px; }
        input, textarea, select { width: 100%; padding: 12px; border: 2px solid #e2e8f0; border-radius: 15px; font-size: 14px; margin-bottom: 10px; outline: none; }
        .main-btn { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: white; border: none; width: 100%; padding: 15px; border-radius: 15px; font-size: 15px; font-weight: 700; cursor: pointer; transition: 0.2s; }
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
    <div class="drawer-item" onclick="toggleTheme()">🌓 डार्क/लाइट मोड</div>
    <div class="drawer-item" onclick="openAbout()">ℹ️ हमारे बारे में</div>
    <div class="drawer-item" onclick="location.reload()">🔄 रिफ्रेश एप</div>
</div>

<div class="modal" id="aboutModal">
    <div class="modal-content">
        <span style="position:absolute; top:15px; right:20px; ';
    }
    function toggleTheme() { document.body.classList.toggle('light-mode'); toggleDrawer(); }
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
        document.getElementById('ageOut').innerText = `${y} साल, ${m} महीने, ${d} दिन`;
    }

    function calcDay() {
        const val = document.getElementById('dayInput').value;
        if(!val) return;
        const days = ["रविवार", "सोमवार", "मंगलवार", "बुधवार", "गुरुवार", "शुक्रवार", "शनिवार"];
        document.getElementById('dayRes').style.display = 'block';
        document.getElementById('dayOut').innerText = "उस दिन " + days[new Date(val).getDay()] + " था।";
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
        document.getElementById('bmrOut').innerText = `आपका BMR: ${bmr.toFixed(2)} कैलोरी/दिन`;
    }
</script>
</body>
</html>
