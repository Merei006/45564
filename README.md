<!DOCTYPE html>
<html lang="kk">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Жеке қауіпсіздік — Интерактивті тапсырма | 7-сынып</title>
  <style>
    :root {
      --primary: #1e4d8c;
      --primary-dk: #0f2f5c;
      --accent: #0d9488;
      --accent-lt: #14b8a6;
      --warn: #dc2626;
      --success: #16a34a;
      --bg: #f5f7fa;
      --card: #ffffff;
      --ink: #1a2332;
      --ink-soft: #3d4a5c;
      --muted: #6b7a8d;
      --border: #e2e8f0;
    }
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
      background: var(--bg);
      color: var(--ink);
      line-height: 1.55;
      min-height: 100vh;
    }
    .header {
      background: linear-gradient(135deg, var(--primary-dk), var(--primary));
      color: white;
      padding: 1.8rem 1.5rem 2.2rem;
      text-align: center;
      position: relative;
      overflow: hidden;
    }
    .header::before {
      content: '';
      position: absolute;
      top: -50%;
      right: -20%;
      width: 60%;
      height: 200%;
      background: radial-gradient(circle, rgba(20,184,166,0.15) 0%, transparent 70%);
    }
    .header h1 {
      font-size: 1.75rem;
      font-weight: 700;
      margin-bottom: 0.4rem;
      position: relative;
    }
    .header p {
      opacity: 0.85;
      font-size: 0.95rem;
      position: relative;
    }
    .badge {
      display: inline-block;
      background: var(--accent);
      color: white;
      font-size: 0.75rem;
      font-weight: 600;
      padding: 0.25rem 0.75rem;
      border-radius: 999px;
      margin-bottom: 0.8rem;
      letter-spacing: 0.5px;
    }
    .container {
      max-width: 820px;
      margin: 0 auto;
      padding: 1.5rem 1rem 3rem;
    }
    .progress-wrap {
      background: white;
      border-radius: 12px;
      padding: 1rem 1.25rem;
      margin-bottom: 1.5rem;
      box-shadow: 0 1px 3px rgba(0,0,0,0.06);
      display: flex;
      align-items: center;
      gap: 1rem;
    }
    .progress-bar {
      flex: 1;
      height: 10px;
      background: var(--border);
      border-radius: 999px;
      overflow: hidden;
    }
    .progress-fill {
      height: 100%;
      background: linear-gradient(90deg, var(--primary), var(--accent));
      border-radius: 999px;
      width: 0%;
      transition: width 0.4s ease;
    }
    .progress-text {
      font-size: 0.85rem;
      font-weight: 600;
      color: var(--muted);
      white-space: nowrap;
    }
    .section {
      background: var(--card);
      border-radius: 14px;
      padding: 1.5rem;
      margin-bottom: 1.25rem;
      box-shadow: 0 2px 8px rgba(0,0,0,0.05);
      border: 1px solid var(--border);
    }
    .section-title {
      display: flex;
      align-items: center;
      gap: 0.6rem;
      font-size: 1.15rem;
      font-weight: 700;
      color: var(--primary);
      margin-bottom: 1.1rem;
      padding-bottom: 0.7rem;
      border-bottom: 2px solid var(--border);
    }
    .section-num {
      background: var(--primary);
      color: white;
      width: 28px;
      height: 28px;
      border-radius: 8px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.85rem;
      font-weight: 700;
      flex-shrink: 0;
    }
    .q-card {
      background: #f8fafc;
      border-radius: 10px;
      padding: 1.1rem 1.2rem;
      margin-bottom: 1rem;
      border: 1px solid var(--border);
      transition: border-color 0.2s;
    }
    .q-card.answered-correct { border-color: var(--success); background: #f0fdf4; }
    .q-card.answered-wrong { border-color: var(--warn); background: #fef2f2; }
    .q-text {
      font-weight: 600;
      font-size: 0.98rem;
      margin-bottom: 0.85rem;
      color: var(--ink);
    }
    .options { display: flex; flex-direction: column; gap: 0.5rem; }
    .opt {
      display: flex;
      align-items: center;
      gap: 0.7rem;
      padding: 0.7rem 1rem;
      background: white;
      border: 1.5px solid var(--border);
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.15s;
      font-size: 0.92rem;
    }
    .opt:hover:not(.disabled) {
      border-color: var(--primary);
      background: #f0f5ff;
    }
    .opt.selected { border-color: var(--primary); background: #e8f0fe; }
    .opt.correct { border-color: var(--success); background: #dcfce7; }
    .opt.wrong { border-color: var(--warn); background: #fee2e2; }
    .opt.disabled { cursor: default; opacity: 0.9; }
    .opt input { display: none; }
    .opt-letter {
      width: 26px;
      height: 26px;
      border-radius: 6px;
      background: var(--border);
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      font-size: 0.8rem;
      color: var(--ink-soft);
      flex-shrink: 0;
    }
    .opt.correct .opt-letter { background: var(--success); color: white; }
    .opt.wrong .opt-letter { background: var(--warn); color: white; }
    .feedback {
      margin-top: 0.7rem;
      padding: 0.6rem 0.9rem;
      border-radius: 8px;
      font-size: 0.88rem;
      display: none;
    }
    .feedback.show { display: block; }
    .feedback.ok { background: #dcfce7; color: #166534; }
    .feedback.no { background: #fee2e2; color: #991b1b; }
    .scenario {
      background: linear-gradient(135deg, #f0f9ff, #ecfdf5);
      border-left: 4px solid var(--accent);
      border-radius: 0 10px 10px 0;
      padding: 1rem 1.2rem;
      margin-bottom: 1rem;
    }
    .scenario-label {
      font-size: 0.75rem;
      font-weight: 700;
      color: var(--accent);
      text-transform: uppercase;
      letter-spacing: 0.5px;
      margin-bottom: 0.4rem;
    }
    .scenario p { font-size: 0.95rem; color: var(--ink-soft); }
    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 0.4rem;
      padding: 0.7rem 1.4rem;
      border: none;
      border-radius: 10px;
      font-size: 0.95rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s;
    }
    .btn-primary {
      background: var(--primary);
      color: white;
    }
    .btn-primary:hover { background: var(--primary-dk); transform: translateY(-1px); }
    .btn-accent {
      background: var(--accent);
      color: white;
    }
    .btn-accent:hover { background: #0f766e; }
    .btn-outline {
      background: white;
      color: var(--primary);
      border: 1.5px solid var(--primary);
    }
    .btn-outline:hover { background: #f0f5ff; }
    .actions {
      display: flex;
      flex-wrap: wrap;
      gap: 0.75rem;
      margin-top: 1.25rem;
      justify-content: center;
    }
    .result-box {
      text-align: center;
      padding: 2rem 1.5rem;
      display: none;
    }
    .result-box.show { display: block; }
    .score-circle {
      width: 110px;
      height: 110px;
      border-radius: 50%;
      background: linear-gradient(135deg, var(--primary), var(--accent));
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      margin: 0 auto 1.2rem;
      font-weight: 700;
    }
    .score-circle .big { font-size: 2rem; line-height: 1; }
    .score-circle .small { font-size: 0.8rem; opacity: 0.85; }
    .result-msg { font-size: 1.15rem; font-weight: 600; margin-bottom: 0.5rem; }
    .result-detail { color: var(--muted); font-size: 0.9rem; margin-bottom: 1.5rem; }
    .match-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 0.75rem;
    }
    @media (max-width: 560px) {
      .match-grid { grid-template-columns: 1fr; }
      .header h1 { font-size: 1.4rem; }
    }
    .match-item {
      padding: 0.85rem 1rem;
      border-radius: 10px;
      border: 2px dashed var(--border);
      background: #f8fafc;
      cursor: pointer;
      text-align: center;
      font-size: 0.9rem;
      font-weight: 500;
      transition: all 0.2s;
      user-select: none;
    }
    .match-item:hover { border-color: var(--primary); background: #f0f5ff; }
    .match-item.selected { border-color: var(--primary); background: #e8f0fe; border-style: solid; }
    .match-item.matched { border-color: var(--success); background: #dcfce7; border-style: solid; pointer-events: none; }
    .match-item.wrong-temp { border-color: var(--warn); background: #fee2e2; }
    .pwd-demo {
      display: flex;
      flex-wrap: wrap;
      gap: 0.6rem;
      margin-top: 0.8rem;
    }
    .pwd-chip {
      padding: 0.45rem 0.9rem;
      border-radius: 8px;
      font-family: 'Consolas', 'Courier New', monospace;
      font-size: 0.88rem;
      font-weight: 600;
      cursor: pointer;
      border: 1.5px solid transparent;
      transition: all 0.15s;
    }
    .pwd-chip.weak { background: #fee2e2; color: #991b1b; }
    .pwd-chip.strong { background: #dcfce7; color: #166534; }
    .pwd-chip:hover { transform: scale(1.03); }
    .pwd-chip.picked { outline: 2px solid var(--primary); outline-offset: 2px; }
    .hidden { display: none !important; }
    .footer-note {
      text-align: center;
      color: var(--muted);
      font-size: 0.8rem;
      margin-top: 2rem;
      padding-top: 1rem;
      border-top: 1px solid var(--border);
    }
  </style>
</head>
<body>
  <div class="header">
    <div class="badge">ИНФОРМАТИКА · 7-СЫНЫП</div>
    <h1>Жеке қауіпсіздік</h1>
    <p>Интерактивті тапсырма · Сұрақтар мен жағдаяттар</p>
  </div>

  <div class="container">
    <!-- Progress -->
    <div class="progress-wrap">
      <div class="progress-bar"><div class="progress-fill" id="progressFill"></div></div>
      <div class="progress-text" id="progressText">0 / 12</div>
    </div>

    <!-- ========== 1. СҰРАҚТАР ========== -->
    <div class="section" id="sec-quiz">
      <div class="section-title">
        <span class="section-num">1</span>
        Сұрақтар (бір дұрыс жауап)
      </div>

      <!-- Q1 -->
      <div class="q-card" data-qid="1" data-answer="b">
        <div class="q-text">1. Сенімді құпиясөздің ең маңызды белгісі қайсысы?</div>
        <div class="options">
          <label class="opt"><input type="radio" name="q1" value="a" /><span class="opt-letter">A</span> Тек сандардан тұруы</label>
          <label class="opt"><input type="radio" name="q1" value="b" /><span class="opt-letter">B</span> Ұзындығы 12+ таңба, әріп, сан және символ болуы</label>
          <label class="opt"><input type="radio" name="q1" value="c" /><span class="opt-letter">C</span> Тек өз атынан тұруы</label>
          <label class="opt"><input type="radio" name="q1" value="d" /><span class="opt-letter">D</span> 4–6 таңба болуы</label>
        </div>
        <div class="feedback"></div>
      </div>

      <!-- Q2 -->
      <div class="q-card" data-qid="2" data-answer="c">
        <div class="q-text">2. 2FA (екі сатылы аутентификация) дегеніміз не?</div>
        <div class="options">
          <label class="opt"><input type="radio" name="q2" value="a" /><span class="opt-letter">A</span> Тек құпиясөзбен кіру</label>
          <label class="opt"><input type="radio" name="q2" value="b" /><span class="opt-letter">B</span> Антивирусты қосу</label>
          <label class="opt"><input type="radio" name="q2" value="c" /><span class="opt-letter">C</span> Құпиясөз + қосымша код/құрылғы арқылы кіру</label>
          <label class="opt"><input type="radio" name="q2" value="d" /><span class="opt-letter">D</span> Файлдарды мұрағаттау</label>
        </div>
        <div class="feedback"></div>
      </div>

      <!-- Q3 -->
      <div class="q-card" data-qid="3" data-answer="a">
        <div class="q-text">3. Антивирустық программаның негізгі міндеті қандай?</div>
        <div class="options">
          <label class="opt"><input type="radio" name="q3" value="a" /><span class="opt-letter">A</span> Зиянды программаларды анықтау және жою</label>
          <label class="opt"><input type="radio" name="q3" value="b" /><span class="opt-letter">B</span> Интернетті жылдамдату</label>
          <label class="opt"><input type="radio" name="q3" value="c" /><span class="opt-letter">C</span> Суреттерді өңдеу</label>
          <label class="opt"><input type="radio" name="q3" value="d" /><span class="opt-letter">D</span> Құпиясөзді өзгерту</label>
        </div>
        <div class="feedback"></div>
      </div>

      <!-- Q4 -->
      <div class="q-card" data-qid="4" data-answer="b">
        <div class="q-text">4. «3-2-1» ережесі нені білдіреді?</div>
        <div class="options">
          <label class="opt"><input type="radio" name="q4" value="a" /><span class="opt-letter">A</span> 3 құпиясөз, 2 антивирус, 1 компьютер</label>
          <label class="opt"><input type="radio" name="q4" value="b" /><span class="opt-letter">B</span> 3 көшірме, 2 түрлі тасымалдағыш, 1 сыртта</label>
          <label class="opt"><input type="radio" name="q4" value="c" /><span class="opt-letter">C</span> 3 минут, 2 сағат, 1 күн</label>
          <label class="opt"><input type="radio" name="q4" value="d" /><span class="opt-letter">D</span> 3 сайт, 2 қолданба, 1 аккаунт</label>
        </div>
        <div class="feedback"></div>
      </div>

      <!-- Q5 -->
      <div class="q-card" data-qid="5" data-answer="d">
        <div class="q-text">5. Қайсысы ең әлсіз құпиясөз?</div>
        <div class="options">
          <label class="opt"><input type="radio" name="q5" value="a" /><span class="opt-letter">A</span> K7#mP9$vL2xQ</label>
          <label class="opt"><input type="radio" name="q5" value="b" /><span class="opt-letter">B</span> Tr0ub4dor&amp;3</label>
          <label class="opt"><input type="radio" name="q5" value="c" /><span class="opt-letter">C</span> Sch00l_7B#Inf!</label>
          <label class="opt"><input type="radio" name="q5" value="d" /><span class="opt-letter">D</span> password123</label>
        </div>
        <div class="feedback"></div>
      </div>
    </div>

    <!-- ========== 2. ЖАҒДАЯТТАР ========== -->
    <div class="section" id="sec-scenarios">
      <div class="section-title">
        <span class="section-num">2</span>
        Жағдаяттар (дұрыс әрекетті таңда)
      </div>

      <!-- S1 -->
      <div class="q-card" data-qid="6" data-answer="b">
        <div class="scenario">
          <div class="scenario-label">Жағдаят 1</div>
          <p>Сізге «Шұғыл! Сіздің банк аккаунтыңыз бұзылған. Төмендегі сілтемеге басып, құпиясөзіңізді растаңыз» деген хат келді. Не істейсіз?</p>
        </div>
        <div class="options">
          <label class="opt"><input type="radio" name="q6" value="a" /><span class="opt-letter">A</span> Сілтемеге басып, құпиясөзді енгіземін</label>
          <label class="opt"><input type="radio" name="q6" value="b" /><span class="opt-letter">B</span> Хатты елемеймін / жоямын, банктің ресми сайтына өзім кіремін</label>
          <label class="opt"><input type="radio" name="q6" value="c" /><span class="opt-letter">C</span> Досыма жіберемін, ол біледі</label>
          <label class="opt"><input type="radio" name="q6" value="d" /><span class="opt-letter">D</span> Құпиясөзді хатқа жауап ретінде жіберемін</label>
        </div>
        <div class="feedback"></div>
      </div>

      <!-- S2 -->
      <div class="q-card" data-qid="7" data-answer="c">
        <div class="scenario">
          <div class="scenario-label">Жағдаят 2</div>
          <p>Досыңыз «Осы ойынды жүкте, free-games.exe, тегін!» деп флешка ұсынады. Не істейсіз?</p>
        </div>
        <div class="options">
          <label class="opt"><input type="radio" name="q7" value="a" /><span class="opt-letter">A</span> Бірден жүктеймін, досым ғой</label>
          <label class="opt"><input type="radio" name="q7" value="b" /><span class="opt-letter">B</span> Антивирусты өшіріп жүктеймін</label>
          <label class="opt"><input type="radio" name="q7" value="c" /><span class="opt-letter">C</span> Жүктемеймін, күдікті файлдан бас тартамын</label>
          <label class="opt"><input type="radio" name="q7" value="d" /><span class="opt-letter">D</span> Басқа достарға да таратамын</label>
        </div>
        <div class="feedback"></div>
      </div>

      <!-- S3 -->
      <div class="q-card" data-qid="8" data-answer="a">
        <div class="scenario">
          <div class="scenario-label">Жағдаят 3</div>
          <p>Сіз Instagram аккаунтына кірдіңіз. Құпиясөз дұрыс, бірақ қосымша код сұрайды. Бұл не?</p>
        </div>
        <div class="options">
          <label class="opt"><input type="radio" name="q8" value="a" /><span class="opt-letter">A</span> 2FA қосылған — телефондағы кодты енгізу керек</label>
          <label class="opt"><input type="radio" name="q8" value="b" /><span class="opt-letter">B</span> Аккаунт бұзылған</label>
          <label class="opt"><input type="radio" name="q8" value="c" /><span class="opt-letter">C</span> Интернет жоқ</label>
          <label class="opt"><input type="radio" name="q8" value="d" /><span class="opt-letter">D</span> Антивирус жұмыс істеп тұр</label>
        </div>
        <div class="feedback"></div>
      </div>

      <!-- S4 -->
      <div class="q-card" data-qid="9" data-answer="b">
        <div class="scenario">
          <div class="scenario-label">Жағдаят 4</div>
          <p>Компьютердегі барлық маңызды жобалар тек бір қатты дискіде сақтаулы. Не істеу керек?</p>
        </div>
        <div class="options">
          <label class="opt"><input type="radio" name="q9" value="a" /><span class="opt-letter">A</span> Ештеңе, бір жерде болса жеткілікті</label>
          <label class="opt"><input type="radio" name="q9" value="b" /><span class="opt-letter">B</span> 3-2-1 ережесін қолданып, қосымша көшірмелер жасау</label>
          <label class="opt"><input type="radio" name="q9" value="c" /><span class="opt-letter">C</span> Барлық файлды жою</label>
          <label class="opt"><input type="radio" name="q9" value="d" /><span class="opt-letter">D</span> Құпиясөзді өзгерту</label>
        </div>
        <div class="feedback"></div>
      </div>

      <!-- S5 -->
      <div class="q-card" data-qid="10" data-answer="c">
        <div class="scenario">
          <div class="scenario-label">Жағдаят 5</div>
          <p>Сіз бір құпиясөзді мектеп поштасы, ойын аккаунты және әлеуметтік желі үшін бірдей қолданасыз. Бұл қауіпті ме?</p>
        </div>
        <div class="options">
          <label class="opt"><input type="radio" name="q10" value="a" /><span class="opt-letter">A</span> Жоқ, ыңғайлы ғой</label>
          <label class="opt"><input type="radio" name="q10" value="b" /><span class="opt-letter">B</span> Тек мектеп үшін қауіпті</label>
          <label class="opt"><input type="radio" name="q10" value="c" /><span class="opt-letter">C</span> Иә, бір аккаунт бұзылса — барлығы қауіпте</label>
          <label class="opt"><input type="radio" name="q10" value="d" /><span class="opt-letter">D</span> Тек ойын үшін қауіпті</label>
        </div>
        <div class="feedback"></div>
      </div>
    </div>

    <!-- ========== 3. ҚҰПИЯСӨЗ СҰРЫПТАУ ========== -->
    <div class="section" id="sec-pwd">
      <div class="section-title">
        <span class="section-num">3</span>
        Құпиясөздерді сұрыпта (әлсіз / күшті)
      </div>
      <p style="margin-bottom:1rem; color:var(--ink-soft); font-size:0.95rem;">
        Әр құпиясөзді басып, оны «Әлсіз» немесе «Күшті» тобына жіберіңіз.
      </p>
      <div class="pwd-demo" id="pwdChips">
        <span class="pwd-chip" data-type="weak" data-pwd="123456">123456</span>
        <span class="pwd-chip" data-type="strong" data-pwd="K7#mP9$vL2">K7#mP9$vL2</span>
        <span class="pwd-chip" data-type="weak" data-pwd="qwerty">qwerty</span>
        <span class="pwd-chip" data-type="strong" data-pwd="Tr0ub4dor&amp;3">Tr0ub4dor&amp;3</span>
        <span class="pwd-chip" data-type="weak" data-pwd="password">password</span>
        <span class="pwd-chip" data-type="strong" data-pwd="Sch00l_7B#Inf!">Sch00l_7B#Inf!</span>
        <span class="pwd-chip" data-type="weak" data-pwd="asma2009">asma2009</span>
        <span class="pwd-chip" data-type="strong" data-pwd="N7#qL9$mR2vT">N7#qL9$mR2vT</span>
      </div>
      <div style="display:grid; grid-template-columns:1fr 1fr; gap:1rem; margin-top:1.2rem;">
        <div>
          <div style="font-weight:700; color:var(--warn); margin-bottom:0.5rem;">❌ Әлсіз</div>
          <div id="weakZone" style="min-height:80px; border:2px dashed #fca5a5; border-radius:10px; padding:0.6rem; background:#fef2f2; display:flex; flex-wrap:wrap; gap:0.4rem;"></div>
        </div>
        <div>
          <div style="font-weight:700; color:var(--success); margin-bottom:0.5rem;">✅ Күшті</div>
          <div id="strongZone" style="min-height:80px; border:2px dashed #86efac; border-radius:10px; padding:0.6rem; background:#f0fdf4; display:flex; flex-wrap:wrap; gap:0.4rem;"></div>
        </div>
      </div>
      <div class="actions" style="margin-top:1rem;">
        <button class="btn btn-outline" onclick="checkPwdSort()">Тексеру</button>
        <button class="btn btn-outline" onclick="resetPwdSort()">Қайта бастау</button>
      </div>
      <div id="pwdFeedback" class="feedback" style="margin-top:0.8rem;"></div>
    </div>

    <!-- ========== 4. СӘЙКЕСТЕНДІРУ ========== -->
    <div class="section" id="sec-match">
      <div class="section-title">
        <span class="section-num">4</span>
        Сәйкестендіру
      </div>
      <p style="margin-bottom:1rem; color:var(--ink-soft); font-size:0.95rem;">
        Сол жақтағы ұғымды оң жақтағы анықтамамен жұптаңыз (екеуін басыңыз).
      </p>
      <div class="match-grid" id="matchGrid">
        <!-- filled by JS -->
      </div>
      <div class="actions" style="margin-top:1rem;">
        <button class="btn btn-outline" onclick="resetMatch()">Қайта бастау</button>
      </div>
      <div id="matchFeedback" class="feedback" style="margin-top:0.8rem;"></div>
    </div>

    <!-- Actions -->
    <div class="actions" id="mainActions">
      <button class="btn btn-primary" onclick="checkAll()">Барлығын тексеру</button>
      <button class="btn btn-outline" onclick="resetAll()">Қайта бастау</button>
    </div>

    <!-- Result -->
    <div class="section result-box" id="resultBox">
      <div class="score-circle">
        <span class="big" id="scoreNum">0</span>
        <span class="small">/ 12</span>
      </div>
      <div class="result-msg" id="resultMsg">Нәтиже</div>
      <div class="result-detail" id="resultDetail"></div>
      <button class="btn btn-accent" onclick="resetAll()">Қайтадан өту</button>
    </div>

    <div class="footer-note">
      Информатика · 7-сынып · Жеке қауіпсіздік және сервистік программалар · Оқу мақсаты 7.4.1.1
    </div>
  </div>

  <script>
    // ---------- State ----------
    let answered = {};
    let score = 0;
    const TOTAL_Q = 10; // quiz + scenarios
    const TOTAL_EXTRA = 2; // pwd sort + match (counted as 1 each if correct)

    const explanations = {
      1: "Күшті құпиясөз — ұзын, әріп+сан+символ комбинациясы.",
      2: "2FA = құпиясөз + екінші фактор (SMS/код/құрылғы).",
      3: "Антивирус зиянды программаларды тауып, жояды.",
      4: "3 көшірме, 2 түрлі тасымалдағыш, 1 сыртта — 3-2-1 ережесі.",
      5: "password123 — өте кең таралған және әлсіз.",
      6: "Фишинг хат! Сілтемеге баспаңыз, ресми сайтқа өзіңіз кіріңіз.",
      7: "Белгісіз .exe файл — вирус болуы мүмкін. Жүктемеңіз.",
      8: "Бұл 2FA жұмыс істеп тұрғанын көрсетеді.",
      9: "Бір жерде сақтау қауіпті. Сақтық көшірме жасаңыз.",
      10: "Бір құпиясөзді бірнеше жерде қолданбаңыз!"
    };

    // ---------- Quiz / Scenario ----------
    document.querySelectorAll('.q-card[data-qid]').forEach(card => {
      const opts = card.querySelectorAll('.opt');
      opts.forEach(opt => {
        opt.addEventListener('click', () => {
          if (card.classList.contains('answered-correct') || card.classList.contains('answered-wrong')) return;
          const input = opt.querySelector('input');
          input.checked = true;
          opts.forEach(o => o.classList.remove('selected'));
          opt.classList.add('selected');
          // auto-check on select
          checkOne(card);
        });
      });
    });

    function checkOne(card) {
      const qid = card.dataset.qid;
      const correct = card.dataset.answer;
      const selected = card.querySelector('input:checked');
      if (!selected) return;

      const val = selected.value;
      const fb = card.querySelector('.feedback');
      const opts = card.querySelectorAll('.opt');

      opts.forEach(o => {
        o.classList.add('disabled');
        const v = o.querySelector('input').value;
        if (v === correct) o.classList.add('correct');
        if (v === val && v !== correct) o.classList.add('wrong');
      });

      if (val === correct) {
        card.classList.add('answered-correct');
        fb.className = 'feedback show ok';
        fb.textContent = '✓ Дұрыс! ' + (explanations[qid] || '');
        if (!answered[qid]) { answered[qid] = true; score++; }
      } else {
        card.classList.add('answered-wrong');
        fb.className = 'feedback show no';
        fb.textContent = '✗ Қате. ' + (explanations[qid] || '');
        answered[qid] = false;
      }
      updateProgress();
    }

    // ---------- Password sort ----------
    let selectedPwd = null;
    document.querySelectorAll('#pwdChips .pwd-chip').forEach(chip => {
      chip.addEventListener('click', () => {
        document.querySelectorAll('#pwdChips .pwd-chip').forEach(c => c.classList.remove('picked'));
        chip.classList.add('picked');
        selectedPwd = chip;
      });
    });

    document.getElementById('weakZone').addEventListener('click', () => placePwd('weak'));
    document.getElementById('strongZone').addEventListener('click', () => placePwd('strong'));

    function placePwd(zone) {
      if (!selectedPwd) return;
      const target = zone === 'weak' ? document.getElementById('weakZone') : document.getElementById('strongZone');
      const clone = selectedPwd.cloneNode(true);
      clone.classList.remove('picked');
      clone.onclick = null;
      clone.style.cursor = 'default';
      target.appendChild(clone);
      selectedPwd.remove();
      selectedPwd = null;
    }

    function checkPwdSort() {
      const weak = [...document.getElementById('weakZone').querySelectorAll('.pwd-chip')];
      const strong = [...document.getElementById('strongZone').querySelectorAll('.pwd-chip')];
      let ok = true;
      weak.forEach(c => { if (c.dataset.type !== 'weak') ok = false; });
      strong.forEach(c => { if (c.dataset.type !== 'strong') ok = false; });
      if (weak.length + strong.length < 8) ok = false;

      const fb = document.getElementById('pwdFeedback');
      if (ok) {
        fb.className = 'feedback show ok';
        fb.textContent = '✓ Барлығы дұрыс сұрыпталған!';
        if (!answered['pwd']) { answered['pwd'] = true; score++; }
      } else {
        fb.className = 'feedback show no';
        fb.textContent = '✗ Қате бар. Әлсіздерді солға, күштілерді оңға қойыңыз.';
        answered['pwd'] = false;
      }
      updateProgress();
    }

    function resetPwdSort() {
      const zone = document.getElementById('pwdChips');
      document.querySelectorAll('#weakZone .pwd-chip, #strongZone .pwd-chip').forEach(c => {
        c.classList.remove('picked');
        zone.appendChild(c);
      });
      document.getElementById('pwdFeedback').className = 'feedback';
      delete answered['pwd'];
      updateProgress();
      // rebind
      document.querySelectorAll('#pwdChips .pwd-chip').forEach(chip => {
        chip.onclick = () => {
          document.querySelectorAll('#pwdChips .pwd-chip').forEach(c => c.classList.remove('picked'));
          chip.classList.add('picked');
          selectedPwd = chip;
        };
      });
    }

    // ---------- Matching ----------
    const matchPairs = [
      { id: 'm1', term: '2FA', def: 'Құпиясөз + қосымша код' },
      { id: 'm2', term: 'Фишинг', def: 'Жалған хат арқылы мәлімет ұрлау' },
      { id: 'm3', term: 'Антивирус', def: 'Зиянды программаларды жояды' },
      { id: 'm4', term: 'Backup', def: 'Деректердің сақтық көшірмесі' },
    ];
    let matchSelected = null;
    let matchScore = 0;

    function initMatch() {
      const grid = document.getElementById('matchGrid');
      grid.innerHTML = '';
      matchScore = 0;
      matchSelected = null;
      const terms = matchPairs.map(p => ({ id: p.id, text: p.term, type: 'term' }));
      const defs = matchPairs.map(p => ({ id: p.id, text: p.def, type: 'def' }));
      // shuffle defs
      for (let i = defs.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [defs[i], defs[j]] = [defs[j], defs[i]];
      }
      const left = document.createElement('div');
      left.style.display = 'flex'; left.style.flexDirection = 'column'; left.style.gap = '0.5rem';
      const right = document.createElement('div');
      right.style.display = 'flex'; right.style.flexDirection = 'column'; right.style.gap = '0.5rem';

      terms.forEach(t => {
        const el = document.createElement('div');
        el.className = 'match-item';
        el.dataset.id = t.id;
        el.dataset.type = 'term';
        el.textContent = t.text;
        el.onclick = () => onMatchClick(el);
        left.appendChild(el);
      });
      defs.forEach(d => {
        const el = document.createElement('div');
        el.className = 'match-item';
        el.dataset.id = d.id;
        el.dataset.type = 'def';
        el.textContent = d.text;
        el.onclick = () => onMatchClick(el);
        right.appendChild(el);
      });
      grid.appendChild(left);
      grid.appendChild(right);
    }

    function onMatchClick(el) {
      if (el.classList.contains('matched')) return;
      if (!matchSelected) {
        matchSelected = el;
        el.classList.add('selected');
        return;
      }
      if (matchSelected === el) {
        el.classList.remove('selected');
        matchSelected = null;
        return;
      }
      // different type?
      if (matchSelected.dataset.type === el.dataset.type) {
        matchSelected.classList.remove('selected');
        matchSelected = el;
        el.classList.add('selected');
        return;
      }
      // check match
      if (matchSelected.dataset.id === el.dataset.id) {
        matchSelected.classList.remove('selected');
        matchSelected.classList.add('matched');
        el.classList.add('matched');
        matchSelected = null;
        matchScore++;
        if (matchScore === matchPairs.length) {
          document.getElementById('matchFeedback').className = 'feedback show ok';
          document.getElementById('matchFeedback').textContent = '✓ Барлық жұптар дұрыс!';
          if (!answered['match']) { answered['match'] = true; score++; }
          updateProgress();
        }
      } else {
        matchSelected.classList.add('wrong-temp');
        el.classList.add('wrong-temp');
        const a = matchSelected, b = el;
        setTimeout(() => {
          a.classList.remove('selected', 'wrong-temp');
          b.classList.remove('wrong-temp');
          matchSelected = null;
        }, 600);
      }
    }

    function resetMatch() {
      document.getElementById('matchFeedback').className = 'feedback';
      delete answered['match'];
      initMatch();
      updateProgress();
    }

    // ---------- Progress & Check All ----------
    function updateProgress() {
      const done = Object.keys(answered).length;
      const total = TOTAL_Q + TOTAL_EXTRA;
      document.getElementById('progressFill').style.width = (done / total * 100) + '%';
      document.getElementById('progressText').textContent = done + ' / ' + total;
    }

    function checkAll() {
      // force check remaining quiz
      document.querySelectorAll('.q-card[data-qid]').forEach(card => {
        if (!card.classList.contains('answered-correct') && !card.classList.contains('answered-wrong')) {
          const sel = card.querySelector('input:checked');
          if (sel) checkOne(card);
        }
      });
      // show result
      const totalPossible = TOTAL_Q + TOTAL_EXTRA;
      const s = score;
      document.getElementById('scoreNum').textContent = s;
      const msg = document.getElementById('resultMsg');
      const det = document.getElementById('resultDetail');
      if (s >= 11) {
        msg.textContent = 'Керемет! Қауіпсіздік бойынша өте жақсы білесіз 🌟';
        det.textContent = 'Сіз сенімді құпиясөз, 2FA, антивирус және мұрағаттауды жақсы меңгердіңіз.';
      } else if (s >= 8) {
        msg.textContent = 'Жақсы нәтиже! 👍';
        det.textContent = 'Кейбір жерлерді қайталап шығыңыз — әлі де жақсартуға болады.';
      } else {
        msg.textContent = 'Қайталап өтіңіз';
        det.textContent = 'Сабақ материалдарын қайталап, тапсырманы қайта орындаңыз.';
      }
      document.getElementById('resultBox').classList.add('show');
      document.getElementById('resultBox').scrollIntoView({ behavior: 'smooth' });
    }

    function resetAll() {
      answered = {};
      score = 0;
      document.querySelectorAll('.q-card').forEach(card => {
        card.classList.remove('answered-correct', 'answered-wrong');
        card.querySelectorAll('.opt').forEach(o => {
          o.classList.remove('selected', 'correct', 'wrong', 'disabled');
          const inp = o.querySelector('input');
          if (inp) inp.checked = false;
        });
        const fb = card.querySelector('.feedback');
        if (fb) { fb.className = 'feedback'; fb.textContent = ''; }
      });
      resetPwdSort();
      resetMatch();
      document.getElementById('resultBox').classList.remove('show');
      updateProgress();
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    // Init
    initMatch();
    updateProgress();
  </script>
</body>
</html>
