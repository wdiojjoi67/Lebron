<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LeBron James - Live Game Simulation</title>
<style>
    body { background: #000; color: #fff; font-family: Arial, sans-serif; margin:0; padding:0; }
    header { text-align:center; padding:50px; background: linear-gradient(to right, #552583,#FDB927); }
    header h1 { font-size:3rem; color: gold; }
    nav { display:flex; justify-content:center; background:#111; }
    nav a { color:#fff; padding:10px 20px; text-decoration:none; font-weight:bold; }
    nav a:hover { color:#FDB927; }
    section { padding:50px 20px; max-width:900px; margin:auto; }
    .stats { display:flex; gap:20px; flex-wrap:wrap; justify-content:center; }
    .stat { background:rgba(85,37,131,0.7); padding:20px; border-radius:15px; text-align:center; width:200px; }
    .stat h3 { font-size:2rem; margin-bottom:10px; }
    .highlight video { width:100%; margin-top:20px; border-radius:15px; }
</style>
</head>
<body>

<header>
    <h1>LeBron James - Live Game Simulation</h1>
</header>

<nav>
    <a href="#stats">Stats</a>
    <a href="#highlights">Highlights</a>
</nav>

<section id="stats">
    <h2>Game Stats</h2>
    <div class="stats">
        <div class="stat">
            <h3 id="points">0</h3>
            <p>Points</p>
        </div>
        <div class="stat">
            <h3 id="assists">0</h3>
            <p>Assists</p>
        </div>
        <div class="stat">
            <h3 id="rebounds">0</h3>
            <p>Rebounds</p>
        </div>
    </div>
</section>

<section id="highlights">
    <h2>Highlights</h2>
    <video id="clip1" src="https://www.w3schools.com/html/mov_bbb.mp4" muted></video>
</section>

<script>
const pointsElem = document.getElementById('points');
const assistsElem = document.getElementById('assists');
const reboundsElem = document.getElementById('rebounds');

// Simulated scoring events (seconds into the video where LeBron scores)
const scoringEvents = [
    {time: 2, points: 2},
    {time: 5, points: 3},
    {time: 8, points: 2}
];

const video = document.getElementById('clip1');
let currentEventIndex = 0;

video.addEventListener('timeupdate', () => {
    if(currentEventIndex < scoringEvents.length){
        const event = scoringEvents[currentEventIndex];
        if(video.currentTime >= event.time){
            let currentPoints = parseInt(pointsElem.textContent);
            currentPoints += event.points;
            pointsElem.textContent = currentPoints;
            currentEventIndex++;
        }
    }
});
</script>

</body>
</html>
