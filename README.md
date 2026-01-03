<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    
    <title>ToolMaster Pro - Age Calculator & Secure Password Generator</title>
    <meta name="description" content="मुफ्त उम्र कैलकुलेटर और सुरक्षित पासवर्ड जनरेटर। अपनी प्राइवेसी सुरक्षित रखें और अपनी सटीक उम्र जानें।">
    <meta name="author" content="ToolMaster Pro Team">
    <link rel="icon" href="https://img.icons8.com/fluency/48/shield.png">

    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <style>
        :root { --primary: #6366f1; --secondary: #a855f7; --accent: #10b981; --bg: #0f172a; }
        * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; scroll-behavior: smooth; }
        
        body { 
            margin: 0; font-family: 'Poppins', sans-serif; background: var(--bg); 
            background-image: radial-gradient(at 0% 0%, rgba(99, 102, 241, 0.15) 0, transparent 50%);
            color: #1e293b; padding: 10px; display: flex; flex-direction: column; align-items: center;
        }

        .container { width: 100%; max-width: 440px; }
        #live-clock { color: #94a3b8; font-size: 11px; margin-bottom: 10px; text-align: center; letter-spacing: 1px; }

        .tool-card { 
            background: rgba(255, 255, 255, 0.98); padding: 25px; border-radius: 35px; 
            box-shadow: 0 20px 40px rgba(0,0,0,0.3); backdrop-filter: blur(10px); 
            margin-bottom: 20px; border: 1px solid rgba(255,255,255,0.2);
        }

        h1 { font-weight: 800; margin: 0; font-size: 28px; text-align: center; background: linear-gradient(to right, var(--primary), var(--secondary)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .tagline { color: #64748b; font-size: 10px; text-align: center; text-transform: uppercase; letter-spacing: 2px; margin-bottom: 25px; display: block; }

        label { font-size: 13px; font-weight: 600; color: #475569; display: block; margin-bottom: 8px; }
        input, textarea { 
            width: 100%; padding: 15px; border: 2px solid #e2e8f0; border-radius: 18px; 
            font-size: 16px; outline: none; margin-bottom: 15px; background: #fff; transition: 0.3s;
        }
        input:focus { border-color: var(--primary); box-shadow: 0 0 10px rgba(99, 102, 241, 0.1); }

        .main-btn { 
            background: linear-gradient(135deg, var(--primary), var(--secondary)); 
            color: white; border: none; width: 100%; padding: 18px; border-radius: 18px; 
            font-size: 16px; font-weight: 700; cursor: pointer; transition: 0.3s;
        }
        .main-btn:active { transform: scale(0.96); }

        .result-box { display: none; margin-top: 15px; padding: 20px; background: #f8fafc; border-radius: 25px; border: 1px solid #e2e8f0; text-align: center; }
        .pass-display { background: #f0fdf4; padding: 15px; border-radius: 15px; margin: 15px 0; font-weight: 700; color: #16a34a; border: 2px dashed #22c55e; font-family: monospace; font-size: 20px; }

        .info-content { text-align: left; font-size: 13px; color: #475569; }
        .info-content h3 { font-size: 16px; color: #1e293b; margin: 15px 0 8px; border-left: 4px solid var(--primary); padding-left: 10px; }

        footer { text-align: center; font-size: 11px; color: #94a3b8; padding: 40px 0; width: 100%; }
        .footer-link { color: #6366f1; cursor: pointer; text-decoration: none; margin: 0 8px; font-weight: 600; }
        
        /* Cookie Banner */
        #cookie-box { position: fixed; bottom: 20px; left: 20px; right: 20px; background: #1e293b; color: white; padding: 15px; border-radius: 15px; font-size: 11px; display: flex; justify-content: space-between; align-items: center; z-index: 999; }
    </style>
</head>
<body>

<div id="cookie-box">
    <span>🍪 हम अनुभव सुधारने के लिए कुकीज़ का उपयोग करते हैं।</span>
    <button onclick="this.parentElement.style.display='none'" style="background:var(--accent); border:none; color:white; padding:5px 10px; border-radius:5px; cursor:pointer;">OK</button>
</div>

<div class="container">
    <div id="live-clock">Loading Time...</div>

    <div class="tool-card">
        <h1>ToolMaster Pro ✨</h1>
        <span class="tagline">The Secure Utility Hub</span>
        
        <label>अपनी जन्मतिथि चुनें 📅</label>
        <input type="date" id="birth-date">
        <button onclick="calculateAge()" class="main-btn">Calculate Now ⚡</button>
        
        <div id="age-result" class="result-box">
            <h3 id="res-years" style="font-size: 55px; margin: 0; color: #1e293b;">0</h3>
            <p id="res-detail" style="font-weight: 600; color: #64748b; margin-top: -5px;">साल के हुए आप</p>
            <div style="background:#eff6ff; padding:12px; border-radius:15px; font-size:11px; color:#1e40af; text-align:left; margin-top:15px;">
                <b>🛡️ बीमा सलाह:</b> आपकी उम्र के अनुसार ₹1 करोड़ का कवर मात्र ₹450/माह से शुरू है।
            </div>
            <a href="#" id="wa-share" style="display:block; margin-top:15px; color:#22c55e; font-weight:700; text-decoration:none; font-size:13px;">WhatsApp पर शेयर करें 📱</a>
        </div>
    </div>

    <div class="tool-card">
        <h3>🔐 Secure Password Generator</h3>
        <p style="font-size: 10px; color: #64748b;">यह टूल सुरक्षित है और पासवर्ड कहीं सेव नहीं होता।</p>
        <button onclick="generatePassword()" class="main-btn" style="background: #10b981;">Generate Password 🎲</button>
        
        <div id="pass-container" class="result-box">
            <div class="pass-display" id="output-pass">********</div>
            <button onclick="copyPass()" style="background:#22c55e; color:white; border:none; padding:15px; border-radius:15px; width:100%; font-weight:700; cursor:pointer;">Copy Password 📋</button>
        </div>
    </div>

    <div class="tool-card info-content">
        <h3>ℹ️ हमारे बारे में</h3>
        <p>ToolMaster Pro एक विश्वसनीय मंच है जहाँ हम बिना किसी डेटा संग्रहण के सटीक गणना उपकरण प्रदान करते हैं।</p>
        
        <h3>❓ अक्सर पूछे जाने वाले सवाल (FAQs)</h3>
        <details style="margin-bottom:10px;">
            <summary style="cursor:pointer; font-weight:600;">क्या यह सुरक्षित है?</summary>
            <p style="padding-top:5px;">हाँ, सभी गणनाएं आपके डिवाइस पर होती हैं।</p>
        </details>
        <details>
            <summary style="cursor:pointer; font-weight:600;">क्या सेवा मुफ्त है?</summary>
            <p style="padding-top:5px;">हाँ, हमारी सभी सेवाएँ 100% मुफ्त हैं।</p>
        </details>
    </div>

    <footer>
        <div style="margin-bottom: 20px;">
            <a class="footer-link" onclick="alert('Privacy Policy: हम कोई निजी डेटा नहीं लेते।')">Privacy</a>
            <a class="footer-link" onclick="alert('Terms: केवल व्यक्तिगत उपयोग के लिए।')">Terms</a>
            <a class="footer-link" onclick="alert('Contact: support@toolmaster.pro')">Contact</a>
        </div>
        <p>© 2026 ToolMaster Pro | सुरक्षित और निजी</p>
    </footer>
</div>

<script>
function updateClock() {
    document.getElementById('live-clock').innerText = new Date().toLocaleString('hi-IN');
}
setInterval(updateClock, 1000);

function calculateAge() {
    const val = document.getElementById('birth-date').value;
    if (!val) return alert("तारीख चुनें!");
    const dob = new Date(val);
    const now = new Date();
    let y = now.getFullYear() - dob.getFullYear();
    let m = now.getMonth() - dob.getMonth();
    if (m < 0 || (m === 0 && now.getDate() < dob.getDate())) y--;
    
    document.getElementById('age-result').style.display = 'block';
    document.getElementById('res-years').innerText = y;
    const msg = `मेरी उम्र ${y} साल है! चेक करें: ${window.location.href}`;
    document.getElementById('wa-share').href = `https://api.whatsapp.com/send?text=${encodeURIComponent(msg)}`;
}

function generatePassword() {
    const c = "ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz23456789!@#$%^&*";
    let p = "";
    for (let i = 0; i < 14; i++) p += c.charAt(Math.floor(Math.random() * c.length));
    document.getElementById('pass-container').style.display = 'block';
    document.getElementById('output-pass').innerText = p;
}

function copyPass() {
    navigator.clipboard.writeText(document.getElementById('output-pass').innerText);
    alert("कॉपी हो गया! ✅");
}
</script>
</body>
</html>
