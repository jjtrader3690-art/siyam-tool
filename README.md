(function() {
    if (document.getElementById('my-custom-dashboard')) {
        document.getElementById('my-custom-dashboard').remove();
    }

    const box = document.createElement('div');
    box.id = 'my-custom-dashboard';
    box.style.cssText = 'position:fixed;top:20px;right:20px;width:320px;background:#1e1e1e;color:#fff;padding:20px;border-radius:10px;box-shadow:0 5px 15px rgba(0,0,0,0.5);z-index:999999;font-family:sans-serif;';
    
    box.innerHTML = `
        <h3 style="margin:0 0 10px;font-size:16px;color:#4CAF50;">আমার ডেমো টুল</h3>
        <p style="font-size:13px;color:#bbb;margin:0 0 15px;">লাইসেন্স কি দিয়ে ব্যালেন্স দেখুন:</p>
        <input type="text" id="license-key" placeholder="যেমন: ADMIN-123" style="width:100%;padding:8px;margin-bottom:10px;background:#333;border:1px solid #555;color:#fff;border-radius:5px;box-sizing:border-box;">
        <button id="check-btn" style="width:100%;padding:8px;background:#4CAF50;color:#fff;border:none;border-radius:5px;cursor:pointer;font-weight:bold;">লগইন করুন</button>
        <div id="result-area" style="margin-top:12px;font-size:13px;"></div>
        <button id="close-btn" style="width:100%;padding:5px;background:#d32f2f;color:#fff;border:none;border-radius:5px;cursor:pointer;margin-top:10px;">বন্ধ করুন</button>
    `;

    document.body.appendChild(box);

    document.getElementById('check-btn').onclick = function() {
        const key = document.getElementById('license-key').value;
        const resultDiv = document.getElementById('result-area');
        
        if(key === "ADMIN-123") {
            resultDiv.innerHTML = `<span style="color:#4CAF50;">সফল! লাইভ ব্যালেন্স: $1,000 (ডেমো)</span>`;
        } else {
            resultDiv.innerHTML = `<span style="color:#ff5252;">ভুল লাইসেন্স কি!</span>`;
        }
    };

    document.getElementById('close-btn').onclick = function() {
        box.remove();
    };
})();
