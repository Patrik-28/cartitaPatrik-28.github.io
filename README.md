<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Carta Para Ti</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 20px;
      background-color: #b2e0f7;
      font-family: 'Georgia', serif;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      gap: 20px;
      position: relative;
    }

    .carta-container {
      width: 100%;
      max-width: 400px;
      background-color: #fff0f5;
      border: 3px solid #f4a9b8;
      border-radius: 10px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
      cursor: pointer;
      padding: 20px;
      text-align: center;
      position: relative;
      transition: all 0.4s ease;
    }

    @keyframes brilloFlores {
      0%, 100% {
        filter: brightness(1);
        transform: translateX(-50%) translateY(0);
      }
      50% {
        filter: brightness(1.2);
        transform: translateX(-50%) translateY(-5px);
      }
    }

    .flores {
      font-size: 24px;
      position: absolute;
      top: -25px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      gap: 10px;
      animation: brilloFlores 3s ease-in-out infinite;
    }

    .carta-container.abierta .flores {
      display: none;
      animation: none;
    }

    .carta-texto {
      font-size: 26px;
      color: #e87ea5;
      font-weight: bold;
    }

    .mensaje {
      display: none;
      text-align: left;
      margin-top: 10px;
      white-space: pre-wrap;
      color: #c25b82;
      font-size: 16px;
      line-height: 1.6;
    }

    .carta-container.abierta .carta-texto {
      display: none;
    }

    .carta-container.abierta .mensaje {
      display: block;
    }

    button {
      background-color: #f4a9b8;
      border: none;
      border-radius: 8px;
      padding: 10px 20px;
      font-size: 18px;
      color: white;
      cursor: pointer;
      box-shadow: 0 4px 10px rgba(0,0,0,0.15);
      transition: background-color 0.3s ease;
    }

    button:hover {
      background-color: #e06c89;
    }

    #btnCerrarCarta {
      display: none;
      margin-top: 10px;
    }

    .carta-container.abierta + #btnCerrarCarta {
      display: inline-block;
    }

    .selector-musica {
      position: fixed;
      top: 50%;
      left: 15px;
      transform: translateY(-50%);
      background-color: #fff0f5;
      border: 2px solid #f4a9b8;
      border-radius: 10px;
      padding: 12px;
      display: flex;
      flex-direction: column;
      gap: 10px;
      z-index: 1000;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
    }

    .selector-musica button {
      font-size: 14px;
      padding: 6px 10px;
      background-color: #f4a9b8;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }

    .selector-musica button:hover {
      background-color: #e06c89;
    }

    @media (max-width: 480px) {
      body {
        padding: 10px;
        gap: 15px;
      }

      .carta-texto {
        font-size: 22px;
      }

      .mensaje {
        font-size: 15px;
      }

      .flores {
        font-size: 20px;
        top: -20px;
      }

      button {
        font-size: 16px;
        padding: 8px 16px;
      }

      .selector-musica {
        left: 5px;
        padding: 8px;
      }

      .selector-musica button {
        font-size: 12px;
      }
    }
  </style>
</head>
<body>

  <div class="selector-musica">
    <button onclick="cambiarCancion('CUCO AmoR.mp3')">🎵 CUCO AmoR</button>
    <button onclick="cambiarCancion('Amor-Emmanuel.mp3')">🎵 Amor-Emmanuel</button>
  </div>

  <div class="carta-container" onclick="abrirCarta(this)">
    <div class="flores">🌸 🌼 🌹 🌸 🌼</div>
    <div class="carta-texto">Para ti 💌</div>
    <div class="mensaje">
Querida Khayra:

En este día tan especial, quiero desearte un feliz cumpleaños lleno de amor 
y felicidad. A pesar del poco tiempo que llevamos hablando y conociéndonos, 
quiero que sepas que la he pasado bien en cada llamada o mensaje de texto 
que me envías. Son las 3:50 am y solo pienso en ti y en las ganas que tengo 
de que estés aquí jsjsjsjs.

Te amo mucho, mi niña. Eres perfecta tal como eres ❤ nunca cambies.

Te amo ∞⋅∞

ATT: Patrik ❤
    </div>
  </div>

  <button onclick="toggleMusica()">🎵 Reproducir / Pausar Música</button>
  <button id="btnCerrarCarta" onclick="cerrarCarta()">← Volver</button>

  <audio id="musicaFondo" src="CUCO AmoR.mp3" loop></audio>

  <script>
    const musica = document.getElementById('musicaFondo');
    let sonando = false;

    function abrirCarta(elemento) {
      if (!elemento.classList.contains('abierta')) {
        elemento.classList.add('abierta');
        musica.play().then(() => { sonando = true; }).catch(e => console.log('Error al reproducir:', e));
        document.getElementById('btnCerrarCarta').style.display = 'inline-block';
      }
    }

    function cerrarCarta() {
      const carta = document.querySelector('.carta-container.abierta');
      if (carta) {
        carta.classList.remove('abierta');
        musica.pause();
        musica.currentTime = 0;
        sonando = false;
        document.getElementById('btnCerrarCarta').style.display = 'none';
      }
    }

    function toggleMusica() {
      if (!sonando) {
        musica.play().then(() => { sonando = true; }).catch(e => console.log('Error al reproducir:', e));
      } else {
        musica.pause();
        sonando = false;
      }
    }

    function cambiarCancion(ruta) {
      const estabaSonando = sonando;
      musica.pause();
      musica.currentTime = 0;
      musica.src = ruta;
      if (estabaSonando) {
        musica.play().then(() => { sonando = true; }).catch(e => console.log('Error al reproducir nueva canción:', e));
      }
    }
  </script>

</body>
</html>
