(function() {
    if (document.getElementById('siyam-qx-panel')) {
        document.getElementById('siyam-qx-panel').remove();
    }

    const panel = document.createElement('div');
    panel.id = 'siyam-qx-panel';
    panel.style.cssText = 'position:fixed;top:10px;left:50%;transform:translateX(-50%);width:92%;max-width:420px;background:#0d061a;color:#fff;padding:15px;border-radius:14px;box-shadow:0 10px 30px rgba(0,0,0,0.8);z-index:999999;font-family:sans-serif;border:1px solid #7b2cbf;max-height:95vh;overflow-y:auto;';

    panel.innerHTML = `
        <div style="background:#130826;padding:8px;border-radius:8px;text-align:center;margin-bottom:12px;border:1px dashed #ff4d4d;">
            <span style="font-size:12px;color:#ff4d4d;font-weight:bold;">Developer: @SiyamX</span><br>
            <span style="font-size:10px;color:#aaa;">Buying from others will result in fraud!</span>
        </div>

        <div style="text-align:center;margin-bottom:10px;">
            <div style="width:45px;height:45px;background:linear-gradient(45deg,#ff007f,#7b2cbf);border-radius:50%;display:inline-flex;align-items:center;justify-content:center;font-weight:bold;font-size:18px;color:#fff;box-shadow:0 0 10px #ff007f;">SX</div>
        </div>

        <label style="font-size:11px;color:#ccc;display:block;margin-bottom:3px;font-weight:bold;">Leaderboard Name:</label>
        <input type="text" id="s-name" placeholder="Enter Name" value="Siyam Trader" style="width:100%;padding:10px;margin-bottom:10px;background:#1a0b2e;border:1px solid #4a154b;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">

        <label style="font-size:11px;color:#ccc;display:block;margin-bottom:3px;font-weight:bold;">Leaderboard Balance:</label>
        <div style="position:relative;margin-bottom:10px;">
            <input type="text" id="s-bal" placeholder="Enter Balance" value="$50,000" style="width:100%;padding:10px;background:#1a0b2e;border:1px solid #4a154b;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">
        </div>

        <label style="font-size:11px;color:#ccc;display:block;margin-bottom:3px;font-weight:bold;">Profile Photo Link:</label>
        <input type="text" id="s-img" placeholder="Enter Profile Photo Link" style="width:100%;padding:10px;margin-bottom:10px;background:#1a0b2e;border:1px solid #4a154b;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">

        <label style="font-size:11px;color:#ccc;display:block;margin-bottom:3px;font-weight:bold;">Country Flag:</label>
        <select id="s-country" style="width:100%;padding:10px;margin-bottom:12px;background:#1a0b2e;border:1px solid #4a154b;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">
            <option value="bd">🇧🇩 Bangladesh</option>
            <option value="in">🇮🇳 India</option>
            <option value="pk">🇵🇰 Pakistan</option>
        </select>

        <div style="background:#130826;padding:12px;border-radius:10px;border:1px solid #3c1361;margin-bottom:12px;">
            <div style="text-align:center;font-size:11px;font-weight:bold;color:#00ffff;margin-bottom:8px;letter-spacing:1px;">LICENSE VERIFICATION</div>
            <input type="password" id="s-key" placeholder="Enter your license key" value="SIYAM-VIP-123" style="width:100%;padding:10px;margin-bottom:10px;background:#1a0b2e;border:1px solid #562380;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">
            
            <button id="s-verify" style="width:100%;padding:11px;background:linear-gradient(90deg,#ff007f,#7b2cbf);color:#fff;border:none;border-radius:6px;cursor:pointer;font-weight:bold;font-size:13px;margin-bottom:8px;box-shadow:0 4px 15px rgba(255,0,127,0.4);">VERIFY LICENSE</button>
            <button style="width:100%;padding:10px;background:#00b074;color:#fff;border:none;border-radius:6px;cursor:pointer;font-weight:bold;font-size:12px;margin-bottom:8px;">ONLINE PAYMENT ACTIVE</button>
            
            <div id="s-status" style="text-align:center;font-size:11px;color:#ff4d4d;font-weight:bold;margin-top:5px;">✘ Not Verified</div>
        </div>

        <button id="s-save" style="width:100%;padding:11px;background:#2a1b4e;color:#ccc;border:1px solid #4a2c8c;border-radius:6px;cursor:pointer;font-weight:bold;font-size:13px;margin-bottom:8px;">SAVE SETTINGS</button>
        <button id="s-close" style="width:100%;padding:11px;background:linear-gradient(90deg,#ff416c,#ff4b2b);color:#fff;border:none;border-radius:6px;cursor:pointer;font-weight:bold;font-size:13px;">CLOSE</button>
    `;

    document.body.appendChild(panel);

    // ক্লোজ বাটন
    document.getElementById('s-close').onclick = function() {
        panel.remove();
    };

    // ভেরিফাই বাটন ক্লিক করলে যা হবে
    document.getElementById('s-verify').onclick = function() {
        const key = document.getElementById('s-key').value;
        const status = document.getElementById('s-status');
        const name = document.getElementById('s-name').value;
        const bal = document.getElementById('s-bal').value;

        if(key === "SIYAM-VIP-123") { // আপনার ইচ্ছামতো লাইসেন্স কি এখানে দিতে পারবেন
            status.innerHTML = "✔ Verified Successfully!";
            status.style.color = "#00ffcc";
            
            // সফল হওয়ার পর ফর্মটি অটোমেটিক হটে যাবে এবং ট্রেড করার সুবিধা দিবে
            setTimeout(() => {
                panel.remove();
                
                // স্ক্রিনে ছোট একটি ফ্লোটিং স্ট্যাটাস দেখাবে
                const floating = document.createElement('div');
                floating.style.cssText = 'position:fixed;bottom:15px;right:15px;background:#130826;color:#fff;padding:8px 12px;border-radius:8px;z-index:999999;font-size:11px;border:1px solid #00ffcc;box-shadow:0 4px 12px rgba(0,0,0,0.5);';
                floating.innerHTML = `🟢 <b>${name}</b> | Bal: <b style="color:#00ffcc;">${bal}</b> <span id="close-float" style="margin-left:8px;cursor:pointer;color:#ff4d4d;font-weight:bold;">✖</span>`;
                document.body.appendChild(floating);

                document.getElementById('close-float').onclick = function() {
                    floating.remove();
                };
            }, 1000);

        } else {
            status.innerHTML = "✘ Invalid License Key!";
            status.style.color = "#ff4d4d";
        }
    };
    
    document.getElementById('s-save').onclick = function() {
        alert("Settings saved successfully!");
        panel.remove();
    };
})();
