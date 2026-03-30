<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Club Selection</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Epilogue:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #f5f2ec;
  --surface: #ffffff;
  --card: #faf8f4;
  --border: #e0dbd2;
  --ink: #1a1714;
  --muted: #8a8278;
  --accent: #c8402a;
  --accent2: #2a6cc8;
  --green: #2a8a4a;
  --yellow: #d4a017;
  --tag-bg: #ede9e1;
}

* { box-sizing: border-box; margin: 0; padding: 0; }

body {
  font-family: 'Epilogue', sans-serif;
  background: var(--bg);
  color: var(--ink);
  min-height: 100vh;
}

/* ── NAV ── */
nav {
  display: flex;
  align-items: center;
  gap: 0;
  background: var(--ink);
  padding: 0 32px;
  position: sticky;
  top: 0;
  z-index: 50;
}

.nav-brand {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 1.1rem;
  color: #fff;
  padding: 18px 0;
  margin-right: auto;
  letter-spacing: 0.04em;
}

.nav-tab {
  font-family: 'Syne', sans-serif;
  font-size: 0.82rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.5);
  padding: 20px 20px;
  cursor: pointer;
  border-bottom: 3px solid transparent;
  transition: color 0.2s, border-color 0.2s;
}

.nav-tab:hover { color: rgba(255,255,255,0.85); }
.nav-tab.active { color: #fff; border-bottom-color: var(--accent); }

/* ── PAGES ── */
.page { display: none; }
.page.active { display: block; }

/* ── STUDENT PAGE ── */
.student-wrap {
  max-width: 780px;
  margin: 0 auto;
  padding: 48px 24px 80px;
}

.page-header {
  margin-bottom: 40px;
}

.page-header h1 {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: clamp(2rem, 5vw, 3.2rem);
  line-height: 1.05;
  color: var(--ink);
}

.page-header p {
  color: var(--muted);
  font-size: 0.95rem;
  font-weight: 300;
  margin-top: 8px;
}

/* name input */
.name-row {
  display: flex;
  gap: 12px;
  margin-bottom: 36px;
  align-items: flex-end;
}

.field {
  display: flex;
  flex-direction: column;
  gap: 6px;
  flex: 1;
}

.field label {
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
}

.field input, .field select {
  background: var(--surface);
  border: 1.5px solid var(--border);
  font-family: 'Epilogue', sans-serif;
  font-size: 0.95rem;
  color: var(--ink);
  padding: 11px 14px;
  border-radius: 8px;
  outline: none;
  transition: border-color 0.2s;
}

.field input:focus, .field select:focus { border-color: var(--accent2); }
.field input::placeholder { color: var(--muted); }
.field input.error { border-color: var(--accent); }

/* clubs grid */
.clubs-label {
  font-family: 'Syne', sans-serif;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--muted);
  margin-bottom: 14px;
}

.clubs-instruction {
  font-size: 0.85rem;
  color: var(--muted);
  font-weight: 300;
  margin-bottom: 20px;
}

.clubs-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 12px;
  margin-bottom: 32px;
}

.club-card {
  background: var(--surface);
  border: 2px solid var(--border);
  border-radius: 12px;
  padding: 16px;
  cursor: pointer;
  transition: border-color 0.18s, transform 0.15s, box-shadow 0.15s;
  position: relative;
  user-select: none;
}

.club-card:hover:not(.full):not(.selected) {
  border-color: var(--accent2);
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(42,108,200,0.1);
}

.club-card.selected {
  border-color: var(--accent2);
  background: #eef3fc;
}

.club-card.full {
  opacity: 0.5;
  cursor: not-allowed;
  background: var(--card);
}

.club-icon { font-size: 1.8rem; margin-bottom: 8px; display: block; }

.club-name {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 0.95rem;
  margin-bottom: 6px;
}

.club-bar-wrap {
  height: 4px;
  background: var(--border);
  border-radius: 99px;
  overflow: hidden;
  margin-bottom: 4px;
}

.club-bar {
  height: 100%;
  background: var(--green);
  border-radius: 99px;
  transition: width 0.4s ease;
}

.club-bar.warn { background: var(--yellow); }
.club-bar.full-bar { background: var(--accent); }

.club-count {
  font-size: 0.75rem;
  color: var(--muted);
  font-weight: 400;
}

.full-badge {
  position: absolute;
  top: 10px; right: 10px;
  background: var(--accent);
  color: #fff;
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  padding: 2px 7px;
  border-radius: 99px;
}

.selected-badge {
  position: absolute;
  top: 10px; right: 10px;
  background: var(--accent2);
  color: #fff;
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  padding: 2px 7px;
  border-radius: 99px;
}

/* submit */
.btn-submit {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 0.9rem;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  background: var(--ink);
  color: #fff;
  border: none;
  padding: 14px 40px;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.15s, transform 0.12s;
}

.btn-submit:hover { background: #333; transform: translateY(-1px); }
.btn-submit:disabled { background: var(--border); color: var(--muted); cursor: not-allowed; transform: none; }

/* already submitted notice */
.submitted-notice {
  background: #eef6f0;
  border: 1.5px solid #b3dfc0;
  border-radius: 12px;
  padding: 20px 24px;
  margin-bottom: 28px;
}

.submitted-notice h3 {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1rem;
  color: var(--green);
  margin-bottom: 4px;
}

.submitted-notice p { font-size: 0.9rem; color: var(--muted); font-weight: 300; }

/* ── ADMIN PAGE ── */
.admin-wrap {
  max-width: 1000px;
  margin: 0 auto;
  padding: 48px 24px 80px;
}

.admin-header {
  display: flex;
  align-items: baseline;
  gap: 16px;
  margin-bottom: 32px;
  flex-wrap: wrap;
}

.admin-header h1 {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 2.2rem;
}

.stat-pill {
  background: var(--tag-bg);
  border: 1px solid var(--border);
  border-radius: 99px;
  padding: 4px 14px;
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--muted);
}

/* club summary cards */
.summary-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
  gap: 10px;
  margin-bottom: 40px;
}

.sum-card {
  background: var(--surface);
  border: 1.5px solid var(--border);
  border-radius: 10px;
  padding: 14px;
}

.sum-card .s-icon { font-size: 1.4rem; }
.sum-card .s-name {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 0.82rem;
  margin: 6px 0 8px;
}

.sum-card .s-bar-wrap {
  height: 6px;
  background: var(--border);
  border-radius: 99px;
  overflow: hidden;
  margin-bottom: 5px;
}

.sum-card .s-bar {
  height: 100%;
  border-radius: 99px;
  background: var(--green);
  transition: width 0.5s;
}

.sum-card .s-bar.warn { background: var(--yellow); }
.sum-card .s-bar.full-bar { background: var(--accent); }

.sum-card .s-count {
  font-size: 0.75rem;
  color: var(--muted);
}

/* student list */
.list-controls {
  display: flex;
  gap: 12px;
  margin-bottom: 20px;
  flex-wrap: wrap;
  align-items: center;
}

.search-box {
  flex: 1;
  min-width: 200px;
  background: var(--surface);
  border: 1.5px solid var(--border);
  font-family: 'Epilogue', sans-serif;
  font-size: 0.9rem;
  color: var(--ink);
  padding: 9px 14px;
  border-radius: 8px;
  outline: none;
  transition: border-color 0.2s;
}

.search-box:focus { border-color: var(--accent2); }

.filter-select {
  background: var(--surface);
  border: 1.5px solid var(--border);
  font-family: 'Epilogue', sans-serif;
  font-size: 0.88rem;
  color: var(--ink);
  padding: 9px 14px;
  border-radius: 8px;
  outline: none;
  cursor: pointer;
}

.btn-export {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 0.78rem;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  background: var(--ink);
  color: #fff;
  border: none;
  padding: 9px 20px;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.15s;
  white-space: nowrap;
}

.btn-export:hover { background: #333; }

.btn-reset {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 0.78rem;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  background: transparent;
  color: var(--accent);
  border: 1.5px solid var(--accent);
  padding: 9px 20px;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.15s;
  white-space: nowrap;
}

.btn-reset:hover { background: var(--accent); color: #fff; }

/* table */
.table-wrap {
  background: var(--surface);
  border: 1.5px solid var(--border);
  border-radius: 12px;
  overflow: hidden;
}

table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.9rem;
}

thead th {
  background: var(--tag-bg);
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 0.72rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
  padding: 12px 16px;
  text-align: left;
  border-bottom: 1.5px solid var(--border);
}

tbody tr {
  border-bottom: 1px solid var(--border);
  transition: background 0.12s;
}

tbody tr:last-child { border-bottom: none; }
tbody tr:hover { background: var(--card); }

tbody td {
  padding: 11px 16px;
  color: var(--ink);
}

.no-results {
  text-align: center;
  color: var(--muted);
  font-size: 0.9rem;
  padding: 32px;
  font-style: italic;
  font-weight: 300;
}

.club-tag {
  display: inline-block;
  background: var(--tag-bg);
  border: 1px solid var(--border);
  border-radius: 5px;
  padding: 2px 8px;
  font-size: 0.8rem;
  font-weight: 500;
}

/* Toast */
#toast {
  position: fixed;
  bottom: 28px; left: 50%;
  transform: translateX(-50%) translateY(70px);
  background: var(--ink);
  color: #fff;
  padding: 12px 24px;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: 500;
  transition: transform 0.3s cubic-bezier(0.34,1.56,0.64,1);
  z-index: 999;
  white-space: nowrap;
}

#toast.show { transform: translateX(-50%) translateY(0); }

@media (max-width: 500px) {
  .name-row { flex-direction: column; }
  .clubs-grid { grid-template-columns: 1fr 1fr; }
}
</style>
</head>
<body>

<nav>
  <div class="nav-brand">Club Sign-Up</div>
  <div class="nav-tab active" onclick="showPage('student')">Student</div>
  <div class="nav-tab" onclick="showPage('admin')">Admin View</div>
</nav>

<!-- ══ STUDENT PAGE ══ -->
<div class="page active" id="page-student">
  <div class="student-wrap">
    <div class="page-header">
      <h1>Choose Your Club</h1>
      <p>Select one club to join. Each club has a maximum of 25 students.</p>
    </div>

    <div id="already-notice" style="display:none" class="submitted-notice">
      <h3>✓ Already submitted</h3>
      <p id="already-text"></p>
    </div>

    <div class="name-row">
      <div class="field">
        <label>Student Number</label>
        <input type="text" id="student-num" placeholder="e.g. S001" maxlength="20" />
      </div>
      <div class="field">
        <label>Full Name</label>
        <input type="text" id="student-name" placeholder="Your name" maxlength="60" />
      </div>
    </div>

    <div class="clubs-label">Available Clubs</div>
    <div class="clubs-instruction">Click a club to select it, then press Submit.</div>

    <div class="clubs-grid" id="clubs-grid"></div>

    <button class="btn-submit" id="submit-btn" disabled>Submit Selection</button>
  </div>
</div>

<!-- ══ ADMIN PAGE ══ -->
<div class="page" id="page-admin">
  <div class="admin-wrap">
    <div class="admin-header">
      <h1>All Submissions</h1>
      <span class="stat-pill" id="total-count">0 / 130 students</span>
    </div>

    <div class="summary-grid" id="summary-grid"></div>

    <div class="list-controls">
      <input class="search-box" type="text" id="search-input" placeholder="Search by name or number…" oninput="renderTable()" />
      <select class="filter-select" id="filter-club" onchange="renderTable()">
        <option value="">All Clubs</option>
      </select>
      <button class="btn-export" onclick="exportCSV()">Export CSV</button>
      <button class="btn-reset" onclick="resetAll()">Reset All</button>
    </div>

    <div class="table-wrap">
      <table>
        <thead>
          <tr>
            <th>#</th>
            <th>Student No.</th>
            <th>Name</th>
            <th>Club</th>
            <th>Time</th>
          </tr>
        </thead>
        <tbody id="student-table"></tbody>
      </table>
      <div id="no-results" class="no-results" style="display:none">No matching students found.</div>
    </div>
  </div>
</div>

<div id="toast"></div>

<script>
// ── CONFIG ──
const CLUBS = [
  { id: 'dance',    name: 'Dance',    icon: '💃', max: 25 },
  { id: 'movie',    name: 'Movie',    icon: '🎬', max: 25 },
  { id: 'badminton',name: 'Badminton',icon: '🏸', max: 25 },
  { id: 'makeup',   name: 'Makeup',   icon: '💄', max: 25 },
  { id: 'tennis',   name: 'Tennis',   icon: '🎾', max: 25 },
  { id: 'go',       name: 'Go',       icon: '⬛', max: 25 },
  { id: 'chess',    name: 'Chess',    icon: '♟️', max: 25 },
  { id: 'handball', name: 'Handball', icon: '🤾', max: 25 },
];

// ── STATE (localStorage) ──
function getSubmissions() {
  try { return JSON.parse(localStorage.getItem('club_submissions') || '[]'); } catch { return []; }
}

function saveSubmissions(arr) {
  localStorage.setItem('club_submissions', JSON.stringify(arr));
}

function clubCounts() {
  const counts = {};
  CLUBS.forEach(c => counts[c.id] = 0);
  getSubmissions().forEach(s => { if (counts[s.clubId] !== undefined) counts[s.clubId]++; });
  return counts;
}

// ── NAVIGATION ──
function showPage(page) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
  document.getElementById('page-' + page).classList.add('active');
  document.querySelectorAll('.nav-tab')[page === 'student' ? 0 : 1].classList.add('active');
  if (page === 'admin') renderAdmin();
  if (page === 'student') renderStudentPage();
}

// ── TOAST ──
function toast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2800);
}

// ── STUDENT PAGE ──
let selectedClub = null;

function renderStudentPage() {
  selectedClub = null;
  const counts = clubCounts();
  const grid = document.getElementById('clubs-grid');
  grid.innerHTML = '';

  CLUBS.forEach(club => {
    const count = counts[club.id];
    const isFull = count >= club.max;
    const pct = Math.round((count / club.max) * 100);

    const card = document.createElement('div');
    card.className = 'club-card' + (isFull ? ' full' : '');
    card.dataset.id = club.id;

    let barClass = '';
    if (pct >= 100) barClass = 'full-bar';
    else if (pct >= 80) barClass = 'warn';

    card.innerHTML = `
      <span class="club-icon">${club.icon}</span>
      <div class="club-name">${club.name}</div>
      <div class="club-bar-wrap"><div class="club-bar ${barClass}" style="width:${pct}%"></div></div>
      <div class="club-count">${count} / ${club.max}</div>
      ${isFull ? '<span class="full-badge">Full</span>' : ''}
    `;

    if (!isFull) {
      card.addEventListener('click', () => selectClub(club.id));
    }

    grid.appendChild(card);
  });

  updateSubmitBtn();
  checkAlreadySubmitted();
}

function checkAlreadySubmitted() {
  const numVal = document.getElementById('student-num').value.trim();
  const subs = getSubmissions();
  const existing = numVal ? subs.find(s => s.studentNum === numVal) : null;
  const notice = document.getElementById('already-notice');
  const alreadyText = document.getElementById('already-text');

  if (existing) {
    const club = CLUBS.find(c => c.id === existing.clubId);
    notice.style.display = 'block';
    alreadyText.textContent = `${existing.name} (${existing.studentNum}) already selected ${club?.icon} ${club?.name}.`;
  } else {
    notice.style.display = 'none';
  }
}

function selectClub(id) {
  selectedClub = id;
  document.querySelectorAll('.club-card').forEach(card => {
    const isSelected = card.dataset.id === id;
    card.classList.toggle('selected', isSelected);
    // update badge
    const old = card.querySelector('.selected-badge');
    if (old) old.remove();
    if (isSelected) {
      const badge = document.createElement('span');
      badge.className = 'selected-badge';
      badge.textContent = '✓ Selected';
      card.appendChild(badge);
    }
  });
  updateSubmitBtn();
}

function updateSubmitBtn() {
  const name = document.getElementById('student-name').value.trim();
  const num = document.getElementById('student-num').value.trim();
  document.getElementById('submit-btn').disabled = !(name && num && selectedClub);
}

document.getElementById('student-name').addEventListener('input', updateSubmitBtn);
document.getElementById('student-num').addEventListener('input', () => { updateSubmitBtn(); checkAlreadySubmitted(); });

document.getElementById('submit-btn').addEventListener('click', () => {
  const name = document.getElementById('student-name').value.trim();
  const num = document.getElementById('student-num').value.trim();
  if (!name || !num || !selectedClub) return;

  const subs = getSubmissions();

  // Check duplicate student number
  if (subs.find(s => s.studentNum === num)) {
    document.getElementById('student-num').classList.add('error');
    toast('⚠ This student number has already submitted.');
    setTimeout(() => document.getElementById('student-num').classList.remove('error'), 1500);
    return;
  }

  // Check capacity again
  const counts = clubCounts();
  const club = CLUBS.find(c => c.id === selectedClub);
  if (counts[selectedClub] >= club.max) {
    toast('⚠ That club just filled up. Please choose another.');
    renderStudentPage();
    return;
  }

  subs.push({
    studentNum: num,
    name,
    clubId: selectedClub,
    time: new Date().toLocaleString()
  });
  saveSubmissions(subs);

  toast(`✓ ${name} joined ${club.icon} ${club.name}!`);
  document.getElementById('student-name').value = '';
  document.getElementById('student-num').value = '';
  selectedClub = null;
  renderStudentPage();
});

// ── ADMIN PAGE ──
function renderAdmin() {
  const subs = getSubmissions();
  const counts = clubCounts();

  // total
  document.getElementById('total-count').textContent = `${subs.length} / 130 students`;

  // summary cards
  const sg = document.getElementById('summary-grid');
  sg.innerHTML = '';
  CLUBS.forEach(club => {
    const count = counts[club.id];
    const pct = Math.round((count / club.max) * 100);
    let barClass = pct >= 100 ? 'full-bar' : pct >= 80 ? 'warn' : '';
    const card = document.createElement('div');
    card.className = 'sum-card';
    card.innerHTML = `
      <div class="s-icon">${club.icon}</div>
      <div class="s-name">${club.name}</div>
      <div class="s-bar-wrap"><div class="s-bar ${barClass}" style="width:${pct}%"></div></div>
      <div class="s-count">${count} / ${club.max}</div>
    `;
    sg.appendChild(card);
  });

  // filter dropdown
  const filterSel = document.getElementById('filter-club');
  filterSel.innerHTML = '<option value="">All Clubs</option>';
  CLUBS.forEach(c => {
    const opt = document.createElement('option');
    opt.value = c.id;
    opt.textContent = `${c.icon} ${c.name}`;
    filterSel.appendChild(opt);
  });

  renderTable();
}

function renderTable() {
  const subs = getSubmissions();
  const search = document.getElementById('search-input').value.trim().toLowerCase();
  const filterClub = document.getElementById('filter-club').value;

  let filtered = subs.filter(s => {
    const matchSearch = !search ||
      s.name.toLowerCase().includes(search) ||
      s.studentNum.toLowerCase().includes(search);
    const matchClub = !filterClub || s.clubId === filterClub;
    return matchSearch && matchClub;
  });

  const tbody = document.getElementById('student-table');
  tbody.innerHTML = '';

  if (filtered.length === 0) {
    document.getElementById('no-results').style.display = 'block';
  } else {
    document.getElementById('no-results').style.display = 'none';
    filtered.forEach((s, i) => {
      const club = CLUBS.find(c => c.id === s.clubId);
      const tr = document.createElement('tr');
      tr.innerHTML = `
        <td style="color:var(--muted);font-size:0.8rem">${i + 1}</td>
        <td style="font-family:'Syne',sans-serif;font-weight:600;font-size:0.85rem">${s.studentNum}</td>
        <td>${s.name}</td>
        <td><span class="club-tag">${club?.icon} ${club?.name || s.clubId}</span></td>
        <td style="color:var(--muted);font-size:0.8rem">${s.time}</td>
      `;
      tbody.appendChild(tr);
    });
  }
}

function exportCSV() {
  const subs = getSubmissions();
  if (subs.length === 0) { toast('No data to export.'); return; }
  const rows = [['Student Number', 'Name', 'Club', 'Time']];
  subs.forEach(s => {
    const club = CLUBS.find(c => c.id === s.clubId);
    rows.push([s.studentNum, s.name, club?.name || s.clubId, s.time]);
  });
  const csv = rows.map(r => r.map(v => `"${v}"`).join(',')).join('\n');
  const blob = new Blob([csv], { type: 'text/csv' });
  const a = document.createElement('a');
  a.href = URL.createObjectURL(blob);
  a.download = 'club_selections.csv';
  a.click();
  toast('CSV exported!');
}

function resetAll() {
  if (!confirm('Reset ALL submissions? This cannot be undone.')) return;
  localStorage.removeItem('club_submissions');
  toast('All submissions cleared.');
  renderAdmin();
}

// ── INIT ──
renderStudentPage();
</script>
</body>
</html>
