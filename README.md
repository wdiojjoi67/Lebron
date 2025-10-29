<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LeBron James - King Broadcast Scoreboard</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@700&display=swap');

body {
    background: radial-gradient(circle at top, #1a1a1a, #000);
    color: #fff;
    font-family: Arial, sans-serif;
    margin:0;
    padding:0;
    overflow-x:hidden;
    position:relative;
}

/* Particle background */
.particle {
    position: absolute;
    border-radius: 50%;
    background: gold;
    opacity: 0.7;
    animation: float 10s linear infinite;
}
@keyframes float {
    0% { transform: translateY(0) translateX(0); opacity: 0.8; }
    50% { opacity: 0.5; }
    100% { transform: translateY(-1200px) translateX(100px); opacity:0; }
}

header {
    text-align:center;
    padding:50px;
    background: linear-gradient(to right, #552583,#FDB927);
    position: relative;
    overflow:hidden;
}
header h1 {
    font-size:3rem;
    color: gold;
    font-family:'Orbitron', sans-serif;
    text-shadow: 0 0 10px #fff;
    animation: glow 2s ease-in-out infinite alternate;
}
@keyframes glow {
    0% { text-shadow: 0 0 10px gold; }
    100% { text-shadow: 0 0 25px #fff; }
}

.crown {
    width: 100px;
    position: absolute;
    top: -30px;
    left: 50%;
    transform: translateX(-50%);
    animation: crown-bounce 1.5s ease-in-out infinite;
}
@keyframes crown-bounce {
    0%,100% { transform: translateX(-50%) translateY(0) rotate(0deg); }
    50% { transform: translateX(-50%) translateY(-15px) rotate(-5deg);}
}

.lebron-img {
    width:120px;
    position:absolute;
    top:50%;
    left:50%;
    transform: translate(-50%,-50%);
    animation: floatImg 3s ease-in-out infinite alternate;
}
@keyframes floatImg {
    0% { transform: translate(-50%, -50%) rotate(0deg); }
    50% { transform: translate(-50%, -55%) rotate(-5deg);}
    100% { transform: translate(-50%, -50%) rotate(0deg);}
}

section {
    padding:50px 20px;
    max-width:700px;
    margin:auto;
    text-align:center;
}

.stats {
    display:flex;
    gap:20px;
    flex-wrap:wrap;
    justify-content:center;
    margin-top:30px;
}
.stat {
    background:rgba(85,37,131,0.7);
    padding:30px;
    border-radius:15px;
    width:150px;
    transition: all 0.4s ease;
    cursor:pointer;
    box-shadow:0 0 10px #000;
    position: relative;
}
.stat:hover {
    transform: scale(1.2) rotate(-2deg);
    background: rgba(253,185,39,0.9);
    color:#000;
    box-shadow: 0 0 35px gold, 0 0 60px #fff;
}
.stat h3 {
    font-size:2.5rem;
    margin-bottom:10px;
    transition: transform 0.3s, text-shadow 0.3s;
}
.stat.glow h3 {
    text-shadow: 0 0 15px gold, 0 0 25px #fff;
}
.stat p {
    font-size:1.2rem;
}
</style>
</head>
<body>

<!-- Particles -->
<script>
for(let i=0;i<60;i++){
    let particle = document.createElement('div');
    particle.classList.add('particle');
    particle.style.width = `${Math.random()*6+4}px`;
    particle.style.height = particle.style.width;
    particle.style.left = `${Math.random()*100}vw`;
    particle.style.top = `${Math.random()*100}vh`;
    particle.style.animationDuration = `${Math.random()*10+5}s`;
    document.body.appendChild(particle);
}
</script>

<header>
    <img src="https://upload.wikimedia.org/wikipedia/commons/0/0e/Crown_icon.png" class="crown" alt="Crown">
    <h1>LeBron James - King Broadcast Scoreboard 👑</h1>
    <img src="https://upload.wikimedia.org/wikipedia/commons/3/33/LeBron_James_Lakers_2022.jpg" alt="LeBron James" class="lebron-img">
</header>

<section>
    <div class="stats">
        <div class="stat" id="points-stat">
            <h3 id="points">0</h3>
            <p>Points</p>
        </div>
        <div class="stat" id="assists-stat">
            <h3 id="assists">0</h3>
            <p>Assists</p>
        </div>
        <div class="stat" id="rebounds-stat">
            <h3 id="rebounds">0</h3>
            <p>Rebounds</p>
        </div>
    </div>
</section>

<script>
const pointsElem = document.getElementById('points');
const assistsElem = document.getElementById('assists');
const reboundsElem = document.getElementById('rebounds');
const pointsStat = document.getElementById('points-stat');
const assistsStat = document.getElementById('assists-stat');
const reboundsStat = document.getElementById('rebounds-stat');

// Animate stat with pop and glow effect
function animateStat(elem, statDiv, target, step=1, interval=50){
    let current = parseInt(elem.textContent);
    const timer = setInterval(() => {
        current += step;
        if(current >= target){
            current = target;
            clearInterval(timer);
        }
        elem.textContent = current;
        statDiv.classList.add('glow');
        elem.style.transform='scale(1.3)';
        setTimeout(() => {
            elem.style.transform='scale(1)';
            statDiv.classList.remove('glow');
        }, 150);
    }, interval);
}

// Simulate live updates
setInterval(()=>{
    animateStat(pointsElem, pointsStat, parseInt(pointsElem.textContent)+Math.floor(Math.random()*3));
    animateStat(assistsElem, assistsStat, parseInt(assistsElem.textContent)+Math.floor(Math.random()*2));
    animateStat(reboundsElem, reboundsStat, parseInt(reboundsElem.textContent)+Math.floor(Math.random()*2));
}, 2000);
</script>

</body>
</html>
