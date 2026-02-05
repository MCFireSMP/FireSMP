<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FireSMP - Home</title>

<link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><text y=%22.9em%22 font-size=%2290%22>🔥</text></svg>">
<link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@700&display=swap" rel="stylesheet">

<style>
body {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
    background: radial-gradient(circle at top, #2b0000, #000);
    color: white;
    text-align: center;
    overflow-x: hidden;
}

/* NAVBAR */
nav {
    display: flex;
    justify-content: center;
    gap: 25px;
    padding: 15px;
    background: rgba(0,0,0,0.7);
    position: sticky;
    top: 0;
    z-index: 10;
}

nav a {
    color: #ff8533;
    text-decoration: none;
    font-weight: bold;
    transition: 0.3s;
}

nav a:hover {
    color: white;
    text-shadow: 0 0 10px orange;
}

/* EMBERS */
.embers {
    position: fixed;
    width: 100%;
    height: 100%;
    pointer-events: none;
}

.ember {
    position: absolute;
    bottom: -10px;
    width: 6px;
    height: 6px;
    background: orange;
    border-radius: 50%;
    animation: rise 6s infinite ease-in;
}

@keyframes rise {
    from { transform: translateY(0); opacity: 1; }
    to { transform: translateY(-110vh); opacity: 0; }
}

header {
    padding: 50px 20px;
}

.logo {
    max-width: 220px;
    animation: float 4s ease-in-out infinite;
    filter: drop-shadow(0 0 25px orange);
}

@keyframes float {
    50% { transform: translateY(-12px); }
}

h1 {
    font-family: 'Cinzel Decorative', serif;
    font-size: 3.5em;
    color: #ff6600;
    text-shadow: 0 0 20px orange;
}

.info-box {
    background: rgba(0,0,0,0.6);
    padding: 15px 25px;
    border-radius: 10px;
    display: inline-block;
    margin: 10px;
}

button {
    padding: 14px 32px;
    background: #ff6600;
    color: white;
    border: none;
    border-radius: 8px;
    font-size: 1.1em;
    cursor: pointer;
}

button:hover {
    background: #ff8533;
    box-shadow: 0 0 20px orange;
}
</style>
</head>
<body>

<nav>
    <a href="index.html">Home</a>
    <a href="rules.html">Rules</a>
    <a href="support.html">Support</a>
    <a href="https://discord.gg/TkssGARqA2" target="_blank">Discord</a>
</nav>

<div class="embers" id="embers"></div>

<header>
    <img src="phoenix.png" class="logo">
    <h1>FireSMP</h1>

    <div class="info-box">
        Server IP: <strong id="serverIP">firesmp.example.com</strong>
    </div>

    <div class="info-box">
        Players Online: <strong id="playercount">Loading...</strong>
    </div>

    <br>
    <button onclick="copyIP()">📋 Copy Server IP</button>
</header>

<script>
function copyIP() {
    navigator.clipboard.writeText("firesmp.example.com");
    alert("Server IP copied!");
}

fetch("https://api.mcstatus.io/v2/status/java/firesmp.example.com")
.then(res => res.json())
.then(data => {
    document.getElementById("playercount").innerText =
        data.players.online + " / " + data.players.max;
})
.catch(() => {
    document.getElementById("playercount").innerText = "Offline";
});

const embers = document.getElementById("embers");
for (let i = 0; i < 40; i++) {
    const e = document.createElement("div");
    e.className = "ember";
    e.style.left = Math.random() * 100 + "vw";
    e.style.animationDuration = (3 + Math.random() * 4) + "s";
    embers.appendChild(e);
}
</script>

</body>
</html>
