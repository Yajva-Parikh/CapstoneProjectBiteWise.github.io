# CapstoneProjectBiteWise.github.io
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="color-scheme" content="light dark">
<title>BiteWise - Smarter food swaps for Indian diets</title>
<meta name="description" content="BiteWise compares what you eat with what your body needs and suggests affordable Indian and Western swaps.">
<script>
/* Set the theme before the page paints so there is no flash. */
(function () {
  var t = null;
  try { t = localStorage.getItem('bitewise.theme'); } catch (e) {}
  if (t !== 'light' && t !== 'dark') {
    t = (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) ? 'dark' : 'light';
  }
  document.documentElement.setAttribute('data-theme', t);
})();
</script>
<style>
:root {
  --bg: #F8FBF5; --card: #FFFFFF; --primary: #2E7D32; --on-primary: #FFFFFF;
  --accent: #F59E0B; --text: #1B2A1F; --muted: #5B6B60; --border: #DCE6D4;
  --bad: #D94F3D; --tile: #EEF5E9; color-scheme: light;
}
[data-theme="dark"] {
  --bg: #0F1A14; --card: #17261D; --primary: #4CAF6A; --on-primary: #0F1A14;
  --accent: #FFB547; --text: #E8F0EA; --muted: #9FB3A6; --border: #25382C;
  --bad: #F07A6B; --tile: #1F3226; color-scheme: dark;
}
* { box-sizing: border-box; }
html { scroll-behavior: smooth; }
body {
  margin: 0; background: var(--bg); color: var(--text);
  font: 16px/1.55 system-ui, -apple-system, "Segoe UI", Roboto, "Noto Sans", sans-serif;
}
.wrap { max-width: 960px; margin: 0 auto; padding: 0 16px 40px; }
h1, h2, h3 { line-height: 1.25; margin: 0 0 8px; }
h1 { font-size: clamp(1.6rem, 4vw, 2.2rem); }
h2 { font-size: 1.25rem; }
h3 { font-size: 1rem; }
p { margin: 0 0 10px; }
.muted { color: var(--muted); }
.sr { position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0,0,0,0); white-space: nowrap; }
.skip { position: absolute; left: -999px; top: 8px; background: var(--primary); color: var(--on-primary); padding: 8px 12px; border-radius: 8px; z-index: 50; }
.skip:focus { left: 8px; }
:focus-visible { outline: 3px solid var(--primary); outline-offset: 2px; }

header.top { display: flex; align-items: center; justify-content: space-between; padding: 14px 0; gap: 12px; }
.logo { display: flex; align-items: center; gap: 8px; font-weight: 700; font-size: 1.4rem; color: var(--primary); }
.hero { padding: 8px 0 18px; }
.hero p { max-width: 62ch; color: var(--muted); }

.card { background: var(--card); border: 1px solid var(--border); border-radius: 14px; padding: 20px; margin-bottom: 16px; }

.btn {
  font: inherit; font-weight: 600; border-radius: 10px; padding: 9px 14px; cursor: pointer;
  border: 1px solid var(--border); background: var(--card); color: var(--text);
  display: inline-flex; align-items: center; gap: 6px; line-height: 1.2;
}
.btn:hover { border-color: var(--primary); }
.btn.primary { background: var(--primary); color: var(--on-primary); border-color: var(--primary); }
.btn.ghost { background: transparent; }
.btn.sm { padding: 6px 10px; font-size: .85rem; }
.btn[hidden] { display: none; }

#themebtn .ic-sun { display: none; }
[data-theme="dark"] #themebtn .ic-sun { display: inline; }
[data-theme="dark"] #themebtn .ic-moon { display: none; }

input, select {
  font: inherit; color: var(--text); background: var(--card); border: 1px solid var(--border);
  border-radius: 10px; padding: 10px 12px; width: 100%;
}
::placeholder { color: var(--muted); opacity: .85; }
label, legend { font-weight: 600; font-size: .92rem; }
.opt { font-weight: 400; color: var(--muted); }
.field { display: flex; flex-direction: column; gap: 6px; }
.grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 14px; margin-bottom: 16px; }
fieldset { border: 0; padding: 0; margin: 0 0 16px; }
legend { padding: 0; margin-bottom: 8px; }
.err { color: var(--bad); min-height: 1.4em; font-weight: 600; margin-bottom: 8px; }
.actions { display: flex; gap: 10px; flex-wrap: wrap; }

.chips { display: flex; flex-wrap: wrap; gap: 8px; position: relative; }
.chips input { position: absolute; opacity: 0; width: 1px; height: 1px; pointer-events: none; }
.chip {
  display: inline-flex; align-items: center; gap: 8px; padding: 9px 14px; font-weight: 500;
  border: 1px solid var(--border); border-radius: 999px; background: var(--card); cursor: pointer;
}
.chips input:checked + .chip {
  border-color: var(--primary); font-weight: 700;
  background: color-mix(in srgb, var(--primary) 16%, transparent);
}
.chips input:focus-visible + .chip { outline: 3px solid var(--primary); outline-offset: 2px; }

.dot {
  width: 14px; height: 14px; border: 2px solid var(--dc); border-radius: 3px;
  display: inline-grid; place-items: center; flex: none; vertical-align: -2px; margin-right: 6px;
}
.dot::after { content: ""; width: 6px; height: 6px; border-radius: 50%; background: var(--dc); }
.dot-v { --dc: #2A9D3F; } .dot-e { --dc: #F59E0B; } .dot-n { --dc: #D94F3D; }
.chip .dot { margin-right: 0; }

.thumb {
  width: 40px; height: 40px; border-radius: 10px; background: var(--tile); flex: none;
  display: grid; place-items: center; font-size: 22px; overflow: hidden;
}
.thumb img { width: 100%; height: 100%; object-fit: cover; display: block; }
.pill { font-size: .72rem; padding: 2px 8px; border-radius: 999px; font-weight: 600; white-space: nowrap; }
.pill-i { background: color-mix(in srgb, var(--primary) 18%, transparent); color: var(--text); }
.pill-w { background: color-mix(in srgb, var(--accent) 28%, transparent); color: var(--text); }
.pill-p { border: 1px solid var(--border); color: var(--muted); }
.pills { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 4px; }
.grow { flex: 1; min-width: 0; }
.nm { font-weight: 600; }
.sub { font-size: .82rem; color: var(--muted); }

.profilebar { display: flex; align-items: center; justify-content: space-between; gap: 12px; flex-wrap: wrap; padding: 14px 20px; }

.searchrow { display: flex; gap: 10px; align-items: flex-start; flex-wrap: wrap; }
.combo { position: relative; flex: 1 1 300px; }
.mealsel { flex: 0 0 150px; }
#sug {
  position: absolute; left: 0; right: 0; top: calc(100% + 6px); z-index: 20; margin: 0; padding: 6px;
  list-style: none; background: var(--card); border: 1px solid var(--border); border-radius: 12px;
  max-height: 380px; overflow: auto; box-shadow: 0 8px 24px rgba(0,0,0,.18);
}
#sug[hidden] { display: none; }
#sug li[role="option"] { display: flex; align-items: center; gap: 10px; padding: 8px 10px; border-radius: 10px; cursor: pointer; }
#sug li.active { background: var(--tile); }
#sug .sughead, #sug .nores { padding: 6px 10px; font-size: .82rem; color: var(--muted); }
#sug strong { color: var(--primary); }
.quick { display: flex; flex-wrap: wrap; gap: 8px; margin: 12px 0 4px; align-items: center; }
.quick .chip { padding: 5px 12px 5px 6px; font-size: .88rem; }
.quick .thumb { width: 28px; height: 28px; font-size: 16px; border-radius: 8px; }

.loghead { display: flex; align-items: center; justify-content: space-between; margin-top: 16px; }
.mealgroup { margin-top: 12px; }
.mealgroup h3 { color: var(--muted); font-size: .85rem; text-transform: uppercase; letter-spacing: .05em; }
.items { list-style: none; margin: 0; padding: 0; display: grid; gap: 10px; }
.item { border: 1px solid var(--border); border-radius: 12px; padding: 10px; }
.row { display: flex; align-items: center; gap: 12px; flex-wrap: wrap; }
.row:focus { outline: none; }
.qty { display: flex; align-items: center; gap: 6px; }
.qv { min-width: 84px; text-align: center; font-size: .88rem; }
.acts { display: flex; gap: 6px; flex-wrap: wrap; }

.panel { margin-top: 12px; padding-top: 12px; border-top: 1px dashed var(--border); }
.planq { padding: 4px 0 2px; }
.planrow { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 10px; }
.planrow .chip { padding: 12px 20px; font-size: 1rem; font-weight: 600; }
.planrow .chip:hover { border-color: var(--primary); }
.planbar { display: flex; align-items: center; gap: 8px; flex-wrap: wrap; }
.swaps { display: grid; grid-template-columns: repeat(auto-fit, minmax(210px, 1fr)); gap: 12px; margin: 10px 0; }
.swapcard { border: 1px solid var(--border); border-radius: 12px; padding: 12px; display: flex; flex-direction: column; gap: 10px; background: var(--bg); }
.sc-top { display: flex; gap: 10px; align-items: flex-start; }
.why { list-style: none; margin: 0; padding: 0; font-size: .86rem; display: grid; gap: 3px; }
.why .good { color: var(--primary); font-weight: 600; }
.why .bad { color: var(--bad); font-weight: 600; }
.swapcard .btn { margin-top: auto; justify-content: center; }
.tablewrap { overflow-x: auto; margin-top: 12px; border: 1px solid var(--border); border-radius: 12px; }
.cmp { width: 100%; border-collapse: collapse; font-size: .85rem; min-width: 520px; }
.cmp caption { text-align: left; padding: 10px 10px 4px; font-weight: 600; }
.cmp th, .cmp td { padding: 7px 10px; text-align: left; border-top: 1px solid var(--border); }
.cmp thead th { color: var(--muted); font-weight: 600; }
.cmp tbody th { font-weight: 500; }
.better { color: var(--primary); font-weight: 700; }

.bar-row { margin-bottom: 12px; }
.bar-top { display: flex; justify-content: space-between; gap: 10px; flex-wrap: wrap; font-size: .9rem; margin-bottom: 4px; }
.bar { height: 9px; border-radius: 5px; background: var(--border); overflow: hidden; }
.bar i { display: block; height: 100%; border-radius: 5px; }
.s-ok { background: var(--primary); } .s-warn { background: var(--accent); } .s-bad { background: var(--bad); }
.note { font-size: .82rem; color: var(--muted); }

.two { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 16px; }
.two .card { margin: 0; }
.two ul { margin: 8px 0 0; padding-left: 18px; display: grid; gap: 6px; }
.stats { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px, 1fr)); gap: 12px; margin-top: 14px; }
.stat { background: var(--tile); border-radius: 12px; padding: 12px; }
.stat b { display: block; font-size: 1.5rem; color: var(--primary); }
.sdgtag { display: inline-block; font-size: .75rem; font-weight: 700; padding: 2px 10px; border-radius: 999px; background: var(--primary); color: var(--on-primary); margin-bottom: 8px; }
footer { color: var(--muted); font-size: .85rem; padding-top: 8px; }
[hidden] { display: none !important; }
@media (prefers-reduced-motion: reduce) { html { scroll-behavior: auto; } }
@media (max-width: 520px) { .mealsel { flex: 1 1 100%; } .card { padding: 16px; } }
</style>
</head>
<body>
<a class="skip" href="#main">Skip to content</a>
<div class="wrap">
  <header class="top">
    <div class="logo">
      <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M11 20A7 7 0 0 1 9.8 6.1C15.5 5 17 4.5 19 2c1 2 2 4.2 2 8 0 5.5-4.8 10-10 10z"/><path d="M2 21c0-3 1.9-5.4 5.1-6.3C9.5 14 12 13 14 11"/></svg>
      BiteWise
    </div>
    <div class="actions">
      <button class="btn" id="themebtn" type="button" aria-label="Switch theme">
        <svg class="ic-moon" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M21 12.8A9 9 0 1 1 11.2 3a7 7 0 0 0 9.8 9.8z"/></svg>
        <svg class="ic-sun" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2M4.9 4.9l1.4 1.4M17.7 17.7l1.4 1.4M2 12h2M20 12h2M4.9 19.1l1.4-1.4M17.7 6.3l1.4-1.4"/></svg>
        <span id="themelabel">Dark mode</span>
      </button>
    </div>
  </header>

  <main id="main">
    <section class="hero">
      <h1>Eat smarter, with swaps from Indian and Western food</h1>
      <p>Tell BiteWise what you ate. It compares your meals with what your body needs and suggests affordable alternatives, so you can pick the change that suits you.</p>
    </section>

    <noscript><div class="card">BiteWise needs JavaScript to run. Please turn it on and reload the page.</div></noscript>

    <section id="onboarding" class="card" aria-labelledby="ob-h">
      <h2 id="ob-h">Tell us a little about you</h2>
      <p class="muted">We use this to compare your food with the amounts recommended for your age, gender and weight. Everything stays on your device.</p>
      <form id="pform" novalidate>
        <div class="grid">
          <div class="field"><label for="age">Age (years)</label><input id="age" name="age" type="number" inputmode="numeric" min="10" max="80" required></div>
          <div class="field"><label for="weight">Weight (kg)</label><input id="weight" name="weight" type="number" inputmode="decimal" min="25" max="200" step="0.1" required></div>
          <div class="field"><label for="height">Height (cm) <span class="opt">optional</span></label><input id="height" name="height" type="number" inputmode="numeric" min="100" max="220"></div>
          <div class="field"><label for="activity">Activity level <span class="opt">optional</span></label>
            <select id="activity" name="activity">
              <option value="">Choose one</option>
              <option value="sedentary">Mostly sitting</option>
              <option value="light">Lightly active</option>
              <option value="moderate">Moderately active</option>
              <option value="active">Very active</option>
            </select>
          </div>
        </div>
        <fieldset>
          <legend>Gender</legend>
          <div class="chips">
            <input type="radio" id="g-m" name="gender" value="male"><label class="chip" for="g-m">Male</label>
            <input type="radio" id="g-f" name="gender" value="female"><label class="chip" for="g-f">Female</label>
            <input type="radio" id="g-o" name="gender" value="other"><label class="chip" for="g-o">Prefer not to say</label>
          </div>
        </fieldset>
        <p id="formerr" class="err" role="alert"></p>
        <div class="actions">
          <button type="button" class="btn primary" id="psave">Save and continue</button>
          <button type="button" class="btn ghost" id="pcancel" hidden>Cancel</button>
        </div>
      </form>
    </section>

    <div id="app" hidden>
      <section class="card profilebar" id="pbar" aria-label="Your details"></section>

      <section class="card" id="logger" aria-labelledby="lg-h">
        <h2 id="lg-h">What did you eat?</h2>
        <p class="muted">Start typing a food and pick it from the suggestions. No need to type the whole name.</p>
        <div class="searchrow">
          <div class="combo">
            <label for="q" class="sr">Search for a food</label>
            <input id="q" type="text" role="combobox" aria-expanded="false" aria-controls="sug" aria-autocomplete="list" autocomplete="off" placeholder="Try: poha, roti, dal, samosa, chai">
            <ul id="sug" role="listbox" aria-label="Food suggestions" hidden></ul>
          </div>
          <div class="field mealsel">
            <label for="meal" class="sr">Meal</label>
            <select id="meal">
              <option>Breakfast</option><option>Lunch</option><option>Snack</option><option>Dinner</option>
            </select>
          </div>
        </div>
        <div class="quick" id="quick" aria-label="Quick add"></div>

        <div class="loghead">
          <h3>Your food today</h3>
          <button class="btn sm ghost" id="clearall" type="button" hidden>Clear all</button>
        </div>
        <div id="log"></div>
        <p id="emptylog" class="muted">Nothing added yet. Search above or tap a quick-add food.</p>
      </section>

      <section class="card" id="today" aria-labelledby="td-h">
        <h2 id="td-h">Today vs your daily target</h2>
        <p id="tgt" class="muted"></p>
        <div id="bars"></div>
        <p id="macros" class="note"></p>
        <p class="note">Log all your meals for the day to get an accurate picture. Targets are approximate, based on general ICMR-NIN style guidance, and are not medical advice. Teens and anyone with a health condition should check with a doctor or dietitian.</p>
      </section>
    </div>

    <section id="sdg" aria-labelledby="sdg-h">
      <h2 id="sdg-h" style="margin-top:8px">How BiteWise supports the SDGs</h2>
      <div class="two">
        <div class="card">
          <span class="sdgtag">SDG 3</span>
          <h3>Good Health and Well-being</h3>
          <ul>
            <li>Daily targets match your age, gender and weight, so advice is personal and not generic.</li>
            <li>Gaps in protein, fiber, iron, calcium and vitamin B12 are shown clearly.</li>
            <li>Swaps move you from refined and fried foods toward whole, nutrient-rich ones, which supports the prevention side of target 3.4 (diet-related non-communicable diseases).</li>
          </ul>
        </div>
        <div class="card">
          <span class="sdgtag">SDG 12</span>
          <h3>Responsible Consumption and Production</h3>
          <ul>
            <li>Every swap shows its approximate cost and favours affordable local staples like dal, millets and chana.</li>
            <li>Plant-based tags help you spot choices that are usually lighter on the planet.</li>
            <li>Clear nutrition information supports informed, sustainable choices (target 12.8).</li>
            <li>Coming next: a use-what-you-have mode to cut food waste (target 12.3).</li>
          </ul>
        </div>
      </div>
      <div class="card" style="margin-top:16px">
        <h3>Your impact today</h3>
        <div class="stats" id="impact" aria-live="polite"></div>
      </div>
    </section>
  </main>

  <footer>
    <p>BiteWise is a student project. Nutrition values come from a small sample dataset and are approximate (per serving). For a real product, replace them with data from the Indian Food Composition Tables (IFCT). This is general guidance, not medical advice.</p>
  </footer>
</div>
<div id="live" class="sr" aria-live="polite" role="status"></div>

<script>
(function () {
'use strict';

/* ---------- helpers ---------- */
function $(s, r) { return (r || document).querySelector(s); }
function h(tag, props, kids) {
  var e = document.createElement(tag);
  if (props) {
    for (var k in props) {
      var v = props[k];
      if (v == null || v === false) continue;
      if (k === 'class') e.className = v;
      else if (k === 'text') e.textContent = v;
      else if (k.slice(0, 2) === 'on') e.addEventListener(k.slice(2), v);
      else e.setAttribute(k, v === true ? '' : v);
    }
  }
  (kids || []).forEach(function (c) {
    if (c == null || c === false) return;
    e.appendChild(typeof c === 'string' ? document.createTextNode(c) : c);
  });
  return e;
}
function fmt(n) { return String(Math.round(n * 10) / 10); }
function announce(msg) { $('#live').textContent = msg; }

/* ---------- food data ----------
   Approximate values PER SERVING (a sample dataset, not official figures).
   Order: id, name, emoji, cuisine (I=Indian, W=Western), diet (v=veg, e=egg, n=non-veg),
          kcal, protein g, carbs g, fat g, fiber g, iron mg, calcium mg, B12 ug,
          cost in rupees, groups (swap families), plant-based (1/0), search keywords.
   Groups: brk=breakfast, drk=drinks, snk=snacks, stp=breads, rce=rice and grains, mel=meals. */
var RAW = [
  ['poha','Poha (1 plate)','🥣','I','v',250,5,45,6,2.5,3.0,20,0,25,'brk',1,'flattened rice kanda poha'],
  ['upma','Upma (1 plate)','🥣','I','v',230,5,36,8,2.5,1.5,25,0,25,'brk',1,'rava suji semolina'],
  ['idli','Idli with sambar (3 pieces)','🍘','I','v',200,7,38,1.5,3,1.6,40,0,35,'brk',1,'idly south indian'],
  ['dosa','Masala dosa (1)','🥞','I','v',330,7,50,11,3,1.8,30,0,60,'brk',1,'dosai south indian'],
  ['aloopar','Aloo paratha, maida (1)','🫓','I','v',300,6,40,13,2,1.5,30,0,25,'brk',0,'parantha potato paratha'],
  ['aloopar-w','Aloo paratha, whole wheat (1)','🫓','I','v',290,7,40,12,5,2.2,35,0,25,'brk',0,'parantha atta potato paratha'],
  ['chilla','Moong dal chilla (2) with chutney','🥞','I','v',230,14,28,6,5,2.8,55,0,22,'brk',1,'cheela pesarattu'],
  ['oats','Oats with banana and peanuts (1 bowl)','🥣','W','v',340,12,52,10,7,2.8,60,0,40,'brk',1,'oatmeal porridge'],
  ['cornflakes','Cornflakes with milk (1 bowl)','🥣','W','v',220,7,40,3.5,1.2,3.0,150,0.9,35,'brk',0,'cereal'],
  ['breadjam','Bread, butter and jam (2 slices)','🍞','W','v',260,5,36,11,1.5,1.3,60,0,15,'brk',0,'toast'],
  ['eggtoast','Boiled eggs (2) with whole wheat toast','🍳','W','e',330,19,22,17,3.5,2.8,90,1.2,28,'brk',0,'egg anda'],
  ['omelette','Masala omelette (2 eggs) with roti','🍳','I','e',340,18,20,20,3,2.9,80,1.1,30,'brk',0,'egg anda'],
  ['gyogurt','Greek yogurt with fruit and seeds (1 bowl)','🥛','W','v',220,15,22,8,3,1.0,180,0.8,70,'brk,snk',0,'yoghurt curd dahi'],
  ['paneersand','Paneer sandwich, whole wheat (1)','🥪','W','v',320,16,33,14,5,2,220,0.6,45,'brk,snk',0,'sandwich'],

  ['chai','Sweet masala chai (1 cup)','☕','I','v',90,2.5,14,3,0,0.1,90,0.3,10,'drk',0,'tea'],
  ['chai-ls','Chai with less sugar (1 cup)','☕','I','v',55,2.5,7,3,0,0.1,90,0.3,10,'drk',0,'tea'],
  ['colddrink','Cold drink (330 ml)','🥤','W','v',140,0,35,0,0,0,5,0,25,'drk',1,'cola coke soda pepsi soft drink'],
  ['juice','Packaged fruit juice (200 ml)','🧃','W','v',100,0.5,24,0,0.2,0.2,10,0,20,'drk',1,'tetra pack'],
  ['chaas','Buttermilk, chaas (1 glass)','🥛','I','v',40,2,4,1.5,0,0.1,100,0.4,10,'drk',0,'chaach mattha'],
  ['coconutw','Coconut water (1 glass)','🥥','I','v',50,1,11,0.5,1,0.3,60,0,40,'drk',1,'nariyal pani'],
  ['milk','Milk, toned (1 glass)','🥛','I','v',120,6.5,9.5,6,0,0.1,240,0.9,14,'drk',0,'doodh'],
  ['nimbu','Nimbu pani (1 glass)','🍋','I','v',50,0.2,12,0,0.2,0.2,8,0,8,'drk',1,'lemon water shikanji'],
  ['blackcoffee','Black coffee (1 cup)','☕','W','v',5,0.3,0,0,0,0.1,5,0,20,'drk',1,'coffee'],

  ['samosa','Samosa (1, fried)','🥟','I','v',260,4,28,15,2,1.2,25,0,15,'snk',1,''],
  ['vadapav','Vada pav (1)','🍔','I','v',300,7,42,11,3,1.8,40,0,20,'snk',1,'vada pao'],
  ['chips','Potato chips (small pack)','🍟','W','v',160,2,15,10,1,0.3,8,0,20,'snk',1,'wafers crisps'],
  ['biscuits','Cream biscuits (4)','🍪','W','v',200,2.5,30,8,0.5,0.8,30,0.1,10,'snk',0,'cookies'],
  ['pakora','Pakora (5 to 6 pieces)','🧆','I','v',250,5,22,16,3,1.5,30,0,20,'snk',1,'pakoda bhajiya bhajji'],
  ['chana','Roasted chana (1 handful)','🌰','I','v',150,8,24,2.5,6,2.4,60,0,8,'snk',1,'chickpea'],
  ['sprouts','Sprouts chaat (1 bowl)','🥗','I','v',160,9,25,2,6,2.5,50,0,20,'snk,brk',1,'moong sprout salad'],
  ['banana','Banana (1)','🍌','I','v',105,1.3,27,0.4,3,0.3,6,0,8,'snk',1,'kela fruit'],
  ['peanuts','Roasted peanuts (1 handful)','🥜','I','v',170,7.5,5,14,2.5,0.8,20,0,10,'snk',1,'mungfali groundnut'],
  ['boiledegg','Boiled eggs (2)','🥚','W','e',155,12.6,1.1,10.6,0,1.8,50,1.1,14,'snk',0,'anda'],
  ['apple','Apple (1 medium)','🍎','W','v',95,0.5,25,0.3,4.4,0.2,11,0,25,'snk',1,'fruit seb'],
  ['noodles','Instant noodles (1 pack)','🍜','W','v',350,7,52,13,2,2.5,35,0,15,'snk,mel',0,'maggi ramen'],

  ['roti','Whole wheat roti (2)','🫓','I','v',200,6,40,3,5,2,20,0,6,'stp',1,'chapati phulka'],
  ['naan','Naan (1)','🫓','I','v',260,8,45,5,2,1.9,60,0.1,40,'stp',0,'butter naan'],
  ['whitebread','White bread (2 slices)','🍞','W','v',150,5,28,2,1.5,1.4,70,0,8,'stp',1,'bread slice'],
  ['wwbread','Whole wheat bread (2 slices)','🍞','W','v',160,7,28,2.5,4,1.8,60,0,10,'stp',1,'brown bread atta'],
  ['jowar','Jowar roti (2)','🫓','I','v',190,6,40,1.5,5,2.8,15,0,10,'stp',1,'jowari sorghum bhakri'],
  ['bajra','Bajra roti (2)','🫓','I','v',230,7,40,5,6,4.5,30,0,10,'stp',1,'pearl millet bhakri'],
  ['maidapar','Plain paratha, maida (1)','🫓','I','v',250,5,35,11,1.5,1.2,20,0,12,'stp',0,'parantha'],

  ['rice','White rice (1 cup cooked)','🍚','I','v',200,4,44,0.4,0.6,0.5,10,0,10,'rce',1,'chawal steamed rice'],
  ['brownrice','Brown rice (1 cup cooked)','🍚','I','v',215,5,45,1.8,3.5,0.8,20,0,16,'rce',1,'chawal'],
  ['millet','Foxtail millet, cooked (1 cup)','🌾','I','v',175,6,33,2,4,2.5,20,0,18,'rce',1,'kangni korra'],
  ['quinoa','Quinoa, cooked (1 cup)','🌾','W','v',222,8,39,3.5,5,2.8,31,0,60,'rce',1,''],
  ['pasta','White pasta (1 cup cooked)','🍝','W','v',220,8,43,1.3,2.5,1.8,10,0,35,'rce',1,'macaroni spaghetti'],
  ['khichdi','Moong dal khichdi (1 bowl)','🍲','I','v',280,10,48,5,5,2.5,40,0,25,'rce,mel',0,'khichadi'],

  ['vegthali','Veg thali (2 roti, dal, sabzi, rice, curd)','🍛','I','v',650,20,100,18,12,6,250,0.6,90,'mel',0,'thali platter'],
  ['southmeal','South Indian meal (rice, sambar, poriyal, curd)','🍛','I','v',600,17,105,12,9,4.5,200,0.5,80,'mel',0,'thali meals'],
  ['dalrice','Dal rice (1 plate)','🍛','I','v',420,14,76,6,6,3.5,60,0,40,'mel',1,'dal chawal'],
  ['rajma','Rajma chawal (1 plate)','🍛','I','v',520,18,88,9,12,4.5,90,0,55,'mel',1,'rajma rice'],
  ['chole','Chole bhature (1 plate)','🍛','I','v',650,17,80,30,10,4.5,90,0,70,'mel',0,'chana bhatura'],
  ['paneerbm','Paneer butter masala with 2 roti','🍛','I','v',600,22,50,34,6,3,350,0.7,120,'mel',0,'paneer curry'],
  ['paneerbh','Paneer bhurji with 2 roti','🍛','I','v',480,22,42,24,6,3,330,0.7,70,'mel',0,'paneer'],
  ['soya','Soya chunk curry with 2 roti','🍛','I','v',400,28,45,10,9,5.5,200,0,45,'mel',1,'soyabean nutrela meal maker'],
  ['chickencurry','Chicken curry with 2 roti','🍗','I','n',480,33,40,18,5,3,60,0.7,120,'mel',0,'chicken'],
  ['eggcurry','Egg curry with 2 roti','🍛','I','e',470,22,42,22,5,3.5,100,1.1,70,'mel',0,'anda curry'],
  ['vegbiryani','Veg biryani (1 plate)','🍛','I','v',480,10,78,14,4,2,50,0,100,'mel',0,'pulao'],
  ['chickenbiryani','Chicken biryani (1 plate)','🍛','I','n',600,28,70,22,3,3,60,0.8,160,'mel',0,'biriyani'],
  ['pizza','Veg pizza (2 slices)','🍕','W','v',520,20,62,20,3,2.5,330,0.6,140,'mel',0,'cheese pizza'],
  ['burger','Veg burger (1)','🍔','W','v',450,12,54,21,4,2.5,120,0.1,90,'mel',0,'aloo tikki burger'],
  ['chickenburger','Chicken burger (1)','🍔','W','n',500,24,45,24,3,2.5,110,0.6,130,'mel',0,''],
  ['alfredo','Pasta alfredo (1 plate)','🍝','W','v',620,18,65,32,3,2,250,0.6,180,'mel',0,'white sauce pasta'],
  ['chickensalad','Grilled chicken salad (1 bowl)','🥗','W','n',320,32,14,14,5,2.5,80,0.4,150,'mel',0,''],
  ['chickpeabowl','Chickpea salad bowl (1)','🥗','W','v',350,15,48,11,12,4.5,90,0,70,'mel',1,'chana salad']
];

/* Optional real photos: add a path and it replaces the emoji, e.g. IMG.poha = 'images/poha.jpg' */
var IMG = {};

/* Refined, fried, sugary or ultra-processed foods: lighter swaps get a small bonus. */
var HEAVY = {};
('colddrink,juice,chips,biscuits,samosa,vadapav,pakora,maidapar,aloopar,whitebread,noodles,breadjam,' +
 'cornflakes,pizza,burger,chickenburger,alfredo,naan,chai,rice,pasta').split(',').forEach(function (i) { HEAVY[i] = 1; });

var FOODS = {}, LIST = [];
RAW.forEach(function (r) {
  var f = { id: r[0], name: r[1], emoji: r[2], cu: r[3], diet: r[4], kcal: r[5], p: r[6], c: r[7], f: r[8],
            fi: r[9], fe: r[10], ca: r[11], b12: r[12], cost: r[13], g: r[14].split(','), plant: !!r[15],
            alias: r[16] || '', img: IMG[r[0]] || '' };
  FOODS[f.id] = f; LIST.push(f);
});

var POPULAR = ['poha', 'idli', 'chai', 'roti', 'dalrice', 'vegthali', 'samosa', 'banana'];
var MEALS = ['Breakfast', 'Lunch', 'Snack', 'Dinner'];
var DIETNAME = { v: 'vegetarian', e: 'eggetarian', n: 'non-vegetarian' };
var DIETSHORT = { v: 'Veg', e: 'Eggetarian', n: 'Non-veg' };
var DIETLABEL = { v: 'Vegetarian', e: 'Contains egg', n: 'Non-vegetarian' };
var BARS = [['kcal', 'Calories', 'kcal'], ['p', 'Protein', 'g'], ['fi', 'Fiber', 'g'],
            ['fe', 'Iron', 'mg'], ['ca', 'Calcium', 'mg'], ['b12', 'Vitamin B12', 'µg']];

function shortName(f) { return f.name.replace(/\s*\(.*?\)\s*/g, ' ').replace(/\s+/g, ' ').trim(); }

/* ---------- state ---------- */
var S = { profile: null, plan: null, log: [], uid: 1, open: null, more: {}, refocus: null, day: new Date().toDateString() };
var KEY = 'bitewise.v1';
function save() {
  try { localStorage.setItem(KEY, JSON.stringify({ profile: S.profile, plan: S.plan, log: S.log, uid: S.uid, day: S.day })); } catch (e) {}
}
function load() {
  try {
    var raw = localStorage.getItem(KEY); if (!raw) return;
    var d = JSON.parse(raw); if (!d) return;
    var p = d.profile;
    if (p && p.age && p.weight && p.gender) S.profile = p;
    if (d.day === S.day && Array.isArray(d.log)) {
      if (DIETNAME[d.plan]) S.plan = d.plan;
      S.log = d.log.filter(function (i) { return i && FOODS[i.id] && i.qty > 0; });
      S.log.forEach(function (i) {
        if (i.from && !FOODS[i.from]) i.from = null;
        if (MEALS.indexOf(i.meal) < 0) i.meal = 'Snack';
      });
      var maxUid = S.log.reduce(function (m, i) { return Math.max(m, i.uid || 0); }, 0);
      S.uid = Math.max(d.uid || 1, maxUid + 1);
    }
  } catch (e) {}
}

/* ---------- nutrition maths ---------- */
function targets() {
  var p = S.profile, male = p.gender === 'male', fem = p.gender === 'female', teen = p.age < 18;
  var ht = p.height || (male ? 172 : (fem ? 159 : 165));
  var bmr = 10 * p.weight + 6.25 * ht - 5 * p.age + (male ? 5 : (fem ? -161 : -78));
  var mult = { sedentary: 1.2, light: 1.375, moderate: 1.55, active: 1.725 }[p.activity || 'light'] || 1.375;
  var kcal = Math.max(1500, Math.round(bmr * mult / 50) * 50);
  return {
    kcal: kcal,
    p: Math.max(35, Math.round(p.weight * (teen ? 0.95 : 0.8))),
    fi: Math.round(kcal / 1000 * 14),
    fe: male ? (teen ? 22 : 19) : (fem ? (teen ? 28 : 29) : (teen ? 25 : 24)),
    ca: 1000,
    b12: 2.2
  };
}
function totals() {
  var t = { kcal: 0, p: 0, c: 0, f: 0, fi: 0, fe: 0, ca: 0, b12: 0 };
  S.log.forEach(function (it) { var f = FOODS[it.id]; for (var k in t) t[k] += f[k] * it.qty; });
  return t;
}
function status(n, r) {
  if (n === 'kcal') {
    if (r >= 0.9 && r <= 1.1) return 'ok';
    if ((r >= 0.7 && r < 0.9) || (r > 1.1 && r <= 1.25)) return 'warn';
    return 'bad';
  }
  return r >= 0.9 ? 'ok' : (r >= 0.6 ? 'warn' : 'bad');
}
function statusLabel(n, st, r) {
  if (st === 'ok') return 'On target';
  if (n === 'kcal') return st === 'warn' ? 'Slightly off' : (r > 1 ? 'High' : 'Low');
  return st === 'warn' ? 'Getting there' : 'Low';
}

/* ---------- swap engine ---------- */
var NUTS = ['p', 'fi', 'fe', 'ca', 'b12'];
function allowed(f) { var d = S.plan; return d === 'n' ? true : (d === 'e' ? f.diet !== 'n' : f.diet === 'v'); }
function weights(tot, t) {
  var w = {};
  NUTS.forEach(function (n) { w[n] = 1 + 2 * Math.max(0, 1 - tot[n] / t[n]); });
  return w;
}
function score(X, C, w, t, dayRatio) {
  var s = 0;
  NUTS.forEach(function (n) { s += w[n] * Math.max(-0.6, Math.min(0.6, (C[n] - X[n]) / t[n])); });
  var dk = C.kcal - X.kcal;
  if (dk > 0) s -= 0.8 * dk / t.kcal; else if (dayRatio > 1.05) s += 0.4 * (-dk) / t.kcal;
  if (HEAVY[X.id] && !HEAVY[C.id]) s += 0.12 + 0.25 * Math.max(0, (X.kcal - C.kcal) / Math.max(X.kcal, 1));
  if (HEAVY[C.id]) s -= 0.2;
  s += Math.max(-1, Math.min(1, (X.cost - C.cost) / Math.max(X.cost, 10))) * 0.08;
  return s;
}
function rank(c) {
  var base = [];
  var bi = c.filter(function (o) { return o.f.cu === 'I'; })[0];
  var bw = c.filter(function (o) { return o.f.cu === 'W'; })[0];
  if (bi) base.push(bi);
  if (bw) base.push(bw);
  c.forEach(function (o) { if (base.length < 3 && base.indexOf(o) < 0) base.push(o); });
  base.sort(function (a, b) { return b.s - a.s; });
  return base.concat(c.filter(function (o) { return base.indexOf(o) < 0; }));
}

/* ---------- small UI pieces ---------- */
function thumb(f) {
  var d = h('span', { class: 'thumb', 'aria-hidden': 'true' });
  if (f.img) {
    var im = h('img', { src: f.img, alt: '', loading: 'lazy' });
    im.addEventListener('error', function () { d.textContent = f.emoji; });
    d.appendChild(im);
  } else { d.textContent = f.emoji; }
  return d;
}
function dietDot(f) { return h('span', { class: 'dot dot-' + f.diet, role: 'img', 'aria-label': DIETLABEL[f.diet] }); }
function pill(text, cls) { return h('span', { class: 'pill ' + cls, text: text }); }
function cuisinePill(f) { return pill(f.cu === 'I' ? 'Indian' : 'Western', f.cu === 'I' ? 'pill-i' : 'pill-w'); }
function hl(name, q) {
  var span = h('span', {});
  q = (q || '').trim().toLowerCase();
  var low = name.toLowerCase(), i = q ? low.indexOf(q) : -1, len = q.length;
  if (i < 0 && q) { var t = q.split(/\s+/)[0]; i = low.indexOf(t); len = t.length; }
  if (i < 0 || !q) { span.textContent = name; return span; }
  span.appendChild(document.createTextNode(name.slice(0, i)));
  span.appendChild(h('strong', { text: name.slice(i, i + len) }));
  span.appendChild(document.createTextNode(name.slice(i + len)));
  return span;
}

/* ---------- search as you type ---------- */
var qIn = $('#q'), sug = $('#sug'), sugItems = [], act = -1;

function matches(raw) {
  var q = raw.trim().toLowerCase();
  if (!q) return POPULAR.map(function (id) { return FOODS[id]; });
  var toks = q.split(/\s+/), out = [];
  LIST.forEach(function (f) {
    var hay = (f.name + ' ' + f.alias).toLowerCase();
    if (!toks.every(function (t) { return hay.indexOf(t) > -1; })) return;
    var nm = f.name.toLowerCase(), s = 0;
    if (nm.indexOf(q) === 0) s += 4; else if (nm.indexOf(q) > -1) s += 3;
    toks.forEach(function (t) {
      if (nm.split(/[\s,()\/]+/).some(function (w) { return w.indexOf(t) === 0; })) s += 2;
      else if (nm.indexOf(t) > -1) s += 1;
    });
    out.push({ f: f, s: s });
  });
  if (!out.length && q.length >= 3) {
    var pre = q.slice(0, 3);
    LIST.forEach(function (f) {
      var words = (f.name + ' ' + f.alias).toLowerCase().split(/[\s,()\/]+/);
      if (words.some(function (w) { return w.indexOf(pre) === 0; })) out.push({ f: f, s: 0 });
    });
  }
  out.sort(function (a, b) { return b.s - a.s || a.f.name.localeCompare(b.f.name); });
  return out.slice(0, 8).map(function (o) { return o.f; });
}
function openSug() { sug.hidden = false; qIn.setAttribute('aria-expanded', 'true'); }
function closeSug() { sug.hidden = true; qIn.setAttribute('aria-expanded', 'false'); qIn.removeAttribute('aria-activedescendant'); act = -1; }
function setActive(i) {
  var opts = sug.querySelectorAll('[role="option"]');
  for (var k = 0; k < opts.length; k++) {
    var on = k === i;
    opts[k].classList.toggle('active', on);
    opts[k].setAttribute('aria-selected', on ? 'true' : 'false');
    if (on) { qIn.setAttribute('aria-activedescendant', opts[k].id); opts[k].scrollIntoView({ block: 'nearest' }); }
  }
  act = i;
}
function renderSug() {
  var q = qIn.value;
  sugItems = matches(q);
  sug.textContent = '';
  if (!sugItems.length) {
    sug.appendChild(h('li', { class: 'nores', role: 'presentation', text: 'No match found. Try a simpler name, like roti or dal.' }));
  } else {
    if (!q.trim()) sug.appendChild(h('li', { class: 'sughead', role: 'presentation', text: 'Popular choices' }));
    sugItems.forEach(function (f, i) {
      var li = h('li', { role: 'option', id: 'opt-' + i, 'aria-selected': 'false' }, [
        thumb(f),
        h('span', { class: 'grow' }, [
          h('span', { class: 'nm' }, [hl(f.name, q)]),
          h('div', { class: 'sub', text: Math.round(f.kcal) + ' kcal, ' + fmt(f.p) + ' g protein' })
        ]),
        dietDot(f),
        cuisinePill(f)
      ]);
      li.addEventListener('mousedown', function (e) { e.preventDefault(); addFood(f.id); });
      sug.appendChild(li);
    });
  }
  openSug();
  setActive(sugItems.length ? 0 : -1);
}
qIn.addEventListener('input', renderSug);
qIn.addEventListener('focus', renderSug);
qIn.addEventListener('click', function () { if (sug.hidden) renderSug(); });
qIn.addEventListener('keydown', function (e) {
  var n = sugItems.length;
  if (e.key === 'ArrowDown') { e.preventDefault(); if (sug.hidden) renderSug(); else if (n) setActive((act + 1) % n); }
  else if (e.key === 'ArrowUp') { e.preventDefault(); if (n) setActive((act - 1 + n) % n); }
  else if (e.key === 'Enter') { if (!sug.hidden && act >= 0 && sugItems[act]) { e.preventDefault(); addFood(sugItems[act].id); } }
  else if (e.key === 'Escape') { closeSug(); }
  else if (e.key === 'Tab') { closeSug(); }
});
document.addEventListener('click', function (e) { if (!e.target.closest('.combo')) closeSug(); });

function addFood(id) {
  var meal = $('#meal').value, f = FOODS[id];
  S.log.push({ uid: S.uid++, id: id, qty: 1, meal: meal, from: null });
  qIn.value = ''; closeSug();
  announce('Added ' + f.name + ' to ' + meal + '.');
  save(); renderAll(); qIn.focus();
}

/* ---------- log actions ---------- */
function find(uid) { return S.log.filter(function (i) { return i.uid === uid; })[0]; }
function setQty(it, d, ref) { it.qty = Math.max(0.5, Math.min(10, it.qty + d)); S.refocus = ref; save(); renderAll(); }
function removeItem(it) {
  S.log = S.log.filter(function (i) { return i !== it; });
  if (S.open === it.uid) S.open = null;
  announce('Removed ' + shortName(FOODS[it.id]) + '.');
  save(); renderAll(); qIn.focus();
}
function toggleSwap(it) { S.open = S.open === it.uid ? null : it.uid; S.refocus = 'swapbtn-' + it.uid; renderAll(); }
function undo(it) {
  var from = it.from; it.id = from; it.from = null;
  announce('Swap undone. Back to ' + shortName(FOODS[from]) + '.');
  S.refocus = 'row-' + it.uid; save(); renderAll();
}
function doSwap(uid, newId) {
  var it = find(uid); if (!it) return;
  var old = FOODS[it.id];
  if (!it.from) it.from = it.id;
  it.id = newId; S.open = null;
  announce('Swapped ' + shortName(old) + ' for ' + shortName(FOODS[newId]) + '.');
  S.refocus = 'row-' + uid; save(); renderAll();
}

/* ---------- rendering ---------- */
function renderProfileBar() {
  var p = S.profile, bar = $('#pbar'); bar.textContent = '';
  var info = [h('span', { class: 'nm', text: p.age + ' years, ' + fmt(p.weight) + ' kg' })];
  if (S.plan) {
    info.push(h('span', { class: 'sub', text: 'Today’s plan:' }));
    info.push(h('span', { class: 'dot dot-' + S.plan, role: 'img', 'aria-label': DIETLABEL[S.plan] }));
    info.push(h('span', { class: 'nm', text: DIETSHORT[S.plan] }));
  }
  bar.appendChild(h('div', { class: 'planbar' }, info));
  bar.appendChild(h('div', { class: 'acts' }, [
    S.plan ? h('button', { class: 'btn sm', type: 'button', text: 'Change plan', onclick: function () {
      S.plan = null; save(); renderAll(); announce('Diet plan cleared. You will be asked again when you open swap ideas.');
    } }) : null,
    h('button', { class: 'btn sm', type: 'button', text: 'Edit details', onclick: function () { showOnboarding(true); } })
  ]));
}

function setPlan(d, uid) {
  S.plan = d;
  announce('Diet plan for today: ' + DIETNAME[d] + '.');
  S.refocus = 'swapbtn-' + uid; save(); renderAll();
}
function planQuestion(it) {
  var wrap = h('div', { class: 'planq' }, [
    h('p', { class: 'nm', id: 'planq-' + it.uid, text: 'What is your diet plan for today?' }),
    h('p', { class: 'sub', text: 'Pick one so BiteWise only suggests foods you eat. You can change it any time.' })
  ]);
  var row = h('div', { class: 'planrow', role: 'group', 'aria-labelledby': 'planq-' + it.uid });
  ['v', 'e', 'n'].forEach(function (d) {
    row.appendChild(h('button', { class: 'chip', type: 'button', onclick: function () { setPlan(d, it.uid); } }, [
      h('span', { class: 'dot dot-' + d, 'aria-hidden': 'true' }), DIETSHORT[d]
    ]));
  });
  wrap.appendChild(row);
  return wrap;
}

function renderQuick() {
  var q = $('#quick'); q.textContent = '';
  q.appendChild(h('span', { class: 'sub', text: 'Quick add:' }));
  POPULAR.slice(0, 6).forEach(function (id) {
    var f = FOODS[id];
    q.appendChild(h('button', { class: 'chip', type: 'button', onclick: function () { addFood(id); } }, [thumb(f), shortName(f)]));
  });
}

function renderLog() {
  var root = $('#log'); root.textContent = '';
  $('#emptylog').hidden = S.log.length > 0;
  $('#clearall').hidden = S.log.length === 0;
  MEALS.forEach(function (m) {
    var items = S.log.filter(function (i) { return i.meal === m; });
    if (!items.length) return;
    var ul = h('ul', { class: 'items' });
    items.forEach(function (it) { ul.appendChild(logItem(it)); });
    root.appendChild(h('div', { class: 'mealgroup' }, [h('h3', { text: m }), ul]));
  });
}

function logItem(it) {
  var f = FOODS[it.id], open = S.open === it.uid;
  var meta = Math.round(f.kcal * it.qty) + ' kcal, ' + fmt(f.p * it.qty) + ' g protein, ' + fmt(f.fi * it.qty) + ' g fiber';
  if (it.from) meta += ' (swapped from ' + shortName(FOODS[it.from]) + ')';
  var row = h('div', { class: 'row', id: 'row-' + it.uid, tabindex: '-1' }, [
    thumb(f),
    h('div', { class: 'grow' }, [
      h('div', { class: 'nm' }, [dietDot(f), h('span', { text: f.name })]),
      h('div', { class: 'sub', text: meta })
    ]),
    h('div', { class: 'qty' }, [
      h('button', { class: 'btn sm', type: 'button', id: 'qm-' + it.uid, 'aria-label': 'Fewer servings of ' + shortName(f), text: '\u2212',
                    onclick: function () { setQty(it, -0.5, 'qm-' + it.uid); } }),
      h('span', { class: 'qv', text: fmt(it.qty) + (it.qty === 1 ? ' serving' : ' servings') }),
      h('button', { class: 'btn sm', type: 'button', id: 'qp-' + it.uid, 'aria-label': 'More servings of ' + shortName(f), text: '+',
                    onclick: function () { setQty(it, 0.5, 'qp-' + it.uid); } })
    ]),
    h('div', { class: 'acts' }, [
      h('button', { class: 'btn sm primary', type: 'button', id: 'swapbtn-' + it.uid, 'aria-expanded': open ? 'true' : 'false',
                    'aria-controls': open ? 'panel-' + it.uid : null, text: open ? 'Hide swaps' : 'Swap ideas',
                    onclick: function () { toggleSwap(it); } }),
      it.from ? h('button', { class: 'btn sm', type: 'button', text: 'Undo swap', onclick: function () { undo(it); } }) : null,
      h('button', { class: 'btn sm', type: 'button', 'aria-label': 'Remove ' + shortName(f), text: 'Remove', onclick: function () { removeItem(it); } })
    ])
  ]);
  var li = h('li', { class: 'item' }, [row]);
  if (open) li.appendChild(swapPanel(it));
  return li;
}

function swapPanel(it) {
  var X = FOODS[it.id], t = targets(), tot = totals(), w = weights(tot, t), ratio = tot.kcal / t.kcal;
  var panel = h('div', { class: 'panel', id: 'panel-' + it.uid });
  if (!S.plan) { panel.appendChild(planQuestion(it)); return panel; }
  var cands = LIST.filter(function (C) {
    return C.id !== X.id && allowed(C) && C.g.some(function (g) { return X.g.indexOf(g) > -1; });
  }).map(function (C) { return { f: C, s: score(X, C, w, t, ratio) }; })
    .filter(function (o) { return o.s > 0.02; })
    .sort(function (a, b) { return b.s - a.s; });

  if (!cands.length) {
    panel.appendChild(h('p', { class: 'muted', text: shortName(X) + ' is already a strong choice for your ' + DIETNAME[S.plan] + ' plan today. No better swap found.' }));
    return panel;
  }
  var ranked = rank(cands), count = S.more[it.uid] || 3, shown = ranked.slice(0, count);
  panel.appendChild(h('p', { text: 'Choose one to replace ' + shortName(X) + '. Every option fits your ' + DIETNAME[S.plan] + ' plan for today.' }));
  var grid = h('div', { class: 'swaps' });
  shown.forEach(function (o) { grid.appendChild(swapCard(it, X, o.f, t)); });
  panel.appendChild(grid);
  if (ranked.length > count) {
    panel.appendChild(h('button', { class: 'btn sm', type: 'button', id: 'more-' + it.uid, text: 'Show more swaps',
      onclick: function () { S.more[it.uid] = count + 3; S.refocus = 'more-' + it.uid; renderAll(); } }));
  }
  panel.appendChild(compareTable(X, shown.map(function (o) { return o.f; })));
  return panel;
}

function swapCard(it, X, C, t) {
  var reasons = [];
  NUTS.forEach(function (n) {
    var d = C[n] - X[n];
    if (d / t[n] >= 0.03) {
      var txt = n === 'p' ? '+' + fmt(d) + ' g protein' : n === 'fi' ? '+' + fmt(d) + ' g fiber' :
                n === 'fe' ? '+' + fmt(d) + ' mg iron' : n === 'ca' ? '+' + Math.round(d) + ' mg calcium' : '+' + fmt(d) + ' µg vitamin B12';
      reasons.push({ rel: d / t[n], txt: txt });
    }
  });
  reasons.sort(function (a, b) { return b.rel - a.rel; });
  var dk = C.kcal - X.kcal, dc = C.cost - X.cost;
  var kTxt = Math.abs(dk) < 5 ? 'Same calories' : (dk > 0 ? '+' : '\u2212') + Math.abs(Math.round(dk)) + ' kcal';
  var cTxt = dc <= -1 ? '\u20B9' + Math.abs(Math.round(dc)) + ' cheaper' : (dc >= 1 ? '\u20B9' + Math.round(dc) + ' costlier' : 'Similar cost');
  var why = h('ul', { class: 'why' });
  reasons.slice(0, 2).forEach(function (r) { why.appendChild(h('li', { class: 'good', text: r.txt })); });
  why.appendChild(h('li', { text: kTxt }));
  why.appendChild(h('li', { class: dc <= -1 ? 'good' : (dc >= 1 ? 'bad' : ''), text: cTxt }));
  return h('div', { class: 'swapcard' }, [
    h('div', { class: 'sc-top' }, [
      thumb(C),
      h('div', { class: 'grow' }, [
        h('div', { class: 'nm' }, [dietDot(C), h('span', { text: C.name })]),
        h('div', { class: 'pills' }, [cuisinePill(C), C.plant ? pill('Plant-based', 'pill-p') : null])
      ])
    ]),
    why,
    h('button', { class: 'btn primary', type: 'button', text: 'Choose this',
                  'aria-label': 'Choose ' + C.name + ' instead of ' + X.name, onclick: function () { doSwap(it.uid, C.id); } })
  ]);
}

function compareTable(X, list) {
  var cols = [X].concat(list);
  var rows = [['Calories (kcal)', 'kcal', 0], ['Protein (g)', 'p', 1], ['Carbs (g)', 'c', 0], ['Fat (g)', 'f', 0],
              ['Fiber (g)', 'fi', 1], ['Iron (mg)', 'fe', 1], ['Calcium (mg)', 'ca', 1], ['Vitamin B12 (\u00B5g)', 'b12', 1],
              ['Approx. cost (\u20B9)', 'cost', -1]];
  var head = h('tr', {}, [h('th', { scope: 'col', text: 'Per serving' })]);
  cols.forEach(function (f, i) { head.appendChild(h('th', { scope: 'col', text: (i === 0 ? 'You ate: ' : '') + shortName(f) })); });
  var body = h('tbody');
  rows.forEach(function (r) {
    var tr = h('tr', {}, [h('th', { scope: 'row', text: r[0] })]);
    cols.forEach(function (f, i) {
      var v = f[r[1]], better = i > 0 && ((r[2] === 1 && v > X[r[1]] + 0.04) || (r[2] === -1 && v < X[r[1]]));
      var shown = (r[1] === 'kcal' || r[1] === 'ca' || r[1] === 'cost') ? String(Math.round(v)) : fmt(v);
      tr.appendChild(h('td', { class: better ? 'better' : '', text: shown }));
    });
    body.appendChild(tr);
  });
  return h('div', { class: 'tablewrap', role: 'region', 'aria-label': 'Nutrition comparison table', tabindex: '0' }, [
    h('table', { class: 'cmp' }, [
      h('caption', { text: 'Nutrition: what you ate vs the suggestions (green means better)' }),
      h('thead', {}, [head]), body
    ])
  ]);
}

function renderToday() {
  var t = targets(), tot = totals(), box = $('#bars');
  $('#tgt').textContent = 'Approximate daily targets for you: ' + t.kcal.toLocaleString('en-IN') + ' kcal, ' + t.p + ' g protein, ' +
    t.fi + ' g fiber, ' + t.fe + ' mg iron, ' + t.ca + ' mg calcium, ' + t.b12 + ' \u00B5g vitamin B12.';
  box.textContent = '';
  if (!S.log.length) {
    box.appendChild(h('p', { class: 'muted', text: 'Add what you ate and your totals will show up here.' }));
    $('#macros').textContent = '';
    return;
  }
  BARS.forEach(function (b) {
    var n = b[0], r = tot[n] / t[n], st = status(n, r);
    var val = n === 'kcal' ? Math.round(tot[n]) : fmt(tot[n]);
    var line = val + ' / ' + (n === 'b12' ? fmt(t[n]) : t[n]) + ' ' + b[2] + ' (' + Math.round(r * 100) + '%) \u00B7 ' + statusLabel(n, st, r);
    box.appendChild(h('div', { class: 'bar-row' }, [
      h('div', { class: 'bar-top' }, [h('strong', { text: b[1] }), h('span', { class: 'muted', text: line })]),
      h('div', { class: 'bar', role: 'img', 'aria-label': b[1] + ': ' + line }, [
        h('i', { class: 's-' + st, style: 'width:' + Math.min(100, Math.round(r * 100)) + '%' })
      ])
    ]));
  });
  $('#macros').textContent = 'Also today: ' + Math.round(tot.c) + ' g carbs and ' + Math.round(tot.f) + ' g fat.';
}

function renderImpact() {
  var swaps = 0, delta = 0, plant = 0;
  S.log.forEach(function (it) {
    if (!it.from) return;
    swaps++; delta += (FOODS[it.id].cost - FOODS[it.from].cost) * it.qty;
    if (FOODS[it.id].plant) plant++;
  });
  var d = Math.round(delta);
  var cost = d < 0 ? '\u20B9' + Math.abs(d) + ' saved' : (d > 0 ? '\u20B9' + d + ' extra' : '\u20B90');
  var box = $('#impact'); box.textContent = '';
  [[String(swaps), 'Swaps made'], [cost, 'Cost change per day'], [String(plant), 'Plant-based swaps']].forEach(function (s) {
    box.appendChild(h('div', { class: 'stat' }, [h('b', { text: s[0] }), h('span', { class: 'sub', text: s[1] })]));
  });
}

function renderAll() {
  if (S.profile) { renderProfileBar(); renderLog(); renderToday(); }
  renderImpact();
  if (S.refocus) {
    var el = document.getElementById(S.refocus); S.refocus = null;
    if (el) el.focus();
  }
}

/* ---------- profile form ---------- */
var form = $('#pform');
function showOnboarding(edit) {
  var el = form.elements, p = S.profile;
  el['age'].value = p ? p.age : ''; el['weight'].value = p ? p.weight : '';
  el['height'].value = p && p.height ? p.height : ''; el['activity'].value = p ? (p.activity || '') : '';
  el['gender'].value = p ? p.gender : '';
  $('#formerr').textContent = '';
  $('#pcancel').hidden = !(edit && S.profile);
  $('#psave').textContent = edit && S.profile ? 'Update details' : 'Save and continue';
  $('#onboarding').hidden = false;
  if (edit) { $('#app').hidden = true; el['age'].focus(); }
}
function showApp() {
  $('#onboarding').hidden = true; $('#app').hidden = false;
  renderAll();
}
function saveProfile() {
  var el = form.elements, err = $('#formerr'); err.textContent = '';
  var age = parseInt(el['age'].value, 10), wt = parseFloat(el['weight'].value);
  var htRaw = el['height'].value, ht = htRaw === '' ? null : parseFloat(htRaw);
  var gender = el['gender'].value;
  if (!(age >= 10 && age <= 80)) { err.textContent = 'Please enter an age between 10 and 80.'; el['age'].focus(); return; }
  if (!(wt >= 25 && wt <= 200)) { err.textContent = 'Please enter a weight between 25 and 200 kg.'; el['weight'].focus(); return; }
  if (ht !== null && !(ht >= 100 && ht <= 220)) { err.textContent = 'Height should be between 100 and 220 cm, or leave it blank.'; el['height'].focus(); return; }
  if (!gender) { err.textContent = 'Please choose a gender option.'; return; }
  S.profile = { age: age, weight: wt, height: ht, gender: gender, activity: el['activity'].value || '' };
  S.open = null; save(); showApp(); qIn.focus();
  window.scrollTo(0, 0);
}
/* Saving does not rely on form submission, so it also works in preview frames that block forms. */
$('#psave').addEventListener('click', saveProfile);
form.addEventListener('submit', function (e) { e.preventDefault(); saveProfile(); });
form.addEventListener('keydown', function (e) {
  if (e.key === 'Enter' && e.target.tagName !== 'BUTTON') { e.preventDefault(); saveProfile(); }
});
$('#pcancel').addEventListener('click', function () { if (S.profile) showApp(); });
var clearArmed = false, clearTimer = null;
function resetClear() { clearArmed = false; clearTimeout(clearTimer); $('#clearall').textContent = 'Clear all'; }
$('#clearall').addEventListener('click', function () {
  if (!clearArmed) {
    clearArmed = true; $('#clearall').textContent = 'Tap again to confirm';
    clearTimer = setTimeout(resetClear, 4000); return;
  }
  resetClear();
  S.log = []; S.open = null; save(); renderAll(); announce('Cleared today\u2019s food.');
});

/* ---------- theme ---------- */
function updateThemeBtn() {
  var dark = document.documentElement.getAttribute('data-theme') === 'dark';
  $('#themelabel').textContent = dark ? 'Light mode' : 'Dark mode';
  $('#themebtn').setAttribute('aria-label', dark ? 'Switch to light mode' : 'Switch to dark mode');
}
$('#themebtn').addEventListener('click', function () {
  var next = document.documentElement.getAttribute('data-theme') === 'dark' ? 'light' : 'dark';
  document.documentElement.setAttribute('data-theme', next);
  try { localStorage.setItem('bitewise.theme', next); } catch (e) {}
  updateThemeBtn();
});

/* ---------- start ---------- */
load();
var hr = new Date().getHours();
$('#meal').value = hr < 11 ? 'Breakfast' : (hr < 15 ? 'Lunch' : (hr < 19 ? 'Snack' : 'Dinner'));
renderQuick(); updateThemeBtn();
if (S.profile) { showOnboarding(false); showApp(); } else { showOnboarding(false); $('#app').hidden = true; }
})();
</script>
</body>
</html>
