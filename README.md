# Love
<!DOCTYPE html>
<html lang="th">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>บอกรักแฟน 💖</title>
<style>
  body {
    margin: 0;
    overflow: hidden;
    background: black;
    font-family: Arial, sans-serif;
  }
  .floating-text {
    position: absolute;
    color: #ff69b4;
    font-size: 5vw; /* ขนาด responsive ตามความกว้างหน้าจอ */
    text-shadow: 0 0 15px #ff00ff;
    pointer-events: none;
    white-space: nowrap;
    user-select: none;
    transition: transform 0.1s linear, opacity 1s;
  }
  .heart {
    position: absolute;
    width: 20px;
    height: 20px;
    background: red;
    transform: rotate(0deg); /* แนวตั้ง */
  }
  .heart:before, .heart:after {
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    background: inherit;
    border-radius: 50%;
  }
  .heart:before { top: -50%; left: 0; }
  .heart:after { top: 0; left: 50%; }
  @keyframes float {
    0% { transform: translateY(100vh) translateX(0) rotate(0deg); opacity: 1; }
    100% { transform: translateY(-10vh) translateX(var(--x)) rotate(0deg); opacity: 0; }
  }
</style>
</head>
<body>
<script>
const colors = ["#ff4d4d","#ff1a75","#ff66b3","#ff80aa","#ff3399"];
const messages = [
  "เค้ารักเธอมากๆ 💖",
  "คิดถึงจัง อยากกอด 🤗",
  "หัวใจเค้าทุกดวงเป็นของเธอ ❤️",
  "อยู่ไกลก็รักเหมือนเดิม 😘",
  "เธอคือโลกทั้งใบของเค้า 🌎💗",
  "คิดถึงรอยยิ้มเธอทุกวัน 😊"
];

// สร้างหัวใจ
function createHeart() {
  const heart = document.createElement("div");
  heart.className = "heart";
  heart.style.left = Math.random() * 100 + "vw";
  const size = 10 + Math.random() * 30;
  heart.style.width = heart.style.height = size + "px";
  const color = colors[Math.floor(Math.random() * colors.length)];
  heart.style.background = color;
  const duration = 3 + Math.random() * 5;
  heart.style.animation = `float ${duration}s linear forwards`;
  const xOffset = (Math.random() - 0.5) * 50;
  heart.style.setProperty('--x', xOffset + "px");
  document.body.appendChild(heart);
  setTimeout(() => heart.remove(), duration * 1000);
}

// สร้างข้อความลอย
function createFloatingText() {
  const text = document.createElement("div");
  text.className = "floating-text";
  text.textContent = messages[Math.floor(Math.random() * messages.length)];
  text.style.color = colors[Math.floor(Math.random() * colors.length)];
  text.style.left = Math.random() * 80 + "vw";
  text.style.top = Math.random() * 80 + "vh";
  document.body.appendChild(text);

  const dx = (Math.random() - 0.5) * 1.2;
  const dy = (Math.random() - 0.5) * 1.2;
  let x = parseFloat(text.style.left);
  let y = parseFloat(text.style.top);

  const move = setInterval(() => {
    x += dx;
    y += dy;
    if (x<0) x=0; if (x>90) x=90;
    if (y<0) y=0; if (y>90) y=90;
    text.style.left = x + "vw";
    text.style.top = y + "vh";
  }, 50);

  setTimeout(() => {
    clearInterval(move);
    text.remove();
  }, 6000);
}

setInterval(createHeart, 300);
setInterval(createFloatingText, 500);
</script>
</body>
</html>