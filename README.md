# My--self-
<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Hey Siri</title>

<style>
body {
  background: #101426;
  color: white;
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 35px 15px;
}

h1 {
  font-size: 38px;
}

.orb {
  width: 170px;
  height: 170px;
  margin: 45px auto 35px;
  border-radius: 50%;
  background: linear-gradient(135deg, #00e5ff, #9b4dff, #ff55c8);
  box-shadow: 0 0 45px #754dff;
}

button {
  background: #7657ff;
  color: white;
  border: none;
  border-radius: 28px;
  padding: 15px 28px;
  font-size: 18px;
  margin: 8px;
}

#message {
  font-size: 18px;
  margin-top: 25px;
}
</style>
</head>

<body>

<h1>Hey Siri</h1>
<p>आपकी अपनी Voice Assistant</p>

<div class="orb"></div>

<button onclick="speakHindi()">बोलकर जवाब</button>
<button onclick="listenHindi()">मेरी बात सुनो 🎤</button>

<p id="message">नमस्ते Prem! मैं तैयार हूँ।</p>

<script>
function speakHindi() {
  const message = "नमस्ते Prem! मैं आपकी क्या मदद कर सकती हूँ?";
  document.getElementById("message").innerText = message;

  if (!("speechSynthesis" in window)) {
    document.getElementById("message").innerText =
      "इस Preview में आवाज उपलब्ध नहीं है।";
    return;
  }

  window.speechSynthesis.cancel();

  const voice = new SpeechSynthesisUtterance(message);
  voice.lang = "hi-IN";
  voice.rate = 0.9;

  window.speechSynthesis.speak(voice);
}

function listenHindi() {
  const SpeechRecognition =
    window.SpeechRecognition ||
    window.webkitSpeechRecognition;

  if (!SpeechRecognition) {
    document.getElementById("message").innerText =
      "Voice recognition इस Preview में उपलब्ध नहीं है।";
    return;
  }

  const recognition = new SpeechRecognition();
  recognition.lang = "hi-IN";
  recognition.interimResults = false;

  document.getElementById("message").innerText =
    "मैं सुन रही हूँ... अब बोलिए।";

  recognition.onresult = function(event) {
    const words = event.results[0][0].transcript;
    document.getElementById("message").innerText =
      "आपने कहा: " + words;

    const reply = new SpeechSynthesisUtterance(
      "आपने कहा " + words
    );
    reply.lang = "hi-IN";
    window.speechSynthesis.speak(reply);
  };

  recognition.onerror = function() {
    document.getElementById("message").innerText =
      "माइक की अनुमति जाँचें या दोबारा कोशिश करें।";
  };

  recognition.start();
}
</script>

</body>
</html>
