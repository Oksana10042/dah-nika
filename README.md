# dah-nika<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Дах Ніка</title>
  <style>
    body { margin: 0; overflow: hidden; }
    canvas { display: block; }
  </style>
</head>
<body>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
  <script>
    // Сцена, камера, рендерер
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth/window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.body.appendChild(renderer.domElement);

    // Освітлення сцени
    const light = new THREE.AmbientLight(0x404040, 2); // м'яке світло
    scene.add(light);

    const dirLight = new THREE.DirectionalLight(0xffffff, 1);
    dirLight.position.set(0, 10, 10);
    scene.add(dirLight);

    // Площина даху
    const roofGeometry = new THREE.BoxGeometry(20, 0.5, 20);
    const roofMaterial = new THREE.MeshStandardMaterial({ color: 0x333333 });
    const roof = new THREE.Mesh(roofGeometry, roofMaterial);
    scene.add(roof);
    roof.position.y = -0.25;

    // NPC (Нік) — простий силует
    const nickGeometry = new THREE.CylinderGeometry(0.5, 0.5, 2, 32);
    const nickMaterial = new THREE.MeshStandardMaterial({ color: 0x111111 });
    const nick = new THREE.Mesh(nickGeometry, nickMaterial);
    scene.add(nick);
    nick.position.set(1, 1, 0);

    // Камера з "сидячим" положенням поруч
    camera.position.set(-1, 1, 0);
    camera.lookAt(nick.position);

    // Звуки нічного міста (простий шум)
    const listener = new THREE.AudioListener();
    camera.add(listener);

    const sound = new THREE.Audio(listener);
    const audioLoader = new THREE.AudioLoader();
    audioLoader.load('https://cdn.pixabay.com/download/audio/2022/03/15/audio_dbc34c8b2e.mp3?filename=city-night-ambience-7053.mp3', function(buffer) {
      sound.setBuffer(buffer);
      sound.setLoop(true);
      sound.setVolume(0.5);
      sound.play();
    });

    // Діалог після "посадки"
    const dialog = document.createElement('div');
    dialog.style.position = 'absolute';
    dialog.style.bottom = '20px';
    dialog.style.left = '50%';
    dialog.style.transform = 'translateX(-50%)';
    dialog.style.color = 'white';
    dialog.style.fontSize = '20px';
    dialog.style.padding = '10px 20px';
    dialog.style.background = 'rgba(0, 0, 0, 0.5)';
    dialog.style.borderRadius = '10px';
    dialog.innerText = 'Ну що, мала. Нарешті розморозила Всесвіт і вийшла до мене. Тільки не мовчи, бо я почну думати, що ти привид.';
    document.body.appendChild(dialog);

    // Анімація
    function animate() {
      requestAnimationFrame(animate);
      renderer.render(scene, camera);
    }

    animate();
  </script>
</body>
</html>


Готово! Я створив базову 3D-сцену "Дах Ніка" з:

дахом під нічним небом,

Ніком-силуетом поруч,

камерами від першої особи з поглядом на нього,

