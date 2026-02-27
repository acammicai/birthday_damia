# birthday_damia
<!DOCTYPE html>
<html>
<head>
<title>Happy Birthday Damia 🌌❤️</title>
<style>
/* Body setup */
body {
    margin:0;
    padding:0;
    overflow:hidden;
    background:black;
    font-family: Arial, sans-serif;
    color:white;
    height:100vh;
    width:100vw;
    position:relative; /* for absolute centering */
}

/* Canvas for stars & fireworks */
canvas {
    position:fixed;
    top:0;
    left:0;
    z-index:0;
    pointer-events:none;
}

/* Glowing text */
h1 {
    font-size:55px;
    animation: glow 2s ease-in-out infinite alternate;
    position: relative;
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
    transition:0.3s;
}
button:hover { transform:scale(1.1); }

/* Container centered */
div.container {
    position:absolute;
    top:50%;
    left:50%;
    transform: translate(-50%, -50%);
    z-index:10; /* above canvas */
    text-align:center;
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
<div class="container">
    <h1>✨ Happy Birthday Damia ✨</h1>
    <button onclick="startParty()">Start Celebration 🎊</button>
</div>

<canvas id="stars"></canvas>

<audio id="music" loop>
    <source src="love.mp3" type="audio/mpeg">
</audio>

<script>
// Canvas setup
const canvas = document.getElementById("stars");
const ctx = canvas.getContext("2d");
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

// Stars
let stars = [];
for(let i=0;i<200;i++){
    stars.push({x:Math.random()*canvas.width,y:Math.random()*canvas.height,size:Math.random()*2,speed:Math.random()*0.5});
}
function drawStars(){
    ctx.clearRect(0,0,canvas.width,canvas.height);
    ctx.fillStyle="white";
    stars.forEach(star=>{
        ctx.beginPath();
        ctx.arc(star.x,star.y,star.size,0,Math.PI*2);
        ctx.fill();
        star.y+=star.speed;
        if(star.y>canvas.height){star.y=0;star.x=Math.random()*canvas.width;}
    });
    requestAnimationFrame(drawStars);
}

// Confetti
function launchConfetti(){
    let pieces=[];
    for(let i=0;i<100;i++){
        pieces.push({x:Math.random()*canvas.width,y:Math.random()*canvas.height,size:Math.random()*6,speed:Math.random()*2+1});
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

// Love emojis around text
function spawnLoveEmojis(){
    const text = document.querySelector("h1");
    setInterval(()=>{
        let love = document.createElement("div");
        love.className="love";
        love.innerHTML="❤️";
        let rect = text.getBoundingClientRect();
        love.style.left = rect.left + rect.width/2 + (Math.random()*200-100) + "px";
        love.style.top = rect.top + (Math.random()*50-25) + "px";
        love.style.animationDuration=(Math.random()*2+2)+"s";
        document.body.appendChild(love);
        setTimeout(()=>love.remove(),4000);
    },300);
}

// Fireworks
let fireworks=[];
function createFirework(){
    let x = Math.random()*canvas.width;
    let y = Math.random()*canvas.height/2;
    for(let i=0;i<30;i++){
        fireworks.push({
            x:x,
            y:y,
            dx:(Math.random()-0.5)*5,
            dy:(Math.random()-0.5)*5,
            color:`hsl(${Math.random()*360},100%,60%)`,
            life:30
        });
    }
}
function drawFireworks(){
    fireworks.forEach((f,i)=>{
        ctx.fillStyle=f.color;
        ctx.beginPath();
        ctx.arc(f.x,f.y,3,0,Math.PI*2);
        ctx.fill();
        f.x+=f.dx; f.y+=f.dy; f.life--;
        if(f.life<=0) fireworks.splice(i,1);
    });
    requestAnimationFrame(drawFireworks);
}

// Start Party
function startParty(){
    document.getElementById("music").play();
    drawStars();
    launchConfetti();
    spawnLoveEmojis();
    setInterval(createFirework,800);
    drawFireworks();
}
</script>
</body>
</html>
