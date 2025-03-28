<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HypeCast - AI Podcast Creator</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; background-color: #111; color: white; padding: 20px; }
        textarea { width: 80%; height: 100px; margin-top: 10px; padding: 10px; font-size: 16px; }
        button { background-color: #007bff; color: white; border: none; padding: 10px 20px; font-size: 18px; cursor: pointer; }
        button:hover { background-color: #0056b3; }
    </style>
</head>
<body>
    <h1>🎙️ HypeCast - AI Podcast Generator</h1>
    <textarea id="text" placeholder="Enter podcast script..."></textarea><br>
    <button onclick="generatePodcast()">Generate Podcast</button>
    <audio id="audioPlayer" controls style="display:none; margin-top: 20px;"></audio>

    <script>
        function generatePodcast() {
            let text = document.getElementById("text").value;
            if (!text) { alert("Please enter text!"); return; }

            fetch("http://127.0.0.1:5000/generate", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ text: text })
            })
            .then(response => response.json())
            .then(data => {
                let audioPlayer = document.getElementById("audioPlayer");
                audioPlayer.src = data.audio_url;
                audioPlayer.style.display = "block";
            })
            .catch(error => console.error("Error:", error));
        }
    </script>
</body>
</html>
