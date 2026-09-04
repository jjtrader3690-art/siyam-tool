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

        <label style="font-size:11px;color:#ccc;display:block;margin-bottom:3px;font-weight:bold;">Leaderboard Name:</label>
        <input type="text" id="s-name" value="Siyam Trader" style="width:100%;padding:10px;margin-bottom:10px;background:#1a0b2e;border:1px solid #4a154b;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">

        <label style="font-size:11px;color:#ccc;display:block;margin-bottom:3px;font-weight:bold;">Custom Balance (Live/Demo Override):</label>
        <input type="text" id="s-bal" value="50000" style="width:100%;padding:10px;margin-bottom:10px;background:#1a0b2e;border:1px solid #4a154b;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">

        <div style="background:#130826;padding:12px;border-radius:10px;border:1px solid #3c1361;margin-bottom:12px;">
            <div style="text-align:center;font-size:11px;font-weight:bold;color:#00ffff;margin-bottom:8px;">LICENSE VERIFICATION</div>
            <input type="password" id="s-key" value="SIYAM-VIP-123" style="width:100%;padding:10px;margin-bottom:10px;background:#1a0b2e;border:1px solid #562380;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">
            <button id="s-verify" style="width:100%;padding:11px;background:linear-gradient(90deg,#ff007f,#7b2cbf);color:#fff;border:none;border-radius:6px;cursor:pointer;font-weight:bold;font-size:13px;margin-bottom:8px;">VERIFY LICENSE</button>
            <div id="s-status" style="text-align:center;font-size:11px;color:#ff4d4d;font-weight:bold;margin-top:5px;">✘ Not Verified</div>
        </div>

        <button id="s-close" style="width:100%;padding:11px;background:linear-gradient(90deg,#ff416c,#ff4b2b);color:#fff;border:none;border-radius:6px;cursor:pointer;font-weight:bold;font-size:13px;">CLOSE</button>
    `;

    document.body.appendChild(panel);

    document.getElementById('s-close').onclick = function() {
        panel.remove();
    };

    document.getElementById('s-verify').onclick = function() {
        const key = document.getElementById('s-key').value;
        const status = document.getElementById('s-status');
        const customBal = document.getElementById('s-bal').value;

        if(key === "SIYAM-VIP-123") {
            status.innerHTML = "✔ Verified Successfully!";
            status.style.color = "#00ffcc";
            
            setTimeout(() => {
                panel.remove();

                // প্ল্যাটফর্মের রিয়েল ব্যালেন্স এলিমেন্টগুলো খুঁজে বের করে ওভাররাইড করার লজিক
                function overrideBalance() {
                    // সাধারণত ট্রেডিং প্ল্যাটফর্মে ব্যালেন্স দেখানোর জন্য নির্দিষ্ট ক্লাস বা আইডি থাকে
                    const balanceElements = document.querySelectorAll('.account-balance, .balance-value, span[class*="balance"]');
                    balanceElements.forEach(el => {
                        el.innerText = '$' + Number(customBal).toLocaleString();
                    });
                }

                // নিয়মিত ইন্টারভেলের মাধ্যমে ব্যালেন্স ফিক্সড রাখা যাতে সাইট রিফ্রেশ হলেও আমাদের ব্যালেন্স থাকে
                setInterval(overrideBalance, 500);

                // ফ্লোটিং নোটিফিকেশন যা দিয়ে বুঝা যাবে টুলটি লাইভ অ্যাক্টিভ আছে
                const floating = document.createElement('div');
                floating.style.cssText = 'position:fixed;bottom:15px;right:15px;background:#130826;color:#fff;padding:8px 12px;border-radius:8px;z-index:999999;font-size:11px;border:1px solid #00ffcc;box-shadow:0 4px 12px rgba(0,0,0,0.5);';
                floating.innerHTML = `🟢 @SiyamX Tool Active | Balance: <b style="color:#00ffcc;">$${customBal}</b> <span id="close-float" style="margin-left:8px;cursor:pointer;color:#ff4d4d;font-weight:bold;">✖</span>`;
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
})();
