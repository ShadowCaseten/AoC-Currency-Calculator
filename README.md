# AoC-Currency-Calculator

STEP 1 - Copy & Paste Code below into   Notepad

STEP 2 - Save as .html

STEP 3 - Drag & Drop onto Desktop

STEP 4 - Open from Desktop

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>AoC Helper Tool</title>
<style>
body {
  background: #0f0f18;
  font-family: Arial, sans-serif;
  color: #e0e0e0;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding: 20px;
}

.container { display: flex; gap: 30px; align-items: flex-start; }

.left-column { display: flex; flex-direction: column; gap: 20px; }

/* Calculator & Tracker */
.calculator, .tracker-container {
  background: #151522;
  border: 2px solid #bfa76a;
  border-radius: 12px;
  padding: 10px 25px 25px 25px;
  width: 340px;
  box-shadow: 0 0 25px rgba(191, 167, 106, 0.3);
  display: flex;
  flex-direction: column;
}

.calculator h2, .tracker-container h3 { 
  color: #f5d76e; 
  text-align: center; 
  letter-spacing: 1px; 
  margin-bottom: 15px;
}

.input-group { display: flex; justify-content: space-between; margin-bottom: 12px; }
.input-group label { flex: 1; padding-top: 6px; }
.input-group input, .input-group select {
  border: 1px solid #555;
  border-radius: 6px;
  color: #fff;
  padding: 6px;
  text-align: center;
  background: #0f0f18;
}

.calculator .input-group input { width: 90px; }
.tracker-container .input-group input { width: 60px; margin-right: 6px; }
.tracker-container .input-group select, 
.tracker-container .input-group input.item-name-input { flex: 1; }

button {
  width: 100%;
  margin-top: 10px;
  padding: 10px;
  background: linear-gradient(135deg, #d4af37, #9f7c1f);
  border: none;
  border-radius: 8px;
  color: #000;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}
button:hover { filter: brightness(1.1); }

.results {
  margin-top: 18px;
  padding: 12px;
  background: #0f0f18;
  border-radius: 8px;
  border: 1px solid #333;
  flex-shrink: 0;
}

.currency-line { display: flex; justify-content: space-between; margin-bottom: 6px; }
.gold { color: #f5d76e; }
.silver { color: #cfd8dc; }
.copper { color: #cd7f32; }
.gold-eq { margin-top: 10px; text-align: center; font-size: 14px; opacity: 0.9; }

.right-column { display:flex; gap:10px; }

/* Notepad */
.notepad {
  background: #151522;
  border: 2px solid #bfa76a;
  border-radius: 12px;
  padding: 15px;
  flex:1;
  display: flex;
  flex-direction: column;
  height: 1080px; /* taller notepad container */
}

#noteArea { 
  flex: 1; 
  background: #0f0f18;
  border: 1px solid #333;
  border-radius: 8px;
  color: #fff;
  padding: 12px;
  overflow-y: auto;
  font-size: 16px;
  min-height: 800px; /* bigger typing area */
  max-height: calc(100% - 60px); /* leave space for tabs */
}

/* Tabs */
.tab {
  padding: 6px 12px;
  border: 1px solid #bfa76a;
  border-radius: 6px;
  cursor: pointer;
  user-select: none;
  color: #fff;
}
.tab.active { outline: 2px solid #d4af37; }

/* Toolbar (moved outside notepad) */
#noteToolbar {
  display:flex; 
  flex-direction: column;
  gap:6px;
  width:60px;
}
#noteToolbar button {
  background: #151522;
  border:1px solid #bfa76a;
  color:#fff;
  padding:6px;
  border-radius:4px;
  cursor:pointer;
}
#noteToolbar button:hover { filter: brightness(1.2); }
#noteToolbar input[type=color] {
  width:100%;
  height:32px;
  padding:0;
  border:none;
  border-radius:4px;
  cursor:pointer;
}

/* Tracker Table */
#trackerTable { width: 100%; border-collapse: collapse; margin-top: 10px; }
#trackerTable td, #trackerTable th {
  border: 1px solid #333;
  padding: 6px;
  text-align: center;
  font-size: 14px;
  background: #151522;
}
td.item-name.Common { color: #e0e0e0; }
td.item-name.Uncommon { color: #00ff00; }
td.item-name.Rare { color: #00aaff; }
td.item-name.Heroic { color: #8C730C; }
td.item-name.Epic { color: #da70d6; }
td.item-name.Legendary { color: #ffa500; }
td.item-name.Artifact { color: #ffff00; }
td.item-name { font-weight: bold; text-shadow: 1px 1px 2px #000; }
.deleteBtn {
  background: #8b0000;
  color: #fff;
  font-weight: bold;
  padding: 4px 8px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
}
.deleteBtn:hover { background: #b22222; }
</style>
</head>
<body>

<div class="container">
  <div class="left-column">
    <!-- Calculator -->
    <div class="calculator">
      <h2>Currency Calc</h2>
      <div class="input-group"><label class="gold">Gold</label><input type="number" id="gold" value="0" min="0"></div>
      <div class="input-group"><label class="silver">Silver</label><input type="number" id="silver" value="0" min="0"></div>
      <div class="input-group"><label class="copper">Copper</label><input type="number" id="copper" value="0" min="0"></div>
      <div class="input-group"><label>Quantity</label><input type="number" id="qty" value="1" min="1"></div>
      <button onclick="calculate()">Calculate</button>
      <div class="results" id="output">
        <div class="currency-line gold"><span>Gold</span><span>0</span></div>
        <div class="currency-line silver"><span>Silver</span><span>0</span></div>
        <div class="currency-line copper"><span>Copper</span><span>0</span></div>
        <div class="gold-eq">Gold Equivalent: 0.0000</div>
      </div>
    </div>

    <!-- Tracker -->
    <div class="tracker-container">
      <h3>Item Tracker</h3>
      <input type="text" id="trackerSearch" placeholder="Search items...">
      <div class="input-group">
        <input type="text" id="itemName" class="item-name-input" placeholder="Item Name">
        <select id="itemRarity">
          <option value="Common" style="color:#e0e0e0;">○ Common</option>
          <option value="Uncommon" style="color:#00ff00;">■ Uncommon</option>
          <option value="Rare" style="color:#00aaff;">▲ Rare</option>
          <option value="Heroic" style="color:#8C730C;">◆ Heroic</option>
          <option value="Epic" style="color:#da70d6;">⬟ Epic</option>
          <option value="Legendary" style="color:#ffa500;">⬢ Legendary</option>
          <option value="Artifact" style="color:#ffff00;">⬣ Artifact</option>
        </select>
      </div>
      <div class="input-group">
        <input type="number" id="itemGold" placeholder="Gold" min="0">
        <input type="number" id="itemSilver" placeholder="Silver" min="0">
        <input type="number" id="itemCopper" placeholder="Copper" min="0">
        <button id="addItem">Add</button>
      </div>
      <table id="trackerTable">
        <tbody></tbody>
      </table>
    </div>
  </div>

  <!-- Notepad + Toolbar -->
  <div class="right-column">
    <div class="notepad">
      <h3>Notepad</h3>
      <!-- Tabs -->
      <div id="noteTabs" style="display:flex; gap:6px; margin-bottom:8px; cursor: grab;"></div>

      <!-- Contenteditable area -->
      <div id="noteArea" contenteditable="true"></div>
    </div>

    <!-- Toolbar outside the notepad -->
    <div id="noteToolbar">
      <button onclick="formatText('bold')"><b>B</b></button>
      <button onclick="formatText('italic')"><i>I</i></button>
      <button onclick="formatText('underline')"><u>U</u></button>
      <button onclick="insertCheckbox()">☐</button>
      <input type="color" id="textColor" title="Text Color">
    </div>
  </div>
</div>

<script>
// Calculator
const COPPER_PER_GOLD = 10000;
const COPPER_PER_SILVER = 100;
function calculate() {
  const gold = parseInt(document.getElementById("gold").value)||0;
  const silver = parseInt(document.getElementById("silver").value)||0;
  const copper = parseInt(document.getElementById("copper").value)||0;
  const qty = parseInt(document.getElementById("qty").value)||1;
  const priceCopper = gold*COPPER_PER_GOLD + silver*COPPER_PER_SILVER + copper;
  const totalCopper = priceCopper*qty;
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

// Tracker
let trackerTableBody = document.querySelector("#trackerTable tbody");
function renderTracker(data){
  trackerTableBody.innerHTML = '';
  data.forEach((item,index)=>{
    trackerTableBody.innerHTML += `<tr>
      <td class="item-name ${item.rarity}">${item.name}</td>
      <td class="gold">${item.gold}</td>
      <td class="silver">${item.silver}</td>
      <td class="copper">${item.copper}</td>
      <td class="item-name ${item.rarity}">${item.rarity}</td>
      <td><span class="deleteBtn" onclick="deleteItem(${index})">X</span></td>
    </tr>`;
  });
}
function getTrackerData(){ return JSON.parse(localStorage.getItem('tracker') || '[]'); }
document.getElementById('addItem').addEventListener('click', ()=>{
  const name = document.getElementById('itemName').value.trim();
  const rarity = document.getElementById('itemRarity').value;
  const gold = parseFloat(document.getElementById('itemGold').value) || 0;
  const silver = parseFloat(document.getElementById('itemSilver').value) || 0;
  const copper = parseFloat(document.getElementById('itemCopper').value) || 0;
  if(!name){ alert("Enter item name!"); return; }
  const saved = getTrackerData();
  saved.push({name,rarity,gold,silver,copper});
  localStorage.setItem('tracker', JSON.stringify(saved));
  document.getElementById('itemName').value='';
  document.getElementById('itemGold').value='';
  document.getElementById('itemSilver').value='';
  document.getElementById('itemCopper').value='';
  renderTracker(saved);
});
function deleteItem(index){
  if(confirm("Delete this item?")){
    const saved = getTrackerData();
    saved.splice(index,1);
    localStorage.setItem('tracker', JSON.stringify(saved));
    renderTracker(saved);
  }
}
document.getElementById('trackerSearch').addEventListener('input', ()=>{
  const searchTerm = document.getElementById('trackerSearch').value.toLowerCase();
  const data = getTrackerData().filter(item=>item.name.toLowerCase().includes(searchTerm));
  renderTracker(data);
});
renderTracker(getTrackerData());

// Notepad
const tabsContainer = document.getElementById("noteTabs");
const noteArea = document.getElementById("noteArea");
let notes = JSON.parse(localStorage.getItem("notes")) || ["","","","",""];
let tabSettings = JSON.parse(localStorage.getItem("tabSettings")) || [
  {name:"Tab 1", color:"#151522"},
  {name:"Tab 2", color:"#151522"},
  {name:"Tab 3", color:"#151522"},
  {name:"Tab 4", color:"#151522"},
  {name:"Tab 5", color:"#151522"}
];
let activeTab = 0;

function renderTabs() {
  tabsContainer.innerHTML = "";
  tabSettings.forEach((tab,index)=>{
    const tabEl = document.createElement("div");
    tabEl.classList.add("tab");
    tabEl.textContent = tab.name;
    tabEl.style.background = tab.color;
    if(index === activeTab) tabEl.classList.add("active");

    tabEl.addEventListener("click", ()=>{
      saveCurrentTab();
      activeTab = index;
      updateTabs();
      noteArea.innerHTML = notes[activeTab];
    });
    tabEl.addEventListener("dblclick", ()=>{
      const newName = prompt("Enter new tab name:", tab.name);
      if(newName && newName.trim()!==""){
        tabSettings[index].name = newName.trim();
        saveTabSettings();
        renderTabs();
      }
    });
    tabEl.addEventListener("contextmenu", e=>{
      e.preventDefault();
      const newColor = prompt("Enter tab color (hex code, e.g., #ff0000):", tab.color);
      if(newColor && /^#([0-9A-F]{3}){1,2}$/i.test(newColor)){
        tabSettings[index].color = newColor;
        saveTabSettings();
        renderTabs();
      }
    });
    tabEl.draggable = true;
    tabEl.addEventListener("dragstart", e=>{ e.dataTransfer.setData("text/plain", index); });
    tabEl.addEventListener("dragover", e=>{ e.preventDefault(); });
    tabEl.addEventListener("drop", e=>{
      e.preventDefault();
      const fromIndex = parseInt(e.dataTransfer.getData("text/plain"));
      const toIndex = index;
      const tempTab = tabSettings.splice(fromIndex,1)[0];
      tabSettings.splice(toIndex,0,tempTab);
      const tempNote = notes.splice(fromIndex,1)[0];
      notes.splice(toIndex,0,tempNote);
      if(activeTab===fromIndex) activeTab=toIndex;
      saveTabSettings();
      saveNotes();
      renderTabs();
      noteArea.innerHTML = notes[activeTab];
    });

    tabsContainer.appendChild(tabEl);
  });
}
function updateTabs(){ document.querySelectorAll(".tab").forEach((tab,index)=>{ tab.classList.toggle("active", index===activeTab); }); }
function saveCurrentTab(){ notes[activeTab] = noteArea.innerHTML; saveNotes(); }
function saveNotes(){ localStorage.setItem("notes", JSON.stringify(notes)); }
function saveTabSettings(){ localStorage.setItem("tabSettings", JSON.stringify(tabSettings)); }
noteArea.addEventListener("input", saveCurrentTab);
renderTabs();
noteArea.innerHTML = notes[activeTab];

function formatText(cmd){ document.execCommand(cmd,false,null); noteArea.focus(); }
function insertCheckbox(){ 
  const checkbox = document.createElement("input"); 
  checkbox.type="checkbox"; 
  checkbox.style.marginRight="6px"; 
  noteArea.appendChild(checkbox); 
  saveCurrentTab(); 
}

// Color changer
document.getElementById("textColor").addEventListener("input", (e)=>{
  const color = e.target.value;
  document.execCommand("foreColor", false, color);
  noteArea.focus();
});
</script>

</body>
</html>
</html>
