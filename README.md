<!--DOCTYPE html-->
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Comparisons Worksheet: (not) as ... as | Auto-Correcting Activities</title>
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
            transition: 0.1s;
        }

        .activity-title {
            font-size: 1.5rem;
            font-weight: 600;
            background: #f8fafc;
            padding: 16px 24px;
            border-radius: 24px 24px 0 0;
            border-bottom: 2px solid #dee4ec;
            color: #0f3b4f;
            letter-spacing: -0.2px;
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

        .rewrite-input {
            width: 100%;
            padding: 12px 16px;
            border-radius: 18px;
            border: 1.5px solid #dce5ec;
            font-size: 0.95rem;
            font-family: monospace;
            background: white;
            transition: 0.2s;
            margin-top: 6px;
        }

        .rewrite-input:focus {
            border-color: #2a6f8f;
            outline: none;
            box-shadow: 0 0 0 3px rgba(42, 111, 143, 0.2);
        }

        .info-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 24px;
            margin: 20px 0 20px;
        }

        .student-card {
            flex: 1;
            background: #f1f6fa;
            border-radius: 24px;
            padding: 18px 20px;
            border-left: 6px solid #ffbe5e;
            box-shadow: 0 2px 6px rgba(0,0,0,0.05);
        }

        .student-card h3 {
            font-size: 1.5rem;
            margin-bottom: 12px;
            font-weight: 700;
        }

        .student-card ul {
            list-style: none;
            padding-left: 0;
        }

        .student-card li {
            margin: 10px 0;
            display: flex;
            align-items: baseline;
            gap: 6px;
        }

        .label-badge {
            font-weight: 600;
            min-width: 110px;
            color: #1e4663;
        }

        .prompt-field {
            margin-top: 16px;
            margin-bottom: 20px;
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
            transition: 0.15s;
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

        .incorrect-feedback {
            color: #c23b22;
        }

        hr {
            margin: 15px 0;
            border-color: #e2e8f0;
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
    </style>
</head>
<body>
<div class="worksheet-container">
    <h1>📝 as ... as / not as ... as</h1>
    <div class="sub">Comparisons — listen, rewrite & compare | auto score check</div>

    <!-- ========== ACTIVITY 1: LISTEN & TICK ========= -->
    <div class="activity-card">
        <div class="activity-title">🎧 1. Listen and tick (✓) the correct sentence</div>
        <div class="activity-content">
            <div class="radio-group" id="listeningGroup">
                <!-- item 1 -->
                <div class="sentence-item" data-q="1">
                    <div class="sentence-text">1️⃣ a. Julie is as old as Suha. &nbsp;&nbsp; b. Suha isn't as old as Julie.</div>
                    <div class="option-buttons">
                        <label><input type="radio" name="q1" value="a"> a</label>
                        <label><input type="radio" name="q1" value="b"> b</label>
                    </div>
                </div>
                <!-- item 2 -->
                <div class="sentence-item" data-q="2">
                    <div class="sentence-text">2️⃣ a. Julie can play baseball as well as Suha. &nbsp;&nbsp; b. Suha doesn't play baseball as well as Julie.</div>
                    <div class="option-buttons"><label><input type="radio" name="q2" value="a"> a</label><label><input type="radio" name="q2" value="b"> b</label></div>
                </div>
                <!-- item 3 -->
                <div class="sentence-item" data-q="3">
                    <div class="sentence-text">3️⃣ a. Julie's hair is as dark as Suha's. &nbsp;&nbsp; b. Suha's hair isn't as fair as Julie's hair.</div>
                    <div class="option-buttons"><label><input type="radio" name="q3" value="a"> a</label><label><input type="radio" name="q3" value="b"> b</label></div>
                </div>
                <!-- item 4 -->
                <div class="sentence-item" data-q="4">
                    <div class="sentence-text">4️⃣ a. Julie isn't as tall as Suha. &nbsp;&nbsp; b. Suha is as tall as Julie.</div>
                    <div class="option-buttons"><label><input type="radio" name="q4" value="a"> a</label><label><input type="radio" name="q4" value="b"> b</label></div>
                </div>
                <!-- item 5 -->
                <div class="sentence-item" data-q="5">
                    <div class="sentence-text">5️⃣ a. Julie is as friendly as Suha. &nbsp;&nbsp; b. Suha isn't as friendly as Julie.</div>
                    <div class="option-buttons"><label><input type="radio" name="q5" value="a"> a</label><label><input type="radio" name="q5" value="b"> b</label></div>
                </div>
                <!-- item 6 -->
                <div class="sentence-item" data-q="6">
                    <div class="sentence-text">6️⃣ a. Julie isn't as funny as Suha. &nbsp;&nbsp; b. Suha is as shy as Julie.</div>
                    <div class="option-buttons"><label><input type="radio" name="q6" value="a"> a</label><label><input type="radio" name="q6" value="b"> b</label></div>
                </div>
            </div>
            <div class="feedback" id="listeningFeedback"></div>
        </div>
    </div>

    <!-- ========== ACTIVITY 2: REWRITE SENTENCES ========= -->
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

    <!-- ========== ACTIVITY 3: GABRIEL vs OMAR (data comparison) ========= -->
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

    <!-- ========== ACTIVITY 4: COMPARE TWO FRIENDS (open practice) ========= -->
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
            <button type="button" id="showSampleFriends" class="small-hint" style="margin-left: 8px;">📖 Show example sentences</button>
            <div id="sampleFriendsDiv" class="feedback" style="margin-top: 12px;"></div>
        </div>
    </div>

    <div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
        <button class="btn-check" id="checkAllBtn">✅ Auto-Correct & Score</button>
        <button class="btn-check" id="resetBtn" style="background: #5e7c8c;">⟳ Reset all answers</button>
    </div>
    <div id="totalScoreArea" class="score-area">📊 Total score: -- / 15</div>
    <div class="sub" style="text-align: center; margin-top: 8px;">✔️ Activity 4 is practice (not scored). Click check for detailed correction on sections 1-3.</div>
</div>

<script>
    // ---------- ANSWER KEYS ----------
    // Listening correct answers (based on typical logical comparisons & common patterns)
    // answer key: 1a, 2a, 3b, 4a, 5a, 6a
    const listeningKey = { q1: 'a', q2: 'a', q3: 'b', q4: 'a', q5: 'a', q6: 'a' };
    
    // Rewrite expected answers (flexible matching)
    const rewriteExpected = [
        { id: 'rewrite2', patterns: [/you are as old as your friend/i, /you're as old as your friend/i, /you are as old as your friend\.?$/i] },
        { id: 'rewrite3', patterns: [/lucia isn't as tidy as her sister/i, /lucia is not as tidy as her sister/i, /lucia isn’t as tidy as her sister/i] },
        { id: 'rewrite4', patterns: [/zaid is as clever as his brother/i, /zaid's as clever as his brother/i] },
        { id: 'rewrite5', patterns: [/i'm as confident as you are/i, /i am as confident as you are/i, /i'm as confident as you$/i] }
    ];
    
    // Gabriel & Omar expected answers (flexible)
    const gabExpected = [
        { id: 'gabTall', patterns: [/omar is as tall as gabriel/i, /omar is as tall as gabriel\.?$/i] },
        { id: 'gabSports', patterns: [/gabriel isn't as keen on sports as omar/i, /gabriel is not as keen on sports as omar/i, /gabriel isn’t as keen on sports as omar/i] },
        { id: 'gabMaths', patterns: [/omar isn't as good at maths as gabriel/i, /omar is not as good at maths as gabriel/i, /omar isn’t as good at maths/i] },
        { id: 'gabHard', patterns: [/gabriel is as hard-working as omar/i, /gabriel is as hardworking as omar/i, /gabriel’s as hard-working as omar/i] },
        { id: 'gabBad', patterns: [/omar isn't as bad as gabriel/i, /omar isn't as bad at keeping secrets as gabriel/i, /omar is not as bad as gabriel/i, /omar is not as bad at keeping secrets as gabriel/i] }
    ];
    
    // helper: check rewrite
    function checkRewriteField(inputElem, patternsArr) {
        let val = inputElem.value.trim();
        if (val === "") return false;
        for (let pattern of patternsArr) {
            if (pattern.test(val)) return true;
        }
        return false;
    }
    
    // compute scores
    function computeScores() {
        // 1. Listening (6 items)
        let listeningScore = 0;
        for (let i = 1; i <= 6; i++) {
            let radioName = `q${i}`;
            let selected = document.querySelector(`input[name="${radioName}"]:checked`);
            if (selected && selected.value === listeningKey[radioName]) {
                listeningScore++;
            }
        }
        let listeningMax = 6;
        
        // 2. Rewrite (4 items)
        let rewriteScore = 0;
        rewriteExpected.forEach(item => {
            let inputField = document.getElementById(item.id);
            if (inputField && checkRewriteField(inputField, item.patterns)) rewriteScore++;
        });
        let rewriteMax = 4;
        
        // 3. Gabriel & Omar (5 items: tall, sports, maths, hard-working, bad) note: old is example not graded.
        let gabScore = 0;
        gabExpected.forEach(item => {
            let inputField = document.getElementById(item.id);
            if (inputField && checkRewriteField(inputField, item.patterns)) gabScore++;
        });
        let gabMax = 5;
        
        let total = listeningScore + rewriteScore + gabScore;
        let totalMax = listeningMax + rewriteMax + gabMax;
        
        // update feedback texts with detailed marking
        displayListeningFeedback(listeningScore, listeningMax);
        displayRewriteFeedback(rewriteScore, rewriteMax);
        displayGabrielFeedback(gabScore, gabMax);
        
        document.getElementById('totalScoreArea').innerHTML = `📊 Total score: ${total} / ${totalMax}  (Listening: ${listeningScore}/${listeningMax} | Rewrite: ${rewriteScore}/${rewriteMax} | Compare Gabriel/Omar: ${gabScore}/${gabMax})`;
        return {total, totalMax};
    }
    
    function displayListeningFeedback(score, max) {
        const container = document.getElementById('listeningFeedback');
        let incorrectList = [];
        for (let i = 1; i <= 6; i++) {
            let radioName = `q${i}`;
            let selected = document.querySelector(`input[name="${radioName}"]:checked`);
            let userVal = selected ? selected.value : "none";
            let correct = listeningKey[radioName];
            if (userVal !== correct) {
                incorrectList.push(`${i} (✓ ${correct.toUpperCase()})`);
            }
        }
        if (incorrectList.length === 0 && score === max) {
            container.innerHTML = `✅ Listening: ${score}/${max} — all correct!`;
            container.style.color = "#2c6e2c";
        } else {
            container.innerHTML = `🎧 Listening score: ${score}/${max}. ${incorrectList.length ? `Mistakes on questions: ${incorrectList.join(', ')}.` : ''} <br> <span style="font-size:0.8rem;">✔ Correct answers: 1a, 2a, 3b, 4a, 5a, 6a</span>`;
            container.style.color = "#a45d2e";
        }
    }
    
    function displayRewriteFeedback(score, max) {
        const feedbackDiv = document.getElementById('rewriteFeedback');
        let details = [];
        const ids = ['rewrite2', 'rewrite3', 'rewrite4', 'rewrite5'];
        const expectedStrings = [
            "You are as old as your friend.",
            "Lucia isn't as tidy as her sister.",
            "Zaid is as clever as his brother.",
            "I'm as confident as you are."
        ];
        ids.forEach((id, idx) => {
            let inputField = document.getElementById(id);
            let isCorrect = false;
            if (inputField) isCorrect = checkRewriteField(inputField, rewriteExpected[idx].patterns);
            if (!isCorrect && inputField && inputField.value.trim() !== "") {
                details.push(`${idx+2} ✘ (expected: "${expectedStrings[idx]}")`);
            } else if (!isCorrect && (!inputField || inputField.value.trim() === "")) {
                details.push(`${idx+2} ✘ (empty)`);
            } else if (isCorrect) {
                details.push(`${idx+2} ✓`);
            }
        });
        feedbackDiv.innerHTML = `✍️ Rewrite score: ${score}/${max}<br> ${details.join(' | ')}`;
        if (score === max) feedbackDiv.style.color = "#2c6e2c";
        else feedbackDiv.style.color = "#bc6c25";
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
            let correct = false;
            if (inp) {
                let patternSet = gabExpected.find(p => p.id === row.id)?.patterns || [];
                correct = checkRewriteField(inp, patternSet);
            }
            let mark = correct ? '✓' : '✘';
            statuses.push(`${row.label}: ${mark}`);
        });
        gabDiv.innerHTML = `📊 Gabriel & Omar section score: ${score}/${max}<br> ${statuses.join(' | ')}<br><span style="font-size:0.75rem;">✔ Expected answers: Omar is as tall as Gabriel. / Gabriel isn't as keen on sports as Omar. / Omar isn't as good at Maths as Gabriel. / Gabriel is as hard-working as Omar. / Omar isn't as bad at keeping secrets as Gabriel.</span>`;
        gabDiv.style.color = score === max ? "#2c6e2c" : "#b45f2b";
    }
    
    // display sample for friends section (not graded)
    document.getElementById('showSampleFriends').addEventListener('click', () => {
        const sampleDiv = document.getElementById('sampleFriendsDiv');
        sampleDiv.innerHTML = `📌 Example comparisons:<br>
        ✨ (old)  → "Anna isn't as old as Luis."<br>
        ✨ (friendly) → "Maria is as friendly as Sofia."<br>
        ✨ (interested in art) → "Tom isn't as interested in art as Leo."<br>
        ✨ (good at languages) → "Elena is as good at languages as Kim."<br>
        ✨ (easy to get on with) → "Carlos is as easy to get on with as David."<br>
        ✨ (confident) → "Maya isn't as confident as Nina."`;
        sampleDiv.style.background = "#eff4fa";
        sampleDiv.style.padding = "10px";
        sampleDiv.style.borderRadius = "18px";
    });
    
    // Reset all fields
    function resetAll() {
        // reset radios
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
    
    document.getElementById('checkAllBtn').addEventListener('click', () => {
        computeScores();
    });
    document.getElementById('resetBtn').addEventListener('click', () => {
        resetAll();
    });
    
    // optional initial hint
    console.log("Worksheet ready — auto-correct active.");
</script>
</body>
</html>
