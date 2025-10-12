<吃飽太閒做的網站，能幫到你我覺得很開心>
<html lang="zh-Hant">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>147測驗｜單一檔案版</title>
    <style>
            /* 回首頁浮動按鈕 */
            #homeBtn {
        position: absolute;
        top: 100px;               /* 深色模式在20px，這裡放在它下方 */
        right: 20px;
        padding: 10px 20px;
        background: #28a745;
        color: #fff;
        border: none;
        border-radius: 8px;
        text-decoration: none;
        font-size: 1em;
        box-shadow: 0 4px 12px rgba(0,0,0,.15);
        transition: background .3s, transform .2s, box-shadow .2s;
        z-index: 1000;
      }
      #homeBtn:hover {
        background: #218838;
        transform: translateY(-2px);
        box-shadow: 0 6px 16px rgba(0,0,0,.25);
      }
      body.dark #homeBtn {
        background: #2e7d32;
      }
      body.dark #homeBtn:hover {
        background: #25652a;
      }

            body {
              font-family: Arial, sans-serif;
              margin: 0;
              padding: 40px;
              font-size: 1.6em;
              background: #f0f4f8;
              color: #000;
              transition: background-color 0.5s, color 0.5s;
            }
            body.dark { background: #121212; color: #fff; }
            #container {
              max-width: 1200px; margin: auto; background: #fff; padding: 40px;
              border-radius: 20px; box-shadow: 0 0 10px rgba(0,0,0,.1);
              transition: background-color .5s, color .5s;
            }
            body.dark #container { background: #1e1e1e; }
            .hidden { display: none; }
            h1, h2 { text-align: center; font-size: 2.4em; }
            #rules {
              background: #e9ecef; padding: 20px; margin-bottom: 40px;
              border-radius: 10px; font-size: 1.2em;
            }
            body.dark #rules { background: #333; }
            .btn {
              background: #007bff; color: #fff; border: none; padding: 20px 40px;
              margin: 10px; border-radius: 10px; cursor: pointer; font-size: 1.2em;
              transition: background-color .3s;
            }
            .btn:hover { background: #0056b3; }
            #leaveBtn { background: #dc3545; }
            #progress, #timer { font-weight: bold; font-size: 1.4em; }
            .progress-container {
              background: #ddd; height: 10px; border-radius: 5px; margin-top: 20px; overflow: hidden;
            }
            body.dark .progress-container { background: #555; }
            .progress-bar { height: 100%; width: 0; background: #007bff; transition: width .6s ease; }
            .question { margin: 40px 0 20px; font-size: 1.8em; }
            .options label { display: block; margin-bottom: 16px; font-size: 1.4em; }
            table { width: 100%; border-collapse: collapse; margin-top: 40px; font-size: 1.2em; }
            th, td { border: 1px solid #ccc; padding: 16px; text-align: left; }
            tr.wrong { background-color: #ffe6e6; }
            body.dark tr.wrong { background-color: #661111; }
            #darkModeToggle {
              position: absolute; top: 20px; right: 20px; padding: 10px 20px;
              background: #333; color: #fff; border: none; border-radius: 8px; cursor: pointer; font-size: 1em;
              transition: background .3s;
            }
            #darkModeToggle:hover { background: #555; }
    </style>
  </head>
  <body>
    <button id="darkModeToggle">深色模式 / Dark Mode</button>
    <a id="homeBtn" href="https://hisausage7.github.io/147test/" title="回首頁"
      >🏠 回首頁</a
    >

    <div id="container">
      <div id="welcome">
        <h1>147測驗M9CAA</h1>
        <div id="rules">
          <p><strong>考試注意事項 / Exam Rules:</strong></p>
          <P>!此章節沒有提供圖片題!
          </p>
            1. 請輸入姓名後才能開始作答。 / You must enter your name to start
            the quiz.
          </p>
          <p>
            2. 考試限時80分鐘，自動倒數。 / The quiz is timed for 80 minutes,
            countdown starts immediately.
          </p>
          <p>
            3. 作答途中可隨時點擊「離開考試」提前結束。 / You can click "Leave
            Quiz" anytime to finish early.
          </p>
          <p>
            4. 完成後會自動顯示所有答題結果與成績。 / Results and scores will be
            displayed after completion.
          </p>
          <p>
            5. 答對題目顯示O，答錯題目顯示X。 / Correct answers will show O,
            incorrect answers will show X.
          </p>
          <p>
            6. 測驗過程為亂序出題。 / The test process was chaotic and
            disordered in setting questions.
          </p>
          <p>!版權及源代碼所有-航機系008沈崑宸!</p>
          <p>!僅作為自我測驗使用!</p>
        </div>
        <input
          type="text"
          id="nameInput"
          placeholder="輸入姓名 / Enter your name"
          style="width:100%;padding:8px;margin-bottom:10px;font-size:1.4em;"
        />
        <input
          type="number"
          id="questionLimit"
          placeholder="輸入題數,至多75題 / Enter number of questions"
          style="width:100%;padding:8px;margin-bottom:10px;font-size:1.4em;"
        />
        <button id="startBtn" class="btn">開始測驗 / Start Quiz</button>
      </div>

      <div id="quiz" class="hidden">
        <div>
          <span id="welcomeName"></span>
          <span id="timer" style="float:right">80:00</span>
        </div>
        <div id="progress">
          題數: <span id="current">0</span> / <span id="total">0</span>
        </div>
        <div class="progress-container">
          <div id="progressBar" class="progress-bar"></div>
        </div>
        <div class="question" id="questionText"></div>
        <div class="options" id="options"></div>
        <button id="prevBtn" class="btn" style="background:#6c757d">
          上一題 / Previous
        </button>
        <button id="leaveBtn" class="btn">離開考試 / Leave Quiz</button>
      </div>

      <div id="results" class="hidden">
        <h2>測驗結果 / Results</h2>
        <div>
          <button id="retryBtn" class="btn">重新開始 / Retry</button>
          <button id="showWrongBtn" class="btn" style="background:#ffc107">
            只看錯題 / Wrong Only
          </button>
          <button id="showAllBtn" class="btn">看全部結果 / Show All</button>
        </div>
        <table>
          <thead>
            <tr>
              <th>題目</th>
              <th>您的答案</th>
              <th>正確答案</th>
              <th>結果</th>
            </tr>
          </thead>
          <tbody id="resultsBody"></tbody>
        </table>
        <div
          id="scoreSummary"
          style="text-align:center;margin-top:20px;font-size:1.2em"
        ></div>
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
    answer: "C"
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
    answer: "B"
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
    answer: "B"
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
    answer: "C"
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
    answer: "B"
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
    answer: "C"
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
    answer: "A"
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
  }






              ];

              function shuffle(array) {
                for (let i = array.length - 1; i > 0; i--) {
                  const j = Math.floor(Math.random() * (i + 1));
                  [array[i], array[j]] = [array[j], array[i]];
                }
                return array;
              }

              let shuffledQuestions;
              let current = 0, total = 0, timer = 80 * 60, interval, answers = [];

              function fmtTime(s) {
                const m = Math.floor(s / 60).toString().padStart(2, "0");
                const sec = (s % 60).toString().padStart(2, "0");
                return m + ":" + sec;
              }

              const startBtn = document.getElementById("startBtn");
              const prevBtn = document.getElementById("prevBtn");
              const leaveBtn = document.getElementById("leaveBtn");
              const retryBtn = document.getElementById("retryBtn");
              const showWrongBtn = document.getElementById("showWrongBtn");
              const showAllBtn = document.getElementById("showAllBtn");
              const darkModeToggle = document.getElementById("darkModeToggle");
              const progressBar = document.getElementById("progressBar");

              startBtn.addEventListener("click", () => {
                const n = document.getElementById("nameInput").value.trim();
                const qLimit = parseInt(document.getElementById("questionLimit").value);

                if (!n) return alert("請輸入姓名 / Enter your name");
                if (!qLimit || qLimit <= 0) return alert("請輸入要作答的題數,最多105題 / Enter number of questions");

                shuffledQuestions = shuffle([...questions]).slice(0, Math.min(qLimit, questions.length));
                total = shuffledQuestions.length;
                current = 0; answers = []; timer = 80 * 60;

                document.getElementById("welcome").classList.add("hidden");
                document.getElementById("quiz").classList.remove("hidden");
                document.getElementById("welcomeName").innerText = "歡迎: " + n;
                document.getElementById("total").innerText = total;
                updateProgress();

                interval = setInterval(() => {
                  if (timer > 0) {
                    timer--;
                    document.getElementById("timer").innerText = fmtTime(timer);
                  } else {
                    clearInterval(interval);
                    finish();
                  }
                }, 1000);

                showQ();
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
              showWrongBtn.addEventListener("click", filterResultsWrong);
              showAllBtn.addEventListener("click", showAllResults);
              darkModeToggle.addEventListener("click", () => document.body.classList.toggle("dark"));

              function showQ() {
                if (current >= total) return finish();
                document.getElementById("current").innerText = current + 1;
                updateProgress();

                const q = shuffledQuestions[current];
                document.getElementById("questionText").innerText = q.question;

                const optDiv = document.getElementById("options");
                optDiv.innerHTML = "";

                let optionsWithFlag = q.options.map((option) => ({
                  text: option,
                  isAnswer: option.charAt(0) === q.answer,
                }));
                optionsWithFlag = shuffle(optionsWithFlag);

                optionsWithFlag.forEach((opt) => {
                  const lbl = document.createElement("label");
                  const rd = document.createElement("input");
                  rd.type = "radio";
                  rd.name = "opt";
                  rd.value = opt.text;
                  rd.onchange = () => {
                    answers.push({
                      q,
                      selectedText: opt.text,
                      correctText: q.options.find((optItem) => optItem.charAt(0) === q.answer),
                      correct: opt.isAnswer,
                    });
                    current++;
                    showQ();
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
                document.getElementById("quiz").classList.add("hidden");
                document.getElementById("results").classList.remove("hidden");
                renderResults(answers);
                document.getElementById("scoreSummary").innerText =
                  `答對 ${answers.filter((a) => a.correct).length} 題 / 已作答 ${answers.length} 題 / 共 ${total} 題`;
                window.scrollTo({ top: 0, behavior: "smooth" });
              }

              function renderResults(data) {
                const tb = document.getElementById("resultsBody");
                tb.innerHTML = "";
                data.forEach((a) => {
                  const tr = document.createElement("tr");
                  tr.innerHTML = `
                    <td>${a.q.question}</td>
                    <td>${a.selectedText}</td>
                    <td>${a.correctText}</td>
                    <td>${a.correct ? "O" : "X"}</td>
                  `;
                  if (!a.correct) tr.classList.add("wrong");
                  tb.append(tr);
                });
              }

              function filterResultsWrong() { renderResults(answers.filter((a) => !a.correct)); }
              function showAllResults() { renderResults(answers); }
            });
    </script>
  </body>
</html>
