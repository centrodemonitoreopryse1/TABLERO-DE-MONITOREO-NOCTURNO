[index.html.html](https://github.com/user-attachments/files/32068454/index.html.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tablero de Guardia — Monitoreo Nocturno 01–10/09/2026</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=Inter:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.4/chart.umd.min.js"></script>
<style>
  :root{
    --bg: #0A1220; --panel: #101B31; --panel-2: #0D1728;
    --border: #1E2D48; --border-soft: #16233B; --text: #E7EDF7; --text-muted: #8AA0C2; --text-dim: #566A8E;
    --teal: #2AC9B8; --teal-soft: rgba(42,201,184,0.12); --amber: #F0A93E; --amber-soft: rgba(240,169,62,0.14);
    --red: #F14C6B; --red-soft: rgba(241,76,107,0.14); --green: #33C077; --green-soft: rgba(51,192,119,0.13);
    --display: 'Space Grotesk', sans-serif; --body: 'Inter', sans-serif; --mono: 'IBM Plex Mono', monospace;
  }
  *{ box-sizing:border-box; }
  html,body{ margin:0; padding:0; }
  body{
    background:
      radial-gradient(1100px 500px at 12% -10%, rgba(42,201,184,0.10), transparent 60%),
      radial-gradient(900px 500px at 100% 0%, rgba(240,169,62,0.06), transparent 55%),
      var(--bg);
    color: var(--text); font-family: var(--body); line-height: 1.5; padding: 0 0 64px 0;
  }
  ::selection{ background: var(--teal); color:#062420; }
  .masthead{
    border-bottom: 1px solid var(--border-soft);
    padding: 28px clamp(18px, 4vw, 56px) 22px;
    display:flex; justify-content:space-between; align-items:flex-end; gap: 24px; flex-wrap: wrap; position: relative;
  }
  .masthead::before{
    content:""; position:absolute; left:0; right:0; top:0; height:2px;
    background: linear-gradient(90deg, transparent, var(--teal) 20%, var(--teal) 80%, transparent); opacity:0.55;
  }
  .brand-row{ display:flex; align-items:center; gap:12px; margin-bottom:10px; }
  .brand-mark{
    width:34px; height:34px; border-radius:9px;
    background: linear-gradient(135deg, var(--teal), #157A6E);
    display:flex; align-items:center; justify-content:center;
    font-family: var(--mono); font-weight:600; font-size:13px; color:#04201B; flex-shrink:0;
  }
  .eyebrow{ font-family: var(--mono); font-size:11.5px; letter-spacing:.14em; text-transform:uppercase; color: var(--text-dim); }
  h1{ font-family: var(--display); font-weight:600; font-size: clamp(24px, 3.4vw, 34px); margin: 2px 0 6px; letter-spacing:-0.01em; }
  .sub{ color: var(--text-muted); font-size:14px; max-width: 720px; }
  .status-pill{
    font-family: var(--mono); font-size:12.5px; letter-spacing:.03em;
    display:inline-flex; align-items:center; gap:8px;
    background: var(--panel); border:1px solid var(--border); padding: 9px 14px; border-radius: 999px; color: var(--text-muted);
  }
  .dot{ width:8px; height:8px; border-radius:50%; background: var(--green); box-shadow:0 0 0 3px var(--green-soft); animation: pulse 2.4s infinite ease-in-out; }
  @keyframes pulse{ 0%,100%{ opacity:1;} 50%{ opacity:.4;} }
  .wrap{ padding: 30px clamp(18px, 4vw, 56px) 0; max-width: 1360px; margin:0 auto; }
  section{ margin-bottom: 40px; }
  .section-head{ display:flex; align-items:baseline; gap:10px; margin-bottom:16px; flex-wrap:wrap; }
  .section-num{ font-family: var(--mono); color: var(--teal); font-size:12.5px; }
  .section-title{ font-family: var(--display); font-size:19px; font-weight:600; }
  .section-note{ color: var(--text-dim); font-size:12.5px; margin-left:auto; font-family: var(--mono); }
  .kpis{ display:grid; grid-template-columns: repeat(5, 1fr); gap:14px; }
  @media (max-width: 980px){ .kpis{ grid-template-columns: repeat(2,1fr);} }
  .kpi{
    background: linear-gradient(180deg, var(--panel), var(--panel-2));
    border:1px solid var(--border); border-radius:14px; padding:18px 18px 16px;
  }
  .kpi .label{ font-size:11.5px; color:var(--text-dim); text-transform:uppercase; letter-spacing:.08em; font-family: var(--mono); }
  .kpi .num{ font-family: var(--display); font-size: 32px; font-weight:600; margin-top:8px; }
  .kpi .foot{ font-size:12px; color: var(--text-muted); margin-top:4px; }
  .kpi.accent-red .num{ color: var(--red); }
  .kpi.accent-amber .num{ color: var(--amber); }
  .kpi.accent-green .num{ color: var(--green); }
  .kpi.accent-teal .num{ color: var(--teal); }
  .timeline-card{ background: var(--panel); border:1px solid var(--border); border-radius:14px; padding: 22px clamp(14px,3vw,26px) 18px; }
  .timeline-legend{ display:flex; gap:18px; margin-bottom:14px; flex-wrap:wrap; font-size:12px; color:var(--text-muted); font-family: var(--mono);}
  .legend-item{ display:flex; align-items:center; gap:7px; }
  .legend-swatch{ width:9px; height:9px; border-radius:2px; }
  .timeline-axis{ position:relative; height: 96px; }
  .timeline-line{ position:absolute; left:0; right:0; top:48px; height:1px; background: var(--border); }
  .timeline-hourmarks{ position:absolute; left:0; right:0; top:64px; height:20px; }
  .hm{ position:absolute; transform: translateX(-50%); font-family: var(--mono); font-size:10.5px; color: var(--text-dim); }
  .hm::before{ content:""; position:absolute; left:50%; top:-16px; width:1px; height:8px; background:var(--border-soft); }
  .tpoint{ position:absolute; top:38px; width:13px; height:13px; border-radius:50%; transform: translateX(-50%); border: 2px solid var(--bg); cursor: default; }
  .tpoint.ok{ background: var(--green); box-shadow:0 0 0 3px var(--green-soft); }
  .tpoint.late{ background: var(--amber); box-shadow:0 0 0 3px var(--amber-soft); }
  .tpoint .tip{
    visibility:hidden; opacity:0; position:absolute; bottom:22px; left:50%; transform: translateX(-50%);
    background:#050B15; border:1px solid var(--border); color:var(--text); font-size:11px;
    font-family: var(--mono); padding:6px 9px; border-radius:8px; white-space:nowrap; z-index:5; transition: opacity .15s ease;
  }
  .tpoint:hover .tip{ visibility:visible; opacity:1; }
  .table-card{ background: var(--panel); border:1px solid var(--border); border-radius:14px; overflow:hidden; overflow-x:auto; }
  table{ width:100%; border-collapse:collapse; font-size:13.5px; }
  thead th{
    text-align:left; font-family: var(--mono); font-size:11px; text-transform:uppercase; letter-spacing:.06em;
    color: var(--text-dim); padding:13px 16px; border-bottom:1px solid var(--border); background: var(--panel-2);
  }
  tbody td{ padding:12px 16px; border-bottom:1px solid var(--border-soft); color: var(--text); vertical-align:top; }
  tbody tr:last-child td{ border-bottom:none; }
  tbody tr:hover{ background: rgba(255,255,255,0.02); }
  td.num, th.num{ font-family: var(--mono); text-align:right; }
  .badge{ display:inline-flex; align-items:center; gap:6px; padding:4px 10px; border-radius:999px; font-family: var(--mono); font-size:11px; letter-spacing:.03em; white-space:nowrap; }
  .badge.ok{ background: var(--green-soft); color: var(--green); }
  .badge.dev{ background: var(--amber-soft); color: var(--amber); }
  .badge-dot{ width:6px; height:6px; border-radius:50%; background:currentColor; }
  .muted{ color: var(--text-muted); }
  .two-col{ display:grid; grid-template-columns: 1fr 1.15fr; gap: 20px; align-items:start; }
  @media (max-width: 980px){ .two-col{ grid-template-columns:1fr; } }
  .empty-box{
    border:1px dashed var(--border); border-radius:10px; padding:20px; color: var(--text-dim);
    font-size:13.5px; text-align:center; background: var(--panel);
  }
  .dev-item{ border:1px solid var(--border); border-left: 3px solid var(--amber); background: var(--panel); border-radius:10px; padding:14px 16px; margin-bottom:12px; }
  .dev-item .row1{ display:flex; justify-content:space-between; align-items:center; margin-bottom:6px; gap:8px; flex-wrap:wrap; }
  .dev-item .ooad{ font-family: var(--display); font-weight:600; font-size:15px; }
  .dev-item .hora{ font-family: var(--mono); color: var(--amber); font-size:13px; }
  .dev-item .who{ font-size:12.5px; color:var(--text-muted); margin-bottom:4px; }
  .dev-item .note{ font-size:12.5px; color: var(--text-dim); }
  .hito-item{ border:1px solid var(--border); background: var(--panel); border-radius:10px; padding:14px 16px; margin-bottom:12px; border-left: 3px solid var(--amber); }
  .hito-item .row1{ display:flex; justify-content:space-between; gap:10px; margin-bottom:6px; flex-wrap:wrap; }
  .hito-item .title{ font-family: var(--display); font-weight:600; font-size:14px; }
  .hito-item .meta{ font-family: var(--mono); font-size:11px; color: var(--text-dim); white-space:nowrap; }
  .hito-item .loc{ font-size:12px; color: var(--text-muted); margin-bottom:5px; }
  .hito-item .note{ font-size:12.5px; color: var(--text-muted); }
  .reg-grid{ display:grid; grid-template-columns: 1.3fr 1fr; gap:20px; }
  @media (max-width: 980px){ .reg-grid{ grid-template-columns:1fr; } }
  .reg-card{ background: var(--panel); border:1px solid var(--border); border-radius:14px; padding:20px; }
  .reg-stats{ display:grid; grid-template-columns:1fr 1fr; gap:12px; margin-bottom: 6px;}
  .stat-box{ background: var(--panel-2); border:1px solid var(--border-soft); border-radius:10px; padding:12px 14px; }
  .stat-box .k{ font-family: var(--mono); font-size:10.5px; color:var(--text-dim); text-transform:uppercase; letter-spacing:.06em; }
  .stat-box .v{ font-family: var(--display); font-size:20px; font-weight:600; margin-top:4px; }
  .chart-wrap{ height: 220px; margin-top: 8px; }
  .reg-notes{ font-size:13px; color: var(--text-muted); }
  .reg-notes li{ margin-bottom:8px; }
  .err-card{ background: var(--panel); border:1px solid var(--border); border-radius:14px; padding: 6px 0; }
  .err-item{ display:flex; gap:12px; padding: 13px 20px; border-bottom:1px solid var(--border-soft); font-size:13.5px; color: var(--text-muted); }
  .err-item:last-child{ border-bottom:none; }
  .err-icon{ font-family: var(--mono); color: var(--amber); flex-shrink:0; font-size:12px; margin-top:2px; }
  footer{
    max-width:1360px; margin: 40px auto 0; padding: 20px clamp(18px,4vw,56px) 0;
    border-top:1px solid var(--border-soft); color: var(--text-dim); font-size:12px; font-family: var(--mono);
    display:flex; justify-content:space-between; flex-wrap:wrap; gap:8px;
  }
</style>
</head>
<body>
<div class="masthead">
  <div>
    <div class="brand-row">
      <div class="brand-mark">CE</div>
      <span class="eyebrow">Centro de Enlace · Monitoreo Nocturno PRYSE</span>
    </div>
    <h1>Tablero de Avances — Monitoreo 01–10/09/2026</h1>
    <div class="sub">Supervisiones virtuales, inicios/cierres de turno e incidencias detectadas en guardia nocturna (Kevin Maldonado e Israel Pérez). No es bitácora de OOAD estatales.</div>
  </div>
  <div class="status-pill"><span class="dot"></span> 10/10 noches con cierre · 84 supervisiones</div>
</div>
<div class="wrap">
  <section><div class="kpis" id="kpiGrid"></div></section>
  <section>
    <div class="section-head">
      <span class="section-num">01</span>
      <span class="section-title">Línea de tiempo — cierres de turno de monitoreo</span>
      <span class="section-note">05:30 – 06:30 hrs</span>
    </div>
    <div class="timeline-card">
      <div class="timeline-legend">
        <div class="legend-item"><span class="legend-swatch" style="background:var(--green)"></span> Cierre OK</div>
        <div class="legend-item"><span class="legend-swatch" style="background:var(--amber)"></span> Cierre con observación (SIN RELEVANCIA / +3 min)</div>
      </div>
      <div class="timeline-axis" id="timelineAxis"></div>
    </div>
  </section>
  <section>
    <div class="section-head">
      <span class="section-num">02</span>
      <span class="section-title">Estatus por coordinador y por noche</span>
      <span class="section-note">01–10/09</span>
    </div>
    <div class="table-card" style="margin-bottom:16px;">
      <table>
        <thead>
          <tr>
            <th>Coordinador</th>
            <th class="num">Registros</th>
            <th class="num">Completos</th>
            <th class="num">Sin relevancia</th>
            <th>Estatus</th>
          </tr>
        </thead>
        <tbody id="coordTableBody"></tbody>
      </table>
    </div>
    <div class="table-card">
      <table>
        <thead>
          <tr>
            <th>Noche</th>
            <th class="num">Regs</th>
            <th class="num">Supervisiones</th>
            <th>Cierre</th>
            <th>Hora cierre</th>
            <th>Coordinador cierre</th>
            <th class="num">Sin relevancia</th>
          </tr>
        </thead>
        <tbody id="dayTableBody"></tbody>
      </table>
    </div>
  </section>
  <section>
    <div class="section-head">
      <span class="section-num">03</span>
      <span class="section-title">Observaciones de cierre e hitos</span>
    </div>
    <div class="two-col">
      <div>
        <div class="section-title" style="font-size:14px; color:var(--amber); margin-bottom:10px;">Cierres con observación</div>
        <div id="devList"></div>
      </div>
      <div>
        <div class="section-title" style="font-size:14px; color:var(--amber); margin-bottom:10px;">Incidentes relevantes (hitos)</div>
        <div id="hitoList"></div>
      </div>
    </div>
  </section>
  <section>
    <div class="section-head">
      <span class="section-num">04</span>
      <span class="section-title">Análisis de regresión — retraso de cierre</span>
      <span class="section-note">Cierres de turno · n=10</span>
    </div>
    <div class="reg-grid">
      <div class="reg-card"><div class="chart-wrap"><canvas id="regChart"></canvas></div></div>
      <div class="reg-card">
        <div class="reg-stats" id="regStats"></div>
        <ul class="reg-notes" id="regNotes" style="margin-top:14px; padding-left:18px;"></ul>
      </div>
    </div>
  </section>
  <section>
    <div class="section-head">
      <span class="section-num">05</span>
      <span class="section-title">Errores e inconsistencias detectadas en limpieza</span>
    </div>
    <div class="err-card" id="errList"></div>
  </section>
</div>
<footer>
  <span>Fuente: TABLA MONITOREO.xlsx · 01–10/09/2026 · registros limpiados</span>
  <span>Tablero de avances · Monitoreo nocturno</span>
</footer>
<script>
const DASH = {"meta": {"fecha": "01–10/09/2026", "total_filas": 105, "registros_reales": 105, "completo": 79, "sinrel": 26, "fuera": 0, "supervisiones": 84, "cierres": 10, "inicios": 8, "codigos_plata": 3, "coord_kevin": 56, "coord_israel": 49}, "errores": ["SLA vacío en las 105 filas; la columna no se utiliza en este extracto de monitoreo.", "Typo en incidencia: folio 3657 «CIERRRE DE TURNO DE MONITOREO» (triple R).", "Typo en incidencia: folio 3965 «SUPERVSION VIRTUAL» (falta I).", "3 horarios capturados como datetime 1900-01-01 (cerca de 00:18–00:23): artefacto de Excel al mezclar fecha y hora.", "Nombre de coordinador con espacio final: «ISRAEL DE JESUS PEREZ » (trailing space) en la fuente.", "Uso inconsistente de ESTATUS «SIN RELEVANCIA»: 26 registros; en su mayoría supervisiones con texto idéntico «sin novedad relevante». En otras noches el mismo texto se marca REPORTADO COMPLETO.", "Noches 03/09 y 05–06/09 concentran casi todos los SIN RELEVANCIA (incluye cierres 3695 y 3838).", "Typos en observaciones: «PIOR/POIR» (por), «REPORTANDPO», «ESTDO», «SUPERVISON», «PLATAEN» (sin espacio).", "Cobertura de cierres completa: 01–10/09 (10/10 noches). Tres cierres a las 06:03 (07, 08 y 09/09).", "No aplica «quién no reportó» a nivel estado: archivo exclusivo de OOAD MONITOREO (Kevin Maldonado e Israel Pérez).", "Regresión de retraso de cierre: n=10; desfase máximo +3 min. Sin casos de fuera de tiempo material; modelo no estimable."], "ooad_summary": [{"ooad": "KEVIN DANIEL MALDONADO", "coordinador": "KEVIN DANIEL MALDONADO", "total": 56, "completo": 35, "fuera": 0, "sinrel": 21, "estatus": "OK"}, {"ooad": "ISRAEL DE JESUS PEREZ", "coordinador": "ISRAEL DE JESUS PEREZ", "total": 49, "completo": 44, "fuera": 0, "sinrel": 5, "estatus": "OK"}], "day_summary": [{"fecha": "01/09", "fecha_iso": "2026-09-01", "total": 9, "supervisiones": 7, "cierre": "Sí", "cierre_hora": "06:00", "cierre_est": "REPORTADO COMPLETO", "coord_cierre": "KEVIN DANIEL MALDONADO", "sinrel": 0, "completo": 9}, {"fecha": "02/09", "fecha_iso": "2026-09-02", "total": 7, "supervisiones": 5, "cierre": "Sí", "cierre_hora": "06:00", "cierre_est": "REPORTADO COMPLETO", "coord_cierre": "ISRAEL DE JESUS PEREZ", "sinrel": 0, "completo": 7}, {"fecha": "03/09", "fecha_iso": "2026-09-03", "total": 8, "supervisiones": 6, "cierre": "Sí", "cierre_hora": "06:00", "cierre_est": "SIN RELEVANCIA", "coord_cierre": "ISRAEL DE JESUS PEREZ", "sinrel": 5, "completo": 3}, {"fecha": "04/09", "fecha_iso": "2026-09-04", "total": 11, "supervisiones": 9, "cierre": "Sí", "cierre_hora": "06:00", "cierre_est": "REPORTADO COMPLETO", "coord_cierre": "KEVIN DANIEL MALDONADO", "sinrel": 0, "completo": 11}, {"fecha": "05/09", "fecha_iso": "2026-09-05", "total": 16, "supervisiones": 13, "cierre": "Sí", "cierre_hora": "06:00", "cierre_est": "REPORTADO COMPLETO", "coord_cierre": "ISRAEL DE JESUS PEREZ", "sinrel": 3, "completo": 13}, {"fecha": "06/09", "fecha_iso": "2026-09-06", "total": 11, "supervisiones": 9, "cierre": "Sí", "cierre_hora": "06:00", "cierre_est": "SIN RELEVANCIA", "coord_cierre": "KEVIN DANIEL MALDONADO", "sinrel": 10, "completo": 1}, {"fecha": "07/09", "fecha_iso": "2026-09-07", "total": 12, "supervisiones": 11, "cierre": "Sí", "cierre_hora": "06:03", "cierre_est": "REPORTADO COMPLETO", "coord_cierre": "KEVIN DANIEL MALDONADO", "sinrel": 8, "completo": 4}, {"fecha": "08/09", "fecha_iso": "2026-09-08", "total": 12, "supervisiones": 10, "cierre": "Sí", "cierre_hora": "06:03", "cierre_est": "REPORTADO COMPLETO", "coord_cierre": "ISRAEL DE JESUS PEREZ", "sinrel": 0, "completo": 12}, {"fecha": "09/09", "fecha_iso": "2026-09-09", "total": 11, "supervisiones": 7, "cierre": "Sí", "cierre_hora": "06:03", "cierre_est": "REPORTADO COMPLETO", "coord_cierre": "ISRAEL DE JESUS PEREZ", "sinrel": 0, "completo": 11}, {"fecha": "10/09", "fecha_iso": "2026-09-10", "total": 8, "supervisiones": 7, "cierre": "Sí", "cierre_hora": "06:00", "cierre_est": "REPORTADO COMPLETO", "coord_cierre": "KEVIN DANIEL MALDONADO", "sinrel": 0, "completo": 8}], "deviations": [{"folio": 3695, "ooad": "MONITOREO", "coordinador": "ISRAEL DE JESUS PEREZ", "hora": "06:00", "fecha": "03/09", "incidencia": "CIERRE DE TURNO DE MONITOREO", "estatus": "SIN RELEVANCIA", "observaciones": "Cierre marcado SIN RELEVANCIA"}, {"folio": 3838, "ooad": "MONITOREO", "coordinador": "KEVIN DANIEL MALDONADO", "hora": "06:00", "fecha": "06/09", "incidencia": "CIERRE DE TURNO DE MONITOREO", "estatus": "SIN RELEVANCIA", "observaciones": "REALIZA CIERRE DE NOVEDADES REPORTANDPO LOS INGRESOS POR CODIGO PLATA EN EL ESTDO DE SINALOA Y REPORTANDO LOS DEMAS ESTADOS SIN NOVEDAD"}, {"folio": 3884, "ooad": "MONITOREO", "coordinador": "KEVIN DANIEL MALDONADO", "hora": "06:03", "fecha": "07/09", "incidencia": "CIERRE DE TURNO DE MONITOREO", "estatus": "REPORTADO COMPLETO", "observaciones": "Cierre 06:03 (posterior a 06:00)"}, {"folio": 3935, "ooad": "MONITOREO", "coordinador": "ISRAEL DE JESUS PEREZ", "hora": "06:03", "fecha": "08/09", "incidencia": "CIERRE DE SUPERVISION NOCTURNO", "estatus": "REPORTADO COMPLETO", "observaciones": "Cierre 06:03 (posterior a 06:00)"}, {"folio": 3979, "ooad": "MONITOREO", "coordinador": "ISRAEL DE JESUS PEREZ", "hora": "06:03", "fecha": "09/09", "incidencia": "CIERRE DE SUPERVISION NOCTURNO", "estatus": "REPORTADO COMPLETO", "observaciones": "REALIZA CIERRE DE NOVEDADES NOCTURNAS CON INCIDENCIA DEL INGRESO DEL CODIGO PLATAEN JALISCO Y SIN NOVEDAD EN LAS DEMAS UNIDADES MEDICAS  · Cierre 06:03 (posterior a 06:00)"}], "hitos": [{"folio": 3776, "ooad": "MONITOREO", "unidad": "UMF#26", "municipio": "XALISCO", "incidencia": "INGRESO DE CODIGO PLATA", "hora": "02:50", "fecha": "05/09", "estatus": "REPORTADO COMPLETO", "observaciones": "SE REPORTA EL INGRESO DE PACIENTE PIOR HERIDA DE ARMA DE FUEGO INGRESA SIN ACOMPAÑANTE Y EN ESPERA DE AUTORIDADES CORRESPONDIENTES "}, {"folio": 3973, "ooad": "MONITOREO", "unidad": "HGSZ#185", "municipio": "ARANDAS JALISCO", "incidencia": "INGRESO DE CODIGO PLATA", "hora": "01:07", "fecha": "09/09", "estatus": "REPORTADO COMPLETO", "observaciones": "INGRESAN PACIENTE POIR HERIDA DE ARMA DE FUEGO LLEGA SIN ACOMPAÑANTE Y EN ESPERA DE AUTORIDADES CORRESPONDIENTES"}, {"folio": 3976, "ooad": "MONITOREO", "unidad": "", "municipio": "", "incidencia": "COMPLEMENTO DE CODIGO PLATA", "hora": "02:10", "fecha": "09/09", "estatus": "REPORTADO COMPLETO", "observaciones": "LLEGA PERSONAL DE POLICIA MUNICIPAL PARA LA INVESTIGACION DEL INGRESO DEL CODIGO PLATA ANTES MENCIONADO "}], "regression": {"n": 10, "umbral": "N/A", "curve": [{"hora": "05:30", "minutos": 330, "prob": 0.0}, {"hora": "05:35", "minutos": 335, "prob": 0.0}, {"hora": "05:40", "minutos": 340, "prob": 0.0}, {"hora": "05:45", "minutos": 345, "prob": 0.0}, {"hora": "05:50", "minutos": 350, "prob": 0.0}, {"hora": "05:55", "minutos": 355, "prob": 0.0}, {"hora": "06:00", "minutos": 360, "prob": 0.0}, {"hora": "06:05", "minutos": 365, "prob": 0.0}, {"hora": "06:10", "minutos": 370, "prob": 0.0}, {"hora": "06:15", "minutos": 375, "prob": 0.0}, {"hora": "06:20", "minutos": 380, "prob": 0.0}, {"hora": "06:25", "minutos": 385, "prob": 0.0}], "points": [{"ooad": "KEVIN", "hora": "06:00", "minutos": 360, "fuera_tiempo": 0, "fecha": "01/09"}, {"ooad": "ISRAEL", "hora": "06:00", "minutos": 360, "fuera_tiempo": 0, "fecha": "02/09"}, {"ooad": "ISRAEL", "hora": "06:00", "minutos": 360, "fuera_tiempo": 1, "fecha": "03/09"}, {"ooad": "KEVIN", "hora": "06:00", "minutos": 360, "fuera_tiempo": 0, "fecha": "04/09"}, {"ooad": "ISRAEL", "hora": "06:00", "minutos": 360, "fuera_tiempo": 0, "fecha": "05/09"}, {"ooad": "KEVIN", "hora": "06:00", "minutos": 360, "fuera_tiempo": 1, "fecha": "06/09"}, {"ooad": "KEVIN", "hora": "06:03", "minutos": 363, "fuera_tiempo": 0, "fecha": "07/09"}, {"ooad": "ISRAEL", "hora": "06:03", "minutos": 363, "fuera_tiempo": 0, "fecha": "08/09"}, {"ooad": "ISRAEL", "hora": "06:03", "minutos": 363, "fuera_tiempo": 0, "fecha": "09/09"}, {"ooad": "KEVIN", "hora": "06:00", "minutos": 360, "fuera_tiempo": 0, "fecha": "10/09"}], "note": "Cierres entre 06:00 y 06:03. Sin retrasos materiales."}};
</script>
<script>
const m = DASH.meta;
document.getElementById('kpiGrid').innerHTML = [
  {label:'Registros totales', val: m.registros_reales, foot: '01–10/09/2026', cls:'accent-teal'},
  {label:'Supervisiones virtuales', val: m.supervisiones, foot: `${m.inicios} inicios de turno`, cls:'accent-teal'},
  {label:'Cierres de turno', val: m.cierres, foot: '10/10 noches cubiertas', cls:'accent-green'},
  {label:'Reportado completo', val: m.completo, foot: `${(m.completo/m.registros_reales*100).toFixed(0)}% del total`, cls:'accent-green'},
  {label:'Sin relevancia', val: m.sinrel, foot: 'uso inconsistente de estatus', cls:'accent-amber'},
].map(k => `<div class="kpi ${k.cls}"><div class="label">${k.label}</div><div class="num">${k.val}</div><div class="foot">${k.foot}</div></div>`).join('');

const axis = document.getElementById('timelineAxis');
const minStart = 330, minEnd = 390;
let hourMarks = '';
for(let h of [5,6]){
  for(let mi of (h===5?[30]:[0,30])){
    const mins = h*60+mi;
    const pct = (mins-minStart)/(minEnd-minStart)*100;
    hourMarks += `<div class="hm" style="left:${pct}%">${String(h).padStart(2,'0')}:${String(mi).padStart(2,'0')}</div>`;
  }
}
axis.innerHTML = `<div class="timeline-line"></div><div class="timeline-hourmarks">${hourMarks}</div>`;
// spread points slightly by index so same-minute cierres don't fully overlap
DASH.regression.points.forEach((p, i) => {
  const jitter = (i - 4.5) * 1.2;
  const pct = Math.min(98, Math.max(2, (p.minutos + jitter - minStart)/(minEnd-minStart)*100));
  const el = document.createElement('div');
  el.className = 'tpoint ' + (p.fuera_tiempo ? 'late' : 'ok');
  el.style.left = pct + '%';
  el.innerHTML = `<div class="tip">${p.fecha} · ${p.hora} · ${p.ooad}${p.fuera_tiempo?' · obs.':''}</div>`;
  axis.appendChild(el);
});

document.getElementById('coordTableBody').innerHTML = DASH.ooad_summary.map(o => `<tr>
  <td style="font-family:var(--display); font-weight:600;">${o.ooad}</td>
  <td class="num">${o.total}</td><td class="num">${o.completo}</td>
  <td class="num" style="color:${o.sinrel>0?'var(--amber)':'var(--text-dim)'}">${o.sinrel}</td>
  <td><span class="badge ok"><span class="badge-dot"></span>OK</span></td>
</tr>`).join('');

document.getElementById('dayTableBody').innerHTML = DASH.day_summary.map(d => `<tr>
  <td style="font-family:var(--mono);">${d.fecha}</td>
  <td class="num">${d.total}</td>
  <td class="num">${d.supervisiones}</td>
  <td>${d.cierre}</td>
  <td class="num">${d.cierre_hora}</td>
  <td class="muted" style="font-size:12px;">${d.coord_cierre}</td>
  <td class="num" style="color:${d.sinrel>0?'var(--amber)':'var(--text-dim)'}">${d.sinrel}</td>
</tr>`).join('');

document.getElementById('devList').innerHTML = DASH.deviations.length ? DASH.deviations.map(d => `
  <div class="dev-item">
    <div class="row1"><span class="ooad">${d.fecha}</span><span class="hora">${d.hora}</span></div>
    <div class="who">Folio ${d.folio} · ${d.coordinador} · ${d.incidencia} · ${d.estatus}</div>
    ${d.observaciones ? `<div class="note">${d.observaciones}</div>` : ''}
  </div>`).join('') : `<div class="empty-box">Sin observaciones de cierre</div>`;

document.getElementById('hitoList').innerHTML = DASH.hitos.length ? DASH.hitos.map(h => `
  <div class="hito-item">
    <div class="row1"><span class="title">${h.incidencia}</span><span class="meta">${h.hora} · ${h.fecha}</span></div>
    <div class="loc">${h.unidad || '—'}${h.municipio ? ' · ' + h.municipio : ''} · Folio ${h.folio}</div>
    ${h.observaciones ? `<div class="note">${h.observaciones}</div>` : ''}
  </div>`).join('') : `<div class="empty-box">Sin incidencias de código plata</div>`;

document.getElementById('regStats').innerHTML = `
  <div class="stat-box"><div class="k">N cierres</div><div class="v">${DASH.regression.n}</div></div>
  <div class="stat-box"><div class="k">Retrasos >5 min</div><div class="v" style="color:var(--green)">0</div></div>
  <div class="stat-box"><div class="k">Cierre típico</div><div class="v">06:00</div></div>
  <div class="stat-box"><div class="k">Máx. desfase</div><div class="v">+3 min</div></div>`;
document.getElementById('regNotes').innerHTML = `
  <li><b>No hay base para regresión logística de “fuera de tiempo”:</b> los 10 cierres están entre 06:00 y 06:03.</li>
  <li>Kevin Maldonado: ${m.coord_kevin} registros. Israel Pérez: ${m.coord_israel} registros.</li>
  <li>2 cierres marcados SIN RELEVANCIA (03/09 y 06/09) pese a horario puntual; criterio de estatus inconsistente.</li>
  <li>${m.codigos_plata} registros ligados a código plata (ingresos + complemento) detectados en guardia nocturna.</li>
  <li>${DASH.regression.note}</li>`;

new Chart(document.getElementById('regChart'), {
  type: 'line',
  data: {
    labels: DASH.regression.curve.map(c => c.hora),
    datasets: [
      { label: 'Prob. retraso (≈0)', data: DASH.regression.curve.map(() => 0),
        borderColor: '#2AC9B8', backgroundColor: 'rgba(42,201,184,0.10)', fill: true, tension: 0.25, pointRadius: 0, borderWidth: 2 },
      { label: 'Cierres observados',
        data: DASH.regression.curve.map(c => {
          const pt = DASH.regression.points.find(p => Math.abs(p.minutos - c.minutos) < 2);
          return pt ? 0 : null;
        }),
        borderColor: 'transparent',
        pointBackgroundColor: DASH.regression.curve.map(c => {
          const pt = DASH.regression.points.find(p => Math.abs(p.minutos - c.minutos) < 2);
          return pt ? (pt.fuera_tiempo ? '#F0A93E' : '#33C077') : 'transparent';
        }),
        pointRadius: DASH.regression.curve.map(c => {
          const pt = DASH.regression.points.find(p => Math.abs(p.minutos - c.minutos) < 2);
          return pt ? 5 : 0;
        }),
        showLine: false }
    ]
  },
  options: {
    responsive:true, maintainAspectRatio:false,
    plugins:{ legend:{ labels:{ color:'#8AA0C2', font:{family:'Inter', size:11} } },
      tooltip:{ backgroundColor:'#0D1728', borderColor:'#1E2D48', borderWidth:1, titleColor:'#E7EDF7', bodyColor:'#8AA0C2' } },
    scales:{
      x:{ ticks:{ color:'#566A8E', maxTicksLimit:8, font:{family:'IBM Plex Mono', size:10} }, grid:{ color:'#16233B' } },
      y:{ ticks:{ color:'#566A8E', callback: v => v+'%', font:{family:'IBM Plex Mono', size:10} }, grid:{ color:'#16233B' }, min:0, max:100 }
    }
  }
});

document.getElementById('errList').innerHTML = DASH.errores.map(e =>
  `<div class="err-item"><span class="err-icon">▲</span><span>${e}</span></div>`).join('');
</script>
</body>
</html>
