<吃飽太閒做的網站，能幫到你我覺得很開心>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>147測驗｜單一檔案版</title>

    <!-- 預先套用主題避免閃爍 -->
    <script>
      (function () {
        try {
          var saved = localStorage.getItem('theme');
          if (saved === 'dark' || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches)) {
            document.documentElement.classList.add('preload-dark');
            document.documentElement.setAttribute('data-theme','dark');
          }
        } catch(e){}
      })();
    </script>

    <style>
      :root{
        --bg:#f0f4f8; --txt:#000; --card:#fff; --rule:#e9ecef; --muted:#666;
        --primary:#007bff; --primary-800:#0056b3; --danger:#dc3545;
        --green:#28a745; --green-800:#218838; --teal:#17a2b8; --teal-800:#138496;
        --table-bd:#ccc;

        /* 正解強調（淺色） */
        --ans-chip-bg:#e7f6ec; --ans-chip-fg:#136d3a;
        --ans-row-bg:#f5fbf7; --ans-row-bd:#cce8d5;
      }
      body.dark {
        --bg:#121212; --txt:#fff; --card:#1e1e1e; --rule:#333; --table-bd:#444; --muted:#aaa;

        /* 正解強調（深色） */
        --ans-chip-bg:#1f3a29; --ans-chip-fg:#b9f6ca;
        --ans-row-bg:#12301f; --ans-row-bd:#2c5a3f;
      }

      html, body { height: 100%; }
      body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 40px;
        /* 基礎自適應字級（桌機普遍上限 24px） */
        font-size: clamp(16px, 1.1vw + 12px, 24px);
        background: var(--bg);
        color: var(--txt);
        transition: background-color .4s, color .4s;
      }

      #container {
        max-width: 1320px; margin: auto; background: var(--card); padding: 40px;
        border-radius: 20px; box-shadow: 0 0 10px rgba(0,0,0,.1);
        transition: background-color .4s, color .4s;
      }

      .hidden { display: none; }
      h1, h2 { text-align: center; font-size: 1.6em; margin: .2em 0 .6em; }
      #rules { background: var(--rule); padding: 16px; margin-bottom: 28px; border-radius: 10px; font-size: .95em; }

      .btn {
        background: var(--primary); color: #fff; border: none; padding: 14px 24px;
        margin: 8px; border-radius: 10px; cursor: pointer; font-size: .95em;
        transition: background-color .2s, transform .1s;
        white-space: nowrap;
      }
      .btn:hover { background: var(--primary-800); }
      #leaveBtn { background: var(--danger); }
      #openBankBtn { background: var(--teal); }
      #openBankBtn:hover { background: var(--teal-800); }

      /* 進度條 */
      #progress, #timer { font-weight: bold; font-size: 1em; }
      .progress-container { background: #ddd; height: 10px; border-radius: 5px; margin-top: 14px; overflow: hidden; }
      body.dark .progress-container { background: #555; }
      .progress-bar { height: 100%; width: 0; background: var(--primary); transition: width .6s ease; }

      .question { margin: 24px 0 12px; font-size: 1.2em; }
      .options label { display: block; margin-bottom: 12px; font-size: 1em; }

      /* 表格與響應式容器 */
      .table-responsive { width: 100%; overflow-x: auto; -webkit-overflow-scrolling: touch; }
      table { width: 100%; border-collapse: collapse; margin-top: 16px; font-size: 1em; min-width: 460px; }
      th, td {
        border: 1px solid var(--table-bd); padding: 12px 14px; text-align: left; vertical-align: top;
        color: var(--txt); word-break: break-word;
      }

      /* 錯題列色（深色模式改亮字） */
      tr.wrong { background-color: #ffe6e6; }
      body.dark tr.wrong { background-color: #5a1a1a; }
      body.dark tr.wrong td { color: #fff; }

      /* 正解強調（提高優先度，避免被錯題底色吃掉） */
      .ans-chip { display:inline-block; padding:2px 8px; border-radius:999px; background: var(--ans-chip-bg); color: var(--ans-chip-fg); font-size:.9em; margin-right:6px; }
      .ans-cell  { background: var(--ans-row-bg) !important; border-left: 3px solid var(--ans-row-bd) !important; color: var(--txt) !important; }
      .opt-row   { display:block; padding:4px 6px; margin:2px 0; border-radius:6px; }
      .opt-row.is-correct { background: var(--ans-row-bg) !important; border-left: 3px solid var(--ans-row-bd) !important; color: var(--txt) !important; }
      tr.wrong td.ans-cell { background: var(--ans-row-bg) !important; color: var(--txt) !important; }

      /* 右上角按鈕固定 */
      #darkModeToggle, #homeBtn {
        position: fixed; right: 20px; padding: 10px 16px; border: none; border-radius: 8px;
        cursor: pointer; font-size: .95em; z-index: 2000; box-shadow: 0 4px 12px rgba(0,0,0,.15);
      }
      #darkModeToggle { top: 20px; background: #333; color: #fff; }
      #darkModeToggle:hover { background: #555; }
      #homeBtn { top: 68px; background: var(--green); color: #fff; text-decoration: none; }
      #homeBtn:hover { background: var(--green-800); }

      .mono { font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Courier New", monospace; }
      .muted { opacity: .8; color: var(--muted); }

      /* 小尺寸優化 */
      @media (max-width: 768px) {
        body { padding: 20px; font-size: clamp(14px, 2.2vw + 8px, 17px); }
        #container { padding: 20px; border-radius: 16px; }
        .btn { padding: 12px 16px; margin: 6px; font-size: .95em; }
        #darkModeToggle, #homeBtn { right: 12px; }
        #darkModeToggle { top: 12px; }
        #homeBtn { top: 56px; }
      }
      @media (max-width: 540px) {
        /* 手機上把「您的答案」隱藏，保留題目/正解/OX */
        #results table th:nth-child(2), #results table td:nth-child(2) { display:none; }
      }
      @media (max-width: 420px) {
        #bank .controls { display: grid; grid-template-columns: 1fr; gap: 8px; }
      }

      /* —— 大螢幕加碼放大（到 4K 前） —— */
      @media (min-width: 1200px) {
        body       { font-size: clamp(18px, 0.9vw + 12px, 26px); }
        #container { max-width: 1440px; }
        h1, h2     { font-size: 2rem; }
      }
      @media (min-width: 1800px) {
        body       { font-size: clamp(20px, 0.7vw + 12px, 28px); }
        #container { max-width: 1680px; }
        h1, h2     { font-size: 2.2rem; }
      }
      @media (min-width: 2400px) {
        body       { font-size: clamp(22px, 0.6vw + 14px, 32px); }
        #container { max-width: 1920px; }
        h1, h2     { font-size: 2.4rem; }
      }

      /* —— 2560×1440（含以上）專用上限 —— */
      @media (min-width: 2560px) and (min-height: 1400px) {
        body       { font-size: clamp(22px, 0.55vw + 16px, 34px); } /* 上限 34px */
        #container { max-width: 2000px; }
        h1, h2     { font-size: 2.6rem; }
      }

      /* 預載深色（head 腳本使用），load 後會移除 */
      .preload-dark body, .preload-dark { background:#121212; color:#fff; }
    </style>
  </head>
  <body>
    <button id="darkModeToggle" aria-pressed="false">深色模式 / Dark Mode</button>
    <a id="homeBtn" href="https://hisausage7.github.io/147test/" title="回首頁">🏠 回首頁</a>

    <div id="container">
      <!-- 歡迎頁 -->
      <div id="welcome">
        <h1>147測驗M9-CAA</h1>
        <div id="rules">
          <p><strong>考試注意事項 / Exam Rules:</strong></p>
          <p>1. 請輸入姓名後才能開始作答。 / You must enter your name to start the quiz.</p>
          <!-- 這行改成可自訂 -->
          <p>2. 考試限時可自訂（預設 80 分鐘,可設定至999分鐘），開始後自動倒數。 / You can set the time limit (default 80 minutes); countdown starts on begin.</p>
          <p>3. 作答途中可隨時點擊「離開考試」提前結束。 / You can click "Leave Quiz" anytime to finish early.</p>
          <p>4. 完成後會自動顯示所有答題結果與成績。 / Results and scores will be displayed after completion.</p>
          <p>5. 答對題目顯示O，答錯題目顯示X。 / Correct answers will show O, incorrect answers will show X.</p>
          <p>6. 測驗過程為亂序出題。 / The test process was chaotic and disordered in setting questions.</p>
          <p>!版權及源代碼所有-航機系008沈崑宸!</p>
          <p>!僅作為自我測驗使用!</p>
          <p>!此章節已包含PART-66!</p>
        </div>
        <input type="text" id="nameInput" placeholder="輸入姓名 / Enter your name"
               style="width:100%;padding:8px;margin-bottom:10px;font-size:1em;" />
        <input type="number" id="questionLimit" placeholder="輸入題數,至多451題 / Enter number of questions"
               style="width:100%;padding:8px;margin-bottom:10px;font-size:1em;" />
        <!-- 新增：作答時間（分鐘），預設 80，限制 1~300 -->
        <input type="number" id="durationInput" value="80" min="1" max="300"
               placeholder="作答時間（分鐘，預設 80,可設定置999分鐘） / Duration in minutes"
               style="width:100%;padding:8px;margin-bottom:10px;font-size:1em;" />
        <div style="text-align:center; display:flex; flex-wrap:wrap; justify-content:center;">
          <button id="startBtn" class="btn">開始測驗 / Start Quiz</button>
          <button id="openBankBtn" class="btn">題庫瀏覽 / Browse Bank</button>
        </div>
      </div>

      <!-- 測驗頁 -->
      <div id="quiz" class="hidden">
        <div style="display:flex; align-items:center; gap:8px;">
          <span id="welcomeName"></span>
          <span id="timer" style="margin-left:auto">80:00</span>
        </div>
        <div class="mono" id="progress">題數: <span id="current">0</span> / <span id="total">0</span></div>
        <div class="progress-container"><div id="progressBar" class="progress-bar"></div></div>
        <div class="question" id="questionText"></div>
        <div class="options" id="options"></div>
        <div style="display:flex;gap:10px;flex-wrap:wrap">
          <button id="prevBtn" class="btn" style="background:#6c757d">上一題 / Previous</button>
          <button id="leaveBtn" class="btn">離開考試 / Leave Quiz</button>
        </div>
      </div>

      <!-- 結果頁 -->
      <div id="results" class="hidden">
        <h2>測驗結果 / Results</h2>
        <div style="display:flex; flex-wrap:wrap; justify-content:center;">
          <button id="retryBtn" class="btn">重新開始 / Retry</button>
          <button id="showWrongBtn" class="btn" style="background:#ffc107">只看錯題 / Wrong Only</button>
          <button id="showAllBtn" class="btn">看全部結果 / Show All</button>
          <button id="toBankFromResults" class="btn" style="background:#17a2b8">題庫瀏覽 / Browse Bank</button>
        </div>
        <div class="table-responsive">
          <table>
            <thead>
              <tr><th>題目</th><th>您的答案</th><th>正確答案</th><th>結果</th></tr>
            </thead>
            <tbody id="resultsBody"></tbody>
          </table>
        </div>
        <div id="scoreSummary" style="text-align:center;margin-top:12px;font-size:1em"></div>
      </div>

      <!-- 題庫瀏覽頁 -->
      <div id="bank" class="hidden">
        <h2>題庫瀏覽 / Question Bank</h2>
        <div class="controls">
          <input id="bankSearch" type="text" placeholder="關鍵字搜尋（會搜尋題目與選項）" />
          <label>每頁顯示
            <select id="perPage">
              <option value="5">5</option>
              <option value="10" selected>10</option>
              <option value="20">20</option>
              <option value="50">50</option>
              <option value="all">全部</option>
            </select>
            題
          </label>
          <button id="backToWelcome" class="btn" style="padding:12px 18px">返回首頁 / Home</button>
        </div>
        <div class="table-responsive">
          <table>
            <thead>
              <tr>
                <th style="width:70px">#</th>
                <th>題目</th>
                <th style="width:34%">選項</th>
                <th style="width:160px">正確答案</th>
              </tr>
            </thead>
            <tbody id="bankBody"></tbody>
          </table>
        </div>
        <div class="pagination" style="display:flex;justify-content:center;align-items:center;gap:10px;margin-top:10px;">
          <button id="prevPage" class="btn" style="padding:10px 16px">上一頁</button>
          <span id="pageInfo" class="mono"></span>
          <button id="nextPage" class="btn" style="padding:10px 16px">下一頁</button>
        </div>
        <div style="text-align:center;margin-top:8px">
          <small class="muted">提示：可用右上角「深色模式」切換外觀；搜尋支援中英文與數字。</small>
        </div>
      </div>
    </div>
    <script>
            document.addEventListener("DOMContentLoaded", function () {
              const questions = [
                // === PART 1 ===
      
  {
    question: "最常⾒的⾶機意外事件都可以追溯為\nThe most of aircraft incidents can be traced to",
    options: ["A. 技術問題 Technical Problem", "B. ⼈為疏失 Human Error", "C. 管理疏失 Management Error", "D. 製造廠 Manufacture"],
    answer: "B"
  },
  {
    question: "⼀名⼯程師在⼀次⽔平尾翼鉚釘檢查時疏忽了⼀條裂縫，這種過失有可能是因為甚麼原因引起的?\nAn engineer misses a crack during a rivet inspection of the horizontal stablizer. This failing would most likely be caused by?",
    options: ["A. 懼⾼症 Acrophobia", "B. 廣場恐懼症 Agoraphobia", "C. 幽閉恐懼症 Claustrophobia", "D. 恐懼蜘蛛症 Arachnephobia"],
    answer: "A"
  },
  {
    question: "在⼀個強⽽有⼒的安全⽂化組織中，下列何者不是重要的部分？\nWhat is NOT a key component in an organization\nwith a strong safety culture?",
    options: ["A. 信息共享 Sharing of information", "B. 信任的氣氛 An atmosphere of trust", "C. 秘密會議 A hidden agenda", "D. 尊重知識 Respect for knowledge"],
    answer: "C"
  },
  {
    question: "噪⾳、照明與溫度，何者與維修⼈為因素有關？",
    options: ["A. 噪⾳", "B. 照明", "C. 溫度", "D. 皆有關"],
    answer: "D"
  },
  {
    question: "⾶機機棚內的燈光應該⾄少\nArea lighting in hangar should be at least",
    options: ["A. 能看清楚⼿冊⽂字並確認裝備位置 Enabling to clearly read manual\ntest and affirm equipment locations.", "B. 與正午機坪作業相同 As bright as the lightness at noon\non ramp.", "C. 無所謂 Doesn't matter", "D. 能辨認⾶機外型輪廓 Enabling to recognize airplanes'\nshapes."],
    answer: "A"
  },
  {
    question: "⼯程師檢查安定⾯的配平插孔螺絲沒有看到⼀斷裂導線，這是何種失誤?\nOn inspection of the stabilizer trim jack screw the engineer does not see a broken hanging wire.\nWhat type failing?",
    options: ["A. 分散注意⼒ divided attention", "B. 集中注意⼒ focused attention", "C. 選擇性注意⼒ selective attention", "D. 持續注意⼒ sustained attention"],
    answer: "C"
  },
  {
    question: "⼯程師在檢查安定⾯配平插孔螺釘被叫出去幫忙移動梯架. 當他返回時錯過了⼀個油點. 什麼類型的關注描述了這個缺點？\nOn an inspection of the stabilizer trim jack screw the engineer is called out to help move a work stand. When he returns he misses one grease point. What type of attention describes this failing?",
    options: ["A. 集中注意⼒ focused attention", "B. 選擇性注意⼒ selective attention", "C. 分散注意⼒ divided attention", "D. 持續注意⼒ sustained attention"],
    answer: "C"
  },
  {
    question: "在⼀個值班的開始，⼀個⼯程師聽從他的⼯作指\n⽰，⽽忽略將⼯作指⽰給他的⼩組成員. 什麼類型的關注描述了這個缺點？\nAt the beginning of a shift, an engineer listens to his work orders and ignores the work orders given to his team members. What type of attention describes this failing?",
    options: ["A. 集中注意⼒ focused attention", "B. 選擇性注意⼒ selective attention", "C. 分散注意⼒ divided attention", "D. 持續注意⼒ sustained attention"],
    answer: "A"
  },
  {
    question: "⼀名⼯⼈變得容易厭倦，並完成他的⼯作有困難. 這種缺點是缺乏 …\nA worker gets easily bored and has difficulty completing his work. This failing is a result of a lack of …",
    options: ["A. 集中注意⼒ focused attention", "B. 選擇性注意⼒ selective attention", "C. 分散注意⼒ divided attention", "D. 持續注意⼒ sustained attention"],
    answer: "D"
  },
  {
    question: "打破\"錯誤鏈\"如何防⽌發⽣意外？\nHow does breaking the \"error chain\" prevent an\naccident?",
    options: ["A. 阻⽌任何先決因素 it stops and preceding causes", "B. 阻⽌任何後續可能因素發⽣ it stops any follwing causes", "C. 阻⽌根本因素 it stops the root causes"],
    answer: "B"
  },
  {
    question: "影響⾝體⽣理節奏之最普遍因素為?\nwhat is the most common terms of disturbance of\nbody rhythm?",
    options: ["A. 周末 weekend", "B. 時差 jet lag", "C. 加班 overtime"],
    answer: "B"
  },
  {
    question: "當使⽤⼀個滅火器時妳⼤約可靠近火源多遠距離\napproximately how close should you be to a fire when usi",
    options: ["A. 2 to 4 feet", "B. 4 to 6 feet", "C. 6 to 8 feet"],
    answer: "C"
  },
  {
    question: "⼀個⾃信⼼不強的⼈\na person with low self-esteem is",
    options: ["A. 減少可能順從同儕的壓⼒ less likely to conform to peer\npresure", "B. 可能順從同儕的壓⼒ more likely to conform to peer\npressure.", "C. 順應同儕的壓⼒但不影響⾃尊的等級 Conformity to peer pressure is\nnot affected by level of self- esteem"],
    answer: "B"
  },
  {
    question: "眼睛需要時間來適應不同層次的光強度。是⼀種\nthe eye requires time to adjust to varying levels of\nlight intensity because the",
    options: ["A. 光化學程序 photochemcial process", "B. 電化學程序 electrochemical process", "C. 神經傳導程序 nerve transmit process"],
    answer: "A"
  },
  {
    question: "在顯⽰器中，⼯作⼈員必須立即採取⾏動以保持系統安全的資訊是屬於\nIn display signal, the crew must react in order to\nmaintain the system safety is",
    options: ["A. 警告 warninig", "B. 提醒 alert", "C. 諮詢 advisory"],
    answer: "A"
  },
  {
    question: "從SHELL模型的觀點，空間迷向的問題屬於哪⼀個界⾯\nFrom SHELL model, the space disorientation problems belong to which interface",
    options: ["A. ⼈-軟體 liveware-software", "B. ⼈-環境 liveware-environment", "C. ⼈-硬體 liveware-handware"],
    answer: "B"
  },
  {
    question: "⼀個簡單系統維護的⽬的是什麼?\n1.⽬的是很容易理解的\n2.外型配置是很容易理解的\n3.功能是很容易理解的\nwhat is a simple system for maintenance\npurposes?\n1.purpose is easy to comprehend\n2.model is easy to comprehend\n3.function is easy to comprehend",
    options: ["A. 2 and 3 only", "B. 1,2 and 3 only", "C. 1 and 2 only"],
    answer: "B"
  },
  {
    question: "什麼是⼈們對不同的氣候條件的容許限度?\nwhat are the levels of tolerance people have to\ndifferent climatic conditions?",
    options: ["A. 最理想的溫度範圍(⾼⾄低)約10度c\nthe range of optimum temperature (high to low ) is about 10 degrees Celsius.", "B. 最理想的溫度範圍(⾼⾄低)約15度c\nthe range of optimum temperature (high to low ) is about 15 degrees Celsius.", "C. 最理想的溫度範圍(⾼⾄低)約7度c\nthe range of optimum\ntemperature (high to low ) is about 7 degrees Celsius."],
    answer: "C"
  },
  {
    question: "什麼是⼈們對不同的氣候條件的容許限度?\nwhat are levels of tolerance people have to\ndifferent climatic conditions?",
    options: ["A. 最佳濕度範圍(⾼⾄低)是20%左右\nthe range of optimum humidity\n(high to low ) is about 20%", "B. 最佳濕度範圍(⾼⾄低)是40%左右\nthe range of optimum humidity\n(high to low ) is about 40%", "C. 最佳濕度範圍(⾼⾄低)是60%左右\nthe range of optimum humidity\n(high to low ) is about 60%"],
    answer: "C"
  },
  {
    question: "什麼是正向同濟壓⼒的安全意涵?\n1.隱藏的壓⼒，降低風險\n2.更多的適應性，降低風險\n3.更⾼的標準，降低風險.\nwhat are the safety implications of positive peer\npressure?\n1.hidden presure 2….",
    options: ["A. 1 and 3 only", "B. 1 and 2 only", "C. 2 and 3 only"],
    answer: "C"
  },
  {
    question: "在⾶機維修⼯程領域什麼是最重要的溝通⽅式\nwhat is the most inportant mean of communication\nin aircraft maintenance",
    options: ["A. 含蓄 Implicit", "B. 逐字的 verbal", "C. 畫⾯ written"],
    answer: "C"
  },
  {
    question: "當指令的格式各不相同，針對⼯作指令有效性的因素何者影響最⼤\nWhat factor of effective work instruction is most affected when instructions use different formats?",
    options: ["A. 指令的可達性 accessibility of instruction", "B. 指令的⼀致性 consistency of instruction", "C. 指令的公信⼒ credibility of instruction"],
    answer: "B"
  },
  {
    question: "什麼有效⼯作指令的因素是受影響最⼤，當主管啟動⼀個的變化和標準化最佳做法的差異？\nWhat factor of effective work instruction is most affected when a supervisor initiates a change and deviates from standardized best practice?",
    options: ["A. 公信⼒的指令 credibility of instruction", "B. 輔助功能的指令 accessibility of instruction", "C. 清晰的指令 clearness of instruction", "D. ⼀致性的指令 consistency of instruction"],
    answer: "A"
  },
  {
    question: "什麼有效的⼯作指令因素是受影響最⼤,當恢復和參考系統是很難使⽤時？\nWhat factor of effective work instruction is most affected when a retrieval and reference system is difficult to use?",
    options: ["A. 公信⼒的指令 credibility of instruction", "B. 輔助功能的指令 accessibility of instruction", "C. 清晰的指令 clearness of instruction", "D. ⼀致性的指令 consistency of instruction"],
    answer: "B"
  },
  {
    question: "什麼有效的⼯作指令因素是受影響最⼤,當指令使⽤不同的格式時？\nWhat factor of effective work instruction is most affected when instructions use different formats?",
    options: ["A. 公信⼒的指令 credibility of instruction", "B. 輔助功能的指令 accessibility of instruction", "C. ⼀致性的指令 consistency of instruction", "D. 清晰的指令 clearness of instruction"],
    answer: "C"
  },
  {
    question: "⼀名⼯⼈在什麼情況會作出錯誤的液壓系統保養?\nIn what case would a worker make an error\nservicing the hydraulic system?",
    options: ["A. ⼯⼈有意或無意地不去加壓液壓系統.\nThe worker knowingly or unknowingly does NOT pressurize the system.", "B. ⼯⼈有意或無意地添加了錯誤的壓⼒.\nThe worker knowingly or unknowingly adds the wrong pressure.", "C. ⼯⼈在不知不覺中添加了錯誤的壓⼒.\nThe worker unknowingly adds the wrong pressure.", "D. ⼯⼈故意添加錯誤的壓⼒.\nThe worker knowingly adds the\nwrong pressure."],
    answer: "C"
  },
  
  {
    question: "在什麼情況下會是⼀個錯誤例⼦，如果⼀個⼯⼈安裝⼀個⽀撐架時？\nIn what case would it be an error if a worker installs a support bracket?",
    options: [
      "A. ⼯作⼈員有意或無意地不安裝螺栓. The worker knowingly or unknowingly does NOT install the bolts.",
      "B. ⼯作⼈員有意或無意地安裝了錯誤的螺栓. The worker knowingly or unknowingly installs the wrong bolts.",
      "C. ⼯作⼈員故意地安裝了錯誤的螺栓. The worker knowingly installs the wrong bolts.",
      "D. ⼯作⼈員在不知不覺中安裝了錯誤的螺栓. The worker unknowingly installs the wrong bolts."
    ],
    answer: "D"
  },
  {
    question: "你檢查⼿冊，並要求你的同事的意⾒。你也有很好的訓練。零件和⼯具都是正確的。你再次檢查你的⼯作。但是，出錯了。是什麼⼈為因素術語描述這種情況呢？\nYou checked the manual and asked your coworkers for advice. You also had good training. The parts and tools were all correct. You double checked your work. But, something went wrong. What human factors term describes this situation?",
    options: [
      "A. 錯誤的冰⼭ the Error Iceberg",
      "B. 錯誤鏈 the Chain of Errors",
      "C. ⾺斯洛階層 Maslow's Hierarchy",
      "D. 墨菲定律 Murphy's law"
    ],
    answer: "D"
  },
  {
    question: "哪種錯誤模式描述了⼤多數向公眾隱藏的維護失誤？\nWhich error model describes most maintenance errors as hidden to the public?",
    options: [
      "A. 錯誤的冰⼭ The Error Iceberg",
      "B. 瑞⼠奶酪模式 The Swiss Cheese Model",
      "C. ⼗⼆⼤禍因 The Dirty Dozen",
      "D. 螺帽和螺栓拆卸，組裝 The Nut and Bolt Disassembly, Assembly"
    ],
    answer: "A"
  },
  {
    question: "哪種誤差模式顯⽰如何“預防或糾正措施”來制⽌⼀個意外發⽣的危險性？\nWhich error model shows how \"preventive or corrective measures\" stop the danger of an accident?",
    options: [
      "A. 錯誤的冰⼭ The Error Iceberg",
      "B. 瑞⼠奶酪模式 The Swiss Cheese Model",
      "C. ⼗⼆⼤禍因 The Dirty Dozen",
      "D. 螺帽和螺栓拆卸，組裝 The Nut and Bolt Disassembly, Assembly"
    ],
    answer: "B"
  },
  {
    question: "哪種錯誤模式描述了維護中常⾒的錯誤？\nWhich error model describes common errors in maintenance?",
    options: [
      "A. 錯誤的冰⼭ The Error Iceberg",
      "B. 瑞⼠奶酪模式 The Swiss Cheese Model",
      "C. ⼗⼆⼤禍因 The Dirty Dozen",
      "D. 螺帽和螺栓拆卸，組裝 The Nut and Bolt Disassembly, Assembly"
    ],
    answer: "C"
  },
  {
    question: "哪種錯誤模式描述了維修⼯作的複雜性是如何增加了出錯的機會？\nWhich error model describes how the complexity of maintenance tasks increase the chance of error?",
    options: [
      "A. 錯誤的冰⼭ The Error Iceberg",
      "B. 瑞⼠奶酪模式 The Swiss Cheese Model",
      "C. ⼗⼆⼤禍因 The Dirty Dozen",
      "D. 螺帽和螺栓拆卸，組裝 The Nut and Bolt Disassembly, Assembly"
    ],
    answer: "D"
  },
  {
    question: "哪種錯誤模式描述⼀件事故發⽣錯誤的組合呢？\nWhich error model describes the occurrence of an accident as a combination of errors?",
    options: [
      "A. 錯誤的冰⼭ The Error Iceberg",
      "B. 瑞⼠奶酪模式 The Swiss Cheese Model",
      "C. 事件的連鎖反應 The Chain of Events",
      "D. 螺帽和螺栓拆卸，組裝 The Nut and Bolt Disassembly, Assembly"
    ],
    answer: "C"
  },
  {
    question: "哪個模型指⽰錯誤可以因重複檢查及交互檢查⽽停⽌?\nWhich model indicates errors can be stopped by duplicate checks and cross-checks?",
    options: [
      "A. 錯誤冰⼭",
      "B. 瑞⼠起司理論",
      "C. Dirty Dozen"
    ],
    answer: "B"
  },
  {
    question: "⼀架⾶機失去了在⾶⾏中的1號發動機整流罩。哪種錯誤模式最佳地描述了未拴緊的整流罩，如同重覆發⽣的問題？\nAn airplane looses its #1 engine cowling in flight. Which error model best describes the unlatched cowling as a re-occurring problem?",
    options: [
      "A. 錯誤的冰⼭ The Error Iceberg",
      "B. 瑞⼠奶酪模式 The Swiss Cheese Model",
      "C. ⼗⼆⼤禍因 The Dirty Dozen",
      "D. 螺帽和螺栓拆卸，組裝 The Nut and Bolt Disassembly, Assembly"
    ],
    answer: "A"
  },
  {
    question: "在他的⾶⾏前檢查，副駕駛注意到＃1發動機整流罩是未鎖上. 哪種錯誤模式最佳地描述了這⼀發現？\nOn his pre-flight check, the co-pilot notices the #1 engine cowling is NOT latched. Which error model best describes this finding?",
    options: [
      "A. 錯誤的冰⼭ The Error Iceberg",
      "B. 瑞⼠奶酪模式 The Swiss Cheese Model",
      "C. ⼗⼆⼤禍因 The Dirty Dozen",
      "D. 螺帽和螺栓拆卸，組裝 The Nut and Bolt Disassembly, Assembly"
    ],
    answer: "B"
  },
  {
    question: "當⼀名機械師正在關閉1號發動機整流罩時他被叫走去移動⼯作梯架. 當他返回現場收⼯時，他錯過了⼀個⾨閂和整流罩在⾶⾏中遺失了. 哪種錯誤模式最佳地描述這個錯誤？\nAs a mechanic is closing the #1 engine cowling, he is called away to help move a work stand. When he returns to close-up the job he misses a latch and the cowling is lost in flight. Which error model best describe this error?",
    options: [
      "A. 錯誤的冰⼭ The Error Iceberg",
      "B. 瑞⼠奶酪模式 The Swiss Cheese Model",
      "C. ⼗⼆⼤禍因 The Dirty Dozen",
      "D. 螺帽和螺栓拆卸，組裝 The Nut and Bolt Disassembly, Assembly"
    ],
    answer: "C"
  },
  {
    question: "⼀名⼯作⼈員正在檢查機翼⾯板的裂縫. 類型⼀的錯誤意味著⼯作⼈員 …\nA worker is checking a wing panel for cracks. A type one error means the worker …",
    options: [
      "A. ... 做了檢查，但沒有看到⼀條裂縫. ... did the inspection but did NOT see a crack.",
      "B. … 沒有做檢查. … did NOT do the inspection.",
      "C. … 在檢查時引起的裂紋. … made the crack during the inspection.",
      "D. … 看到了⼀條縫，確定它是無關緊要. … saw a crack and decided it was too small."
    ],
    answer: "D"
  },
  {
    question: "⼀名⼯作⼈員正在檢查機翼⾯板的裂縫. 類型⼆的錯誤意味著⼯作⼈員 …\nA worker is checking a wing panel for cracks. A type two error means the worker …",
    options: [
      "A. ... 做了檢查，但沒有看到⼀條裂縫. ... did the inspection but did NOT see a crack.",
      "B. … 沒有做檢查. … did NOT do the inspection.",
      "C. … 在檢查時引起的裂紋. … made the crack during the inspection.",
      "D. … 看到了⼀條縫，確定它是無關緊要. … saw a crack and decided it was too small."
    ],
    answer: "A"
  },
  {
    question: "是什麼類型的錯誤，如果存在⼀個故障，但不是在檢查中發現的呢？\nWhat type of error is it if a fault exists but is not found during an inspection?",
    options: [
      "A. 類型⼀的錯誤 type one error",
      "B. 類型⼆的錯誤 ytpe two error",
      "C. 類型三的錯誤 type three error",
      "D. 類型四的錯誤 type four error"
    ],
    answer: "B"
  },
  {
    question: "什麼類型的錯誤是如果發現故障就採取錯誤的⾏動呢？\nWhat type of error is it if a fault is found and the wrong action is taken?",
    options: [
      "A. 類型⼀的錯誤 type one error",
      "B. 類型⼆的錯誤 ytpe two error",
      "C. 類型三的錯誤 type three error",
      "D. 類型四的錯誤 type four error"
    ],
    answer: "A"
  },
  {
    question: "由於在維修⼿冊中的錯誤並未使⽤校正⼯具去安裝在⼀個渦輪發動機的後進油料管. 這些錯誤是如何分類的？\nDue to an error in the maintenance manual an alignment tool is not used to install the rear oil feed tube of a turbine engine. How are these errors classified?",
    options: [
      "A. 維修⼿冊是潛在錯誤和安裝錯誤是積極的. The maintenance manual error is latent and the installation error is active.",
      "B. 維修⼿冊的錯誤，並且安裝錯誤是潛在的問題. Both the maintenance manual error and the installation error are latent.",
      "C. 維修⼿冊錯誤是積極的和安裝錯誤是潛在的. The maintenance manual error is active and the installation error is latent.",
      "D. 維修⼿冊的錯誤和安裝錯誤是積極的. Both the maintenance manual error and the installation error are active."
    ],
    answer: "B"
  },
  {
    question: "由於在維修⼿冊中的錯誤並未使⽤校正⼯具去安裝在⼀個渦輪發動機的後進油料管. 在操作中進料管上的壓⼒造成裂紋. 這些錯誤是如何分類的？\nDue to an error in the maintenance manual an alignment tool is not used to install the rear oil feed tube of a turbine engine. In operation, the stress on the feed line is causing a crack. How are these errors classified?",
    options: [
      "A. 維修⼿冊是潛在錯誤和安裝錯誤是積極的. The maintenance manual error is latent and the installation error is active.",
      "B. 維修⼿冊的錯誤，並且安裝錯誤是潛在的問題. Both the maintenance manual error and the installation error are latent.",
      "C. 維修⼿冊的錯誤和安裝錯誤是積極的. Both the maintenance manual error and the installation error are active.",
      "D. 維修⼿冊錯誤是積極的和安裝錯誤是潛在的. The maintenance manual error is active and the installation error is latent."
    ],
    answer: "C"
  },
  {
    question: "上緊螺絲時抓住燃料電池檢測板⽽不使⽤扭⼒扳⼿是 …\nNot using a torque wrench to tighten the screws holding the fuel cell inspection plate is …",
    options: [
      "A. … ⼀個潛在的錯誤如果螺紋滑牙和⼀個主動的錯誤如果他們沒有滑牙. … a latent error if the threads are stripped and an active error if they are NOT stripped.",
      "B. … ⼀個潛在的錯誤如果螺紋滑牙和⼀個潛在的錯誤如果他們沒有滑牙. … a latent error if the threads are stripped and a latent error if they are NOT stripped.",
      "C. … ⼀個主動的錯誤如果螺紋滑牙和⼀個主動的錯誤如果他們沒有滑牙. … an active error if the threads are stripped and an active error if they are NOT stripped.",
      "D. … ⼀個主動的錯誤如果螺紋滑牙和⼀個潛在的錯誤如果他們沒有滑牙. … an active error if the threads are stripped and a latent error if they are NOT stripped."
    ],
    answer: "D"
  },
  {
    question: "何謂潛在失效?\nWhat is a latent failure?",
    options: [
      "A. 可被偵測到之失效 A failure which could have been predicted",
      "B. 遵從不熟悉⾶機維修之管理者指⽰ Receiving bad instruction from a manager who is out of touch with maintenance",
      "C. 未被預測到之失效 a failure which could not have been predicted"
    ],
    answer: "C"
  },
  {
    question: "以下哪些原因被列為事故？\n1）⾶機在機棚火災被摧毀.\n2）整流罩在⾶⾏過程中脫落.\n3）⾶機經歷了機艙減壓.\nWhich of the following are classified as incidents?\n1)An aircraft is destroyed in a hangar fire.\n2)The cowling comes off during flight.\n3)The airplane experiences a cabin depressurization.",
    options: [
      "A. 僅（1）和（2）",
      "B. 僅（2）和（3）",
      "C. 僅（1）和（3）",
      "D. (1), (2) 和 (3)"
    ],
    answer: "B"
  },
  {
    question: "下列哪項被歸類意外？\n1）⾶機在機棚火災被摧毀.\n2）整流罩在⾶⾏過程中脫落，發動機損壞.\n3）兩個⼈被吸出機外在⼀個失壓過程中.\nWhich of the following are classified as accidents?\n1)An aircraft is destroyed in a hangar fire.\n2)The cowling comes off during flight and the engine is damaged.\n3)Two people are sucked out of the plane during a depressurization.",
    options: ["A. 僅（1）和（2）", "B. 僅（2）和（3）", "C. 僅（1）和（3）", "D. (1), (2) 和 (3)"],
    answer: "C"
  },
  {
    question: "為什麼不尋常的維修⼈員將被控訴過失犯罪？\nWhy is it unusual for maintenance workers to be charged with criminal negligence?",
    options: [
      "A. 指控的威脅妨礙調查. The threat of charges impedes investigations.",
      "B. 錯誤通常還是在於管理. The fault usually lies with the management.",
      "C. 維修⼯⼈很少犯錯誤. Maintenance workers rarely make errors.",
      "D. 宣傳損害了航空業. The publicity damages the air industry."
    ],
    answer: "A"
  },
  {
    question: "當維修錯誤指責是分攤 ...\nWhen blame for maintenance errors is apportioned …",
    options: [
      "A. … 責任變得釐清. … responsibility becomes clear.",
      "B. ...它有⼀個學習過程中的負⾯影響. … it has a negative affect on the learning process.",
      "C. … 它可以防⽌再次發⽣錯誤. … it prevents the errors from re-occurring.",
      "D. … 它改善了⼯作者的習慣和動⼒. … it improves worker habits and motivation."
    ],
    answer: "B"
  },
  {
    question: "在⾶⾏中關⾞的內部調查著重在維修⼯⼈使⽤了錯誤O型圈的責任. 這種類型的發現 …\nAn internal investigation on an in flight shut down placed the responsibility on the maintenance worker for using the wrong O rings. This type of finding …",
    options: [
      "A. … 使⼯⼈在他們的⼯作更加細⼼. … makes workers more attentive in their work.",
      "B. … 防⽌了錯誤的再次發⽣. … prevents a re-occurrence of the error.",
      "C. … 可能再次出現的錯誤. … makes the error likely to re-occur.",
      "D. … 需要責任的釐清. … makes the need for responsibility clear."
    ],
    answer: "C"
  },
  {
    question: "為什麼意外事故調查要尋找很多可能構成⼀連串的原因？\nWhy do accident/incident investigations look for many causes that make up a chain of events?",
    options: [
      "A. 它給每個⼈更多的動⼒做好⼯作. It gives everyone more motive to do good work.",
      "B. 它有助於防⽌錯誤的再次發⽣. It helps prevent a re-occurrence of the error.",
      "C. 它使公眾感到更加安全. It makes the public feel more safe.",
      "D. 它可以幫助分攤責任. It helps apportion the responsibility."
    ],
    answer: "B"
  },
  {
    question: "什麼是正確的順序在維護錯誤決策援助過程中的三個步驟?\nWhat is the correct order of the three steps in the MEDA process?",
    options: [
      "A. 採取糾正措施，找到促成因素和識別錯誤. Take corrective actions, find contributing factors and identify the error.",
      "B. 採取糾正措施，識別錯誤和發現促成因素. Take corrective actions, identify the error and find contributing factors.",
      "C. 識別錯誤，採取糾正措施，並找到促成因素. Identify the error, take corrective actions and find contributing factors.",
      "D. 識別錯誤，找到促成因素，並採取糾正措施. Identify the error, find contributing factors and take corrective actions."
    ],
    answer: "D"
  },
  {
    question: "什麼不是維護錯誤決策援助過程中的⼀部分？\nWhat is NOT a part of the MEDA process?",
    options: [
      "A. 責任分配 proportioning responsibility",
      "B. 識別錯誤 identifying errors",
      "C. 找出促成因素 finding contributing factors",
      "D. 採取糾正措施 taking corrective actions"
    ],
    answer: "A"
  },
  {
    question: "維護錯誤決策援助⾸要的理念是什麼？\nWhat is the prime philosophy of MEDA?",
    options: [
      "A. 因為我們是⼈都會做出錯誤. Because we're human we make mistakes.",
      "B. 所有的錯誤都是可以避免的. All errors are preventable.",
      "C. 我們可以學到很多來⾃我們的錯誤. We can learn a lot from our errors.",
      "D. 如果它會做錯，就會出問題. If it can go wrong it will go wrong."
    ],
    answer: "C"
  },
  {
    question: "維護錯誤決策援助和⼗⼆⼤禍因被⽤來標⽰維護錯誤的促成因素. 什麼是真正的改正措施？\nBoth MEDA and the Dirty dozen can be used to identify contributing factors of maintenance errors. What is true for the corrective actions?",
    options: [
      "A. 只有維護錯誤決策援助有⼀套改正措施. Only MEDA has a set of corrective actions",
      "B. 兩者都有⼀套改正措施. Both have a set of corrective actions.",
      "C. 只有⼗⼆⼤禍因有⼀套改正措施. Only the dirty dozen has a set of corrective actions.",
      "D. 兩者都沒有⼀套改正措施. Neither have a set of corrective actions."
    ],
    answer: "B"
  },
  {
    question: "以下哪項陳述是真實的依據維護錯誤決策援助的調查⽽採⽤改正措施？\nWhich of the following statements is true for the use of corrective action following a MEDA investigation?",
    options: [
      "A. 它們是⼀般⼯作地點所依賴的失誤. They are general to the work place and depend on the error.",
      "B. 它們是特定⼯作地點所依賴的失誤. They are specific to the work place and depend on the error.",
      "C. 他們是⼀般⼯作地點所依賴的提供因素. They are general to the work place and depend on the contributing factors.",
      "D. 它們是特定⼯作地點所依賴的提供因素. They are specific to the work place and depend on the contributing factors."
    ],
    answer: "D"
  },
  {
    question: "什麼是真正的危害⼯作場所的識別和報告？\nWhat is true for the recognizing and reporting of hazards in the work place?",
    options: [
      "A. 雇主必須認識到潛在的危險和僱員必須報告它們. The employer must recognize potential hazards and an employee must report them.",
      "B. 雇主必須認識到的危害和報告它們. The employer must recognize hazards and report them.",
      "C. 員⼯必須認識到潛在的危險，雇主必須他們報告它們. The employee must recognize potential hazards and an employer must report them.",
      "D. 員⼯必須認識到危害並報告它們. The employee must recognize hazards and report them."
    ],
    answer: "A"
  },
  {
    question: "誰有責任去提供援助和防護來⾃⼯作場所的危險？\nWhose responsibility is it to provide aid and protection from work place hazards?",
    options: [
      "A. 雇主必須提供援助和僱員必須提供保護. The employer must provide aid and the employee must provide protection.",
      "B. 雇主必須提供援助和保護. The employer must provide both aid and protection.",
      "C. 雇員必須提供援助和保護. The employee must provide both aid and protection.",
      "D. 雇員必須提供援助和僱主必須提供保護. The employee must provide aid and the employer must provide protection."
    ],
    answer: "B"
  },
  {
    question: "什麼是真實的為了去除或消除危險⽽製做的安全信息？\nWhat is true for the removal or elimination of hazards and making note of safety information?",
    options: [
      "A. 僱員必須清除或消除危險和雇主必須使⽤附註的安全信息. The employee must remove or eliminate hazards and the employer must take note of safety information.",
      "B. 僱員必須清除或消除危險和使⽤附註的安全信息. The employee must remove or eliminate hazards and must take note of safety information.",
      "C. 雇主必須清除或消除危險和僱員必須使⽤附註的安全信息. The employer must remove or eliminate hazards and the employee must take note of safety information.",
      "D. 僱主必須清除或消除危險和使⽤附註的安全信息. The employer must remove or eliminate hazards and must take note of safety information."
    ],
    answer: "C"
  },
  {
    question: "誰有責任確保使⽤所提供的安全措施?\n（1）雇主\n（2）⺠航局\n（3）僱員\nWho is responsible for making sure the provided safety measures are used?\n(1)the employer\n(2)the CAA\n(3)the employee",
    options: ["A. 只有（1）", "B. 只有（1）和（2）", "C. 只有（3）", "D. （1），（2）和（3）"],
    answer: "C"
  },
  {
    question: "以下哪種危險對⾶機維修環境是最常⾒的？\nWhich of the following hazards is most common to the aircraft maintenance environment?",
    options: [
      "A. 因溢出滑油或噴射燃油⽽滑倒 slipping on spilled oil or jet fuel",
      "B. 傷⼝碰到液壓油 getting hydraulic oil on a cut",
      "C. 在熱發動機零件上燙傷你的⼿ burning your hands on hot engine parts",
      "D. 你的頭撞到發動機整流罩. Hitting your head on an engine cowling."
    ],
    answer: "D"
  },
  {
    question: "以下哪種危險對⾶機維修環境是最常⾒的？\nWhich of the following hazards is most common to the aircraft maintenance environment?",
    options: [
      "A. 在⼀個平台上，梯⼦或檢修棚絆倒 tripping on a platform, ladder or dock",
      "B. 傷⼝碰到液壓油 getting hydraulic oil on a cut",
      "C. 在熱發動機零件上燙傷你的⼿ burning your hands on hot engine parts",
      "D. 因溢出滑油或噴射燃油⽽滑倒 slipping on spilled oil or jet fuel"
    ],
    answer: "A"
  },
  {
    question: "什麼樣類型的⼯作場所有⼀個紅⾊圓形帶和⼀個紅⾊的斜線的標誌？\nWhat type of workplace sign has a red circular band and a red diagonal line?",
    options: [
      "A. 禁⽌的標誌 sign of prohibition",
      "B. 必要的預防措施 essential precaution",
      "C. 警告標誌 warning sign",
      "D. 安全性的信息 information of a safety nature"
    ],
    answer: "A"
  },
  {
    question: "什麼類型的⼯作場所標誌使⽤⼀個藍⾊的盤狀物?\nWhat type of workplace sign uses a blue disc?",
    options: [
      "A. 禁⽌的標誌 sign of prohibition",
      "B. 必要的預防措施 essential precaution",
      "C. 警告標誌 warning sign",
      "D. 安全性的信息 information of a safety nature"
    ],
    answer: "B"
  },
  {
    question: "什麼類型的標誌已鑲上⿊⾊帶黃⾊三⾓形？\nWhat type of sign has a yellow triangle bordered by a black band?",
    options: [
      "A. 禁⽌的標誌 sign of prohibition",
      "B. 必要的預防措施 essential precaution",
      "C. 警告標誌 warning sign",
      "D. 安全性的信息 information of a safety nature"
    ],
    answer: "C"
  },
  {
    question: "什麼類型的標誌在⼀個綠⾊正⽅形上有⼀個⽩⾊的記號？\nWhat type of sign has a white symbol on a green square?",
    options: [
      "A. 禁⽌的標誌 sign of prohibition",
      "B. 必要的預防措施 essential precaution",
      "C. 警告標誌 warning sign",
      "D. 安全性的信息 information of a safety nature"
    ],
    answer: "D"
  },
  {
    question: "對於⼀般的緊急情況你應該 ...\nFor general emergencies you should …",
    options: [
      "A. … 在照顧受害者之前報告緊急情況. … report the emergency before taking care of a victim.",
      "B. … ⽤任何辦法幫忙在你報告緊急情況之前. … help in any way you can before you report the emergency.",
      "C. … 報告緊急情況在你確信發⽣的事情之前. … report the emergency before you are sure of what happened.",
      "D. … 使得事情無危險在你報告緊急情況之前. … make things safe before you report the emergency."
    ],
    answer: "A"
  },
  {
    question: "有五點處理⼀般緊急情況. 最後⼀點是 …\nThere are five points for dealing with general emergencies. The last of these is …",
    options: [
      "A. … 報告緊急情況. … report the emergency.",
      "B. ... 你可以⽤任何⽅式幫忙. … help in any way you can.",
      "C. ... 使得事情無危險性. … make things safe.",
      "D. … 採取照顧受害者. … take care of the victim."
    ],
    answer: "B"
  },
  {
    question: "你聽到了很多從機棚後⾯傳來的聲響，並看到儲藏室冒煙. 在地板上有⼀些⼈燙傷,但每個⼈沒有立即的危險. 你應該怎麼做呢？\nYou hear a lot of noise coming from the back of the hangar and see smoke coming out of the store room. There are some people with burns on the floor but everyone is out of immediate danger.\nWhat should you do?",
    options: [
      "... 你可以⽤任何⽅式幫忙. … help in any way you can.",
      "... 使得事情無危險性. … make things safe.",
      "… 報告緊急情況. … report the emergency.",
      "… 採取照顧受害者. … take care of the victims."
    ],
    answer: "C"
  },
  {
    question: "處理⼀般緊急情況五個重點中，最後⼀點是？",
    options: [
      "A. 可以⽤任何⽅式幫忙",
      "B. 使事情無危險性",
      "C. 照顧受害勢",
      "D. 報告緊急情況"
    ],
    answer: "A"
  },
  {
    question: "⼀個⼿提式滅火器完全流出⼤約需要多久時間？\nApproximately how long does it take for a portable fire extinguisher to discharge completely?",
    options: [
      "A. 4秒 4 seconds",
      "B. 8秒 8 seconds",
      "C. 12秒 12 seconds",
      "D. 16秒 16 seconds"
    ],
    answer: "B"
  },
  {
    question: "操作滅火器時最重要的考慮因素是什麼？\nWhat is the most important consideration when operating a fire extinguisher?",
    options: [
      "A. 檢查操作指令 checking the instructions",
      "B. 滅火器排出時間 extinguisher discharge time",
      "C. 滅火器的位置 location of the fire extinguisher",
      "D. 逃⽣路線 an escape route"
    ],
    answer: "D"
  },
  {
    question: "你⼤約可靠近火源多遠距離當使⽤⼀個滅火器時？\nApproximately how close should you be to a fire when using an extinguisher?",
    options: [
      "A. 2⾄4英尺 2 to 4 feet",
      "B. 4⾄6英尺 4 to 6 feet",
      "C. 6⾄8英尺 6 to 8 feet",
      "D. 8⾄10英尺 6 to 10 feet"
    ],
    answer: "C"
  },
  {
    question: "有煙和火從機棚牆壁上的斷路器盒冒出來. 你需要什麼類型滅火器來滅火？\nThere is smoke and fire coming out of a breaker box on the hangar wall. What class of fire extinguisher do you need?",
    options: ["A. A類型", "B. B類型", "C. C類型", "D. D類型"],
    answer: "C"
  },
  {
    question: "下列哪些說法是正確的？有煙和火從機棚牆壁上的斷路器盒冒出來. 您注意到⼀個乾粉和⼀個⼆氧化碳滅火器.\nWhat statement is true for the following conditions? There is smoke and fire coming out of a breaker box on the hangar wall. You notice a dry powder and a CO2 extinguisher.",
    options: [
      "A. 火源是⼀種B類型火災，您可以同時使⽤兩者滅火器. The fire is a class B fire and you can use both extinguishers.",
      "B. 火是⼀種B類型火災，你僅可以使⽤化學乾粉. The fire is a class B fire and you can use the dry powder chemical ONLY.",
      "C. 火源是⼀種C類型火災，您可以同時使⽤兩者滅火器. The fire is a class C fire and you can use both extinguishers.",
      "D. 火是⼀種C類型火災，你僅可以使⽤化學乾粉. The fire is a class C fire and you can use the dry powder chemical ONLY."
    ],
    answer: "C"
  },
  {
    question: "實施⼼肺復甦術(氣道、呼吸、循環)胸部按壓是屬於",
    options: [
      "A. 循環急救",
      "B. 呼吸急救",
      "C. 氣道和呼吸急救"
    ],
    answer: "A"
  },
  {
    question: "什麼是ABC的急救⽅法當處理失去知覺的個⼈時？\nWhat is the ABC of first aid when dealing with an unconscious person?",
    options: [
      "A. 評估，⼩⼼，呼叫 assess, beware, call",
      "B. 氣道，呼吸，循環 airway, breathing, circulation",
      "C. 氣道，休息，逃避 airway, breaks, cuts",
      "D. 協助，意識，覆蓋和保護 assist, be aware, cover and protect"
    ],
    answer: "B"
  },
  {
    question: "你發現⼀個⼈昏迷⽽你必須做的ABC（氣道，呼吸，循環）急救時. 聽覺和感覺是屬於哪⼀部分 …\nYou find a person unconscious and you must do ABC (airway, breathing, circulation) first aid. Listening and feeling are part of the …",
    options: [
      "A. … 氣道急救. … airway first aid.",
      "B. … 呼吸急救. … breathing first aid.",
      "C. … 氣道和呼吸急救. … airway and breathing first aid.",
      "D. … 氣道和呼吸急救. … airway, breathing and circulation first aid."
    ],
    answer: "B"
  },
  {
    question: "你發現⼀個⼈昏迷，並要實⾏施ABC（氣道，呼  吸，循環）急救. 傾斜頭部抬下巴操演是屬於哪⼀部分 …\nYou find a person unconscious and will do ABC (airway, breathing, circulation) first aid. The head tilt chin lift maneuver is part of the …",
    options: [
      "A. … 氣道急救. … airway first aid.",
      "B. … 呼吸急救. … breathing first aid.",
      "C. … 氣道和呼吸急救. … airway and breathing first aid.",
      "D. … 氣道和呼吸急救. … airway, breathing and circulation first aid."
    ],
    answer: "A"
  },
  {
    question: "你發現⼀個⼈昏迷，並要實⾏施ABC（氣道，呼吸，循環）急救. 胸部按壓是屬於哪⼀部分 …\nYou find a person unconscious and will do ABC first aid (airway, breathing, circulation). Chest compressions are part of the …",
    options: [
      "A. … 呼吸急救. … breathing first aid.",
      "B. … 氣道和呼吸急救. … airway and breathing first aid.",
      "C. … 氣道急救. … airway first aid.",
      "D. … 循環急救. … circulation first aid."
    ],
    answer: "D"
  },
  {
    question: "在信息處理模式中什麼遵循發⽣器的決定？\nWhat follows the decision generator in the information processing model?",
    options: [
      "A. 信號輸入和存儲 signal input and storage",
      "B. 意識的模組 awareness module",
      "C. ⾏動和反饋意⾒ action and feedback",
      "D. 注意機制 attention mechanism"
    ],
    answer: "C"
  },
  {
    question: "⾺斯洛說⼤多數⼈⾏動的動機是什麼呢？\nWhat does Maslow say is the motive for most human actions?",
    options: [
      "A. ⾃我實現 self realization",
      "B. ⽣理需要 physiological needs",
      "C. 歸屬感和親情 belonging and affection",
      "D. ⾃尊⼼ self esteem"
    ],
    answer: "B"
  },
  {
    question: "⾺斯洛需求理論中最低層次的需求是…",
    options: [
      "A. 尊重需要",
      "B. ⾃我實現需要",
      "C. 安全需要",
      "D. ⾝体需要"
    ],
    answer: "D"
  },
  {
    question: "壓⼒是⼀個正常的⽣活和健康的⼀部分是屬於 …\nStress that is a normal and healthy part of life is …",
    options: [
      "A. … 正⾯的. … positive.",
      "B. … 負⾯的. … negative.",
      "C. … 中性的. … neutral.",
      "D. … 累積的. … cumulative."
    ],
    answer: "A"
  },
  {
    question: "你是在燃料電池的⼯作中感到恐慌症開始發作. 你會怎麼做？\nYou are working in a fuel cell and feel the start of a panic attack. What do you do?",
    options: [
      "A. … 數到⼆⼗. … count to twenty.",
      "B. … 深呼吸. … take a deep breath.",
      "C. … 專注在您的⼯作. … focus on your work.",
      "D. … 告訴你的同事. … tell your co-workers."
    ],
    answer: "D"
  },
  {
    question: "什麼類型的⼯作最常感到⾃滿？\nWhat type of task most often causes complacency?",
    options: [
      "A. … 新的⼯作. … new tasks.",
      "B. … 挑戰性的⼯作. … challenging tasks.",
      "C. … 重複性的⼯作. … repetitive tasks.",
      "D. … 舊的⼯作. … old tasks."
    ],
    answer: "C"
  },
  {
    question: "⼀個⼩組成員指⽰你如何更換油塞。你如何給你的⼩組成員表明您已瞭解了嗎？\nA team member instructs you on how to change an oil plug. What do you give your team member to show you understand?",
    options: [
      "A. 想法 ideas",
      "B. 反饋意⾒ feedback",
      "C. 編碼 encoding",
      "D. 解碼 de-conding"
    ],
    answer: "B"
  },{
    question: "什麼樣的錯誤模式顯⽰常⾒的錯誤？\nWhat error model shows common errors?",
    options: [
      "A. 錯誤模式鏈 the chain of errors model",
      "B. 錯誤的冰⼭模式 the error iceberg model",
      "C. 瑞⼠奶酪模式 the Swiss cheese model",
      "D. 螺⺟和螺栓模式 the nuts and bolt model"
    ],
    answer: "A"
  },
  {
    question: "逃⽣路線，集合點，和⾏為規則清單是什麼的⼀部分 ...\nEscape routes, assembly points, and a checklist for rules of behavior are part of …",
    options: [
      "A. … ⼀個設施⼿冊. … a facilities manual.",
      "B. … ⼀個危險的區劃. … a danger zoning.",
      "C. … ⼀個緊急報告. … an emergency report.",
      "D. … ⼀個警報計劃. … an alarm plan."
    ],
    answer: "D"
  },
  {
    question: "航空器事故涉及⼈為因素問題時，與錯誤鏈的關係如何?",
    options: [
      "A. ⼈為因素問題是第⼀個錯誤鏈的連結",
      "B. ⼈為因素問題是最後⼀個錯誤鏈的連結",
      "C. ⼈為因素問題是所有錯誤鏈的連結"
    ],
    answer: "C"
  },
  {
    question: "⼈為因素研究最初⽬的是什麼？\nWhat is the original purpose of human factors research?",
    options: [
      "A. ⼈機配合 Man Machine fit",
      "B. 減少壓⼒ Reduction of pressure.",
      "C. 減少⼈為錯誤 Reduction of human error.",
      "D. 改善通訊 Improved communications."
    ],
    answer: "C"
  },
  {
    question: "⼈為的因素如何影響⼯程師的⼯作？\n1）⼈為因素造成的不滿.\n2）⼈為因素造成的缺勤.\n3）⼈為因素⿎勵⼯作者\nHow do human factors affect an engineers work?\n1)Human factors cause dissatisfaction.\n2)Human factors cause absenteeism.\n3)Human factors encourage a worker.",
    options: [
      "A. 1 & 2",
      "B. 2 & 3",
      "C. 1 & 3",
      "D. 1 & 2 & 3"
    ],
    answer: "D"
  },
  {
    question: "⼈為因素如何影響社會和實際的⼯作環境？\nHow do human factors affect the social and physical working environment?",
    options: [
      "A. ⼈為因素對社會環境有正⾯的影響和對實際環境有負⾯的影響. Human factors have a positive affect on the social environment and a negative affect on the physical environment.",
      "B. ⼈為因素對社會環境有負⾯的影響和對實際環境有負⾯的影響. Human factors have a negative affect on the social environment and a negative affect on the physical environment.",
      "C. ⼈為因素對社會和實際環境有著正⾯和負⾯的影響. Human factors have both positive and negative affects on the social and physical environments.",
      "D. ⼈為因素對社會環境有負⾯的影響和對實際環境有正⾯的影響. Human factors have a negative affect on the social environment and a positive affect on the physical environment."
    ],
    answer: "C"
  },
  {
    question: "SHEL模式⼯作是如何作為⼀個⼈為因素的架構？\nHow does the SHEL model work as a framework for human factors?",
    options: [
      "A. 它顯⽰了個別標題是如何的相互分離. It shows how individual topics are separated from each other.",
      "B. 它顯⽰了個別標題如何相互影響. It shows how individual topics affect each other.",
      "C. 它顯⽰了⼈為疏失的領域. It shows the areas for human error.",
      "D. 它顯⽰了如何可以防⽌⼈為疏失. It shows how human errors can be prevented."
    ],
    answer: "B"
  },
  {
    question: "⼯程師與 SHEL模式在實務的航空職位有何關係？\nHow does an engineer relate to the SHEL model in a practical aviation situation?",
    options: [
      "A. ⼯程師是S. The engineer is the S.",
      "B. ⼯程師是H. The engineer is the H.",
      "C. ⼯程師是E. The engineer is the E.",
      "D. ⼯程師是L. The engineer is the L."
    ],
    answer: "D"
  },
  {
    question: "⽤什麼⽅式來降低⼈類的不可靠性？\nWhat is a way to reduce human unreliability?",
    options: [
      "A. ⼈的協議 the human protocol",
      "B. 墨菲定律 Murphy's law",
      "C. 信息處理 information processing",
      "D. ⾃信管理 complacent management"
    ],
    answer: "A"
  },
  {
    question: "如何⽤訓練來降低維修疏失？\nHow does training reduce maintenance errors?",
    options: [
      "A. 訓練提⾼⼀般的⾃滿. Training increases general complacency.",
      "B. 訓練提⾼⼀般警覺性. Training increases general awareness.",
      "C. 培訓減少對溝通的需求. Training decreases the need for communication.",
      "D. 培訓減少對⾃信的需求. Training decreases the need for assertiveness."
    ],
    answer: "B"
  },
  {
    question: "以下哪個空難是由於維修不當在事故發⽣前22年？\nWhich of the following air crashes was due to an improper repair 22 years before the accident?",
    options: [
      "A. China Airlines flight 611 (B747)",
      "B. Singapore Airlines flight 606 (B747)",
      "C. Aloha Airlines flight 243 (B737)",
      "D. Chicago Airlines flight 191 (DC 10)"
    ],
    answer: "A"
  },
  {
    question: "以下哪個空難是由於改變了施⼯程序？\nWhich of the following air crashes was due to changed work procedures?",
    options: [
      "A. China Airlines flight 611 (B747)",
      "B. Singapore Airlines flight 606 (B747)",
      "C. Aloha Airlines flight 243 (B737)",
      "D. Chicago Airlines flight 191 (DC 10)"
    ],
    answer: "D"
  },
  {
    question: "以下哪個空難是由於許多⼈為因素造成的，包括修復程序，受訓，認證和關於技⼯和檢查員的資格限定？\nWhich of the following accidents / incidents was due to the fitting of incorrect bolts?",
    options: [
      "A. China Airlines flight 611 (B747)",
      "B. Singapore Airlines flight 606 (B747)",
      "C. Aloha Airlines flight 243 (B737)",
      "D. Chicago Airlines flight 191 (DC 10)"
    ],
    answer: "C"
  },
  {
    question: "在1996年5⽉, Valu Jet航班592墜毀在佛羅⾥達⼤沼澤地. 這起事故的主要原因是 …\nIn May 1996, Valu Jet flight 592 crashed into the Florida everglades. The main cause of this accident was …",
    options: [
      "A. 訓練不⾜ Insufficient Training.",
      "B. 缺乏溝通 Lack of communication.",
      "C. ⾃滿 Complacency",
      "D. 疲勞 Fatigue."
    ],
    answer: "A"
  },
  {
    question: "以下哪個意外/事故是由於裝配不正確的螺桿?\nWhich of the following accidents / incidents was due to the fitting of incorrect bolts?",
    options: [
      "A. China Airlines flight 120 (B737)",
      "B. Korean Airlines flight 801 (A300)",
      "C. British airways flight 5390 (BAC111)",
      "D. Valu Jet flight 592 (DC 9)"
    ],
    answer: "C"
  },
  {
    question: "以下哪個空難不是由維修失誤造成的？\nWhich of the following air crashes was NOT due to a maintenance error?",
    options: [
      "A. China Airlines flight 611 (B747)",
      "B. Singapore Airlines flight 606 (B747)",
      "C. Aloha Airlines flight 243 (B737)",
      "D. Chicago Airlines flight 191 (DC 10)"
    ],
    answer: "B"
  },
  {
    question: "限制性和因窒息的恐懼可能會導致 …\nThe fear of restriction and fear of suffocation can cause a …",
    options: [
      "A. … 懼⾼症. … acrophobics attack.",
      "B. ...幽閉恐懼症. … claustrophobic attack.",
      "C. … 廣場恐懼症. … agoraphobia.",
      "D. … 恐懼蜘蛛症. … arachnephobia attack."
    ],
    answer: "B"
  },
  {
    question: "什麼類型恐懼症的⼈極有可能害怕站在⼀個短的凳⼦上？\nWhat type of phobia would someone who has a fear of standing on a short stool most likely have?",
    options: [
      "A. 幽閉恐懼症 claustrophobia",
      "B. … 廣場恐懼症. … agoraphobia.",
      "C. 懼⾼症 acrophobia",
      "D. … 恐懼蜘蛛症. … arachnephobia."
    ],
    answer: "C"
  },
  {
    question: "⼀名⼯程師錯過了燃油箱裸線的檢查. 這種過失有可能是什麼原因引起的 …\nAn engineer misses a bare wire during a fuel cell inspection. This failing would most likely be caused by …",
    options: [
      "A. ... 懼⾼症. … acrophobia.",
      "B. … 廣場恐懼症. … agoraphobia.",
      "C. … 恐懼蜘蛛症. … arachnephobia.",
      "D. … 幽閉恐懼症. … claustrophobia."
    ],
    answer: "D"
  },
  {
    question: "在儲存和記憶恢復有三個主要階段. 什麼是這些階段的正確順序？\nThere are three main stages in the storage and retrieval of memory. What is the correct ordering of these stages?",
    options: [
      "A. 存儲，恢復和編碼 storing, retrieval and encoding",
      "B. 編碼，存儲和恢復 encoding, storing and retrieval",
      "C. 恢復，和編碼存儲 retrieval, encoding and storing",
      "D. 存儲，編碼和恢復 storing, encoding and retrieval"
    ],
    answer: "B"
  },
  {
    question: "在值班時你的督導給您⼯作的指⽰. 什麼記憶的過程是最有效的？\nYour supervisor is giving you instructions for the jobs on your shift. What memory process is most active?",
    options: [
      "A. 分組 grouping",
      "B. 存儲 storing",
      "C. 編碼 encoding",
      "D. 恢復 retrieval"
    ],
    answer: "C"
  },
  {
    question: "你正在檢查藍⾊液壓系統的壓⼒. 在開始任務之前你有校正資料來完成⼯作. 什麼記憶的過程是最有效 的？\nYou are checking the pressure on the blue hydraulic system. You have done the job and have reviewed the information before starting the task. What memory process is most active?",
    options: [
      "A. 分組 grouping",
      "B. 存儲 storing",
      "C. 編碼 encoding",
      "D. 恢復 retrieval"
    ],
    answer: "D"
  },
  {
    question: "您已經完成#2號發動機的機油濾⼼更換，休息⼀下喝杯咖啡. 什麼記憶的過程是最有效的？\nYou have finished changing the oil filter on the number two engine and will take a coffee break. What memory process is most active?",
    options: [
      "A. 分組 grouping",
      "B. 存儲 storing",
      "C. 編碼 encoding",
      "D. 恢復 retrieval"
    ],
    answer: "B"
  },
  {
    question: "不同的運動形式有不同的結果. 瑜伽…\nDifferent forms of exercise have different outcomes. Yoga …",
    options: [
      "A. … 增加在肌⾁和關節的運動範圍. … increases the range of motion in muscles and joints.",
      "B. … 提⾼⼼⾎管耐⼒. … increases cardiovascular endurance.",
      "C. … 增加短期的肌⾁⼒量. … increases short term muscle strength.",
      "D. … 增加了肥胖的可能性. … increases the likelihood of obesity."
    ],
    answer: "A"
  },
  {
    question: "不同的運動形式有不同的結果. 慢跑 …\nDifferent forms of exercise have different outcomes. Jogging …",
    options: [
      "A. … 增加在肌⾁和關節的運動範圍. … increases the range of motion in muscles and joints.",
      "B. … 提⾼⼼⾎管耐⼒. … increases cardiovascular endurance.",
      "C. … 增加短期的肌⾁⼒量. … increases short term muscle strength.",
      "D. … 增加了肥胖的可能性. … increases the likelihood of obesity."
    ],
    answer: "B"
  },
  {
    question: "不同的運動形式有不同的結果. 舉重 …\nDifferent forms of exercise have different outcomes. Weight lifting …",
    options: [
      "A. … 增加在肌⾁和關節的運動範圍. … increases the range of motion in muscles and joints.",
      "B. … 提⾼⼼⾎管耐⼒. … increases cardiovascular endurance.",
      "C. … 增加短期的肌⾁⼒量. … increases short term muscle strength.",
      "D. … 增加了肥胖的可能性. … increases the likelihood of obesity."
    ],
    answer: "C"
  },
  {
    question: "不同的運動形式有不同的結果，但缺乏運動 …\nDifferent forms of exercise have different outcomes\nbut a lack of exercise …",
    options: [
      "A. … 增加在肌⾁和關節的運動範圍. … increases the range of motion in muscles and joints.",
      "B. … 提⾼⼼⾎管耐⼒. … increases cardiovascular endurance.",
      "C. … 增加短期的肌⾁⼒量. … increases short term muscle strength.",
      "D. … 增加了肥胖的可能性. … increases the likelihood of obesity."
    ],
    answer: "D"
  },
  {
    question: "什麼是積極性的壓⼒反應？\nWhat is a reaction of positive stress?",
    options: [
      "A. 信息儲存 messengers are stored",
      "B. 在性能上減少 decrease in performance",
      "C. 感覺良好 feeling well",
      "D. 胃痛 stomach pains"
    ],
    answer: "C"
  },
  {
    question: "什麼是積極性的壓⼒反應？\n1）提⾼了性能\n2）信息儲存\n3）感覺良好\nWhat is a reaction of positive stress?\n1)increased performance\n2)messengers are stored\n3)feeling well",
    options: [
      "A. 僅（1）和（2） (1) and (2) only.",
      "B. 僅（2）和（3） (2) and (3) only.",
      "C. 僅（1）和（3） (1) and (3) only.",
      "D. (1), (2) 和 (3) (1), (2) and (3)"
    ],
    answer: "C"
  },
  {
    question: "關於壓⼒什麼說法是正確的？\nWhat statement on stress is true?",
    options: [
      "A. 壓⼒是積極的，當它放在立即⾏動時. Stress is positive when it is put into immediate action.",
      "B. 壓⼒是負⾯的，當它放在立即⾏動時.. Stress is negative when it is put into immediate action.",
      "C. 壓⼒是積極的，當它的信息被儲存. Stress is positive when its messengers are stored.",
      "D. 壓⼒始終為負⾯的. Stress is always negative."
    ],
    answer: "A"
  },
  {
    question: "你有充分的時間來完成⼀個任務⽽把它拖延. 由此產⽣的壓⼒可能 …\nYou have a task to do and have lots of time to do it\nso put it off. The resultant stress is likely to …",
    options: [
      "A. … 減少信息. … decrease messengers.",
      "B. … 貯存信息. … store messengers.",
      "C. … 提⾼性能. … boost performance.",
      "D. … 增加福祉. … increase well being."
    ],
    answer: "C"
  },
  {
    question: "什麼不是⼀種壓⼒信息？\nWhat is NOT a stress messenger?",
    options: [
      "A. 膽固醇 cholesterol",
      "B. 腎上腺素 adrenaline",
      "C. ⼼率下降 decreased heart rate",
      "D. ⾎壓升⾼ increased blood pressure"
    ],
    answer: "C"
  },
  {
    question: "時間的壓⼒可以藉由減少⼯作份量，分擔⼯作的負荷，增加知識，並要求更多的時間.  是誰處於最佳位置以降低時間壓⼒？\nTime pressure can be reduced by reducing the number of tasks, sharing the work load, increasing knowledge and asking for more time. Who is in the best position to reduce time pressure?",
    options: [
      "A. 管理者 the management",
      "B. 輪班督導 shift supervisors",
      "C. ⼩組領導 team leaders",
      "D. ⼯作者 the workers"
    ],
    answer: "D"
  },
  {
    question: "從時間上的壓⼒察覺,最常⾒的原因是什麼？\nWhat is the most common cause of perceived\npressure from time?",
    options: [
      "A. 有太多的⼯作. There are too many tasks.",
      "B. 缺乏技能培訓. A lack of skill training.",
      "C. 缺乏溝通. A lack of communication.",
      "D. ⼯作量未分配. The workload is NOT distributed."
    ],
    answer: "A"
  },
  {
    question: "什麼是正確的說明關於⼯作場所的刺激程度？\nWhat is a correct statement on the level of\nstimulation in the work place?",
    options: [
      "A. 過度刺激造成壓⼒ over stimulation causes stress",
      "B. 中等刺激引起厭煩 mid levels of stimulation cause boredom",
      "C. 過度刺激提供了最好的⼯作成果 over stimulation gives the best work results",
      "D. 中等刺激對個⼈有相當的影響 the level of stimulation has an equal affect on individuals"
    ],
    answer: "A"
  },
  {
    question: "您被賦予去執⾏⼀個⼯作，因為你做了比其它⼈更多的時間. 你最有可能作出錯誤是由於 …\nYou have been given a job to do because you have done it more times than anyone else. You are most likely to make an error due to …",
    options: [
      "A. … 過度刺激. … over stimulation.",
      "B. …未受到刺激. … under stimulation.",
      "C. … 壓⼒增⼤. … increased stress.",
      "D. … ⼯作量過多. … high workload."
    ],
    answer: "B"
  },
  {
    question: "你被賦予去執⾏數個新的⼯作，因為你是⼀個好的⼯作者. 你最有可能作出錯誤由於 ...\nYou have been given several new jobs to do\nbecause you are a good worker. You are most likely to make an error due to …",
    options: [
      "A. … 過度刺激. … over stimulation.",
      "B. …未受到刺激. … under stimulation.",
      "C. … 環境因素. … environmental factors.",
      "D. … 採取走捷徑. … taking short cuts."
    ],
    answer: "A"
  },
  {
    question: "晝夜⽣理節律是什麼？\nWhat are circadian rhythms?",
    options: [
      "A. 需要多少刺激量去做⼯作 the amount of stimulation needed to do a task",
      "B. 腦波頻率變化的原因 the cause of brain wave frequency changes",
      "C. 在⾝體的⾃然時鐘 the natural clock in the body",
      "D. ⼿和眼睛之間的協調 the coordination between hand and eye"
    ],
    answer: "C"
  },
  {
    question: "慢性疲勞的⼀些症狀是什麼？\nWhat are some symptoms of chronic fatigue?",
    options: [
      "A. 增加能源和幸福感 increased energy and sense of well being",
      "B. 刺激不⾜和無聊 under stimulation and boredom",
      "C. 過渡刺激和無聊 over stimulation and boredom",
      "D. 降低體⼒和幸福感 decreased energy and sense of well being"
    ],
    answer: "D"
  },
  {
    question: "你上班前喝三瓶啤酒和您的⾎液中酒精含量是0.8％mil. 在這個層⾯上需要你 …\nYou have three beer before going to work and your\nblood alcohol level is .8 per mil. At this level it takes you ...",
    options: [
      "A. … 10％更長的時間來反應. … 10% longer to react.",
      "B. … 25％更長的時間來反應. … 25% longer to react.",
      "C. … 35％更長的時間來反應. … 35% longer to react.",
      "D. … 50％更長的時間來反應. … 50% longer to react."
    ],
    answer: "D"
  },
  {
    question: "你在凌晨1:00結束飲酒去睡覺與⾎液中酒精含量是1.6 mil. 當你在6:00上午去⼯作，你的⾎液中酒精含量是 …\nYou finished drinking at 1:00 am and went to bed with a blood alcohol level of 1.6 per mil. When you go to work that morning at 6:00 am your blood alcohol level is ...",
    options: [
      "A. … 0.2％mil.",
      "B. … 0.45％mil.",
      "C. … 0.85％mil.",
      "D. … 1.2％mil."
    ],
    answer: "C"
  },
  {
    question: "你的⼩組長給⼈⼀種驚訝的神情，當你告訴他螺紋滑牙在上緊螺桿時. 他的反應是哪⼀種類型 …\nYour team leader gives a surprised look when you tell him you stripped the threads when tightening a bolt. His reaction is a type of ...",
    options: [
      "A. … 知識. … knowledge.",
      "B. ... 溝通. … communication.",
      "C. … ⾃滿. … complacency.",
      "D. … 察覺. … awareness."
    ],
    answer: "B"
  },
  {
    question: "你的上司告訴你約翰⽣病，並要求您來接班⼯作. 你不說什麼,在你的臉上痛苦的樣⼦是⼀個什麼象徵 …\nYour supervisor tells you John called in sick and asks you to work the next shift. You don't say anything. The pained look on your face is a type of ...",
    options: [
      "A. … 反饋. … feedback.",
      "B. … 刺激. … stimulation.",
      "C. … 編碼. … encoding.",
      "D. … 解碼. … decoding."
    ],
    answer: "A"
  },
  {
    question: "你的⼩組領導分配你和傑克在⽔平安定⾯⼯作. 你對傑克很⽣氣但不說什麼. 你如何描述你和上司之間的溝通？\nYour team leader assigns you to work on the horizontal stabilizer trim with Jack. You are angry with jack but don't say anything. How do you describe the communication between you and your supervisor?",
    options: [
      "A. 沒有迴饋的雙向溝通 two way communication with no feedback",
      "B. 有迴饋的單向溝通 one way communication with feedback",
      "C. 沒有迴饋的單向溝通 one way communication with no feedback",
      "D. 有迴饋的雙向溝通 two way communication with feedback"
    ],
    answer: "C"
  },
  {
    question: "什麼是雙向溝通需要去完成的？\nWhat does two way communication need to be complete?",
    options: [
      "A. ⾝體語⾔ body language.",
      "B. 書⾯的⾔論 written words",
      "C. 語調 intonation",
      "D. 迴饋 feedback"
    ],
    answer: "D"
  },
  {
    question: "編碼時溝通思想的⼀個重要因素是什麼？\nWhat is an important factor when encoding ideas for communication?",
    options: [
      "A. 你得到的迴饋 the feedback you are getting",
      "B. 你的清晰發⾔ the clearness of your speech",
      "C. 聽者的認知 the knowledge of the listener",
      "D. 正確的語調 the correct intonation"
    ],
    answer: "C"
  },
  {
    question: "論及⼀個雙向溝通的模式哪些說法是正確的？\nWhat statement is true for a two way communication model?",
    options: [
      "A. 接收⼈的編碼訊息 the receiver encodes the message",
      "B. 發件⼈的編碼訊息 the sender encodes the message",
      "C. 發送者和接收者兩者的編碼訊息 both the sender and receiver encode the message",
      "D. 發送者和接收者兩者的解碼訊息 both the sender and receiver decode the message"
    ],
    answer: "C"
  },
  {
    question: "以下哪些策略是確保良好的填寫⼯作⽇誌和記錄？\n1）按照三C.\n2）要求，如有需要澄清.\n3）考慮寫⼀個安全事宜.\nWhich of the following strategies ensure good\nwriting in log books and records?\n1)Follow the three Cs.\n2)Ask if any clarification is needed.\n3)Consider writing a matter of safety.",
    options: [
      "A. 僅（1）和（2）",
      "B. 僅（2）和（3）",
      "C. 僅（1）和（3）",
      "D. (1), (2) 和 (3)"
    ],
    answer: "C"
  },
  {
    question: "為什麼要填寫⾶機維修⽇誌？\nWhy must you make log book entries for aircraft\nmaintenance?",
    options: [
      "A. 保持⼯作記錄 to keep a record of the work",
      "B. 未來的問題 for future problems",
      "C. 通知機組⼈員 to inform the flight crew",
      "D. 遵循法律 to follow the law"
    ],
    answer: "D"
  },
  {
    question: "什麼是兩個保存完好的⽇誌簿提供的必備東⻄？\nWhat are the two essential things that well kept log\nbooks provide?",
    options: [
      "A. 記錄⽇期和職責 a record of dates and accountability",
      "B. ⾶機的狀況和缺陷的概述 an overview of the airplane condition and defects",
      "C. 安全和符合法律規定 safety and compliance with the law",
      "D. 執⾏⼯作和責任制的記錄 a record of work performed and accountability"
    ],
    answer: "C"
  },
  {
    question: "在⾶航⽇誌中你發現輸入以下信息：2010/Sep/10;燃料電池;約翰 A ·史密斯 A&P689143IA\n什麼說法是正確的針對這個登錄？\nIn the log book you find the following information entered:\n2010/Sep/10; Fuel cell; John A. Smith A&P689143IA\nWhat statement is true for this entry?",
    options: [
      "A. 這個項⽬是可以接受的，因為它給了職責。 This entry is acceptable because it gives accountability.",
      "B. 這個項⽬是不能接受的，因為它需要說做了什麼。 This entry is NOT acceptable because it needs to say what was done.",
      "C. 因為沒有缺陷指出，這個項⽬是可以接受的。 This entry is acceptable because NO defects are noted.",
      "D. 這個項⽬是不能接受的，因為它只有⼀個簽名。 This entry is NOT acceptable because it only has one signature."
    ],
    answer: "B"
  },
  {
    question: "在⾶航⽇誌中你發現輸入以下信息：2011/Nov/13;更換襟翼唧筒O形環;液壓系統;約翰 A ·史密斯 A&P689143IA\n什麼說法是正確的針對這個登錄？\nIn the log book you find the following information entered:\n2011/Nov/13; replaced o-rings flap cylinder; hydraulic system; John A. Smith A&P689143IA\nWhat statement is true for this entry?",
    options: [
      "A. 它遵循3Cs是可以接受的。 It follows the 3 Cs and is acceptable.",
      "B. 它遵循3Cs但是不能接受的。 It follows the 3 Cs but is not acceptable.",
      "C. 它僅遵循3Cs其中的兩項。 It follows ONLY two of the 3 Cs.",
      "D. 它僅遵循3Cs其中的⼀項。 It follows ONLY one of the 3 Cs."
    ],
    answer: "A"
  },
  {
    question: "哪兩個要素在培訓時被使⽤，當⼀位同事給你看如何在泵螺桿上打保險？\nWhat two elements of training are used when a co-worker shows you how to lock wire the bolts of a pump?",
    options: [
      "A. 反思和評價 reflection and assessment",
      "B. 模仿和經驗 imitation and experience",
      "C. 準備和模仿 preparation and imitation",
      "D. 準備和評估 preparation and assessment"
    ],
    answer: "C"
  },
  {
    question: "哪兩個要素在培訓時被使⽤,當⼀位同事告訴您如何檢查你的保險絲？\nWhat two elements of training are used when a co-worker shows you how to check your lock wiring?",
    options: [
      "A. 準備及應⽤ preparation and application",
      "B. 模仿與反思 imitation and reflection",
      "C. 模仿和評估 imitation and assessment",
      "D. 交付和⽰範 delivery and demonstration"
    ],
    answer: "D"
  },
  {
    question: "哪兩個要素在培訓時被使⽤,當您的同事表明給你檢查保險絲的⽅式？\nWhat two elements of training are used when you check your lock-wiring the way your co-worker showed you to?",
    options: [
      "A. 準備和模仿 preparation and imitation",
      "B. ⽰範和模仿 demonstration and imitation",
      "C. 準備和評估 preparation and assessment",
      "D. 交付和⽰範 delivery and demonstration"
    ],
    answer: "B"
  },
  {
    question: "什麼類型的培訓能使⼯作者更好地識別系統狀態？\nWhat type of training will make a worker better at recognizing the state of a system?",
    options: [
      "A. 意識的培養 awareness training",
      "B. 溝通培訓 communication training",
      "C. 技能培訓 hand skill training",
      "D. ⾃信訓練 assertiveness training"
    ],
    answer: "A"
  },
  {
    question: "持續培訓提⾼⼯作者的意識⽬的是什麼？\n1）它有助於預測可能影響其他系統。\n2）它有助於識別系統狀態。\n3）它有助於修改標準⼯作程序。\nWhat is the purpose of improving a worker's awareness with continued training?\n1)It helps with predicting possible affects on other systems.\n2)It helps with recognizing the state of a system.\n3)It helps with modifying standard work procedures.",
    options: [
      "A. 僅（1）和（2） (1) and (2) only",
      "B. 僅（2）和（3） (2) and (3) only",
      "C. 僅（1）和（3） (1) and (3) only",
      "D. (1), (2) 和 (3) (1), (2) and (3)"
    ],
    answer: "B"
  },
  {
    question: "墨菲定律是什麼呢？\nWhat is Murphy's law?",
    options: [
      "A. 五種感官在局限性的規則。 A rule on the limitations of the five senses.",
      "B. ⾃然法則限制的規則。 A rule on physical limitations.",
      "C. 可能性和或然性的規則。 A rule on possibility and probability.",
      "D. ⼈類需要的規則。 A rule on human need."
    ],
    answer: "C"
  },
  {
    question: "墨菲定律的規則是什麼？\nWhat does Murphy's law rule over?",
    options: [
      "A. 動機和努⼒ the motivation and effort",
      "B. 可能的和⼤概的 possible and probable",
      "C. 努⼒和可能的 effort and possible",
      "D. 動機和⼤概的 motivation and possible"
    ],
    answer: "B"
  },
  {
    question: "⾃滿與墨菲定律有何關係？\nHow does complacency relate to Murphy's law?",
    options: [
      "A. ⾃滿是從墨菲定律引起的。 Complacency is caused from Murphy's law.",
      "B. ⾃滿降低了墨菲定律的規則。 Complacency decreases the rule of Murphy's Law.",
      "C. ⾃滿增加了墨菲定律的規則。 Complacency increases the rule of Murphy's law.",
      "D. ⾃滿跟墨菲定律⼀樣。 Complacency is the same as Murphy's law."
    ],
    answer: "C"
  },
  {
    question: "⾃滿與墨菲定律有何關係？\nHow does complacency relate to Murphy's law?",
    options: [
      "A. 墨菲定律的規則是在⼀個薄弱團隊中⼯作。 The rule of Murphy's law works on the weak points of a team.",
      "B. 墨菲定律的規則，降低了團隊的⼯作負荷。 The rule of Murphy's law reduces the work load of a team.",
      "C. 墨菲定律的規則，改善了團隊的溝通。 The rule of Murphy's law improves the communication of a team.",
      "D. 墨菲定律的規則使團隊更有效率。 The rule of Murphy's law makes the team more efficient."
    ],
    answer: "A"
  },
  {
    question: "墨菲定律的規則如何影響分⼼？\nHow does Murphy's law rule the affect of distractions?",
    options: [
      "A. 通過增加分⼼，幫助⼈們提⾼注意⼒。 By increasing distractions and helping people to improve attention.",
      "B. 通過減少分⼼，幫助⼈們提⾼注意⼒。 By decreasing distractions and helping people to improve attention.",
      "C. 經由降低分⼼，引起⼈們失去注意⼒。 By decreasing distractions and causing people to lose attention.",
      "D. 經由增加分⼼，引起⼈們失去注意⼒。 By increasing distractions and causing people to lose attention."
    ],
    answer: "D"
  },
  {
    question: "在⾃滿環境中⼯作，是什麼錯誤原因造成的？\nWhat is a cause of errors due to complacency in the work environment?",
    options: [
      "A. ⾺斯洛的需求層次 Maslow's hierarchy of needs",
      "B. 框架模式 The SHEL Model",
      "C. 墨菲定律 Murphy's law",
      "D. ⽣物鐘 The Circadian clock"
    ],
    answer: "C"
  },
  {
    question: "什麼是周邊視⼒？\nWhat is peripheral vision?",
    options: [
      "A. 有關的焦點視線 sight related to a point of focus",
      "B. 與遠處物體的視線 sight related to distant objects",
      "C. 有關近處物體的視線 sight related to close objects",
      "D. 與側邊有關的視線 sight related to the sides"
    ],
    answer: "D"
  },
  {
    question: "什麼類型的視野讓您開⾞通過隧道不會撞到兩側？\nWhat type of vision allows you to drive through a tunnel without hitting the sides?",
    options: [
      "A. 近視視⼒ myopia vision",
      "B. ⾊盲視覺 achromatopsia vision",
      "C. 周邊視⼒ peripheral vision",
      "D. 盲視⼒ deuteranopia vision"
    ],
    answer: "C"
  },
  {
    question: "什麼改變進入眼睛的光線量？\nWhat changes the amount of light that enters into the eye?",
    options: [
      "A. 閃爍頻率 blink rate",
      "B. 瞳孔的反射 pupillary reflex",
      "C. 兩種感光細胞 rods and cones",
      "D. 視神經 optic nerve"
    ],
    answer: "B"
  },
  {
    question: "由於光線量度減少使瞳孔變 …\nAs the amount of light decreases the pupils become …",
    options: [
      "A. … ⼤且感光細胞變得更加敏感。 … larger and the rods and cones become more sensitive.",
      "B. … ⼩且感光細胞變得更加敏感。 … smaller and the rods and cones become more sensitive.",
      "C. … ⼤且感光細胞變得較不敏感。 … larger and the rods and cones become less sensitive.",
      "D. … ⼩且感光細胞變得較不敏感。 … smaller and the rods and cones become less sensitive."
    ],
    answer: "A"
  },
  {
    question: "由於光線量度增加使瞳孔變 …\nAs the amount of light increases the pupils become …",
    options: [
      "A. … ⼤且感光細胞變得更加敏感。 … larger and the rods and cones become more sensitive.",
      "B. … ⼩且感光細胞變得更加敏感。 … smaller and the rods and cones become more sensitive.",
      "C. … ⼤且感光細胞變得較不敏感。 … larger and the rods and cones become less sensitive.",
      "D. … ⼩且感光細胞變得較不敏感。 … smaller and the rods and cones become less sensitive."
    ],
    answer: "D"
  },
  {
    question: "耳朵的哪⼀部分增加了對⾼頻率聲⾳的⾳量？\nWhat part of the ear increases the volume of high frequency sounds?",
    options: [
      "A. 耳⿎ the ear drum",
      "B. 耳蝸 the cochlea",
      "C. 耳道 the ear canal",
      "D. 耳咽管 the eustachian tube"
    ],
    answer: "C"
  },
  {
    question: "耳朵的哪⼀部分接收和放⼤震動？\nWhich part of the ear receives and amplifies vibrations?",
    options: [
      "A. 外耳 the outer ear",
      "B. 中耳 the middle ear",
      "C. 內耳 the inner ear",
      "D. 耳咽管 the eustachian tube"
    ],
    answer: "B"
  },
  {
    question: "耳朵的哪⼀部分包含聽覺和平衡的器官？\nWhich part of the ear contains the organ for hearing and balance?",
    options: [
      "A. 內耳 the inner ear",
      "B. 中耳 the middle ear",
      "C. 外耳 the outer ear",
      "D. 耳咽管 the eustachian tube"
    ],
    answer: "A"
  },
  {
    question: "下列哪⼀項是耳朵導致的頭暈和頭昏眼花的狀況？\nWhich of the following is a condition of the ear that causes head spin and dizziness?",
    options: [
      "A. 暈眩 vertigo",
      "B. 耳鳴 tinnitus",
      "C. 中耳炎 otitis media",
      "D. 外耳炎 otitis externa"
    ],
    answer: "A"
  },
  {
    question: "下列哪⼀項狀況是耳朵雜⾳或聲響在頭部所導致的？\nWhich of the following is a condition of the ear that causes noises or ringing in the head?",
    options: [
      "A. 眩暈 vertigo",
      "B. 外耳炎 otitis externa",
      "C. 中耳炎 otitis media",
      "D. 耳鳴 tinnitus"
    ],
    answer: "D"
  },
  {
    question: "積極傾聽過程的正確順序是甚麼？\nWhat is the correct order for the active listening process?",
    options: [
      "A. 理解，解釋和評估 understand, interpret and evaluate",
      "B. 解釋，理解和評估 interpret, understanding and evaluate",
      "C. 解釋，評估和理解 interpret, evaluate and understanding",
      "D. 理解，評估和解釋 understanding, evaluate and interpret"
    ],
    answer: "A"
  },
  {
    question: "群體決策四個階段的正確順序是甚麼？\n1.出現 (emergence)\n2.強化 (reinforcement)\n3.衝突 (conflict)\n4.定向 (orientation)\nWhat is the correct order for the four stages of group decision making?",
    options: [
      "A. 4, 2, 3, 1",
      "B. 4, 3, 1, 2",
      "C. 4, 1, 2, 3",
      "D. 4, 2, 1, 3"
    ],
    answer: "B"
  },
  {
    question: "決策過程的第⼀步是輸入，最後⼀個階段是⾏動和反饋。三個階段之間的正確順序是什麼？\n1）察覺 2）決定 3）注意\nThe first step of the decision making process is the input and the last stage is action and feedback. What is the correct ordering of the three stages between?\n1) awareness 2) decision 3) attention",
    options: [
      "A. 2, 3, 1",
      "B. 1, 3, 2",
      "C. 3, 1, 2",
      "D. 3, 2, 1"
    ],
    answer: "C"
  },
  {
    question: "您會注意到⼀個引擎的起火信號當發動機處於慢⾞狀態。什麼階段是在你的決策過程中？\nYou notice an engine fire signal when the engine is idle. What stage of the decision process are you in?",
    options: [
      "A. 輸入 input",
      "B. 注意 attention",
      "C. 察覺 awareness",
      "D. 決定 decision"
    ],
    answer: "B"
  },
  {
    question: "您會注意到⼀個引擎的起火信號，當發動機處於慢⾞狀態並思考造成的原因。什麼階段是在你的決策過程中？\nYou notice an engine fire signal when the engine is idle and think about the cause. What stage of the decision process are you in?",
    options: [
      "A. 輸入 input",
      "B. 注意 attention",
      "C. 察覺 awareness",
      "D. 決定 decision"
    ],
    answer: "C"
  },
  {
    question: "維修及檢驗⼈員不依照建立的程序與⽅法，是為？\nMaintenance and inspection personnel not following established procedures is classified as?",
    options: [
      "A. ⼈為錯誤 Human error",
      "B. 潛在錯誤 Latent error",
      "C. 監督錯誤 Supervisory error",
      "D. 主動錯誤 Active error"
    ],
    answer: "A"
  },
  {
    question: "非同步的溝通包括？\nAsynchronous communication includes?",
    options: [
      "A. ⾯對⾯ Face-to-face",
      "B. 無線電即時語⾳ Radio real-time voice",
      "C. 技術⼿冊、備忘錄、諮詢通告 Technical manuals, memos, advisory circulars",
      "D. ⼯作後報告 Post-job briefing"
    ],
    answer: "C"
  },
  {
    question: "慢波睡眠？\nSlow-wave sleep corresponds to?",
    options: [
      "A. 1–2 階段 Stage 1–2",
      "B. 2–4 階段 Stage 2–4",
      "C. 反常睡眠 Paradoxical sleep",
      "D. 快速眼動 REM sleep"
    ],
    answer: "B"
  },
  {
    question: "在燃油箱的⼯作中感到恐慌症發作，該怎麼做？\nYou are working in a fuel cell and feel a panic attack starting. What should you do?",
    options: [
      "A. 告訴同事 Tell your co-workers",
      "B. 數到⼆⼗ Count to twenty",
      "C. 專注在⼯作 Focus on your work",
      "D. 深呼吸 Take a deep breath"
    ],
    answer: "A"
  },
  {
    question: "瞳孔變⼩…\nPupils become smaller…",
    options: [
      "A. 在漸增的光照情況下 with increasing light",
      "B. 在集中視網膜中央窩 at the fovea",
      "C. 以集中視柱細胞 due to cone concentration",
      "D. 在漸低的光照情況下 with decreasing light"
    ],
    answer: "A"
  },
  {
    question: "眼睛如何調節進光量？\nHow does the eye regulate the amount of incoming light?",
    options: [
      "A. 視神經 Optic nerve",
      "B. 瞳孔縮放 Pupillary reflex",
      "C. 感光細胞 Rods and cones",
      "D. 眨眼速率 Blink rate"
    ],
    answer: "B"
  },
  {
    question: "何者不是儀錶板優先提供的基本資訊？\nWhich is NOT a primary instrument/basic flight info?",
    options: [
      "A. 航向 Heading",
      "B. 攻⾓ Angle of attack",
      "C. 姿態 Attitude",
      "D. 速度 Airspeed"
    ],
    answer: "B"
  },
  {
    question: "當計劃⼀項任務時，督導⼈必須做什麼？\nWhen planning a task, what must a supervisor do?",
    options: [
      "A. 增加成員間同儕壓⼒ Increase peer pressure",
      "B. 考慮需要的施⼯⽅法和⼯具 Consider required methods and tools",
      "C. 在任務的全部資料上簽名 Sign all task documents",
      "D. 單獨集中於⼀項⼯作 Focus only on a single specific job"
    ],
    answer: "B"
  },
  {
    question: "⼀個正常運作的團隊要如何相亙⽀持？\nHow should a well-functioning team support each other?",
    options: [
      "A. 做⼀樣的⼯作量 Do the same workload",
      "B. 找到團隊成員的缺點 Find team members’ faults",
      "C. 在弱點上⼯作 Work on weaknesses",
      "D. 提⾼⾃⼰的能⼒ Improve one’s own capability"
    ],
    answer: "D"
  },
  {
    question: "什麼類型的照明提供最好的⾊覺？\nWhich lighting gives the best color rendering?",
    options: [
      "A. ⽔銀燈 Mercury lamp",
      "B. ⿄素燈 (Sodium/other) lamp",
      "C. ⽩熱燈 Incandescent",
      "D. 螢光燈 Fluorescent"
    ],
    answer: "D"
  },
  {
    question: "有⼀場發動機火災，你試圖記得可能的原因，在訊息決策程序裡你在那裡？\nThere is an engine fire; you try to recall possible causes. Where are you in the information/decision process?",
    options: [
      "A. 注意 Attention",
      "B. 輸入 Input",
      "C. 決定 Decision",
      "D. 回饋 Feedback"
    ],
    answer: "D"
  },
  {
    question: "哪種模型顯⽰⼀項複雜的任務會增加錯誤的機會?\nWhich model shows that complex tasks increase the chance of error?",
    options: [
      "A. 瑞⼠起司模型 Swiss Cheese model",
      "B. 錯誤冰⼭ Error Iceberg",
      "C. 螺⺟與螺栓拆裝 Nuts and Bolts",
      "D. Dirty Dozen"
    ],
    answer: "C"
  },
  {
    question: "⼯作前，書⾯指導的重要性是甚麼?\nWhat is the importance of written instructions before work?",
    options: [
      "A. 提供良好⼼理與⽣理互動 Provides good psycho-physiological interaction",
      "B. 減少疲勞和壓⼒ Reduces fatigue and stress",
      "C. 可免除對執⾏⼯作的疑慮 Removes doubts about performing the job",
      "D. 消除同事間的溝通需求 Eliminates the need for coworker communication"
    ],
    answer: "C"
  },
  {
    question: "航空組織⼯作的負責⼈指誰?\nWho is responsible for a work task in an aviation organization?",
    options: [
      "A. 安全經理 Safety manager",
      "B. 品管經理 Quality manager",
      "C. ⼩組/團隊領導 Team/Group leader",
      "D. 公司負責⼈ Accountable executive"
    ],
    answer: "C"
  },
  {
    question: "決定⼈際溝通的品質與有效性的因素是？\nWhich factor determines the quality and effectiveness of interpersonal communication?",
    options: [
      "A. 簡潔度 Conciseness",
      "B. 完整性 Completeness",
      "C. 清晰度 Clarity",
      "D. 可理解性 Comprehensibility"
    ],
    answer: "B"
  },
  {
    question: "壓⼒是⼀個正常的⽣活和健康的⼀部分是屬於…\nStress that is a normal and healthy part of life is…",
    options: [
      "A. …正⾯的 Positive",
      "B. …負⾯的 Negative",
      "C. …累積的 Cumulative",
      "D. …中性的 Neutral"
    ],
    answer: "A"
  },
  {
    question: "你被賦予去執⾏數個新的⼯作，因為你是⼀個好的⼯作者，你最有可能犯錯由於…\nYou’re given several new jobs because you’re a good worker. You’re most likely to err due to…",
    options: [
      "A. …採取走捷徑 Taking shortcuts",
      "B. …過度刺激 Overstimulation",
      "C. …環境因素 Environmental factors",
      "D. …未受到刺激 Understimulation"
    ],
    answer: "B"
  },
  {
    question: "⼀個好的團隊是每個成員都有…\nA good team is one where each member has…",
    options: [
      "A. 投入 Involvement/engagement",
      "B. 產出 Output",
      "C. 意⾒ Opinions",
      "D. ⼯作 Jobs"
    ],
    answer: "A"
  },
  {
    question: "近視須以何種鏡片加以矯正？\nMyopia is corrected with which lens?",
    options: [
      "A. 凹透鏡 Concave lens",
      "B. 雙光眼鏡 Bifocals",
      "C. 凸透鏡 Convex lens",
      "D. 平⾯鏡片 Plano lens"
    ],
    answer: "A"
  },
  {
    question: "⼯程師檢查安定⾯的配平插孔螺絲沒有看到⼀斷裂導線，這是何種失誤？\nOn inspection of the stabilizer trim jack screw the engineer does not see a broken hanging wire. What type of failing?",
    options: [
      "A. 分散注意⼒ Divided attention",
      "B. 集中注意⼒ Focused attention",
      "C. 選擇性注意⼒ Selective attention"
    ],
    answer: "C"
  }, 
  {
    question: "當使⽤⼀個滅火器時妳⼤約可靠近火源多遠距離\napproximately how close should you be to a fire when using an extinguisher?",
    options: [
      "A. 2 to 4 feet",
      "B. 4 to 6 feet",
      "C. 6 to 8 feet"
    ],
    answer: "C"
  },
  {
    question: "⼀個⾃信⼼不強的⼈\na person with low self-esteem is",
    options: [
      "A. 減少可能順從同儕的壓⼒ less likely to conform to peer pressure",
      "B. 增加可能順從同儕的壓⼒ more likely to conform to peer pressure",
      "C. 順應同儕的壓⼒但不影響⾃尊的等級 Conformity to peer pressure is not affected by level of self-esteem"
    ],
    answer: "B"
  },
  {
    question: "眼睛需要時間來適應不同層次的光強度。是⼀種\nthe eye requires time to adjust to varying levels of light intensity because the",
    options: [
      "A. 光化學程序 photochemical process",
      "B. 電化學程序 electrochemical process",
      "C. 神經傳導程序 nerve transmit process"
    ],
    answer: "A"
  },
  {
    question: "從SHELL模型的觀點，空間迷向的問題屬於哪⼀個界⾯\nFrom SHELL model, the space disorientation problems belong to which interface",
    options: [
      "A. ⼈-軟體 liveware-software",
      "B. ⼈-環境 liveware-environment",
      "C. ⼈-硬體 liveware-hardware"
    ],
    answer: "B"
  },
  {
    question: "什麼是⼈們對不同的氣候條件的容許限度?\nwhat are the levels of tolerance people have to different climatic conditions?",
    options: [
      "A. 最理想的溫度範圍(⾼⾄低)約10°C the range of optimum temperature (high to low) is about 10°C",
      "B. 最理想的溫度範圍(⾼⾄低)約15°C the range of optimum temperature (high to low) is about 15°C",
      "C. 最理想的溫度範圍(⾼⾄低)約7°C the range of optimum temperature (high to low) is about 7°C"
    ],
    answer: "C"
  },
  {
    question: "實施⼼肺復甦術(氣道、呼吸、循環)胸部按壓是屬於",
    options: [
      "A. 循環急救 circulation first aid",
      "B. 呼吸急救 breathing first aid",
      "C. 氣道和呼吸急救 airway and breathing first aid"
    ],
    answer: "A"
  },
  {
    question: "當指令的格式各不相同，針對⼯作指令有效性的因素何者影響最⼤\nWhat factor of effective work instruction is most affected when instructions use different formats?",
    options: [
      "A. 指令的可達性 accessibility of instruction",
      "B. 指令的⼀致性 consistency of instruction",
      "C. 指令的公信⼒ credibility of instruction"
    ],
    answer: "B"
  },
  {
    question: "哪個模型指⽰錯誤可以因重複檢查及交互檢查⽽停⽌?",
    options: [
      "A. 錯誤冰⼭ Error Iceberg",
      "B. 瑞⼠起司理論 Swiss Cheese Model",
      "C. Dirty Dozen"
    ],
    answer: "B"
  },
  {
    question: "航空器事故涉及⼈為因素問題時，與錯誤鏈的關係如何?",
    options: [
      "A. ⼈為因素問題是第⼀個錯誤鏈的連結",
      "B. ⼈為因素問題是最後⼀個錯誤鏈的連結",
      "C. ⼈為因素問題是所有錯誤鏈的連結"
    ],
    answer: "C"
  },
  {
    question: "最常⾒的⾶機意外事件都可以追溯為\nThe most of aircraft incidents can be traced to",
    options: [
      "A. 技術問題 Technical Problem",
      "B. ⼈為疏失 Human Error",
      "C. 管理失誤 Management Error",
      "D. 製造廠 Manufacture"
    ],
    answer: "B"
  },
  {
    question: "⼀名⼯程師在⼀次⽔平尾翼鉚釘檢查時疏忽了⼀條裂縫。這種過失有可能是什麼原因引起的?\nAn engineer misses a crack during a rivet inspection of the horizontal stabilizer. This failing would most likely be caused by?",
    options: [
      "A. 懼⾼症 Acrophobia",
      "B. 廣場恐懼症 Agoraphobia",
      "C. 幽閉恐懼症 Claustrophobia",
      "D. 恐懼蜘蛛症 Arachnephobia"
    ],
    answer: "A"
  },
  {
    question: "在⼀個強⽽有⼒的安全⽂化組織中，下列何者不是重要的部分？\nWhat is NOT a key component in an organization with a strong safety culture?",
    options: [
      "A. 信息共享 Sharing of information",
      "B. 信任的氣氛 An atmosphere of trust",
      "C. 秘密會議 A hidden agenda",
      "D. 尊重知識 Respect for knowledge"
    ],
    answer: "C"
  },
  {
    question: "噪⾳、照明與溫度，何者與維修⼈為因素有關？",
    options: [
      "A. 噪⾳ Noise",
      "B. 照明 Lighting",
      "C. 溫度 Temperature",
      "D. 皆有關 All of the above"
    ],
    answer: "D"
  },
  {
    question: "⾶機機棚內的燈光應該⾄少\nArea lighting in hangar should be at least",
    options: [
      "A. 能看清⼿冊⽂字並確認裝備位置 Enabling to clearly read manual text and affirm equipment locations.",
      "B. 與正午機坪作業相同 As bright as the lightness at noon on ramp.",
      "C. 無所謂 Doesn't matter",
      "D. 能辨認⾶機外型輪廓 Enabling to recognize airplanes' shapes."
    ],
    answer: "A"
  },
  { "question": "事故和工程故障是。\nAccidents and engineering faults are.", "options": ["A. 微不足道且正在減少。 insignificant and decreasing.", "B. 顯著且不斷增加。 significant and increasing.", "C. 微不足道且正在增加。 insignificant and increasing."], "answer": "B" },
  { "question": "墨菲定律主要由以下因素延續。\nMurphy's law is perpetuated mainly by.", "options": ["A. 違規行為。 violations.", "B. 糟糕的飛機設計。 poor aircraft design.", "C. 自滿。 complacency."], "answer": "C" },
  { "question": "墨菲定律可以被視為下列概念。\nMurphy's law can be regarded as the notion.", "options": ["A. 如果有事可能出錯，就一定會出錯。 'If something can go wrong it will'.", "B. 這永遠不會發生在我身上。 'It can never happen to me'.", "C. 出了問題我一定會被怪罪。 'If something goes wrong I am certain to get the blame'."], "answer": "A" },
  { "question": "公司的安全政策應該被定義於。\nA company's safety policy should be defined in.", "options": ["A. CAP 716。 in CAP 716.", "B. 維修時程表。 the Maintenance Schedule.", "C. 維修組織說明書。 the Maintenance Organization Exposition."], "answer": "C" },
  { "question": "下列何者與人為因素學關聯最小？\nWhich of the following is least associated with the study of human factors?.", "options": ["A. 人體工學。 Ergonomics.", "B. 健康與安全。 Health and Safety.", "C. 人為錯誤。 Human error."], "answer": "B" },
  { "question": "一架 737 兩具發動機皆漏油的事件係直接源於。\nThe incident where a 737 lost oil from both engines is a direct result of.", "options": ["A. 設計不良。 poor design.", "B. 人為錯誤。 human error.", "C. 發動機振動。 engine vibration."], "answer": "B" },
  { "question": "若 737 兩具發動機都做過維修且在飛行中皆喪失機油，這。\nIf a 737 had both engines serviced and lost oil from both engines in flight. This.", "options": ["A. 可因機隊數量而在統計上可預期。 can be expected statistically due to fleet size.", "B. 直接源於人為錯誤。 would be a direct result of human error.", "C. 可視為可接受之機率。 can be considered an acceptable probability."], "answer": "B" },
  { "question": "當有人失溫（低體溫）時你應該。\nWhat do you do when someone is hypothermic?.", "options": ["A. 讓他們保暖。 Warm them up.", "B. 因糖尿病給他們吃甜食。 Feed them sweet things because of their diabetes.", "C. 因脫水給他們喝飲料。 Give them a drink because of dehydration."], "answer": "A" },
  { "question": "由維修與檢查原因所導致事故的比例是。\nThe percentage of accidents attributable to aircraft maintenance and inspection causes is.", "options": ["A. 因更複雜的飛機而較不重要。 now less significant due to more sophisticated aircraft.", "B. 重要且正在上升。 significant and rising.", "C. 因更進步的維修實務而較不重要。 now less significant due to advanced maintenance practices."], "answer": "B" },
  { "question": "1995 年某 737 失去油壓轉降事件的促成因素是。\nWhat happened to contribute towards the incident in 1995 where a Boeing 737 lost oil pressure and had to divert?.", "options": ["A. 警告交叉連接導致兩個指示皆失效。 Both warnings faulty due to crossed connections.", "B. 兩具發動機的高壓轉子驅動蓋在內視鏡檢查後未復裝。 HP rotor drive covers not refitted after borescope.", "C. 內視鏡檢查不充分。 The borescope inspection had been inadequate."], "answer": "B" },
  { "question": "飛行中發動機關車（停車）最常見的原因是。\nWhat is the most common cause of in-flight engine shutdown?.", "options": ["A. 安裝不完整。 Incomplete installation.", "B. 錯誤之隔離/檢查/測試。 Improper fault isolation/inspection/test.", "C. 異物損害。 Foreign object damage."], "answer": "A" },
  { "question": "多數與工程相關的事件係因。\nMost engineering related incidents are due to.", "options": ["A. 安裝髒汙接頭。 installing dirty connectors.", "B. 錯誤安裝零件。 installing components incorrectly.", "C. 安裝磨損或老舊零件。 installing worn or old components."], "answer": "B" },
  { "question": "最多飛機事故的主因是。\nWhat causes the most aircraft accidents?.", "options": ["A. 技術故障。 Technical faults.", "B. 溝通。 Communication.", "C. 進場時管制與飛行員誤解。 Misunderstanding ATC–pilot on approach."], "answer": "B" },

  { "question": "眼睛總聚焦能力的 70–80% 由哪一部分負責？\n70 - 80% of the total focusing ability of the eye is carried out by the.", "options": ["A. 虹膜。 iris.", "B. 角膜。 cornea.", "C. 晶狀體。 lens."], "answer": "B" },
  { "question": "在安靜房間中，無聽力障礙者應可在何距離聽到一般談話聲？\nAt what distance should a person without hearing difficulties hear an average conversational voice in a quiet room.", "options": ["A. 2 公尺（6 呎）。 2 metres (6 feet).", "B. 3 公尺（9 呎）。 3 metres (9 feet).", "C. 1 公尺（3 呎）。 1 metre (3 feet)."], "answer": "A" },
  { "question": "下列何種情況可能導致鼓膜穿孔？\nA perforated ear drum could occur if.", "options": ["A. 暴露於 25 kHz 以上間歇噪音。 intermittent noise above 25 kHz.", "B. 過度擤鼻。 blew your nose excessively.", "C. 長時間暴露於 8 kHz 以下連續噪音。 continuous noise below 8 kHz."], "answer": "C" },
  { "question": "短期記憶記住 7 個項目的時間大約是。\nHow long is the short term memory good for remembering 7 items?.", "options": ["A. 30–60 秒。 30 to 60 seconds.", "B. 最多 30 秒。 Up to 30 seconds.", "C. 超過 60 秒。 Above 60 seconds."], "answer": "B" },
  { "question": "有人在密閉空間（如油箱）作業時，外面的人需隨時通訊以。\nWhen someone is working in an enclosed space, another person should be outside in constant communication to.", "options": ["A. 指導技工。 provide instructions.", "B. 確保遵循維修手冊。 ensure compliance with the manual.", "C. 安全理由。 for safety reasons."], "answer": "C" },
  { "question": "對人體尺寸進行測量之科學稱為。\nThe scientific study of measurements of the human body is known as.", "options": ["A. 人體工學。 ergonomics.", "B. 生理學。 physiology.", "C. 人體測量學。 anthropometrics."], "answer": "C" },
  { "question": "聽覺反射可保護耳朵免受巨響的時間為。\nHow long can the aural reflex protect the ear from loud noise?.", "options": ["A. 5 秒。 5 seconds.", "B. 15 秒。 15 seconds.", "C. 15 分鐘。 15 minutes."], "answer": "C" },
  { "question": "控制入眼光量的部位是。\nWhat part of the eye controls the amount of light entering the eye?.", "options": ["A. 瞳孔。 pupil.", "B. 虹膜。 iris.", "C. 角膜。 cornea."], "answer": "B" },
  { "question": "透過反覆練習形成例行作業的學習稱為。\nLearning of a routine by repeated practice is known as.", "options": ["A. 認知學習。 cognitive learning.", "B. 動作程式化。 motor programming.", "C. 情節記憶。 episodic memory."], "answer": "B" },
  { "question": "耳朵用來偵測的是。\nThe ear is used to detect.", "options": ["A. 速度。 speed.", "B. 非加速度亦非速度。 neither acceleration nor speed.", "C. 加速度。 acceleration."], "answer": "C" },
  { "question": "光線進入眼睛是經由。\nLight enters the eye through the.", "options": ["A. 角膜。 cornea.", "B. 視覺皮質。 visual cortex.", "C. 視網膜。 retina."], "answer": "A" },
  { "question": "為聚焦近物，晶狀體必須。\nTo focus on a near object, the lens of the eye must.", "options": ["A. 變寬。 be widened.", "B. 變扁。 be flattened.", "C. 變厚。 be thickened."], "answer": "C" },
  { "question": "最易受外界影響干擾的記憶類型是。\nWhich type of memory is most susceptible to interference from external influences?.", "options": ["A. 長期記憶。 Long term.", "B. 極短期記憶。 Ultra short term.", "C. 短期記憶。 Short term."], "answer": "C" },
  { "question": "周邊視覺主要由何者偵測？\nPeripheral vision is detected by the.", "options": ["A. 錐狀細胞。 cones.", "B. 黃斑中央凹。 fovea.", "C. 桿狀細胞。 rods."], "answer": "C" },
  { "question": "維修工程師在狹小空間作業所產生的極度不適稱為。\nExtreme discomfort due to working in a confined space is known as.", "options": ["A. 幽閉恐懼症。 claustrophobia.", "B. 懼高症。 acrophobia.", "C. 廣場恐懼症。 agoraphobia."], "answer": "A" },
  { "question": "對顏色敏感的視覺受器為。\nWhat part of the eye is colour sensitive?.", "options": ["A. 桿狀細胞。 rods.", "B. 錐狀細胞。 cones.", "C. 虹膜。 iris."], "answer": "B" },
  { "question": "矯正近視所用的鏡片為。\nWhat type of lens is used to overcome short sightedness?.", "options": ["A. 凹透鏡。 Concave.", "B. 雙焦點。 Bi-focal.", "C. 凸透鏡。 Convex."], "answer": "A" },
  { "question": "最容易被「預期應該發生的事」所影響的記憶是。\nThe type of memory most influenced by expectations is the.", "options": ["A. 長期記憶。 long term memory.", "B. 語義記憶。 semantic memory.", "C. 情節記憶。 episodic memory."], "answer": "C" },
  { "question": "眼睛調節能力不足稱為。\nThe inability for the eyes to accommodate sufficiently is known as.", "options": ["A. 老花眼。 Presbyopia.", "B. 遠視。 Hypermetropia.", "C. 近視。 myopia."], "answer": "A" },
  { "question": "配戴眼鏡/隱形眼鏡之維修工程師應。\nAn aircraft maintenance engineer who wears glasses or contact lenses should.", "options": ["A. 只要全程佩戴即可不需限制職務。 no restriction if worn at all times.", "B. 應限制其職務。 have duties restricted.", "C. 經常檢查鏡片適當性則不需限制。 no restriction with frequent adequacy checks."], "answer": "C" },
  { "question": "極短期記憶（聽覺回音）持續約。\nUltra short term memory has a duration of about.", "options": ["A. 10–20 秒。 10 to 20 seconds.", "B. 80–100 毫秒。 80 - 100 milliseconds.", "C. 2 秒。 2 seconds."], "answer": "C" },
  { "question": "矯正遠視所用的鏡片為。\nWhat type of lens is used to correct long sightedness?.", "options": ["A. 凹透鏡。 Concave.", "B. 凸透鏡。 Convex.", "C. 雙焦點。 Bi-focal."], "answer": "B" },
  { "question": "視敏度定義為。\nVisual Acuity is the ability.", "options": ["A. 區分不同顏色。 to differentiate colours.", "B. 偵測周邊視野物體。 to detect peripheral objects.", "C. 在不同距離辨識銳利細節。 to discriminate sharp detail at varying distances."], "answer": "C" },
  { "question": "「工作記憶」是。\nThe 'working memory' is.", "options": ["A. 長期記憶。 long term memory.", "B. 短期記憶。 short term memory.", "C. 極短期記憶。 ultra short term memory."], "answer": "B" },
  { "question": "色覺缺陷影響的人口比例為。\nColour defective vision affects.", "options": ["A. 約十分之一男性。 almost 1 in 10 men.", "B. 女性多於男性。 more women than men.", "C. 約十分之一女性。 almost 1 in 10 women."], "answer": "A" },
  { "question": "在較低光照下，主要負責視覺的是。\nAt lower light levels, visual sensing is performed mainly by the.", "options": ["A. 中央凹。 fovea.", "B. 錐狀細胞。 cones.", "C. 桿狀細胞。 rods."], "answer": "C" },
  { "question": "若視網膜成像與正常知覺相反轉，觀察者將。\nIf an image on the retina is inverted relative to normal perception, the viewer will.", "options": ["A. 迷失方向且眩暈。 become disoriented and dizzy.", "B. 有意識地心智反轉影像。 consciously mentally revert the image.", "C. 行為與感受皆正常。 behave and feel normal."], "answer": "C" },
  { "question": "色覺缺陷者通常難以區分。\nPeople with colour defective vision usually have difficulty differentiating between.", "options": ["A. 紅與綠。 red and green.", "B. 藍與黃。 blue and yellow.", "C. 藍與綠。 blue and green."], "answer": "A" },
  { "question": "「雞尾酒會效應」描述的是。\nThe 'cocktail party effect' is descriptive of.", "options": ["A. 選擇性注意。 selective attention.", "B. 分散性注意。 divided attention.", "C. 集中性注意。 focused attention."], "answer": "A" },
  { "question": "遠視的醫學名詞是。\nHypermetropia is the medical name for.", "options": ["A. 近視。 short sightedness.", "B. 遠視。 long sightedness.", "C. 失聰。 deafness."], "answer": "B" },
  { "question": "老年性耳聾初期通常先受損的音域為。\nWhat range of sound is usually impaired first with the onset of presbycusis?.", "options": ["A. 高音。 High pitch sound.", "B. 低音。 Low pitch sound.", "C. 中音。 Mid range sound."], "answer": "A" },
  { "question": "進入眼內的光量可變動的倍數約為。\nThe amount of light allowed to enter the eye can vary by a factor of.", "options": ["A. 500:1。 500:1.", "B. 5:1。 5:1.", "C. 1:5。 1:5."], "answer": "B" },
  { "question": "老花常出現在幾歲之後？\nPresbyopia often affects people after the age of.", "options": ["A. 55", "B. 40", "C. 70"], "answer": "B" },
  { "question": "聽力通常從幾歲開始下降？\nFrom what age does hearing ability normally begin to decline?.", "options": ["A. 40", "B. 50", "C. 30"], "answer": "C" },
  { "question": "視力 20/40 的人相較 20/20 者。\nA person with 20/40 vision has.", "options": ["A. 視力較差。 worse eyesight than 20/20.", "B. 視力較好。 better eyesight than 20/20.", "C. 視力相同。 the same eyesight as 20/20."], "answer": "A" },
  { "question": "長期記憶容量通常是。\nLong term memory capacity is usually.", "options": ["A. 幾乎無上限。 unlimited.", "B. 4–8 年。 4 - 8 years.", "C. 12 個月。 12 months."], "answer": "A" },
  { "question": "眼睛無法充分調節稱為。\nThe inability for the eyes to accommodate sufficiently is known as.", "options": ["A. 近視。 myopia.", "B. 遠視。 hypermetropia.", "C. 老花眼。 presbyopia."], "answer": "C" },
  { "question": "極短期記憶（視覺圖像/回音）持續約。\nUltra short term memory has a duration of about.", "options": ["A. 10–20 秒。 10 to 20 seconds.", "B. 2 秒。 2 seconds.", "C. 80–100 毫秒。 80 - 100 milliseconds."], "answer": "B" },
  { "question": "記憶可透過下列方式輔助。\nThe memory can be aided by.", "options": ["A. 檢查清單。 a checklist.", "B. 記憶校核。 memory checking.", "C. 心智記錄。 mind logging."], "answer": "A" },
  { "question": "AWN 47 建議的聽力測試為。\nIn AWN 47 what is the recommended hearing test?.", "options": ["A. 10 呎距離聽到一般談話聲。 hear average voice at 10 ft.", "B. 8 呎處聽到特定噪音。 hear a certain noise at 8 ft.", "C. 6 呎距離聽到一般談話聲。 hear average voice at 6 ft."], "answer": "C" },
  { "question": "圖像式（iconic）記憶。\nIconic memory.", "options": ["A. 儲存聲音可達 2 秒。 stores sounds up to 2 s.", "B. 儲存視覺約 1/2 秒。 stores visual info up to 1/2 s.", "C. 儲存視覺可達 2 秒。 stores visual info up to 2 s."], "answer": "B" },
  { "question": "資訊處理的第一階段是。\nThe first stage in information processing is.", "options": ["A. 決策。 decision.", "B. 記憶。 memorizing.", "C. 知覺。 perception."], "answer": "C" },
  { "question": "若不複誦，資訊會在何時自短期記憶流失？\nInformation, if not rehearsed, is lost in.", "options": ["A. 10–20 秒。 10 - 20 seconds.", "B. 1 分鐘。 1 minute.", "C. 30–40 秒。 30 - 40 seconds."], "answer": "A" },
  { "question": "AWN 47 規定的標準聽力測試為。\nIn AWN 47, what is the standard hearing test?.", "options": ["A. 在安靜房 2 公尺處能聽到對話。 hear conversation at 2 m quiet room.", "B. 在安靜房 10 公尺處能聽到對話。 hear conversation at 10 m.", "C. 在嘈雜房 2 公尺處能聽到對話。 hear conversation at 2 m noisy room."], "answer": "A" },
  { "question": "未複誦之短期記憶會在多久內流失？\nInformation in the short term memory not rehearsed will be lost in.", "options": ["A. 10–20 秒。 10 - 20 seconds.", "B. 1–3 個月。 1 - 3 months.", "C. 2–3 週。 2 - 3 weeks."], "answer": "A" },
  { "question": "CAA 的視力標準為。\nWhat is the CAA standard for vision?.", "options": ["A. 可接受之未矯正視力。 Acceptable uncorrected vision.", "B. 可接受之矯正後視力。 Acceptable corrected vision.", "C. 18/20 視力。 18/20 vision."], "answer": "B" },
  { "question": "使影像聚焦到視網膜所需的大部分折射由何者完成？\nIn the human eye most refraction to focus on the retina is accomplished by the.", "options": ["A. 晶狀體。 lens.", "B. 角膜。 cornea.", "C. （無）"], "answer": "B" },
  { "question": "工作記憶的平均容量約為。\nThe average capacity of the working memory is about.", "options": ["A. 7 個組塊。 7 chunks of information.", "B. 4 個組塊。 4 chunks of information.", "C. 12 個組塊。 12 chunks of information."], "answer": "A" },
  { "question": "視網膜位於。\nThe retina is situated.", "options": ["A. 角膜後與晶狀體一起。 behind the cornea with the lens.", "B. 角膜前方。 in front of the cornea.", "C. 眼後部連接視神經。 at the back of the eye with the optic nerve."], "answer": "C" },
  { "question": "運動程序是指。\nMotor programme refers to.", "options": ["A. 勵志計算機軟件。 motivational computer software.", "B. 一項已經執行多次以至於自動完成的任務。 a task that has been carried out so many times that it becomes automatic.", "C. 一項被編程到短期記憶中的任務。 a task that becomes programmed into short term memory."], "answer": "B" },
  { "question": "哪種記憶會受到個人對「應該發生」之事的期望影響？\nMemory which can be influenced by a person's expectations of what should have happened is.", "options": ["A. 迴聲記憶。 echoic.", "B. 語義記憶。 semantic.", "C. 情節記憶。 episodic."], "answer": "C" },
  { "question": "關於長期記憶，下列敘述何者正確？\nInformation in the long term memory.", "options": ["A. 很容易轉移到短期記憶。 is easily transferred to the short term memory.", "B. 很容易丟失。 is easily lost.", "C. 只能在催眠下取得。 is only available under hypnosis."], "answer": "B" },
  { "question": "短期記憶可同時儲存多少項目？\nHow many things can be stored in the short term memory?", "options": ["A. 0–5。 0 - 5.", "B. 9–15。 9 - 15.", "C. 無上限。 No limit."], "answer": "B" },
  { "question": "視錐細胞主要用於。\nIn the eye, the cones are used mainly in.", "options": ["A. 明亮光線下提供精細細節。 bright light to give fine detail.", "B. 明亮光線下但色覺較差。 bright light levels and they give poor colour vision.", "C. 昏暗光線下且色覺較差。 low light levels and they give poor colour vision."], "answer": "A" },
  { "question": "患有老花眼的人通常會。\nA person suffering from presbyopia would normally.", "options": ["A. 閱讀或近距工作時配戴眼鏡。 wear spectacles when reading or doing close work.", "B. 色覺缺陷而不得進行線束維修。 have defective colour vision and not be allowed to work on looms.", "C. 近視需配戴眼鏡看 30 公分外物體。 be short sighted and need spectacles beyond 30 cm."], "answer": "A" },
  { "question": "噪聲訊號經由何者傳至大腦？\nNoise signals are carried to the brain by the.", "options": ["A. 感覺神經。 sensory nerve.", "B. 聽神經。 auditory nerve.", "C. 咽鼓神經。 Eustachian nerve."], "answer": "B" },
  { "question": "避免將尖銳物插入耳朵，以免導致。\nPoking sharp objects into the ear should be avoided as it is likely to result in.", "options": ["A. 耳鳴。 tinnitus ringing.", "B. 傳導性聽力損失。 conductive hearing loss.", "C. 鼓膜穿孔。 tympanic membrane perforation."], "answer": "C" },
  { "question": "「注意力吸引物」的設計目的在於。\nAttention Getters are designed to.", "options": ["A. 取得注意同時讓操作者持續作業。 gain attention while allowing task continuation.", "B. 使操作者完全聚焦於眼前任務。 make the operator fully focus on the task.", "C. 取得操作者的全神貫注。 get the operator's full attention."], "answer": "C" },
  { "question": "人耳可聽的最高頻率約為。\nAt what maximum frequency does the human ear hear?", "options": ["A. 16 kHz.", "B. 8 kHz.", "C. 20 kHz."], "answer": "C" },
  { "question": "運動程式（Motor programmes）。\nMotor programmes.", "options": ["A. 是行為子程序。 are behaviour subroutines.", "B. 需要有意識思考才能啟動。 require conscious thought to engage.", "C. 以工作規則形式儲存在長期記憶。 are stored as working rules in long term memory."], "answer": "C" },
  { "question": "在何種情況下瞳孔會變小？\nThe pupil of the eye grows smaller.", "options": ["A. 光線減少時。 in condition of reduced light.", "B. 為了聚焦中央凹。 to focus the fovea.", "C. 光線增加時。 in condition of increased light."], "answer": "C" },
  { "question": "傳導性耳聾可能由何部位受損引起？\nConductive deafness can be caused by damage to the.", "options": ["A. 耳蝸。 cochlea.", "B. 耳石。 otoliths.", "C. 半規管。 semi circular canals."], "answer": "A" },
  { "question": "細節最佳由____感知；運動最佳由____感知。\nDetail is best sensed by the ______ and movement best sensed by the ______.", "options": ["A. 周邊；周邊。 the periphery; the periphery.", "B. 周邊；中央凹。 the periphery; fovea.", "C. 中央凹；周邊。 the fovea; periphery."], "answer": "C" },
  { "question": "色盲者最難區分的顏色為。\nIf a person is colour blind, which colours would be most difficult to see?", "options": ["A. 紅與綠。 Red and green.", "B. 藍與紅。 Blue and red.", "C. 黃與紅。 Yellow and red."], "answer": "A" },
  { "question": "近視是______，需用______鏡矯正。\nMyopia is _______ and a ______ lens is needed to correct it.", "options": ["A. 遠視；凹透鏡。 long sightedness; concave.", "B. 近視；凸透鏡。 short sightedness; convex.", "C. 近視；凹透鏡。 short sightedness; concave."], "answer": "C" },
  { "question": "耳石感測的是。\nThe Otoliths detect.", "options": ["A. 角加速度。 angular acceleration.", "B. 線性加速度。 linear acceleration.", "C. 角與線性加速度皆是。 both angular and linear acceleration."], "answer": "B" },
  { "question": "鼻子的功能為。\nThe nose.", "options": ["A. 過濾空氣進入肺部。 filters the air into the lungs.", "B. 過濾、加溫並加濕空氣進入肺部。 filters, warms and moistens the air into the lungs.", "C. 過濾空氣進入肺部。 filters the air into the lungs."], "answer": "B" },
  { "question": "近視最常見的原因是。\nThe most common cause of myopia is.", "options": ["A. 調節力弱。 weak accommodation.", "B. 眼球縮短。 a shortened eyeball.", "C. 眼球拉長。 an elongated eyeball."], "answer": "C" },

  { "question": "什麼是同儕壓力？\nWhat is peer group pressure?", "options": ["A. 上議院對下議院的影響。 influence of House of Lords over Commons.", "B. 朋友同事對我們行為的影響。 behaviour influenced by friends and colleagues.", "C. 個人對群體的影響力。 influence an individual has over a group."], "answer": "B" },
  { "question": "個人的常規行為稱為。\nA regular behaviour of an individual is known as.", "options": ["A. 常態。 the norm.", "B. 習慣。 habit.", "C. 文化。 culture."], "answer": "B" },
  { "question": "討論中最可能被同意的人是。\nIn a discussion, the person who is most likely to be agreed with is.", "options": ["A. 最常重複論點者。 the person who repeats the point most.", "B. 最愛爭論者。 the most argumentative person.", "C. 地位最高者。 the person with the highest status."], "answer": "C" },
  { "question": "自行發明作業方式的工程師。\nAn engineer who has developed his own way of performing a task.", "options": ["A. 屬經常違規。 is in regular violation.", "B. 提升維修效率。 is improving maintenance efficiency.", "C. 應讚揚其機智。 should be commended for resourcefulness."], "answer": "A" },
  { "question": "組織內人因計畫之目標是。\nThe aim of human factors programs within an organization is.", "options": ["A. 以降低工安事故保障人員安全。 safeguard health and safety by reducing accidents.", "B. 最佳化人員與系統之關係以提升安全效率福祉。 optimize relationship between personnel and systems to improve safety, efficiency, well-being.", "C. 以提效增安減錯降本。 reduce costs by increasing efficiency, safety, quality and decreasing error waste."], "answer": "B" },
  { "question": "具有「責任」的飛機工程師是指。\nAn aircraft engineer who has 'responsibility'.", "options": ["A. 必須具該機型執照。 must be licensed on that type.", "B. 對所管事務需負責可被追究。 liable to be called to account; in charge or answerable.", "C. 公司的管理職。 is in a management position."], "answer": "B" },
  { "question": "人為因素與人為錯誤的影響最重要於。\nThe impact of human factors and human error is most important to.", "options": ["A. 技師與工程師。 technicians and engineers.", "B. 規劃與管理者。 planners and managers.", "C. 對上述各角色同樣重要。 equally important to technicians, engineers, planners and managers."], "answer": "C" },
  { "question": "持照工程師的職責訂於何處？\nWhere are the responsibilities of Licensed Aircraft Engineers laid down?", "options": ["A. AWN 3.", "B. 空中航行令。 The Air Navigation Order.", "C. CAP 715."], "answer": "A" },
  { "question": "責任分散可能發生於。\nDiffusion of responsibility may occur.", "options": ["A. 作為團隊一員工作時。 to an individual working as a team member.", "B. 特定人，不論單獨或團隊。 with certain people whether in a team or alone.", "C. 獨自工作的人。 to an individual working alone."], "answer": "A" },
  { "question": "「風險轉移（risky shift）」是指。\n'Risky shift' is.", "options": ["A. 被分派含風險任務的機率。 probability of being assigned risky tasks.", "B. 輪班交接不充分之名。 name for inadequate shift handover.", "C. 團體傾向作出比個人更冒險的決策。 tendency for a group to choose a riskier course than any individual would."], "answer": "C" },
  { "question": "為維持機型現況能力，技師需。\nTo ensure a technician remains current on authorized aircraft types, they are required that.", "options": ["A. 只需適當繼訓/複訓。 appropriate continuation/refresher training only.", "B. 任一 2 年內至少 6 個月實作經驗。 at least 6 months actual maintenance in any 2-year period only.", "C. 任一 2 年內至少 6 個月實作並具適當繼訓/複訓。 at least 6 months actual maintenance in any 2 years and appropriate continuation/refresher training."], "answer": "C" },
  { "question": "一個人「能做」與「會做」的差異主要取決於其。\nThe difference between what a person 'can' do and what he 'will' do is largely determined by his.", "options": ["A. 動機。 motivation.", "B. 教育與訓練。 education and training.", "C. 身心健康。 physical and mental health."], "answer": "A" },
  { "question": "工程師就新技術與程序保持最新的責任在於。\nWhose responsibility is it that an engineer remains current on new technology and procedures?", "options": ["A. 組織。 The organization's.", "B. CAA。 The CAA's.", "C. 工程師本人。 The engineer's."], "answer": "C" },
  { "question": "依馬斯洛理論，安全需求。\nAccording to Maslow, safety needs.", "options": ["A. 是所有需求滿足後的最後需求。 the last need after others satisfied.", "B. 僅次於生理需求。 second only to physiological needs.", "C. 是人類最原始的需求。 the most primal need."], "answer": "B" },
  { "question": "缺乏動機（去動機）的症狀與哪個相似？\nThe symptoms of de-motivation are very similar to the symptoms of.", "options": ["A. 壓力。 stress.", "B. 疲勞。 tiredness.", "C. 精神疾病。 mental illness."], "answer": "A" },
  { "question": "順應群體讓觀點行為受情境影響的傾向稱為。\nThe desire to 'conform' to a group by allowing one's opinions, attitudes and actions to be affected is known as.", "options": ["A. 同儕壓力。 peer pressure.", "B. 尊重需求。 esteem needs.", "C. 文化議題。 culture issues."], "answer": "A" },
  { "question": "「確認偏差」是指。\n'Confirmation bias' is.", "options": ["A. 主管自檢自簽的作業錯誤。 error by a supervisor who inspected and signed own work.", "B. 由獨立人員進行的檢查。 inspection by an independent inspector/supervisor.", "C. 潛意識偏重支持自身信念的證據、忽視相反證據。 subconscious attention to confirming evidence; inattention to contradictory evidence."], "answer": "C" },
  { "question": "自尊心低的人。\nA person with low self-esteem is.", "options": ["A. 更易受同儕壓力影響。 more likely to conform to peer pressure.", "B. 較不受同儕壓力影響。 less likely to conform.", "C. 與自尊無關。 not affected by self-esteem."], "answer": "A" },
  { "question": "動機是。\nMotivation is.", "options": ["A. 用以減少錯誤的獎懲。 reward or punishment to reduce errors.", "B. 用以提高工作率的獎懲。 reward or punishment to increase work rate.", "C. 驅使人去做某事的內在驅力。 the thing that drives someone to do something."], "answer": "C" },
  { "question": "同儕壓力是指。\nPeer pressure is", "options": ["A. 以同事的方式執行任務之感知壓力。 perceived pressure to do tasks as colleagues would.", "B. 遵從你認為同事對你期望之感知壓力。 perceived pressure to conform to what you believe colleagues expect.", "C. 無。 Nothing."], "answer": "B" },
  { "question": "工程師視力的責任在於。\nThe eyesight of an engineer is the responsibility of.", "options": ["A. 品質經理。 the Quality Manager.", "B. 配鏡師。 the optician.", "C. 工程師本人。 the engineer."], "answer": "C" },
  { "question": "一個好的團隊是每個成員都有。\nA good team is one where every member has.", "options": ["A. 一個意見。 an opinion.", "B. 參與投入。 an input.", "C. 一份工作。 a job."], "answer": "B" },
  { "question": "AWN 47 規定工程師。\nAWN 47 states that the engineer.", "options": ["A. 對健康安全負責。 is responsible for health and safety.", "B. 對自己簽署之工作負責。 is responsible for the work he has signed for.", "C. 若身體不適則不報到上班。 does not report for work if unfit."], "answer": "C" },
  { "question": "有效的小組工作是當。\nAn effective group work is when.", "options": ["A. 每個人都以某種方式貢獻。 everyone contributes in some way.", "B. 每個人都討論想法與意見。 everyone discusses ideas and opinions.", "C. 每個人都有工作做。 everyone has a job to do."], "answer": "A" },
  { "question": "何者定義了同儕壓力情境？\nWhich of the following defines a peer pressure situation?", "options": ["A. 主管催你準時完成任務。 manager pressuring timely completion.", "B. 女友要求你陪她外出。 girlfriend telling you to go out.", "C. 同事催你加快好讓他們回家。 colleagues pressuring you to work faster so they can go home."], "answer": "C" },
  { "question": "成功的工作團隊具備下列何種特質？\nSuccessful working teams have the following attributes:-", "options": ["A. 參與團隊並保有個人要求。 members participate but retain individual requirements.", "B. 全體皆參與活動與討論。 all members participate in activities and discussions.", "C. 各自單獨工作提供高度個別解。 all members work in isolation."], "answer": "A" },
  { "question": "良好的維修監督判斷通常基於。\nGood aircraft maintenance supervisory judgment is usually based upon.", "options": ["A. 知識、經驗與核准資料。 knowledge and experience and reference to approved data.", "B. 現有證據與強勢管理。 evidence available and forceful management ability.", "C. 知識、經驗與課程筆記。 knowledge and experience and reference to course notes."], "answer": "A" },
  { "question": "組織文化（好或壞）最好描述為。\nOrganizational culture (whether good or bad) is best described as.", "options": ["A. 「我們在此處理事的方式」。 'the way we do things around here'.", "B. 書面程序。 written procedures.", "C. 團隊資源管理。 team resource management."], "answer": "A" },
  { "question": "實施人因的組織中，對錯誤的態度是。\nIn an organization which practices human factors there is.", "options": ["A. 對所有違規皆處罰。 punishment for all violations.", "B. 除非故意違規，否則不責備。 no blame unless there is a deliberate violation.", "C. 完全無責備文化。 a no blame culture."], "answer": "B" },
  { "question": "可說一個人有動機，當他/她。\nA person can be said to be motivated if.", "options": ["A. 為求快而偷工減料。 they cut corners to finish quickly.", "B. 領生產力獎金。 they are on a productivity bonus.", "C. 正採取行動以達成目標。 they are taking action to achieve something."], "answer": "C" },
  { "question": "群體兩極化可能導致。\nGroup polarisation can result in.", "options": ["A. 團體做出更謹慎或更極端的決策。 a group making a more cautious or extreme decision.", "B. 團體比個人做出更佳決策。 a group making a better decision than the individual.", "C. 成員彼此不交談。 members of the group not talking to one another."], "answer": "A" },
  { "question": "誰最可能偏離標準程序？\nWho is most likely to deviate from standard procedure?", "options": ["A. 年輕且缺乏經驗者。 Young, inexperienced man.", "B. 過度自信的年輕人。 Over confident, young man.", "C. 年老疲憊者。 Old tired man."], "answer": "B" },
  { "question": "專業飛機工程師的理想行為是。\nThe ideal behaviour of a professional aircraft engineer is.", "options": ["A. 目標導向而非人導向。 goal directed rather than person directed.", "B. 同時兼具人導向與目標導向。 both person and goal directed.", "C. 既非人導向亦非目標導向。 neither person or goal directed."], "answer": "B" },
  {"question":"有關毒品與酒精的資訊可在哪裡找到？ | Information on drugs and alcohol can be found in.","options":["A. BCARs｜BCARs","B. AWN 47｜AWN 47","C. AWN 3｜AWN 3"],"answer":"B"},
  {"question":"醫師剛開新藥時你應該？ | If you have been prescribed new medicine by your doctor you should.","options":["A. 照常上班｜continue with your normal shift pattern.","B. 請3天假試藥｜take 3 days off work to try out the new medication.","C. 先試用24小時｜give the new medication a 24 hour trial."],"answer":"C"},
  {"question":"全身麻醉後你應該？ | After a general anaesthetic you should.","options":["A. 盡快復工｜return to work as soon as possible.","B. 至少休息24–48小時｜not return to work for at least 24 to 48 hours.","C. 至少休息7天｜take at least 7 days off work."],"answer":"B"},
  {"question":"因憂鬱服用鎮靜劑時你應該？ | Tranquillisers for depression: you should.","options":["A. 不告知雇主照常工作｜not tell your employer and carry on work as normal.","B. 告知雇主照常工作｜tell your employer and carry on work as normal.","C. 服藥期間不從事工作｜not work at all when taking the tranquillizers."],"answer":"C"},
  {"question":"工程師使用提神藥丸（pep pills）？ | The use of 'pep' pills by an aircraft engineer.","options":["A. 夜班或加班可用｜recommended when working late or nights.","B. 刺激感官減少事故｜they make you less prone to accidents.","C. 不應使用（咖啡例外）｜should never be done (except coffee)."],"answer":"C"},
  {"question":"服用SUDAFED鼻充血藥時你應該？ | You are taking SUDAFED to relieve nasal congestion. You should.","options":["A. 停工至不需用藥｜stay away from work until no longer required.","B. 可在工作中持續服用｜continue to take them at work.","C. 避免工程決策/簽放職務｜avoid engineering decisions or licensed duties."],"answer":"C"},
  {"question":"何謂慢波睡眠？ | What is slow wave sleep?","options":["A. 矛盾睡眠｜Paradoxical sleep.","B. 第2–4期睡眠｜Stage 2–4 sleep.","C. 快速動眼期｜REM."],"answer":"B"},
  {"question":"第3/4期睡眠 | Phase 3/4 sleep.","options":["A. 可由酒精誘導｜can be induced by alcohol.","B. 每個睡眠週期僅一次｜occurs only once per cycle.","C. 最有助身體恢復｜most beneficial for restoration."],"answer":"C"},
  {"question":"人為錯誤可能由何造成？ | Human error can be caused by.","options":["A. 體溫過高｜high body temperature.","B. 正常體溫｜normal body temperature.","C. 體溫過低｜low body temperature."],"answer":"C"},
  {"question":"長班後建議餐點？ | Meal most recommended after a long shift?","options":["A. 高碳水｜High carbohydrates.","B. 低碳水｜Low carbohydrates.","C. 高蛋白｜High protein."],"answer":"A"},
  {"question":"長時間輪班會？ | Long shift work will.","options":["A. 先降後升能力｜initially decrease then increase ability.","B. 一直降低能力｜always decrease ability.","C. 一直提高能力｜always increase ability."],"answer":"B"},
  {"question":"晝夜節律的體溫變化？ | The circadian cycle body temperature.","options":["A. 不變｜does not vary.","B. 變化1.5°C｜varies by 1.5°C.","C. 變化1.5°F｜varies by 1.5°F."],"answer":"C"},
  {"question":"急性壓力是？ | Acute stress is.","options":["A. 長期強烈壓力｜intense of long duration.","B. 強烈但短暫｜typically intense but short.","C. 頻繁或長期壓力｜frequently recurring/long."],"answer":"B"},
  {"question":"慢性壓力是？ | Chronic stress is.","options":["A. 頻繁或長期壓力｜frequently recurring/long.","B. 強烈但短暫｜intense but short.","C. 長期強烈壓力｜intense long duration."],"answer":"A"},
  {"question":"吸食大麻的影響？ | Smoking cannabis.","options":["A. 微幅損害表現至24小時｜subtly impairs up to 24h.","B. 僅短期影響｜only short term affect.","C. 顯著影響至24小時｜noticeable up to 24h."],"answer":"A"},
  {"question":"績效與喚醒關係？ | Performance is.","options":["A. 與喚醒成反比｜inversely proportional to arousal.","B. 與喚醒成正比｜directly proportional.","C. 只有單一最佳點最大｜only one optimum peak."],"answer":"A"},
  {"question":"為趕進度而不休息？ | Missing a break to meet timeframe.","options":["A. 只要主管休息即可｜ok if supervisors break.","B. 可能適得其反（疲勞）｜can be counterproductive (fatigue).","C. 末班補足休息即可｜ok if rest at shift end."],"answer":"B"},
  {"question":"疲勞對視力敏銳度？ | Tiredness causes visual acuity to.","options":["A. 降低｜decrease.","B. 不受影響｜not affected.","C. 提高｜increase."],"answer":"A"},
  {"question":"注意力縮窄發生於？ | Narrowing of attention occurs at.","options":["A. 低喚醒｜low arousal.","B. 高低皆是｜both high and low.","C. 高喚醒｜high arousal."],"answer":"C"},
  {"question":"血液酒精限值？ | Blood/alcohol limit is.","options":["A. 機組/管制20mg/100ml；維修80mg/100ml｜20mg for aircrew/ATC; 80mg for maintenance.","B. 40mg/100ml｜40 mg/100 ml.","C. 全部20mg/100ml｜20 mg for all."],"answer":"A"},
  {"question":"矛盾睡眠別名？ | Paradoxical sleep is also known as.","options":["A. 第3期｜Stage 3 sleep.","B. 第4期｜Stage 4 sleep.","C. 快速動眼睡眠｜REM sleep."],"answer":"C"},
  {"question":"首次用藥時？ | When taking medicine for the first time.","options":["A. 值勤前≥24小時先試一劑｜first dose ≥24h before duty.","B. 用藥期間整段缺勤｜absent for duration.","C. 需執勤再諮詢醫師｜consult doctor if duties."],"answer":"A"},
  {"question":"男性每週建議最大飲酒單位？ | Recommended max alcohol intake (men).","options":["A. 每週3–4單位｜3–4 units/week.","B. 每週28單位｜28 units/week.","C. 每天28單位｜28 units/day."],"answer":"B"},
  {"question":"人類晝夜節律週期？ | Human circadian rhythms cycle on a.","options":["A. 25小時｜25 hours.","B. 8小時｜8 hours.","C. 24小時｜24 hours."],"answer":"A"},
  {"question":"血中酒精代謝可加速嗎？ | Removal of alcohol from bloodstream.","options":["A. 睡覺可加速｜speeded by sleeping.","B. 不能加速｜cannot be speeded up.","C. 濃咖啡可加速｜speeded by strong coffee."],"answer":"B"},
  {"question":"正常晝夜節律下體溫最低時段？ | Lowest body temperature (normal circadian).","options":["A. 凌晨4–6時｜between 4–6 am.","B. 醒來時｜upon waking.","C. 正午｜at midday."],"answer":"A"},
  {"question":"工程師感冒/流感應？ | If a maintenance engineer has a cold/flu he should.","options":["A. 合約有病假再缺勤｜absent only if paid.","B. 無人力缺口才缺勤｜absent only if no shortage.","C. 康復前皆缺勤｜absent until fully recovered."],"answer":"C"},
  {"question":"飲酒對反應時間？ | Consumption of alcohol.","options":["A. 增加反應時間（變慢）｜increases reaction times.","B. 無影響｜no effect.","C. 減少反應時間（變快）｜decreases reaction times."],"answer":"A"},
  {"question":"體溫與警覺表現？ | Alertness/performance is reduced when body temperature is.","options":["A. 高於正常｜above normal.","B. 低於正常｜below normal.","C. 高於或低於正常｜either above or below."],"answer":"B"},
  {"question":"睡眠經驗法則？ | Rule of thumb for adequate sleep.","options":["A. 1小時優質睡=2小時活動｜1h HQ sleep → 2h activity.","B. 2小時優質睡=1小時活動｜2h → 1h.","C. 1小時優質睡=1小時活動｜1h → 1h."],"answer":"A"},
  {"question":"熟悉任務變得困難是何徵兆？ | Familiar tasks feel harder → early sign of.","options":["A. 急性壓力｜acute stress.","B. 慢性疲勞｜chronic fatigue.","C. 感冒或流感｜a cold or flu."],"answer":"B"},
  {"question":"唯一允許的興奮劑？ | The only permitted stimulant is.","options":["A. 溴｜bromine.","B. 咖啡因｜caffeine.","C. 安非他命｜amphetamine."],"answer":"B"},
  {"question":"大量咖啡因可能？ | Large amounts of caffeine can.","options":["A. 引起焦慮/頭痛/壓力｜cause anxiety, headaches, stress.","B. 減少焦慮與壓力｜reduce anxiety and stress.","C. 提升警覺與意識｜improve alertness and awareness."],"answer":"A"},
  {"question":"壓力症狀？ | The symptoms of stress are.","options":["A. 暴力、疾病、曠工、藥酒濫用｜violence, sickness, absence, drug/alcohol abuse.","B. 工作表現變好跡象｜improved performance.","C. 易怒、健忘、疾病、曠工、藥酒濫用｜irritability, forgetfulness, sickness, absence, drug/alcohol abuse."],"answer":"C"},
  {"question":"安眠藥可能？ | Sleeping tablets can.","options":["A. 反應變慢、感官遲鈍｜slow reaction, dull senses.","B. 隔日更警覺｜increase alertness next morning.","C. 幫助REM並校正節律｜help REM & realign rhythms."],"answer":"A"},
  {"question":"員工不適時之認證資訊載於？ | Info for certifying staff when medically unfit is in.","options":["A. AWN 3","B. AWN 47","C. ANO"],"answer":"B"},
  {"question":"飲用3–5單位酒精之影響？ | Effect of 3–5 units of alcohol.","options":["A. 睡眠品質下降｜loss of quality sleep.","B. 低REM睡眠｜low REM sleep.","C. 體溫下降｜drop in body temperature."],"answer":"A"},
  {"question":"長時間輪班的效應？ | Long shift work.","options":["A. 降低缺陷辨識能力｜decreases ability to recognize defects.","B. 提高辨識能力｜increases ability.","C. 無影響｜no effect."],"answer":"A"},
  {"question":"晝夜節律控制？ | Circadian rhythms control.","options":["A. 體溫｜body temperature.","B. 尿量｜urine output.","C. 睡眠型態｜sleeping patterns."],"answer":"A"},
  {"question":"無處方可用的興奮劑？ | Stimulant allowed without prescription is.","options":["A. 溴｜bromine.","B. 咖啡因｜caffeine.","C. 抗組胺藥｜antihistamine."],"answer":"B"},
  {"question":"AWN 47的適用情況？ | Conditions in AWN 47 are applicable to engineers.","options":["A. 簽署完工時｜who sign for work completed.","B. 受酒/藥影響時｜when under influence of drink/drugs.","C. 為工作安全｜for their safety at work."],"answer":"B"},
  {"question":"睡前飲3–4單位酒精會？ | 3–4 units of alcohol before sleep can.","options":["A. 增加REM｜increase REM.","B. 降低睡眠品質｜decrease quality of sleep.","C. 降低體溫｜lower body temperature."],"answer":"B"},
  {"question":"體溫/睡眠需求/警覺之循環稱為？ | Cycles of body temperature, sleep need and alertness are called.","options":["A. 地球循環｜earth cycles.","B. 晝夜節律｜circadian rhythms.","C. 外經循環｜ecto-meridian cycles."],"answer":"B"},
  {"question":"適量咖啡因可造成？ | Moderate caffeine intake can result in.","options":["A. 焦慮、頭痛、負向情緒｜anxiety, headaches, negative mood.","B. 缺眠與節律紊亂｜lack of sleep & circadian disruption.","C. 暫時提升警覺/守望力｜temporary vigilance/alertness boost."],"answer":"C"},
  {"question":"非社交時段過長輪班可導致？ | Excessively long shifts at unsociable hours can lead to.","options":["A. 維修辨識缺陷能力下降｜decreased ability to detect defects.","B. 對壓力更免疫｜increased immunity to stress.","C. 辨識能力增加｜increased ability to detect defects."],"answer":"A"},
  {"question":"理論上人為錯誤最可能發生於？ | In theory, human error most likely occurs.","options":["A. 體溫最低時｜when body temperature lowest.","B. 酷熱天氣｜during very hot weather.","C. 體溫穩定時｜when temperature stable."],"answer":"A"},
  {"question":"壓力下面對可勝任任務時易認為？ | Under stress when facing a within-capability task, one may think it is.","options":["A. 要求過高｜too demanding.","B. 要求不夠｜not demanding enough.","C. 別人的責任｜someone else’s responsibility."],"answer":"C"},
  {"question":"AWN 47未提及？ | AWN 47 does not mention.","options":["A. 提神藥（pep’s）｜pep’s.","B. 速達非德（Sudafed）｜sudafed.","C. 褪黑激素｜melatonin."],"answer":"C"},
  {"question":"睡前飲3–4單位酒精會降低？ | 3–4 units of alcohol before sleep reduces.","options":["A. 兩者皆是｜both.","B. 睡眠量｜quantity of sleep.","C. 睡眠質｜quality of sleep."],"answer":"A"},
  {"question":"睡眠中何者重要？ | Which is important in sleep?","options":["A. 量｜Quantity.","B. 質｜Quality.","C. 兩者｜Both."],"answer":"C"},
  {"question":"噪音與高溫等環境壓力源會？ | Stressors in noise/heat environment will cause.","options":["A. 不會失去注意力｜no loss of attention.","B. 完全失去注意力｜total loss of attention.","C. 注意力下降與分心｜loss of attention and distraction."],"answer":"C"},
  {"question":"從白班到夜班時，效率會如何變化？ | When going from day shift to night shift, efficiency…","options":["A. 保持不變｜stays the same.","B. 前四週後才下降｜will drop off after the first four weeks.","C. 前四週內會下降｜will drop off in the first four weeks."],"answer":"C"},
  {"question":"在飛機上工作時，飲酒的規定？ | When working on aircraft, the consumption of alcohol…","options":["A. 不超標即可｜is permissible if not exceeding drink-drive limit.","B. 大量飲酒 8 小時後仍不可工作｜you cannot work even 8h after large quantities.","C. 少量允許｜a certain amount is permissible."],"answer":"B"},
  {"question":"睡前喝 3–4 單位酒精的結果？ | Drinking 3–4 units of alcohol before sleeping results in…","options":["A. 非REM睡眠流失｜loss of non-REM sleep.","B. 失去優質睡眠｜loss of quality sleep.","C. 體溫下降｜a drop in body temperature."],"answer":"B"},
  {"question":"酒精對睡眠的影響？ | What effect does alcohol have on sleep?","options":["A. 兩者皆減少（量與質）｜Both.","B. 降低睡眠量｜Decreases quantity of sleep.","C. 降低睡眠質｜Decreases quality of sleep."],"answer":"A"},
  {"question":"注意力縮小發生在何種喚醒狀態？ | Narrowing of attention occurs in states of…","options":["A. 最佳喚醒｜optimum arousal.","B. 低喚醒｜low arousal.","C. 高喚醒｜high arousal."],"answer":"C"},
  {"question":"缺氧對視覺的影響？ | Hypoxia can…","options":["A. 因未迅速回暖而昏迷｜cause coma if not warmed up.","B. 降低視桿靈敏度、影響視力｜impair rod sensitivity and eyesight.","C. 改善視錐的夜視力｜improve cones’ night vision."],"answer":"B"},
  {"question":"服用處方藥時應？ | You are taking prescribed drugs.","options":["A. 知道主副作用即可繼續工作｜Carry on working if you know side effects.","B. 不要工作｜Do not work.","C. 只顧工作其他不管｜Work and don’t care about other things."],"answer":"A"},
  {"question":"維修允許的物質？ | Acceptable substance regarding aircraft maintenance.","options":["A. 盤尼西林｜Penicillin.","B. 咖啡因｜Caffeine.","C. β受體阻滯劑｜Beta blockers."],"answer":"B"},
  {"question":"晝夜節律的週期為？ | Circadian Rhythms have a cycle of…","options":["A. 25 小時｜25 Hours.","B. 24 小時｜24 Hours.","C. 23 小時｜23 Hours."],"answer":"A"},
  {"question":"酒精吸收取決於？ | After drinking alcohol, absorption is dependent on…","options":["A. 體重｜weight.","B. 年齡｜age.","C. 時間｜time."],"answer":"C"},
  {"question":"BMI=28 的分類？ | An engineer with BMI 28 would normally be classed as…","options":["A. 健康體重、無風險｜healthy weight, no real risk.","B. 過輕、無風險｜underweight, no real risk.","C. 過重且有風險｜overweight with risk."],"answer":"A"},
  {"question":"4 單位酒精降到 2 單位需多久？ | From four units to two units takes…","options":["A. 4 小時｜four hours.","B. 8 小時｜eight hours.","C. 2 小時｜two hours."],"answer":"C"},
  {"question":"睡眠分幾期？ | How many stages of sleep are there?","options":["A. 5","B. 3","C. 4"],"answer":"A"},
  {"question":"REM 睡眠又稱？ | REM sleep can also be referred to as…","options":["A. 超自然睡眠｜paranormal sleep.","B. 慢波睡眠｜slow wave sleep.","C. 矛盾睡眠｜paradoxical sleep."],"answer":"C"},
  {"question":"對健康有害物的存在屬於何種壓力源？ | Presence of something damaging to health is a…","options":["A. 心理壓力源｜psychological stressor.","B. 反應性壓力源｜reactive stressor.","C. 物理壓力源｜physical stressor."],"answer":"C"},
  {"question":"維持健康的常識性作法稱為？ | Common-sense steps to maintain fitness/health are known as…","options":["A. 自我提升措施｜self-improvement measures.","B. 積極自我完善｜positive self-improvement.","C. 積極措施｜positive measures."],"answer":"C"},
  {"question":"某任務的壓力取決於？ | Stress experienced with a task depends on…","options":["A. 感知需求與實際能力｜perceived demand & actual ability.","B. 感知需求與感知能力｜perceived demand & perceived ability.","C. 實際需求與實際能力｜actual demand & actual ability."],"answer":"B"},
  {"question":"長時間輪班會？ | Long shift work will…","options":["A. 提升診斷維護能力｜increase ability.","B. 先降後習慣｜initially decrease then you get used to it.","C. 降低診斷維護能力｜decrease ability."],"answer":"C"},
  {"question":"第3/4期睡眠是？ | Phase 3 and 4 sleep is…","options":["A. 每個週期僅一次｜occurs only once per cycle.","B. 最有利身體恢復｜most beneficial for recovery.","C. 由酒精誘發｜induced by alcohol."],"answer":"B"},
  {"question":"臨床失眠可由何致？ | Clinical insomnia can be caused by…","options":["A. 咖啡因｜caffeine.","B. 時差｜jet lag.","C. 環境改變｜change of environment."],"answer":"A"},
  {"question":"晝夜節律失常的恢復速率？ | Normal recovery for circadian dysrhythmia is…","options":["A. 每日 2.5 小時｜2.5 h/day.","B. 每日 1.5 小時｜1.5 h/day.","C. 每日 2 小時｜2 h/day."],"answer":"B"},
  {"question":"噪音對人因表現的比較？ | Comparing noise levels on Human Performance…","options":["A. 無影響｜noise has no effect.","B. 討厭但可無限期表現良好｜annoying yet perform well indefinitely.","C. 噪音與錯誤與速度成正比｜noise directly proportional to errors & speed."],"answer":"C"},

  {"question":"環境壓力來源？ | Environmental stresses are…","options":["A. 噪音/煙霧/熱/振動造成｜caused by noise, fumes, heat, vibration.","B. 人人同等容忍｜tolerated equally by everyone.","C. 通常不會累積｜not normally cumulative."],"answer":"A"},
  {"question":"需提供護耳器的噪音門檻？ | Employers must provide ear protectors if noise reaches…","options":["A. 70 dB","B. 85 dB","C. 60 dB"],"answer":"B"},
  {"question":"最大允許噪聲劑量？ | Maximum allowable noise dose is…","options":["A. 85 dB","B. 任何超過 90 dB TWA 的噪音/時間組合｜any combo exceeding 90 dB TWA.","C. 90 dB 持續 24 小時｜90 dB for 24h."],"answer":"B"},
  {"question":"『環境捕獲』易發於？ | ‘Environmental capture’ likely when doing same job…","options":["A. 但在不同機型上｜on different aircraft types.","B. 在同一機型上｜on the same aircraft type.","C. 在很短時間內｜in a short timescale."],"answer":"B"},
  {"question":"英國空側坡道駕駛最易哪側失聰？ | UK air-side ramp driver likely to go deaf in…","options":["A. 左耳｜left ear.","B. 雙耳｜both ears.","C. 右耳｜right ear."],"answer":"C"},
  {"question":"發動機運轉時建議護耳的距離？ | Use ear protection up to proximity…","options":["A. 200–300 m","B. 20–30 m","C. 2–3 m"],"answer":"A"},
  {"question":"55°F 室外工作對手部靈巧度影響？ | Working outside at 55°F affects hand dexterity…","options":["A. 約 50%｜Around 50%.","B. 非常輕微｜Very slight.","C. 無影響｜None."],"answer":"A"},
  {"question":"強光作業應注意？ | When working with bright lights consider…","options":["A. 影像模糊｜blurred image.","B. 陰影｜shadows.","C. 眩光｜glare."],"answer":"C"},
  {"question":"哪個敘述正確？ | Which of the following is true?","options":["A. 噪音與工作標準成正比影響｜Noise affects standard proportionately.","B. 噪音不影響工作標準｜Noise does not affect standard.","C. 噪音會影響某些人的工作標準｜Noise does affect certain people."],"answer":"C"},
  {"question":"環境噪音對工程師？ | Effect of environmental noise on an engineer…","options":["A. 提高專注與品質｜improves concentration and quality.","B. 降低專注與品質｜decreases concentration and quality.","C. 無影響｜no affect."],"answer":"B"},
  {"question":"過度噪音會？ | Excess noise in a working environment can…","options":["A. 提升對其他壓力的抵抗｜raise resistance.","B. 不影響表現｜not affect performance.","C. 降低對其他壓力的抵抗｜lower resistance."],"answer":"C"},
  {"question":"線上作業 −15°C 應？ | If temperature is −15°C while on the line, you should…","options":["A. 定期輪替並監督｜rotate engineers and supervise.","B. 無論天氣繼續以保飛｜carry on regardless to keep flying.","C. 停止維修待天氣好轉｜stop all maintenance until weather improves."],"answer":"C"},
  {"question":"再度：55°F 對手部靈巧度？ | Studies show at 55°F hand dexterity…","options":["A. 無影響｜None.","B. 約 50% 降低｜Around 50% reduction.","C. 非常輕微降低｜Very slight reduction."],"answer":"B"},
  {"question":"影響冷壓力的因素？ | Cold stress can be influenced by…","options":["A. 維生素不足｜insufficient vitamins.","B. 體溫下降｜drop in body temperature.","C. 風寒係數｜wind chill factor."],"answer":"C"},
  {"question":"極端高溫且嘈雜環境造成？ | Environmental stresses in extreme heat/noise cause…","options":["A. 注意力被打擾與分散｜attention disturbed/distributed.","B. 無注意力流失｜no loss of attention.","C. 完全失去注意力｜total loss of attention."],"answer":"A"},
  {"question":"最適合維修的環境？ | Best environment for aircraft maintenance…","options":["A. 夜間戶外雨中｜outside at night in rain.","B. 戶外正午烈日｜outside in direct midday sun.","C. 室內明亮舒適機庫｜inside a well-lit comfortable hangar."],"answer":"C"},
  {"question":"強噪音可能導致？ | Intense/loud noise may lead to…","options":["A. 失聰｜deafness.","B. 疲勞｜fatigue.","C. 無影響｜no effects."],"answer":"B"},
  {"question":"機庫設施照明應？ | Facility lighting in a hangar should be…","options":["A. 不超過10 lux｜no brighter than 10 lux.","B. 固定燈具，光影 3:1｜fixed units giving light:shadow 3:1.","C. 便攜式以利個別任務｜portable for individual tasks."],"answer":"B"},
  {"question":"設計任務時可舉起的最大重量？ | Max mass an engineer should lift when designing tasks…","options":["A. 32 kg","B. 23 kg","C. 50 kg"],"answer":"B"},
  {"question":"感知/知覺錯誤最可能來自？ | Sensing & perception errors most likely from…","options":["A. 他人干擾｜distraction of other engineers.","B. 照明差或噪音｜poor lighting or noise.","C. 訓練不足｜lack of training."],"answer":"B"},
  {"question":"機庫任務照明主要應為？ | Task lighting in a hangar is mainly…","options":["A. 固定照明提供｜provided by fixed lighting.","B. 螢光燈管提供｜provided by fluorescent tubes.","C. 可攜以照亮個別任務｜portable so tasks are well lit."],"answer":"C"},

  {"question":"檢查小裂縫時為避免漏看應？ | Inspecting for small cracks: to avoid missing a crack you should…","options":["A. 盯住同一區數秒以對焦｜hold vision stationary for seconds.","B. 不用鏡子｜not use a mirror.","C. 讓眼睛持續掃過區域｜constantly move eyes across/around area."],"answer":"C"},
  {"question":"由暗到亮最短適應時間？ | From poorly lit to well-lit area, minimum adaptation time…","options":["A. 7 分鐘｜7 minutes.","B. 7 秒｜7 seconds.","C. 30 秒｜30 seconds."],"answer":"A"},
  {"question":"逐項檢查單應如何處理？ | Itemized checklists should be dealt with…","options":["A. 任意順序只要做完｜in any order if all steps completed.","B. 逐項按順序完成｜item by item, in order.","C. 全靠記憶｜as memorized."],"answer":"B"},
  {"question":"非常亮的人造光下檢查之主要缺點？ | Main disadvantage of critical inspections under very bright artificial light…","options":["A. 眩光｜glare.","B. 陰影｜shadows.","C. 濾光｜filtered light."],"answer":"A"},
  {"question":"何時易發生視差誤差？ | Parallax error likely when…","options":["A. 用 5x/10x 放大鏡檢查｜using 5x/10x magnifier.","B. 用游標卡尺/電錶等精密量測｜using precision instruments (vernier/AVO).","C. 無｜Nothing."],"answer":"B"},

  {"question":"良好的交接包含？ | What constitutes a good work handover?","options":["A. 書面＋口頭說明｜written and verbal account.","B. 僅書面｜written documentation.","C. 僅口頭｜verbal account."],"answer":"A"},
  {"question":"良好輪班交接應含？ | A good shift handover should include details of…","options":["A. 已完工/人員/待辦與工具｜completed; persons; to-do; tools.","B. 已完工、進行中與狀態/問題、待辦與工具｜completed; in-progress status/problems; to-do; tools.","C. 已完工、進行中與狀態/問題、待辦與一般公司與技術資訊｜completed; in-progress status/problems; to-do; general company & technical info."],"answer":"C"},
  {"question":"排班交接的建議重疊時間？ | Good practice is rostered overlap of…","options":["A. 2–3 小時｜2–3 hours.","B. 5–10 分鐘｜5–10 minutes.","C. 20–30 分鐘｜20–30 minutes."],"answer":"C"},
  {"question":"「非同步」的通訊包括？ | 'Asynchronous' communication includes…","options":["A. 透過無線電的即時語音｜immediate voice by radio link.","B. 技術手冊、備忘錄、諮詢通告、適航指令｜technical manuals, memos, ACs, ADs.","C. 面對面溝通｜face-to-face communications."],"answer":"B"},
  {"question":"最有效的溝通方式是？ | The most effective form of communication is…","options":["A. 口頭｜verbal.","B. 書面｜written.","C. 明確式（Explicit）｜explicit."],"answer":"C"},
  {"question":"飛機維修工程中最重要的溝通手段？ | Most important means of communication in aircraft maintenance engineering…","options":["A. 書面｜Written.","B. 含蓄/隱含｜Implicit.","C. 口語｜Verbal."],"answer":"A"},
  {"question":"若被指派不確定的任務，你應該？ | If you are given a task you are unsure of, you should…","options":["A. 查閱適當的核准資料｜consult appropriate approved data.","B. 問做過的人｜ask someone who has done it.","C. 看型別課程筆記｜consult type course notes."],"answer":"A"},
  {"question":"重要系統故障的警告方式應該是？ | Alerting for an important system failure should be…","options":["A. 聽覺警告｜aural warning.","B. 紅色閃爍視覺信號｜flashing visual, preferably red.","C. Dolls-eye 指示器｜dolls-eye indicator."],"answer":"A"},

  {"question":"SHEL 模型考量哪些面向？ | SHEL model takes into account…","options":["A. 軟體/硬體/環境/活體（人）｜Software, Hardware, Environment, Liveware.","B. 軟體/硬體/效率/活體｜Software, Hardware, Efficiency, Liveware.","C. 軟體/硬體/環境/地點｜Software, Hardware, Environment, Location."],"answer":"A"},
  {"question":"維護手冊的撰寫與解讀屬於 SHEL 的哪一項？ | Writing & interpretation of maintenance manuals fit…","options":["A. 硬體｜Hardware.","B. 軟體｜Software.","C. 環境｜Environment."],"answer":"B"},
  {"question":"「誤差鏈」理論是指？ | The 'error chain' theory refers to…","options":["A. 調查組織內錯誤鏈以移除最弱員工。","B. 只要移除最弱環節就可防錯。","C. 錯誤由連鎖事件導致，打斷任一環即可避免事故｜errors caused by linked events; break a link to prevent error."],"answer":"C"},
  {"question":"飛機設計屬於 SHEL 的？ | Aircraft design fits into…","options":["A. 人（Liveware）","B. 硬體（Hardware）","C. 環境（Environment）"],"answer":"B"},
  {"question":"最難以『設計排除』或『繞開』錯誤的 SHEL 面向？ | Most difficult SHEL part to design out/work around…","options":["A. 人（Liveware）","B. 軟體（Software）","C. 環境（Environment）"],"answer":"A"},
  {"question":"維修程序中的違規通常是？ | A violation in maintenance procedure…","options":["A. 多半出於想把事做好之善意｜usually with best intentions to 'get the job done'.","B. 一律視為破壞或蓄意破壞。","C. 總為滿足個人需求與任務無關。"],"answer":"A"},
  {"question":"最容易修正的人為錯誤類型？ | Which type of human error is easiest to correct?","options":["A. 恆常誤差（Constant error）","B. 可逆誤差（Reversible error）","C. 變異誤差（Variable error）"],"answer":"A"},
  {"question":"忘了裝回發動機整流罩屬於？ | Forgetting to replace an engine cowling is a…","options":["A. Mistake（錯誤）","B. Lapse（失念/遺漏）","C. Slip（手滑/差錯）"],"answer":"B"},
  {"question":"在『slips/lapses/mistakes』分類中，Mistake 多發生於？ | A mistake typically occurs at the…","options":["A. 記憶儲存階段｜storage (memory) stage.","B. 執行階段｜execution stage.","C. 規劃階段｜planning stage."],"answer":"C"},
  {"question":"因壓力在複雜任務中採用自訂程序，法律上稱為？ | Using own procedures under pressure on a complex task is legally…","options":["A. 修改（modification）","B. 主動（initiative）","C. 違規（violation）"],"answer":"C"},
  {"question":"『有經驗』工程師的目視檢查屬於？ | Visual inspection by an experienced engineer is…","options":["A. 知識＋規則基礎｜knowledge & rule based.","B. 技能＋知識基礎｜skill & knowledge based.","C. 技能＋規則基礎｜skill & rule based."],"answer":"A"},
  {"question":"Troubleshooting 屬於？ | Troubleshooting is…","options":["A. 規則基礎｜rule based.","B. 技能基礎｜skill based.","C. 知識基礎｜knowledge based."],"answer":"A"},
  {"question":"Violation 的定義是？ | A violation is…","options":["A. 無意之錯誤｜unintentional error.","B. 蓄意偏離規則｜deliberate departure from rules.","C. 蓄意破壞行為｜intentional sabotage."],"answer":"B"},
  {"question":"Mistake 的定義是？ | A mistake is…","options":["A. 蓄意偏離規則","B. 蓄意破壞","C. 無意之錯誤｜unintentional error"],"answer":"C"},
  {"question":"扳手被踢落進開啟的發動機罩打壞感測器是？ | Spanner kicked off into open cowl breaking a sensor is…","options":["A. 技能基礎錯誤｜skill-based error.","B. 墨菲定律｜Murphy’s law.","C. 可處罰事件｜punishable occurrence."],"answer":"B"},
  {"question":"經驗工程師在例行更換中裝錯密封屬於？ | Experienced engineer fits wrong seal during routine change is…","options":["A. 技能基礎｜skill based.","B. 規則基礎｜rule based.","C. 知識基礎｜knowledge based."],"answer":"B"},
  {"question":"在翼上作業把扳手踢進發動機罩打壞感測器屬於？ | Kicking a spanner into cowl breaking a sensor is…","options":["A. 知識基礎錯誤","B. 技能基礎錯誤（slip）","C. 規則基礎錯誤"],"answer":"B"},
  {"question":"Mistake 與 Violation 的差別？ | Difference between a mistake and a violation…","options":["A. Mistake 較不嚴重。","B. Violation 非刻意。","C. Mistake 無意、Violation 蓄意｜mistake unintentional; violation deliberate."],"answer":"C"},
  {"question":"裝閥門時遺漏必要密封屬於？ | Fitting a valve without a required seal is…","options":["A. 知識基礎｜Knowledge based.","B. 規則基礎｜Rule based.","C. 技能基礎｜Skill based."],"answer":"B"},
  {"question":"SHEL 模型的樞紐為？ | The hub of the SHEL model is…","options":["A. 人（Liveware）","B. 硬體（Hardware）","C. 環境（Environment）"],"answer":"A"},
  {"question":"Type 1 目視檢查錯誤是？ | A type 1 visual inspection error occurs when…","options":["A. 漏掉瑕疵品｜a faulty item is missed.","B. 好品被錯判為不良｜a good item is wrongly identified as faulty.","C. 未做重檢｜duplicate inspection not carried out."],"answer":"B"},
  {"question":"Error 與 Violation 的差別？ | Difference between error and violation…","options":["A. Violation 是蓄意，Error 不是｜Violation deliberate; error not.","B. Error 蓄意、Violation 不是。","C. 沒差別。"],"answer":"A"},
  {"question":"何謂潛在故障（Latent failure）？ | What is a latent failure?","options":["A. 已犯但尚未導致事故的錯誤｜a mistake already made but not yet caused an accident.","B. 來自不懂維修的主管之錯誤指示。","C. 無法預測的失敗。"],"answer":"A"},
  {"question":"打斷『誤差鏈』會？ | What happens when you break the chain of error?","options":["A. 事故發生。","B. 飛行員 72 小時內報告。","C. 事故不會發生｜Accident does not happen."],"answer":"C"},
  {"question":"忘了在放油塞裝密封屬於？ | Forgetting to fit a seal to an engine drain plug is…","options":["A. 作為錯誤（commission）","B. 違規","C. 遺漏錯誤（omission）"],"answer":"C"},
  {"question":"為趕期限在不理想條件下工作屬於？ | Performing a task in less-than-ideal conditions to meet a deadline is…","options":["A. 例行錯誤（routine error）","B. 情境違規（situational violation）","C. 規則基礎 slip"],"answer":"B"},
  {"question":"自行發展複雜任務的作法屬於？ | Developing one’s own method for a complex task is…","options":["A. 值得讚揚的機智。","B. 規則基礎行為。","C. 經常性的違規｜violating on a regular basis."],"answer":"C"},
  {"question":"維護過程中的容錯（Error tolerance）是指？ | Error tolerance in maintenance process refers to…","options":["A. 執行專為找錯而設計的任務。","B. 系統在維護錯誤後仍可運作的能力｜ability to remain functional after an error.","C. 消除導致錯誤之因素的過程｜process of eliminating contributing factors."],"answer":"B / C（題目給兩個可接受定義）"},

  {"question":"高處作業的主要危害？ | Working on raised platforms/ladders contributes danger of…","options":["A. 鷹架可能是木製。","B. 梯子打滑人員墜落｜ladder may slip and man falls.","C. 兩人同時在同一升降設備維護。"],"answer":"B"},
  {"question":"風險評估與管理是？ | Risk assessment and management is…","options":["A. 將風險降到可容忍並持續監控｜reduce risks to tolerable level & monitor.","B. 徹底移除所有風險並監控新作法。","C. 改用更便宜供應商。"],"answer":"A"},
  {"question":"進行風險評估時應？ | When carrying out a risk assessment…","options":["A. 必須戴安全帽。","B. 辨識設備/程序可能失效處｜identify where equipment/procedures might fail.","C. 無需作為。"],"answer":"B"},

              ];

              function shuffle(array) {
          for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [array[i], array[j]] = [array[j], array[i]];
          }
          return array;
        }
        function fmtTime(s) {
          const m = Math.floor(s / 60).toString().padStart(2, "0");
          const sec = (s % 60).toString().padStart(2, "0");
          return m + ":" + sec;
        }
        function showView(idToShow) {
          ["welcome","quiz","results","bank"].forEach(id => {
            const el = document.getElementById(id);
            if (!el) return;
            if (id === idToShow) el.classList.remove("hidden");
            else el.classList.add("hidden");
          });
          window.scrollTo({ top: 0, behavior: "smooth" });
        }

        /* ====== 深色模式：持久化 ====== */
        const darkBtn = document.getElementById("darkModeToggle");
        function applyInitialTheme() {
          try {
            const saved = localStorage.getItem('theme');
            const isDark = (saved === 'dark') || (!saved && window.matchMedia('(prefers-color-scheme: dark)').matches);
            document.body.classList.toggle('dark', isDark);
            darkBtn.setAttribute('aria-pressed', String(isDark));
          } catch(e) {}
          document.documentElement.classList.remove('preload-dark');
        }
        applyInitialTheme();
        darkBtn.addEventListener('click', function(){
          const willDark = !document.body.classList.contains('dark');
          document.body.classList.toggle('dark', willDark);
          darkBtn.setAttribute('aria-pressed', String(willDark));
          try { localStorage.setItem('theme', willDark ? 'dark' : 'light'); } catch(e){}
        });

        /* ====== 測驗狀態 ====== */
        let shuffledQuestions;
        let current = 0, total = 0, timer = 80 * 60, interval, answers = [];
        let quizActive = false;
        const progressBar = document.getElementById("progressBar");

        /* ====== 元件 ====== */
        const startBtn = document.getElementById("startBtn");
        const prevBtn = document.getElementById("prevBtn");
        const leaveBtn = document.getElementById("leaveBtn");
        const retryBtn = document.getElementById("retryBtn");
        const showWrongBtn = document.getElementById("showWrongBtn");
        const showAllBtn = document.getElementById("showAllBtn");
        const openBankBtn = document.getElementById("openBankBtn");
        const toBankFromResults = document.getElementById("toBankFromResults");

        /* ====== 題庫瀏覽 ====== */
        const bankBody = document.getElementById("bankBody");
        const bankSearch = document.getElementById("bankSearch");
        const perPageSel = document.getElementById("perPage");
        const pageInfo = document.getElementById("pageInfo");
        const prevPageBtn = document.getElementById("prevPage");
        const nextPageBtn = document.getElementById("nextPage");
        const backToWelcome = document.getElementById("backToWelcome");
        const pagination = document.querySelector('#bank .pagination');

        // 抓取自訂時間輸入框
        const durationInput = document.getElementById("durationInput");

        let bankFiltered = questions.slice();
        let page = 1;
        function totalPages() {
          const sel = perPageSel.value;
          if (sel === 'all') return 1;
          return Math.max(1, Math.ceil(bankFiltered.length / parseInt(sel || "10")));
        }

        /* ====== 測驗流程 ====== */
        startBtn.addEventListener("click", () => {
          const n = document.getElementById("nameInput").value.trim();
          const qLimit = parseInt(document.getElementById("questionLimit").value);

          if (!n) return alert("請輸入姓名 / Enter your name");
          if (!qLimit || qLimit <= 0) return alert("請輸入要作答的題數,最多5題 / Enter number of questions");

          // 讀取自訂時間（分鐘）；預設 80，限制 1~300 分鐘
          let minutes = parseInt((durationInput && durationInput.value) ? durationInput.value : "80");
          if (isNaN(minutes)) minutes = 80;
          minutes = Math.max(1, Math.min(999, minutes));

          shuffledQuestions = shuffle(questions.slice()).slice(0, Math.min(qLimit, questions.length));
          total = shuffledQuestions.length;
          current = 0; answers = [];
          timer = minutes * 60;            // 用自訂分鐘
          quizActive = true;

          document.getElementById("welcomeName").innerText = "歡迎: " + n;
          document.getElementById("total").innerText = total;
          // 進場前先把右上角時計顯示成正確的起始值
          document.getElementById("timer").innerText = fmtTime(timer);
          updateProgress();

          // 確保不會重複計時
          clearInterval(interval);
          interval = setInterval(() => {
            if (timer > 0 && quizActive) {
              timer--;
              document.getElementById("timer").innerText = fmtTime(timer);
            } else if (quizActive && timer <= 0) {
              clearInterval(interval);
              finish();
            }
          }, 1000);

          showQ();
          showView("quiz");
        });

        prevBtn.addEventListener("click", () => {
          if (current > 0) {
            current--;
            answers.pop();
            showQ();
          }
        });

        leaveBtn.addEventListener("click", finish);
        retryBtn.addEventListener("click", () => location.reload());
        showWrongBtn.addEventListener("click", () => renderResults(answers.filter(a => !a.correct)));
        showAllBtn.addEventListener("click", () => renderResults(answers));
        openBankBtn.addEventListener("click", enterBank);
        toBankFromResults.addEventListener("click", enterBank);

        /* ====== 題庫事件 ====== */
        bankSearch.addEventListener("input", applyFilter);
        perPageSel.addEventListener("change", () => { page = 1; renderBank(); });
        prevPageBtn.addEventListener("click", () => { if (page > 1) { page--; renderBank(); } });
        nextPageBtn.addEventListener("click", () => { if (page < totalPages()) { page++; renderBank(); } });
        backToWelcome.addEventListener("click", () => showView("welcome"));

        function enterBank() {
          if (quizActive) { alert("測驗進行中不可瀏覽題庫。請先完成或離開考試。"); return; }
          if (!bankSearch.value) { bankFiltered = questions.slice(); page = 1; }
          renderBank();
          showView("bank");
        }

        function applyFilter() {
          const kw = bankSearch.value.trim().toLowerCase();
          bankFiltered = kw
            ? questions.filter(q => q.question.toLowerCase().includes(kw) ||
                                    q.options.some(o => o.toLowerCase().includes(kw)))
            : questions.slice();
          page = 1; renderBank();
        }

        function renderBank() {
          bankBody.innerHTML = "";
          const sel = perPageSel.value;
          const per = (sel === 'all') ? bankFiltered.length : parseInt(sel || "10");
          const start = (page - 1) * per;
          const items = (sel === 'all') ? bankFiltered.slice() : bankFiltered.slice(start, start + per);

          items.forEach((q, idx) => {
            const tr = document.createElement("tr");
            const num = (sel === 'all') ? (idx + 1) : (start + idx + 1);
            const correctText = q.options.find(o => o.charAt(0) === q.answer) || "";

            const optsHtml = q.options.map(o => {
              const isC = (o.charAt(0) === q.answer);
              return `<span class="opt-row ${isC ? 'is-correct' : ''}">${isC ? '<span class="ans-chip">正解</span>' : ''}${o}</span>`;
            }).join("");

            tr.innerHTML =
              '<td class="mono">#' + num + "</td>" +
              "<td>" + q.question + "</td>" +
              "<td>" + optsHtml + "</td>" +
              '<td class="mono ans-cell">' + (q.answer + "｜" + correctText) + "</td>";
            bankBody.append(tr);
          });

          const tp = totalPages();
          if (sel === 'all') {
            if (pagination) pagination.style.display = 'none';
            pageInfo.textContent = "全部顯示（共 " + bankFiltered.length + " 題）";
            prevPageBtn.disabled = true; nextPageBtn.disabled = true;
          } else {
            if (pagination) pagination.style.display = 'flex';
            pageInfo.textContent = "第 " + page + " / " + tp + " 頁（共 " + bankFiltered.length + " 題）";
            prevPageBtn.disabled = (page <= 1); nextPageBtn.disabled = (page >= tp);
          }
        }

        /* ====== 測驗：出題/進度/結束 ====== */
        function showQ() {
          if (current >= total) return finish();
          document.getElementById("current").innerText = current + 1;
          updateProgress();

          const q = shuffledQuestions[current];
          document.getElementById("questionText").innerText = q.question;

          const optDiv = document.getElementById("options");
          optDiv.innerHTML = "";

          let optionsWithFlag = q.options.map(option => ({ text: option, isAnswer: option.charAt(0) === q.answer }));
          optionsWithFlag = shuffle(optionsWithFlag);

          optionsWithFlag.forEach(opt => {
            const lbl = document.createElement("label");
            const rd = document.createElement("input");
            rd.type = "radio"; rd.name = "opt"; rd.value = opt.text;
            rd.onchange = function () {
              answers.push({
                q, selectedText: opt.text,
                correctText: q.options.find(optItem => optItem.charAt(0) === q.answer),
                correct: opt.isAnswer
              });
              current++; showQ();
            };
            lbl.append(rd, " ", opt.text);
            optDiv.append(lbl);
          });
        }

        function updateProgress() {
          const percent = (current / total) * 100;
          progressBar.style.width = percent + "%";
        }

        function finish() {
          clearInterval(interval);
          quizActive = false; // 結束後可進入題庫
          showView("results");
          renderResults(answers);
          document.getElementById("scoreSummary").innerText =
            "答對 " + answers.filter(a => a.correct).length +
            " 題 / 已作答 " + answers.length + " 題 / 共 " + total + " 題";
        }

        function renderResults(data) {
          const tb = document.getElementById("resultsBody");
          tb.innerHTML = "";
          data.forEach(a => {
            const tr = document.createElement("tr");
            tr.innerHTML =
              "<td>" + a.q.question + "</td>" +
              "<td>" + a.selectedText + "</td>" +
              '<td class="ans-cell">' + a.correctText + "</td>" +
              "<td>" + (a.correct ? "O" : "X") + "</td>";
            if (!a.correct) tr.classList.add("wrong");
            tb.append(tr);
          });
        }
      });
    </script>
  </body>
</html>

</html>
