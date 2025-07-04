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
</html>
