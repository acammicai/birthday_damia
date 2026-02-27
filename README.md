# birthday_damia
happy birthdayy damia
<!DOCTYPE html>
<html>
<head>
<title>Happy Birthday Damiaaa 🌌❤️</title>
<style>
/* Body setup */
body {
    margin:0;
    padding:0;
    overflow:hidden;
    background:black;
    font-family: Arial, sans-serif;
    color:white;
    display:flex;
    justify-content:center;
    align-items:center;
    height:100vh;
    text-align:center;
}

/* Canvas for stars & confetti */
canvas {
    position:fixed;
    top:0;
    left:0;
    z-index:0;            /* behind everything */
    pointer-events:none;   /* clicks pass through */
}

/* Glowing text */
h1 {
    font-size:55px;
    z-index:1;
    animation: glow 2s ease-in-out infinite alternate;
}

@keyframes glow {
    from { text-shadow: 0 0 10px #fff; }
    to { text-shadow: 0 0 30px #ff69b4; }
}

/* Button styling */
button {
    margin-top:20px;
    padding:12px 25px;
    font-size:18px;
    border:none;
    border-radius:20px;
    cursor:pointer;
    background:#ff69b4;
    color:white;
    z-index:1;
    transition:0.3s;
}
button:hover {
    transform:scale(1.1);
}

/* Container above canvas */
div.container {
    position: relative;
    z-index:10; /* above canvas */
}

/* Love emoji animation */
.love {
    position:absolute;
    font-size:25px;
    animation: floatUp linear infinite;
}

@keyframes floatUp {
    from { transform: translateY(100vh) scale(1); opacity:1; }
    to { transform: translateY(-50px) scale(1.5); opacity:0; }
}
</style>
</head>

<body>

<!-- Text + button container -->
<div class="container">
    <h1>✨ Happy Birthday Damiaaa ✨</h1>
    <button onclick="startParty()">Start Celebration 🎊</button>
</div>

<!-- Canvas for stars & confetti -->
<canvas id="stars"></canvas>

<!-- Music -->
<audio id="music" loop>
    <source src="love.mp3" type="audio/mpeg">
</audio>

<script>
// Button function
function startParty(){
    document.getElementById("music").play();
    drawStars();
    launchConfetti();
    spawnLoveEmojis();
}

/* Night Sky Stars */
const canvas = document.getElementById("stars");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;
let stars = [];
for(let i=0;i<200;i++){
    stars.push({
        x:Math.random()*canvas.width,
        y:Math.random()*canvas.height,
        size:Math.random()*2,
        speed:Math.random()*0.5
    });
}
function drawStars(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle="white";
    stars.forEach(star=>{
        ctx.beginPath();
        ctx.arc(star.x,star.y,star.size,0,Math.PI*2);
        ctx.fill();
        star.y+=star.speed;
        if(star.y>canvas.height){
            star.y=0;
            star.x=Math.random()*canvas.width;
        }
    });
    requestAnimationFrame(drawStars);
}

/* Confetti */
function launchConfetti(){
    let pieces = [];
    for(let i=0;i<100;i++){
        pieces.push({
            x:Math.random()*canvas.width,
            y:Math.random()*canvas.height,
            size:Math.random()*6,
            speed:Math.random()*2+1
        });
    }
    function drawConfetti(){
        pieces.forEach(p=>{
            ctx.fillStyle="pink";
            ctx.fillRect(p.x,p.y,p.size,p.size);
            p.y+=p.speed;
            if(p.y>canvas.height)p.y=0;
        });
        requestAnimationFrame(drawConfetti);
    }
    drawConfetti();
}

/* Love emojis */
function spawnLoveEmojis(){
    setInterval(()=>{
        let love = document.createElement("div");
        love.className="love";
        love.innerHTML="❤️";
        love.style.left=Math.random()*100+"vw";
        love.style.animationDuration=(Math.random()*2+2)+"s";
        document.body.appendChild(love);
        setTimeout(()=>love.remove(),4000);
    },300);
}
</script>

</body>
</html>
