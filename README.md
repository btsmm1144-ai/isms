<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>iMessage Generator - iOS 16/17 Style</title>
  <style>
    body {
      background: #latest ios;
      font-family: -apple-system, BlinkMacSystemFont, "Helvetica Neue", sans-serif;
      text-align: center;
      margin: 0;
      padding: 20px;
    }

    h2 {
      margin-bottom: 10px;
      font-size: 24px;
      color: #333;
    }

    .controls {
      margin-bottom: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    input, button {
      padding: 12px 20px;
      border: 1px solid #ccc;
      border-radius: 30px;
      margin: 10px 0;
      font-size: 16px;
      width: 80%;
      max-width: 500px;
    }

    input {
      background-color: #fff;
      color: #333;
    }

    button {
      background-color: #007aff;
      color: white;
      cursor: pointer;
    }

    button:hover {
      background-color: #005ecb;
    }

    .iphone {
      width: 375px;
      height: 667px;
      margin: 0 auto;
      border-radius: 50px;
      background: white;
      box-shadow: 0 0 40px rgba(0, 0, 0, 0.2);
      overflow: hidden;
      position: relative;
    }

    .status-bar {
      height: 20px;
      background: #f2f2f7;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 2px 10px;
      font-size: 12px;
      color: #555;
    }

    .header {
      background: #f2f2f7;
      border-bottom: 1px solid #ddd;
      padding: 8px 15px;
      font-weight: 600;
      font-size: 16px;
      color: #000;
      text-align: left;
    }

    .chatArea {
      background: #e5e5ea;
      height: 500px;
      overflow-y: auto;
      padding: 10px;
      text-align: left;
      padding-top: 30px;
    }

    .bubble {
      display: inline-block;
      padding: 12px 18px;
      border-radius: 25px;
      margin: 10px 0;
      max-width: 75%;
      word-wrap: break-word;
      position: relative;
    }

    .sent {
      background: #007aff;
      color: white;
      float: right;
      border-bottom-right-radius: 5px;
    }

    .received {
      background: #e5e5ea;
      color: #333;
      float: left;
      border-bottom-left-radius: 5px;
    }

    .time {
      font-size: 10px;
      color: #999;
      clear: both;
      text-align: center;
      margin-top: 6px;
    }

    .download-btn {
      padding: 12px 24px;
      background-color: #34c759;
      color: white;
      border: none;
      border-radius: 50px;
      cursor: pointer;
      margin-top: 15px;
    }

    .download-btn:hover {
      background-color: #28a745;
    }

    .reaction {
      font-size: 16px;
      margin-top: 8px;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <h2>iMessage Generator - iOS 16/17</h2>

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

      // Add emoji reactions (as in iOS)
      const reactions = document.createElement("div");
      reactions.className = "reaction";
      reactions.innerHTML = "👍 ❤️ 😄";
      msg.appendChild(reactions);

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
        link.download = "fake-imessage-ios16.png";
        link.href = canvas.toDataURL();
        link.click();
      });
    }

    // Initialize time when page loads
    updateTime();
  </script>

</body>
</html>
