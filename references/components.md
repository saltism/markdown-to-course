# Component Library Reference

Reusable JS components for markdown-to-course. The AI calls functions with data; the functions generate all HTML, SVG, and interactivity. **Never write raw SVG or complex HTML by hand when a component exists.**

## Setup

Every generated HTML file needs these in `<head>`:

```html
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
```

And at the bottom of `<body>`, after all module HTML:

```html
<script>/* paste component library below */</script>
<script>
  // Component calls go here (see examples below)
  MTC.conceptCards('#m1-costs', { cards: [...] });
  MTC.loop('#m3-viral-loop', { nodes: [...] });
  // ...
  MTC.init(); // MUST call last — initializes icons, scroll reveal, tooltips, etc.
</script>
```

---

## Quick Reference

| Component | Function | Lucide? | Use when... |
|---|---|---|---|
| Concept cards | `MTC.conceptCards(sel, data)` | Yes | List of 2–6 related concepts with icons |
| Spotlight | `MTC.spotlight(sel, data)` | No | Key term/framework that must stick |
| Loop diagram | `MTC.loop(sel, data)` | No | Cyclical process (growth loops, habit loops) |
| Funnel | `MTC.funnel(sel, data)` | No | Narrowing stages (margins, conversions) |
| Matrix | `MTC.matrix(sel, data)` | No | 2×2 framework |
| Comparison | `MTC.comparison(sel, data)` | No | Side-by-side contrast |
| Data highlights | `MTC.dataHighlights(sel, data)` | No | 2–4 key metrics |
| Steps | `MTC.steps(sel, data)` | No | Sequential numbered process |
| Flow | `MTC.flow(sel, data)` | No | Horizontal step chain with arrows |
| Quote | `MTC.quote(sel, data)` | No | Expert quote with attribution |
| Takeaway | `MTC.takeaway(sel, data)` | No | Module-end key insight |
| Quiz | `MTC.quiz(sel, data)` | No | Multiple-choice question |
| Scenario quiz | `MTC.scenarioQuiz(sel, data)` | No | Quiz with situation context |
| Chain | `MTC.chain(sel, data)` | No | Interactive step-through (ELMR-style) |
| Waterfall | `MTC.waterfall(sel, data)` | No | Formula breakdown (subtraction/addition) |
| Calculator | `MTC.calculator(sel, data)` | No | Interactive formula with sliders |
| Cascade | `MTC.cascade(sel, data)` | No | Compounding cycle visualization |

---

## Component API

### `MTC.conceptCards(selector, data)`

```javascript
MTC.conceptCards('#costs', {
  cards: [
    { icon: 'package', title: 'COGS', desc: 'Unit cost of delivery: cloth, hosting, packaging.' },
    { icon: 'megaphone', title: 'SG&A', desc: 'Sales & marketing: the ad, the commission.' },
    { icon: 'building-2', title: 'OpEx', desc: 'Fixed overhead: rent, R&D, salaries.' },
    { icon: 'landmark', title: 'Finance & Tax', desc: 'Loan interest, taxes, depreciation.' }
  ]
});
```

- `icon`: Lucide icon name (see https://lucide.dev/icons)
- `title`: can include `<span class="term" data-definition="...">` for glossary terms
- Cards auto-grid: 2–4 columns depending on count and viewport

### `MTC.spotlight(selector, data)`

```javascript
MTC.spotlight('#cm-spotlight', {
  term: 'Contribution Margin',
  explanation: 'Revenue minus COGS minus sales & marketing.',
  exampleLabel: 'Why it matters',
  example: 'A CMO\'s job is to improve this number.'
});
```

- Generates the black-panel + explanation layout with auto geometric decoration
- One per screen maximum

### `MTC.loop(selector, data)`

```javascript
MTC.loop('#viral-loop', {
  nodes: [
    { label: 'Sign up' },
    { label: 'Invite' },
    { label: 'Click' },
    { label: 'New user' }
  ]
});
```

- Renders SVG circle with animated orbit, dashed accent ring, moving dot
- Nodes positioned evenly around the circle
- Optional `desc` field per node for sub-label
- Supports 3–6 nodes

### `MTC.funnel(selector, data)`

```javascript
MTC.funnel('#margin-funnel', {
  stages: [
    { label: 'Gross Margin', metric: 'Revenue − COGS', width: 100, color: 'var(--success)' },
    { label: 'Contribution Margin', metric: '− SG&A', width: 72, color: 'var(--info)' },
    { label: 'EBITDA', metric: '− OpEx', width: 48, color: 'var(--accent)' },
    { label: 'Net Margin', metric: '− Everything', width: 28, color: 'var(--ink)' }
  ]
});
```

- Bars animate width on scroll (IntersectionObserver)
- Width is percentage (100 = full width)

### `MTC.matrix(selector, data)`

```javascript
MTC.matrix('#content-2x2', {
  xLabel: '← Company distributes · User distributes →',
  yLabel: '↑ User creates · Company creates ↓',
  cells: [
    { title: 'UG–CD', desc: 'Yelp reviews indexed by Google.' },
    { title: 'UG–UD', desc: 'TikTok, Instagram.' },
    { title: 'CG–CD', desc: 'HubSpot content marketing.' },
    { title: 'CG–UD', desc: 'BuzzFeed, NYT.' }
  ]
});
```

### `MTC.comparison(selector, data)`

```javascript
MTC.comparison('#margins', {
  left: { label: 'Low margin', labelColor: 'var(--error)', title: 'Physical retail', items: ['10–20% GM', 'Supply chain focus'] },
  right: { label: 'High margin', labelColor: 'var(--success)', title: 'SaaS', items: ['70–90% GM', 'Acquire & retain'] }
});
```

### `MTC.dataHighlights(selector, data)`

```javascript
MTC.dataHighlights('#ltv-cac-ratios', {
  cards: [
    { value: '1:1', label: 'Losing money' },
    { value: '3:1', label: 'Ready to scale', countUp: true, target: 3 }
  ]
});
```

- `countUp: true` + `target` enables scroll-triggered count-up animation (appends `:1`)

### `MTC.steps(selector, data)`

```javascript
MTC.steps('#degradation', {
  items: [
    { title: 'Best audience first', desc: 'You target the most qualified prospects.' },
    { title: 'Expand to lower quality', desc: 'To scale, you reach less qualified people.' }
  ]
});
```

### `MTC.flow(selector, data)`

```javascript
MTC.flow('#payback', {
  steps: [
    { tag: 'Step 01', title: 'Acquire', detail: 'Spend $100 CAC' },
    { tag: 'Step 02', title: 'Earn back', detail: '$25/month revenue' },
    { tag: 'Step 03', title: 'Break even', detail: '4 months payback' }
  ]
});
```

### `MTC.quote(selector, data)`

```javascript
MTC.quote('#opendoor', {
  text: 'At Opendoor, we turned off Meta ads because the numbers looked bad. Our CAC went up across every other channel.',
  cite: 'Opendoor MarTech experiment'
});
```

### `MTC.takeaway(selector, data)`

```javascript
MTC.takeaway('#m1-takeaway', {
  text: 'At high-margin businesses, the growth team is a core investment.'
});
```

### `MTC.quiz(selector, data)`

```javascript
MTC.quiz('#m1-quiz', {
  question: 'A company sells t-shirts at $20 each, $5 COGS, $12 marketing. Contribution margin?',
  options: [
    { id: 'a', text: '$15 — subtract only COGS' },
    { id: 'b', text: '$3 — subtract COGS and marketing' },
    { id: 'c', text: '$8 — subtract only marketing' }
  ],
  correct: 'b',
  correctText: '$20 − $5 − $12 = $3. Only 15% — tight, but positive.',
  incorrectText: 'Contribution margin subtracts both COGS and sales/marketing.'
});
```

### `MTC.scenarioQuiz(selector, data)`

```javascript
MTC.scenarioQuiz('#m2-quiz', {
  scenario: 'Your SaaS spends $1M → $5M LTV. CEO doubles to $2M. Total LTV reaches $6M.',
  question: 'Should you keep the $2M budget?',
  options: [...],
  correct: 'c',
  correctText: '...',
  incorrectText: '...'
});
```

### `MTC.chain(selector, data)`

Interactive step-through. User clicks "Next" to light up each stage sequentially.

```javascript
MTC.chain('#elmr', {
  steps: [
    { letter: 'E', name: 'Emotion', desc: 'Fear, curiosity, ambition — sparks the decision' },
    { letter: 'L', name: 'Logic', desc: 'Features, stats — justifies the emotion' },
    { letter: 'M', name: 'Motivation', desc: 'Urgency, scarcity — overcomes friction' },
    { letter: 'R', name: 'Reward', desc: 'Extrinsic, intrinsic, social — confirms the choice' }
  ]
});
```

### `MTC.waterfall(selector, data)`

Animated formula breakdown: bars show addition/subtraction steps.

```javascript
MTC.waterfall('#revenue-breakdown', {
  steps: [
    { label: 'Revenue', value: 100 },
    { label: '− COGS', value: -30 },
    { label: '− SG&A', value: -25 },
    { label: '− OpEx', value: -20 },
    { label: 'Net Margin', value: 25, isResult: true }
  ],
  unit: '$',
  animate: true
});
```

- Positive values: ink color. Negative: error color. Result: accent color.
- Bars animate height on scroll. Running total shown as connecting line.

### `MTC.calculator(selector, data)`

Interactive sliders that compute a formula in real-time.

```javascript
MTC.calculator('#k-factor', {
  title: 'K-Factor calculator',
  inputs: [
    { id: 'invites', label: 'Invites sent per user', min: 1, max: 20, default: 5, step: 1 },
    { id: 'conv', label: 'Invite conversion rate', min: 0.05, max: 0.5, default: 0.2, step: 0.05, format: 'percent' }
  ],
  formula: (vals) => (vals.invites * vals.conv).toFixed(2),
  resultLabel: 'K-Factor',
  thresholds: [
    { value: 1, label: 'Self-sustaining growth', color: 'var(--success)' }
  ]
});
```

- Each input renders as a labeled range slider with live value display
- Result updates on every input change
- Threshold line shows when result crosses a meaningful boundary

### `MTC.cascade(selector, data)`

Compounding cycle visualization (Growth Multiplier).

```javascript
MTC.cascade('#growth-multiplier', {
  title: 'Growth Multiplier',
  initial: 1000,
  ratio: 0.54,
  maxCycles: 6,
  suffix: ' users'
});
```

- Renders diminishing horizontal bars: Cycle 1 = 1000, Cycle 2 = 540, etc.
- Final row shows TOTAL with accent highlight
- Includes V slider to explore different ratios interactively

---

## Full Implementation

Copy the entire block below into a `<script>` tag in the generated HTML, BEFORE the component calls.

```javascript
const MTC = {};

// ---- CONCEPT CARDS ----
MTC.conceptCards = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'concept-cards stagger-children';
  el.innerHTML = data.cards.map(c =>
    `<div class="concept-card animate-in">
      <div class="concept-icon"><i data-lucide="${c.icon}"></i></div>
      <h4 class="concept-title">${c.title}</h4>
      <p class="concept-desc">${c.desc}</p>
    </div>`
  ).join('');
};

// ---- SPOTLIGHT ----
MTC.spotlight = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  const decos = [
    '<line x1="4" y1="10" x2="36" y2="10"/><line x1="8" y1="20" x2="32" y2="20"/><line x1="12" y1="30" x2="28" y2="30"/>',
    '<circle cx="20" cy="20" r="16"/><circle cx="20" cy="20" r="9"/><circle cx="20" cy="20" r="3"/>',
    '<path d="M6 32L14 24L22 28L34 12"/><path d="M26 12H34V20"/>',
    '<path d="M10 20H20"/><path d="M20 20L32 10"/><path d="M20 20L32 30"/><circle cx="10" cy="20" r="3"/><circle cx="32" cy="10" r="3"/><circle cx="32" cy="30" r="3"/>',
    '<circle cx="20" cy="20" r="14"/><path d="M20 8V20L28 26"/>',
    '<circle cx="20" cy="20" r="6"/><circle cx="20" cy="20" r="12"/><circle cx="20" cy="20" r="18"/>',
    '<circle cx="10" cy="10" r="3"/><circle cx="30" cy="10" r="3"/><circle cx="20" cy="28" r="3"/><path d="M13 10H27"/><path d="M11 13L18 26"/><path d="M29 13L22 26"/>'
  ];
  const deco = decos[Math.floor(Math.random() * decos.length)];
  el.className = 'spotlight-block animate-in';
  el.innerHTML =
    `<div class="spotlight-concept">
      <span class="spotlight-label">Key concept</span>
      <h3 class="spotlight-term">${data.term}</h3>
      <svg class="spotlight-deco" viewBox="0 0 40 40">${deco}</svg>
    </div>
    <div class="spotlight-explanation">
      <span class="spotlight-label">In plain language</span>
      <p class="spotlight-text">${data.explanation}</p>
      ${data.example ? `<div class="spotlight-example"><span class="spotlight-example-label">${data.exampleLabel || 'Example'}</span><p>${data.example}</p></div>` : ''}
    </div>`;
};

// ---- LOOP DIAGRAM ----
MTC.loop = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  const n = data.nodes.length, R = 130, CX = 200, CY = 200;
  const nw = data.nodes.some(d => d.desc) ? 130 : 110;
  const nh = data.nodes.some(d => d.desc) ? 60 : 46;
  let nodesG = '', pathD = '';
  data.nodes.forEach((nd, i) => {
    const a = (i / n) * Math.PI * 2 - Math.PI / 2;
    const x = CX + R * Math.cos(a), y = CY + R * Math.sin(a);
    pathD += (i === 0 ? 'M' : `A${R},${R} 0 0,1 `) + `${x.toFixed(1)},${y.toFixed(1)} `;
    nodesG += `<g class="loop-node-g" transform="translate(${x.toFixed(1)},${y.toFixed(1)})">`;
    nodesG += `<rect x="${-nw/2}" y="${-nh/2}" width="${nw}" height="${nh}"/>`;
    nodesG += `<text text-anchor="middle" dy="${nd.desc ? '-2' : '4'}" style="font-family:var(--font-sans);font-size:11px;font-weight:600;fill:var(--ink);letter-spacing:.03em">${nd.label}</text>`;
    if (nd.desc) nodesG += `<text text-anchor="middle" dy="12" style="font-family:var(--font-sans);font-size:9px;fill:var(--ink-60)">${nd.desc}</text>`;
    nodesG += '</g>';
  });
  const a0 = -Math.PI / 2;
  pathD += `A${R},${R} 0 0,1 ${(CX + R * Math.cos(a0)).toFixed(1)},${(CY + R * Math.sin(a0)).toFixed(1)}`;
  const pid = '_lp' + Math.random().toString(36).slice(2, 7);
  const vb = CY + R + nh/2 + 10;
  el.className = 'loop-container animate-in';
  el.innerHTML = `<svg viewBox="0 0 400 ${vb}" style="width:100%;max-width:420px;margin:0 auto;display:block">
    <circle cx="${CX}" cy="${CY}" r="${R}" fill="none" stroke="var(--ink-20)" stroke-width="1.5"/>
    <circle cx="${CX}" cy="${CY}" r="${R}" fill="none" stroke="var(--accent)" stroke-width="2" stroke-dasharray="8 6" style="animation:_orbSpin 12s linear infinite"/>
    ${nodesG}
    <path id="${pid}" d="${pathD}" fill="none"/>
    <circle r="5" fill="var(--accent)"><animateMotion dur="${2.5 + n * 0.5}s" repeatCount="indefinite"><mpath href="#${pid}"/></animateMotion></circle>
  </svg>`;
};

// ---- FUNNEL ----
MTC.funnel = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'funnel-diagram';
  el.innerHTML = data.stages.map(s =>
    `<div class="funnel-stage"><div class="funnel-bar" style="--w:${s.width}%;background:${s.color}"><span class="funnel-label">${s.label}</span><span class="funnel-metric">${s.metric}</span></div></div>`
  ).join('');
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { el.querySelectorAll('.funnel-bar').forEach((b, i) => setTimeout(() => b.classList.add('animated'), i * 200)); obs.unobserve(el); }});
  }, { threshold: 0.3 });
  obs.observe(el);
};

// ---- MATRIX ----
MTC.matrix = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'matrix-diagram animate-in';
  el.innerHTML =
    `${data.xLabel ? `<div class="matrix-label">${data.xLabel}</div>` : ''}
    <div class="matrix-grid">${data.cells.map(c => `<div class="matrix-cell"><strong>${c.title}</strong><p>${c.desc}</p></div>`).join('')}</div>
    ${data.yLabel ? `<div class="matrix-label">${data.yLabel}</div>` : ''}`;
};

// ---- COMPARISON ----
MTC.comparison = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'comparison-cards animate-in';
  const card = (d) => `<div class="comparison-card">
    <span class="comparison-label" style="background:${d.labelBg || 'var(--ink-10)'};color:${d.labelColor || 'var(--ink)'}">${d.label}</span>
    <h4>${d.title}</h4>
    <ul>${d.items.map(i => `<li>${i}</li>`).join('')}</ul>
  </div>`;
  el.innerHTML = card(data.left) + '<div class="comparison-vs">VS</div>' + card(data.right);
};

// ---- DATA HIGHLIGHTS ----
MTC.dataHighlights = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'data-highlights stagger-children';
  el.innerHTML = data.cards.map(c => {
    const cls = c.countUp ? ' count-up' : '';
    const dt = c.countUp ? ` data-target="${c.target}"` : '';
    return `<div class="data-card animate-in"><span class="data-value${cls}"${dt}>${c.countUp ? '0' : c.value}</span><span class="data-label">${c.label}</span>${c.context ? `<p class="data-context">${c.context}</p>` : ''}</div>`;
  }).join('');
};

// ---- STEPS ----
MTC.steps = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'step-cards stagger-children';
  el.innerHTML = data.items.map((s, i) =>
    `<div class="step-card animate-in"><div class="step-num">${i + 1}</div><div class="step-body"><strong>${s.title}</strong><p>${s.desc}</p></div></div>`
  ).join('');
};

// ---- FLOW ----
MTC.flow = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'flow-steps animate-in';
  el.innerHTML = data.steps.map(s =>
    `<div class="flow-step"><span class="flow-step-tag">${s.tag}</span><strong>${s.title}</strong><p class="flow-step-detail">${s.detail}</p></div>`
  ).join('');
};

// ---- QUOTE ----
MTC.quote = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'quote-callout animate-in';
  el.innerHTML = `<blockquote>"${data.text}"</blockquote><cite>— ${data.cite}</cite>`;
};

// ---- TAKEAWAY ----
MTC.takeaway = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'takeaway-callout animate-in';
  el.innerHTML = `<div class="takeaway-icon">→</div><div class="takeaway-content"><strong class="takeaway-title">Key takeaway</strong><p>${data.text}</p></div>`;
};

// ---- QUIZ ----
MTC.quiz = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  const qid = '_q' + Math.random().toString(36).slice(2, 7);
  el.className = 'quiz-container';
  el.innerHTML =
    `<div class="quiz-header">// Check your understanding</div>
    <div class="quiz-question-block" id="${qid}" data-correct="${data.correct}">
      <h3 class="quiz-question">${data.question}</h3>
      <div class="quiz-options">${data.options.map(o =>
        `<button class="quiz-option" data-value="${o.id}" onclick="MTC._selectOpt(this)"><div class="quiz-option-radio"></div><span>${o.text}</span></button>`
      ).join('')}</div>
      <div class="quiz-feedback" data-correct-text="${MTC._esc(data.correctText)}" data-incorrect-text="${MTC._esc(data.incorrectText)}"></div>
    </div>
    <button class="quiz-check-btn" onclick="MTC._checkQuiz(this)">Check answer</button>`;
};

// ---- SCENARIO QUIZ ----
MTC.scenarioQuiz = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  const qid = '_q' + Math.random().toString(36).slice(2, 7);
  el.className = 'quiz-container';
  el.innerHTML =
    `<div class="quiz-header">${data.header || '// Check your understanding'}</div>
    <div class="scenario-context"><span class="scenario-label">Scenario</span><p>${data.scenario}</p></div>
    <div class="quiz-question-block" id="${qid}" data-correct="${data.correct}">
      <h3 class="quiz-question">${data.question}</h3>
      <div class="quiz-options">${data.options.map(o =>
        `<button class="quiz-option" data-value="${o.id}" onclick="MTC._selectOpt(this)"><div class="quiz-option-radio"></div><span>${o.text}</span></button>`
      ).join('')}</div>
      <div class="quiz-feedback" data-correct-text="${MTC._esc(data.correctText)}" data-incorrect-text="${MTC._esc(data.incorrectText)}"></div>
    </div>
    <button class="quiz-check-btn" onclick="MTC._checkQuiz(this)">Check answer</button>`;
};

// ---- CHAIN (generalized ELMR) ----
MTC.chain = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  const cid = '_ch' + Math.random().toString(36).slice(2, 7);
  el.innerHTML =
    `<div class="elmr-chain" id="${cid}">${data.steps.map((s, i) =>
      `<div class="elmr-step" data-idx="${i}"><div class="elmr-letter">${s.letter}</div><div class="elmr-name">${s.name}</div><div class="elmr-desc">${s.desc}</div></div>`
    ).join('')}</div>
    <div class="elmr-controls">
      <button onclick="MTC._chainNext('${cid}')">Next stage →</button>
      <button onclick="MTC._chainReset('${cid}')">Reset</button>
    </div>`;
  el.classList.add('animate-in');
};

// ---- WATERFALL (formula breakdown) ----
MTC.waterfall = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'waterfall-chart animate-in';
  const maxVal = Math.max(...data.steps.map(s => Math.abs(s.value)));
  let running = 0;
  const bars = data.steps.map(s => {
    const prev = running;
    if (!s.isResult) running += s.value;
    const barVal = s.isResult ? s.value : Math.abs(s.value);
    const pct = (barVal / maxVal) * 100;
    const color = s.isResult ? 'var(--accent)' : (s.value > 0 ? 'var(--ink)' : 'var(--error)');
    return `<div class="wf-row"><span class="wf-label">${s.label}</span><div class="wf-track"><div class="wf-bar" style="--w:${pct}%;background:${color}">${data.unit || ''}${Math.abs(s.value)}</div></div></div>`;
  });
  el.innerHTML = bars.join('');
  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => { if (e.isIntersecting) { el.querySelectorAll('.wf-bar').forEach((b, i) => setTimeout(() => b.classList.add('animated'), i * 180)); obs.unobserve(el); }});
  }, { threshold: 0.3 });
  obs.observe(el);
};

// ---- CALCULATOR (interactive formula) ----
MTC.calculator = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'calc-container animate-in';
  const cid = '_calc' + Math.random().toString(36).slice(2, 7);
  const inputs = data.inputs.map(inp => {
    const fmt = inp.format === 'percent' ? `(${inp.default * 100}%)` : inp.default;
    return `<div class="calc-input">
      <label>${inp.label}: <span id="${cid}_${inp.id}_val">${fmt}</span></label>
      <input type="range" id="${cid}_${inp.id}" min="${inp.min}" max="${inp.max}" value="${inp.default}" step="${inp.step}" oninput="MTC._calcUpdate('${cid}')">
    </div>`;
  }).join('');
  el.innerHTML =
    `${data.title ? `<div class="calc-title">${data.title}</div>` : ''}
    ${inputs}
    <div class="calc-result"><span class="calc-result-label">${data.resultLabel}:</span> <span id="${cid}_result" class="calc-result-value"></span></div>
    ${data.thresholds ? `<div class="calc-threshold" id="${cid}_threshold"></div>` : ''}`;
  el._data = data;
  el._cid = cid;
  MTC._calcUpdate(cid);
};

// ---- CASCADE (compounding cycles) ----
MTC.cascade = function(sel, data) {
  const el = document.querySelector(sel); if (!el) return;
  el.className = 'cascade-container animate-in';
  const cid = '_cas' + Math.random().toString(36).slice(2, 7);
  el.innerHTML =
    `${data.title ? `<div class="calc-title">${data.title}</div>` : ''}
    <div class="calc-input"><label>V (ratio): <span id="${cid}_vval">${data.ratio}</span></label>
      <input type="range" id="${cid}_v" min="0.1" max="0.95" value="${data.ratio}" step="0.01" oninput="MTC._cascadeUpdate('${cid}')">
    </div>
    <div id="${cid}_bars" class="cascade-bars"></div>
    <div id="${cid}_total" class="cascade-total"></div>`;
  el._data = data;
  el._cid = cid;
  MTC._cascadeUpdate(cid);
};

// ---- INTERNAL HELPERS ----
MTC._esc = function(s) { return s.replace(/"/g, '&quot;'); };

MTC._selectOpt = function(btn) {
  btn.closest('.quiz-question-block').querySelectorAll('.quiz-option').forEach(o => o.classList.remove('selected'));
  btn.classList.add('selected');
};

MTC._checkQuiz = function(btn) {
  const c = btn.closest('.quiz-container');
  c.querySelectorAll('.quiz-question-block').forEach(q => {
    const s = q.querySelector('.quiz-option.selected'), f = q.querySelector('.quiz-feedback'), cv = q.dataset.correct;
    if (!s) { f.textContent = 'Pick an answer.'; f.className = 'quiz-feedback show'; f.style.background = 'var(--info-light)'; f.style.color = 'var(--info)'; return; }
    if (s.dataset.value === cv) { s.classList.add('correct'); f.innerHTML = '<strong>Correct.</strong> ' + f.dataset.correctText; f.className = 'quiz-feedback show success'; }
    else { s.classList.add('incorrect'); const cb = q.querySelector(`[data-value="${cv}"]`); if (cb) cb.classList.add('correct'); f.innerHTML = '<strong>Not quite.</strong> ' + f.dataset.incorrectText; f.className = 'quiz-feedback show error'; }
    q.querySelectorAll('.quiz-option').forEach(o => o.disabled = true);
  });
  btn.style.display = 'none';
};

MTC._chainStates = {};
MTC._chainNext = function(id) {
  if (!(id in MTC._chainStates)) MTC._chainStates[id] = -1;
  const steps = document.querySelectorAll('#' + id + ' .elmr-step');
  MTC._chainStates[id] = Math.min(MTC._chainStates[id] + 1, steps.length - 1);
  steps.forEach((s, i) => { if (i <= MTC._chainStates[id]) s.classList.add('lit'); else s.classList.remove('lit'); });
};
MTC._chainReset = function(id) {
  MTC._chainStates[id] = -1;
  document.querySelectorAll('#' + id + ' .elmr-step').forEach(s => s.classList.remove('lit'));
};

MTC._calcUpdate = function(cid) {
  const container = document.querySelector(`[class*="calc-container"]`);
  let c = null;
  document.querySelectorAll('.calc-container').forEach(el => { if (el._cid === cid) c = el; });
  if (!c) return;
  const data = c._data;
  const vals = {};
  data.inputs.forEach(inp => {
    const slider = document.getElementById(cid + '_' + inp.id);
    if (!slider) return;
    vals[inp.id] = parseFloat(slider.value);
    const display = document.getElementById(cid + '_' + inp.id + '_val');
    if (display) display.textContent = inp.format === 'percent' ? (vals[inp.id] * 100).toFixed(0) + '%' : vals[inp.id];
  });
  const result = data.formula(vals);
  const resultEl = document.getElementById(cid + '_result');
  if (resultEl) resultEl.textContent = result;
  if (data.thresholds) {
    const thEl = document.getElementById(cid + '_threshold');
    const num = parseFloat(result);
    const hit = data.thresholds.find(t => num >= t.value);
    if (thEl) {
      if (hit) { thEl.textContent = hit.label; thEl.style.color = hit.color; thEl.style.opacity = '1'; }
      else { thEl.textContent = ''; thEl.style.opacity = '0'; }
    }
  }
};

MTC._cascadeUpdate = function(cid) {
  let c = null;
  document.querySelectorAll('.cascade-container').forEach(el => { if (el._cid === cid) c = el; });
  if (!c) return;
  const data = c._data;
  const vSlider = document.getElementById(cid + '_v');
  const v = parseFloat(vSlider.value);
  document.getElementById(cid + '_vval').textContent = v.toFixed(2);
  const barsEl = document.getElementById(cid + '_bars');
  const totalEl = document.getElementById(cid + '_total');
  let current = data.initial, total = 0;
  const rows = [];
  for (let i = 0; i < (data.maxCycles || 6); i++) {
    if (i > 0) current = Math.round(current * v);
    if (current < 1) break;
    total += current;
    const pct = (current / data.initial) * 100;
    rows.push(`<div class="cascade-row"><span class="cascade-label">Cycle ${i + 1}</span><div class="cascade-track"><div class="cascade-bar" style="width:${pct}%">${current.toLocaleString()}${data.suffix || ''}</div></div></div>`);
  }
  barsEl.innerHTML = rows.join('');
  const mult = (1 / (1 - v)).toFixed(1);
  totalEl.innerHTML = `<strong>Total: ${total.toLocaleString()}${data.suffix || ''}</strong> · Multiplier: <strong>${mult}×</strong>`;
};

// ---- INIT ----
MTC.init = function() {
  // Lucide icons
  if (typeof lucide !== 'undefined') lucide.createIcons();

  // Scroll reveal
  const obs = new IntersectionObserver(e => { e.forEach(x => { if (x.isIntersecting) { x.target.classList.add('visible'); obs.unobserve(x.target); }}); }, { rootMargin: '0px 0px -8% 0px', threshold: 0.1 });
  document.querySelectorAll('.animate-in').forEach(el => obs.observe(el));
  document.querySelectorAll('.stagger-children').forEach(p => { Array.from(p.children).forEach((c, i) => c.style.setProperty('--si', i)); });

  // Count-up
  const countObs = new IntersectionObserver(e => { e.forEach(x => { if (x.isIntersecting) { const tgt = parseInt(x.target.dataset.target); let c = 0; const step = () => { c++; x.target.textContent = c + ':1'; if (c < tgt) requestAnimationFrame(step); }; requestAnimationFrame(step); countObs.unobserve(x.target); }}); }, { threshold: 0.5 });
  document.querySelectorAll('.count-up').forEach(el => countObs.observe(el));

  // Progress bar
  const pBar = document.querySelector('.progress-bar');
  if (pBar) window.addEventListener('scroll', () => requestAnimationFrame(() => { const s = window.scrollY, h = document.documentElement.scrollHeight - window.innerHeight; pBar.style.width = (h > 0 ? s / h * 100 : 0) + '%'; }), { passive: true });

  // Nav dots
  const dots = document.querySelectorAll('.nav-dot'), mods = document.querySelectorAll('.module');
  dots.forEach(d => d.addEventListener('click', () => { const t = document.getElementById(d.dataset.target); if (t) t.scrollIntoView({ behavior: 'smooth' }); }));
  const mObs = new IntersectionObserver(e => { e.forEach(x => { if (x.isIntersecting) { const id = x.target.id; dots.forEach(d => { d.classList.remove('active'); if (d.dataset.target === id) d.classList.add('active'); }); document.querySelector(`[data-target="${id}"]`)?.classList.add('visited'); }}); }, { rootMargin: '-30% 0px -30% 0px' });
  mods.forEach(m => mObs.observe(m));

  // Keyboard nav
  const mIds = Array.from(mods).map(m => m.id); let cur = 0;
  document.addEventListener('keydown', e => { if (['INPUT', 'TEXTAREA'].includes(e.target.tagName)) return; if (e.key === 'ArrowDown' || e.key === 'ArrowRight') { e.preventDefault(); cur = Math.min(cur + 1, mIds.length - 1); document.getElementById(mIds[cur]).scrollIntoView({ behavior: 'smooth' }); } if (e.key === 'ArrowUp' || e.key === 'ArrowLeft') { e.preventDefault(); cur = Math.max(cur - 1, 0); document.getElementById(mIds[cur]).scrollIntoView({ behavior: 'smooth' }); }});

  // Glossary tooltips
  let aT = null;
  function posT(t, tip) { const r = t.getBoundingClientRect(), w = 280; let l = r.left + r.width / 2 - w / 2; l = Math.max(8, Math.min(l, window.innerWidth - w - 8)); document.body.appendChild(tip); const h = tip.offsetHeight; if (r.top - h - 8 < 0) { tip.style.top = (r.bottom + 8) + 'px'; tip.classList.add('flip'); } else { tip.style.top = (r.top - h - 8) + 'px'; tip.classList.remove('flip'); } tip.style.left = l + 'px'; }
  document.querySelectorAll('.term').forEach(t => {
    const tip = document.createElement('span'); tip.className = 'term-tooltip'; tip.textContent = t.dataset.definition;
    t.addEventListener('mouseenter', () => { if (aT && aT !== tip) { aT.classList.remove('visible'); aT.remove(); } posT(t, tip); requestAnimationFrame(() => tip.classList.add('visible')); aT = tip; });
    t.addEventListener('mouseleave', () => { tip.classList.remove('visible'); setTimeout(() => { if (!tip.classList.contains('visible')) tip.remove(); }, 150); aT = null; });
    t.addEventListener('click', e => { e.stopPropagation(); if (aT && aT !== tip) { aT.classList.remove('visible'); aT.remove(); } if (tip.classList.contains('visible')) { tip.classList.remove('visible'); tip.remove(); aT = null; } else { posT(t, tip); requestAnimationFrame(() => tip.classList.add('visible')); aT = tip; }});
  });
  document.addEventListener('click', () => { if (aT) { aT.classList.remove('visible'); aT.remove(); aT = null; }});
};
```

---

## Lucide Icon Reference (common picks)

| Concept | Icon name |
|---|---|
| Cost / COGS | `package` |
| Marketing / SG&A | `megaphone` |
| Office / OpEx | `building-2` |
| Finance / Bank | `landmark` |
| Declining | `trending-down` |
| Link / Connected | `link` |
| Word of mouth | `message-circle` |
| Loop / Cycle | `refresh-cw` |
| Visibility | `eye` |
| Gift / Incentive | `gift` |
| Inbox / Inbound | `inbox` |
| Growth / PLG | `trending-up` |
| Infinity / Double | `infinity` |
| Bidirectional | `arrow-left-right` |
| Forward / Future | `circle-arrow-right` |
| Features / Gear | `settings` |
| Statistics | `bar-chart-3` |
| Trust / Shield | `shield` |
| Price / Dollar | `dollar-sign` |
| Reward / Star | `star` |
| Diamond / Value | `diamond` |
| People / Social | `users` |
| New user | `user-plus` |
| Mail / Invite | `mail` |
| Click / Pointer | `mouse-pointer` |
| Trigger / Zap | `zap` |
| Target | `target` |
| Clock / Time | `clock` |
| Brain / Psych | `brain` |
| Scale / Balance | `scale` |
| Layers | `layers` |
| Network | `network` |
| Search / Research | `search` |
| Lock / Security | `lock` |
| Globe / Market | `globe` |
| Repeat | `repeat` |
