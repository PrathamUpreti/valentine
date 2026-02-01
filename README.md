# valentine
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Be My Valentine 💖</title>

<style>
* { box-sizing: border-box; }

body {
    margin: 0;
    height: 100vh;
    font-family: 'Poppins', sans-serif;
    overflow: hidden;
    background: linear-gradient(135deg, #ff758c, #ff7eb3);
}

/* Title Card */
.card {
    position: absolute;
    top: 25%;
    left: 50%;
    transform: translateX(-50%);
    text-align: center;
    color: white;
    backdrop-filter: blur(10px);
}

h1 {
    font-size: 32px;
    text-shadow: 0 0 10px rgba(255,255,255,0.6);
}

/* Buttons */
button {
    padding: 14px 28px;
    font-size: 16px;
    border: none;
    border-radius: 30px;
    cursor: pointer;
    position: fixed;
    font-weight: bold;
    letter-spacing: 1px;
    transition: all 0.4s ease;
}

/* YES Button Glow */
#yesBtn {
    background: linear-gradient(45deg, #ff4d88, #ff1a66);
    color: white;
    box-shadow: 0 0 15px rgba(255, 0, 100, 0.7);
}

#yesBtn:hover {
    box-shadow: 0 0 25px rgba(255, 0, 100, 1);
}

/* NO Button Soft */
#noBtn {
    background: rgba(255,255,255,0.8);
    color: #444;
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
}

/* 404 Overlay */
#errorScreen {
    position: fixed;
    inset: 0;
    background: rgba(0,0,0,0.75);
    display: none;
    justify-content: center;
    align-items: center;
}

/* 404 Box */
#errorBox {
    background: linear-gradient(145deg, #ffffff, #ffe6ec);
    padding: 40px;
    border-radius: 20px;
    text-align: center;
    box-shadow: 0 0 40px rgba(255, 0, 100, 0.5);
    animation: pop 0.3s ease;
}

#errorBox h2 {
    color: #ff1a66;
    font-size: 60px;
    margin: 0;
}

#errorBox p {
    margin-top: 10px;
    color: #333;
    font-weight: 500;
}

@keyframes pop {
    from { transform: scale(0.7); opacity: 0; }
    to { transform: scale(1); opacity: 1; }
}

/* Sad Emoji */
.sad {
    position: absolute;
    font-size: 24px;
    animation: fall 3s linear forwards;
}

@keyframes fall {
    0% { transform: translateY(0); opacity: 1; }
    100% { transform: translateY(200px); opacity: 0; }
}
</style>
</head>

<body>

<div class="card">
    <h1>Will you be my Valentine? 💖</h1>
</div>

<button id="yesBtn">Yes 😍</button>
<button id="noBtn">No 🙈</button>

<div id="errorScreen">
    <div id="errorBox">
        <h2>404</h2>
        <p>Love Not Found 💔<br>Please try again never 😂</p>
    </div>
</div>

<script>
const yesBtn = document.getElementById("yesBtn");
const noBtn = document.getElementById("noBtn");
const errorScreen = document.getElementById("errorScreen");

function setInitialPositions() {
    const w = window.innerWidth;
    const h = window.innerHeight;
    yesBtn.style.left = (w * 0.7) + "px";
    yesBtn.style.top = (h * 0.65) + "px";
    noBtn.style.left = (w * 0.2) + "px";
    noBtn.style.top = (h * 0.65) + "px";
}
setInitialPositions();

/* Smooth movement + keep distance */
function moveYes(eX, eY) {
    const rect = yesBtn.getBoundingClientRect();
    const noRect = noBtn.getBoundingClientRect();
    const centerX = rect.left + rect.width/2;
    const centerY = rect.top + rect.height/2;
    const distance = Math.hypot(eX - centerX, eY - centerY);

    if (distance < 120) {
        let newX, newY, distFromNo;
        do {
            newX = Math.random() * (window.innerWidth - rect.width);
            newY = Math.random() * (window.innerHeight - rect.height);
            distFromNo = Math.hypot(newX - noRect.left, newY - noRect.top);
        } while (distFromNo < 160);

        yesBtn.style.left = newX + "px";
        yesBtn.style.top = newY + "px";
    }
}

document.addEventListener("mousemove", (e) => moveYes(e.clientX, e.clientY));
document.addEventListener("touchmove", (e) => moveYes(e.touches[0].clientX, e.touches[0].clientY));

yesBtn.addEventListener("click", () => {
    errorScreen.style.display = "flex";
});

noBtn.addEventListener("click", () => {
    for (let i = 0; i < 10; i++) {
        const sad = document.createElement("div");
        sad.innerText = "😢";
        sad.classList.add("sad");
        sad.style.left = Math.random() * window.innerWidth + "px";
        sad.style.top = Math.random() * 200 + "px";
        document.body.appendChild(sad);
    }
});
</script>

</body>
</html>
