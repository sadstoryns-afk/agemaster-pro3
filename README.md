# Drop landing page demo

Demo site to be used for [Netlify Drop](https://app.netlify.com/drop).

Thanks to [Andy Bell](https://piccalil.li/) for [User-controlled light/dark mode](https://piccalil.li/tutorial/create-a-user-controlled-dark-or-light-mode/) and [Rasmus Andersson](https://twitter.com/rsms) for creating [Inter UI font](https://rsms.me/inter/).

<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AgeMaster Pro - Smart Life Tracker</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;800&display=swap" rel="stylesheet">
    
    <style>
        :root { --primary: #6366f1; --secondary: #a855f7; --glass: rgba(255, 255, 255, 0.95); }
        body { margin: 0; font-family: 'Poppins', sans-serif; background: #0f172a; background-image: radial-gradient(at 0% 0%, rgba(99, 102, 241, 0.15) 0, transparent 50%); min-height: 100vh; display: flex; justify-content: center; align-items: center; padding: 20px; color: #1e293b; }
        .container { background: var(--glass); width: 100%; max-width: 450px; padding: 30px; border-radius: 35px; box-shadow: 0 25px 50px -12px rgba(0,0,0,0.5); backdrop-filter: blur(10px); text-align: center; border: 1px solid rgba(255,255,255,0.2); }
        h1 { font-weight: 800; margin-bottom: 5px; background: linear-gradient(to right, var(--primary), var(--secondary)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .tagline { color: #64748b; font-size: 11px; margin-bottom: 25px; text-transform: uppercase; letter-spacing: 2px; }
        input[type="date"] { width: 100%; padding: 15px; border: 2px solid #e2e8f0; border-radius: 16px; font-size: 16px; box-sizing: border-box; outline: none; background: white; }
        .main-btn { background: linear-gradient(135deg, var(--primary), var(--secondary)); color: white; border: none; width: 100%; padding: 18px; border-radius: 16px; font-size: 16px; font-weight: 700; cursor: pointer; margin-top: 20px; transition: 0.3s; }
        #result-area { margin-top: 30px; display: none; animation: slideUp 0.6s ease-out; }
        @keyframes slideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        .big-card { background: white; padding: 25px; border-radius: 24px; margin-bottom: 15px; border: 1px solid #f1f5f9; }
        .big-card h2 { font-size: 48px; margin: 0; color: #1e293b; }
        .stats-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 15px; }
        .mini-card { background: white; padding: 15px; border-radius: 18px; border: 1px solid #f1f5f9; }
        .insurance-box { background: #eff6ff; border: 1px solid #bfdbfe; padding: 20px; border-radius: 20px; margin: 20px 0; text-align: left; }
        .insurance-box h4 { margin: 0 0 5px; color: #1e40af; }
        .share-btn { background: #22c55e; color: white; text-decoration: none; display: flex; align-items: center; justify-content: center; gap: 8px; padding: 15px; border-radius: 16px; font-weight: 700; margin-top: 15px; }
        .legal-section { display: none; text-align: left; margin-top: 20px; font-size: 12px; background: #eee; padding: 15px; border-radius: 15px; }
        footer { margin-top: 30px; font-size: 11px; color: #94a3b8; border-top: 1px solid #e2e8f0; padding-top: 20px; }
        .footer-link { color: #6366f1; cursor: pointer; text-decoration: underline; margin: 0 10px; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>AgeMaster Pro ✨</h1>
        <p class="tagline">The Ultimate Life Insights</p>
    </header>

    <div style="text-align: left; margin-bottom: 20px;">
        <label style="font-size: 13px; font-weight: 600; color: #475569;">अपनी जन्मतिथि चुनें 📅</label>
        <input type="date" id="birth-date">
    </div>

    <button onclick="calculate()" class="main-btn">जादुई गणना करें ⚡</button>

    <div id="result-area">
        <div class="big-card">
            <h2 id="res-years">0</h2>
            <p id="res-detail">0 Months | 0 Days</p>
        </div>

        <div class="stats-grid">
            <div class="mini-card"><i>❤️</i> <small style="display:block; font-size:10px; color:#94a3b8;">दिल की धड़कन</small><b id="stat-heart">0</b></div>
            <div class="mini-card"><i>🌬️</i> <small style="display:block; font-size:10px; color:#94a3b8;">कुल सांसें</small><b id="stat-breath">0</b></div>
        </div>

        <div class="insurance-box">
            <h4>🛡️ ₹1 करोड़ का सुरक्षा चक्र</h4>
            <p style="font-weight: 800; font-size: 20px; color: #2563eb; margin: 5px 0;" id="ins-price">₹450/महीना*</p>
            <p style="font-size: 11px;">आपकी उम्र बीमा शुरू करने के लिए एकदम सही है। कम प्रीमियम में बड़ी सुरक्षा पाएं!</p>
        </div>

        <div style="background: #fff7ed; padding: 15px; border-radius: 18px; color: #c2410c; font-weight: 600; font-size: 13px;" id="res-countdown"></div>

        <a href="#" id="whatsapp-btn" class="share-btn">WhatsApp पर शेयर करें 📱</a>
    </div>

    <div id="legal-box" class="legal-section">
        <h3 id="legal-title"></h3>
        <p id="legal-text"></p>
        <button onclick="document.getElementById('legal-box').style.display='none'" style="background:#6366f1; color:white; border:none; padding:5px 10px; border-radius:5px; cursor:pointer;">बंद करें</button>
    </div>

    <footer>
        <div style="margin-bottom: 10px;">
            <span class="footer-link" onclick="showLegal('privacy')">Privacy Policy</span>
            <span class="footer-link" onclick="showLegal('disclaimer')">Disclaimer</span>
        </div>
        <p>© 2026 AgeMaster Pro | Private & Secured 🔒</p>
    </footer>
</div>

<script>
function calculate() {
    const dobValue = document.getElementById('birth-date').value;
    if (!dobValue) { alert("कृपया तारीख चुनें!"); return; }

    const dob = new Date(dobValue);
    const now = new Date();

    // माइनस उम्र ठीक करने के लिए लॉजिक
    let years = now.getFullYear() - dob.getFullYear();
    let months = now.getMonth() - dob.getMonth();
    let days = now.getDate() - dob.getDate();

    if (days < 0) { months--; days += new Date(now.getFullYear(), now.getMonth(), 0).getDate(); }
    if (months < 0) { years--; months += 12; }
    if (years < 0) { alert("भविष्य की तारीख नहीं चुन सकते!"); return; }

    // Life Statistics
    const totalMin = Math.floor((now - dob) / (1000 * 60));
    document.getElementById('stat-heart').innerText = (totalMin * 72).toLocaleString();
    document.getElementById('stat-breath').innerText = (totalMin * 16).toLocaleString();

    // Insurance Premium
    let prem = years < 25 ? 450 : years < 35 ? 650 : 950;
    document.getElementById('ins-price').innerText = `₹${prem}/महीना*`;

    // Countdown
    let nextBday = new Date(now.getFullYear(), dob.getMonth(), dob.getDate());
    if (now > nextBday) nextBday.setFullYear(now.getFullYear() + 1);
    const diff = Math.ceil((nextBday - now) / (1000 * 60 * 60 * 24));

    document.getElementById('result-area').style.display = 'block';
    document.getElementById('res-years').innerText = years;
    document.getElementById('res-detail').innerText = `${months} महीने और ${days} दिन के हुए आप 🎈`;
    document.getElementById('res-countdown').innerText = diff === 365 || diff === 0 ? "🎉 आज आपका जन्मदिन है!" : `🎂 अगले जन्मदिन में ${diff} दिन बाकी हैं!`;

    const shareMsg = `मेरी उम्र ${years} साल है! ✨ मेरा दिल अब तक ${(totalMin * 72).toLocaleString()} बार धड़क चुका है। आप भी चेक करें: ${window.location.href}`;
    document.getElementById('whatsapp-btn').href = `https://api.whatsapp.com/send?text=${encodeURIComponent(shareMsg)}`;
}

function showLegal(type) {
    const box = document.getElementById('legal-box');
    const title = document.getElementById('legal-title');
    const text = document.getElementById('legal-text');
    box.style.display = 'block';
    if(type === 'privacy') {
        title.innerText = "Privacy Policy";
        text.innerText = "हम आपका कोई भी व्यक्तिगत डेटा या जन्मतिथि स्टोर नहीं करते हैं। यह गणना पूरी तरह से आपके ब्राउज़र में होती है।";
    } else {
        title.innerText = "Disclaimer";
        text.innerText = "यह कैलकुलेटर केवल मनोरंजन के लिए है। स्वास्थ्य या वित्तीय निर्णय लेने से पहले विशेषज्ञों से सलाह लें।";
    }
}
</script>
</body>
</html>
