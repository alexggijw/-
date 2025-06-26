<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>AR Video with Custom Marker</title>
  <script src="https://aframe.io/releases/1.4.0/aframe.min.js"></script>
  <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
  <style>
    .arjs-loader {
      height: 100vh;
      width: 100%;
      position: absolute;
      top: 0;
      left: 0;
      background: #000;
      color: #fff;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: Arial;
    }
    .marker-info {
      position: fixed;
      bottom: 20px;
      left: 0;
      right: 0;
      text-align: center;
      background: rgba(0,0,0,0.7);
      color: white;
      padding: 10px;
      z-index: 1000;
    }
  </style>
</head>
<body>
  <!-- Лоадер -->
  <div class="arjs-loader">
    <div>Инициализация AR... Разрешите доступ к камере</div>
  </div>

  <!-- AR-сцена -->
  <a-scene 
    vr-mode-ui="enabled: false"
    renderer="logarithmicDepthBuffer: true;"
    embedded 
    arjs="sourceType: webcam; detectionMode: mono_and_matrix; matrixCodeType: 3x3;"
  >
    <!-- Ваше видео -->
    <a-marker preset="hiro">
      <a-video
        src="https://files.catbox.moe/bmswfc.mp4"
        position="0 0 0"
        width="1.6"
        height="0.9"
        rotation="-90 0 0"
        autoplay
        loop
        playsinline
      ></a-video>
    </a-marker>
    <a-entity camera></a-entity>
  </a-scene>

  <!-- Инструкция -->
  <div class="marker-info">
    <a href="https://ar-js-org.github.io/AR.js/data/images/hiro.png" download style="color: #00bcd4;">
      Скачать маркер Hiro
    </a>
    <p style="margin-top: 5px;">Наведите камеру на маркер</p>
  </div>

  <script>
    // Автоплей и скрытие лоадера
    document.querySelector('a-scene').addEventListener('loaded', function() {
      document.querySelector('.arjs-loader').style.display = 'none';
      
      const video = document.querySelector('a-video').components.material.material.map.image;
      video.play().catch(e => {
        console.log("Автовоспроизведение заблокировано. Требуется взаимодействие пользователя.");
      });
    });
  </script>
</body>
</html>
