HTML Result  
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Medical Study Checklist</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    min-height: 100vh;
    background: #07070f;
    color: #ddd;
    font-family: 'Georgia', serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding-bottom: 60px;
  }

  .wrap {
    width: 100%;
    max-width: 580px;
    padding: 0 18px;
  }

  /* Header */
  .header {
    padding-top: 32px;
    text-align: center;
    margin-bottom: 22px;
  }
  .header .sub {
    font-size: 10px;
    letter-spacing: 0.3em;
    color: #444;
    text-transform: uppercase;
    font-family: monospace;
  }
  .header h1 {
    font-size: 26px;
    font-weight: 400;
    color: #ececec;
    letter-spacing: -0.02em;
    margin-top: 6px;
  }

  /* Overall progress card */
  .progress-card {
    background: #0f0f1a;
    border: 1px solid #1c1c2e;
    border-radius: 12px;
    padding: 16px 18px;
    margin-bottom: 18px;
  }
  .progress-header {
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-bottom: 10px;
  }
  .progress-label {
    font-size: 10px;
    color: #555;
    letter-spacing: 0.18em;
    text-transform: uppercase;
    font-family: monospace;
  }
  .progress-count {
    font-size: 13px;
    color: #888;
    font-family: monospace;
  }
  .progress-count span {
    font-size: 20px;
    color: #eee;
    font-weight: 300;
  }
  .bar-track {
    height: 5px;
    background: #17172a;
    border-radius: 3px;
    overflow: hidden;
  }
  .bar-fill {
    height: 100%;
    background: linear-gradient(90deg, #e63946, #2196f3, #43a047);
    border-radius: 3px;
    transition: width .5s cubic-bezier(.4,0,.2,1);
  }

  /* Mini subject stats */
  .mini-stats {
    display: flex;
    gap: 8px;
    margin-top: 14px;
  }
  .mini-card {
    flex: 1;
    background: #111120;
    border: 1px solid #1c1c2e;
    border-radius: 8px;
    padding: 10px 10px 8px;
    cursor: pointer;
    transition: all .2s;
  }
  .mini-card.active { background: var(--color-bg); border-color: var(--color-border); }
  .mini-card-label {
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    font-family: monospace;
    margin-bottom: 4px;
  }
  .mini-card-count {
    font-size: 16px;
    color: #ddd;
    font-weight: 300;
    margin-bottom: 6px;
  }
  .mini-card-count small { font-size: 11px; color: #444; }
  .mini-bar { height: 3px; background: #1c1c2e; border-radius: 2px; overflow: hidden; }
  .mini-bar-fill { height: 100%; border-radius: 2px; transition: width .4s; }

  /* Tabs */
  .tabs {
    display: flex;
    border-radius: 10px;
    overflow: hidden;
    border: 1px solid #1c1c2e;
    margin-bottom: 14px;
  }
  .tab-btn {
    flex: 1;
    padding: 11px 4px;
    background: #0c0c18;
    border: none;
    border-right: 1px solid #1c1c2e;
    border-bottom: 2px solid transparent;
    color: #3a3a55;
    cursor: pointer;
    font-size: 11px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    font-family: monospace;
    transition: all .2s;
  }
  .tab-btn:last-child { border-right: none; }
  .tab-btn.active { background: var(--color-bg); border-bottom-color: var(--color); color: var(--accent); }

  /* Subject header */
  .subject-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 12px;
    padding: 0 2px;
  }
  .subject-title {
    font-size: 11px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    font-family: monospace;
  }
  .subject-count {
    font-size: 11px;
    color: #444;
    font-family: monospace;
  }

  /* Topic rows */
  .topic-row {
    display: flex;
    align-items: center;
    gap: 14px;
    padding: 13px 16px;
    margin-bottom: 5px;
    background: #0d0d1c;
    border: 1px solid #181828;
    border-radius: 9px;
    cursor: pointer;
    transition: all .18s cubic-bezier(.4,0,.2,1);
    user-select: none;
  }
  .topic-row.done { background: var(--color-bg); border-color: var(--color-border); }

  .checkbox {
    width: 26px;
    height: 26px;
    border-radius: 50%;
    border: 1.5px solid #2a2a40;
    background: transparent;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    transition: all .18s;
    font-family: monospace;
    font-size: 9px;
    color: #2e2e50;
  }
  .topic-row.done .checkbox {
    background: var(--color);
    border-color: var(--color);
    color: white;
    font-size: 13px;
  }

  .topic-label {
    flex: 1;
    font-size: 14.5px;
    color: #b0b0c8;
    transition: all .18s;
    letter-spacing: 0.01em;
  }
  .topic-row.done .topic-label {
    text-decoration: line-through;
    text-decoration-color: var(--color-half);
    color: var(--accent);
  }

  .badge {
    font-size: 9px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    font-family: monospace;
    color: #222238;
    padding: 3px 8px;
    border-radius: 4px;
    background: transparent;
    border: 1px solid #1a1a2e;
    transition: all .18s;
  }
  .topic-row.done .badge {
    color: var(--accent);
    background: var(--color-light);
    border-color: var(--color-border);
  }

  /* Actions */
  .actions {
    display: flex;
    gap: 8px;
    margin-top: 16px;
  }
  .btn {
    flex: 1;
    padding: 9px 0;
    border-radius: 7px;
    cursor: pointer;
    font-size: 10px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    font-family: monospace;
    transition: all .2s;
    border: 1px solid #1c1c2e;
    background: transparent;
    color: #333;
  }
  .btn.primary {
    background: var(--color-light);
    border-color: var(--color-border);
    color: var(--accent);
  }
  .btn.reset { padding: 9px 14px; flex: 0 0 auto; color: #2a2a40; }

  /* Save indicator */
  .saved-badge {
    text-align: center;
    margin-top: 18px;
    font-size: 10px;
    color: #2a2a40;
    font-family: monospace;
    letter-spacing: 0.12em;
  }
</style>
</head>
<body>

<div class="wrap">
  <div class="header">
    <p class="sub">Medical · Study Tracker</p>
    <h1>Study Checklist</h1>
  </div>

  <!-- Overall progress -->
  <div class="progress-card">
    <div class="progress-header">
      <span class="progress-label">Overall</span>
      <span class="progress-count"><span id="done-count">0</span>/<span id="total-count">0</span> &nbsp;·&nbsp; <span id="done-pct">0</span>%</span>
    </div>
    <div class="bar-track"><div class="bar-fill" id="overall-bar" style="width:0%"></div></div>
    <div class="mini-stats" id="mini-stats"></div>
  </div>

  <!-- Tabs -->
  <div class="tabs" id="tabs"></div>

  <!-- Subject header -->
  <div class="subject-header">
    <span class="subject-title" id="subject-title"></span>
    <span class="subject-count" id="subject-count"></span>
  </div>

  <!-- Topic list -->
  <div id="topic-list"></div>

  <!-- Actions -->
  <div class="actions">
    <button class="btn primary" id="btn-all">✓ All</button>
    <button class="btn" id="btn-clear">✕ Clear</button>
    <button class="btn reset" id="btn-reset">Reset All</button>
  </div>

  <p class="saved-badge" id="saved-badge">● Progress auto-saved</p>
</div>

<script>
const SUBJECTS = {
  Physiology: {
    color: "#e63946", accent: "#ff8a80", icon: "🫀",
    topics: [
      "Blood Pressure 1","Blood Pressure 2","Blood Pressure 3",
      "Blood Physiology 1","Blood Physiology 2","Blood Physiology 3",
      "Respiratory Physiology 1","Respiratory Physiology 2","Respiratory Physiology 3",
      "Renal Physiology 1","Renal Physiology 2","Renal Physiology 3",
      "Digestive System 1","Digestive System 2","Digestive System 3"
    ]
  },
  Anatomy: {
    color: "#2196f3", accent: "#82cfff", icon: "🦴",
    topics: [
      "Respiratory System","Digestive System","Urinary System",
      "Male Reproductive System","Female Reproductive System","Nervous Systems",
      "General Embryology 1","General Embryology 2","General Embryology 3",
      "General Embryology 4","General Embryology 5","General Embryology 6"
    ]
  },
  Histology: {
    color: "#43a047", accent: "#a5d6a7", icon: "🔬",
    topics: [
      "Blood","Adipose Tissue","Cartilage",
      "Bone 1","Bone 2","Muscle 1","Muscle 2",
      "Nervous 1","Nervous 2","Integumentary System"
    ]
  }
};

const STORAGE_KEY = "med_checklist_v1";
let checked = {};
let activeTab = "Physiology";

function allIds() {
  return Object.entries(SUBJECTS).flatMap(([sub, s]) =>
    s.topics.map((_, i) => `${sub}-${i}`)
  );
}

function load() {
  try { checked = JSON.parse(localStorage.getItem(STORAGE_KEY)) || {}; }
  catch { checked = {}; }
}

function save() {
  localStorage.setItem(STORAGE_KEY, JSON.stringify(checked));
  const badge = document.getElementById("saved-badge");
  badge.textContent = "✓ Saved · " + new Date().toLocaleTimeString();
  badge.style.color = "#3a3a55";
  setTimeout(() => { badge.textContent = "● Progress auto-saved"; badge.style.color = "#2a2a40"; }, 2000);
}

function setVars(color, accent) {
  const r = document.documentElement;
  r.style.setProperty("--color", color);
  r.style.setProperty("--accent", accent);
  r.style.setProperty("--color-bg", color + "14");
  r.style.setProperty("--color-border", color + "50");
  r.style.setProperty("--color-half", color + "99");
  r.style.setProperty("--color-light", color + "20");
}

function render() {
  const ids = allIds();
  const doneAll = ids.filter(id => checked[id]).length;
  const total = ids.length;
  const pct = total ? Math.round(doneAll / total * 100) : 0;

  document.getElementById("done-count").textContent = doneAll;
  document.getElementById("total-count").textContent = total;
  document.getElementById("done-pct").textContent = pct;
  document.getElementById("overall-bar").style.width = pct + "%";

  // Mini stats
  const ms = document.getElementById("mini-stats");
  ms.innerHTML = "";
  Object.entries(SUBJECTS).forEach(([name, s]) => {
    const d = s.topics.filter((_, i) => checked[`${name}-${i}`]).length;
    const t = s.topics.length;
    const p = Math.round(d / t * 100);
    const isActive = name === activeTab;
    const card = document.createElement("div");
    card.className = "mini-card" + (isActive ? " active" : "");
    card.style.setProperty("--color", s.color);
    card.style.setProperty("--color-bg", s.color + "18");
    card.style.setProperty("--color-border", s.color + "55");
    card.style.borderTop = `2px solid ${s.color}`;
    card.innerHTML = `
      <div class="mini-card-label" style="color:${s.accent}">${s.icon} ${name.slice(0,4)}</div>
      <div class="mini-card-count">${d}<small>/${t}</small></div>
      <div class="mini-bar"><div class="mini-bar-fill" style="width:${p}%;background:${s.color}"></div></div>`;
    card.onclick = () => { activeTab = name; render(); };
    ms.appendChild(card);
  });

  // Tabs
  const tabsEl = document.getElementById("tabs");
  tabsEl.innerHTML = "";
  Object.entries(SUBJECTS).forEach(([name, s]) => {
    const btn = document.createElement("button");
    btn.className = "tab-btn" + (name === activeTab ? " active" : "");
    btn.style.setProperty("--color", s.color);
    btn.style.setProperty("--color-bg", s.color + "1a");
    btn.style.setProperty("--accent", s.accent);
    btn.textContent = `${s.icon} ${name}`;
    btn.onclick = () => { activeTab = name; render(); };
    tabsEl.appendChild(btn);
  });

  // Active subject
  const s = SUBJECTS[activeTab];
  setVars(s.color, s.accent);
  const subDone = s.topics.filter((_, i) => checked[`${activeTab}-${i}`]).length;
  const subPct = Math.round(subDone / s.topics.length * 100);
  document.getElementById("subject-title").textContent = `${s.icon} ${activeTab}`;
  document.getElementById("subject-title").style.color = s.accent;
  document.getElementById("subject-count").textContent = `${subDone}/${s.topics.length} · ${subPct}%`;

  // Topic list
  const list = document.getElementById("topic-list");
  list.innerHTML = "";
  s.topics.forEach((label, i) => {
    const id = `${activeTab}-${i}`;
    const done = !!checked[id];
    const row = document.createElement("div");
    row.className = "topic-row" + (done ? " done" : "");
    row.style.setProperty("--color", s.color);
    row.style.setProperty("--accent", s.accent);
    row.style.setProperty("--color-bg", s.color + "14");
    row.style.setProperty("--color-border", s.color + "50");
    row.style.setProperty("--color-half", s.color + "99");
    row.style.setProperty("--color-light", s.color + "20");
    row.innerHTML = `
      <div class="checkbox">${done ? "✓" : String(i+1).padStart(2,"0")}</div>
      <span class="topic-label">${label}</span>
      <span class="badge">${done ? "Done" : "—"}</span>`;
    row.onclick = () => {
      checked[id] = !checked[id];
      save();
      render();
    };
    list.appendChild(row);
  });

  // Action labels
  document.getElementById("btn-all").textContent = `✓ All ${activeTab}`;
  document.getElementById("btn-clear").textContent = `✕ Clear ${activeTab}`;
}

document.getElementById("btn-all").onclick = () => {
  SUBJECTS[activeTab].topics.forEach((_, i) => { checked[`${activeTab}-${i}`] = true; });
  save(); render();
};
document.getElementById("btn-clear").onclick = () => {
  SUBJECTS[activeTab].topics.forEach((_, i) => { checked[`${activeTab}-${i}`] = false; });
  save(); render();
};
document.getElementById("btn-reset").onclick = () => {
  if (confirm("Reset all progress?")) { checked = {}; save(); render(); }
};

load();
render();
</script>
</body>
</html>





