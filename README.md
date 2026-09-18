<!DOCTYPE html>
<html lang="lv">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mēmu Kastes</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Archivo+Black&family=DM+Sans:wght@400;500;700&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #1b2a8a;
    --bg-deep: #141f6b;
    --ink: #14123a;
    --paper: #ffffff;
    --paper-soft: #eef0ff;
    --lemon: #ffe14d;
    --pink: #ff6fa8;
    --mint: #5eead4;
    --sky: #6ec1ff;
    --orange: #ff9a3d;
    --violet: #b48cff;

    --c-common: #e6e8f5;
    --c-rare: #9fd8ff;
    --c-epic: #d3b8ff;
    --c-legendary: #ffe14d;
    --c-mythic: #ff8fbe;
    --c-divine: #b6fff0;

    --display: "Archivo Black", "Arial Black", Impact, sans-serif;
    --body: "DM Sans", system-ui, -apple-system, "Segoe UI", Roboto, sans-serif;
  }

  * { box-sizing: border-box; }

  html { background: var(--bg-deep); }

  body {
    margin: 0;
    min-height: 100vh;
    font-family: var(--body);
    color: var(--ink);
    background:
      radial-gradient(circle at 1px 1px, rgba(255,255,255,.09) 1.5px, transparent 0) 0 0 / 26px 26px,
      var(--bg);
  }

  button { font: inherit; color: inherit; cursor: pointer; }
  button:disabled { cursor: not-allowed; }
  :focus-visible { outline: 3px solid var(--lemon); outline-offset: 3px; }

  /* ---------- top bar ---------- */
  .topbar {
    position: sticky; top: 0; z-index: 20;
    display: flex; align-items: center; justify-content: space-between; gap: 16px;
    padding: 14px clamp(16px, 4vw, 40px);
    background: var(--bg-deep);
    border-bottom: 4px solid var(--ink);
  }
  .brand {
    margin: 0;
    font-family: var(--display);
    font-size: clamp(22px, 4vw, 34px);
    line-height: 1;
    color: var(--paper);
    letter-spacing: -0.02em;
    text-shadow: 3px 3px 0 var(--ink);
  }
  .wallet {
    display: flex; align-items: center; gap: 10px;
    background: var(--lemon);
    border: 3px solid var(--ink);
    border-radius: 999px;
    padding: 6px 18px 6px 8px;
    box-shadow: 4px 4px 0 var(--ink);
  }
  .wallet .coin {
    width: 34px; height: 34px; border-radius: 50%;
    display: grid; place-items: center;
    background: var(--orange);
    border: 3px solid var(--ink);
    font-size: 16px;
  }
  .wallet output {
    font-family: var(--display);
    font-size: clamp(20px, 3.4vw, 28px);
    min-width: 3ch;
  }
  .wallet.bump { animation: bump .35s ease; }
  @keyframes bump { 40% { transform: scale(1.08) rotate(-1.5deg); } }

  /* ---------- layout ---------- */
  main {
    max-width: 1240px;
    margin: 0 auto;
    padding: clamp(20px, 4vw, 40px) clamp(16px, 4vw, 40px) 80px;
    display: grid;
    grid-template-columns: minmax(0, 1.25fr) minmax(0, 1fr);
    gap: clamp(24px, 4vw, 44px);
    align-items: start;
  }
  @media (max-width: 900px) { main { grid-template-columns: 1fr; } }

  h2 {
    margin: 0 0 6px;
    font-family: var(--display);
    font-size: clamp(26px, 4vw, 38px);
    color: var(--paper);
    text-shadow: 3px 3px 0 var(--ink);
    letter-spacing: -0.01em;
  }
  .lead { margin: 0 0 20px; color: #dfe3ff; max-width: 52ch; line-height: 1.5; }

  /* ---------- shop ---------- */
  .boxes { display: grid; grid-template-columns: repeat(auto-fill, minmax(230px, 1fr)); gap: 22px; }

  .box {
    position: relative;
    display: flex; flex-direction: column; gap: 12px;
    padding: 18px;
    background: var(--paper);
    border: 3px solid var(--ink);
    border-radius: 24px;
    box-shadow: 6px 6px 0 var(--ink);
    transition: transform .12s ease, box-shadow .12s ease;
  }
  .box:nth-child(odd) { transform: rotate(-.6deg); }
  .box:nth-child(even) { transform: rotate(.6deg); }
  .box:hover { transform: translate(-2px, -3px) rotate(0); box-shadow: 8px 9px 0 var(--ink); }
  .box .art {
    height: 110px; border-radius: 16px; border: 3px solid var(--ink);
    display: grid; place-items: center; font-size: 62px;
    background: var(--tint, var(--paper-soft));
  }
  .box h3 { margin: 0; font-family: var(--display); font-size: 22px; letter-spacing: -.01em; }
  .odds { display: flex; flex-wrap: wrap; gap: 6px; margin: 0; padding: 0; list-style: none; }
  .odds li {
    font-size: 12.5px; font-weight: 700;
    padding: 3px 9px; border: 2px solid var(--ink); border-radius: 999px;
    background: var(--chip);
  }
  .buy {
    margin-top: auto;
    display: flex; align-items: center; justify-content: center; gap: 8px;
    padding: 11px 14px;
    font-family: var(--display); font-size: 18px;
    background: var(--pink);
    border: 3px solid var(--ink); border-radius: 999px;
    box-shadow: 3px 3px 0 var(--ink);
    transition: transform .1s, box-shadow .1s, background .1s;
  }
  .buy:hover:not(:disabled) { transform: translate(-1px, -1px); box-shadow: 4px 4px 0 var(--ink); }
  .buy:active:not(:disabled) { transform: translate(3px, 3px); box-shadow: 0 0 0 var(--ink); }
  .buy:disabled { background: #d5d7e6; color: #6c7090; box-shadow: 3px 3px 0 #8d90ad; border-color: #6c7090; }

  .buy.free:not(:disabled) { background: var(--mint); }
  .box.free-box { border-style: dashed; }

  .hustle {
    margin-top: 26px;
    display: flex; align-items: center; gap: 14px; flex-wrap: wrap;
    padding: 14px 18px;
    background: var(--bg-deep);
    border: 3px dashed rgba(255,255,255,.45);
    border-radius: 18px;
    color: #dfe3ff;
  }
  .hustle button {
    padding: 9px 16px;
    font-weight: 700;
    background: var(--mint);
    color: var(--ink);
    border: 3px solid var(--ink); border-radius: 999px;
    box-shadow: 3px 3px 0 var(--ink);
  }
  .hustle button:active { transform: translate(3px, 3px); box-shadow: none; }

  /* ---------- inventory ---------- */
  .inv-head { display: flex; align-items: flex-end; justify-content: space-between; gap: 12px; flex-wrap: wrap; margin-bottom: 14px; }
  .inv-head h2 { margin: 0; }
  .sell-all {
    padding: 10px 16px; font-family: var(--display); font-size: 15px;
    background: var(--lemon);
    border: 3px solid var(--ink); border-radius: 999px;
    box-shadow: 3px 3px 0 var(--ink);
  }
  .sell-all:disabled { background: #d5d7e6; color: #6c7090; border-color: #6c7090; box-shadow: 3px 3px 0 #8d90ad; }
  .sell-all:active:not(:disabled) { transform: translate(3px, 3px); box-shadow: none; }

  .inventory { display: grid; gap: 12px; }
  .meme {
    display: grid; grid-template-columns: 58px 1fr auto; gap: 12px; align-items: center;
    padding: 10px 12px;
    background: var(--tint, var(--paper));
    border: 3px solid var(--ink); border-radius: 16px;
    box-shadow: 4px 4px 0 var(--ink);
  }
  .meme .emoji {
    width: 58px; height: 58px; display: grid; place-items: center;
    font-size: 32px; background: var(--paper);
    border: 3px solid var(--ink); border-radius: 12px;
  }
  .meme b { display: block; font-size: 16px; line-height: 1.2; }
  .meme small { font-weight: 500; }
  .meme .actions { display: flex; flex-direction: column; gap: 6px; }
  .meme .actions button {
    padding: 5px 12px; font-size: 13px; font-weight: 700;
    background: var(--paper);
    border: 2px solid var(--ink); border-radius: 999px;
  }
  .meme .actions button:hover { background: var(--lemon); }
  .count { font-family: var(--display); }

  .empty {
    padding: 28px 20px; text-align: center; line-height: 1.5;
    background: rgba(255,255,255,.08);
    border: 3px dashed rgba(255,255,255,.4); border-radius: 18px;
    color: #dfe3ff;
  }

  .stats { margin-top: 22px; display: flex; gap: 10px; flex-wrap: wrap; }
  .stats span {
    padding: 6px 12px; font-size: 13.5px; font-weight: 700;
    background: var(--bg-deep); color: #dfe3ff;
    border: 2px solid rgba(255,255,255,.35); border-radius: 999px;
  }
  .reset {
    margin-top: 16px; padding: 7px 14px; font-size: 13px;
    background: transparent; color: #b9c0f5;
    border: 2px solid rgba(255,255,255,.3); border-radius: 999px;
  }
  .reset:hover { color: var(--paper); border-color: var(--paper); }

  /* ---------- opening overlay ---------- */
  .overlay {
    position: fixed; inset: 0; z-index: 50;
    display: none; place-items: center;
    background: rgba(10, 14, 60, .86);
    padding: 20px;
  }
  .overlay.show { display: grid; }
  .stage { text-align: center; width: min(360px, 100%); }
  .shaking { font-size: 130px; animation: shake .9s ease-in-out; filter: drop-shadow(6px 8px 0 rgba(0,0,0,.35)); }
  @keyframes shake {
    0%, 100% { transform: rotate(0) scale(1); }
    15% { transform: rotate(-14deg) scale(1.05); }
    30% { transform: rotate(14deg) scale(1.1); }
    45% { transform: rotate(-12deg) scale(1.15); }
    60% { transform: rotate(12deg) scale(1.2); }
    80% { transform: rotate(-6deg) scale(1.25); }
  }
  .reveal {
    padding: 26px 22px 22px;
    background: var(--tint, var(--paper));
    border: 4px solid var(--ink); border-radius: 28px;
    box-shadow: 8px 8px 0 var(--ink);
    animation: pop .35s cubic-bezier(.2, 1.4, .4, 1);
  }
  @keyframes pop { from { transform: scale(.4) rotate(-6deg); opacity: 0; } to { transform: scale(1) rotate(0); opacity: 1; } }
  .reveal .big { font-size: 96px; line-height: 1.1; }
  .reveal h3 { margin: 8px 0 4px; font-family: var(--display); font-size: 26px; letter-spacing: -.01em; }
  .reveal p { margin: 0 0 18px; font-weight: 700; }
  .reveal .row { display: flex; gap: 10px; justify-content: center; flex-wrap: wrap; }
  .reveal .row button {
    padding: 10px 18px; font-family: var(--display); font-size: 15px;
    border: 3px solid var(--ink); border-radius: 999px; box-shadow: 3px 3px 0 var(--ink);
    background: var(--paper);
  }
  .reveal .row .primary { background: var(--pink); }
  .reveal .row button:active { transform: translate(3px, 3px); box-shadow: none; }

  /* ---------- toast ---------- */
  .toast {
    position: fixed; left: 50%; bottom: 24px; z-index: 60;
    transform: translate(-50%, 30px); opacity: 0; pointer-events: none;
    padding: 12px 20px; font-weight: 700;
    background: var(--paper); border: 3px solid var(--ink); border-radius: 999px;
    box-shadow: 4px 4px 0 var(--ink);
    transition: transform .2s, opacity .2s;
  }
  .toast.show { transform: translate(-50%, 0); opacity: 1; }

  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after { animation-duration: .01ms !important; transition-duration: .01ms !important; }
    .box:nth-child(odd), .box:nth-child(even) { transform: none; }
  }
</style>
</head>
<body>

<header class="topbar">
  <h1 class="brand">Mēmu Kastes</h1>
  <div class="wallet" id="wallet" aria-live="polite">
    <span class="coin" aria-hidden="true">🪙</span>
    <output id="coins">0</output>
  </div>
</header>

<main>
  <section aria-labelledby="shop-title">
    <h2 id="shop-title">Veikals</h2>
    <p class="lead">Nopērc kasti, atver to un uzzini, kurš mēms iekšā. Pārdod mēmus, lai nopelnītu monētas dārgākām kastēm.</p>
    <div class="boxes" id="boxes"></div>

    <div class="hustle">
      <span>Beigušās monētas un nav ko pārdot?</span>
      <button id="hustle" type="button">Pastrādāt +5 🪙</button>
    </div>
  </section>

  <section aria-labelledby="inv-title">
    <div class="inv-head">
      <h2 id="inv-title">Mans krājums</h2>
      <button class="sell-all" id="sellAll" type="button">Pārdot visu</button>
    </div>
    <div class="inventory" id="inventory"></div>
    <div class="stats" id="stats"></div>
    <button class="reset" id="reset" type="button">Sākt spēli no jauna</button>
  </section>
</main>

<div class="overlay" id="overlay" role="dialog" aria-modal="true" aria-label="Kastes atvēršana">
  <div class="stage" id="stage"></div>
</div>
<div class="toast" id="toast" role="status"></div>

<script>
/* =========================================================
   IESTATĪJUMI - šeit vari mainīt cenas, mēmus un varbūtības
   ========================================================= */

const START_COINS = 200;

const RARITIES = {
  common:    { name: "Parasts",     tint: "var(--c-common)" },
  rare:      { name: "Rets",        tint: "var(--c-rare)" },
  epic:      { name: "Episks",      tint: "var(--c-epic)" },
  legendary: { name: "Leģendārs",   tint: "var(--c-legendary)" },
  mythic:    { name: "Mītisks",     tint: "var(--c-mythic)" },
  divine:    { name: "Dievišķs",    tint: "var(--c-divine)" }
};

// value = par cik monētām mēmu var pārdot
const MEMES = [
  { id: "kakis",    emoji: "🐱", name: "Nožēlojošais kaķis", rarity: "common",    value: 30 },
  { id: "varde",    emoji: "🐸", name: "Skumjā varde",       rarity: "common",    value: 40 },
  { id: "maize",    emoji: "🍞", name: "Maizes mēms",        rarity: "common",    value: 25 },
  { id: "moai",     emoji: "🗿", name: "Moai skatiens",      rarity: "common",    value: 50 },
  { id: "pica",     emoji: "🍕", name: "Picas mēms",         rarity: "common",    value: 35 },
  { id: "kartupelis", emoji: "🥔", name: "Kartupeļa mēms",   rarity: "common",    value: 20 },

  { id: "doge",     emoji: "🐕", name: "Doge",               rarity: "rare",      value: 150 },
  { id: "domatajs", emoji: "🤔", name: "Domātājs",           rarity: "rare",      value: 120 },
  { id: "uguns",    emoji: "🔥", name: "Šis ir labi",        rarity: "rare",      value: 250 },
  { id: "smadzenes",emoji: "🧠", name: "Galaxy brain",       rarity: "rare",      value: 300 },
  { id: "robots",   emoji: "🤖", name: "Robota mēms",        rarity: "rare",      value: 200 },

  { id: "pile",     emoji: "🦆", name: "Pīle ar cepuri",     rarity: "epic",      value: 700 },
  { id: "raketa",   emoji: "🚀", name: "Uz mēnesi!",         rarity: "epic",      value: 1000 },
  { id: "karalis",  emoji: "👑", name: "Mēmu karalis",       rarity: "epic",      value: 1500 },
  { id: "pingvins", emoji: "🐧", name: "Elegantais pingvīns",rarity: "epic",      value: 900 },

  { id: "nyan",     emoji: "🌈", name: "Varavīksnes kaķis",  rarity: "legendary", value: 5000 },
  { id: "dimants",  emoji: "💎", name: "Dimanta mēms",       rarity: "legendary", value: 12000 },
  { id: "pukis",    emoji: "🐲", name: "Pūķa mēms",          rarity: "legendary", value: 7000 },

  { id: "kosmoss",  emoji: "🌌", name: "Kosmiskais mēms",    rarity: "mythic",    value: 60000 },
  { id: "kauss",    emoji: "🏆", name: "Visu laiku mēms",    rarity: "mythic",    value: 150000 },

  { id: "multiverss", emoji: "🌀", name: "Multiversa mēms",  rarity: "divine",    value: 300000 },
  { id: "vienradzis", emoji: "🦄", name: "Vienradža mēms",   rarity: "divine",    value: 1000000 }
];

// odds = svars katrai retumam (nav jābūt 100 summai)
// free: true = bezmaksas kaste; cooldown = gaidīšanas laiks sekundēs
const BOXES = [
  { id: "free",     emoji: "🎈", name: "Bezmaksas kaste",   price: 0,      tint: "#c9fbe9",
    free: true, cooldown: 60,
    odds: { common: 85, rare: 15 } },
  { id: "koka",     emoji: "📦", name: "Koka kaste",        price: 100,    tint: "#f1e2c6",
    odds: { common: 70, rare: 26, epic: 4 } },
  { id: "bronza",   emoji: "🥉", name: "Bronzas kaste",     price: 250,    tint: "#f0d2b0",
    odds: { common: 35, rare: 50, epic: 15 } },
  { id: "sudraba",  emoji: "🧰", name: "Sudraba kaste",     price: 500,    tint: "#dfe3ee",
    odds: { common: 30, rare: 45, epic: 22, legendary: 3 } },
  { id: "zelta",    emoji: "🎁", name: "Zelta kaste",       price: 2500,   tint: "#ffeea0",
    odds: { rare: 30, epic: 50, legendary: 19, mythic: 1 } },
  { id: "rubina",   emoji: "♦️", name: "Rubīna kaste",      price: 6000,   tint: "#ffc4cf",
    odds: { epic: 65, legendary: 32, mythic: 3 } },
  { id: "dimanta",  emoji: "💠", name: "Dimanta kaste",     price: 12000,  tint: "#b9ecff",
    odds: { epic: 30, legendary: 60, mythic: 10 } },
  { id: "kosmiska", emoji: "🛸", name: "Kosmiskā kaste",    price: 60000,  tint: "#d9c6ff",
    odds: { legendary: 30, mythic: 70 } },
  { id: "caurums",  emoji: "🕳️", name: "Melnā cauruma kaste", price: 250000, tint: "#c7b8f5",
    odds: { mythic: 70, divine: 30 } }
];

/* =========================================================
   SPĒLES LOĢIKA
   ========================================================= */

const SAVE_KEY = "memu-kastes-v1";
let state = loadState();
let busy = false;

const $ = (id) => document.getElementById(id);
const fmt = (n) => n.toLocaleString("lv-LV");
const memeById = (id) => MEMES.find((m) => m.id === id);

function freshState() {
  return { coins: START_COINS, inv: {}, opened: 0, earned: 0, freeAt: 0 };
}

function loadState() {
  try {
    const raw = localStorage.getItem(SAVE_KEY);
    if (raw) return Object.assign(freshState(), JSON.parse(raw));
  } catch (e) { /* ja nav pieejams, spēle darbosies bez saglabāšanas */ }
  return freshState();
}

function saveState() {
  try { localStorage.setItem(SAVE_KEY, JSON.stringify(state)); } catch (e) {}
}

function toast(text) {
  const t = $("toast");
  t.textContent = text;
  t.classList.add("show");
  clearTimeout(toast.timer);
  toast.timer = setTimeout(() => t.classList.remove("show"), 2200);
}

function pickMeme(box) {
  const entries = Object.entries(box.odds);
  const total = entries.reduce((s, [, w]) => s + w, 0);
  let roll = Math.random() * total;
  let rarity = entries[entries.length - 1][0];
  for (const [r, w] of entries) {
    if (roll < w) { rarity = r; break; }
    roll -= w;
  }
  const pool = MEMES.filter((m) => m.rarity === rarity);
  return pool[Math.floor(Math.random() * pool.length)];
}

function addCoins(n) {
  state.coins += n;
  const w = $("wallet");
  w.classList.remove("bump");
  void w.offsetWidth;
  w.classList.add("bump");
}

function openBox(boxId) {
  if (busy) return;
  const box = BOXES.find((b) => b.id === boxId);
  if (box.free) {
    if (freeLeft(box) > 0) { toast("Bezmaksas kaste vēl nav gatava."); return; }
    state.freeAt = Date.now();
  } else if (state.coins < box.price) {
    toast("Nepietiek monētu šai kastei.");
    return;
  }

  busy = true;
  state.coins -= box.price;
  state.opened += 1;
  const meme = pickMeme(box);
  state.inv[meme.id] = (state.inv[meme.id] || 0) + 1;
  saveState();
  renderWallet();

  const overlay = $("overlay");
  const stage = $("stage");
  stage.innerHTML = `<div class="shaking" aria-hidden="true">${box.emoji}</div>`;
  overlay.classList.add("show");

  setTimeout(() => {
    const r = RARITIES[meme.rarity];
    stage.innerHTML = `
      <div class="reveal" style="--tint:${r.tint}">
        <div class="big" aria-hidden="true">${meme.emoji}</div>
        <h3>${meme.name}</h3>
        <p>${r.name} · vērtība ${fmt(meme.value)} 🪙</p>
        <div class="row">
          <button type="button" id="sellNow">Pārdot par ${fmt(meme.value)}</button>
          <button type="button" class="primary" id="keep">Paturēt</button>
        </div>
      </div>`;
    $("keep").focus();
    $("keep").onclick = closeOverlay;
    $("sellNow").onclick = () => { sellOne(meme.id, true); closeOverlay(); };
    render();
  }, 950);
}

function closeOverlay() {
  $("overlay").classList.remove("show");
  busy = false;
  render();
}

function sellOne(id, silent) {
  if (!state.inv[id]) return;
  const meme = memeById(id);
  state.inv[id] -= 1;
  if (state.inv[id] <= 0) delete state.inv[id];
  state.earned += meme.value;
  addCoins(meme.value);
  saveState();
  render();
  if (!silent) toast(`Pārdots: ${meme.name} (+${fmt(meme.value)} 🪙)`);
}

function sellStack(id) {
  const count = state.inv[id] || 0;
  if (!count) return;
  const meme = memeById(id);
  const gain = count * meme.value;
  delete state.inv[id];
  state.earned += gain;
  addCoins(gain);
  saveState();
  render();
  toast(`Pārdoti ${count}× ${meme.name} (+${fmt(gain)} 🪙)`);
}

function sellEverything() {
  let gain = 0, n = 0;
  for (const [id, count] of Object.entries(state.inv)) {
    gain += memeById(id).value * count;
    n += count;
  }
  if (!n) return;
  state.inv = {};
  state.earned += gain;
  addCoins(gain);
  saveState();
  render();
  toast(`Pārdoti ${n} mēmi (+${fmt(gain)} 🪙)`);
}

/* =========================================================
   ATTĒLOŠANA
   ========================================================= */

function renderWallet() {
  $("coins").textContent = fmt(state.coins);
}

function freeLeft(box) {
  return Math.max(0, Math.ceil((state.freeAt + box.cooldown * 1000 - Date.now()) / 1000));
}

function freeLabel(box) {
  const left = freeLeft(box);
  if (left === 0) return "Atvērt bezmaksas";
  const m = Math.floor(left / 60), sec = String(left % 60).padStart(2, "0");
  return `Nākamā pēc ${m}:${sec}`;
}

function renderBoxes() {
  $("boxes").innerHTML = BOXES.map((b) => {
    const total = Object.values(b.odds).reduce((s, w) => s + w, 0);
    const chips = Object.entries(b.odds).map(([r, w]) => {
      const pct = Math.round((w / total) * 1000) / 10;
      return `<li style="--chip:${RARITIES[r].tint}">${RARITIES[r].name} ${pct}%</li>`;
    }).join("");
    const can = b.free ? freeLeft(b) === 0 : state.coins >= b.price;
    const label = b.free ? freeLabel(b) : `Atvērt · ${fmt(b.price)} 🪙`;
    return `
      <article class="box${b.free ? " free-box" : ""}">
        <div class="art" style="--tint:${b.tint}" aria-hidden="true">${b.emoji}</div>
        <h3>${b.name}</h3>
        <ul class="odds">${chips}</ul>
        <button class="buy${b.free ? " free" : ""}" type="button" data-box="${b.id}" ${can && !busy ? "" : "disabled"}>${label}</button>
      </article>`;
  }).join("");
}

function renderInventory() {
  const ids = Object.keys(state.inv);
  const order = { common: 0, rare: 1, epic: 2, legendary: 3, mythic: 4, divine: 5 };
  ids.sort((a, b) => order[memeById(b).rarity] - order[memeById(a).rarity] || memeById(b).value - memeById(a).value);

  if (!ids.length) {
    $("inventory").innerHTML = `<div class="empty">Krājums ir tukšs.<br>Atver savu pirmo kasti veikalā.</div>`;
  } else {
    $("inventory").innerHTML = ids.map((id) => {
      const m = memeById(id), n = state.inv[id], r = RARITIES[m.rarity];
      return `
        <div class="meme" style="--tint:${r.tint}">
          <div class="emoji" aria-hidden="true">${m.emoji}</div>
          <div>
            <b>${m.name} <span class="count">×${n}</span></b>
            <small>${r.name} · ${fmt(m.value)} 🪙 gabalā</small>
          </div>
          <div class="actions">
            <button type="button" data-sell="${id}">Pārdot 1</button>
            ${n > 1 ? `<button type="button" data-sellstack="${id}">Pārdot visus</button>` : ""}
          </div>
        </div>`;
    }).join("");
  }

  const totalValue = ids.reduce((s, id) => s + memeById(id).value * state.inv[id], 0);
  $("sellAll").disabled = !ids.length;
  $("sellAll").textContent = ids.length ? `Pārdot visu (+${fmt(totalValue)})` : "Pārdot visu";
}

function renderStats() {
  $("stats").innerHTML = `
    <span>Atvērtas kastes: ${fmt(state.opened)}</span>
    <span>Nopelnīts pārdodot: ${fmt(state.earned)} 🪙</span>`;
}

function render() {
  renderWallet();
  renderBoxes();
  renderInventory();
  renderStats();
}

/* =========================================================
   NOTIKUMI
   ========================================================= */

$("boxes").addEventListener("click", (e) => {
  const btn = e.target.closest("[data-box]");
  if (btn) openBox(btn.dataset.box);
});

$("inventory").addEventListener("click", (e) => {
  const one = e.target.closest("[data-sell]");
  const stack = e.target.closest("[data-sellstack]");
  if (one) sellOne(one.dataset.sell);
  if (stack) sellStack(stack.dataset.sellstack);
});

$("sellAll").addEventListener("click", sellEverything);

$("hustle").addEventListener("click", () => {
  addCoins(5);
  saveState();
  render();
});

$("reset").addEventListener("click", () => {
  if (confirm("Vai tiešām sākt no jauna? Visi mēmi un monētas tiks dzēsti.")) {
    state = freshState();
    saveState();
    render();
  }
});

document.addEventListener("keydown", (e) => {
  if (e.key === "Escape" && $("overlay").classList.contains("show") && $("keep")) closeOverlay();
});

render();

// bezmaksas kastes atpakaļskaitīšana (atjauno tikai pogu, nevis visu lapu)
setInterval(() => {
  const b = BOXES.find((x) => x.free);
  if (!b) return;
  const btn = document.querySelector(`[data-box="${b.id}"]`);
  if (!btn) return;
  btn.textContent = freeLabel(b);
  btn.disabled = busy || freeLeft(b) > 0;
}, 1000);
</script>
</body>
</html>
