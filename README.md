# Hjulgeomtri-pwa-<!DOCTYPE html>
<html lang="no">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <link rel="manifest" href="manifest.json" />
  <title>Toe & Camber Kalkulator</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 1em; }
    label, input, select { display: block; margin-bottom: .5em; }
    .card { border: 1px solid #ccc; border-radius: 8px; padding: 1em; margin-bottom: 1em; }
    .results { font-weight: bold; }
  </style>
</head>
<body>
  <h1>Toe & Camber Kalkulator</h1>
  <div class="card">
    <label>Vinkel (minutter):
      <input type="number" id="vinkel" value="10" min="0">
    </label>
    <label>Felgstørrelse (13–22″):
      <select id="rimSize"></select>
    </label>
    <button id="beregn">Beregn</button>
  </div>
  <div class="card results">
    <p>Toe per hjul: <span id="toeWheel">0</span> mm</p>
    <p>Total toe per aksel: <span id="toeTotal">0</span> mm</p>
    <p>Camber høydeforskjell: <span id="camber">0</span> mm</p>
  </div>
  <script src="app.js"></script>
</body>
</html>function angleMinutesToMM(minutes, diameterMM) {
  const angleDeg = minutes / 60;
  const radians = angleDeg * Math.PI / 180;
  const radius = diameterMM / 2;
  return 2 * radius * Math.tan(radians);
}

const rimSelect = document.getElementById('rimSize');
for (let i = 13; i <= 22; i++) {
  const opt = document.createElement('option');
  opt.value = i;
  opt.textContent = `${i}"`;
  rimSelect.appendChild(opt);
}

function calculate() {
  const minutes = Number(document.getElementById('vinkel').value);
  const rim = Number(rimSelect.value);
  const diameter = rim * 25.4;
  const toeWheel = angleMinutesToMM(minutes, diameter);
  const toeTotal = toeWheel * 2;
  const camber = toeWheel;
  document.getElementById('toeWheel').textContent = toeWheel.toFixed(2);
  document.getElementById('toeTotal').textContent = toeTotal.toFixed(2);
  document.getElementById('camber').textContent = camber.toFixed(2);
}

document.getElementById('beregn').addEventListener('click', calculate);
calculate();{
  "name": "Toe & Camber Kalkulator",
  "short_name": "HjulGeom",
  "start_url": ".",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#3f51b5",
  "icons": [
    { "src": "icon-192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "icon-512.png", "sizes": "512x512", "type": "image/png" }
  ]
}const cacheName = 'hjulgeom-v1';
const filesToCache = [
  '.',
  'index.html',
  'app.js',
  'manifest.json',
  'icon-192.png',
  'icon-512.png'
];

self.addEventListener('install', e => {
  e.waitUntil(caches.open(cacheName).then(cache => cache.addAll(filesToCache)));
});

self.addEventListener('fetch', e => {
  e.respondWith(caches.match(e.request).then(resp => resp || fetch(e.request)));
});
