<!DOCTYPE html>
<html lang="nl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>De Belastingmeter</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 2rem; background: #f5f5f5; }
    h1 { color: #1a1a1a; }
    label, input { display: block; margin-bottom: 10px; }
    input[type="number"] { padding: 5px; width: 100%; max-width: 300px; }
    .resultaat { margin-top: 20px; padding: 10px; background: white; border-radius: 8px; }
    button { padding: 10px 15px; background-color: #0073e6; color: white; border: none; border-radius: 5px; cursor: pointer; }
    button:hover { background-color: #005bb5; }
  </style>
</head>
<body>
  <h1>De Belastingmeter</h1>
  <p>Bereken hoeveel je jaarlijks echt aan de overheid betaalt via zichtbare en onzichtbare belastingen.</p>

  <form id="belastingForm">
    <label>Bruto jaarinkomen (€):
      <input type="number" id="inkomen" value="40000">
    </label>

    <label>Btw op aankopen per maand (€):
      <input type="number" id="btwMaand" value="250">
    </label>

    <label>Accijnzen (brandstof, alcohol, tabak) per maand (€):
      <input type="number" id="accijnzen" value="50">
    </label>

    <label>Huur per maand (€):
      <input type="number" id="huur" value="800">
    </label>

    <label>Overige verborgen belastingen per maand (€):
      <input type="number" id="verborgen" value="100">
    </label>

    <button type="button" onclick="berekenBelastingen()">Bereken totaal</button>
  </form>

  <div class="resultaat" id="resultaat"></div>

  <script>
    function berekenBelastingen() {
      const inkomen = parseFloat(document.getElementById('inkomen').value) || 0;
      const btw = parseFloat(document.getElementById('btwMaand').value) * 12 || 0;
      const accijnzen = parseFloat(document.getElementById('accijnzen').value) * 12 || 0;
      const huur = parseFloat(document.getElementById('huur').value) * 12 || 0;
      const verborgen = parseFloat(document.getElementById('verborgen').value) * 12 || 0;

      // Aangenomen effectieve inkomstenbelasting gemiddeld 35%
      const inkomstenbelasting = inkomen * 0.35;

      // Verhuurdersheffing verwerkt in huur, geschat aandeel: 10%
      const indirecteHuurbelasting = huur * 0.10;

      const totaal = inkomstenbelasting + btw + accijnzen + verborgen + indirecteHuurbelasting;

      document.getElementById('resultaat').innerHTML = `
        <h2>Jaarlijkse belastingdruk:</h2>
        <p><strong>€ ${totaal.toLocaleString('nl-NL', {minimumFractionDigits: 2, maximumFractionDigits: 2})}</strong></p>
        <p>Waarvan:</p>
        <ul>
          <li>Inkomstenbelasting: € ${inkomstenbelasting.toFixed(2)}</li>
          <li>Btw: € ${btw.toFixed(2)}</li>
          <li>Accijnzen: € ${accijnzen.toFixed(2)}</li>
          <li>Verborgen belastingen: € ${verborgen.toFixed(2)}</li>
          <li>Verhuurdersheffing via huur: € ${indirecteHuurbelasting.toFixed(2)}</li>
        </ul>
      `;
    }
  </script>
</body>
</html>
Debelastingmeter/
│
├── index.html
├── css/
│   └── style.css
└── js/
    └── script.js
