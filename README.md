<!--DOCTYPE html-->
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>🔒 Secure Worksheet: Anti-Leave + Password Block (Enhanced)</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #eef2f5;
            font-family: 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
            padding: 40px 20px;
            color: #1e2a3a;
            transition: filter 0.2s;
        }

        /* Blur overlay when locked */
        body.locked .worksheet-container {
            filter: blur(5px);
            pointer-events: none;
            user-select: none;
        }

        body.locked .lock-overlay {
            display: flex;
        }

        .lock-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(8px);
            z-index: 10000;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', system-ui;
        }

        .lock-card {
            background: white;
            max-width: 460px;
            width: 90%;
            padding: 32px 28px;
            border-radius: 48px;
            text-align: center;
            box-shadow: 0 25px 45px rgba(0,0,0,0.3);
            animation: fadeInUp 0.2s ease;
        }

        .lock-card h2 {
            font-size: 1.8rem;
            margin-bottom: 12px;
            color: #c4452c;
        }

        .lock-card p {
            margin-bottom: 24px;
            color: #2c3e4e;
        }

        .lock-card input {
            width: 100%;
            padding: 14px 18px;
            font-size: 1rem;
            border: 2px solid #d4dee8;
            border-radius: 60px;
            margin-bottom: 18px;
            outline: none;
            text-align: center;
            letter-spacing: 1px;
        }

        .lock-card input:focus {
            border-color: #1f5a7a;
        }

        .lock-card button {
            background: #1f5a7a;
            border: none;
            color: white;
            font-weight: bold;
            padding: 12px 24px;
            border-radius: 60px;
            font-size: 1rem;
            cursor: pointer;
            width: 100%;
            transition: 0.1s;
        }

        .lock-card button:hover {
            background: #0f415b;
        }

        .error-msg {
            color: #d9534f;
            margin-top: 12px;
            font-size: 0.85rem;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* rest of original worksheet styles */
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

        .option-buttons input {
            margin: 0;
            accent-color: #2a6f8f;
            width: 18px;
            height: 18px;
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
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .btn-check:hover {
            background: #0f415b;
            transform: scale(0.98);
        }

        .score-area {
            background: #eef3f7;
            border-radius: 28px;
            padding: 16px 25px;
            margin: 28px 0 10px;
            font-weight: 600;
            font-size: 1.2rem;
            text-align: center;
            border: 1px solid #cde1ec;
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
            font-size: 0.75rem;
        }

        .info-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 24px;
            margin: 20px 0;
        }

        .student-card {
            flex: 1;
            background: #f1f6fa;
            border-radius: 24px;
            padding: 18px 20px;
            border-left: 6px solid #ffbe5e;
        }
        .student-card h3 { margin-bottom: 12px; }
        .student-card ul { list-style: none; padding-left: 0; }
        .student-card li { margin: 10px 0; display: flex; gap: 6px; }
        .label-badge { font-weight: 600; min-width: 110px; }

        @media (max-width: 700px) {
            .worksheet-container { padding: 20px; }
            .sentence-item { flex-direction: column; align-items: flex-start; }
        }
    </style>
</head>
<body>

<!-- LOCK OVERLAY (password wall) - enhanced with features from best Exam General -->
<div id="lockOverlay" class="lock-overlay">
    <div class="lock-card">
        <h2>🔒 Activity Locked</h2>
        <p>⚠️ You left the page, minimized the tab, completed the activity, or the window lost focus.<br>Enter teacher password to continue.</p>
        <input type="password" id="passwordInput" placeholder="Enter password" autocomplete="off">
        <button id="unlockBtn">Unlock Worksheet</button>
        <div id="lockErrorMsg" class="error-msg"></div>
    </div>
</div>

<div class="worksheet-container">
    <h1>📝 as ... as / not as ... as</h1>
    <div class="sub">Comparisons — listen, rewrite & compare | 🔐 Auto-lock on page leave/minimize + Result lock + Window blur + Visibility API</div>

    <!-- ACTIVITY 1 -->
    <div class="activity-card">
        <div class="activity-title">🎧 1. Listen and tick (✓) the correct sentence</div>
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
        <div class="activity-title">✍️ 2. Rewrite with (not) as ... as + underlined adjective</div>
        <div class="activity-content">
            <div class="example-text">📌 Example: Yousuf is tall, but Paul is much taller. → Yousuf isn't as tall as Paul.</div>
            <div style="margin-top: 20px;">
                <div class="field-row"><span class="field-label">2️⃣ You (13) / friend (13):</span> <input type="text" id="rewrite2" class="field-input" placeholder="You are as old as your friend."></div>
                <div class="field-row"><span class="field-label">3️⃣ Lucia / her sister (tidy):</span> <input type="text" id="rewrite3" class="field-input" placeholder="Lucia isn't as tidy as her sister."></div>
                <div class="field-row"><span class="field-label">4️⃣ Zaid / his brother (clever):</span> <input type="text" id="rewrite4" class="field-input" placeholder="Zaid is as clever as his brother."></div>
                <div class="field-row"><span class="field-label">5️⃣ I / you (confident):</span> <input type="text" id="rewrite5" class="field-input" placeholder="I'm as confident as you are."></div>
            </div>
            <div id="rewriteFeedback" class="feedback"></div>
        </div>
    </div>

    <!-- ACTIVITY 3 -->
    <div class="activity-card">
        <div class="activity-title">📊 3. Compare Gabriel & Omar</div>
        <div class="activity-content">
            <div class="info-grid">
                <div class="student-card"><h3>📘 GABRIEL</h3><ul><li><span class="label-badge">Age:</span> 12</li><li><span class="label-badge">Height:</span> 150 cm</li><li><span class="label-badge">Sports:</span> not keen</li><li><span class="label-badge">Maths:</span> good</li><li><span class="label-badge">Hard-working:</span> very</li><li><span class="label-badge">Secrets:</span> very bad</li></ul></div>
                <div class="student-card"><h3>⚽ OMAR</h3><ul><li><span class="label-badge">Age:</span> 13</li><li><span class="label-badge">Height:</span> 150 cm</li><li><span class="label-badge">Sports:</span> very keen</li><li><span class="label-badge">Maths:</span> not good</li><li><span class="label-badge">Hard-working:</span> very</li><li><span class="label-badge">Secrets:</span> bad</li></ul></div>
            </div>
            <div class="example-text">✅ (old) Gabriel → Gabriel isn't as old as Omar. (given)</div>
            <div class="field-row"><span class="field-label">📏 (tall) Omar:</span> <input type="text" id="gabTall" class="field-input" placeholder="Omar is as tall as Gabriel."></div>
            <div class="field-row"><span class="field-label">⚽ (sports) Gabriel:</span> <input type="text" id="gabSports" class="field-input" placeholder="Gabriel isn't as keen on sports as Omar."></div>
            <div class="field-row"><span class="field-label">📐 (Maths) Omar:</span> <input type="text" id="gabMaths" class="field-input" placeholder="Omar isn't as good at Maths as Gabriel."></div>
            <div class="field-row"><span class="field-label">💪 (hard-working) Gabriel:</span> <input type="text" id="gabHard" class="field-input" placeholder="Gabriel is as hard-working as Omar."></div>
            <div class="field-row"><span class="field-label">🤐 (bad) Omar:</span> <input type="text" id="gabBad" class="field-input" placeholder="Omar isn't as bad at keeping secrets as Gabriel."></div>
            <div id="gabrielFeedback" class="feedback"></div>
        </div>
    </div>

    <!-- ACTIVITY 4 -->
    <div class="activity-card">
        <div class="activity-title">👥 4. Compare two friends (Practice)</div>
        <div class="activity-content">
            <div class="field-row"><span class="field-label">(old)</span> <input type="text" id="friendOld" class="field-input" placeholder="e.g., Tom isn't as old as Jerry."></div>
            <div class="field-row"><span class="field-label">(friendly)</span> <input type="text" id="friendFriendly" class="field-input" placeholder="... as friendly as ..."></div>
            <div class="field-row"><span class="field-label">(interested in art)</span> <input type="text" id="friendArt" class="field-input" placeholder="... as interested in art as ..."></div>
            <div class="field-row"><span class="field-label">(good at languages)</span> <input type="text" id="friendLang" class="field-input" placeholder="... as good at languages as ..."></div>
            <div class="field-row"><span class="field-label">(easy to get on with)</span> <input type="text" id="friendEasy" class="field-input" placeholder="... as easy to get on with as ..."></div>
            <div class="field-row"><span class="field-label">(confident)</span> <input type="text" id="friendConfident" class="field-input" placeholder="... as confident as ..."></div>
            <button type="button" id="showSampleFriends" class="small-hint">📖 Show examples</button>
            <div id="sampleFriendsDiv" class="feedback" style="margin-top: 12px;"></div>
        </div>
    </div>

    <div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
        <button class="btn-check" id="checkAllBtn">✅ Auto-Correct & Score</button>
        <button class="btn-check" id="resetBtn" style="background: #5e7c8c;">⟳ Reset all answers</button>
    </div>
    <div id="totalScoreArea" class="score-area">📊 Total score: -- / 15</div>
</div>

<script>
   /* --- GLOBAL SECURITY - STARTS IMMEDIATELY --- */

// Prevents right-click from the first second
document.oncontextmenu = () => { alert("Right-click disabled"); return false; };

// Locks if they even THINK about leaving the tab
document.addEventListener("visibilitychange", () => {
    if (document.hidden) lockPage();
});

// The actual lock function
function lockPage() {
    document.getElementById('lockOverlay').style.display = 'flex';
    document.body.style.filter = "blur(10px)";
    localStorage.setItem('worksheet_status', 'locked');
}
    // This starts the moment the browser finishes loading the elements
window.onload = function() {
    
    // 1. Check if they were already locked from a previous visit
    if (localStorage.getItem('worksheet_status') === 'locked') {
        lockPage();
    }

    // 2. Start monitoring tab-switching IMMEDIATELY
    document.addEventListener('visibilitychange', function() {
        // No "if started" check here - if they leave, it locks.
        if (document.hidden) {
            console.log("Security Trigger: Tab Hidden");
            lockPage();
        }
    });

    // 3. Start monitoring window focus IMMEDIATELY
    window.addEventListener("blur", function() {
        console.log("Security Trigger: Window Lost Focus");
        lockPage();
    });
};
    // ======================== PASSWORD & LOCK MECHANISM (ENHANCED with features from best Exam General) ========================
    // Teacher password (as per best Exam General style, but keeping original theme)
    const TEACHER_PASSWORD = "5533";   // default secure word (can be changed)
    
    let isLocked = false;
    let lockTriggeredByResult = false;
    let resultWasClicked = false;
    
    const lockOverlay = document.getElementById('lockOverlay');
    const passwordInput = document.getElementById('passwordInput');
    const unlockBtn = document.getElementById('unlockBtn');
    const lockErrorMsg = document.getElementById('lockErrorMsg');
    
    // Function to lock the page (show password wall, blur worksheet)
    function lockPage(reason = "generic") {
        if (isLocked) return;
        isLocked = true;
        document.body.classList.add('locked');
        lockOverlay.style.display = 'flex';
        console.log(`🔒 Locked due to: ${reason}`);
        lockErrorMsg.innerText = '';
        passwordInput.value = '';
        // Additionally, store lock state in localStorage to survive reloads (as per best Exam General)
        localStorage.setItem("worksheet_status", "locked");
    }
    
    // Unlock the page
    function unlockPage() {
        if (!isLocked) return;
        const entered = passwordInput.value.trim();
        if (entered === TEACHER_PASSWORD) {
            isLocked = false;
            lockTriggeredByResult = false;
            resultWasClicked = false;
            document.body.classList.remove('locked');
            lockOverlay.style.display = 'none';
            lockErrorMsg.innerText = '';
            localStorage.removeItem("worksheet_status");
        } else {
            lockErrorMsg.innerText = '❌ Incorrect password. Access denied.';
            passwordInput.value = '';
        }
    }
    
    unlockBtn.addEventListener('click', unlockPage);
    passwordInput.addEventListener('keypress', (e) => {
        if (e.key === 'Enter') unlockPage();
    });
    
    // ========== Enhanced Security: PAGE LEAVE / MINIMIZE / WINDOW BLUR & VISIBILITY from best Exam General ==========
    // 1) Visibility API: if student minimizes tab OR switches to another tab → lock immediately
    // 2) Window blur: detect if window loses focus (clicking another app, popup, etc.) → lock
    // 3) beforeunload detection + sessionStorage to preserve lock on reload
    
    let hasAnswersBeforeLeave = false;
    function checkAnyAnswer() {
        // check radios
        for (let i = 1; i <= 6; i++) {
            let radios = document.querySelectorAll(`input[name="q${i}"]`);
            for (let r of radios) if (r.checked) return true;
        }
        const textInputs = document.querySelectorAll('input[type="text"], input.field-input');
        for (let inp of textInputs) if (inp.value.trim() !== "") return true;
        return false;
    }
    
    function updateAnswerFlag() { hasAnswersBeforeLeave = checkAnyAnswer(); }
    document.addEventListener('change', updateAnswerFlag);
    document.addEventListener('input', updateAnswerFlag);
    
    // Security: visibility change (tab minimize/switch)
    document.addEventListener('visibilitychange', function() {
        if (document.hidden && !isLocked && hasAnswersBeforeLeave) {
            lockPage('tab minimize / switch (visibility API)');
            // Optional alert behavior from best Exam General
            alert("Activity Locked: You left the page during the exam.");
        }
    });
    
    // Security: window loses focus (blur)
    window.addEventListener("blur", function() {
        if (!isLocked && hasAnswersBeforeLeave && document.getElementById('checkAllBtn')) {
            lockPage('window lost focus (blur event)');
            alert("Activity Locked: Window lost focus.");
        }
    });
    
    // beforeunload: set pending lock flag for reload/close
    window.addEventListener('beforeunload', function(e) {
        if (hasAnswersBeforeLeave && !isLocked) {
            sessionStorage.setItem('pendingLockOnReload', 'true');
        }
    });
    
    // On page load, check if we need to lock due to previous reload / localStorage locked state
    window.addEventListener('load', function() {
        updateAnswerFlag();
        // Check localStorage lock status from previous lock (best exam general feature)
        if (localStorage.getItem('worksheet_status') === 'locked') {
            if (!isLocked) lockPage('persisted lock from localStorage');
        }
        if (sessionStorage.getItem('pendingLockOnReload') === 'true') {
            sessionStorage.removeItem('pendingLockOnReload');
            if (!isLocked && hasAnswersBeforeLeave) {
                lockPage('page reload/leave detected');
            }
        }
    });
    
    // ========== RESULT ICON / BUTTON BEHAVIOR: LOCK AFTER SHOWING SCORES ==========
    // Scoring logic preserved from original worksheet
    
    const listeningKey = { q1: 'a', q2: 'a', q3: 'b', q4: 'a', q5: 'a', q6: 'a' };
    const rewriteExpected = [
        { id: 'rewrite2', patterns: [/you are as old as your friend/i, /you're as old as your friend/i, /you are as old as your friend\.?$/i] },
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
    
    function computeAndDisplayScores() {
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
        document.getElementById('listeningFeedback').innerHTML = `🎧 Listening: ${listeningScore}/6 ${listeningScore===6 ? '✅' : ''}`;
        document.getElementById('rewriteFeedback').innerHTML = `✍️ Rewrite: ${rewriteScore}/4`;
        document.getElementById('gabrielFeedback').innerHTML = `📊 Gabriel & Omar: ${gabScore}/5`;
        document.getElementById('totalScoreArea').innerHTML = `📊 Total score: ${total} / ${totalMax}  (Listening: ${listeningScore}/6 | Rewrite: ${rewriteScore}/4 | Compare: ${gabScore}/5)`;
        return total;
    }
    
    // new version: show score AND lock after if answers exist (Result lock as per best exam general)
    function onResultClick() {
        if (isLocked) return;
        computeAndDisplayScores();
        if (hasAnswersBeforeLeave || checkAnyAnswer()) {
            lockTriggeredByResult = true;
            lockPage('Result button clicked - activity completed');
            alert("Activity Completed and Locked. Please ask teacher to unlock.");
        }
    }
    
    // Replace original click with new locking result button
    const freshCheckBtn = document.getElementById('checkAllBtn');
    // Clone to avoid multiple listeners
    const newBtn = freshCheckBtn.cloneNode(true);
    freshCheckBtn.parentNode.replaceChild(newBtn, freshCheckBtn);
    newBtn.id = 'checkAllBtn';
    newBtn.addEventListener('click', onResultClick);
    
    // Reset button: clear fields and unlock if possible (but remain locked state requires password)
    function resetAllFields() {
        for (let i = 1; i <= 6; i++) {
            document.querySelectorAll(`input[name="q${i}"]`).forEach(r => r.checked = false);
        }
        ['rewrite2','rewrite3','rewrite4','rewrite5'].forEach(id => document.getElementById(id).value = '');
        ['gabTall','gabSports','gabMaths','gabHard','gabBad'].forEach(id => document.getElementById(id).value = '');
        ['friendOld','friendFriendly','friendArt','friendLang','friendEasy','friendConfident'].forEach(id => document.getElementById(id).value = '');
        document.getElementById('listeningFeedback').innerHTML = '';
        document.getElementById('rewriteFeedback').innerHTML = '';
        document.getElementById('gabrielFeedback').innerHTML = '';
        document.getElementById('sampleFriendsDiv').innerHTML = '';
        document.getElementById('totalScoreArea').innerHTML = '📊 Total score: -- / 15';
        updateAnswerFlag();
        if (isLocked) {
            alert('All answers cleared. To unlock worksheet please use teacher password.');
        } else {
            // optionally reset any lock flags
        }
    }
    document.getElementById('resetBtn').addEventListener('click', resetAllFields);
    
    // sample friends
    document.getElementById('showSampleFriends').addEventListener('click', () => {
        document.getElementById('sampleFriendsDiv').innerHTML = `📌 Example: (old) → "Anna isn't as old as Luis."<br>✨ (friendly) → "Maria is as friendly as Sofia."`;
    });
    
    // block right-click and developer shortcuts for security (standard)
    document.addEventListener('contextmenu', e => e.preventDefault());
    document.addEventListener('keydown', function(e) {
        if (e.key === 'F12' || (e.ctrlKey && e.shiftKey && (e.key === 'I' || e.key === 'J')) || (e.ctrlKey && e.key === 'u') || (e.ctrlKey && e.key === 'r') || (e.metaKey && e.key === 'r')) {
            e.preventDefault();
            if ((e.ctrlKey && e.key === 'r') || (e.metaKey && e.key === 'r')) {
                e.preventDefault();
                return false;
            }
        }
    });
    
    // Initialize answer flag and check for any pre-existing lock from earlier session
    updateAnswerFlag();
    if (localStorage.getItem('worksheet_status') === 'locked') {
        lockPage('initial load from localStorage locked state');
    }
</script>
</body>
</html>
