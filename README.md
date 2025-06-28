<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>تعريف أحمد - هاكر ستايل</title>
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css"
  />
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');

    /* خلفية أرقام متحركة */
    body {
      margin: 0;
      height: 100vh;
      background: black;
      overflow: hidden;
      font-family: 'Share Tech Mono', monospace;
      color: #22ff00;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    /* كود مصفوفة رقمية */
    .matrix {
      position: fixed;
      top: 0; left: 0; right: 0; bottom: 0;
      pointer-events: none;
      z-index: 0;
      font-size: 14px;
      line-height: 1.2;
      color: #22ff00;
      user-select: none;
      animation: flicker 3s infinite alternate;
    }

    @keyframes flicker {
      0%, 100% {opacity: 0.7;}
      50% {opacity: 1;}
    }

    /* انشاء أعمدة أرقام من الJS */

    /* الكارد */
    .card {
      position: relative;
      z-index: 1;
      width: 320px;
      background: rgba(0, 0, 0, 0.85);
      border: 1px solid #22ff00;
      border-radius: 10px;
      padding: 25px;
      box-sizing: border-box;
      box-shadow: 0 0 20px #22ff00aa;
      backdrop-filter: blur(10px);
      color: #22ff00;
    }

    .titlebar {
      font-family: 'Share Tech Mono', monospace;
      font-size: 28px;
      font-weight: 700;
      background: #003300;
      padding: 12px 0;
      text-align: center;
      border-radius: 6px;
      box-shadow: 0 0 15px #22ff00;
      letter-spacing: 2px;
      animation: glow 2.5s ease-in-out infinite alternate;
    }

    @keyframes glow {
      0% {
        text-shadow: 0 0 8px #22ff00aa, 0 0 20px #22ff00bb;
      }
      100% {
        text-shadow: 0 0 18px #22ff00ff, 0 0 30px #22ff00ff;
      }
    }

    .info-item {
      display: flex;
      align-items: center;
      gap: 15px;
      margin: 20px 0;
      font-size: 20px;
      cursor: default;
      animation: pulse 3s ease-in-out infinite;
    }

    @keyframes pulse {
      0%, 100% {
        color: #22ff00;
        text-shadow: 0 0 5px #22ff00;
      }
      50% {
        color: #aaffaa;
        text-shadow: 0 0 15px #aaffaa;
      }
    }

    .info-item i {
      font-size: 30px;
      width: 40px;
      text-align: center;
      color: #22ff00;
      animation: iconGlow 4s ease-in-out infinite;
    }

    @keyframes iconGlow {
      0%, 100% {
        filter: drop-shadow(0 0 6px #22ff00);
      }
      50% {
        filter: drop-shadow(0 0 15px #aaffaa);
      }
    }

    .telegram-link {
      color: #22ff00;
      text-decoration: none;
      font-weight: bold;
    }

    .telegram-link:hover {
      color: #aaffaa;
      text-decoration: underline;
      text-shadow: 0 0 8px #aaffaa;
    }
  </style>
</head>
<body>
  <canvas id="matrix"></canvas>

  <div class="card">
    <div class="titlebar">تعريف أحمد</div>

    <div class="info-item">
      <i class="fa-solid fa-user"></i>
      <span>الاسم: Ahmed</span>
    </div>

    <div class="info-item">
      <i class="fa-solid fa-code"></i>
      <span>الهواية: Programming</span>
    </div>

    <div class="info-item">
      <i class="fa-solid fa-flag-iraq"></i>
      <span>الدولة: Iraq</span>
    </div>

    <div class="info-item">
      <i class="fa-brands fa-telegram"></i>
      <a href="https://t.me/hoopis_6" target="_blank" class="telegram-link">@hoopis_6</a>
    </div>
  </div>

  <script>
    // كود الـ Matrix background

    const canvas = document.getElementById('matrix');
    const ctx = canvas.getContext('2d');

    // ضبط حجم الكانفس مع تغيير حجم النافذة
    let width = canvas.width = window.innerWidth;
    let height = canvas.height = window.innerHeight;

    // حروف وأرقام تظهر بالخلفية
    const letters = '01';

    const fontSize = 16;
    const columns = Math.floor(width / fontSize);

    // مصفوفة لارتفاع كل عمود (تمثل كم تتقدم الحروف)
    const drops = [];
    for(let x = 0; x < columns; x++) drops[x] = Math.random() * height;

    function draw() {
      // خلفية شفافة مع تأثير تلاشي
      ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
      ctx.fillRect(0, 0, width, height);

      ctx.fillStyle = '#22ff00';
      ctx.font = fontSize + 'px monospace';

      for(let i = 0; i < columns; i++) {
        // نختار حرف عشوائي
        const text = letters.charAt(Math.floor(Math.random() * letters.length));
        // نرسمه في العمود الحالي عند موقع drops[i]
        ctx.fillText(text, i * fontSize, drops[i] * fontSize);

        // زيادة ارتفاع الحرف لأعلى العمود
        drops[i]++;

        // إعادة تعيين العمود إذا خرج خارج الشاشة
        if(drops[i] * fontSize > height && Math.random() > 0.975) {
          drops[i] = 0;
        }
      }
    }

    setInterval(draw, 50);

    // ضبط الكانفس مع تغيير حجم النافذة
    window.addEventListener('resize', () => {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    });
  </script>
</body>
</html>
