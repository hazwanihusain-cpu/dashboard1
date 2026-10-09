<!DOCTYPE html>
<html lang="ms">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dashboard Penilaian Formatif Pelajar</title>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #f4f6fb;
      --surface: #ffffff;
      --border: #e2e6ef;
      --text: #1e2330;
      --muted: #5a6478;
      --accent: #2563eb;
      --success: #16a34a;
      --warning: #d97706;
      --danger: #dc2626;
      --purple: #7c3aed;
      --radius: 10px;
    }

    body {
      font-family: -apple-system, "Segoe UI", system-ui, sans-serif;
      background: var(--bg);
      color: var(--text);
      font-size: 14px;
      line-height: 1.6;
    }

    /* ── Header ── */
    header {
      background: var(--accent);
      color: #fff;
      padding: 18px 28px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
      gap: 10px;
    }
    header h1 { font-size: 1.15rem; font-weight: 700; }
    header p  { font-size: 0.8rem; opacity: 0.85; margin-top: 2px; }
    .header-meta { text-align: right; font-size: 0.78rem; opacity: 0.85; }

    /* ── Layout ── */
    .wrapper { max-width: 1280px; margin: 0 auto; padding: 24px 20px; }

    /* ── Summary Cards ── */
    .summary-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(170px, 1fr));
      gap: 14px;
      margin-bottom: 26px;
    }
    .card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 16px 18px;
    }
    .card-label { font-size: 0.72rem; text-transform: uppercase; letter-spacing: .05em; color: var(--muted); }
    .card-value { font-size: 1.7rem; font-weight: 700; margin-top: 4px; }
    .card-sub   { font-size: 0.75rem; color: var(--muted); margin-top: 2px; }
    .card.blue   .card-value { color: var(--accent); }
    .card.green  .card-value { color: var(--success); }
    .card.amber  .card-value { color: var(--warning); }
    .card.red    .card-value { color: var(--danger); }
    .card.purple .card-value { color: var(--purple); }

    /* ── Section ── */
    .section-title {
      font-size: 0.85rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: .06em;
      color: var(--muted);
      margin-bottom: 12px;
      padding-bottom: 6px;
      border-bottom: 2px solid var(--border);
    }
    .section { margin-bottom: 30px; }

    /* ── Tabs ── */
    .tabs { display: flex; gap: 6px; flex-wrap: wrap; margin-bottom: 16px; }
    .tab-btn {
      padding: 6px 16px;
      border: 1px solid var(--border);
      border-radius: 20px;
      background: var(--surface);
      color: var(--muted);
      font-size: 0.78rem;
      font-weight: 600;
      cursor: pointer;
      transition: background .15s, color .15s;
    }
    .tab-btn.active { background: var(--accent); color: #fff; border-color: var(--accent); }

    /* ── Table ── */
    .table-wrap { overflow-x: auto; border-radius: var(--radius); border: 1px solid var(--border); }
    table { width: 100%; border-collapse: collapse; background: var(--surface); }
    thead th {
      background: #f0f3fb;
      font-size: 0.72rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: .05em;
      color: var(--muted);
      padding: 10px 14px;
      text-align: left;
      border-bottom: 1px solid var(--border);
    }
    tbody tr:not(:last-child) { border-bottom: 1px solid var(--border); }
    tbody tr:hover { background: #f8f9fc; }
    tbody td { padding: 9px 14px; font-size: 0.82rem; vertical-align: middle; }

    /* ── Badges ── */
    .badge {
      display: inline-block;
      padding: 2px 8px;
      border-radius: 20px;
      font-size: 0.7rem;
      font-weight: 600;
    }
    .badge-green  { background: #dcfce7; color: #15803d; }
    .badge-red    { background: #fee2e2; color: #b91c1c; }
    .badge-amber  { background: #fef3c7; color: #92400e; }
    .badge-blue   { background: #dbeafe; color: #1d4ed8; }
    .badge-purple { background: #ede9fe; color: #6d28d9; }
    .badge-gray   { background: #f1f5f9; color: #475569; }

    /* ── Progress bar ── */
    .prog-wrap { background: #e5e7eb; border-radius: 99px; height: 7px; width: 90px; display: inline-block; vertical-align: middle; }
    .prog-bar  { height: 100%; border-radius: 99px; }
    .prog-green { background: var(--success); }
    .prog-amber { background: var(--warning); }
    .prog-red   { background: var(--danger); }

    /* ── Checklist ── */
    .checklist-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 14px;
    }
    .checklist-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      overflow: hidden;
    }
    .checklist-header {
      padding: 10px 16px;
      font-size: 0.8rem;
      font-weight: 700;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .cl-blue   { background: #dbeafe; color: #1d4ed8; }
    .cl-green  { background: #dcfce7; color: #15803d; }
    .cl-purple { background: #ede9fe; color: #6d28d9; }
    .checklist-body { padding: 10px 16px; }
    .cl-item {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 5px 0;
      font-size: 0.8rem;
      border-bottom: 1px solid #f1f5f9;
    }
    .cl-item:last-child { border-bottom: none; }
    .cl-check {
      width: 15px; height: 15px;
      border-radius: 3px;
      border: 1.5px solid #cbd5e1;
      display: inline-flex; align-items: center; justify-content: center;
      flex-shrink: 0;
      cursor: pointer;
      transition: background .15s;
    }
    .cl-check.checked { background: var(--success); border-color: var(--success); }
    .cl-check.checked::after { content: "✓"; font-size: 9px; color: #fff; }
    .cl-name { flex: 1; }
    .cl-score { font-weight: 700; color: var(--accent); }

    /* ── Intervensi ── */
    .intervensi-table tbody td { font-size: 0.8rem; }
    .priority-high   { color: var(--danger); font-weight: 700; }
    .priority-medium { color: var(--warning); font-weight: 700; }
    .priority-low    { color: var(--success); font-weight: 700; }

    /* ── Markah Keseluruhan ── */
    .markah-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 14px;
    }
    .markah-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius);
      padding: 16px 20px;
    }
    .markah-name { font-weight: 700; font-size: 0.88rem; margin-bottom: 10px; }
    .markah-row  { display: flex; justify-content: space-between; font-size: 0.78rem; padding: 3px 0; color: var(--muted); }
    .markah-row strong { color: var(--text); }
    .markah-total {
      margin-top: 10px;
      padding-top: 8px;
      border-top: 1px solid var(--border);
      display: flex;
      justify-content: space-between;
      font-weight: 700;
      font-size: 0.88rem;
    }
    .grade-A { color: var(--success); }
    .grade-B { color: var(--accent); }
    .grade-C { color: var(--warning); }
    .grade-D { color: var(--danger); }

    /* ── Print ── */
    .print-btn {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 7px 14px;
      font-size: 0.78rem;
      font-weight: 600;
      cursor: pointer;
      color: var(--accent);
      float: right;
      margin-bottom: 6px;
    }
    @media print {
      .print-btn, .tabs, header .header-meta { display: none; }
      body { background: #fff; }
    }
    @media (max-width: 600px) {
      header { padding: 14px 16px; }
      .wrapper { padding: 16px 12px; }
    }
  </style>
</head>
<body>

<header>
  <div>
    <h1>📊 Dashboard Penilaian Formatif Pelajar</h1>
    <p>Kursus: Teknologi Maklumat &nbsp;|&nbsp; Semester 2 / 2024–2025</p>
  </div>
  <div class="header-meta">
    Pensyarah: Encik Ahmad Faris<br>
    Dikemaskini: <span id="lastUpdated"></span>
  </div>
</header>

<div class="wrapper">

  <!-- ── Summary Cards ── -->
  <div class="summary-grid">
    <div class="card blue">
      <div class="card-label">Jumlah Pelajar</div>
      <div class="card-value" id="totalStudents">0</div>
      <div class="card-sub">Berdaftar dalam kursus</div>
    </div>
    <div class="card green">
      <div class="card-label">Purata Kehadiran</div>
      <div class="card-value" id="avgAttendance">0%</div>
      <div class="card-sub">Daripada 14 minggu</div>
    </div>
    <div class="card amber">
      <div class="card-label">Purata Markah</div>
      <div class="card-value" id="avgScore">0%</div>
      <div class="card-sub">Penilaian formatif</div>
    </div>
    <div class="card red">
      <div class="card-label">Perlu Intervensi</div>
      <div class="card-value" id="needIntervention">0</div>
      <div class="card-sub">Pelajar berisiko</div>
    </div>
    <div class="card purple">
      <div class="card-label">Lulus Keseluruhan</div>
      <div class="card-value" id="passCount">0</div>
      <div class="card-sub">Gred A / B / C</div>
    </div>
  </div>

  <!-- ── TABS ── -->
  <div class="tabs">
    <button class="tab-btn active" onclick="switchTab('kehadiran', this)">📅 Kehadiran</button>
    <button class="tab-btn" onclick="switchTab('kuiz', this)">📝 Kuiz</button>
    <button class="tab-btn" onclick="switchTab('laporan', this)">🔬 Laporan & Ujian</button>
    <button class="tab-btn" onclick="switchTab('intervensi', this)">⚠️ Intervensi</button>
    <button class="tab-btn" onclick="switchTab('markah', this)">🏆 Markah Keseluruhan</button>
  </div>

  <!-- ═══════════════════════════════════════════ -->
  <!-- TAB: KEHADIRAN -->
  <!-- ═══════════════════════════════════════════ -->
  <div id="tab-kehadiran" class="section tab-content">
    <button class="print-btn" onclick="window.print()">🖨 Cetak</button>
    <div class="section-title">Senarai Kehadiran Pelajar</div>
    <div class="table-wrap">
      <table id="tableKehadiran">
        <thead>
          <tr>
            <th>#</th>
            <th>No. Matrik</th>
            <th>Nama Pelajar</th>
            <th>Hadir (Minggu)</th>
            <th>Peratus</th>
            <th>Status</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>
  </div>

  <!-- ═══════════════════════════════════════════ -->
  <!-- TAB: KUIZ -->
  <!-- ═══════════════════════════════════════════ -->
  <div id="tab-kuiz" class="section tab-content" style="display:none">
    <div class="section-title">Checklist Penilaian Kuiz (3 Jenis Kuiz)</div>
    <div class="checklist-grid" id="kuizChecklist"></div>
  </div>

  <!-- ═══════════════════════════════════════════ -->
  <!-- TAB: LAPORAN & UJIAN -->
  <!-- ═══════════════════════════════════════════ -->
  <div id="tab-laporan" class="section tab-content" style="display:none">
    <div class="section-title">Laporan &amp; Ujian</div>
    <div class="table-wrap">
      <table id="tableLaporan">
        <thead>
          <tr>
            <th>#</th>
            <th>Nama Pelajar</th>
            <th>Laporan 1</th>
            <th>Laporan 2</th>
            <th>Laporan 3</th>
            <th>Ujian 1 (30)</th>
            <th>Ujian 2 (30)</th>
            <th>Status Laporan</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>
  </div>

  <!-- ═══════════════════════════════════════════ -->
  <!-- TAB: INTERVENSI -->
  <!-- ═══════════════════════════════════════════ -->
  <div id="tab-intervensi" class="section tab-content" style="display:none">
    <div class="section-title">Tindakan Intervensi Pelajar</div>
    <div class="table-wrap">
      <table id="tableIntervensi" class="intervensi-table">
        <thead>
          <tr>
            <th>#</th>
            <th>Nama Pelajar</th>
            <th>Isu Dikenal Pasti</th>
            <th>Keutamaan</th>
            <th>Tindakan Intervensi</th>
            <th>Tarikh Tindakan</th>
            <th>Status</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>
  </div>

  <!-- ═══════════════════════════════════════════ -->
  <!-- TAB: MARKAH KESELURUHAN -->
  <!-- ═══════════════════════════════════════════ -->
  <div id="tab-markah" class="section tab-content" style="display:none">
    <div class="section-title">Markah Keseluruhan Penilaian Formatif</div>
    <div class="markah-grid" id="markahGrid"></div>
  </div>

</div><!-- /wrapper -->

<script>
/* ══════════════════════════════════════════════════
   DATA
══════════════════════════════════════════════════ */
const TOTAL_WEEKS = 14;

const students = [
  { id: "2024001", name: "Ahmad Hakimi Razali",    attend: 13 },
  { id: "2024002", name: "Nurul Ain Zulkifli",     attend: 14 },
  { id: "2024003", name: "Muhammad Fariz Hamdan",  attend: 10 },
  { id: "2024004", name: "Siti Nabilah Othman",    attend: 12 },
  { id: "2024005", name: "Khairul Anwar Yusof",    attend: 8  },
  { id: "2024006", name: "Fatin Husna Idris",      attend: 13 },
  { id: "2024007", name: "Zulhilmi Bakar",         attend: 11 },
  { id: "2024008", name: "Aisyah Mohd Nor",        attend: 14 },
  { id: "2024009", name: "Hazwan Hafiz Ismail",    attend: 9  },
  { id: "2024010", name: "Liyana Syafiqah Kamal",  attend: 13 },
];

// Kuiz: 3 types × 10 students
const quizTypes = [
  { label: "Kuiz 1 – Teori Asas",     color: "cl-blue",   max: 20 },
  { label: "Kuiz 2 – Aplikasi Praktikal", color: "cl-green", max: 25 },
  { label: "Kuiz 3 – Analisis Kes",   color: "cl-purple", max: 25 },
];

const quizData = [
  { q1: 18, q2: 22, q3: 21 },
  { q1: 19, q2: 24, q3: 23 },
  { q1: 12, q2: 15, q3: 14 },
  { q1: 17, q2: 20, q3: 19 },
  { q1: 9,  q2: 11, q3: 10 },
  { q1: 18, q2: 23, q3: 22 },
  { q1: 14, q2: 17, q3: 16 },
  { q1: 20, q2: 25, q3: 24 },
  { q1: 10, q2: 13, q3: 11 },
  { q1: 17, q2: 21, q3: 20 },
];

// Lab reports & tests
const reportData = [
  { lm1: "Hantar", lm2: "Hantar", lm3: "Hantar", u1: 26, u2: 25 },
  { lm1: "Hantar", lm2: "Hantar", lm3: "Hantar", u1: 28, u2: 27 },
  { lm1: "Hantar", lm2: "Lewat",  lm3: "Belum",  u1: 16, u2: 14 },
  { lm1: "Hantar", lm2: "Hantar", lm3: "Hantar", u1: 24, u2: 22 },
  { lm1: "Lewat",  lm2: "Belum",  lm3: "Belum",  u1: 12, u2: 10 },
  { lm1: "Hantar", lm2: "Hantar", lm3: "Hantar", u1: 27, u2: 26 },
  { lm1: "Hantar", lm2: "Hantar", lm3: "Lewat",  u1: 20, u2: 18 },
  { lm1: "Hantar", lm2: "Hantar", lm3: "Hantar", u1: 29, u2: 28 },
  { lm1: "Lewat",  lm2: "Belum",  lm3: "Belum",  u1: 13, u2: 12 },
  { lm1: "Hantar", lm2: "Hantar", lm3: "Hantar", u1: 25, u2: 24 },
];

// Intervention records (only at-risk students)
const interventionData = [
  {
    studentIdx: 2, issue: "Kehadiran rendah & markah kuiz lemah",
    priority: "Tinggi", action: "Bimbingan individu + tugasan tambahan",
    date: "2025-03-10", status: "Dalam Proses"
  },
  {
    studentIdx: 4, issue: "Kehadiran < 60%, laporan tidak lengkap",
    priority: "Tinggi", action: "Surat amaran + pertemuan waris",
    date: "2025-03-08", status: "Dalam Proses"
  },
  {
    studentIdx: 6, issue: "Markah ujian di bawah 50%",
    priority: "Sederhana", action: "Sesi pemulihan setiap Jumaat",
    date: "2025-03-15", status: "Dijadualkan"
  },
  {
    studentIdx: 8, issue: "Kehadiran rendah & laporan tidak dihantar",
    priority: "Tinggi", action: "Bimbingan individu + laporan gantian",
    date: "2025-03-07", status: "Dalam Proses"
  },
  {
    studentIdx: 3, issue: "Prestasi kuiz menurun",
    priority: "Rendah", action: "Nasihat akademik & modul e-pembelajaran",
    date: "2025-03-20", status: "Dijadualkan"
  },
];

/* ══════════════════════════════════════════════════
   HELPERS
══════════════════════════════════════════════════ */
function pct(v, max) { return Math.round(v / max * 100); }

function progBar(val, max) {
  const p = pct(val, max);
  const cls = p >= 80 ? "prog-green" : p >= 60 ? "prog-amber" : "prog-red";
  return `<span class="prog-wrap"><span class="prog-bar ${cls}" style="width:${p}%"></span></span> ${p}%`;
}

function attendBadge(weeks) {
  const p = pct(weeks, TOTAL_WEEKS);
  if (p >= 80) return `<span class="badge badge-green">Baik</span>`;
  if (p >= 60) return `<span class="badge badge-amber">Berisiko</span>`;
  return `<span class="badge badge-red">Kritikal</span>`;
}

function lmBadge(status) {
  if (status === "Hantar") return `<span class="badge badge-green">Hantar</span>`;
  if (status === "Lewat")  return `<span class="badge badge-amber">Lewat</span>`;
  return `<span class="badge badge-red">Belum Hantar</span>`;
}

function prioritySpan(p) {
  if (p === "Tinggi")   return `<span class="priority-high">▲ Tinggi</span>`;
  if (p === "Sederhana") return `<span class="priority-medium">● Sederhana</span>`;
  return `<span class="priority-low">▼ Rendah</span>`;
}

function statusBadge(s) {
  if (s === "Selesai")      return `<span class="badge badge-green">Selesai</span>`;
  if (s === "Dalam Proses") return `<span class="badge badge-blue">Dalam Proses</span>`;
  return `<span class="badge badge-amber">Dijadualkan</span>`;
}

function computeTotal(i) {
  const q = quizData[i];
  const r = reportData[i];
  const s = students[i];
  const attend = pct(s.attend, TOTAL_WEEKS);

  // Weightings (total 100)
  const kuizScore = ((q.q1 / quizTypes[0].max) * 0.6 +
                     (q.q2 / quizTypes[1].max) * 0.6 +
                     (q.q3 / quizTypes[2].max) * 0.6) / 3 * 20; // 20%

  const lmScore = ["lm1", "lm2", "lm3"].reduce((acc, k) => {
    return acc + (r[k] === "Hantar" ? 10 : r[k] === "Lewat" ? 6 : 0);
  }, 0); // 30%

  const ujianScore = ((r.u1 / 30) + (r.u2 / 30)) / 2 * 30; // 30%

  const hadirScore = Math.min(attend / 100 * 20, 20); // 20%

  const total = kuizScore + lmScore + ujianScore + hadirScore;
  return {
    kuiz: Math.round(kuizScore),
    laporan: Math.round(lmScore),
    ujian: Math.round(ujianScore),
    hadir: Math.round(hadirScore),
    total: Math.round(total),
    grade: total >= 85 ? "A" : total >= 70 ? "B" : total >= 55 ? "C" : total >= 40 ? "D" : "E"
  };
}

/* ══════════════════════════════════════════════════
   BUILD SUMMARY CARDS
══════════════════════════════════════════════════ */
function buildSummary() {
  document.getElementById("lastUpdated").textContent =
    new Date().toLocaleDateString("ms-MY", { year: "numeric", month: "long", day: "numeric" });

  document.getElementById("totalStudents").textContent = students.length;

  const avgAtt = Math.round(students.reduce((a, s) => a + pct(s.attend, TOTAL_WEEKS), 0) / students.length);
  document.getElementById("avgAttendance").textContent = avgAtt + "%";

  const totals = students.map((_, i) => computeTotal(i).total);
  const avgMark = Math.round(totals.reduce((a, b) => a + b, 0) / totals.length);
  document.getElementById("avgScore").textContent = avgMark + "%";

  const atRisk = students.filter((s, i) => {
    const p = pct(s.attend, TOTAL_WEEKS);
    return p < 80 || totals[i] < 55;
  }).length;
  document.getElementById("needIntervention").textContent = atRisk;

  const pass = totals.filter(t => t >= 55).length;
  document.getElementById("passCount").textContent = pass;
}

/* ══════════════════════════════════════════════════
   BUILD KEHADIRAN
══════════════════════════════════════════════════ */
function buildKehadiran() {
  const tbody = document.querySelector("#tableKehadiran tbody");
  tbody.innerHTML = students.map((s, i) => {
    const p = pct(s.attend, TOTAL_WEEKS);
    return `<tr>
      <td>${i + 1}</td>
      <td>${s.id}</td>
      <td><strong>${s.name}</strong></td>
      <td>${s.attend} / ${TOTAL_WEEKS}</td>
      <td>${progBar(s.attend, TOTAL_WEEKS)}</td>
      <td>${attendBadge(s.attend)}</td>
    </tr>`;
  }).join("");
}

/* ══════════════════════════════════════════════════
   BUILD KUIZ CHECKLIST
══════════════════════════════════════════════════ */
function buildKuiz() {
  const container = document.getElementById("kuizChecklist");
  container.innerHTML = quizTypes.map((qt, qi) => {
    const key = ["q1", "q2", "q3"][qi];
    const items = students.map((s, si) => {
      const score = quizData[si][key];
      const passed = pct(score, qt.max) >= 50;
      return `<div class="cl-item">
        <div class="cl-check ${passed ? "checked" : ""}" title="${passed ? "Lulus" : "Gagal/Belum"}"></div>
        <span class="cl-name">${s.name}</span>
        <span class="cl-score">${score}/${qt.max}</span>
        ${passed ? `<span class="badge badge-green">✓</span>` : `<span class="badge badge-red">✗</span>`}
      </div>`;
    }).join("");

    const passCount = quizData.filter(q => pct(q[key], qt.max) >= 50).length;
    return `<div class="checklist-card">
      <div class="checklist-header ${qt.color}">
        📝 ${qt.label}
        <span class="badge badge-gray" style="margin-left:auto">${passCount}/${students.length} Lulus</span>
      </div>
      <div class="checklist-body">${items}</div>
    </div>`;
  }).join("");
}

/* ══════════════════════════════════════════════════
   BUILD LAPORAN & UJIAN
══════════════════════════════════════════════════ */
function buildLaporan() {
  const tbody = document.querySelector("#tableLaporan tbody");
  tbody.innerHTML = students.map((s, i) => {
    const r = reportData[i];
    return `<tr>
      <td>${i + 1}</td>
      <td><strong>${s.name}</strong></td>
      <td>${lmBadge(r.lm1)}</td>
      <td>${lmBadge(r.lm2)}</td>
      <td>${lmBadge(r.lm3)}</td>
      <td>${r.u1}<span style="color:var(--muted)">/30</span></td>
      <td>${r.u2}<span style="color:var(--muted)">/30</span></td>
      <td>${
        r.lm1 === "Hantar" && r.lm2 === "Hantar" && r.lm3 === "Hantar"
          ? `<span class="badge badge-green">Lengkap</span>`
          : r.lm1 === "Belum" || r.lm2 === "Belum"
            ? `<span class="badge badge-red">Tidak Lengkap</span>`
            : `<span class="badge badge-amber">Separa</span>`
      }</td>
    </tr>`;
  }).join("");
}

/* ══════════════════════════════════════════════════
   BUILD INTERVENSI
══════════════════════════════════════════════════ */
function buildIntervensi() {
  const tbody = document.querySelector("#tableIntervensi tbody");
  tbody.innerHTML = interventionData.map((iv, i) => {
    const s = students[iv.studentIdx];
    return `<tr>
      <td>${i + 1}</td>
      <td><strong>${s.name}</strong><br><small style="color:var(--muted)">${s.id}</small></td>
      <td>${iv.issue}</td>
      <td>${prioritySpan(iv.priority)}</td>
      <td>${iv.action}</td>
      <td>${iv.date}</td>
      <td>${statusBadge(iv.status)}</td>
    </tr>`;
  }).join("");
}

/* ══════════════════════════════════════════════════
   BUILD MARKAH KESELURUHAN
══════════════════════════════════════════════════ */
function buildMarkah() {
  const grid = document.getElementById("markahGrid");
  grid.innerHTML = students.map((s, i) => {
    const t = computeTotal(i);
    const gc = `grade-${t.grade}`;
    return `<div class="markah-card">
      <div class="markah-name">${s.name}<br><small style="color:var(--muted)">${s.id}</small></div>
      <div class="markah-row"><span>Kehadiran (20%)</span><strong>${t.hadir}/20</strong></div>
      <div class="markah-row"><span>Kuiz (20%)</span><strong>${t.kuiz}/20</strong></div>
      <div class="markah-row"><span>Laporan (30%)</span><strong>${t.laporan}/30</strong></div>
      <div class="markah-row"><span>Ujian (30%)</span><strong>${t.ujian}/30</strong></div>
      <div class="markah-total">
        <span>Jumlah</span>
        <span>${t.total}/100 &nbsp;<span class="${gc}">Gred ${t.grade}</span></span>
      </div>
    </div>`;
  }).join("");
}

/* ══════════════════════════════════════════════════
   TAB SWITCHING
══════════════════════════════════════════════════ */
function switchTab(name, btn) {
  document.querySelectorAll(".tab-content").forEach(el => el.style.display = "none");
  document.querySelectorAll(".tab-btn").forEach(b => b.classList.remove("active"));
  document.getElementById("tab-" + name).style.display = "block";
  btn.classList.add("active");
}

/* ══════════════════════════════════════════════════
   INIT
══════════════════════════════════════════════════ */
buildSummary();
buildKehadiran();
buildKuiz();
buildLaporan();
buildIntervensi();
buildMarkah();
</script>
</body>
</html>

