<!DOCTYPE html>
<html lang="th" class="dark">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>AURUM GOLD - แพลตฟอร์มออมทองดิจิทัล</title>
<script src="https://cdn.tailwindcss.com"></script>
<script>
tailwind.config = { darkMode: 'class', theme: { extend: {
  colors: { navy: { 800: '#0f172a', 900: '#0b0f19', 950: '#030712' } },
  fontFamily: { sans: ['Kanit', 'Inter', 'sans-serif'] } } } }
</script>
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.1/dist/chart.umd.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Kanit:wght@300;400;500;600;700&display=swap" rel="stylesheet">
<style>
:root { box-sizing: border-box; padding-top: env(safe-area-inset-top, 0px); padding-bottom: env(safe-area-inset-bottom, 0px); }
html { scroll-padding-top: env(safe-area-inset-top, 0px); }
body { font-family: 'Kanit','Inter',sans-serif; background: #030712; color: #f1f5f9; }
.gold-text { background: linear-gradient(135deg,#fde68a,#f59e0b 50%,#d97706); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
.gold-bg { background: linear-gradient(135deg,#f59e0b,#d97706); }
.gold-bg:hover { background: linear-gradient(135deg,#fbbf24,#f59e0b); }
.glass { background: rgba(15,23,42,.8); backdrop-filter: blur(16px); border: 1px solid rgba(255,255,255,.08); }
.glow { box-shadow: 0 0 20px rgba(245,158,11,.15); border: 1px solid rgba(245,158,11,.25); }
.pulse { animation: pulse 2s infinite; }
@keyframes pulse { 0%{box-shadow:0 0 0 0 rgba(16,185,129,.7)} 70%{box-shadow:0 0 0 8px rgba(16,185,129,0)} 100%{box-shadow:0 0 0 0 rgba(16,185,129,0)} }
.scroll-x { overflow-x: auto; max-width: 100%; }
</style>
</head>
<body class="min-h-screen flex flex-col selection:bg-amber-500 selection:text-navy-950">

<header class="sticky top-0 z-40 glass border-b border-slate-800/80 px-4 lg:px-8 py-3" style="top:env(safe-area-inset-top,0px)">
  <div class="max-w-7xl mx-auto flex items-center justify-between gap-3">
    <div class="flex items-center gap-3">
      <div class="w-11 h-11 rounded-2xl gold-bg flex items-center justify-center text-navy-950 text-2xl shadow-lg shadow-amber-500/20">🪙</div>
      <div>
        <div class="flex items-center gap-2">
          <h1 class="font-extrabold text-xl leading-none tracking-wide gold-text uppercase">AURUM GOLD</h1>
          <span class="text-[10px] bg-amber-500/20 text-amber-300 font-mono font-semibold px-2 py-0.5 rounded-full border border-amber-500/30">PRO</span>
        </div>
        <span class="text-[10px] text-slate-400 tracking-wider font-light block mt-0.5">แพลตฟอร์มออมทองดิจิทัล</span>
      </div>
    </div>
    <div class="hidden lg:flex items-center gap-4 bg-navy-900/90 px-4 py-1.5 rounded-full border border-slate-800 text-xs">
      <span class="flex items-center gap-2"><span class="w-2.5 h-2.5 rounded-full bg-emerald-500 pulse"></span>ข้อมูลจำลอง</span>
      <span class="text-slate-700">|</span>
      <span class="font-mono">Spot: <span class="text-amber-400 font-semibold" id="spot">$2,742.50</span></span>
      <span class="text-slate-700">|</span>
      <span class="font-mono">FX: <span id="fx">35.82</span> THB/$</span>
    </div>
    <div class="flex items-center gap-3">
      <button id="modeBtn" class="px-3.5 py-2 rounded-xl bg-slate-900 hover:bg-slate-800 text-xs font-semibold border border-amber-500/30 transition">🛡️ <span id="modeLabel">สลับเป็น Admin</span></button>
      <div class="hidden sm:flex items-center gap-2 pl-3 border-l border-slate-800">
        <div class="w-9 h-9 rounded-full border-2 border-amber-500/60 bg-navy-800 text-amber-400 flex items-center justify-center text-sm font-bold">ส</div>
        <div><div class="text-xs font-bold">คุณสมชาย มั่งคั่ง ✔</div><span class="text-[9px] text-emerald-400 bg-emerald-950/80 border border-emerald-800/80 px-1.5 rounded font-mono">KYC L2</span></div>
      </div>
    </div>
  </div>
</header>

<main class="max-w-7xl w-full mx-auto px-4 lg:px-8 py-6 space-y-6 flex-grow">

  <!-- Price banner -->
  <section class="glass rounded-2xl p-5 glow flex flex-wrap items-center justify-between gap-4">
    <div>
      <div class="flex items-center gap-2 flex-wrap">
        <span class="text-xs text-slate-400 font-semibold uppercase tracking-wider">ราคาทองคำแท่ง 96.5%</span>
        <span class="text-[10px] bg-amber-950 text-amber-400 border border-amber-800/60 px-2 py-0.5 rounded-full font-mono">DEMO</span>
      </div>
      <div class="text-xs text-slate-400 mt-1">อัปเดตล่าสุด: <span id="updated" class="text-slate-200 font-mono">--:--:--</span> (ครั้งที่ <span id="tick">0</span>)</div>
    </div>
    <div class="flex items-center gap-6 sm:gap-10">
      <div><span class="text-xs text-slate-400 block">รับซื้อคืน (บาทละ)</span><span class="text-2xl sm:text-3xl font-extrabold font-mono text-emerald-400" id="buyP">43,850</span><span class="text-[10px] block" id="chg"></span></div>
      <div class="h-10 w-px bg-slate-800"></div>
      <div><span class="text-xs text-slate-400 block">ขายออก (บาทละ)</span><span class="text-2xl sm:text-3xl font-extrabold font-mono text-amber-400" id="sellP">43,950</span></div>
    </div>
  </section>

  <!-- USER VIEW -->
  <div id="userView" class="space-y-6">
    <section class="grid grid-cols-1 lg:grid-cols-3 gap-4">
      <div class="glass rounded-2xl p-5 glow">
        <div class="text-xs text-slate-400">พอร์ตทองของฉัน</div>
        <div class="text-3xl font-extrabold font-mono gold-text mt-1" id="pfValue">฿0</div>
        <div class="text-xs text-slate-400 mt-2">ถือครอง <span class="text-slate-100 font-mono" id="pfWeight">0.0000</span> บาททอง</div>
        <div class="text-xs mt-1">กำไร/ขาดทุน: <span id="pfPL" class="font-mono font-semibold"></span></div>
      </div>
      <div class="glass rounded-2xl p-5 lg:col-span-2">
        <div class="text-sm font-semibold mb-3">ราคาย้อนหลัง (รับซื้อคืน)</div>
        <div style="position:relative;height:180px"><canvas id="chart"></canvas></div>
      </div>
    </section>

    <section class="grid grid-cols-1 lg:grid-cols-2 gap-4">
      <div class="glass rounded-2xl p-5">
        <h2 class="font-semibold mb-3">คำนวณการออมทอง</h2>
        <label class="text-xs text-slate-400">จำนวนเงินที่ต้องการออม (บาท)</label>
        <input id="amt" type="number" min="100" value="5000" class="w-full mt-1 mb-4 bg-navy-900 border border-slate-700 rounded-xl px-4 py-2.5 font-mono focus:outline-none focus:border-amber-500">
        <div class="grid grid-cols-2 gap-3 text-center">
          <div class="bg-navy-900 rounded-xl p-3"><div class="text-[11px] text-slate-400">ได้รับทอง (บาททอง)</div><div class="text-xl font-mono text-amber-400" id="outBaht">0</div></div>
          <div class="bg-navy-900 rounded-xl p-3"><div class="text-[11px] text-slate-400">คิดเป็นกรัม</div><div class="text-xl font-mono text-amber-400" id="outGram">0</div></div>
        </div>
        <button id="buyBtn" class="gold-bg text-navy-950 font-semibold w-full mt-4 py-2.5 rounded-xl transition">ซื้อทอง (จำลอง)</button>
        <p class="text-[11px] text-slate-500 mt-2" id="msg">1 บาททอง = 15.244 กรัม</p>
      </div>
      <div class="glass rounded-2xl p-5">
        <h2 class="font-semibold mb-3">แผนออมทอง</h2>
        <div class="space-y-3">
          <button class="plan w-full text-left bg-navy-900 hover:border-amber-500/60 border border-slate-800 rounded-xl p-3 transition" data-amt="500"><b>ออมเริ่มต้น</b> <span class="float-right font-mono text-amber-400">฿500/เดือน</span><div class="text-xs text-slate-400">เหมาะสำหรับผู้เริ่มออม</div></button>
          <button class="plan w-full text-left bg-navy-900 hover:border-amber-500/60 border border-slate-800 rounded-xl p-3 transition" data-amt="3000"><b>ออมสม่ำเสมอ</b> <span class="float-right font-mono text-amber-400">฿3,000/เดือน</span><div class="text-xs text-slate-400">สะสมต่อเนื่องระยะยาว</div></button>
          <button class="plan w-full text-left bg-navy-900 hover:border-amber-500/60 border border-slate-800 rounded-xl p-3 transition" data-amt="10000"><b>ออมพรีเมียม</b> <span class="float-right font-mono text-amber-400">฿10,000/เดือน</span><div class="text-xs text-slate-400">เป้าหมายสร้างความมั่งคั่ง</div></button>
        </div>
      </div>
    </section>

    <section class="glass rounded-2xl p-5">
      <h2 class="font-semibold mb-3">ประวัติธุรกรรม</h2>
      <div class="scroll-x"><table class="w-full text-sm min-w-[420px]">
        <thead class="text-xs text-slate-400 text-left"><tr><th class="py-2">เวลา</th><th>รายการ</th><th>จำนวนเงิน</th><th>ทองที่ได้</th></tr></thead>
        <tbody id="txBody"><tr><td colspan="4" class="py-4 text-slate-500 text-center">ยังไม่มีธุรกรรม</td></tr></tbody>
      </table></div>
    </section>
  </div>

  <!-- ADMIN VIEW -->
  <div id="adminView" class="space-y-6 hidden">
    <section class="grid grid-cols-2 lg:grid-cols-4 gap-4">
      <div class="glass rounded-2xl p-4"><div class="text-xs text-slate-400">ผู้ใช้ทั้งหมด</div><div class="text-2xl font-mono text-amber-400">12,480</div></div>
      <div class="glass rounded-2xl p-4"><div class="text-xs text-slate-400">ทองในระบบ (บาททอง)</div><div class="text-2xl font-mono text-amber-400">3,942</div></div>
      <div class="glass rounded-2xl p-4"><div class="text-xs text-slate-400">ยอดซื้อวันนี้</div><div class="text-2xl font-mono text-emerald-400">฿2.4M</div></div>
      <div class="glass rounded-2xl p-4"><div class="text-xs text-slate-400">KYC รอตรวจ</div><div class="text-2xl font-mono text-slate-100">37</div></div>
    </section>
    <section class="glass rounded-2xl p-5 glow">
      <h2 class="font-semibold mb-3">ตั้งค่าส่วนต่างราคา (Spread)</h2>
      <div class="flex flex-wrap items-end gap-3">
        <div><label class="text-xs text-slate-400 block">ส่วนต่างซื้อ-ขาย (บาท)</label><input id="spread" type="number" value="100" min="0" class="mt-1 bg-navy-900 border border-slate-700 rounded-xl px-4 py-2 font-mono w-40 focus:outline-none focus:border-amber-500"></div>
        <button id="spreadBtn" class="gold-bg text-navy-950 font-semibold px-5 py-2 rounded-xl transition">บันทึก</button>
        <span class="text-xs text-slate-400" id="spreadMsg"></span>
      </div>
    </section>
  </div>
</main>

<footer class="border-t border-slate-800 py-6 text-center text-xs text-slate-500 px-4">
  © 2026 AURUM GOLD · เว็บไซต์ต้นแบบ ราคาและธุรกรรมทั้งหมดเป็นข้อมูลจำลองเพื่อการสาธิตเท่านั้น
</footer>

<script>
const G = 15.244;
let buy = 43850, spread = 100, tick = 0, isAdmin = false;
let hold = 0, cost = 0;
const hist = [43500,43550,43620,43580,43700,43760,43700,43810,43790,43850];
const $ = id => document.getElementById(id);
const f = n => Math.round(n).toLocaleString('en-US');

const chart = new Chart($('chart'), {
  type: 'line',
  data: { labels: hist.map((_, i) => i + 1), datasets: [{ data: hist, borderColor: '#f59e0b', backgroundColor: 'rgba(245,158,11,.12)', fill: true, tension: .35, pointRadius: 0 }] },
  options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } },
    scales: { x: { display: false }, y: { ticks: { color: '#94a3b8' }, grid: { color: 'rgba(255,255,255,.05)' } } } }
});

function render() {
  const sell = buy + spread;
  $('buyP').textContent = f(buy); $('sellP').textContent = f(sell);
  const d = buy - hist[hist.length - 2];
  $('chg').textContent = (d >= 0 ? '▲ +' : '▼ ') + d + ' บาท';
  $('chg').className = 'text-[10px] block ' + (d >= 0 ? 'text-emerald-400' : 'text-red-400');
  $('updated').textContent = new Date().toLocaleTimeString('th-TH');
  $('tick').textContent = tick;
  $('spot').textContent = '$' + (buy / 15.98).toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',');
  const val = hold * buy;
  $('pfValue').textContent = '฿' + f(val);
  $('pfWeight').textContent = hold.toFixed(4);
  const pl = val - cost;
  $('pfPL').textContent = (pl >= 0 ? '+' : '') + f(pl) + ' บาท';
  $('pfPL').className = 'font-mono font-semibold ' + (pl >= 0 ? 'text-emerald-400' : 'text-red-400');
  calc();
}
function calc() {
  const a = parseFloat($('amt').value) || 0;
  const w = a / (buy + spread);
  $('outBaht').textContent = w.toFixed(4);
  $('outGram').textContent = (w * G).toFixed(3);
}
function step() {
  tick++;
  buy = Math.max(1000, buy + Math.round((Math.random() - 0.48) * 100 / 50) * 50);
  hist.push(buy); hist.shift();
  chart.data.datasets[0].data = hist; chart.update('none');
  render();
}
$('amt').addEventListener('input', calc);
$('buyBtn').onclick = () => {
  const a = parseFloat($('amt').value) || 0;
  if (a < 100) { $('msg').textContent = 'ขั้นต่ำ 100 บาท'; return; }
  const w = a / (buy + spread);
  hold += w; cost += a;
  const body = $('txBody');
  if (body.children[0].children.length === 1) body.innerHTML = '';
  const tr = document.createElement('tr');
  tr.className = 'border-t border-slate-800';
  tr.innerHTML = `<td class="py-2 font-mono text-xs">${new Date().toLocaleTimeString('th-TH')}</td><td>ซื้อทอง</td><td class="font-mono">฿${f(a)}</td><td class="font-mono text-amber-400">${w.toFixed(4)}</td>`;
  body.prepend(tr);
  $('msg').textContent = 'ทำรายการสำเร็จ (จำลอง)';
  render();
};
document.querySelectorAll('.plan').forEach(b => b.onclick = () => { $('amt').value = b.dataset.amt; calc(); window.scrollTo({ top: 0, behavior: 'smooth' }); });
$('modeBtn').onclick = () => {
  isAdmin = !isAdmin;
  $('userView').classList.toggle('hidden', isAdmin);
  $('adminView').classList.toggle('hidden', !isAdmin);
  $('modeLabel').textContent = isAdmin ? 'สลับเป็นผู้ใช้' : 'สลับเป็น Admin';
};
$('spreadBtn').onclick = () => {
  const v = parseFloat($('spread').value);
  if (isNaN(v) || v < 0) { $('spreadMsg').textContent = 'ค่าไม่ถูกต้อง'; return; }
  spread = v; $('spreadMsg').textContent = 'บันทึกแล้ว'; render();
};
render();
setInterval(step, 5000);
</script>
</body>
</html>
