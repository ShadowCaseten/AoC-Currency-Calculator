# AoC-Currency-Calculator

STEP 1 - Copy & Paste Code below into   Notepad

STEP 2 - Save as .html

STEP 3 - Drag & Drop onto Desktop

STEP 4 - Open from Desktop

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>AoC Currency Calculator</title>

<style>
  body {
    background: radial-gradient(circle at top, #1e1e2f, #0f0f18);
    font-family: Arial, sans-serif;
    color: #e0e0e0;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }

  .calculator {
    background: #151522;
    border: 2px solid #bfa76a;
    border-radius: 12px;
    padding: 25px;
    width: 340px;
    box-shadow: 0 0 25px rgba(191, 167, 106, 0.3);
  }

  h2 {
    text-align: center;
    color: #f5d76e;
    margin-bottom: 20px;
    letter-spacing: 1px;
  }

  .input-group {
    display: flex;
    justify-content: space-between;
    margin-bottom: 12px;
  }

  .input-group label {
    flex: 1;
    padding-top: 6px;
  }

  .input-group input {
    width: 90px;
    background: #0f0f18;
    border: 1px solid #555;
    border-radius: 6px;
    color: #fff;
    padding: 6px;
    text-align: right;
  }

  button {
    width: 100%;
    margin-top: 15px;
    padding: 10px;
    background: linear-gradient(135deg, #d4af37, #9f7c1f);
    border: none;
    border-radius: 8px;
    color: #000;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
  }

  button:hover {
    filter: brightness(1.1);
  }

  .results {
    margin-top: 18px;
    padding: 12px;
    background: #0f0f18;
    border-radius: 8px;
    border: 1px solid #333;
  }

  .currency-line {
    display: flex;
    justify-content: space-between;
    margin-bottom: 6px;
  }

  .gold { color: #f5d76e; }
  .silver { color: #cfd8dc; }
  .copper { color: #cd7f32; }

  .gold-eq {
    margin-top: 10px;
    text-align: center;
    font-size: 14px;
    opacity: 0.9;
  }
</style>
</head>

<body>

<div class="calculator">
  <h2>AoC Price Calculator</h2>

  <div class="input-group">
    <label class="gold">Gold</label>
    <input type="number" id="gold" value="0">
  </div>

  <div class="input-group">
    <label class="silver">Silver</label>
    <input type="number" id="silver" value="0">
  </div>

  <div class="input-group">
    <label class="copper">Copper</label>
    <input type="number" id="copper" value="0">
  </div>

  <div class="input-group">
    <label>Quantity</label>
    <input type="number" id="qty" value="1">
  </div>

  <button onclick="calculate()">Calculate</button>

  <div class="results" id="output">
    <div class="currency-line gold"><span>Gold</span><span>0</span></div>
    <div class="currency-line silver"><span>Silver</span><span>0</span></div>
    <div class="currency-line copper"><span>Copper</span><span>0</span></div>
    <div class="gold-eq">Gold Equivalent: 0.0000</div>
  </div>
</div>

<script>
function calculate() {
  const gold = parseInt(document.getElementById("gold").value) || 0;
  const silver = parseInt(document.getElementById("silver").value) || 0;
  const copper = parseInt(document.getElementById("copper").value) || 0;
  const qty = parseInt(document.getElementById("qty").value) || 1;

  const COPPER_PER_GOLD = 10000;
  const COPPER_PER_SILVER = 100;

  const priceCopper =
    gold * COPPER_PER_GOLD +
    silver * COPPER_PER_SILVER +
    copper;

  const totalCopper = priceCopper * qty;

  const totalGold = Math.floor(totalCopper / COPPER_PER_GOLD);
  const remAfterGold = totalCopper % COPPER_PER_GOLD;
  const totalSilver = Math.floor(remAfterGold / COPPER_PER_SILVER);
  const totalCopperFinal = remAfterGold % COPPER_PER_SILVER;

  const goldEquivalent = (totalCopper / COPPER_PER_GOLD).toFixed(4);

  document.getElementById("output").innerHTML = `
    <div class="currency-line gold"><span>Gold</span><span>${totalGold}</span></div>
    <div class="currency-line silver"><span>Silver</span><span>${totalSilver}</span></div>
    <div class="currency-line copper"><span>Copper</span><span>${totalCopperFinal}</span></div>
    <div class="gold-eq">Gold Equivalent: ${goldEquivalent}</div>
  `;
}
</script>

</body>
</html>
