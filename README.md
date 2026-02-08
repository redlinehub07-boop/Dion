# Dino🦕🦖
<!DOCTYPE html>
<html>
<head>
  <title>Dino Game</title>
  <style>
    body {
      margin: 0;
      background: #f7f7f7;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
    canvas {
      background: white;
      border: 2px solid black;
    }
  </style>
</head>
<body>

<canvas id="game" width="800" height="200"></canvas>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

let dino = { x: 50, y: 150, w: 40, h: 40, dy: 0, jump: false };
let cactus = { x: 800, y: 160, w: 20, h: 40 };
let gravity = 0.6;
let score = 0;

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);

  // Dino
  ctx.fillStyle = "black";
  ctx.fillRect(dino.x, dino.y, dino.w, dino.h);

  // Cactus
  ctx.fillRect(cactus.x, cactus.y, cactus.w, cactus.h);

  // Score
  ctx.fillText("Score: " + score, 10, 20);
}

function update() {
  // Jump physics
  dino.y += dino.dy;
  dino.dy += gravity;

  if (dino.y >= 150) {
    dino.y = 150;
    dino.jump = false;
  }

  // Move cactus
  cactus.x -= 5;
  if (cactus.x < 0) {
    cactus.x = canvas.width;
    score++;
  }

  // Collision
  if (
    dino.x < cactus.x + cactus.w &&
    dino.x + dino.w > cactus.x &&
    dino.y < cactus.y + cactus.h &&
    dino.y + dino.h > cactus.y
  ) {
    alert("Game Over! Score: " + score);
    location.reload();
  }
}

function loop() {
  update();
  draw();
  requestAnimationFrame(loop);
}

document.addEventListener("keydown", e => {
  if (e.code === "Space" && !dino.jump) {
    dino.dy = -12;
    dino.jump = true;
  }
});

loop();
</script>

</body>
</html>
