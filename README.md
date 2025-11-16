<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Fake iMessage Generator</title>
  <style>
    body {
      background: #d1d1d6;
      font-family: -apple-system, BlinkMacSystemFont, "Helvetica Neue", sans-serif;
      text-align: center;
      margin: 0;
      padding: 20px;
    }

    h2 {
      margin-bottom: 10px;
    }

    .controls {
      margin-bottom: 20px;
    }

    input {
      padding: 8px;
      border: 1px solid #ccc;
      border-radius: 8px;
      margin: 5px;
      width: 80%;
    }

    button {
      padding: 8px 12px;
      border: none;
      border-radius: 8px;
      background: #007aff;
      color: white;
      cursor: pointer;
      margin: 5px;
    }

    button:hover {
      background: #005ecb;
    }

    .iphone {
      width: 340px;
      height: 640px;
      margin: 0 auto;
      border: 16px solid #333;
      border-radius: 40px;
      background: #fefefe;
      position: relative;
      box-shadow: 0 6px 18px rgba(0,0,0,0.3);
      overflow: hidden;
    }

    .status-bar {
      height: 20px;
      background: #fefefe;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 2px 10px;
      font-size: 12px;
      color: #555;
    }

    .header {
      background: #fefefe;
      border-bottom: 1px solid #ddd;
      padding: 8px;
      text-align: center;
      font-weight: 600;
      font-size: 15px;
      color: #000;
    }

    .chatArea {
      background: #f0f0f5;
      height: 560px;
      overflow-y: auto;
      padding: 15px;
      text-align: left;
    }

    .bubble {
      display: inline-block;
      padding: 10px 15px;
      border-radius: 18px;
      margin: 8px 0;
      max-width: 75%;
      clear: both;
      word-wrap: break-word;
    }

    .sent {
      background: #007aff;
      color: white;
      float: right;
      border-bottom-right-radius: 4px;
    }

    .received {
      background: #e5e5ea;
      color: black;
      float: left;
      border-bottom-left-radius: 4px;
    }

    .time {
      font-size: 10px;
      color: #999;
      clear: both;
      text-align: center;
      margin-top: 4px;
    }

    #contactName {
      width: 80%;
      padding: 8px;
      margin-bottom: 10px;
    }

    .download-btn {
      padding: 8px 12px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      margin-top: 15px;
    }

    .download-btn:hover {
      background-color: #45a049;
    }
  </style>
</head>
<body>

  <h2>Fake iMessage Generator</h2>

  <div class="controls">
    <input id="contactName" placeholder="Enter Contact Name (e.g. John)">
    <input id="message" placeholder="Type your message..." />
    <button onclick="addMessage('sent')">Send ➤</button>
    <button onclick="addMessage('received')">Receive ⬅</button>
  </div>

  <div class="iphone" id="chatBox">
    <div class="status-bar">
      <span id="timeNow">9:41</span>
      <span>🔋 100%</span>
    </div>
    <div class="header" id="contactHeader">Contact Name</div>
    <div class="chatArea" id="chatArea"></div>
  </div>

  <button class="download-btn" onclick="downloadChat()">📸 Download Screenshot</button>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <script>
    // Add a message to the chat
    function addMessage(type) {
      const name = document.getElementById("contactName").value.trim();
      const messageText = document.getElementById("message").value.trim();
      if (!messageText) return;

      // Set contact name in header
      if (name) document.getElementById("contactHeader").textContent = name;

      const chatArea = document.getElementById("chatArea");

      // Create message bubble
      const msg = document.createElement("div");
      msg.className = "bubble " + type;
      msg.textContent = messageText;

      chatArea.appendChild(msg);

      // Add time below message
      const now = new Date();
      const time = document.createElement("div");
      time.className = "time";
      time.textContent = now.getHours() + ":" + (now.getMinutes()<10?"0":"") + now.getMinutes();
      chatArea.appendChild(time);

      chatArea.scrollTop = chatArea.scrollHeight; // Scroll to bottom
      document.getElementById("message").value = ""; // Clear input box
    }

    // Update time in the status bar
    function updateTime() {
      const now = new Date();
      let hours = now.getHours();
      let minutes = now.getMinutes();
      if (minutes < 10) minutes = "0" + minutes;
      document.getElementById("timeNow").textContent = hours + ":" + minutes;
    }

    // Download the chat as a screenshot
    function downloadChat() {
      const chatBox = document.getElementById("chatBox");
      html2canvas(chatBox).then(canvas => {
        const link = document.createElement("a");
        link.download = "fake-imessage.png";
        link.href = canvas.toDataURL();
        link.click();
      });
    }

    // Initialize time when page loads
    updateTime();
  </script>

</body>
</html>
