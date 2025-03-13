<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>句子排列</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      background: #f7f7f7;
    }
    .container {
      text-align: center;
      font-size: 24px;
      font-family: Arial, sans-serif;
      background: #fff;
      padding: 20px 30px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    input, button {
      font-size: 24px;
      padding: 10px;
      margin: 10px;
    }
    /* 題目區：顯示打亂後的字詞 */
    #scrambledContainer {
      border: 2px dashed #ccc;
      padding: 10px;
      margin: 10px;
      min-height: 50px;
    }
    /* 答案區：以虛線框格呈現 */
    #answerContainer {
      border: 2px dashed #ccc;
      padding: 10px;
      margin: 10px;
      min-height: 50px;
      display: flex;
      justify-content: center;
    }
    .answer-slot {
      width: 50px;
      height: 50px;
      border: 2px dashed #ccc;
      margin: 5px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 24px;
    }
    /* 正確與錯誤時，答案框的背景及邊框改變 */
    .correct {
      background-color: #a4f9a4;
      border-color: green;
    }
    .incorrect {
      background-color: #f9a4a4;
      border-color: red;
    }
    /* 可拖拉的字詞 */
    .draggable {
      font-size: 24px;
      margin: 5px;
      padding: 10px 15px;
      border: 1px solid #ccc;
      background: #fafafa;
      cursor: move;
    }
    /* 灑花容器與動畫 */
    #confetti-container {
      position: fixed;
      top: 0; left: 0;
      width: 100%;
      height: 100%;
      pointer-events: none;
      overflow: hidden;
    }
    @keyframes spread {
      0% { opacity: 1; transform: translate(0, 0) scale(0.5); }
      100% { opacity: 0; transform: translate(var(--tx), var(--ty)) scale(2); }
    }
    .confetti {
      position: absolute;
      width: 10px;
      height: 10px;
      opacity: 0.8;
      animation: spread 3s linear forwards;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>句子排列</h1>
    <input type="text" id="inputSentence" placeholder="請輸入句子">
    <button onclick="startGame()">輸入句子</button>
    
    <h3>題目</h3>
    <div id="scrambledContainer" class="dropzone"></div>
    
    <h3>你的答案</h3>
    <div id="answerContainer" class="dropzone"></div>
  </div>
  
  <div id="confetti-container"></div>
  
  <!-- 正確與錯誤音效 -->
  <audio id="correctSound" src="correct.mp3"></audio>
  <audio id="errorSound" src="error.mp3"></audio>
  <!-- 完成後的音效 -->
  <audio id="successSound" src="success.mp3"></audio>
  
  <script>
    let originalSentence = "";
    let letterArray = []; // 原始字詞資料 [{id, char}, ...]
    
    // Fisher-Yates 洗牌演算法
    function shuffleArray(array) {
      for (let i = array.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    }
    
    // 使用 Web Speech API 播放語音
    function speak(text) {
      let utterance = new SpeechSynthesisUtterance(text);
      utterance.lang = 'zh-TW';
      window.speechSynthesis.speak(utterance);
    }
    
    // 播放指定的音效
    function playSound(id) {
      const sound = document.getElementById(id);
      if (sound) {
        sound.currentTime = 0;
        sound.play();
      }
    }
    
    // 遊戲啟動：取得輸入句子，建立題目與答案區
    function startGame() {
      originalSentence = document.getElementById("inputSentence").value.trim();
      if (!originalSentence) {
        alert("請先輸入句子！");
        return;
      }
      
      // 將句子拆解成字，並建立包含唯一 id 的陣列
      letterArray = originalSentence.split("").map((char, index) => {
        return { id: "letter-" + index, char: char };
      });
      
      // 打亂順序（複製一份用於題目區）
      let shuffledArray = shuffleArray(letterArray.slice());
      
      // 清空題目與答案容器
      const scrambledContainer = document.getElementById("scrambledContainer");
      const answerContainer = document.getElementById("answerContainer");
      scrambledContainer.innerHTML = "";
      answerContainer.innerHTML = "";
      
      // 在題目區建立可拖拉字詞
      shuffledArray.forEach(letter => {
        const btn = createDraggableElement(letter);
        scrambledContainer.appendChild(btn);
      });
      
      // 根據原始句子長度，在答案區建立對應的虛線框格
      for (let i = 0; i < originalSentence.length; i++) {
        let slot = document.createElement("div");
        slot.className = "answer-slot";
        slot.dataset.index = i;
        slot.addEventListener("dragover", dragOverHandler);
        slot.addEventListener("drop", dropOnAnswerHandler);
        answerContainer.appendChild(slot);
      }
      
      // 題目區也設定為可放置區（方便拖回）
      scrambledContainer.addEventListener("dragover", dragOverHandler);
      scrambledContainer.addEventListener("drop", dropOnScrambledHandler);
    }
    
    // 建立可拖拉的字詞元素
    function createDraggableElement(letter) {
      let btn = document.createElement("button");
      btn.className = "draggable";
      btn.id = letter.id;
      btn.innerText = letter.char;
      btn.setAttribute("draggable", "true");
      btn.addEventListener("dragstart", dragStartHandler);
      return btn;
    }
    
    // 拖拉開始：播放該字語音
    function dragStartHandler(e) {
      // 若已鎖定則不允許拖拉
      if (e.target.getAttribute("draggable") === "false") {
        e.preventDefault();
        return;
      }
      e.dataTransfer.setData("text/plain", e.target.id);
      speak(e.target.innerText);
    }
    
    // 允許拖拉進入
    function dragOverHandler(e) {
      e.preventDefault();
    }
    
    // 當拖拉字詞放到答案框上
    function dropOnAnswerHandler(e) {
      e.preventDefault();
      const slot = e.currentTarget;
      // 若此答案框已有字詞則不接受
      if (slot.children.length > 0) return;
      
      const letterId = e.dataTransfer.getData("text/plain");
      const letterElement = document.getElementById(letterId);
      slot.appendChild(letterElement);
      
      // 將字詞元素背景及邊框設為透明，讓答案框原有背景完整呈現
      letterElement.style.backgroundColor = "transparent";
      letterElement.style.border = "none";
      
      // 根據該位置應有的字判斷正確與否
      const index = parseInt(slot.dataset.index);
      if(letterElement.innerText === originalSentence[index]) {
        slot.classList.remove("incorrect");
        slot.classList.add("correct");
        // 鎖定正確字詞（不可再拖動）
        letterElement.setAttribute("draggable", "false");
        playSound("correctSound");
      } else {
        slot.classList.remove("correct");
        slot.classList.add("incorrect");
        playSound("errorSound");
      }
      
      checkCompletion();
    }
    
    // 當拖拉字詞放回題目區
    function dropOnScrambledHandler(e) {
      e.preventDefault();
      const scrambledContainer = document.getElementById("scrambledContainer");
      const letterId = e.dataTransfer.getData("text/plain");
      const letterElement = document.getElementById(letterId);
      
      // 若原先在答案區，則清除其答案框的樣式
      const parent = letterElement.parentElement;
      if (parent && parent.classList.contains("answer-slot")) {
        parent.classList.remove("correct", "incorrect");
      }
      // 恢復原本按鈕樣式
      letterElement.style.backgroundColor = "";
      letterElement.style.border = "";
      scrambledContainer.appendChild(letterElement);
    }
    
    // 檢查答案是否完成（所有答案框皆正確）
    function checkCompletion() {
      const answerContainer = document.getElementById("answerContainer");
      let slots = answerContainer.children;
      let complete = true;
      for (let i = 0; i < slots.length; i++) {
        let slot = slots[i];
        if(slot.children.length === 0 || !slot.classList.contains("correct")) {
          complete = false;
          break;
        }
      }
      if(complete) {
        showConfetti();
        playSound("successSound");
      }
    }
    
    // 顯示灑花動畫：confetti 從畫面四處隨機位置出現，並由小而大擴散
    function showConfetti() {
      const confettiContainer = document.getElementById("confetti-container");
      for(let i = 0; i < 100; i++){
        let confetti = document.createElement("div");
        confetti.className = "confetti";
        // 隨機位置於整個畫面
        confetti.style.left = Math.random() * window.innerWidth + "px";
        confetti.style.top = Math.random() * window.innerHeight + "px";
        
        // 隨機方向與距離
        let angle = Math.random() * 2 * Math.PI;
        let distance = Math.random() * 500;
        let tx = Math.cos(angle) * distance;
        let ty = Math.sin(angle) * distance;
        confetti.style.setProperty('--tx', tx + "px");
        confetti.style.setProperty('--ty', ty + "px");
        
        confetti.style.backgroundColor = randomColor();
        confetti.style.animationDelay = Math.random() * 1 + "s";
        confettiContainer.appendChild(confetti);
      }
      // 3 秒後清除灑花
      setTimeout(() => {
        confettiContainer.innerHTML = "";
      }, 3000);
    }
    
    // 隨機取得顏色
    function randomColor() {
      const colors = ["#f94144", "#f3722c", "#f8961e", "#f9c74f", "#90be6d", "#43aa8b", "#577590"];
      return colors[Math.floor(Math.random() * colors.length)];
    }
    
  </script>
</body>
</html>
