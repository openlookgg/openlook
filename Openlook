<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>OpenLook — مهامي</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: system-ui, -apple-system, 'Segoe UI', sans-serif;
    background: #0f0f0f;
    color: #e8e8e8;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 4rem 1.5rem;
  }
  h1 { font-size: 2.4rem; font-weight: 600; letter-spacing: -1px; margin-bottom: 0.3rem; }
  .sub { color: #777; font-size: 0.95rem; margin-bottom: 3rem; }
  .box { width: 100%; max-width: 540px; }
  .row { display: flex; gap: 10px; margin-bottom: 2rem; }
  input[type="text"] {
    flex: 1;
    padding: 14px 16px;
    background: #1a1a1a;
    border: 1px solid #2a2a2a;
    border-radius: 10px;
    color: #e8e8e8;
    font-size: 1rem;
    outline: none;
    transition: border 0.2s;
  }
  input[type="text"]:focus { border-color: #555; }
  button {
    padding: 14px 24px;
    background: #e8e8e8;
    color: #0f0f0f;
    border: none;
    border-radius: 10px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: opacity 0.2s;
  }
  button:hover { opacity: 0.85; }
  ul { list-style: none; }
  li {
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 14px 0;
    border-bottom: 1px solid #1f1f1f;
  }
  li:last-child { border-bottom: none; }
  li.done .txt { text-decoration: line-through; color: #555; }
  .txt { flex: 1; font-size: 1rem; }
  .del {
    background: none;
    border: none;
    color: #555;
    font-size: 1.4rem;
    cursor: pointer;
    padding: 0 8px;
    line-height: 1;
  }
  .del:hover { color: #e8e8e8; }
  .empty { color: #444; text-align: center; padding: 2rem 0; font-size: 0.95rem; }
  .count { color: #555; font-size: 0.85rem; margin-top: 1.5rem; text-align: center; }
</style>
</head>
<body>
  <h1>OpenLook</h1>
  <p class="sub">مهامك، بدون تعقيد.</p>

  <div class="box">
    <div class="row">
      <input type="text" id="inp" placeholder="اكتب مهمة جديدة..." onkeydown="if(event.key==='Enter') add()">
      <button onclick="add()">إضافة</button>
    </div>
    <ul id="list"></ul>
    <div class="count" id="count"></div>
  </div>

<script>
const inp = document.getElementById('inp');
const list = document.getElementById('list');
const count = document.getElementById('count');
let tasks = JSON.parse(localStorage.getItem('openlook_tasks') || '[]');

function save() { localStorage.setItem('openlook_tasks', JSON.stringify(tasks)); }

function render() {
  list.innerHTML = '';
  if (tasks.length === 0) {
    list.innerHTML = '<div class="empty">لا مهام بعد. أضف أول وحدة.</div>';
    count.textContent = '';
    return;
  }
  tasks.forEach((t, i) => {
    const li = document.createElement('li');
    if (t.done) li.classList.add('done');

    const cb = document.createElement('input');
    cb.type = 'checkbox';
    cb.checked = t.done;
    cb.onchange = () => { tasks[i].done = cb.checked; save(); render(); };

    const span = document.createElement('span');
    span.className = 'txt';
    span.textContent = t.text;

    const del = document.createElement('button');
    del.className = 'del';
    del.textContent = '×';
    del.onclick = () => { tasks.splice(i, 1); save(); render(); };

    li.appendChild(cb);
    li.appendChild(span);
    li.appendChild(del);
    list.appendChild(li);
  });
  const left = tasks.filter(t => !t.done).length;
  count.textContent = left + ' مهمة متبقية من ' + tasks.length;
}

function add() {
  const text = inp.value.trim();
  if (!text) return;
  tasks.push({ text, done: false });
  inp.value = '';
  save();
  render();
}

render();
</script>
</body>
</html>
