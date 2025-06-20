
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Chat IA Gratuit (OpenRouter)</title>
  <style>
    body {
      background-color: #1c1c2b;
      font-family: Arial, sans-serif;
      color: white;
      max-width: 800px;
      margin: auto;
      padding: 20px;
    }
    h1 {
      text-align: center;
      color: #4caf50;
    }
    #chat {
      background: #2c2c3e;
      padding: 15px;
      border-radius: 10px;
      min-height: 200px;
      max-height: 400px;
      overflow-y: auto;
    }
    .message {
      margin: 10px 0;
    }
    .user { color: #00bfff; }
    .bot { color: #7fff00; }
    #inputArea {
      display: flex;
      gap: 10px;
      margin-top: 20px;
    }
    #prompt {
      flex: 1;
      padding: 10px;
      border-radius: 5px;
      border: none;
    }
    #send {
      background: #4caf50;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <h1>Chat IA Gratuit</h1>
  <div id="chat"></div>
  <div id="inputArea">
    <input type="text" id="prompt" placeholder="Pose une question..." />
    <button id="send">Envoyer</button>
  </div>

  <script>
    const chat = document.getElementById("chat");
    const promptInput = document.getElementById("prompt");
    const sendButton = document.getElementById("send");

    const API_KEY = "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"; // Mets ta vraie clé ici
    const MODEL = "mistral/mistral-7b-instruct"; // Ou un autre modèle dispo

    function addMessage(role, content) {
      const div = document.createElement("div");
      div.className = "message " + role;
      div.textContent = (role === "user" ? "👤" : "🤖") + " " + content;
      chat.appendChild(div);
      chat.scrollTop = chat.scrollHeight;
    }

    async function sendPrompt() {
      const prompt = promptInput.value.trim();
      if (!prompt) return;
      addMessage("user", prompt);
      promptInput.value = "";

      try {
        const response = await fetch("https://openrouter.ai/api/v1/chat/completions", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${API_KEY}`,
            "HTTP-Referer": "https://ton-site.exemple.com", // ← Mets l'URL de ton site ici
          },
          body: JSON.stringify({
            model:'gpt-3.5-turbo',
            prompt:userinput,
            max_tokens:150,
            messages: [{ role: "user", content: prompt }],
          }),
        });

        const data = await response.json();
        const reply = data.choices?.[0]?.message?.content || "(Pas de réponse)";
        addMessage("bot", reply);
      } catch (err) {
        console.error(err);
        addMessage("bot", "[Erreur API ou réseau]");
      }
    }

    sendButton.onclick = sendPrompt;
    promptInput.addEventListener("keydown", e => {
      if (e.key === "Enter") sendPrompt();
    });
  </script>
</body>
</html>

    function addMessage(role, text) {
      const d = document.createElement('div');
      d.className = `msg ${role}`;
      d.textContent = text;
      chatEl.appendChild(d);
    }

    function addCitation(url) {
      const c = document.createElement('div');
      c.className = 'citation';
      c.textContent = '🔗 ' + url;
      chatEl.appendChild(c);
    }
  </script>
</body>
</html>

