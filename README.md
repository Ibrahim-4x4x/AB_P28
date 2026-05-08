<!--DOCTYPE html-->
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>🔐 Protected Worksheet | as...as Comparisons</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: #eef2f5;
            font-family: 'Segoe UI', Roboto, 'Helvetica Neue', sans-serif;
            padding: 0;
            margin: 0;
            min-height: 100vh;
            position: relative;
        }

        /* ---------- PASSWORD MODAL (full page overlay) ---------- */
        .password-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            backdrop-filter: blur(8px);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 2000;
            transition: opacity 0.3s ease;
        }

        .password-card {
            background: white;
            max-width: 450px;
            width: 90%;
            padding: 2rem 2rem 2.2rem;
            border-radius: 48px;
            text-align: center;
            box-shadow: 0 25px 40px rgba(0, 0, 0, 0.3);
            border: 1px solid rgba(255,255,240,0.3);
        }

        .password-card h2 {
            font-size: 2rem;
            margin-bottom: 0.5rem;
            color: #1f4870;
        }

        .password-card p {
            color: #4a627a;
            margin-bottom: 1.8rem;
            font-size: 0.95rem;
        }

        .password-card input {
            width: 100%;
            padding: 14px 18px;
            font-size: 1rem;
            border: 2px solid #cddfea;
            border-radius: 60px;
            outline: none;
            margin-bottom: 1.2rem;
            transition: 0.2s;
            text-align: center;
            letter-spacing: 1px;
        }

        .password-card input:focus {
            border-color: #2a6f8f;
            box-shadow: 0 0 0 3px rgba(42,111,143,0.2);
        }

        .password-card button {
            background: #1f5a7a;
            border: none;
            color: white;
            font-weight: 700;
            font-size: 1.1rem;
            padding: 12px 20px;
            border-radius: 60px;
            width: 100%;
            cursor: pointer;
            transition: 0.15s;
            margin-bottom: 12px;
        }

        .password-card button:hover {
            background: #0f415b;
            transform: scale(0.98);
        }

        .error-msg {
            color: #c23b22;
            font-size: 0.85rem;
            margin-top: 8px;
            font-weight: 500;
        }

        .hint-text {
            font-size: 0.75rem;
            color: #6b8baa;
            margin-top: 16px;
            border-top: 1px solid #e2edf5;
            padding-top: 12px;
        }

        /* ---------- MAIN WORKSHEET (initially hidden) ---------- */
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
            transition: 0.1s;
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

        .btn-check, .btn-reset {
            background: #1f5a7a;
            border: none;
            color: white;
            font-weight: 600;
            padding: 12px 28px;
            border-radius: 60px;
            font-size: 1rem;
            cursor: pointer;
            transition: 0.15s;
            margin-top: 12px;
            margin-bottom: 18px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .btn-reset {
            background: #5e7c8c;
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
        }

        .feedback {
            font-size: 0.85rem;
            margin-top: 5px;
            color: #2c6e2c;
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

        .student-card h3 {
            font-size: 1.5rem;
            margin-bottom: 12px;
        }

        .student-card ul {
            list-style: none;
            padding-left: 0;
        }

        .student-card li {
            margin: 10px 0;
            display: flex;
            gap: 6px;
        }

        .label-badge {
            font-weight: 600;
            min-width: 110px;
            color: #1e4663;
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

        @media (max-width: 700px) {
            .worksheet-container {
                padding: 20px;
            }
            .sentence-item {
                flex-direction: column;
                align-items: flex-start;
            }
        }

        .hidden-worksheet {
            display: none;
        }
    </style>
</head>
<body>

<!-- PASSWORD LOCK SCREEN -->
<div id="passwordOverlay" class="password-overlay">
    <div class="password-card">
        <h2>🔐 Worksheet Access</h2>
        <p>Enter the password to begin the activity.<br>You can complete the exercises only once per session.</p>
        <input type="password" id="passwordInput" placeholder="Enter password" autocomplete="off">
        <button id="unlockBtn">Unlock & Start</button>
        <div id="passwordError" class="error-msg"></div>
        <div class="hint-text">💡 Hint: The password is <strong>worksheet2025</strong></div>
    </div>
</div>

<!-- MAIN WORKSHEET CONTENT (hidden until password success) -->
<div id="mainWorksheet" style="padding: 40px 20px; display: none;">
    <div class="worksheet-container">
        <h1>📝 as ... as / not as ... as</h1>
        <div class="sub">Comparisons — listen, rewrite & compare | auto score check</div>

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
                    <div class="field-row"><span class="field-label">2️⃣ You (13) / friend (13):</span> <input type="text" id="rewrite2" class="field-input" placeholder="e.g., You are as old as your friend."></div>
                    <div class="field-row"><span class="field-label">3️⃣ Lucia / her sister (tidy):</span> <input type="text" id="rewrite3" class="field-input" placeholder="Lucia isn't as tidy as her sister."></div>
                    <div class="field-row"><span class="field-label">4️⃣ Zaid / his brother (clever):</span> <input type="text" id="rewrite4" class="field-input" placeholder="Zaid is as clever as his brother."></div>
                    <div class="field-row"><span class="field-label">5️⃣ I / you (confident):</span> <input type="text" id="rewrite5" class="field-input" placeholder="I'm as confident as you are."></div>
                </div>
                <div id="rewriteFeedback" class="feedback"></div>
            </div>
        </div>

        <!-- ACTIVITY 3: GABRIEL & OMAR -->
        <div class="activity-card">
            <div class="activity-title">📊 3. Compare Gabriel & Omar — write sentences with (not) as ... as</div>
            <div class="activity-content">
                <div class="info-grid">
                    <div class="student-card"><h3>📘 GABRIEL</h3><ul><li><span class="label-badge">Age:</span> 12 years old</li><li><span class="label-badge">Height:</span> 150 cm</li><li><span class="label-badge">Sports:</span> not keen on sports</li><li><span class="label-badge">Maths:</span> good at Maths</li><li><span class="label-badge">Hard-working:</span> very hard-working</li><li><span class="label-badge">Keeping secrets:</span> very bad</li></ul></div>
                    <div class="student-card"><h3>⚽ OMAR</h3><ul><li><span class="label-badge">Age:</span> 13 years old</li><li><span class="label-badge">Height:</span> 150 cm</li><li><span class="label-badge">Sports:</span> very keen on sports</li><li><span class="label-badge">Maths:</span> not good at Maths</li><li><span class="label-badge">Hard-working:</span> very hard-working</li><li><span class="label-badge">Keeping secrets:</span> bad</li></ul></div>
                </div>
                <div class="example-text">✅ (old) Gabriel → Gabriel isn't as old as Omar. (given)</div>
                <div class="prompt-field">
                    <div class="field-row"><span class="field-label">📏 (tall) Omar:</span> <input type="text" id="gabTall" class="field-input" placeholder="Omar is as tall as Gabriel."></div>
                    <div class="field-row"><span class="field-label">⚽ (sports) Gabriel:</span> <input type="text" id="gabSports" class="field-input" placeholder="Gabriel isn't as keen on sports as Omar."></div>
                    <div class="field-row"><span class="field-label">📐 (Maths) Omar:</span> <input type="text" id="gabMaths" class="field-input" placeholder="Omar isn't as good at Maths as Gabriel."></div>
                    <div class="field-row"><span class="field-label">💪 (hard-working) Gabriel:</span> <input type="text" id="gabHard" class="field-input" placeholder="Gabriel is as hard-working as Omar."></div>
                    <div class="field-row"><span class="field-label">🤐 (bad) Omar:</span> <input type="text" id="gabBad" class="field-input" placeholder="Omar isn't as bad at keeping secrets as Gabriel."></div>
                </div>
                <div id="gabrielFeedback" class="feedback"></div>
            </div>
        </div>

        <!-- ACTIVITY 4: FRIENDS (practice, not scored) -->
        <div class="activity-card">
            <div class="activity-title">👥 4. Compare two friends — use (not) as ... as</div>
            <div class="activity-content">
                <p style="margin-bottom: 14px;">Write your own comparison sentences about two real or imaginary friends.</p>
                <div class="field-row"><span class="field-label">(old)</span> <input type="text" id="friendOld" class="field-input" placeholder="e.g., Tom isn't as old as Jerry."></div>
                <div class="field-row"><span class="field-label">(friendly)</span> <input type="text" id="friendFriendly" class="field-input" placeholder="... as friendly as ..."></div>
                <div class="field-row"><span class="field-label">(interested in art)</span> <input type="text" id="friendArt" class="field-input" placeholder="... as interested in art as ..."></div>
                <div class="field-row"><span class="field-label">(good at languages)</span> <input type="text" id="friendLang" class="field-input" placeholder="... as good at languages as ..."></div>
                <div class="field-row"><span class="field-label">(easy to get on with)</span> <input type="text" id="friendEasy" class="field-input" placeholder="... as easy to get on with as ..."></div>
                <div class="field-row"><span class="field-label">(confident)</span> <input type="text" id="friendConfident" class="field-input" placeholder="... as confident as ..."></div>
                <button type="button" id="showSampleFriends" class="small-hint">📖 Show example sentences</button>
                <div id="sampleFriendsDiv" class="feedback" style="margin-top: 12px;"></div>
            </div>
        </div>

        <div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
            <button class="btn-check" id="checkAllBtn">✅ Auto-Correct & Score</button>
            <button class="btn-reset" id="resetBtn">⟳ Reset all answers</button>
        </div>
        <div id="totalScoreArea" class="score-area">📊 Total score: -- / 15</div>
        <div class="sub" style="text-align: center; margin-top: 8px;">✔️ Activity 4 is practice (not scored). Click check for detailed correction.</div>
    </div>
</div>

<script>
    // PASSWORD AND ONE-TIME ACCESS LOGIC
    (function() {
        const CORRECT_PASSWORD = "2026";
        const STORAGE_KEY = "worksheet_unlocked_v1";

        // Check if already unlocked in sessionStorage (avoid password re-entry on refresh)
        const alreadyUnlocked = sessionStorage.getItem(STORAGE_KEY);
        const overlay = document.getElementById("passwordOverlay");
        const worksheetDiv = document.getElementById("mainWorksheet");

        if (alreadyUnlocked === "true") {
            // Session already authorized: show worksheet directly
            if (overlay) overlay.style.display = "none";
            if (worksheetDiv) worksheetDiv.style.display = "block";
        } else {
            // wait for password submission
            const unlockBtn = document.getElementById("unlockBtn");
            const passwordInput = document.getElementById("passwordInput");
            const errorSpan = document.getElementById("passwordError");

            function attemptUnlock() {
                const entered = passwordInput.value.trim();
                if (entered === CORRECT_PASSWORD) {
                    // correct password: hide overlay, show worksheet, store session flag
                    sessionStorage.setItem(STORAGE_KEY, "true");
                    overlay.style.display = "none";
                    worksheetDiv.style.display = "block";
                    errorSpan.innerText = "";
                } else {
                    errorSpan.innerText = "❌ Incorrect password. Access denied. Hint: worksheet2025";
                    passwordInput.value = "";
                    passwordInput.focus();
                }
            }

            unlockBtn.addEventListener("click", attemptUnlock);
            passwordInput.addEventListener("keypress", function(e) {
                if (e.key === "Enter") attemptUnlock();
            });
        }

        // Also prevent any attempt to disable overlay via inspect tricks (visual only, fine)
        // Additional: block right-click and devtools inside worksheet for security (optional, same as previous)
        document.addEventListener('contextmenu', function(e) {
            if (worksheetDiv.style.display === "block") {
                e.preventDefault();
                return false;
            }
        });
        document.addEventListener('keydown', function(e) {
            if (worksheetDiv.style.display === "block") {
                if (e.key === 'F12' || (e.ctrlKey && e.shiftKey && (e.key === 'I' || e.key === 'J')) ||
                    (e.ctrlKey && e.key === 'u') || (e.ctrlKey && e.key === 'r') ||
                    (e.ctrlKey && e.shiftKey && e.key === 'R') || (e.metaKey && e.key === 'r')) {
                    e.preventDefault();
                    e.stopPropagation();
                    return false;
                }
            }
        });
    })();

    // ---------- ANSWER KEYS AND AUTO-CORRECT (same as original) ----------
    const listeningKey = { q1: 'a', q2: 'a', q3: 'b', q4: 'a', q5: 'a', q6: 'a' };
    const rewriteExpected = [
        { id: 'rewrite2', patterns: [/you are as old as your friend/i, /you're as old as your friend/i, /you are as old as your friend\.?$/i] },
        { id: 'rewrite3', patterns: [/lucia isn't as tidy as her sister/i, /lucia is not as tidy as her sister/i, /lucia isn’t as tidy as her sister/i] },
        { id: 'rewrite4', patterns: [/zaid is as clever as his brother/i, /zaid's as clever as his brother/i] },
        { id: 'rewrite5', patterns: [/i'm as confident as you are/i, /i am as confident as you are/i, /i'm as confident as you$/i] }
    ];
    const gabExpected = [
        { id: 'gabTall', patterns: [/omar is as tall as gabriel/i, /omar is as tall as gabriel\.?$/i] },
        { id: 'gabSports', patterns: [/gabriel isn't as keen on sports as omar/i, /gabriel is not as keen on sports as omar/i, /gabriel isn’t as keen on sports as omar/i] },
        { id: 'gabMaths', patterns: [/omar isn't as good at maths as gabriel/i, /omar is not as good at maths as gabriel/i, /omar isn’t as good at maths/i] },
        { id: 'gabHard', patterns: [/gabriel is as hard-working as omar/i, /gabriel is as hardworking as omar/i, /gabriel’s as hard-working as omar/i] },
        { id: 'gabBad', patterns: [/omar isn't as bad as gabriel/i, /omar isn't as bad at keeping secrets as gabriel/i, /omar is not as bad as gabriel/i, /omar is not as bad at keeping secrets as gabriel/i] }
    ];

    function checkRewriteField(inputElem, patternsArr) {
        let val = inputElem.value.trim();
        if (val === "") return false;
        for (let pattern of patternsArr) {
            if (pattern.test(val)) return true;
        }
        return false;
    }

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
        let totalMax = 6 + 4 + 5;
        displayListeningFeedback(listeningScore, 6);
        displayRewriteFeedback(rewriteScore, 4);
        displayGabrielFeedback(gabScore, 5);
        document.getElementById('totalScoreArea').innerHTML = `📊 Total score: ${listeningScore + rewriteScore + gabScore} / ${totalMax}  (Listening: ${listeningScore}/6 | Rewrite: ${rewriteScore}/4 | Compare: ${gabScore}/5)`;
    }

    function displayListeningFeedback(score, max) {
        const container = document.getElementById('listeningFeedback');
        let incorrectList = [];
        for (let i = 1; i <= 6; i++) {
            let selected = document.querySelector(`input[name="q${i}"]:checked`);
            let userVal = selected ? selected.value : "none";
            if (userVal !== listeningKey[`q${i}`]) incorrectList.push(`${i} (✓ ${listeningKey[`q${i}`].toUpperCase()})`);
        }
        if (incorrectList.length === 0 && score === max) container.innerHTML = `✅ Listening: ${score}/${max} — all correct!`;
        else container.innerHTML = `🎧 Listening score: ${score}/${max}. ${incorrectList.length ? `Mistakes on questions: ${incorrectList.join(', ')}.` : ''} <br> <span style="font-size:0.8rem;">✔ Correct answers: 1a, 2a, 3b, 4a, 5a, 6a</span>`;
    }

    function displayRewriteFeedback(score, max) {
        const feedbackDiv = document.getElementById('rewriteFeedback');
        let details = [];
        const ids = ['rewrite2', 'rewrite3', 'rewrite4', 'rewrite5'];
        const expectedStrings = ["You are as old as your friend.", "Lucia isn't as tidy as her sister.", "Zaid is as clever as his brother.", "I'm as confident as you are."];
        ids.forEach((id, idx) => {
            let inputField = document.getElementById(id);
            let isCorrect = inputField ? checkRewriteField(inputField, rewriteExpected[idx].patterns) : false;
            if (!isCorrect && inputField && inputField.value.trim() !== "") details.push(`${idx+2} ✘ (expected: "${expectedStrings[idx]}")`);
            else if (!isCorrect && (!inputField || inputField.value.trim() === "")) details.push(`${idx+2} ✘ (empty)`);
            else details.push(`${idx+2} ✓`);
        });
        feedbackDiv.innerHTML = `✍️ Rewrite score: ${score}/${max}<br> ${details.join(' | ')}`;
    }

    function displayGabrielFeedback(score, max) {
        const gabDiv = document.getElementById('gabrielFeedback');
        let rows = [
            { id: 'gabTall', label: 'tall (Omar)', expected: 'Omar is as tall as Gabriel.' },
            { id: 'gabSports', label: 'sports (Gabriel)', expected: 'Gabriel isn\'t as keen on sports as Omar.' },
            { id: 'gabMaths', label: 'Maths (Omar)', expected: 'Omar isn\'t as good at Maths as Gabriel.' },
            { id: 'gabHard', label: 'hard-working (Gabriel)', expected: 'Gabriel is as hard-working as Omar.' },
            { id: 'gabBad', label: 'bad (Omar)', expected: 'Omar isn\'t as bad at keeping secrets as Gabriel.' }
        ];
        let statuses = [];
        rows.forEach(row => {
            let inp = document.getElementById(row.id);
            let patternSet = gabExpected.find(p => p.id === row.id)?.patterns || [];
            let correct = inp ? checkRewriteField(inp, patternSet) : false;
            statuses.push(`${row.label}: ${correct ? '✓' : '✘'}`);
        });
        gabDiv.innerHTML = `📊 Gabriel & Omar section score: ${score}/${max}<br> ${statuses.join(' | ')}<br><span style="font-size:0.75rem;">✔ Expected answers: Omar is as tall as Gabriel. / Gabriel isn't as keen on sports as Omar. / Omar isn't as good at Maths as Gabriel. / Gabriel is as hard-working as Omar. / Omar isn't as bad at keeping secrets as Gabriel.</span>`;
    }

    document.getElementById('showSampleFriends')?.addEventListener('click', () => {
        const sampleDiv = document.getElementById('sampleFriendsDiv');
        sampleDiv.innerHTML = `📌 Example comparisons:<br>✨ (old) → "Anna isn't as old as Luis."<br>✨ (friendly) → "Maria is as friendly as Sofia."<br>✨ (interested in art) → "Tom isn't as interested in art as Leo."<br>✨ (good at languages) → "Elena is as good at languages as Kim."<br>✨ (easy to get on with) → "Carlos is as easy to get on with as David."<br>✨ (confident) → "Maya isn't as confident as Nina."`;
    });

    function resetAll() {
        for (let i = 1; i <= 6; i++) {
            let radios = document.querySelectorAll(`input[name="q${i}"]`);
            radios.forEach(radio => radio.checked = false);
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
        document.getElementById('sampleFriendsDiv').innerHTML = '';
        document.getElementById('totalScoreArea').innerHTML = '📊 Total score: -- / 15';
    }

    const checkBtn = document.getElementById('checkAllBtn');
    const resetBtn = document.getElementById('resetBtn');
    if (checkBtn) checkBtn.addEventListener('click', computeScores);
    if (resetBtn) resetBtn.addEventListener('click', resetAll);
</script>
</body>
</html>
