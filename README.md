<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Pergunta Sim ou Não</title>
  <style>
    body {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      font-family: sans-serif;
      background-color: #f0f0f0;
      overflow: hidden;
      margin: 0;
    }

    h1 {
      margin-bottom: 130px;
      transition: opacity 0.5s ease;
    }

    .btn-container {
      position: relative;
      width: 300px;
      height: 300px;
    }

    button {
      width: 120px;
      height: 60px;
      font-size: 1rem;
      cursor: pointer;
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      transition: all 0.2s ease;
      border: none;
      border-radius: 12px;
      box-shadow: 2px 2px 10px rgba(0,0,0,0.1);
    }

    #yes {
      left: 0;
      background-color: #4caf50;
      color: white;
    }

    #no {
      right: 0;
      background-color: #f44336;
      color: white;
    }

    #resultado, #triste {
      display: none;
      flex-direction: column;
      align-items: center;
      animation: fadeIn 1s ease;
    }

    #resultado img, #triste img {
      width: 300px;
      height: auto;
      margin-bottom: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    }

    #atributos {
      font-size: 1.2rem;
      text-align: center;
      line-height: 1.8;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.95); }
      to { opacity: 1; transform: scale(1); }
    }
  </style>
</head>
<body>

  <h1 id="pergunta">Mereço um aumento?</h1>

  <div class="btn-container" id="botoes">
    <button id="yes">Sim meu melhor funcionário</button>
    <button id="no">Não</button>
  </div>

  <!-- Resultado positivo -->
  <div id="resultado">
    <img src="https://via.placeholder.com/300x200.png?text=Level+Up" alt="Atributos Melhorados">
    <div id="atributos">
      <strong>Atributos melhorados</strong><br>
      Trabalho em equipe +40%<br>
      Desempenho +65%<br>
      Respostas mais rápidas +56%<br>
      Elogios aos chefes +32%
    </div>
  </div>

  <!-- Resultado negativo: gato triste -->
  <div id="triste">
    <img src="https://i.imgur.com/yv8JrMo.jpeg" alt="Gato Molhado Triste">
    <div id="atributos">
      <strong>😭 Que crueldade...</strong><br>
      Você disse <em>não</em> para seu melhor funcionário.<br>
      Agora até o gato ficou molhado e triste. 🐱💧
    </div>
  </div>

  <script>
    const noBtn = document.getElementById('no');
    const container = document.querySelector('.btn-container');

    container.addEventListener('mousemove', (e) => {
      const rect = noBtn.getBoundingClientRect();
      const mouseX = e.clientX;
      const mouseY = e.clientY;

      const dx = mouseX - (rect.left + rect.width / 2);
      const dy = mouseY - (rect.top + rect.height / 2);
      const distance = Math.hypot(dx, dy);

      if (distance < 150) { // botão foge mais longe
        const angle = Math.atan2(dy, dx);
        const moveX = Math.cos(angle) * 150;
        const moveY = Math.sin(angle) * 150;

        const newLeft = Math.min(
          container.clientWidth - rect.width,
          Math.max(0, rect.left - container.getBoundingClientRect().left - moveX)
        );
        const newTop = Math.min(
          container.clientHeight - rect.height,
          Math.max(0, rect.top - container.getBoundingClientRect().top - moveY)
        );

        noBtn.style.left = `${newLeft}px`;
        noBtn.style.top = `${newTop}px`;
      }
    });

    // Sim: mostra atributos positivos
    document.getElementById('yes').addEventListener('click', () => {
      document.getElementById('pergunta').style.opacity = '0';
      document.getElementById('botoes').style.display = 'none';
      document.getElementById('resultado').style.display = 'flex';
    });

    // Não: mostra gato triste
    noBtn.addEventListener('click', () => {
      document.getElementById('pergunta').style.opacity = '0';
      document.getElementById('botoes').style.display = 'none';
      document.getElementById('triste').style.display = 'flex';
    });
  </script>


