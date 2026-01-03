
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>ToolMaster Pro - Smart Magic Hub</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    <style>
        :root { --primary: #6366f1; --secondary: #a855f7; --accent: #10b981; --bg: #0f172a; --card: #ffffff; }
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
        
        body { 
            margin: 0; font-family: 'Poppins', sans-serif; background: var(--bg); color: #1e293b;
            background-image: radial-gradient(circle at 50% -20%, #312e81, #0f172a);
            min-height: 100vh; display: flex; flex-direction: column; align-items: center; padding-bottom: 40px;
        }

        /* Header & Clock */
        .header { width: 100%; max-width: 500px; display: flex; justify-content: space-between; align-items: center; padding: 20px; }
        .nav-btn { background: white; border: none; width: 45px; height: 45px; border-radius: 12px; font-size: 20px; cursor: pointer; box-shadow: 0 5px 15px rgba(0,0,0,0.3); }
        .live-timer { color: white; font-weight: 700; font-size: 16px; background: rgba(255,255,255,0.1); padding: 8px 20px; border-radius: 30px; border: 1px solid rgba(255,255,255,0.2); }

        /* Container & Cards */
        .container { width: 92%; max-width: 450px; }
        .tool-card { 
            background: var(--card); padding: 25px; border-radius: 30px; 
            box-shadow: 0 20px 40px rgba(0,0,0,0.5); margin-bottom: 25px; text-align: center;
            border: 1px solid rgba(255,255,255,0.1);
        }
        h2 { background: linear-gradient(to right, #6366f1, #a855f7); -webkit-background-clip: text; -webkit-text-fill-color: transparent; font-weight: 800; margin: 0 0 15px 0; font-size: 22px; }
        
        input { width: 100%; padding: 14px; border: 2px solid #e2e8f0; border-radius: 15px; font-size: 15px; margin-bottom: 12px; outline: none; transition: 0.3s; }
        input:focus { border-color: var(--primary); }
        .main-btn { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: white; border: none; width: 100%; padding: 16px; border-radius: 15px; font-size: 16px; font-weight: 700; cursor: pointer; transition: 0.3s; }
        .main-btn:active { transform: scale(0.96); }

        .res-box { display: none; background: #f8fafc; padding: 15px; border-radius: 15px; border: 1px solid #ddd; margin-top: 15px; animation: pop 0.4s ease; }
        @keyframes pop { from { transform: scale(0.8); opacity: 0; } to { transform: scale(1); opacity: 1; } }

        /* Side Menu */
        #side-drawer { position: fixed; top: 0; left: -100%; width: 280px; height: 100%; background: white; z-index: 3000; transition: 0.5s; padding: 40px 20px; }
        #side-drawer.active { left: 0; }
        .drawer-overlay { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); z-index: 2500; }
        .drawer-item { padding: 15px; margin-bottom: 10px; border-radius: 12px; background: #f1f5f9; cursor: pointer; font-weight: 600; color: #444; }

        /* Modal */
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.85); z-index: 5000; align-items: center; justify-content: center; padding: 20px; }
        .modal-content { background: white; width: 100%; max-width: 400px; border-radius: 25px; padding: 25px; position: relative; }
    </style>
</head>
<body>

<div class="header">
    <button class="nav-btn" onclick="toggleDrawer()">☰</button>
    <div class="live-timer" id="clock">00:00:00</div>
</div>

<div class="drawer-overlay" id="overlay" onclick="toggleDrawer()"></div>

<div id="side-drawer">
    <h2 style="background:none; -webkit-text-fill-color:initial; color:var(--primary)">ToolMenu</h2>
    <div class="drawer-item" onclick="openInfo('festivals')">🗓️ त्यौहार सूची 2026</div>
    <div class="drawer-item" onclick="openInfo('privacy')">🔒 प्राइवेसी पॉलिसी</div>
    <div class="drawer-item" onclick="location.reload()">🔄 रिफ्रेश एप</div>
    <p style="text-align:center; margin-top:50px; font-size:11px; color:#94a3b8;">Version 7.0 Pro</p>
</div>

<div class="modal" id="modal">
    <div class="modal-content">
        <span style="position:absolute; top:15px; right:20px; font-size:25px; cursor:pointer;" onclick="closeModal()">&times;</span>
        <h3 id="modal-title">Info</h3>
        <div id="modal-body" style="font-size:14px; line-height:1.6; color:#475569;"></div>
    </div>
</div>

<div class="container">
    
    <div class="tool-card">
        <h2>Age Calculator 🎂</h2>
        <input type="date" id="dob">
        <button onclick="calculateAge()" class="main-btn">Calculated Age ⚡</button>
        <div id="age-res" class="res-box">
            <div id="age-out" style="font-weight:800; color:var(--primary); font-size:18px;"></div>
        </div>
    </div>

    <div class="tool-card">
        <h2>Love Matcher ❤️</h2>
        <input type="text" id="name1" placeholder="आपका नाम">
        <input type="text" id="name2" placeholder="उनका नाम">
        <button onclick="loveMagic()" class="main-btn" style="background:var(--secondary)">जादू देखें ✨</button>
        <div id="love-res" class="res-box">
            <div id="love-out" style="font-size:22px; font-weight:800; color:#ef4444;"></div>
            <p style="font-size:10px; color:#94a3b8; margin-top:5px;">(सिर्फ मनोरंजन के लिए)</p>
        </div>
    </div>

    <div class="tool-card">
        <h2>Day Finder 🔮</h2>
        <p style="font-size:11px; color:#64748b; margin-bottom:10px;">कोई भी तारीख चुनें, यह दिन बता देगा!</p>
        <input type="date" id="magic-date">
        <button onclick="findDay()" class="main-btn" style="background:var(--accent)">दिन का पता लगाएँ</button>
        <div id="day-res" class="res-box">
            <div id="day-out" style="font-weight:800; font-size:18px; color:var(--bg);"></div>
        </div>
    </div>

    <div class="tool-card">
        <h2>Password Gen 🔐</h2>
        <button onclick="makePass()" class="main-btn">Secure Password बनाएँ</button>
        <div id="pass-res" class="res-box" style="font-family:monospace; font-weight:800; color:var(--accent); font-size:18px; letter-spacing:1px;"></div>
    </div>

</div>

<script>
    // Live Clock
    setInterval(() => { document.getElementById('clock').innerText = new Date().toLocaleTimeString(); }, 1000);

    function toggleDrawer() {
        const d = document.getElementById('side-drawer');
        const o = document.getElementById('overlay');
        d.classList.toggle('active');
        o.style.display = d.classList.contains('active') ? 'block' : 'none';
    }

    function openInfo(key) {
        toggleDrawer();
        const m = document.getElementById('modal');
        const t = document.getElementById('modal-title');
        const b = document.getElementById('modal-body');
        m.style.display = 'flex';
        if(key === 'festivals') {
            t.innerText = "2026 मुख्य त्यौहार";
            b.innerHTML = "<b>Holi:</b> 04 March<br><b>Eid:</b> 20 March<br><b>Independence Day:</b> 15 Aug<br><b>Diwali:</b> 08 Nov<br><b>Christmas:</b> 25 Dec";
        } else {
            t.innerText = "Privacy Policy";
            b.innerHTML = "हम आपका कोई डेटा सेव नहीं करते। यह पूरी तरह से सुरक्षित है और मनोरंजन व सुविधा के लिए बनाया गया है।";
        }
    }
    function closeModal() { document.getElementById('modal').style.display = 'none'; }

    // Logic: Age Calculator (Fixed)
    function calculateAge() {
        const val = document.getElementById('dob').value;
        if(!val) return;
        const dob = new Date(val); const now = new Date();
        let y = now.getFullYear() - dob.getFullYear();
        let m = now.getMonth() - dob.getMonth();
        let d = now.getDate() - dob.getDate();
        if (d < 0) { m--; d += new Date(now.getFullYear(), now.getMonth(), 0).getDate(); }
        if (m < 0) { y--; m += 12; }
        const res = document.getElementById('age-res');
        res.style.display = 'block';
        document.getElementById('age-out').innerText = `${y} साल, ${m} महीने, ${d} दिन`;
    }

    // Logic: Love Magic
    function loveMagic() {
        const n1 = document.getElementById('name1').value;
        const n2 = document.getElementById('name2').value;
        if(!n1 || !n2) return alert("दोनों नाम भरें!");
        const score = Math.floor(Math.random() * 41) + 60; // 60-100 के बीच स्कोर
        const res = document.getElementById('love-res');
        res.style.display = 'block';
        document.getElementById('love-out').innerText = score + "% Match! ❤️";
    }

    // Logic: Day Finder
    function findDay() {
        const val = document.getElementById('magic-date').value;
        if(!val) return;
        const date = new Date(val);
        const days = ["रविवार (Sunday)", "सोमवार (Monday)", "मंगलवार (Tuesday)", "बुधवार (Wednesday)", "गुरुवार (Thursday)", "शुक्रवार (Friday)", "शनिवार (Saturday)"];
        const res = document.getElementById('day-res');
        res.style.display = 'block';
        document.getElementById('day-out').innerText = "उस दिन " + days[date.getDay()] + " था/होगा।";
    }

    // Logic: Password
    function makePass() {
        const p = Math.random().toString(36).slice(-8).toUpperCase() + "@" + Math.floor(Math.random()*99);
        const res = document.getElementById('pass-res');
        res.style.display = 'block';
        res.innerText = p;
    }
</script>
</body>
</html>
