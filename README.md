<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>QUARK // Centro de Control Académico</title>
<link rel="manifest" href="manifest.json">
<meta name="theme-color" content="#040011">
<link rel="icon" href="icon-192.png">
<link rel="apple-touch-icon" href="icon-192.png">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800&family=Share+Tech+Mono&family=Rajdhani:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#060a10;
  --bg-deep:#03050a;
  --panel:rgba(18,26,38,0.55);
  --panel-solid:#0d1420;
  --line:rgba(120,200,255,0.12);
  --cyan:#4df3ff;
  --violet:#a37bff;
  --green:#5dffb0;
  --amber:#ffc766;
  --red:#ff6b7a;
  --text:#dfe9f7;
  --text-dim:#7f93ab;
  --radius:14px;
}
*{box-sizing:border-box; margin:0; padding:0;}
body{
  background:
    radial-gradient(ellipse at 20% -10%, rgba(77,243,255,0.08), transparent 50%),
    radial-gradient(ellipse at 90% 10%, rgba(163,123,255,0.08), transparent 45%),
    var(--bg-deep);
  color:var(--text);
  font-family:'Rajdhani', sans-serif;
  min-height:100vh;
  overflow-x:hidden;
}
.scanlines{
  position:fixed; inset:0; pointer-events:none; z-index:999;
  background:repeating-linear-gradient(180deg, rgba(255,255,255,0.015) 0px, rgba(255,255,255,0.015) 1px, transparent 1px, transparent 3px);
  mix-blend-mode:overlay;
}
h1,h2,h3,.mono{font-family:'Orbitron', sans-serif;}
.mono-data{font-family:'Share Tech Mono', monospace;}

/* ---------- Layout ---------- */
.app{display:flex; min-height:100vh;}
.sidebar{
  width:76px; flex-shrink:0;
  background:linear-gradient(180deg, rgba(10,15,24,0.9), rgba(6,10,16,0.9));
  border-right:1px solid var(--line);
  display:flex; flex-direction:column; align-items:center;
  padding:20px 0; gap:6px; position:sticky; top:0; height:100vh;
}
.brand{
  font-family:'Orbitron'; font-weight:800; font-size:13px; letter-spacing:3px;
  color:var(--cyan); margin-bottom:24px; writing-mode:vertical-rl; text-orientation:mixed;
  text-shadow:0 0 12px rgba(77,243,255,0.6);
}
.nav-btn{
  width:52px; height:52px; border-radius:12px; border:1px solid transparent;
  background:transparent; color:var(--text-dim); display:flex; flex-direction:column;
  align-items:center; justify-content:center; gap:2px; cursor:pointer; font-size:20px;
  transition:all .2s ease;
}
.nav-btn span{font-size:8px; font-family:'Share Tech Mono'; letter-spacing:.5px;}
.nav-btn:hover{background:rgba(77,243,255,0.08); color:var(--cyan);}
.nav-btn.active{
  background:rgba(77,243,255,0.12); color:var(--cyan);
  border-color:rgba(77,243,255,0.35); box-shadow:0 0 16px rgba(77,243,255,0.15) inset;
}
.main{flex:1; padding:28px 32px 80px; max-width:1100px; margin:0 auto; width:100%;}
.view{display:none; animation:fadeIn .35s ease;}
.view.active{display:block;}
@keyframes fadeIn{from{opacity:0; transform:translateY(6px);} to{opacity:1; transform:translateY(0);}}

/* ---------- Cards ---------- */
.card{
  background:var(--panel); border:1px solid var(--line); border-radius:var(--radius);
  padding:20px; backdrop-filter:blur(10px); position:relative; overflow:hidden;
}
.card::before{
  content:''; position:absolute; top:0; left:0; right:0; height:1px;
  background:linear-gradient(90deg, transparent, rgba(77,243,255,0.5), transparent);
}
.grid2{display:grid; grid-template-columns:1fr 1fr; gap:18px;}
.grid3{display:grid; grid-template-columns:repeat(3,1fr); gap:16px;}
@media(max-width:800px){.grid2,.grid3{grid-template-columns:1fr;}}

/* ---------- Header / boot ---------- */
.boot{margin-bottom:22px;}
.boot .tag{font-family:'Share Tech Mono'; font-size:11px; color:var(--green); letter-spacing:2px;}
.boot h1{font-size:26px; letter-spacing:1px; margin:6px 0 2px; color:#fff;}
.boot .sub{color:var(--text-dim); font-size:14px;}

.status-line{display:flex; align-items:center; gap:8px; font-family:'Share Tech Mono'; font-size:13px; color:var(--text-dim); margin:3px 0;}
.dot{width:7px; height:7px; border-radius:50%; background:var(--green); box-shadow:0 0 8px var(--green);}
.dot.amber{background:var(--amber); box-shadow:0 0 8px var(--amber);}
.dot.red{background:var(--red); box-shadow:0 0 8px var(--red);}

.recommend{
  margin-top:14px; padding:14px 16px; border-left:2px solid var(--violet);
  background:rgba(163,123,255,0.06); border-radius:0 8px 8px 0; font-size:14px;
}
.recommend b{color:var(--violet);}

/* ---------- Buttons / inputs ---------- */
button{font-family:'Rajdhani'; font-weight:600; cursor:pointer;}
.btn{
  padding:9px 16px; border-radius:9px; border:1px solid var(--line);
  background:rgba(77,243,255,0.08); color:var(--cyan); font-size:13px; letter-spacing:.5px;
  transition:all .15s;
}
.btn:hover{background:rgba(77,243,255,0.18);}
.btn.ghost{background:transparent; color:var(--text-dim);}
.btn.violet{background:rgba(163,123,255,0.1); color:var(--violet); border-color:rgba(163,123,255,0.3);}
.btn.violet:hover{background:rgba(163,123,255,0.2);}
.btn.green{background:rgba(93,255,176,0.1); color:var(--green); border-color:rgba(93,255,176,0.3);}
.btn.red{background:rgba(255,107,122,0.1); color:var(--red); border-color:rgba(255,107,122,0.3);}
.btn.small{padding:5px 10px; font-size:11px;}
input,select,textarea{
  background:rgba(255,255,255,0.03); border:1px solid var(--line); color:var(--text);
  border-radius:8px; padding:9px 11px; font-family:'Rajdhani'; font-size:14px; width:100%;
}
input:focus,select:focus,textarea:focus{outline:none; border-color:var(--cyan);}
label{font-size:11px; color:var(--text-dim); font-family:'Share Tech Mono'; letter-spacing:.5px; display:block; margin-bottom:4px;}

/* ---------- Progress bars ---------- */
.bar-track{width:100%; height:8px; border-radius:6px; background:rgba(255,255,255,0.06); overflow:hidden;}
.bar-fill{height:100%; border-radius:6px; transition:width .4s ease;}

/* ---------- Section titles ---------- */
.section-title{
  font-size:12px; letter-spacing:2px; color:var(--text-dim); margin:26px 0 12px;
  display:flex; align-items:center; gap:10px; text-transform:uppercase;
}
.section-title::after{content:''; flex:1; height:1px; background:var(--line);}

/* ---------- Calendar ---------- */
.cal-head{display:flex; justify-content:space-between; align-items:center; margin-bottom:14px;}
.cal-grid{display:grid; grid-template-columns:repeat(7,1fr); gap:6px;}
.cal-dow{text-align:center; font-size:10px; color:var(--text-dim); font-family:'Share Tech Mono'; padding-bottom:4px;}
.cal-day{
  aspect-ratio:1; border-radius:9px; border:1px solid var(--line); background:rgba(255,255,255,0.02);
  display:flex; flex-direction:column; align-items:center; justify-content:center; cursor:pointer;
  font-family:'Share Tech Mono'; font-size:13px; position:relative; transition:all .15s;
}
.cal-day:hover{border-color:var(--cyan); background:rgba(77,243,255,0.06);}
.cal-day.other{opacity:.25;}
.cal-day.today{border-color:var(--cyan); box-shadow:0 0 10px rgba(77,243,255,0.3) inset;}
.cal-day .dots{display:flex; gap:2px; margin-top:3px;}
.cal-day .dots span{width:4px; height:4px; border-radius:50%;}

/* ---------- Tasks ---------- */
.task{
  display:flex; align-items:center; gap:12px; padding:12px 14px; border:1px solid var(--line);
  border-radius:10px; margin-bottom:8px; background:rgba(255,255,255,0.015);
}
.task.done{opacity:.45;}
.task.done .task-title{text-decoration:line-through;}
.check{
  width:20px; height:20px; border-radius:6px; border:1.5px solid var(--text-dim);
  flex-shrink:0; cursor:pointer; display:flex; align-items:center; justify-content:center; font-size:12px;
}
.check.on{background:var(--green); border-color:var(--green); color:#04140c;}
.task-body{flex:1; min-width:0;}
.task-title{font-size:14px; font-weight:600;}
.task-meta{font-size:11px; color:var(--text-dim); font-family:'Share Tech Mono'; margin-top:2px; display:flex; gap:8px; flex-wrap:wrap;}
.chip{padding:2px 8px; border-radius:20px; font-size:10px; font-family:'Share Tech Mono'; letter-spacing:.5px;}

/* ---------- Subjects ---------- */
.subj-card{padding:16px; border-radius:12px; border:1px solid var(--line); background:rgba(255,255,255,0.02);}
.subj-top{display:flex; justify-content:space-between; align-items:center; margin-bottom:10px;}
.subj-name{font-weight:700; font-size:15px;}
.subj-detail{font-size:12px; color:var(--text-dim); margin-top:8px; display:grid; grid-template-columns:1fr 1fr; gap:4px;}

/* ---------- AI ---------- */
.ai-core{
  width:70px; height:70px; border-radius:50%; margin:0 auto 10px;
  background:radial-gradient(circle at 35% 30%, rgba(77,243,255,0.9), rgba(163,123,255,0.4) 60%, transparent 75%);
  position:relative; box-shadow:0 0 30px rgba(77,243,255,0.35);
}
.ai-core.thinking{animation:pulse 1s ease-in-out infinite;}
@keyframes pulse{0%,100%{transform:scale(1);} 50%{transform:scale(1.08);}}
.chat-log{max-height:340px; overflow-y:auto; display:flex; flex-direction:column; gap:10px; margin-bottom:12px; padding-right:4px;}
.msg{padding:10px 13px; border-radius:10px; font-size:14px; max-width:88%; line-height:1.45;}
.msg.user{align-self:flex-end; background:rgba(77,243,255,0.1); border:1px solid rgba(77,243,255,0.25);}
.msg.ai{align-self:flex-start; background:rgba(163,123,255,0.08); border:1px solid rgba(163,123,255,0.22);}
.msg.system{align-self:center; color:var(--text-dim); font-family:'Share Tech Mono'; font-size:11px;}
.quick-row{display:flex; gap:8px; flex-wrap:wrap; margin-bottom:14px;}
.propose-card{border:1px solid rgba(255,199,102,0.4); background:rgba(255,199,102,0.06); border-radius:10px; padding:12px; margin-bottom:8px;}

/* ---------- Universe ---------- */
.moon-visual{width:64px; height:64px; border-radius:50%; background:#1a2230; position:relative; overflow:hidden; box-shadow:0 0 20px rgba(77,243,255,0.15);}
.moon-shadow{position:absolute; top:0; height:100%; background:#05070a;}

/* ---------- Toggle ---------- */
.toggle{display:inline-flex; align-items:center; gap:10px; cursor:pointer;}
.toggle .track{width:42px; height:22px; border-radius:20px; background:rgba(255,255,255,0.08); position:relative; transition:.2s;}
.toggle .knob{width:16px; height:16px; border-radius:50%; background:var(--text-dim); position:absolute; top:3px; left:3px; transition:.2s;}
.toggle.on .track{background:rgba(93,255,176,0.25);}
.toggle.on .knob{left:23px; background:var(--green);}

.empty{color:var(--text-dim); font-size:13px; text-align:center; padding:20px 0; font-family:'Share Tech Mono';}

/* ---------- Laboratorio ---------- */
.lab-tabs{display:flex; gap:8px; margin-bottom:16px; flex-wrap:wrap;}
.lab-tab{padding:8px 14px; border-radius:9px; border:1px solid var(--line); background:transparent; color:var(--text-dim); font-size:12px; font-family:'Share Tech Mono'; cursor:pointer;}
.lab-tab.active{background:rgba(77,243,255,0.12); color:var(--cyan); border-color:rgba(77,243,255,0.35);}
.lab-panel{display:none;}
.lab-panel.active{display:block;}
.const-row{display:flex; justify-content:space-between; align-items:center; padding:10px 12px; border:1px solid var(--line); border-radius:9px; margin-bottom:6px; background:rgba(255,255,255,0.015);}
.const-name{font-size:13px; font-weight:600;}
.const-sym{color:var(--violet); font-family:'Share Tech Mono'; font-size:12px; margin-left:6px;}
.const-val{font-family:'Share Tech Mono'; font-size:13px; color:var(--cyan); text-align:right;}
.formula-group{margin-bottom:18px;}
.formula-group h4{font-size:13px; letter-spacing:1px; color:var(--text-dim); margin-bottom:8px; text-transform:uppercase;}
.formula-card{display:flex; justify-content:space-between; align-items:flex-start; gap:10px; padding:12px; border:1px solid var(--line); border-radius:9px; margin-bottom:8px; background:rgba(255,255,255,0.015);}
.formula-expr{font-family:'Share Tech Mono'; font-size:15px; color:var(--green); margin-bottom:3px;}
.formula-desc{font-size:12px; color:var(--text-dim);}
.star-btn{background:none; border:none; font-size:16px; color:var(--text-dim); cursor:pointer; flex-shrink:0;}
.star-btn.on{color:var(--amber);}
.conv-row{display:grid; grid-template-columns:1fr auto 1fr; gap:10px; align-items:end; margin-bottom:14px;}
.conv-result{font-family:'Share Tech Mono'; font-size:20px; color:var(--cyan); text-align:center; margin-top:10px;}
::-webkit-scrollbar{width:6px;} ::-webkit-scrollbar-thumb{background:rgba(77,243,255,0.2); border-radius:6px;}
</style>
</head>
<body>
<div class="scanlines"></div>
<div class="app">
  <div class="sidebar">
    <div class="brand">QUARK</div>
    <button class="nav-btn active" data-view="control">⌘<span>CONTROL</span></button>
    <button class="nav-btn" data-view="calendar">📅<span>CALEND</span></button>
    <button class="nav-btn" data-view="subjects">📚<span>MATERIAS</span></button>
    <button class="nav-btn" data-view="tasks">✓<span>TAREAS</span></button>
    <button class="nav-btn" data-view="lab">⚛<span>LAB</span></button>
    <button class="nav-btn" data-view="stats">📊<span>STATS</span></button>
    <button class="nav-btn" data-view="ai">◈<span>IA</span></button>
    <button class="nav-btn" data-view="universe">☾<span>UNIVERSO</span></button>
    <button class="nav-btn" data-view="settings">⚙<span>CONFIG</span></button>
  </div>

  <div class="main">

    <!-- CONTROL -->
    <div class="view active" id="view-control">
      <div class="boot">
        <div class="tag" id="bootTag">SISTEMA INICIADO</div>
        <h1 id="greeting">Buenos días, Sae.</h1>
        <div class="sub mono-data" id="todayLong"></div>
      </div>
      <div class="grid2">
        <div class="card">
          <div class="status-line"><span class="dot" id="dotTasks"></span><span id="statTasks">-- tareas pendientes</span></div>
          <div class="status-line"><span class="dot green"></span><span id="statSubjects">-- materias activas</span></div>
          <div class="status-line"><span class="dot amber" id="dotExam"></span><span id="statExam">Sin exámenes cargados</span></div>
          <div class="recommend" id="recommendBox"><b>Recomendación:</b> <span id="recommendText">cargá tareas y materias para recibir sugerencias.</span></div>
        </div>
        <div class="card">
          <h3 style="font-size:13px; letter-spacing:1px; color:var(--text-dim); margin-bottom:10px;">UNIVERSO HOY</h3>
          <div style="display:flex; align-items:center; gap:14px;">
            <div class="moon-visual" id="moonVisualMini"><div class="moon-shadow" id="moonShadowMini"></div></div>
            <div>
              <div style="font-size:14px; font-weight:700;" id="moonNameMini">--</div>
              <div class="mono-data" style="font-size:12px; color:var(--text-dim);" id="moonPctMini">--% iluminada</div>
              <div class="mono-data" style="font-size:11px; color:var(--text-dim); margin-top:6px;" id="sunTimesMini">☀ -- / -- </div>
            </div>
          </div>
        </div>
      </div>

      <div class="section-title">AUTOPILOTO</div>
      <div class="card" style="display:flex; justify-content:space-between; align-items:center;">
        <div>
          <div style="font-weight:700; font-size:14px;" id="autopilotLabel">🔴 Autopiloto desactivado</div>
          <div style="font-size:12px; color:var(--text-dim); margin-top:3px;">La IA puede sugerir reorganizar tu agenda. Nunca borra ni edita sin tu confirmación.</div>
        </div>
        <div class="toggle" id="autopilotToggle"><div class="track"><div class="knob"></div></div></div>
      </div>
    </div>

    <!-- CALENDAR -->
    <div class="view" id="view-calendar">
      <div class="cal-head">
        <button class="btn ghost" id="calPrev">◀</button>
        <h2 id="calMonthLabel" style="font-size:16px; letter-spacing:1px;"></h2>
        <button class="btn ghost" id="calNext">▶</button>
      </div>
      <div class="cal-grid" id="calDow"></div>
      <div class="cal-grid" id="calGrid" style="margin-top:6px;"></div>

      <div id="dayPanel" style="display:none;">
        <div class="section-title" id="dayPanelTitle">DÍA</div>
        <div class="card">
          <div id="dayTasks"></div>
          <button class="btn small" id="addTaskFromDay" style="margin-top:10px;">+ Agregar tarea este día</button>
        </div>
      </div>
    </div>

    <!-- SUBJECTS -->
    <div class="view" id="view-subjects">
      <div class="section-title">MATERIAS</div>
      <div id="subjectsGrid" class="grid2"></div>
      <button class="btn violet" id="addSubjectBtn" style="margin-top:16px;">+ Nueva materia</button>
    </div>

    <!-- TASKS -->
    <div class="view" id="view-tasks">
      <div class="section-title">TAREAS</div>
      <div style="display:flex; gap:8px; margin-bottom:14px; flex-wrap:wrap;">
        <select id="taskFilter" style="width:auto;">
          <option value="all">Todas</option>
          <option value="pending">Pendientes</option>
          <option value="done">Completadas</option>
        </select>
        <button class="btn" id="addTaskBtn">+ Nueva tarea</button>
      </div>
      <div id="tasksList"></div>
    </div>

    <!-- LAB -->
    <div class="view" id="view-lab">
      <div class="section-title">LABORATORIO — FÍSICA</div>
      <div class="lab-tabs">
        <button class="lab-tab active" data-lab="constants">Constantes</button>
        <button class="lab-tab" data-lab="formulas">Fórmulas</button>
        <button class="lab-tab" data-lab="converter">Conversor de unidades</button>
      </div>

      <div class="lab-panel active" id="lab-constants">
        <input id="constSearch" placeholder="Buscar constante (ej: gravitación, Planck, c)..." style="margin-bottom:14px;">
        <div class="card" id="constList"></div>
      </div>

      <div class="lab-panel" id="lab-formulas">
        <div style="margin-bottom:12px;">
          <button class="btn small" id="favFilterBtn">⭐ Ver solo favoritas</button>
        </div>
        <div id="formulasList"></div>
      </div>

      <div class="lab-panel" id="lab-converter">
        <div class="card">
          <label>Categoría</label>
          <select id="convCategory" style="margin-bottom:14px;"></select>
          <div class="conv-row">
            <div><label>Valor</label><input id="convValue" type="number" value="1"></div>
            <div style="padding-bottom:9px; color:var(--text-dim);">→</div>
            <div><label>De</label><select id="convFrom"></select></div>
          </div>
          <label>A</label><select id="convTo" style="margin-bottom:6px;"></select>
          <div class="conv-result" id="convResult">--</div>
        </div>
      </div>
    </div>

    <!-- STATS -->
    <div class="view" id="view-stats">
      <div class="section-title">ESTADÍSTICAS</div>
      <div class="grid3">
        <div class="card"><div class="mono-data" style="font-size:11px; color:var(--text-dim);">RACHA</div><div style="font-size:28px; font-weight:800; color:var(--cyan);" id="statStreak">0</div><div style="font-size:11px; color:var(--text-dim);">días seguidos</div></div>
        <div class="card"><div class="mono-data" style="font-size:11px; color:var(--text-dim);">COMPLETADAS</div><div style="font-size:28px; font-weight:800; color:var(--green);" id="statDonePct">0%</div><div style="font-size:11px; color:var(--text-dim);">del total</div></div>
        <div class="card"><div class="mono-data" style="font-size:11px; color:var(--text-dim);">MATERIA TOP</div><div style="font-size:20px; font-weight:800; color:var(--violet);" id="statTopSubject">--</div><div style="font-size:11px; color:var(--text-dim);">más tareas activas</div></div>
      </div>
      <div class="section-title">TAREAS POR MATERIA</div>
      <div class="card" id="subjectBars"></div>
    </div>

    <!-- AI -->
    <div class="view" id="view-ai">
      <div style="text-align:center; margin-bottom:8px;">
        <div class="ai-core" id="aiCore"></div>
        <div class="mono-data" style="font-size:11px; color:var(--text-dim);">QUARK IA</div>
      </div>
      
    <!-- UNIVERSE -->
    <div class="view" id="view-universe">
      <div class="section-title">UNIVERSO HOY</div>
      <div class="grid2">
        <div class="card" style="text-align:center;">
          <div class="moon-visual" id="moonVisual" style="width:96px; height:96px; margin:0 auto 12px;"><div class="moon-shadow" id="moonShadow"></div></div>
          <div style="font-weight:700; font-size:16px;" id="moonName">--</div>
          <div class="mono-data" style="color:var(--text-dim); font-size:13px;" id="moonPct">-- % iluminada</div>
        </div>
        <div class="card">
          <div class="status-line">☀ <span id="sunrise">--:--</span> amanecer</div>
          <div class="status-line">🌇 <span id="sunset">--:--</span> atardecer</div>
          <div class="status-line mono-data" style="font-size:11px; margin-top:10px; color:var(--text-dim);" id="locLabel">Ubicación: --</div>
        </div>
      </div>
      <div class="section-title">NOTA</div>
      <div class="card" style="font-size:13px; color:var(--text-dim);">
        La fase lunar y los horarios de sol se calculan matemáticamente en tu navegador (sin conexión a servicios externos), por eso son una muy buena aproximación. El planetario 3D, el tracking de la ISS y las posiciones planetarias en vivo quedan para una fase futura del proyecto — requieren APIs astronómicas dedicadas.
      </div>
    </div>

    <!-- SETTINGS -->
    <div class="view" id="view-settings">
      <div class="section-title">CONFIGURACIÓN</div>
      <div class="card" style="display:flex; flex-direction:column; gap:16px;">
        <div>
          <label>Tu nombre</label>
          <input id="settingsName" placeholder="Sae">
        </div>
        <div>
          <button class="btn red" id="resetData">Borrar todos los datos</button>
        </div>
      </div>
    </div>

  </div>
</div>

<!-- Modal -->
<div id="modalOverlay" style="display:none; position:fixed; inset:0; background:rgba(3,5,10,0.7); backdrop-filter:blur(4px); z-index:200; align-items:center; justify-content:center;">
  <div class="card" id="modalBox" style="width:min(420px,90vw); max-height:85vh; overflow-y:auto;"></div>
</div>

<script>
/* ================= STORAGE HELPERS ================= */
async function sGet(key, fallback){
  try{ const r = await window.storage.get(key); return r ? JSON.parse(r.value) : fallback; }
  catch(e){ return fallback; }
}
async function sSet(key, value){
  try{ await window.storage.set(key, JSON.stringify(value)); }catch(e){ console.error('storage error', e); }
}
function uid(){ return Math.random().toString(36).slice(2,10); }
function todayISO(){ const d=new Date(); return d.toISOString().slice(0,10); }

/* ================= STATE ================= */
let STATE = {
  name:'Sae',
  autopilot:false,
  subjects:[],
  tasks:[],
  streakLog:[],
  chat:[]
};
let calCursor = new Date();
let selectedDay = null;

const SUBJECT_DEFAULTS = [
  {name:'Física', color:'#4df3ff'},
  {name:'Matemática', color:'#5dffb0'},
  {name:'Campo Teórico de la Práctica', color:'#a37bff'},
  {name:'Cultura Digital y Educación', color:'#ffc766'},
  {name:'Introducción a los Sistemas Biológicos', color:'#ff6b7a'},
];

async function loadState(){
  STATE.name = await sGet('settings-name', 'Sae');
  STATE.autopilot = await sGet('settings-autopilot', false);
  STATE.subjects = await sGet('subjects', SUBJECT_DEFAULTS.map(s=>({id:uid(), name:s.name, color:s.color, professor:'', horario:'', promedio:'', progress:0})));
  STATE.tasks = await sGet('tasks', []);
  STATE.streakLog = await sGet('streak-log', []);
  STATE.chat = await sGet('ai-chat-log', []);
}
async function saveSubjects(){ await sSet('subjects', STATE.subjects); }
async function saveTasks(){ await sSet('tasks', STATE.tasks); }
async function saveStreak(){ await sSet('streak-log', STATE.streakLog); }
async function saveChat(){ await sSet('ai-chat-log', STATE.chat.slice(-24)); }

/* ================= NAVIGATION ================= */
document.querySelectorAll('.nav-btn').forEach(btn=>{
  btn.addEventListener('click', ()=>{
    document.querySelectorAll('.nav-btn').forEach(b=>b.classList.remove('active'));
    document.querySelectorAll('.view').forEach(v=>v.classList.remove('active'));
    btn.classList.add('active');
    document.getElementById('view-'+btn.dataset.view).classList.add('active');
    if(btn.dataset.view==='stats') renderStats();
    if(btn.dataset.view==='subjects') renderSubjects();
    if(btn.dataset.view==='tasks') renderTasks();
    if(btn.dataset.view==='calendar') renderCalendar();
    if(btn.dataset.view==='lab') renderLabConstants();
  });
});

/* ================= MODAL ================= */
function openModal(html){
  document.getElementById('modalBox').innerHTML = html;
  document.getElementById('modalOverlay').style.display='flex';
}
function closeModal(){ document.getElementById('modalOverlay').style.display='none'; }
document.getElementById('modalOverlay').addEventListener('click', e=>{ if(e.target.id==='modalOverlay') closeModal(); });

/* ================= DASHBOARD ================= */
function greetingWord(){
  const h = new Date().getHours();
  if(h<12) return 'Buenos días';
  if(h<19) return 'Buenas tardes';
  return 'Buenas noches';
}
function renderDashboard(){
  document.getElementById('greeting').textContent = `${greetingWord()}, ${STATE.name}.`;
  document.getElementById('todayLong').textContent = new Date().toLocaleDateString('es-AR',{weekday:'long', day:'numeric', month:'long', year:'numeric'});

  const pending = STATE.tasks.filter(t=>!t.done);
  document.getElementById('statTasks').textContent = `${pending.length} tarea${pending.length!==1?'s':''} pendiente${pending.length!==1?'s':''}`;
  document.getElementById('dotTasks').className = 'dot ' + (pending.length>5?'red':pending.length>0?'amber':'');
  document.getElementById('statSubjects').textContent = `${STATE.subjects.length} materia${STATE.subjects.length!==1?'s':''} activa${STATE.subjects.length!==1?'s':''}`;

  const exams = STATE.tasks.filter(t=>t.isExam && !t.done && t.date).sort((a,b)=>a.date.localeCompare(b.date));
  if(exams.length){
    const days = Math.ceil((new Date(exams[0].date) - new Date(todayISO()))/86400000);
    document.getElementById('statExam').textContent = `${exams[0].title} en ${days} día${days!==1?'s':''}`;
    document.getElementById('dotExam').className = 'dot ' + (days<=3?'red':'amber');
  } else {
    document.getElementById('statExam').textContent = 'Sin exámenes cargados';
  }

  // recommendation (local heuristic, no AI call needed for dashboard)
  let rec = 'Todo tranquilo. Buen momento para adelantar algo de lectura.';
  if(exams.length && Math.ceil((new Date(exams[0].date)-new Date(todayISO()))/86400000) <= 5){
    rec = `Repasar para "${exams[0].title}" — quedan pocos días.`;
  } else if(pending.length>0){
    const bySubj={};
    pending.forEach(t=>{bySubj[t.subject]=(bySubj[t.subject]||0)+1;});
    const top = Object.entries(bySubj).sort((a,b)=>b[1]-a[1])[0];
    if(top) rec = `Tenés ${top[1]} tarea(s) de ${top[0]} pendientes. Es un buen bloque para hoy.`;
  }
  document.getElementById('recommendText').textContent = rec;

  // autopilot toggle visual
  const t = document.getElementById('autopilotToggle');
  t.classList.toggle('on', STATE.autopilot);
  document.getElementById('autopilotLabel').textContent = STATE.autopilot ? '🟢 Autopiloto activado' : '🔴 Autopiloto desactivado';

  renderUniverseMini();
}
document.getElementById('autopilotToggle').addEventListener('click', async ()=>{
  STATE.autopilot = !STATE.autopilot;
  await sSet('settings-autopilot', STATE.autopilot);
  renderDashboard();
});
     
/* ================= SUBJECTS ================= */
function renderSubjects(){
  const grid = document.getElementById('subjectsGrid');
  if(!STATE.subjects.length){ grid.innerHTML = '<div class="empty">Sin materias todavía.</div>'; return; }
  grid.innerHTML = STATE.subjects.map(s=>{
    const pending = STATE.tasks.filter(t=>t.subject===s.name && !t.done).length;
    return `<div class="subj-card">
      <div class="subj-top">
        <div style="display:flex; align-items:center; gap:8px;">
          <span style="width:10px;height:10px;border-radius:50%;background:${s.color};box-shadow:0 0 8px ${s.color};display:inline-block;"></span>
          <span class="subj-name">${s.name}</span>
        </div>
        <button class="btn ghost small" onclick="editSubject('${s.id}')">✎</button>
      </div>
      <div class="bar-track"><div class="bar-fill" style="width:${s.progress||0}%; background:${s.color};"></div></div>
      <div class="subj-detail">
        <div>Prof: ${s.professor||'--'}</div>
        <div>Horario: ${s.horario||'--'}</div>
        <div>Promedio: ${s.promedio||'--'}</div>
        <div>Pendientes: ${pending}</div>
      </div>
    </div>`;
  }).join('');
}
window.editSubject = function(id){
  const s = STATE.subjects.find(x=>x.id===id);
  openModal(`
    <h3 style="margin-bottom:14px;">${s.name}</h3>
    <label>Profesor/a</label><input id="mProf" value="${s.professor||''}" style="margin-bottom:10px;">
    <label>Horario</label><input id="mHor" value="${s.horario||''}" style="margin-bottom:10px;">
    <label>Promedio</label><input id="mProm" value="${s.promedio||''}" style="margin-bottom:10px;">
    <label>Avance (%)</label><input id="mProg" type="number" min="0" max="100" value="${s.progress||0}" style="margin-bottom:16px;">
    <div style="display:flex; gap:8px;">
      <button class="btn" id="mSave">Guardar</button>
      <button class="btn red" id="mDelete">Eliminar materia</button>
      <button class="btn ghost" onclick="closeModal()">Cancelar</button>
    </div>
  `);
  document.getElementById('mSave').onclick = async ()=>{
    s.professor=document.getElementById('mProf').value;
    s.horario=document.getElementById('mHor').value;
    s.promedio=document.getElementById('mProm').value;
    s.progress=Number(document.getElementById('mProg').value)||0;
    await saveSubjects(); closeModal(); renderSubjects(); renderDashboard();
  };
  document.getElementById('mDelete').onclick = async ()=>{
    STATE.subjects = STATE.subjects.filter(x=>x.id!==id);
    await saveSubjects(); closeModal(); renderSubjects(); renderDashboard();
  };
};
document.getElementById('addSubjectBtn').addEventListener('click', ()=>{
  openModal(`
    <h3 style="margin-bottom:14px;">Nueva materia</h3>
    <label>Nombre</label><input id="nName" style="margin-bottom:10px;">
    <label>Color</label><input id="nColor" type="color" value="#4df3ff" style="margin-bottom:16px; height:38px;">
    <div style="display:flex; gap:8px;">
      <button class="btn" id="nSave">Crear</button>
      <button class="btn ghost" onclick="closeModal()">Cancelar</button>
    </div>
  `);
  document.getElementById('nSave').onclick = async ()=>{
    const name = document.getElementById('nName').value.trim();
    if(!name) return;
    STATE.subjects.push({id:uid(), name, color:document.getElementById('nColor').value, professor:'', horario:'', promedio:'', progress:0});
    await saveSubjects(); closeModal(); renderSubjects();
  };
});
