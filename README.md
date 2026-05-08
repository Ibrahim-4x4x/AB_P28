<!--DOCTYPE html-->
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>🔒 Secure Worksheet: Comparisons (Password Protected)</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: text;
        }

        body {
            background: #eef2f5;
            font-family: 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
            padding: 40px 20px;
            color: #1e2a3a;
            transition: filter 0.2s;
        }

        /* overlay for blocking when locked */
        .lock-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.92);
            backdrop-filter: blur(8px);
            z-index: 10000;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: monospace;
            flex-direction: column;
            gap: 25px;
            color: white;
        }

        .lock-card {
            background: #1e2f3c;
            padding: 35px 40px;
            border-radius: 48px;
            text-align: center;
            max-width: 450px;
            width: 90%;
            box-shadow: 0 25px 40px rgba(0,0,0,0.4);
            border: 1px solid #ffcd7e;
        }

        .lock-card h2 {
            font-size: 2rem;
            margin-bottom: 12px;
            color: #ffcd7e;
        }

        .lock-card input {
            width: 100%;
            padding: 14px 18px;
            font-size: 1.1rem;
            margin: 18px 0;
            border-radius: 60px;
            border: none;
            outline: none;
            text-align: center;
            font-family: monospace;
            background: #fef9e8;
        }

        .lock-card button {
            background: #ffb347;
            border: none;
            padding: 12px 28px;
            font-weight: bold;
            font-size: 1rem;
            border-radius: 60px;
            cursor: pointer;
            margin-top: 8px;
            transition: 0.1s;
        }

        .lock-card button:hover {
            background: #ff9f1c;
            transform: scale(0.97);
        }

        .error-msg {
            color: #ffaa88;
            margin-top: 10px;
            font-size: 0.85rem;
        }

        .worksheet-container {
            max-width: 1100px;
            margin: 0 auto;
            background: white;
            border-radius: 28px;
            box-shadow: 0 20px 35px -12px rgba(0, 0, 0, 0.15);
            overflow: hidden;
            padding: 30px 35px 45px;
            transition: all 0.2s;
        }

        h1 {
            font-size: 1.9rem;
            font-weight: 600;
            background: linear-gradient(135deg, #1f4870, #2a6f8f);
            background-clip: text;
            -webkit-background-clip: text;
            color: transparent;
            border-left: 6px solid #2a6f8f;
            padding-left: 20px;
            margin-bottom: 12px;
        }

        .sub {
            color: #4b6f8c;
            margin-bottom: 32px;
            font-size: 1rem;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 10px;
        }

        .activity-card {
            background: #fefefe;
            border-radius: 24px;
            margin-bottom: 40px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.03);
            border: 1px solid #e9edf2;
        }

        .activity-title {
            font-size: 1.5rem;
            font-weight: 600;
            background: #f8fafc;
            padding: 16px 24px;
            border-radius: 24px 24px 0 0;
            border-bottom: 2px solid #dee4ec;
            color: #0f3b4f;
        }

        .activity-content {
            padding: 20px 28px 28px 28px;
        }

        .radio-group {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            margin-bottom: 12px;
        }

        .sentence-item {
            background: #f9fafb;
            padding: 12px 16px;
            border-radius: 20px;
            border: 1px solid #eef2f6;
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            gap: 20px;
        }

        .sentence-text {
            flex: 2;
            font-size: 1rem;
            font-weight: 450;
        }

        .option-buttons {
            display: flex;
            gap: 20px;
            align-items: center;
        }

        .option-buttons label {
            display: inline-flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            background: white;
            padding: 6px 14px;
            border-radius: 60px;
            border: 1px solid #cfdfed;
        }

        .field-row {
            display: flex;
            flex-wrap: wrap;
            align-items: baseline;
            gap: 12px;
            margin-bottom: 18px;
            background: #ffffff;
            padding: 8px 12px;
            border-radius: 18px;
            border: 1px solid #e9edf2;
        }

        .field-label {
            font-weight: 600;
            min-width: 85px;
            color: #1f4e6e;
        }

        .field-input {
            flex: 2;
            padding: 10px 14px;
            border-radius: 40px;
            border: 1px solid #cddfea;
            font-family: monospace;
        }

        .btn-check {
            background: #1f5a7a;
            border: none;
            color: white;
            font-weight: 600;
            padding: 12px 28px;
            border-radius: 60px;
            font-size: 1rem;
            cursor: pointer;
            margin-top: 12px;
            margin-bottom: 18px;
        }

        .score-area {
            background: #eef3f7;
            border-radius: 28px;
            padding: 16px 25px;
            margin: 28px 0 10px;
            font-weight: 600;
            font-size: 1.2rem;
            text-align: center;
        }

        .feedback {
            font-size: 0.85rem;
            margin-top: 5px;
            color: #2c6e2c;
        }

        .example-text {
            color: #3b7c9c;
            background: #eef5f9;
            padding: 6px 12px;
            border-radius: 14px;
            font-size: 0.85rem;
        }

        button.small-hint {
            background: none;
            border: 1px solid #bdd7e7;
            padding: 6px 14px;
            border-radius: 30px;
            cursor: pointer;
        }

        @media (max-width: 700px) {
            .worksheet-container { padding: 20px; }
            .sentence-item { flex-direction: column; align-items: flex-start; }
        }
    </style>
</head>
<body>

<div class="worksheet-container" id="mainWorksheet">
    <h1>🔐 as ... as / not as ... as (Secure Mode)</h1>
    <div class="sub">Comparisons — auto-score + full lockdown: leaving/minimize/refresh triggers password block after results shown.</div>

    <!-- ACTIVITY 1 -->
    <div class="activity-card">
        <div class="activity-title">🎧 1. Listen and tick (✓)</div>
        <div class="activity-content">
            <div class="radio-group" id="listeningGroup">
                <div class="sentence-item"><div class="sentence-text">1️⃣ a. Julie is as old as Suha. &nbsp;&nbsp; b. Suha isn't as old as Julie.</div><div class="option-buttons"><label><input type="radio" name="q1" value="a"> a</label><label><input type="radio" name="q1" value="b"> b</label></div></div>
                <div class="sentence-item"><div class="sentence-text">2️⃣ a. Julie can play baseball as well as Suha. &nbsp;&nbsp; b. Suha doesn't play baseball as well as Julie.</div><div class="option-buttons"><label><input type="radio" name="q2" value="a"> a</label><label><input type="radio" name="q2" value="b"> b</label></div></div>
                <div class="sentence-item"><div class="sentence-text">3️⃣ a. Julie's hair is as dark as Suha's. &nbsp;&nbsp; b. Suha's hair isn't as fair as Julie's hair.</div><div class="option-buttons"><label><input type="radio" name="q3" value="a"> a</label><label><input type="radio" name="q3" value="b"> b</label></div></div>
                <div class="sentence-item"><div class="sentence-text">4️⃣ a. Julie isn't as tall as Suha. &nbsp;&nbsp; b. Suha is as tall as Julie.</div><div class="option-buttons"><label><input type="radio" name="q4" value="a"> a</label><label><input type="radio" name="q4" value="b"> b</label></div></div>
                <div class="sentence-item"><div class="sentence-text">5️⃣ a. Julie is as friendly as Suha. &nbsp;&nbsp; b. Suha isn't as friendly as Julie.</div><div class="option-buttons"><label><input type="radio" name="q5" value="a"> a</label><label><input type="radio" name="q5" value="b"> b</label></div></div>
                <div class="sentence-item"><div class="sentence-text">6️⃣ a. Julie isn't as funny as Suha. &nbsp;&nbsp; b. Suha is as shy as Julie.</div><div class="option-buttons"><label><input type="radio" name="q6" value="a"> a</label><label><input type="radio" name="q6" value="b"> b</label></div></div>
            </div>
            <div class="feedback" id="listeningFeedback"></div>
        </div>
    </div>

    <!-- ACTIVITY 2 -->
    <div class="activity-card">
        <div class="activity-title">✍️ 2. Rewrite with (not) as ... as</div>
        <div class="activity-content">
            <div class="example-text">📌 Example: Yousuf is tall, but Paul is much taller. → Yousuf isn't as tall as Paul.</div>
            <div class="field-row"><span class="field-label">2️⃣ You (13) / friend (13):</span> <input type="text" id="rewrite2" class="field-input" placeholder="You are as old as your friend."></div>
            <div class="field-row"><span class="field-label">3️⃣ Lucia / her sister (tidy):</span> <input type="text" id="rewrite3" class="field-input" placeholder="Lucia isn't as tidy as her sister."></div>
            <div class="field-row"><span class="field-label">4️⃣ Zaid / his brother (clever):</span> <input type="text" id="rewrite4" class="field-input" placeholder="Zaid is as clever as his brother."></div>
            <div class="field-row"><span class="field-label">5️⃣ I / you (confident):</span> <input type="text" id="rewrite5" class="field-input" placeholder="I'm as confident as you are."></div>
            <div id="rewriteFeedback" class="feedback"></div>
        </div>
    </div>

    <!-- ACTIVITY 3: Gabriel vs Omar -->
    <div class="activity-card">
        <div class="activity-title">📊 3. Compare Gabriel & Omar</div>
        <div class="activity-content">
            <div class="info-grid" style="display:flex; gap:20px; flex-wrap:wrap; margin-bottom:16px;">
                <div style="background:#f1f6fa; padding:15px; border-radius:24px; flex:1"><strong>📘 GABRIEL</strong><br>12 yo, 150 cm, not keen on sports, good at Maths, very hard-working, very bad at secrets</div>
                <div style="background:#f1f6fa; padding:15px; border-radius:24px; flex:1"><strong>⚽ OMAR</strong><br>13 yo, 150 cm, very keen on sports, not good at Maths, very hard-working, bad at secrets</div>
            </div>
            <div class="example-text">✅ (old) Gabriel → Gabriel isn't as old as Omar.</div>
            <div class="field-row"><span class="field-label">📏 (tall) Omar:</span> <input type="text" id="gabTall" class="field-input" placeholder="Omar is as tall as Gabriel."></div>
            <div class="field-row"><span class="field-label">⚽ (sports) Gabriel:</span> <input type="text" id="gabSports" class="field-input" placeholder="Gabriel isn't as keen on sports as Omar."></div>
            <div class="field-row"><span class="field-label">📐 (Maths) Omar:</span> <input type="text" id="gabMaths" class="field-input" placeholder="Omar isn't as good at Maths as Gabriel."></div>
            <div class="field-row"><span class="field-label">💪 (hard-working) Gabriel:</span> <input type="text" id="gabHard" class="field-input" placeholder="Gabriel is as hard-working as Omar."></div>
            <div class="field-row"><span class="field-label">🤐 (bad) Omar:</span> <input type="text" id="gabBad" class="field-input" placeholder="Omar isn't as bad at keeping secrets as Gabriel."></div>
            <div id="gabrielFeedback" class="feedback"></div>
        </div>
    </div>

    <!-- ACTIVITY 4: friends (free practice) -->
    <div class="activity-card">
        <div class="activity-title">👥 4. Compare two friends (practice)</div>
        <div class="activity-content">
            <div class="field-row"><span class="field-label">(old)</span> <input type="text" id="friendOld" class="field-input" placeholder="e.g., Tom isn't as old as Jerry."></div>
            <div class="field-row"><span class="field-label">(friendly)</span> <input type="text" id="friendFriendly" class="field-input" placeholder="... as friendly as ..."></div>
            <div class="field-row"><span class="field-label">(interested in art)</span> <input type="text" id="friendArt" class="field-input" placeholder="... as interested in art as ..."></div>
            <div class="field-row"><span class="field-label">(good at languages)</span> <input type="text" id="friendLang" class="field-input" placeholder="... as good at languages as ..."></div>
            <div class="field-row"><span class="field-label">(easy to get on with)</span> <input type="text" id="friendEasy" class="field-input" placeholder="... as easy to get on with as ..."></div>
            <div class="field-row"><span class="field-label">(confident)</span> <input type="text" id="friendConfident" class="field-input" placeholder="... as confident as ..."></div>
            <button type="button" id="showSampleFriends" class="small-hint">📖 Example sentences</button>
            <div id="sampleFriendsDiv" class="feedback" style="margin-top:10px;"></div>
        </div>
    </div>

    <div style="display:flex; justify-content:center; gap:20px; flex-wrap:wrap;">
        <button class="btn-check" id="checkAllBtn">✅ Auto-Correct & Score</button>
        <button class="btn-check" id="resetBtn" style="background:#5e7c8c;">⟳ Reset answers</button>
    </div>
    <div id="totalScoreArea" class="score-area">📊 Total score: -- / 15</div>
    <div class="sub" style="text-align:center;">⚠️ If you leave/minimize this tab AFTER viewing results, the page will lock permanently. Password required to resume.</div>
</div>

<script>
    // ---------- ANSWER KEYS (unchanged) ----------
    const listeningKey = { q1: 'a', q2: 'a', q3: 'b', q4: 'a', q5: 'a', q6: 'a' };
    const rewriteExpected = [
        { id: 'rewrite2', patterns: [/you are as old as your friend/i, /you're as old as your friend/i] },
        { id: 'rewrite3', patterns: [/lucia isn't as tidy as her sister/i, /lucia is not as tidy as her sister/i] },
        { id: 'rewrite4', patterns: [/zaid is as clever as his brother/i, /zaid's as clever as his brother/i] },
        { id: 'rewrite5', patterns: [/i'm as confident as you are/i, /i am as confident as you are/i] }
    ];
    const gabExpected = [
        { id: 'gabTall', patterns: [/omar is as tall as gabriel/i] },
        { id: 'gabSports', patterns: [/gabriel isn't as keen on sports as omar/i] },
        { id: 'gabMaths', patterns: [/omar isn't as good at maths as gabriel/i] },
        { id: 'gabHard', patterns: [/gabriel is as hard-working as omar/i, /gabriel is as hardworking as omar/i] },
        { id: 'gabBad', patterns: [/omar isn't as bad as gabriel/i, /omar isn't as bad at keeping secrets as gabriel/i] }
    ];

    function checkRewriteField(inputElem, patternsArr) {
        let val = inputElem.value.trim();
        if (val === "") return false;
        return patternsArr.some(p => p.test(val));
    }

    // GLOBAL STATE FOR LOCKDOWN
    let hasEverShownScore = false;         // once score displayed => lockdown mode active after visibility loss
    let isPageLocked = false;              // overlay active?
    let lockOverlay = null;

    // Password (teacher set: "teacher123" can be changed)
    const MASTER_PASSWORD = "teacher123";

    // Helper: create lock screen
    function showLockScreen(reason = "Activity locked due to tab change or minimize after results.") {
        if (isPageLocked) return;
        if (!hasEverShownScore) return;    // only lock if score was shown at least once (results obtained)
        isPageLocked = true;
        // remove existing overlay if any
        if (lockOverlay) lockOverlay.remove();
        lockOverlay = document.createElement('div');
        lockOverlay.className = 'lock-overlay';
        lockOverlay.innerHTML = `
            <div class="lock-card">
                <h2>🔒 Page Locked</h2>
                <p style="margin-bottom:10px;">${reason}</p>
                <p style="font-size:0.9rem; background:#00000055; padding:8px; border-radius:40px;">⚠️ You left the tab or minimized after seeing your score.<br>Worksheet is blocked for security.</p>
                <input type="password" id="unlockPassword" placeholder="Enter master password" autocomplete="off">
                <button id="unlockBtn">Unlock & Resume</button>
                <div id="lockError" class="error-msg"></div>
                <p style="font-size:11px; margin-top:16px;">Only teacher password can restore.</p>
            </div>
        `;
        document.body.appendChild(lockOverlay);
        const unlockBtn = document.getElementById('unlockBtn');
        const passInput = document.getElementById('unlockPassword');
        const errorDiv = document.getElementById('lockError');
        unlockBtn.addEventListener('click', () => {
            if (passInput.value === MASTER_PASSWORD) {
                // unlock and reset locked flag but keep score shown status? after unlock we allow work again but leftover answers remain.
                isPageLocked = false;
                if (lockOverlay) lockOverlay.remove();
                lockOverlay = null;
                // reset the visibility lock flag: we can still lock again if they minimize after result (but result already shown)
                // However to prevent re-lock directly we keep hasEverShownScore true but allow interaction. fine.
                // Also clean any pending visibility trigger after unlock
            } else {
                errorDiv.innerText = "❌ Incorrect password. Access denied.";
            }
        });
        passInput.addEventListener('keypress', (e) => { if(e.key === 'Enter') unlockBtn.click(); });
    }

    // Page Visibility API: student minimizes tab or switches to another tab
    function handleVisibilityChange() {
        if (document.hidden && hasEverShownScore && !isPageLocked) {
            // Student minimized / left tab AFTER getting score
            showLockScreen("⛔ You minimized or switched tabs after viewing your results. Access blocked.");
        }
    }

    // Beforeunload: if they try to refresh/close after score shown -> lock on next load (remember via sessionStorage)
    window.addEventListener('beforeunload', function (e) {
        if (hasEverShownScore && !isPageLocked) {
            // Mark that a lockdown should be triggered if page reloads or leaves
            sessionStorage.setItem('pending_lock_after_score', 'true');
            e.preventDefault();
            e.returnValue = "⚠️ You have viewed your score. Leaving or refreshing will lock this worksheet. Password required to continue.";
            return e.returnValue;
        }
    });

    // On page load, check if we had pending lockdown after score (meaning user refreshed after seeing results)
    function checkPendingLockOnLoad() {
        if (sessionStorage.getItem('pending_lock_after_score') === 'true') {
            sessionStorage.removeItem('pending_lock_after_score');
            hasEverShownScore = true;   // we know results were previously shown
            showLockScreen("You refreshed/reloaded the page after seeing your final score. Activity locked for integrity.");
        }
    }

    // additional: detect if user tries to navigate away using back/forward? we use popstate
    window.addEventListener('popstate', function() {
        if (hasEverShownScore && !isPageLocked) {
            showLockScreen("Navigation detected after final score. Page locked.");
        }
    });

    // disable copy paste on password field? not needed.
    // COMPUTE SCORE and set flag if score computed at least once
    function computeScores() {
        let listeningScore = 0;
        for (let i = 1; i <= 6; i++) {
            let selected = document.querySelector(`input[name="q${i}"]:checked`);
            if (selected && selected.value === listeningKey[`q${i}`]) listeningScore++;
        }
        let rewriteScore = 0;
        rewriteExpected.forEach(item => {
            let inputField = document.getElementById(item.id);
            if (inputField && checkRewriteField(inputField, item.patterns)) rewriteScore++;
        });
        let gabScore = 0;
        gabExpected.forEach(item => {
            let inputField = document.getElementById(item.id);
            if (inputField && checkRewriteField(inputField, item.patterns)) gabScore++;
        });
        let total = listeningScore + rewriteScore + gabScore;
        let totalMax = 15;
        displayListeningFeedback(listeningScore);
        displayRewriteFeedback(rewriteScore);
        displayGabrielFeedback(gabScore);
        document.getElementById('totalScoreArea').innerHTML = `📊 Total score: ${total} / ${totalMax}  (Listening: ${listeningScore}/6 | Rewrite: ${rewriteScore}/4 | Gabriel/Omar: ${gabScore}/5)`;
        
        // IMPORTANT: once student clicks "Auto-Correct & Score" at least once, we set hasEverShownScore = true
        if (!hasEverShownScore) {
            hasEverShownScore = true;
            // also store a session flag to remember score was shown (for reload protection)
            sessionStorage.setItem('score_was_shown', 'true');
        }
        return total;
    }

    function displayListeningFeedback(score) {
        const container = document.getElementById('listeningFeedback');
        container.innerHTML = `🎧 Listening score: ${score}/6. Correct answers: 1a,2a,3b,4a,5a,6a.`;
    }
    function displayRewriteFeedback(score) {
        document.getElementById('rewriteFeedback').innerHTML = `✍️ Rewrite score: ${score}/4.`;
    }
    function displayGabrielFeedback(score) {
        document.getElementById('gabrielFeedback').innerHTML = `📊 Gabriel & Omar section: ${score}/5.`;
    }

    // Reset function (clear answers but keep worksheet active)
    function resetAll() {
        if (isPageLocked) return;
        for (let i = 1; i <= 6; i++) {
            let radios = document.querySelectorAll(`input[name="q${i}"]`);
            radios.forEach(r => r.checked = false);
        }
        const rewriteIds = ['rewrite2','rewrite3','rewrite4','rewrite5'];
        rewriteIds.forEach(id => document.getElementById(id).value = '');
        const gabIds = ['gabTall','gabSports','gabMaths','gabHard','gabBad'];
        gabIds.forEach(id => document.getElementById(id).value = '');
        const friendIds = ['friendOld','friendFriendly','friendArt','friendLang','friendEasy','friendConfident'];
        friendIds.forEach(id => document.getElementById(id).value = '');
        document.getElementById('listeningFeedback').innerHTML = '';
        document.getElementById('rewriteFeedback').innerHTML = '';
        document.getElementById('gabrielFeedback').innerHTML = '';
        document.getElementById('totalScoreArea').innerHTML = '📊 Total score: -- / 15';
        // Do NOT reset hasEverShownScore because score might be recalculated later, but user might avoid showing score. Fine.
    }

    document.getElementById('checkAllBtn').addEventListener('click', () => {
        computeScores();
    });
    document.getElementById('resetBtn').addEventListener('click', resetAll);
    document.getElementById('showSampleFriends').addEventListener('click', () => {
        const sampleDiv = document.getElementById('sampleFriendsDiv');
        sampleDiv.innerHTML = `📌 Example: (old) → "Anna isn't as old as Luis."<br>✨ (friendly) "Maria is as friendly as Sofia."<br>✨ (interested in art) "Tom isn't as interested in art as Leo."`;
    });

    // BLOCK RIGHT-CLICK & F12 / Ctrl+U / Ctrl+R / Ctrl+Shift+I to prevent circumventing lock
    document.addEventListener('contextmenu', (e) => e.preventDefault());
    document.addEventListener('keydown', (e) => {
        if (e.key === 'F12' || (e.ctrlKey && e.shiftKey && (e.key === 'I' || e.key === 'J')) || (e.ctrlKey && e.key === 'u') || (e.ctrlKey && e.key === 'r') || (e.ctrlKey && e.shiftKey && e.key === 'R') || (e.metaKey && e.key === 'r')) {
            e.preventDefault();
            e.stopPropagation();
            return false;
        }
    });

    // Initialize & recover from previous score state
    if (sessionStorage.getItem('score_was_shown') === 'true') {
        hasEverShownScore = true;
        // Check if page was reloaded after score, and also lock if needed (but we don't auto-lock unless user minimizes after)
        // but we also handle pending lock after beforeunload
    }
    checkPendingLockOnLoad();

    // monitor visibility (minimize or tab switch)
    document.addEventListener('visibilitychange', handleVisibilityChange);

    // extra: disable developer console shortcuts via repeated interval? not needed.
    console.log("Secure worksheet active: password lock on tab minimize/leave after score.");
</script>
</body>
</html>
