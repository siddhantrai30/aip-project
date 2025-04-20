<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Real-Time Chat</title>
  <link rel="stylesheet" href="/style.css">
</head>
<body>

  <div id="chat-container">
    <h1>Real-Time Chat</h1>

    <div id="messages"></div>

    <input id="message-input" type="text" placeholder="Type a message..." />
    <button id="send-button">Send</button>
  </div>

  <script src="/socket.io/socket.io.js"></script>
  <script>
    const socket = io(); // Connect to the server

    // DOM Elements
    const messageInput = document.getElementById('message-input');
    const sendButton = document.getElementById('send-button');
    const messagesDiv = document.getElementById('messages');

    // Send a message when the Send button is clicked
    sendButton.addEventListener('click', () => {
      const message = messageInput.value;
      if (message.trim() !== '') {
        socket.emit('chat message', message); // Emit message to server
        messageInput.value = ''; // Clear input field
      }
    });

    // Listen for incoming messages and display them
    socket.on('chat message', (msg) => {
      const messageElement = document.createElement('div');
      messageElement.textContent = msg;
      messagesDiv.appendChild(messageElement); // Append message to chat
    });
  </script>

</body>
</html>
