<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Presente 💖</title>

<style>
body {
    margin: 0;
    background: black;
    overflow: hidden;
    font-family: Arial, sans-serif;
}

/* Tela inicial */
#start {
    position: fixed;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: white;
    background: radial-gradient(circle, #111, #000);
    z-index: 10;
}

#startText {
    font-size: 20px;
    margin-top: 20px;
    animation: pulseText 1.2s infinite;
}

@keyframes pulseText {
    0%,100% { opacity: 0.6; transform: scale(1); }
    50% { opacity: 1; transform: scale(1.08); }
}

/* Coração */
#heart {
    position: absolute;
    top: 58%;
    left: 50%;
    width: 160px;
    height: 160px;
    background: red;
    transform: translate(-50%, -50%) rotate(-45deg);
    display: none;
    animation: beat 1s infinite;
    box-shadow: 0 0 50px red;
}

#heart::before,
#heart::after {
    content: "";
    position: absolute;
    width: 160px;
    height: 160px;
    background: red;
    border-radius: 50%;
}

#heart::before {
    top: -80px;
    left: 0;
}

#heart::after {
    left: 80px;
    top: 0;
}

@keyframes beat {
    0% { transform: translate(-50%, -50%) rotate(-45deg) scale(1); }
    50% { transform: translate(-50%, -50%) rotate(-45deg) scale(1.12); box-shadow: 0 0 90px pink; }
    100% { transform: translate(-50%, -50%) rotate(-45deg) scale(1); }
}

/* Textos */
#mainText {
    position: absolute;
    top: 6%;
    width: 100%;
    text-align: center;
    color: red;
    font-size: 38px;
    display: none;
}

#subText {
    font-size: 18px;
    color: pink;
}

/* Mensagem secreta */
#secret {
    position: absolute;
    bottom: 12%;
    width: 100%;
    text-align: center;
    font-size: 15px;
    color: pink;
    opacity: 0;
    transition: opacity 0.6s;
}

/* Partículas */
.particle {
    position: absolute;
    width: 8px;
    height: 8px;
    background: pink;
    border-radius: 50%;
    opacity: 0.9;
    animation: float 5s linear infinite;
}

@keyframes float {
    from { transform: translateY(100vh) scale(0.5); }
    to { transform: translateY(-10vh) scale(1.2); opacity: 0; }
}

/* Luz toque */
.light {
    position: absolute;
    width: 140px;
    height: 140px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(255,105,180,0.9), transparent);
    pointer-events: none;
    animation: fadeLight 0.6s forwards;
}

@keyframes fadeLight {
    to { opacity: 0; transform: scale(1.6); }
}
</style>
</head>

<body>

<div id="start">
    ❤️
    <div id="startText">Toque para abrir seu presente</div>
</div>

<div id="mainText">
    Je t'aime ❤️
    <div id="subText">Não desista do seu sonho, você consegue 🥰</div>
</div>

<div id="heart"></div>

<div id="secret">
    você é mais incrível do que acha que é,<br>
    acredite em você mesmo,<br>
    só sua força de vontade já é suficiente.
</div>

<!-- Sons -->
<audio id="music" loop preload="auto">
    <source src="https://cdn.pixabay.com/audio/2022/10/03/audio_4c0f7d7b84.mp3">
</audio>

<audio id="beat" preload="auto">
    <source src="https://cdn.pixabay.com/audio/2021/09/06/audio_9e5fa0c7c4.mp3">
</audio>

<audio id="clickSound" preload="auto">
    <source src="https://cdn.pixabay.com/audio/2022/03/10/audio_8b2c1f8f6e.mp3">
</audio>

<script>
const start = document.getElementById("start");
const heart = document.getElementById("heart");
const mainText = document.getElementById("mainText");
const secret = document.getElementById("secret");

const music = document.getElementById("music");
const beat = document.getElementById("beat");
const clickSound = document.getElementById("clickSound");

let beatInterval;

start.addEventListener("click", () => {
    start.style.display = "none";
    heart.style.display = "block";
    mainText.style.display = "block";

    music.volume = 0.4;
    music.play();

    beatInterval = setInterval(() => {
        beat.currentTime = 0;
        beat.volume = 0.8;
        beat.play();
        if (navigator.vibrate) navigator.vibrate(30);
    }, 1000);

    createParticles();
});

heart.addEventListener("click", e => {
    clickSound.currentTime = 0;
    clickSound.volume = 0.8;
    clickSound.play();

    secret.style.opacity = 1;

    const light = document.createElement("div");
    light.className = "light";
    light.style.left = (e.clientX - 70) + "px";
    light.style.top = (e.clientY - 70) + "px";
    document.body.appendChild(light);

    setTimeout(() => light.remove(), 600);
});

function createParticles() {
    setInterval(() => {
        for (let i = 0; i < 3; i++) {
            const p = document.createElement("div");
            p.className = "particle";
            p.style.left = Math.random() * window.innerWidth + "px";
            p.style.animationDuration = (4 + Math.random() * 3) + "s";
            document.body.appendChild(p);
            setTimeout(() => p.remove(), 5000);
        }
    }, 200);
}
</script>

</body>
</html>
