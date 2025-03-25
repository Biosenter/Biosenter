<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Biosensors Enterprise</title>
  <style>
    body {
      margin: 0;
      background: radial-gradient(ellipse at center, #000428, #004e92);
      overflow: hidden;
      height: 100vh;
      font-family: 'Courier New', monospace;
      display: flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      color: #00ff88;
    }

    .stars {
      position: absolute;
      width: 100%;
      height: 100%;
      z-index: 0;
    }

    .star {
      position: absolute;
      background: white;
      border-radius: 50%;
      opacity: 0;
      animation: blink 2s infinite ease-in-out;
    }

    @keyframes blink {
      0%, 100% { opacity: 0; }
      50% { opacity: 1; }
    }

    .intro-container {
      position: relative;
      z-index: 2;
    }

    .intro-text {
      font-size: 2.5rem;
      font-weight: bold;
      color: #00ff88;
      text-shadow: 0 0 15px #00ff88, 0 0 30px #00ff88;
      transition: transform 0.4s ease, opacity 0.5s ease;
    }

    .explode {
      animation: explode 0.6s forwards ease-out;
    }

    @keyframes explode {
      0% { transform: scale(1); opacity: 1; }
      100% { transform: scale(3); opacity: 0; }
    }

    .mist {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 250px;
      height: 250px;
      background: radial-gradient(circle, rgba(255,140,0,0.4) 0%, transparent 70%);
      transform: translate(-50%, -50%);
      border-radius: 50%;
      opacity: 0;
      pointer-events: none;
      z-index: 1;
    }

    .mist.show {
      animation: fadeMist 1.2s forwards ease-out;
    }

    @keyframes fadeMist {
      0% { opacity: 0; transform: translate(-50%, -50%) scale(0.8); }
      100% { opacity: 1; transform: translate(-50%, -50%) scale(1.5); }
    }

    .text-line {
      font-size: 1.5rem;
      text-shadow: 0 0 10px #00ff88, 0 0 20px #00ff88;
      white-space: nowrap;
      z-index: 2;
      margin: 10px 0;
      opacity: 0;
    }

    .text-line.visible {
      opacity: 1;
      transition: opacity 0.4s ease-in;
    }

    .letter {
      display: inline-block;
      opacity: 0;
      position: relative;
    }

    .letter.visible {
      opacity: 1;
      transition: opacity 0.1s ease-in;
    }

    .beam {
      position: absolute;
      top: -60px;
      left: 50%;
      transform: translateX(-50%);
      width: 2px;
      height: 60px;
      background: #00ff88;
      box-shadow: 0 0 10px #00ff88, 0 0 20px #00ff88;
      animation: beamDrop 0.15s ease-out forwards;
      z-index: 3;
    }

    @keyframes beamDrop {
      0% { top: -60px; opacity: 1; }
      100% { top: 0px; opacity: 0; }
    }

    .logo-grid {
      display: grid;
      grid-template-columns: repeat(13, 18px);
      grid-template-rows: repeat(9, 18px);
      gap: 6px;
      margin-top: 40px;
      opacity: 0;
      transform: scale(0.95);
      transition: all 1s ease-out;
      z-index: 2;
    }

    .logo-grid.show {
      opacity: 1;
      transform: scale(1);
    }

    .dot {
      width: 12px;
      height: 12px;
      border-radius: 50%;
      background-color: #111111;
      box-shadow: none;
      transition: background-color 0.3s ease, box-shadow 0.3s ease;
    }

    .dot.red.on {
      background-color: #ff3c00;
      box-shadow: 0 0 6px #ff3c00, 0 0 12px #ff3c00;
    }

    .dot.green.on {
      background-color: #00ff88;
      box-shadow: 0 0 8px #00ff88, 0 0 16px #00ff88;
    }

    .dot.blinking {
      animation: blinkTwice 0.6s ease-in-out 2;
    }

    @keyframes blinkTwice {
      0%, 100% { opacity: 1; }
      25%, 75% { opacity: 0.2; }
      50% { opacity: 1; }
    }

    footer {
      position: absolute;
      bottom: 20px;
      text-align: center;
      color: #00ff88;
      font-size: 0.9rem;
      text-shadow: 0 0 5px #00ff88;
      z-index: 3;
    }

    footer a {
      color: #00ff88;
      text-decoration: none;
    }

    footer a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>

  <div class="stars" id="stars"></div>

  <!-- BIOSENTER Explosion -->
  <div class="intro-container">
    <div class="intro-text" id="intro">BIOSENTER</div>
    <div class="mist" id="mist"></div>
  </div>

  <!-- Laser Sentence -->
  <div class="text-line" id="line1"></div>
  <div class="text-line" id="line2"></div>

  <!-- BE Logo -->
  <div class="logo-grid" id="logoGrid"></div>

  <!-- Footer -->
  <footer>
    <div>Contact: <a href="mailto:biosensorsenterprise@gmail.com">biosensorsenterprise@gmail.com</a></div>
    <div>© 2025 Biosensors Enterprise. All rights reserved.</div>
  </footer>

  <script>
    // 🌌 Starfield
    const starsContainer = document.getElementById("stars");
    for (let i = 0; i < 300; i++) {
      const star = document.createElement("div");
      star.classList.add("star");
      const size = Math.random() * 2 + 1;
      star.style.width = `${size}px`;
      star.style.height = `${size}px`;
      star.style.top = `${Math.random() * 100}%`;
      star.style.left = `${Math.random() * 100}%`;
      star.style.animationDuration = `${Math.random() * 3 + 2}s`;
      starsContainer.appendChild(star);
    }

    const intro = document.getElementById("intro");
    const mist = document.getElementById("mist");
    const line1 = document.getElementById("line1");
    const line2 = document.getElementById("line2");

    const lines = [
      "Biosensors Enterprise",
      "A Revolution in Point-of-Care Diagnostics"
    ];

    const containers = [line1, line2];
    let lineIndex = 0;
    let charIndex = 0;

    function writeNextLetter() {
      const line = lines[lineIndex];
      const container = containers[lineIndex];

      if (charIndex === 0) {
        container.classList.add("visible");
      }

      if (charIndex < line.length) {
        const span = document.createElement("span");
        span.classList.add("letter");
        span.innerHTML = line[charIndex] === ' ' ? '&nbsp;' : line[charIndex];
        container.appendChild(span);

        const beam = document.createElement("div");
        beam.classList.add("beam");
        span.appendChild(beam);

        setTimeout(() => {
          span.classList.add("visible");
        }, 100);

        charIndex++;
        setTimeout(writeNextLetter, 75);
      } else if (lineIndex < lines.length - 1) {
        lineIndex++;
        charIndex = 0;
        setTimeout(writeNextLetter, 300);
      } else {
        // After typing, show logo
        setTimeout(() => {
          document.getElementById("logoGrid").classList.add("show");
          blinkDotsRandomly();
        }, 1000);
      }
    }

    // 💥 BIOSENTER explosion
    setTimeout(() => {
      intro.classList.add("explode");
      mist.classList.add("show");

      setTimeout(() => {
        intro.style.display = "none";
        writeNextLetter();
      }, 700);
    }, 2000);

    // 🧩 BE Logo Matrix
    const pattern = [
      [0,0,0,0,0,0,0,0,0,0,0,0,0],
      [0,1,1,1,1,0, 0,1,1,1,1,1,0],
      [0,1,0,0,0,1, 0,1,0,0,0,0,0],
      [0,1,0,0,0,1, 0,1,0,0,0,0,0],
      [0,1,1,1,1,0, 0,1,1,1,1,0,0],
      [0,1,0,0,0,1, 0,1,0,0,0,0,0],
      [0,1,0,0,0,1, 0,1,0,0,0,0,0],
      [0,1,1,1,1,0, 0,1,1,1,1,1,0],
      [0,0,0,0,0,0,0,0,0,0,0,0,0]
    ];

    const grid = document.getElementById("logoGrid");
    const dots = [];

    for (let r = 0; r < pattern.length; r++) {
      for (let c = 0; c < pattern[0].length; c++) {
        const dot = document.createElement("div");
        dot.classList.add("dot");
        if (pattern[r][c] === 1) {
          dot.classList.add("green");
        } else {
          dot.classList.add("red");
        }
        grid.appendChild(dot);
        dots.push(dot);
      }
    }

    function blinkDotsRandomly() {
      const shuffled = [...dots].sort(() => Math.random() - 0.5);
      let i = 0;
      const interval = setInterval(() => {
        if (i >= shuffled.length) {
          clearInterval(interval);
        } else {
          const dot = shuffled[i];
          dot.classList.add("blinking");
          setTimeout(() => {
            dot.classList.add("on");
            dot.classList.remove("blinking");
          }, 600);
          i++;
        }
      }, 80);
    }
  </script>

</body>
</html>

