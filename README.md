<html lang="es">
<head>
  <meta charset="UTF-8">
  <title></title> <!-- Esto deja la pestaña vacía -->
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body{
      font-family: Arial, sans-serif;
      background: linear-gradient(180deg,#ffd1dc,#ffe6f0);
      padding: 20px;
      min-height: 100vh;
    }

    .card{
      background:#fff;
      width: 90%;
      max-width: 500px;
      border-radius: 25px;
      padding: 20px;
      text-align: center;
      box-shadow: 0 10px 25px rgba(0,0,0,.15);
      margin: 20px auto;
    }

    h1{
      color:#ff4d6d;
      font-size: 22px;
      margin-bottom: 15px;
    }

    .hidden{
      display: none !important;
    }

    button{
      width: 100%;
      padding: 15px;
      margin: 10px 0;
      border: none;
      border-radius: 30px;
      font-size: 18px;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .yes{
      background:#ff4d6d;
      color: white;
    }

    .no{
      background:#f2f2f2;
      color: #333;
    }

    .option{
      background:#ffe6ee;
      border: 2px solid transparent;
      color: #333;
      margin: 0;
      font-size: 14px;
    }

    .option.selected{
      border-color:#ff4d6d;
      background:#ffd1dc;
      color: #333;
    }

    .confirm-btn{
      background:#ff4d6d;
      color: white;
      margin-top: 20px;
    }

    img{
      width: 100%;
      border-radius: 20px;
      margin: 10px 0;
    }

    .img-container {
      width: 100%;
      height: 120px;
      border-radius: 10px;
      overflow: hidden;
      background-color: #f0f0f0;
    }

    .option-img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: center;
      margin: 0;
      border-radius: 0;
    }

    .floating-love {
      position: fixed;
      bottom: -20px;
      font-size: 40px;
      color: #ff4d6d;
      pointer-events: none;
      z-index: 100;
      animation: floatUp 15s linear forwards;
    }

    @keyframes floatUp {
      to {
        transform: translateY(-90vh);
        opacity: 0;
      }
    }

    .options-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 15px;
      margin-bottom: 20px;
    }

    .option-card {
      background: #fff;
      border: 3px solid #e0e0e0;
      border-radius: 15px;
      padding: 10px;
      text-align: center;
      position: relative;
      transition: all 0.2s ease;
    }

    .option-card.selected {
      border: 3px solid #ff4d6d;
    }

    .check-mark {
      position: absolute;
      top: -12px;
      right: -12px;
      background: #ff4d6d;
      color: #fff;
      width: 30px;
      height: 30px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: bold;
    }

    .option-card .option {
      width: 100%;
      padding: 10px;
    }
  </style>
</head>
<body>

  <!-- Paso 1 -->
  <div class="card" id="step1">
    <h1>¿Me dejarías ser tu San Valentín?</h1>
    <img src="https://i.postimg.cc/y6PfpPqK/906a0aa0178e34058edb3d30fb183608.jpg" alt="Foto bonita">
    <button class="yes" id="yesBtn">Sí</button>
    <button class="no" id="noBtn">No</button>
  </div>

  <!-- Paso 2 -->
  <div class="card hidden" id="step2">
    <h1>¿Eres libre este día?</h1>
    <button class="option date-option">14/02/2026 – 19:00</button>
    <button class="confirm-btn" id="confirmDate">Confirmar fecha</button>
  </div>

  <!-- Paso 3 -->
  <div class="card hidden" id="step3">
    <h1>¿Qué te gustaría comer?</h1>
    <div class="options-grid">
      <!-- Repetí las option-card de comida que tenías -->
    </div>
    <button class="confirm-btn" id="confirmFood">Confirmar comida</button>
  </div>

  <!-- Paso 4 -->
  <div class="card hidden" id="step4">
    <h1>¿Qué te gustaría hacer?</h1>
    <div class="options-grid">
      <!-- Repetí las option-card de actividades que tenías -->
    </div>
    <button class="confirm-btn" id="confirmActivity">Confirmar opción</button>
  </div>

  <!-- Paso final -->
  <div class="card hidden" id="final">
    <img src="https://i.postimg.cc/G9wd28YK/8a5cf78cf7cf0c8f23e081ec6dea3ccc.jpg" alt="Feliz San Valentín">
    <h1>
      ¡Ya está todo listo para nuestra cita!<br><br>
      No te atrevas a faltar eh. Te estaré<br><br>
      esperando y si no vienes, mi corazón se<br><br>
      va a hacer añicos, ¡nos vemos guapo! 😘
    </h1>
  </div>

  <script>
    const yesBtn = document.getElementById("yesBtn");
    const noBtn = document.getElementById("noBtn");
    let scale = 1;

    const loveElements = ["💖","💗","💕","💘","❤️","Te amo","Mi amor","Eres mío","😍","✨","Te quiero","Amor mio","Mi príncipe","Hermoso mío","Pecas","Me perteneces","Eres mi mundo","Mi calabacín","Encantador","Te estoy vigilando","Siempre te estoy viendo","Guapo","Grandioso","Brillante","Bello","😘","🫦","🥰","💝","💓","💞","❤️‍🩹","💋","❣️","Cariño","Dulzura","Tesoro","Corazón","cielo","Ternura","Sol","Luna"];

    function showLove() {
      const love = document.createElement("div");
      love.className = "floating-love";
      love.innerText = loveElements[Math.floor(Math.random() * loveElements.length)];
      love.style.left = Math.random() * 100 + "vw";
      love.style.animationDuration = (2 + Math.random() * 2) + "s";
      love.style.fontSize = (18 + Math.random() * 8) + "px";
      document.body.appendChild(love);
      setTimeout(() => love.remove(), 15000);
    }

    noBtn.onclick = () => {
      scale += 0.2;
      yesBtn.style.transform = `scale(${scale})`;
    };

    yesBtn.onclick = () => goToStep(2);

    document.querySelectorAll(".date-option").forEach(btn => {
      btn.onclick = () => {
        document.querySelectorAll(".date-option").forEach(b => b.classList.remove("selected"));
        btn.classList.add("selected");
        showLove();
      }
    });

    document.querySelectorAll(".food-option").forEach(btn => {
      btn.onclick = () => {
        const card = btn.closest(".option-card");
        card.classList.toggle("selected");
        const check = card.querySelector(".check-mark");
        check.classList.toggle("hidden");
        showLove();
      }
    });

    document.querySelectorAll(".activity-option").forEach(btn => {
      btn.onclick = () => {
        const card = btn.closest(".option-card");
        card.classList.toggle("selected");
        const check = card.querySelector(".check-mark");
        check.classList.toggle("hidden");
        showLove();
      }
    });

    document.getElementById("confirmDate").onclick = () => {
      if(document.querySelector(".date-option.selected")) goToStep(3);
      else alert("Elige una fecha primero amor ❤️");
    };

    document.getElementById("confirmFood").onclick = () => {
      if(document.querySelector(".option-card.selected[data-type='food']")) goToStep(4);
      else alert("Elige al menos una comida ❤️");
    };

    document.getElementById("confirmActivity").onclick = () => {
      if(document.querySelector(".option-card.selected[data-type='activity']")) goToStep(5);
      else alert("Elige al menos una actividad ❤️");
    };

    function goToStep(stepNumber) {
      document.querySelectorAll(".card").forEach(card => card.classList.add("hidden"));
      if(stepNumber === 5) document.getElementById("final").classList.remove("hidden");
      else document.getElementById("step" + stepNumber).classList.remove("hidden");
    }
  </script>
</body>
</html>
