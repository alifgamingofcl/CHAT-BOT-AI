# CHAT-BOT-AI
POWERED BY VEVO
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatbot Interface</title>
    <style>
        body { font-family: Arial, sans-serif; }
        #chatbox {
            width: 100%;
            height: 300px;
            border: 1px solid #ccc;
            padding: 10px;
            overflow-y: auto;
        }
        #input {
            width: 80%;
            padding: 10px;
        }
        #sendButton {
            padding: 10px;
            background-color: #007BFF;
            color: white;
            border: none;
            cursor: pointer;
        }
        #sendButton:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>

    <h1>Chat with AI</h1>
    <div id="chatbox"></div>
    <input type="text" id="input" placeholder="Type your message...">
    <button id="sendButton">Send</button>

    <script>
        document.getElementById('sendButton').onclick = async function () {
            let inputText = document.getElementById('input').value;
            if (inputText.trim() !== "") {
                let chatbox = document.getElementById('chatbox');
                chatbox.innerHTML += `<div><strong>You:</strong> ${inputText}</div>`;
                document.getElementById('input').value = ''; // Clear the input field

                // You can replace this with an API call to your backend that communicates with OpenAI's API
                // Example with mock response
                let responseText = await getChatbotResponse(inputText);
                chatbox.innerHTML += `<div><strong>AI:</strong> ${responseText}</div>`;
                chatbox.scrollTop = chatbox.scrollHeight; // Scroll to the bottom
            }
        }

        async function getChatbotResponse(inputText) {
            // Placeholder for API call, here we simulate a response from the chatbot
            return new Promise((resolve) => {
                setTimeout(() => {
                    resolve(`This is a mock response for: ${inputText}`);
                }, 1000);
            });
        }
    </script>

</body>
</html>
async function getChatbotResponse(inputText) {
    const response = await fetch("https://api.openai.com/v1/chat/completions", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            "Authorization": "Bearer YOUR_API_KEY"
        },
        body: JSON.stringify({
            model: "gpt-3.5-turbo",
            messages: [{"role": "user", "content": inputText}]
        })
    });

    const data = await response.json();
    return data.choices[0].message.content;
}
