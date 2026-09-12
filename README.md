[index.html.html](https://github.com/user-attachments/files/32148260/index.html.html)
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tablero Monitoreo — 05–12/09/2026</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@500;600;700&family=Inter:wght@400;500;600;700&family=IBM+Plex+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.4/chart.umd.min.js"></script>
<style>
  :root{
    --bg:#0A1220; --panel:#101B31; --panel-2:#0D1728; --border:#1E2D48; --border-soft:#16233B;
    --text:#E7EDF7; --text-muted:#8AA0C2; --text-dim:#566A8E;
    --teal:#2AC9B8; --teal-soft:rgba(42,201,184,.12); --amber:#F0A93E; --amber-soft:rgba(240,169,62,.14);
    --red:#F14C6B; --red-soft:rgba(241,76,107,.14); --green:#33C077; --green-soft:rgba(51,192,119,.13);
    --display:'Space Grotesk',sans-serif; --body:'Inter',sans-serif; --mono:'IBM Plex Mono',monospace;
  }
  *{box-sizing:border-box} html,body{margin:0;padding:0}
  body{background:radial-gradient(1100px 500px at 12% -10%,rgba(42,201,184,.10),transparent 60%),radial-gradient(900px 500px at 100% 0%,rgba(240,169,62,.06),transparent 55%),var(--bg);color:var(--text);font-family:var(--body);line-height:1.5;padding:0 0 64px}
  .masthead{border-bottom:1px solid var(--border-soft);padding:28px clamp(18px,4vw,56px) 22px;display:flex;justify-content:space-between;align-items:flex-end;gap:24px;flex-wrap:wrap;position:relative}
  .masthead::before{content:"";position:absolute;left:0;right:0;top:0;height:2px;background:linear-gradient(90deg,transparent,var(--teal) 20%,var(--teal) 80%,transparent);opacity:.55}
  .brand-row{display:flex;align-items:center;gap:12px;margin-bottom:10px}
  .brand-mark{width:34px;height:34px;border-radius:9px;background:linear-gradient(135deg,var(--teal),#157A6E);display:flex;align-items:center;justify-content:center;font-family:var(--mono);font-weight:600;font-size:13px;color:#04201B}
  .eyebrow{font-family:var(--mono);font-size:11.5px;letter-spacing:.14em;text-transform:uppercase;color:var(--text-dim)}
  h1{font-family:var(--display);font-weight:600;font-size:clamp(22px,3.2vw,32px);margin:2px 0 6px}
  .sub{color:var(--text-muted);font-size:14px;max-width:700px}
  .status-pill{font-family:var(--mono);font-size:12.5px;display:inline-flex;align-items:center;gap:8px;background:var(--panel);border:1px solid var(--border);padding:9px 14px;border-radius:999px;color:var(--text-muted)}
  .dot{width:8px;height:8px;border-radius:50%;background:var(--teal);box-shadow:0 0 0 3px var(--teal-soft)}
  .wrap{padding:30px clamp(18px,4vw,56px) 0;max-width:1360px;margin:0 auto}
  section{margin-bottom:40px}
  .section-head{display:flex;align-items:baseline;gap:10px;margin-bottom:16px;flex-wrap:wrap}
  .section-num{font-family:var(--mono);color:var(--teal);font-size:12.5px}
  .section-title{font-family:var(--display);font-size:19px;font-weight:600}
  .section-note{color:var(--text-dim);font-size:12.5px;margin-left:auto;font-family:var(--mono)}
  .kpis{display:grid;grid-template-columns:repeat(5,1fr);gap:14px}
  @media(max-width:980px){.kpis{grid-template-columns:repeat(2,1fr)}}
  .kpi{background:linear-gradient(180deg,var(--panel),var(--panel-2));border:1px solid var(--border);border-radius:14px;padding:18px}
  .kpi .label{font-size:11.5px;color:var(--text-dim);text-transform:uppercase;letter-spacing:.08em;font-family:var(--mono)}
  .kpi .num{font-family:var(--display);font-size:32px;font-weight:600;margin-top:8px}
  .kpi .foot{font-size:12px;color:var(--text-muted);margin-top:4px}
  .kpi.accent-red .num{color:var(--red)} .kpi.accent-amber .num{color:var(--amber)}
  .kpi.accent-green .num{color:var(--green)} .kpi.accent-teal .num{color:var(--teal)}
  .timeline-card{background:var(--panel);border:1px solid var(--border);border-radius:14px;padding:22px clamp(14px,3vw,26px) 18px}
  .timeline-legend{display:flex;gap:18px;margin-bottom:14px;flex-wrap:wrap;font-size:12px;color:var(--text-muted);font-family:var(--mono)}
  .legend-item{display:flex;align-items:center;gap:7px}
  .legend-swatch{width:9px;height:9px;border-radius:2px}
  .timeline-axis{position:relative;height:96px}
  .timeline-line{position:absolute;left:0;right:0;top:48px;height:1px;background:var(--border)}
  .timeline-hourmarks{position:absolute;left:0;right:0;top:64px;height:20px}
  .hm{position:absolute;transform:translateX(-50%);font-family:var(--mono);font-size:10.5px;color:var(--text-dim)}
  .hm::before{content:"";position:absolute;left:50%;top:-16px;width:1px;height:8px;background:var(--border-soft)}
  .tpoint{position:absolute;top:38px;width:13px;height:13px;border-radius:50%;transform:translateX(-50%);border:2px solid var(--bg)}
  .tpoint.ok{background:var(--green);box-shadow:0 0 0 3px var(--green-soft)}
  .tpoint.late{background:var(--red);box-shadow:0 0 0 3px var(--red-soft)}
  .tpoint .tip{visibility:hidden;opacity:0;position:absolute;bottom:22px;left:50%;transform:translateX(-50%);background:#050B15;border:1px solid var(--border);color:var(--text);font-size:11px;font-family:var(--mono);padding:6px 9px;border-radius:8px;white-space:nowrap;z-index:5}
  .tpoint:hover .tip{visibility:visible;opacity:1}
  .table-card{background:var(--panel);border:1px solid var(--border);border-radius:14px;overflow:hidden;overflow-x:auto}
  table{width:100%;border-collapse:collapse;font-size:13.5px}
  thead th{text-align:left;font-family:var(--mono);font-size:11px;text-transform:uppercase;letter-spacing:.06em;color:var(--text-dim);padding:13px 16px;border-bottom:1px solid var(--border);background:var(--panel-2)}
  tbody td{padding:12px 16px;border-bottom:1px solid var(--border-soft);vertical-align:top}
  tbody tr:last-child td{border-bottom:none}
  tbody tr:hover{background:rgba(255,255,255,.02)}
  td.num,th.num{font-family:var(--mono);text-align:right}
  .badge{display:inline-flex;align-items:center;gap:6px;padding:4px 10px;border-radius:999px;font-family:var(--mono);font-size:11px;white-space:nowrap}
  .badge.ok{background:var(--green-soft);color:var(--green)}
  .badge.dev{background:var(--red-soft);color:var(--red)}
  .badge-dot{width:6px;height:6px;border-radius:50%;background:currentColor}
  .muted{color:var(--text-muted)}
  .two-col{display:grid;grid-template-columns:1fr 1.15fr;gap:20px;align-items:start}
  @media(max-width:980px){.two-col{grid-template-columns:1fr}}
  .dev-item{border:1px solid var(--border);border-left:3px solid var(--red);background:var(--panel);border-radius:10px;padding:14px 16px;margin-bottom:12px}
  .dev-item .row1{display:flex;justify-content:space-between;align-items:center;margin-bottom:6px;gap:8px;flex-wrap:wrap}
  .dev-item .ooad{font-family:var(--display);font-weight:600;font-size:15px}
  .dev-item .hora{font-family:var(--mono);color:var(--red);font-size:13px}
  .dev-item .who{font-size:12.5px;color:var(--text-muted);margin-bottom:4px}
  .dev-item .note{font-size:12.5px;color:var(--text-dim)}
  .hito-item{border:1px solid var(--border);background:var(--panel);border-radius:10px;padding:14px 16px;margin-bottom:12px;border-left:3px solid var(--amber)}
  .hito-item .row1{display:flex;justify-content:space-between;gap:10px;margin-bottom:6px;flex-wrap:wrap}
  .hito-item .title{font-family:var(--display);font-weight:600;font-size:14px}
  .hito-item .meta{font-family:var(--mono);font-size:11px;color:var(--text-dim);white-space:nowrap}
  .hito-item .loc{font-size:12px;color:var(--text-muted);margin-bottom:5px}
  .hito-item .note{font-size:12.5px;color:var(--text-muted)}
  .reg-grid{display:grid;grid-template-columns:1.3fr 1fr;gap:20px}
  @media(max-width:980px){.reg-grid{grid-template-columns:1fr}}
  .reg-card{background:var(--panel);border:1px solid var(--border);border-radius:14px;padding:20px}
  .reg-stats{display:grid;grid-template-columns:1fr 1fr;gap:12px}
  .stat-box{background:var(--panel-2);border:1px solid var(--border-soft);border-radius:10px;padding:12px 14px}
  .stat-box .k{font-family:var(--mono);font-size:10.5px;color:var(--text-dim);text-transform:uppercase;letter-spacing:.06em}
  .stat-box .v{font-family:var(--display);font-size:20px;font-weight:600;margin-top:4px}
  .chart-wrap{height:260px;margin-top:8px}
  .reg-notes{font-size:13px;color:var(--text-muted)}
  .reg-notes li{margin-bottom:8px}
  .err-card{background:var(--panel);border:1px solid var(--border);border-radius:14px;padding:6px 0}
  .err-item{display:flex;gap:12px;padding:13px 20px;border-bottom:1px solid var(--border-soft);font-size:13.5px;color:var(--text-muted)}
  .err-item:last-child{border-bottom:none}
  .err-icon{font-family:var(--mono);color:var(--amber);flex-shrink:0;font-size:12px;margin-top:2px}
  footer{max-width:1360px;margin:40px auto 0;padding:20px clamp(18px,4vw,56px) 0;border-top:1px solid var(--border-soft);color:var(--text-dim);font-size:12px;font-family:var(--mono);display:flex;justify-content:space-between;flex-wrap:wrap;gap:8px}
</style>
</head>
<body>
<div class="masthead">
  <div>
    <div class="brand-row"><div class="brand-mark">CE</div><span class="eyebrow">Centro de Enlace · Monitoreo nocturno</span></div>
    <h1>Tablero de Avances — Monitoreo 05–12/09/2026</h1>
    <div class="sub">Supervisiones virtuales, desviaciones de estatus (SIN RELEVANCIA), cierres de turno e incidentes relevantes registrados por los monitoristas.</div>
  </div>
  <div class="status-pill"><span class="dot"></span> 2 monitoristas · 96 registros · 8 noches</div>
</div>
<div class="wrap">
  <section><div class="kpis" id="kpiGrid"></div></section>
  <section>
    <div class="section-head"><span class="section-num">01</span><span class="section-title">Línea de tiempo de cierres de turno</span><span class="section-note">05:50 – 06:30 hrs</span></div>
    <div class="timeline-card">
      <div class="timeline-legend">
        <div class="legend-item"><span class="legend-swatch" style="background:var(--green)"></span> A tiempo (≤06:05)</div>
        <div class="legend-item"><span class="legend-swatch" style="background:var(--red)"></span> Tardío / sin cierre</div>
      </div>
      <div class="timeline-axis" id="timelineAxis"></div>
    </div>
  </section>
  <section>
    <div class="section-head"><span class="section-num">02</span><span class="section-title">Estatus por monitorista</span><span class="section-note" id="devCountNote"></span></div>
    <div class="table-card">
      <table>
        <thead><tr>
          <th>Monitorista</th><th class="num">Reportes</th><th class="num">Completos</th>
          <th class="num">Sin relevancia</th><th class="num">Cierre tardío</th><th class="num">Cód. plata</th><th>Estatus</th>
        </tr></thead>
        <tbody id="ooadTableBody"></tbody>
      </table>
    </div>
  </section>
  <section>
    <div class="section-head"><span class="section-num">03</span><span class="section-title">Desviaciones e hitos</span></div>
    <div class="two-col">
      <div>
        <div class="section-title" style="font-size:14px;color:var(--red);margin-bottom:10px">Sin relevancia / cierre tardío</div>
        <div id="devList"></div>
      </div>
      <div>
        <div class="section-title" style="font-size:14px;color:var(--amber);margin-bottom:10px">Incidentes relevantes (hitos)</div>
        <div id="hitoList"></div>
      </div>
    </div>
  </section>
  <section>
    <div class="section-head"><span class="section-num">04</span><span class="section-title">Análisis de regresión — SIN RELEVANCIA vs hora</span><span class="section-note">Logística regularizada</span></div>
    <div class="reg-grid">
      <div class="reg-card"><div class="chart-wrap"><canvas id="regChart"></canvas></div></div>
      <div class="reg-card">
        <div class="reg-stats" id="regStats"></div>
        <ul class="reg-notes" id="regNotes" style="margin-top:14px;padding-left:18px"></ul>
      </div>
    </div>
  </section>
  <section>
    <div class="section-head"><span class="section-num">05</span><span class="section-title">Errores e inconsistencias detectadas</span></div>
    <div class="err-card" id="errList"></div>
  </section>
</div>
<footer>
  <span>Fuente: tabla de monitoreo.xlsx · OOAD MONITOREO</span>
  <span>Tablero de avances · 05–12/09/2026</span>
</footer>
<script>const DASH = {"meta": {"fecha": "05–12/09/2026", "total": 96, "completo": 75, "sinrel": 21, "codigos": 3, "monitores": 2, "noches": 8}, "errores": ["SLA vacío en el 100% de las filas.", "Typos en INCIDENCIA: \"SUPERVSION VIRTUAL\" (falta I) en al menos 2 registros.", "Horas mal capturadas por Excel: folios 3926 y 3927 aparecen como 1900-01-01 con hora embebida.", "Kevin marca SIN RELEVANCIA en casi todas las supervisiones de las noches 05/09 y 06/09 (21 registros).", "Cierre de Kevin el 11/09 a las 06:16 (folio 4087): fuera de la ventana habitual ≤06:05.", "Noche 10/09: Israel inicia (20:05) pero el cierre 06:16 queda a nombre de Kevin; relevo poco claro.", "Supervisiones diurnas de Kevin el 10/09 (10:44–11:34) fuera de franja nocturna 22:00–06:00.", "Observaciones con faltas: \"PIOR\", \"POIR\", \"REPORTANDPO\", \"ESTDO\", \"PLATAEN\".", "Este archivo solo contiene OOAD MONITOREO; no hay reportes matutinos/vespertinos de estados.", "Totales: 96 registros · 75 completos · 21 sin relevancia · 3 códigos plata."], "ooad_summary": [{"ooad": "Kevin D. Maldonado", "total": 56, "completo": 35, "fuera": 21, "late_cierre": 1, "codigos": 0, "supervisiones": 47, "estatus": "CON DESVIACION"}, {"ooad": "Israel de J. Pérez", "total": 40, "completo": 40, "fuera": 0, "late_cierre": 0, "codigos": 3, "supervisiones": 32, "estatus": "OK"}], "deviations": [{"folio": 3821, "monitor": "KEVIN DANIEL MALDONADO", "hora": "22:35", "fecha": "05/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HR#14", "municipio": "SAN LUIS POTOSI", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3823, "monitor": "KEVIN DANIEL MALDONADO", "hora": "23:06", "fecha": "05/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HGZ#10", "municipio": "NAYARIT", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3825, "monitor": "KEVIN DANIEL MALDONADO", "hora": "23:43", "fecha": "05/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HGZ#92", "municipio": "COAHUILA", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3828, "monitor": "KEVIN DANIEL MALDONADO", "hora": "00:20", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "UMF#79", "municipio": "TAMAULIPAS", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3830, "monitor": "KEVIN DANIEL MALDONADO", "hora": "01:09", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "UMF#6", "municipio": "AGUASCALIENTES", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3831, "monitor": "KEVIN DANIEL MALDONADO", "hora": "01:50", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HGR#180", "municipio": "JALISCO", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3832, "monitor": "KEVIN DANIEL MALDONADO", "hora": "02:30", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HGS-MF#26", "municipio": "BAJA SUR ", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3833, "monitor": "KEVIN DANIEL MALDONADO", "hora": "03:10", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HGZ#35", "municipio": "CHIHUAHUA", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3834, "monitor": "KEVIN DANIEL MALDONADO", "hora": "04:08", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HR#51", "municipio": "ZACATECAS", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3835, "monitor": "KEVIN DANIEL MALDONADO", "hora": "04:40", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "UMF#35", "municipio": "SINALOA", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3838, "monitor": "KEVIN DANIEL MALDONADO", "hora": "06:00", "fecha": "06/09", "incidencia": "CIERRE DE TURNO DE MONITOREO", "unidad": "", "municipio": "", "tipo": "SIN RELEVANCIA", "obs": "REALIZA CIERRE DE NOVEDADES REPORTANDPO LOS INGRESOS POR CODIGO PLATA EN EL ESTDO DE SINALOA Y REPORTANDO LOS DEMAS ESTA"}, {"folio": 3869, "monitor": "KEVIN DANIEL MALDONADO", "hora": "23:15", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HR#14", "municipio": "SAN LUIS POTOSI", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3870, "monitor": "KEVIN DANIEL MALDONADO", "hora": "23:45", "fecha": "06/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "UMMA#28", "municipio": "NAYARIT", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3871, "monitor": "KEVIN DANIEL MALDONADO", "hora": "00:16", "fecha": "07/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "UMF#25", "municipio": "COAHUILA", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3872, "monitor": "KEVIN DANIEL MALDONADO", "hora": "00:49", "fecha": "07/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HGZ#2", "municipio": "DURANGO", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3873, "monitor": "KEVIN DANIEL MALDONADO", "hora": "01:24", "fecha": "07/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "UMF#41", "municipio": "CHIHUAHUA", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3874, "monitor": "KEVIN DANIEL MALDONADO", "hora": "01:48", "fecha": "07/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HRG#70", "municipio": "TAMAULIPAS", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3875, "monitor": "KEVIN DANIEL MALDONADO", "hora": "03:04", "fecha": "07/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "UMF#9", "municipio": "SINALOA", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3876, "monitor": "KEVIN DANIEL MALDONADO", "hora": "03:28", "fecha": "07/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HGZ/MF#26", "municipio": "JALISCO", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3877, "monitor": "KEVIN DANIEL MALDONADO", "hora": "04:14", "fecha": "07/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "HR#53", "municipio": "ZACATECAS", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 3878, "monitor": "KEVIN DANIEL MALDONADO", "hora": "04:40", "fecha": "07/09", "incidencia": "SUPERVISION VIRTUAL", "unidad": "UMF#65", "municipio": "JALISCO", "tipo": "SIN RELEVANCIA", "obs": "SE REALIZA LLAMADA A GUARDIA DE TURNO  DE LA UNIDAD REPORTANDO SIN NOVEDAD RELEVANTE AL MOMENTO "}, {"folio": 4087, "monitor": "KEVIN DANIEL MALDONADO", "hora": "06:16", "fecha": "11/09", "incidencia": "CIERRE DE SUPERVISION NOCTURNO", "unidad": "", "municipio": "", "tipo": "CIERRE TARDÍO", "obs": ""}], "dev_total": 22, "hitos": [{"folio": 3776, "monitor": "ISRAEL DE JESUS PEREZ", "hora": "02:50", "fecha": "05/09", "incidencia": "INGRESO DE CODIGO PLATA ", "unidad": "UMF#26", "municipio": "XALISCO", "obs": "SE REPORTA EL INGRESO DE PACIENTE PIOR HERIDA DE ARMA DE FUEGO INGRESA SIN ACOMPAÑANTE Y EN ESPERA DE AUTORIDADES CORRESPONDIENTES "}, {"folio": 3973, "monitor": "ISRAEL DE JESUS PEREZ", "hora": "01:07", "fecha": "09/09", "incidencia": "INGRESO DE CODIGO PLATA", "unidad": "HGSZ#185", "municipio": "ARANDAS JALISCO", "obs": "INGRESAN PACIENTE POIR HERIDA DE ARMA DE FUEGO LLEGA SIN ACOMPAÑANTE Y EN ESPERA DE AUTORIDADES CORRESPONDIENTES"}, {"folio": 3976, "monitor": "ISRAEL DE JESUS PEREZ", "hora": "02:10", "fecha": "09/09", "incidencia": "COMPLEMENTO DE CODIGO PLATA ", "unidad": "", "municipio": "", "obs": "LLEGA PERSONAL DE POLICIA MUNICIPAL PARA LA INVESTIGACION DEL INGRESO DEL CODIGO PLATA ANTES MENCIONADO "}, {"folio": 4078, "monitor": "ISRAEL DE JESUS PEREZ", "hora": "02:23", "fecha": "11/09", "incidencia": "SUPERVISION VIRTUAL (hallazgo uniformidad)", "unidad": "CSS", "municipio": "MONCLOVA", "obs": "NO LE PIDIO A LA GUARDIA SE CERRARA LA CAMISOLA Y SE LE VE LA PLAYERA ROJA ABAJO"}, {"folio": 4079, "monitor": "KEVIN DANIEL MALDONADO", "hora": "02:50", "fecha": "11/09", "incidencia": "SUPERVISION VIRTUAL (hallazgo uniformidad)", "unidad": "UMF 6", "municipio": "AGUASCALIENTES", "obs": "EN LA FOTO LA GUARDIA APARECE CON CABELLO DESALINEADO"}], "nights": [{"noche": "2026-09-04", "lbl": "04/09", "primary": "ISRAEL DE JESUS PEREZ", "total": 12, "sup": 10, "sinrel": 0, "cierre": "06:00", "late": false, "missing_cierre": false}, {"noche": "2026-09-05", "lbl": "05/09", "primary": "KEVIN DANIEL MALDONADO", "total": 12, "sup": 10, "sinrel": 11, "cierre": "06:00", "late": false, "missing_cierre": false}, {"noche": "2026-09-06", "lbl": "06/09", "primary": "KEVIN DANIEL MALDONADO", "total": 12, "sup": 10, "sinrel": 10, "cierre": "06:03", "late": false, "missing_cierre": false}, {"noche": "2026-09-07", "lbl": "07/09", "primary": "ISRAEL DE JESUS PEREZ", "total": 10, "sup": 9, "sinrel": 0, "cierre": "06:03", "late": false, "missing_cierre": false}, {"noche": "2026-09-08", "lbl": "08/09", "primary": "ISRAEL DE JESUS PEREZ", "total": 12, "sup": 8, "sinrel": 0, "cierre": "06:03", "late": false, "missing_cierre": false}, {"noche": "2026-09-09", "lbl": "09/09", "primary": "KEVIN DANIEL MALDONADO", "total": 15, "sup": 13, "sinrel": 0, "cierre": "06:00", "late": false, "missing_cierre": false}, {"noche": "2026-09-10", "lbl": "10/09", "primary": "ISRAEL DE JESUS PEREZ", "total": 8, "sup": 6, "sinrel": 0, "cierre": "06:16", "late": true, "missing_cierre": false}, {"noche": "2026-09-11", "lbl": "11/09", "primary": "KEVIN DANIEL MALDONADO", "total": 15, "sup": 13, "sinrel": 0, "cierre": "06:00", "late": false, "missing_cierre": false}], "timeline": [{"label": "04/09 ISRAEL", "hora": "06:00", "minutos": 360, "late": false}, {"label": "05/09 KEVIN", "hora": "06:00", "minutos": 360, "late": false}, {"label": "06/09 KEVIN", "hora": "06:03", "minutos": 363, "late": false}, {"label": "07/09 ISRAEL", "hora": "06:03", "minutos": 363, "late": false}, {"label": "08/09 ISRAEL", "hora": "06:03", "minutos": 363, "late": false}, {"label": "09/09 KEVIN", "hora": "06:00", "minutos": 360, "late": false}, {"label": "10/09 ISRAEL", "hora": "06:16", "minutos": 376, "late": true}, {"label": "11/09 KEVIN", "hora": "06:00", "minutos": 360, "late": false}], "regression": {"b0": -0.9216737685926877, "b1": -0.00046157668683953626, "r": -0.029645023983054405, "p": 0.7953668328048273, "n": 79, "curve": [{"hora": "20:00", "minutos": 0, "prob": 0.2846}, {"hora": "20:15", "minutos": 15, "prob": 0.2832}, {"hora": "20:30", "minutos": 30, "prob": 0.2818}, {"hora": "20:45", "minutos": 45, "prob": 0.2804}, {"hora": "21:00", "minutos": 60, "prob": 0.279}, {"hora": "21:15", "minutos": 75, "prob": 0.2776}, {"hora": "21:30", "minutos": 90, "prob": 0.2762}, {"hora": "21:45", "minutos": 105, "prob": 0.2749}, {"hora": "22:00", "minutos": 120, "prob": 0.2735}, {"hora": "22:15", "minutos": 135, "prob": 0.2721}, {"hora": "22:30", "minutos": 150, "prob": 0.2707}, {"hora": "22:45", "minutos": 165, "prob": 0.2694}, {"hora": "23:00", "minutos": 180, "prob": 0.268}, {"hora": "23:15", "minutos": 195, "prob": 0.2667}, {"hora": "23:30", "minutos": 210, "prob": 0.2653}, {"hora": "23:45", "minutos": 225, "prob": 0.264}, {"hora": "00:00", "minutos": 240, "prob": 0.2626}, {"hora": "00:15", "minutos": 255, "prob": 0.2613}, {"hora": "00:30", "minutos": 270, "prob": 0.2599}, {"hora": "00:45", "minutos": 285, "prob": 0.2586}, {"hora": "01:00", "minutos": 300, "prob": 0.2573}, {"hora": "01:15", "minutos": 315, "prob": 0.256}, {"hora": "01:30", "minutos": 330, "prob": 0.2546}, {"hora": "01:45", "minutos": 345, "prob": 0.2533}, {"hora": "02:00", "minutos": 360, "prob": 0.252}, {"hora": "02:15", "minutos": 375, "prob": 0.2507}, {"hora": "02:30", "minutos": 390, "prob": 0.2494}, {"hora": "02:45", "minutos": 405, "prob": 0.2481}, {"hora": "03:00", "minutos": 420, "prob": 0.2468}, {"hora": "03:15", "minutos": 435, "prob": 0.2456}, {"hora": "03:30", "minutos": 450, "prob": 0.2443}, {"hora": "03:45", "minutos": 465, "prob": 0.243}, {"hora": "04:00", "minutos": 480, "prob": 0.2417}, {"hora": "04:15", "minutos": 495, "prob": 0.2405}, {"hora": "04:30", "minutos": 510, "prob": 0.2392}, {"hora": "04:45", "minutos": 525, "prob": 0.2379}, {"hora": "05:00", "minutos": 540, "prob": 0.2367}, {"hora": "05:15", "minutos": 555, "prob": 0.2354}, {"hora": "05:30", "minutos": 570, "prob": 0.2342}, {"hora": "05:45", "minutos": 585, "prob": 0.233}, {"hora": "06:00", "minutos": 600, "prob": 0.2317}], "points": [{"monitor": "ISRAEL", "hora": "00:12", "minutos": 252, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:50", "minutos": 290, "sr": 0}, {"monitor": "ISRAEL", "hora": "01:22", "minutos": 322, "sr": 0}, {"monitor": "ISRAEL", "hora": "02:05", "minutos": 365, "sr": 0}, {"monitor": "ISRAEL", "hora": "02:47", "minutos": 407, "sr": 0}, {"monitor": "ISRAEL", "hora": "03:21", "minutos": 441, "sr": 0}, {"monitor": "ISRAEL", "hora": "04:02", "minutos": 482, "sr": 0}, {"monitor": "ISRAEL", "hora": "04:14", "minutos": 494, "sr": 0}, {"monitor": "ISRAEL", "hora": "04:34", "minutos": 514, "sr": 0}, {"monitor": "ISRAEL", "hora": "04:43", "minutos": 523, "sr": 0}, {"monitor": "KEVIN", "hora": "22:35", "minutos": 155, "sr": 1}, {"monitor": "KEVIN", "hora": "23:06", "minutos": 186, "sr": 1}, {"monitor": "KEVIN", "hora": "23:43", "minutos": 223, "sr": 1}, {"monitor": "KEVIN", "hora": "00:20", "minutos": 260, "sr": 1}, {"monitor": "KEVIN", "hora": "01:09", "minutos": 309, "sr": 1}, {"monitor": "KEVIN", "hora": "01:50", "minutos": 350, "sr": 1}, {"monitor": "KEVIN", "hora": "02:30", "minutos": 390, "sr": 1}, {"monitor": "KEVIN", "hora": "03:10", "minutos": 430, "sr": 1}, {"monitor": "KEVIN", "hora": "04:08", "minutos": 488, "sr": 1}, {"monitor": "KEVIN", "hora": "04:40", "minutos": 520, "sr": 1}, {"monitor": "KEVIN", "hora": "23:15", "minutos": 195, "sr": 1}, {"monitor": "KEVIN", "hora": "23:45", "minutos": 225, "sr": 1}, {"monitor": "KEVIN", "hora": "00:16", "minutos": 256, "sr": 1}, {"monitor": "KEVIN", "hora": "00:49", "minutos": 289, "sr": 1}, {"monitor": "KEVIN", "hora": "01:24", "minutos": 324, "sr": 1}, {"monitor": "KEVIN", "hora": "01:48", "minutos": 348, "sr": 1}, {"monitor": "KEVIN", "hora": "03:04", "minutos": 424, "sr": 1}, {"monitor": "KEVIN", "hora": "03:28", "minutos": 448, "sr": 1}, {"monitor": "KEVIN", "hora": "04:14", "minutos": 494, "sr": 1}, {"monitor": "KEVIN", "hora": "04:40", "minutos": 520, "sr": 1}, {"monitor": "ISRAEL", "hora": "23:20", "minutos": 200, "sr": 0}, {"monitor": "ISRAEL", "hora": "23:42", "minutos": 222, "sr": 0}, {"monitor": "ISRAEL", "hora": "23:59", "minutos": 239, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:18", "minutos": 258, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:23", "minutos": 263, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:54", "minutos": 294, "sr": 0}, {"monitor": "ISRAEL", "hora": "01:33", "minutos": 333, "sr": 0}, {"monitor": "ISRAEL", "hora": "02:24", "minutos": 384, "sr": 0}, {"monitor": "ISRAEL", "hora": "02:36", "minutos": 396, "sr": 0}, {"monitor": "ISRAEL", "hora": "22:08", "minutos": 128, "sr": 0}, {"monitor": "ISRAEL", "hora": "22:31", "minutos": 151, "sr": 0}, {"monitor": "ISRAEL", "hora": "23:13", "minutos": 193, "sr": 0}, {"monitor": "ISRAEL", "hora": "23:53", "minutos": 233, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:16", "minutos": 256, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:30", "minutos": 270, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:51", "minutos": 291, "sr": 0}, {"monitor": "ISRAEL", "hora": "01:32", "minutos": 332, "sr": 0}, {"monitor": "KEVIN", "hora": "22:55", "minutos": 175, "sr": 0}, {"monitor": "KEVIN", "hora": "23:20", "minutos": 200, "sr": 0}, {"monitor": "KEVIN", "hora": "23:38", "minutos": 218, "sr": 0}, {"monitor": "KEVIN", "hora": "00:10", "minutos": 250, "sr": 0}, {"monitor": "KEVIN", "hora": "00:37", "minutos": 277, "sr": 0}, {"monitor": "KEVIN", "hora": "00:48", "minutos": 288, "sr": 0}, {"monitor": "KEVIN", "hora": "02:00", "minutos": 360, "sr": 0}, {"monitor": "KEVIN", "hora": "02:10", "minutos": 370, "sr": 0}, {"monitor": "KEVIN", "hora": "02:52", "minutos": 412, "sr": 0}, {"monitor": "KEVIN", "hora": "03:26", "minutos": 446, "sr": 0}, {"monitor": "KEVIN", "hora": "10:44", "minutos": 884, "sr": 0}, {"monitor": "KEVIN", "hora": "11:10", "minutos": 910, "sr": 0}, {"monitor": "KEVIN", "hora": "11:34", "minutos": 934, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:17", "minutos": 257, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:33", "minutos": 273, "sr": 0}, {"monitor": "ISRAEL", "hora": "00:52", "minutos": 292, "sr": 0}, {"monitor": "ISRAEL", "hora": "02:11", "minutos": 371, "sr": 0}, {"monitor": "ISRAEL", "hora": "02:23", "minutos": 383, "sr": 0}, {"monitor": "KEVIN", "hora": "02:50", "minutos": 410, "sr": 0}, {"monitor": "KEVIN", "hora": "22:38", "minutos": 158, "sr": 0}, {"monitor": "KEVIN", "hora": "23:07", "minutos": 187, "sr": 0}, {"monitor": "KEVIN", "hora": "23:38", "minutos": 218, "sr": 0}, {"monitor": "KEVIN", "hora": "00:08", "minutos": 248, "sr": 0}, {"monitor": "KEVIN", "hora": "00:48", "minutos": 288, "sr": 0}, {"monitor": "KEVIN", "hora": "01:29", "minutos": 329, "sr": 0}, {"monitor": "KEVIN", "hora": "02:05", "minutos": 365, "sr": 0}, {"monitor": "KEVIN", "hora": "02:28", "minutos": 388, "sr": 0}, {"monitor": "KEVIN", "hora": "03:08", "minutos": 428, "sr": 0}, {"monitor": "KEVIN", "hora": "03:30", "minutos": 450, "sr": 0}, {"monitor": "KEVIN", "hora": "03:55", "minutos": 475, "sr": 0}, {"monitor": "KEVIN", "hora": "04:11", "minutos": 491, "sr": 0}, {"monitor": "KEVIN", "hora": "04:27", "minutos": 507, "sr": 0}], "note": "Probabilidad de SIN RELEVANCIA según hora de supervisión (desde 20:00). Correlación débil: el patrón es por monitorista, no por hora."}};</script>
<script>
const m = DASH.meta;
const fmtPct = v => (v*100).toFixed(1)+'%';
document.getElementById('kpiGrid').innerHTML = [
  {label:'Registros', val:m.total, foot:m.noches+' noches operativas', cls:'accent-teal'},
  {label:'Reportado completo', val:m.completo, foot:fmtPct(m.completo/m.total), cls:'accent-green'},
  {label:'Sin relevancia', val:m.sinrel, foot:fmtPct(m.sinrel/m.total), cls:'accent-red'},
  {label:'Códigos plata', val:m.codigos, foot:'documentados por Israel', cls:'accent-amber'},
  {label:'Monitoristas', val:m.monitores, foot:'Kevin e Israel', cls:'accent-teal'},
].map(k=>`<div class="kpi ${k.cls}"><div class="label">${k.label}</div><div class="num">${k.val}</div><div class="foot">${k.foot}</div></div>`).join('');

const axis = document.getElementById('timelineAxis');
const minStart=350, minEnd=400; // 05:50-06:40
let hm='';
for(let h=6;h<=6;h++){ for(let mm of [0,15,30]){ const mins=h*60+mm; const pct=(mins-minStart)/(minEnd-minStart)*100; if(pct>=0&&pct<=100) hm+=`<div class="hm" style="left:${pct}%">${String(h).padStart(2,'0')}:${String(mm).padStart(2,'0')}</div>`;}}
// also 05:50
hm=`<div class="hm" style="left:${(350-minStart)/(minEnd-minStart)*100}%">05:50</div>`+hm;
axis.innerHTML=`<div class="timeline-line"></div><div class="timeline-hourmarks">${hm}</div>`;
DASH.timeline.forEach(p=>{
  const pct=Math.min(100,Math.max(0,(p.minutos-minStart)/(minEnd-minStart)*100));
  const el=document.createElement('div');
  el.className='tpoint '+(p.late?'late':'ok');
  el.style.left=pct+'%';
  el.innerHTML=`<div class="tip">${p.label} · ${p.hora}${p.late?' · TARDÍO':''}</div>`;
  axis.appendChild(el);
});

const sorted=[...DASH.ooad_summary].sort((a,b)=>b.fuera-a.fuera);
document.getElementById('ooadTableBody').innerHTML=sorted.map(o=>{
  const badge=o.estatus==='CON DESVIACION'
    ?'<span class="badge dev"><span class="badge-dot"></span>Con desviación</span>'
    :'<span class="badge ok"><span class="badge-dot"></span>OK</span>';
  return `<tr>
    <td style="font-family:var(--display);font-weight:600">${o.ooad}</td>
    <td class="num">${o.total}</td><td class="num">${o.completo}</td>
    <td class="num" style="color:${o.fuera>0?'var(--red)':'var(--text-dim)'}">${o.fuera}</td>
    <td class="num" style="color:${o.late_cierre>0?'var(--red)':'var(--text-dim)'}">${o.late_cierre}</td>
    <td class="num">${o.codigos}</td><td>${badge}</td></tr>`;
}).join('');
document.getElementById('devCountNote').textContent=
  DASH.ooad_summary.filter(o=>o.estatus!=='OK').length+' de 2 con desviación';

// show first 12 deviations to keep UI clean, note total
const showDev=DASH.deviations.slice(0,12);
document.getElementById('devList').innerHTML=showDev.map(d=>`
  <div class="dev-item">
    <div class="row1"><span class="ooad">${d.monitor.split(' ')[0]}</span><span class="hora">${d.hora} · ${d.fecha}</span></div>
    <div class="who">Folio ${d.folio} · ${d.tipo}${d.unidad?' · '+d.unidad:''}</div>
    ${d.obs?`<div class="note">${d.obs}</div>`:''}
  </div>`).join('') + (DASH.dev_total>12?`<div class="muted" style="font-size:12.5px;padding:8px">… y ${DASH.dev_total-12} desviaciones más (total ${DASH.dev_total})</div>`:'');

document.getElementById('hitoList').innerHTML=DASH.hitos.map(h=>`
  <div class="hito-item">
    <div class="row1"><span class="title">${h.incidencia}</span><span class="meta">${h.hora} · ${h.fecha}</span></div>
    <div class="loc">${h.monitor.split(' ').slice(0,2).join(' ')}${h.unidad?' · '+h.unidad:''}${h.municipio?' · '+h.municipio:''} · Folio ${h.folio}</div>
    ${h.obs?`<div class="note">${h.obs}</div>`:''}
  </div>`).join('') || '<div class="muted">Sin hitos</div>';

const reg=DASH.regression;
document.getElementById('regStats').innerHTML=`
  <div class="stat-box"><div class="k">Correlación (r)</div><div class="v">${reg.r.toFixed(2)}</div></div>
  <div class="stat-box"><div class="k">Valor p</div><div class="v">${reg.p.toFixed(3)}</div></div>
  <div class="stat-box"><div class="k">N supervisiones</div><div class="v">${reg.n}</div></div>
  <div class="stat-box"><div class="k">Sin relevancia</div><div class="v">${m.sinrel}</div></div>`;
document.getElementById('regNotes').innerHTML=`
  <li>${reg.note}</li>
  <li>Correlación casi nula (r=${reg.r.toFixed(2)}, p=${reg.p.toFixed(3)}): la hora <b>no</b> predice SIN RELEVANCIA.</li>
  <li>El patrón es por <b>monitorista</b>: los 21 SIN RELEVANCIA pertenecen a Kevin (noches 05 y 06/09).</li>
  <li>Israel: 0 SIN RELEVANCIA y 3 códigos plata documentados (Xalisco, Arandas + complemento).</li>
  <li>Cierre tardío: Kevin 11/09 a las 06:16.</li>`;

new Chart(document.getElementById('regChart'),{
  type:'line',
  data:{
    labels:reg.curve.map(c=>c.hora),
    datasets:[
      {label:'Prob. estimada SIN RELEVANCIA', data:reg.curve.map(c=>c.prob*100),
        borderColor:'#2AC9B8', backgroundColor:'rgba(42,201,184,0.10)', fill:true, tension:0.25, pointRadius:0, borderWidth:2},
      {label:'Observados (0/100)',
        data:reg.curve.map(c=>{const pt=reg.points.find(p=>Math.abs(p.minutos-c.minutos)<8); return pt?(pt.sr?100:0):null;}),
        borderColor:'transparent',
        pointBackgroundColor:reg.curve.map(c=>{const pt=reg.points.find(p=>Math.abs(p.minutos-c.minutos)<8); if(!pt)return 'transparent'; return pt.sr?'#F14C6B':'#33C077';}),
        pointRadius:reg.curve.map(c=>{const pt=reg.points.find(p=>Math.abs(p.minutos-c.minutos)<8); return pt?4:0;}),
        showLine:false}
    ]
  },
  options:{
    responsive:true, maintainAspectRatio:false,
    plugins:{legend:{labels:{color:'#8AA0C2',font:{family:'Inter',size:11}}},
      tooltip:{backgroundColor:'#0D1728',borderColor:'#1E2D48',borderWidth:1,titleColor:'#E7EDF7',bodyColor:'#8AA0C2'}},
    scales:{
      x:{ticks:{color:'#566A8E',maxTicksLimit:10,font:{family:'IBM Plex Mono',size:10}},grid:{color:'#16233B'}},
      y:{ticks:{color:'#566A8E',callback:v=>v+'%',font:{family:'IBM Plex Mono',size:10}},grid:{color:'#16233B'},min:0,max:100}
    }
  }
});

document.getElementById('errList').innerHTML=DASH.errores.map(e=>
  `<div class="err-item"><span class="err-icon">▲</span><span>${e}</span></div>`).join('');
</script>
</body>
</html>
