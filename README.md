<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Sports Brainrot Dictionary – Top 10 Players</title>
<style>
:root { --bg:#071021; --accent:#00ffd1; --gold:#FFD700; --card:#0f1230; --text:#eaf2ff; --muted:#9aa8c9;}
body { margin:0; font-family:sans-serif; background:var(--bg); color:var(--text);}
.container { max-width:1200px; margin:20px auto; padding:20px;}
h1 { font-size:28px; margin-bottom:20px; text-align:center; }

.section { margin-bottom:20px; border:1px solid rgba(255,255,255,0.1); border-radius:10px; overflow:hidden;}
.section-header { padding:16px; cursor:pointer; background:rgba(0,255,209,0.05); display:flex; justify-content:space-between; align-items:center; font-size:20px; font-weight:600; transition:background 0.3s ease;}
.section-header:hover { background:rgba(0,255,209,0.15);}
.section-body { display:grid; grid-template-columns:repeat(auto-fit,minmax(280px,1fr)); gap:15px; padding:15px; max-height:1000px; overflow:hidden; transition:max-height 0.5s ease, padding 0.5s ease; }
.section.collapsed .section-body { max-height:0; padding:0; }

.card { background:var(--card); padding:15px; border-radius:10px; border:1px solid rgba(255,255,255,0.12); cursor:pointer; position:relative;
  transition: transform 0.3s ease, box-shadow 0.3s ease, border 0.3s ease;}
.card:hover { transform:translateY(-6px) scale(1.02); box-shadow:0 12px 35px rgba(0,255,209,0.4); border-color:var(--accent);}
.card.favorite { border:2px solid var(--gold); box-shadow:0 0 15px var(--gold);}

.favorite-btn { position:absolute; top:10px; right:10px; cursor:pointer; font-size:22px; color:rgba(255,255,255,0.3); transition: color 0.4s ease, transform 0.3s ease;}
.favorite-btn:hover { color:var(--gold); transform:scale(1.3); }

.player-name { font-weight:700; font-size:18px; margin-bottom:6px;}
.jersey-number { font-weight:600; font-size:15px; color:var(--accent); margin-bottom:8px;}
.definition { font-size:14px; color:var(--muted); margin-bottom:8px;}
.stats { font-size:13px; color:var(--muted); max-height:0; overflow:hidden; transition:max-height 0.5s ease, opacity 0.5s ease; opacity:0;}
.card.expanded .stats { max-height:300px; opacity:1; }
</style>
</head>
<body>
<div class="container">
<h1>Sports Brainrot Dictionary – Top 10 Players</h1>
<div class="sections" id="sections"></div>
</div>
<script>
const DATA = {
  basketball: [
    {name:"LeBron James", jersey:6, desc:"NBA legend • 4× MVP", stats:"Career avg: 27.1 pts, 7.5 reb, 7.4 ast • All-time leading scorer"},
    {name:"Stephen Curry", jersey:30, desc:"3-point genius • 2× MVP", stats:"2× MVP • 4× NBA champion"},
    {name:"Kevin Durant", jersey:7, desc:"Elite scorer", stats:"Career PPG ~27 • 2× NBA champ • 2014 MVP"},
    {name:"Giannis Antetokounmpo", jersey:34, desc:"Greek Freak • 2× MVP", stats:"2× MVP • 2021 NBA champion"},
    {name:"Kobe Bryant", jersey:24, desc:"5× NBA champion", stats:"33,643 career pts • 5× NBA champ • 2008 MVP"},
    {name:"Michael Jordan", jersey:23, desc:"GOAT • 6× NBA champion", stats:"32,292 career pts • 6× NBA champ • 5× MVP"},
    {name:"Shaquille O'Neal", jersey:34, desc:"Dominant center", stats:"28,596 career pts • 4× NBA champ • 3× Finals MVP"},
    {name:"Tim Duncan", jersey:21, desc:"The Big Fundamental", stats:"5× NBA champ • 2× MVP • 15× All‑NBA"},
    {name:"James Harden", jersey:13, desc:"Scoring wizard", stats:"2018 MVP • Multiple scoring titles"},
    {name:"Anthony Davis", jersey:3, desc:"Elite big man", stats:"1× NBA champ • Multiple All‑Star selections"}
  ],
  football: [
    {name:"Tom Brady", jersey:12, desc:"Legendary QB • 7× Super Bowl champ", stats:"624 TDs, 89,214 passing yards"},
    {name:"Patrick Mahomes", jersey:15, desc:"Dynamic QB • 2× MVP", stats:"2022 Super Bowl champ • 21-7 playoff record"},
    {name:"Aaron Rodgers", jersey:12, desc:"Precision QB • 4× MVP", stats:"4× MVP • 420 TDs"},
    {name:"Derrick Henry", jersey:22, desc:"Power RB", stats:"2× rushing champ • 2020 Offensive Player of the Year"},
    {name:"DeAndre Hopkins", jersey:10, desc:"Elite WR", stats:"Multiple All-Pro • 1,500+ yard season"},
    {name:"Aaron Donald", jersey:99, desc:"Defensive monster", stats:"3× Defensive Player of the Year"},
    {name:"Drew Brees", jersey:9, desc:"All-time passing leader", stats:"80,358 passing yards • 571 TDs"},
    {name:"J.J. Watt", jersey:99, desc:"Pass rusher extraordinaire", stats:"3× Defensive Player of the Year"},
    {name:"Tyreek Hill", jersey:10, desc:"Speed demon WR", stats:"Multiple 1,400+ yard seasons"},
    {name:"Travis Kelce", jersey:87, desc:"Elite TE", stats:"1,400+ receiving yards • 2× All-Pro"}
  ],
  soccer: [
    {name:"Lionel Messi", jersey:10, desc:"GOAT • 7× Ballon d'Or", stats:"700+ career goals • Multiple Champions League wins"},
    {name:"Cristiano Ronaldo", jersey:7, desc:"Goal machine • 5× Ballon d'Or", stats:"800+ career goals • Multiple Champions League wins"},
    {name:"Neymar Jr.", jersey:10, desc:"Skillful forward • Brazil", stats:"400+ career goals • 3× Champions League winner"},
    {name:"Kylian Mbappe", jersey:7, desc:"Young superstar • France", stats:"200+ career goals • 2022 World Cup winner"},
    {name:"Kevin De Bruyne", jersey:17, desc:"Midfield maestro • Belgium", stats:"Multiple Premier League assists leader"},
    {name:"Robert Lewandowski", jersey:9, desc:"Prolific striker • Poland", stats:"500+ career goals • Multiple Bundesliga titles"},
    {name:"Virgil van Dijk", jersey:4, desc:"Top defender • Netherlands", stats:"Premier League champion • Defensive anchor"},
    {name:"Sergio Ramos", jersey:4, desc:"Elite defender • Spain", stats:"World Cup winner • 4× Champions League winner"},
    {name:"Luka Modric", jersey:10, desc:"Midfield genius • Croatia", stats:"2018 Ballon d'Or winner • 5× Champions League winner"},
    {name:"Mohamed Salah", jersey:11, desc:"Egyptian speedster • Liverpool", stats:"Premier League Golden Boot • Multiple 20+ goal seasons"}
  ],
  baseball: [
    {name:"Babe Ruth", jersey:3, desc:"Legendary slugger • Yankees", stats:"714 career HRs • 7× World Series champ"},
    {name:"Willie Mays", jersey:24, desc:"The Say Hey Kid", stats:"660 career HRs • 24× All-Star"},
    {name:"Hank Aaron", jersey:44, desc:"Home run king", stats:"755 career HRs • 25× All-Star"},
    {name:"Derek Jeter", jersey:2, desc:"Yankees SS • Captain", stats:"14× All-Star • 5× World Series champ"},
    {name:"Cal Ripken Jr.", jersey:8, desc:"Iron Man • SS", stats:"2× MVP • 19× All-Star"},
    {name:"Barry Bonds", jersey:25, desc:"Power & discipline", stats:"762 career HRs • 7× MVP"},
    {name:"Alex Rodriguez", jersey:13, desc:"Prolific 3B/SS", stats:"696 career HRs • 3× MVP"},
    {name:"Ken Griffey Jr.", jersey:24, desc:"Smooth swing • CF", stats:"630 career HRs • 13× All-Star"},
    {name:"Mickey Mantle", jersey:7, desc:"Switch-hitting legend", stats:"536 career HRs • 7× World Series champ"},
    {name:"Roger Clemens", jersey:21, desc:"Dominant pitcher", stats:"354 wins • 4× Cy Young Award"}
  ]
};

// Render sections
const sectionsEl = document.getElementById('sections');
Object.keys(DATA).forEach(sport=>{
  const section = document.createElement('div');
  section.classList.add('section');
  section.innerHTML = `
    <div class="section-header">
      <span>${sport.charAt(0).toUpperCase()+sport.slice(1)} (${DATA[sport].length})</span>
    </div>
    <div class="section-body">
      ${DATA[sport].map(p=>`
        <div class="card">
          <div class="favorite-btn">&#9733;</div>
          <div class="player-name">${p.name}</div>
          <div class="jersey-number">#${p.jersey}</div>
          <div class="definition">${p.desc}</div>
          <div class="stats">${p.stats}</div>
        </div>
      `).join('')}
    </div>
  `;
  sectionsEl.appendChild(section);
  section.querySelector('.section-header').addEventListener('click',()=>section.classList.toggle('collapsed'));
});

// Card interactions
document.querySelectorAll('.card').forEach(card=>{
  const fav = card.querySelector('.favorite-btn');
  fav.addEventListener('click', e=>{ e.stopPropagation(); card.classList.toggle('favorite'); });
  card.addEventListener('click', ()=>card.classList.toggle('expanded'));
});
</script>
</body>
</html>
