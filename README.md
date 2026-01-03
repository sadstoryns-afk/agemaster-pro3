# Drop landing page demo

Demo site to be used for [Netlify Drop](https://app.netlify.com/drop).

Thanks to [Andy Bell](https://piccalil.li/) for [User-controlled light/dark mode](https://piccalil.li/tutorial/create-a-user-controlled-dark-or-light-mode/) and [Rasmus Andersson](https://twitter.com/rsms) for creating [Inter UI font](https://rsms.me/inter/).
<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ToolMaster Pro - Age & Password Tracker</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <style>
        :root { --primary: #6366f1; --secondary: #a855f7; --accent: #10b981; --glass: rgba(255, 255, 255, 0.95); }
        body { margin: 0; font-family: 'Poppins', sans-serif; background: #0f172a; background-image: radial-gradient(at 0% 0%, rgba(99, 102, 241, 0.15) 0, transparent 50%); min-height: 100vh; padding: 20px; color: #1e293b; }
        
        .container { max-width: 500px; margin: 0 auto; }
        .tool-card { background: var(--glass); padding: 30px; border-radius: 35px; box-shadow: 0 20px 40px rgba(0,0,0,0.3); backdrop-filter: blur(10px); margin-bottom: 30px; border: 1px solid rgba(255,255,255,0.2); text-align: center; }
        
        h1 { font-weight: 800; margin-bottom: 20px; background: linear-gradient(to right, var(--primary), var(--secondary)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        h2 { font-size: 20px; margin-bottom: 15px; color: #334155; display: flex; align-items: center; justify-content: center; gap: 10px; }

        input { width: 100%; padding: 15px; border: 2px solid #e2e8f0; border-radius: 16px; font-size: 16px; box-sizing: border-box; outline: none; margin-bottom: 15px; }
        
        .main-btn { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: white; border: none; width: 100%; padding: 18px; border-radius: 16px; font-size: 16px; font-weight: 700; cursor: pointer; transition: 0.3s; }
        .main-btn:hover { transform: scale(1.02); }

        /* Age Result Style */
        #age-result { display: none; margin-top: 20px; background: #f8fafc; padding: 15px; border-radius: 20px; }

        /* Password Result Style */
        .pass-box { background: #f1f5f9; padding: 15px; border-radius: 12px; margin-top: 15px; font-weight: 700; font-size: 18px; color: var(--primary); word-break: break-all; border: 1px dashed var(--primary); position: relative; }
        .copy-btn { background: var(--accent); color: white; border: none; padding: 8px 15px; border-radius: 8px; font-size: 12px; cursor: pointer; margin-top: 10px; }

        .insurance-box { background: #eff6ff; border: 1px solid #bfdbfe; padding: 15px; border-radius: 15px; margin-top: 15px; text-align: left; font-size: 12px; }
        
        footer { text-align: center; font-size: 11px; color: #94a3b8; border-top: 1px solid #e2e8f0; padding-top: 20px; }
        .legal-link { color: #6366f1; cursor: pointer; text-decoration: underline; margin: 0 10px; }
    </style>
</head>
<body>

<div class="container">
    
    <div class="tool-card">
        <h1>ToolMaster Pro ✨</h1>
        <h2>📅 Age Calculator</h2>
        <input type="date" id="birth-date">
        <button onclick="calculateAge()" class="main-btn">Calculate Age ⚡</button>
        
        <div id="age-result">
            <h3 id="res-years" style="font-size: 40px; margin: 0;">0</h3>
            <p id="res-detail">0 Months | 0 Days</p>
            <div class="insurance-box">
                <b>🛡️ Insurance Tip:</b> आपकी उम्र के लिए ₹1 करोड़ का कवर मात्र <span id="ins-price">₹450</span>/महीने से शुरू है।
            </div>
            <a href="#" id="wa-share" style="text-decoration:none; color:#22c55e; font-weight:700; display:block; margin-top:10px;">Share on WhatsApp 📱</a>
        </div>
    </div>

    <div class="tool-card">
        <h2>🔐 Strong Password Generator</h2>
        <p style="font-size: 12px; color: #64748b; margin-bottom: 15px;">अपने सोशल मीडिया के लिए सुरक्षित पासवर्ड बनाएं</p>
        <button onclick="generatePassword()" class="main-btn" style="background: var(--accent);">Generate Password 🎲</button>
        
        <div id="pass-container" style="display: none;">
            <div class="pass-box" id="output-pass">********</div>
            <button onclick="copyPass()" class="copy-btn">Copy Password 📋</button>
        </div>
    </div>

    <footer>
        <p>
            <span class="legal-link">Privacy Policy</span> | 
            <span class="legal-link">Disclaimer</span>
        </p>
        <p>© 2026 ToolMaster Pro | Private & Secured 🔒</p>
    </footer>

</div>

<script>
// --- Age Logic ---
function calculateAge() {
    const dobValue = document.getElementById('birth-date').value;
    if (!dobValue) return alert("तारीख चुनें!");

    const dob = new Date(dobValue);
    const now = new Date();
    let years = now.getFullYear() - dob.getFullYear();
    let months = now.getMonth() - dob.getMonth();
    let days = now.getDate() - dob.getDate();

    if (days < 0) { months--; days += new Date(now.getFullYear(), now.getMonth(), 0).getDate(); }
    if (months < 0) { years--; months += 12; }

    document.getElementById('age-result').style.display = 'block';
    document.getElementById('res-years').innerText = years;
    document.getElementById('res-detail').innerText = `${months} महीने और ${days} दिन`;
    
    // Insurance Price
    let price = years < 25 ? 450 : years < 35 ? 650 : 950;
    document.getElementById('ins-price').innerText = "₹" + price;

    const msg = `मेरी उम्र ${years} साल है! आप भी चेक करें: ${window.location.href}`;
    document.getElementById('wa-share').href = `https://api.whatsapp.com/send?text=${encodeURIComponent(msg)}`;
}

// --- Password Logic ---
function generatePassword() {
    const chars = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789!@#$%^&*()_+";
    let password = "";
    for (let i = 0; i < 12; i++) {
        password += chars.charAt(Math.floor(Math.random() * chars.length));
    }
    document.getElementById('pass-container').style.display = 'block';
    document.getElementById('output-pass').innerText = password;
}

function copyPass() {
    const pass = document.getElementById('output-pass').innerText;
    navigator.clipboard.writeText(pass);
    alert("पासवर्ड कॉपी हो गया! ✅");
}
</script>

</body>
</html>
