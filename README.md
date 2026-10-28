# Drive-_Arena
index.html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">

<title>Drive Arena</title>

style.css
</head>

<body>

<div id="gameHud">

    <div id="playerHud">
        <h3>🚗 Buggy</h3>

        <div class="statRow">
            <span>🛡</span>
            <div class="miniBar">
                <div id="playerShield"
                class="shieldFill"></div>
            </div>
        </div>

        <div class="statRow">
            <span>❤️</span>
            <div class="miniBar">
                <div id="playerHealth"
                class="healthFill"></div>
            </div>
        </div>
    </div>

    <div id="centerHud">
        <div id="timer">1:30</div>
        <button id="startBtn">
            Start Match
        </button>
    </div>

    <div id="enemyHud">
        <h3>🏎 Racer</h3>

        <div class="statRow">
            <span>🛡</span>
            <div class="miniBar">
                <div id="enemyShield"
                class="shieldFill"></div>
            </div>
        </div>

        <div class="statRow">
            <span>❤️</span>
            <div class="miniBar">
                <div id="enemyHealth"
                class="healthFill"></div>
            </div>
        </div>
    </div>

</div>

<canvas id="game"></canvas>

game.jsscript>

</body>
</html>
style.css
body{
    margin:0;
    overflow:hidden;
    background:#111;
    color:white;
    font-family:Arial;
}

canvas{
    display:block;
    background:#222;
}

#gameHud{
    position:fixed;
    top:10px;
    left:0;
    right:0;

    display:flex;
    justify-content:space-between;

    padding:10px;

    z-index:10;
}

#playerHud,
#enemyHud{
    width:140px;
}

#centerHud{
    text-align:center;
}

#timer{
    font-size:32px;
    font-weight:bold;
}

#startBtn{
    margin-top:10px;
    padding:10px 20px;
}

.statRow{
    display:flex;
    align-items:center;
    gap:5px;
    margin:4px 0;
}

.miniBar{
    width:90px;
    height:10px;

    background:#333;

    border-radius:4px;

    overflow:hidden;
}

.healthFill{
    width:100%;
    height:100%;
    background:#00cc66;
}

.shieldFill{
    width:100%;
    height:100%;
    background:#33aaff;
}

@media(max-width:600px){

    #playerHud,
    #enemyHud{

        width:100px;

    }

    .miniBar{

        width:70px;

    }

}
game.js
const canvas =
document.getElementById("game");

const ctx =
canvas.getContext("2d");

function resize(){

    canvas.width =
    window.innerWidth;

    canvas.height =
    window.innerHeight;

}

resize();

window.addEventListener(
"resize",
resize
);

let timer = 90;

let countdown = 3;

let matchRunning = false;

let player = {

    x:200,
    y:300,

    health:100,
    shield:50

};

let enemy = {

    x:600,
    y:300,

    health:100,
    shield:50

};

document
.getElementById("startBtn")
.addEventListener(
"click",
startMatch
);

function startMatch(){

    countdown = 3;

    const interval =
    setInterval(()=>{

        document
        .getElementById("timer")
        .textContent =
        countdown;

        countdown--;

        if(countdown < 0){

            clearInterval(
                interval
            );

            matchRunning =
            true;

        }

    },1000);

}

function update(){

    if(matchRunning){

        timer -= 1/60;

        const mins =
        Math.floor(
            timer/60
        );

        const secs =
        Math.floor(
            timer%60
        );

        document
        .getElementById(
        "timer"
        )
        .textContent =

        mins +
        ":" +
        String(secs)
        .padStart(2,"0");

    }

}

function draw(){

    ctx.clearRect(
        0,
        0,
        canvas.width,
        canvas.height
    );

    ctx.fillStyle =
    "dodgerblue";

    ctx.fillRect(
        player.x,
        player.y,
        80,
        30
    );

    ctx.fillStyle =
    "crimson";

    ctx.fillRect(
        enemy.x,
        enemy.y,
        80,
        30
    );

}

function loop(){

    update();

    draw();

    requestAnimationFrame(
        loop
    );

}

loop();
