
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>ChatGPT Formulaire IA</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      padding: 40px;
    }
    .chat-container {
      max-width: 600px;
      margin: auto;
      background: #fff;
      padding: 20px;
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    input, button {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      font-size: 16px;
    }
    #response {
      margin-top: 20px;
      background: #e6f7ff;
      padding: 15px;
      border-left: 4px solid #1890ff;
    }
  </style>
</head>
<body>
  <div class="chat-container">
    <h2>Pose ta question à ChatGPT</h2>
    <input type="text" id="userInput" placeholder="Ex: Quel est le sens de la vie ?">
    <button onclick="askChatGPT()">Envoyer</button>
    <div id="response"></div>
  </div>

  <script>
    async function askChatGPT() {
      const userInput = document.getElementById("userInput").value;
      const responseDiv = document.getElementById("response");

      responseDiv.innerHTML = "⏳ Chargement...";

      const apiKey = "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"; // ⚠️ Ne PAS utiliser en production côté client

      try {
        const response = await fetch("https://api.openai.com/v1/chat/completions", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
            "Authorization": `Bearer ${apiKey}`
          },
          body: JSON.stringify({
            model: "gpt-3.5-turbo",
            messages: [{ role: "user", content: userInput }]
          })
        });

        const data = await response.json();
        const message = data.choices[0].message.content;
        responseDiv.innerHTML = `<strong>Réponse :</strong><br>${message}`;
      } catch (error) {
        responseDiv.innerHTML = "❌ Une erreur est survenue : " + error.message;
      }
    }
  </script>
</body>
</html>
