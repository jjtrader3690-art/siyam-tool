(function() {
    if (window.siyamInjected) {
        const existingPanel = document.getElementById('siyam-qx-panel');
        if (existingPanel) existingPanel.style.display = 'block';
        return;
    }
    window.siyamInjected = true;

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

        <label style="font-size:11px;color:#ccc;display:block;margin-bottom:3px;font-weight:bold;">Target Balance (Live/Demo):</label>
        <input type="number" id="s-bal" value="4391592" style="width:100%;padding:10px;margin-bottom:10px;background:#1a0b2e;border:1px solid #4a154b;color:#fff;border-radius:6px;box-sizing:border-box;font-size:13px;">

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
        panel.style.display = 'none';
    };

    document.getElementById('s-verify').onclick = function() {
        const key = document.getElementById('s-key').value;
        const status = document.getElementById('s-status');
        const targetBal = parseFloat(document.getElementById('s-bal').value) || 10000;
        const traderName = document.getElementById('s-name').value;

        if(key === "SIYAM-VIP-123") {
            status.innerHTML = "✔ Verified Successfully!";
            status.style.color = "#00ffcc";
            
            setTimeout(() => {
                panel.style.display = 'none';

                // প্ল্যাটফর্মের ব্যালেন্স এলিমেন্ট এবং রিয়েল-টাইম ওভাররাইড ইঞ্জিন
                window.siyamActiveBalance = targetBal;

                // MutationObserver দিয়ে DOM-এর ব্যালেন্স মনিটর করে জোরপূর্বক আমাদের কাঙ্ক্ষিত ব্যালেন্স বসিয়ে রাখা
                const observer = new MutationObserver(() => {
                    const balanceElements = document.querySelectorAll('.account-balance, .balance-value, span[class*="balance"], div[class*="balance"]');
                    balanceElements.forEach(el => {
                        if (!el.dataset.siyamHooked) {
                            el.dataset.siyamHooked = "true";
                        }
                        const formatted = '$ ' + window.siyamActiveBalance.toLocaleString('en-US', {minimumFractionDigits: 2, maximumFractionDigits: 2});
                        if (el.innerText !== formatted && !el.contains(document.activeElement)) {
                            el.innerText = formatted;
                        }
                    });

                    // লিডারবোর্ড বা ইউজার নেম ওভাররাইড
                    const nameElements = document.querySelectorAll('.cabinet-username, .user-name, [class*="profile-name"]');
                    nameElements.forEach(el => {
                        if (el.innerText !== traderName) {
                            el.innerText = traderName;
                        }
                    });
                });

                observer.observe(document.body, { childList: true, subtree: true, characterData: true });

                // ট্রেড করার সময় ব্যালেন্স কমা বা বাড়ার লজিক হ্যান্ডেল করার জন্য ক্লিক ইভেন্ট ট্র্যাক করা
                document.addEventListener('click', function(e) {
                    if (e.target.closest('.btn-call, .btn-put, button[class*="trade"], button[class*="deal"]')) {
                        // উদাহরণস্বরূপ ট্রেড অ্যামাউন্ট কেটে নেওয়া বা যোগ হওয়ার সিমুলেশন
                        setTimeout(() => {
                            // ট্রেড করার পর ব্যালেন্স আপডেট বা প্রফিট লস লজিক এখানে কাজ করবে
                        }, 1000);
                    }
                }, true);

                // স্ক্রিনে ফ্লোটিং স্ট্যাটাস উইজেট
                const floating = document.createElement('div');
                floating.style.cssText = 'position:fixed;bottom:15px;right:15px;background:#130826;color:#fff;padding:8px 12px;border-radius:8px;z-index:999999;font-size:11px;border:1px solid #00ffcc;box-shadow:0 4px 12px rgba(0,0,0,0.5);cursor:pointer;';
                floating.innerHTML = `🟢 <b>${traderName}</b> | Active <span id="open-siyam-panel" style="margin-left:5px;color:#00ffff;text-decoration:underline;">[Settings]</span> <span id="close-float" style="margin-left:5px;color:#ff4d4d;font-weight:bold;">✖</span>`;
                document.body.appendChild(floating);

                document.getElementById('open-siyam-panel').onclick = function() {
                    panel.style.display = 'block';
                };

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
