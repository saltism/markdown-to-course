# Design System Reference

Complete CSS for the course. Copy the full `<style>` block below into the generated HTML. Adapt accent color to suit the content's personality.

## Setup

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
```

## Full CSS

Copy this entire block into `<style>`:

```css
:root{
  --bg:#E4DFD0;--ink:#080808;--ink-60:rgba(8,8,8,.6);--ink-20:rgba(8,8,8,.2);--ink-10:rgba(8,8,8,.1);
  --accent:#6C4AB6;--accent-light:#EDE8F5;--accent-dark:#4a337e;
  --surface:#fff;--surface-warm:#F0EDE4;
  --success:#2D8B55;--success-light:#E8F5EE;
  --error:#C93B3B;--error-light:#FDE8E8;
  --info:#2A7B9B;--info-light:#E4F2F7;
  --font-sans:'Helvetica Neue',Helvetica,Arial,sans-serif;
  --font-mono:'Space Mono','Courier New',monospace;
  --text-xs:.7rem;--text-sm:.8125rem;--text-base:.9375rem;--text-lg:1.0625rem;
  --text-xl:1.25rem;--text-2xl:1.5rem;--text-3xl:2rem;--text-4xl:2.5rem;
  --nav-height:52px;
}
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-snap-type:y proximity;scroll-behavior:smooth}
body{font-family:var(--font-sans);background:var(--bg);color:var(--ink);line-height:1.6;-webkit-font-smoothing:antialiased}
::-webkit-scrollbar{width:5px}
::-webkit-scrollbar-track{background:transparent}
::-webkit-scrollbar-thumb{background:var(--ink-20);border-radius:99px}

/* ---- NAV ---- */
.nav{position:fixed;top:0;left:0;right:0;z-index:100;background:rgba(228,223,208,.92);backdrop-filter:blur(16px);border-bottom:2px solid var(--ink)}
.progress-bar{position:absolute;top:0;left:0;height:2px;background:var(--accent);transition:width .3s;width:0}
.nav-inner{display:flex;align-items:center;justify-content:space-between;max-width:1200px;margin:0 auto;padding:0 2rem;height:var(--nav-height)}
.nav-title{font-weight:500;font-size:var(--text-sm);text-transform:uppercase;letter-spacing:.05em}
.nav-title sup{font-family:var(--font-mono);font-size:.6rem;font-weight:400;margin-left:4px}
.nav-dots{display:flex;gap:12px;align-items:center}
.nav-dot{width:8px;height:8px;border:1.5px solid var(--ink-60);background:transparent;cursor:pointer;transition:all .2s;padding:0;border-radius:0}
.nav-dot.active{background:var(--accent);border-color:var(--accent)}
.nav-dot.visited{background:var(--ink);border-color:var(--ink)}
.nav-dot:hover{border-color:var(--accent);transform:scale(1.4)}

/* ---- MODULE ---- */
.module{min-height:100dvh;min-height:100vh;scroll-snap-align:start;padding:5rem 2rem 4rem;padding-top:calc(var(--nav-height) + 3rem)}
.module-content{max-width:860px;margin:0 auto}
.module-header{margin-bottom:4rem;border-top:2px solid var(--ink);padding-top:1.5rem}
.module-number{font-family:var(--font-mono);font-size:var(--text-xs);text-transform:uppercase;letter-spacing:.15em;color:var(--ink-60);display:block;margin-bottom:.75rem}
.module-title{font-size:var(--text-4xl);font-weight:500;letter-spacing:-.02em;line-height:1.1}
.module-subtitle{font-size:var(--text-base);color:var(--ink-60);margin-top:.75rem;max-width:55ch}
.screen{margin-bottom:5rem}
.screen-heading{font-size:var(--text-xl);font-weight:500;letter-spacing:.01em;margin-bottom:1.5rem;padding-bottom:.75rem;border-bottom:1px solid var(--ink-20)}
.screen p{font-size:var(--text-base);line-height:1.7;color:var(--ink);margin-bottom:1rem;max-width:60ch}

/* ---- ANIMATE ---- */
.animate-in{opacity:0;transform:translateY(16px);transition:opacity .6s cubic-bezier(.16,1,.3,1),transform .6s cubic-bezier(.16,1,.3,1)}
.animate-in.visible{opacity:1;transform:translateY(0)}
.stagger-children>.animate-in{transition-delay:calc(var(--si,0)*.1s)}
@keyframes _orbSpin{to{stroke-dashoffset:-100}}

/* ---- CONCEPT CARDS ---- */
.concept-cards{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:1px;margin:2rem 0;background:var(--ink-20)}
.concept-card{background:var(--bg);padding:1.5rem;transition:background .2s}
.concept-card:hover{background:var(--surface-warm)}
.concept-icon{margin-bottom:.75rem;color:var(--ink-60)}
.concept-icon svg,.concept-icon i{width:22px;height:22px}
.concept-title{font-family:var(--font-mono);font-size:var(--text-xs);font-weight:700;letter-spacing:.05em;margin-bottom:.5rem}
.concept-desc{font-size:var(--text-sm);color:var(--ink-60);line-height:1.5}

/* ---- SPOTLIGHT ---- */
.spotlight-block{display:grid;grid-template-columns:1fr 1.4fr;margin:2.5rem 0;border:2px solid var(--ink);overflow:hidden}
.spotlight-concept{background:var(--ink);color:var(--bg);padding:2.5rem 2rem;display:flex;flex-direction:column;justify-content:center}
.spotlight-label{font-family:var(--font-mono);font-size:.6rem;text-transform:uppercase;letter-spacing:.15em;opacity:.5;display:block;margin-bottom:.5rem}
.spotlight-term{font-size:var(--text-2xl);font-weight:500;letter-spacing:.01em;margin:0}
.spotlight-deco{width:40px;height:40px;opacity:.35;margin-top:1rem}
.spotlight-deco *{fill:none;stroke:var(--bg);stroke-width:1.5;stroke-linecap:round;stroke-linejoin:round}
.spotlight-explanation{background:var(--bg);padding:2rem;border-left:none}
.spotlight-text{font-size:var(--text-base);line-height:1.7;margin-bottom:1rem}
.spotlight-example{background:var(--surface-warm);padding:1rem 1.25rem;border-left:3px solid var(--ink-20)}
.spotlight-example-label{font-family:var(--font-mono);font-size:.6rem;font-weight:700;color:var(--ink-60);text-transform:uppercase;letter-spacing:.1em}
.spotlight-example p{font-size:var(--text-sm);color:var(--ink-60);margin-top:.25rem;margin-bottom:0}

/* ---- COMPARISON ---- */
.comparison-cards{display:grid;grid-template-columns:1fr auto 1fr;gap:1rem;margin:2rem 0;align-items:start}
.comparison-card{border:1px solid var(--ink-20);padding:1.5rem}
.comparison-label{display:inline-block;font-family:var(--font-mono);font-size:.6rem;font-weight:700;text-transform:uppercase;letter-spacing:.1em;padding:.25rem .75rem;margin-bottom:1rem}
.comparison-card h4{font-size:var(--text-lg);font-weight:500;letter-spacing:.01em;margin-bottom:1rem}
.comparison-card ul{list-style:none;padding:0}
.comparison-card li{font-size:var(--text-sm);color:var(--ink-60);padding:.5rem 0;border-bottom:1px solid var(--ink-10)}
.comparison-card li:last-child{border:none}
.comparison-vs{font-family:var(--font-mono);font-weight:700;font-size:var(--text-sm);color:var(--ink-60);align-self:center;text-transform:uppercase}

/* ---- DATA HIGHLIGHTS ---- */
.data-highlights{display:grid;grid-template-columns:repeat(auto-fit,minmax(160px,1fr));gap:1px;margin:2rem 0;background:var(--ink-20)}
.data-card{background:var(--bg);padding:1.5rem;text-align:center}
.data-value{font-family:var(--font-mono);font-size:var(--text-3xl);font-weight:700;display:block}
.data-label{font-family:var(--font-mono);font-size:.65rem;text-transform:uppercase;letter-spacing:.1em;display:block;margin-top:.5rem;color:var(--ink-60)}
.data-context{font-size:var(--text-xs);color:var(--ink-60);margin-top:.25rem}
.count-up{font-variant-numeric:tabular-nums}

/* ---- LOOP DIAGRAM ---- */
.loop-container{margin:3rem auto;max-width:420px}
.loop-node-g rect{fill:var(--bg);stroke:var(--ink);stroke-width:1.5;transition:fill .2s}
.loop-node-g:hover rect{fill:var(--surface-warm)}

/* ---- FUNNEL ---- */
.funnel-diagram{max-width:560px;margin:2.5rem auto}
.funnel-stage{display:flex;justify-content:center;margin-bottom:3px}
.funnel-bar{padding:.75rem 1.25rem;display:flex;justify-content:space-between;align-items:center;color:var(--bg);transition:width 1s cubic-bezier(.16,1,.3,1);width:0}
.funnel-bar.animated{width:var(--w)}
.funnel-label{font-weight:500;font-size:var(--text-sm);letter-spacing:.02em}
.funnel-metric{font-family:var(--font-mono);font-size:var(--text-xs);opacity:.8}

/* ---- MATRIX ---- */
.matrix-diagram{max-width:480px;margin:2.5rem auto;text-align:center}
.matrix-grid{display:grid;grid-template-columns:1fr 1fr;gap:2px;background:var(--ink-20)}
.matrix-cell{padding:1.5rem;text-align:center;background:var(--bg);transition:background .2s}
.matrix-cell:hover{background:var(--surface-warm)}
.matrix-cell strong{font-family:var(--font-mono);font-size:var(--text-sm);font-weight:700;display:block;margin-bottom:.5rem}
.matrix-cell p{font-size:var(--text-sm);color:var(--ink-60);margin:0;line-height:1.4}
.matrix-label{font-family:var(--font-mono);font-size:.6rem;color:var(--ink-60);text-transform:uppercase;letter-spacing:.12em;margin:1rem 0 .5rem}

/* ---- FLOW STEPS ---- */
.flow-steps{display:flex;align-items:stretch;gap:0;margin:2rem 0}
.flow-step{flex:1;padding:1.25rem;border:1px solid var(--ink-20);border-right:none;position:relative}
.flow-step:last-child{border-right:1px solid var(--ink-20)}
.flow-step-tag{font-family:var(--font-mono);font-size:.6rem;font-weight:700;text-transform:uppercase;letter-spacing:.1em;color:var(--accent);display:block;margin-bottom:.5rem}
.flow-step strong{display:block;font-size:var(--text-sm);font-weight:600;letter-spacing:.01em;margin-bottom:.25rem}
.flow-step-detail{font-size:var(--text-xs);color:var(--ink-60);line-height:1.4}
.flow-step::after{content:'→';position:absolute;right:-8px;top:50%;transform:translateY(-50%);font-size:1rem;color:var(--accent);z-index:1;background:var(--bg);padding:2px 0}
.flow-step:last-child::after{display:none}

/* ---- QUOTE ---- */
.quote-callout{border-left:3px solid var(--accent);padding:1.5rem 2rem;margin:2rem 0;background:var(--surface-warm)}
.quote-callout blockquote{font-size:var(--text-base);font-style:italic;line-height:1.7;margin:0}
.quote-callout cite{display:block;margin-top:.75rem;font-size:var(--text-xs);font-style:normal;font-family:var(--font-mono);text-transform:uppercase;letter-spacing:.05em;color:var(--ink-60)}

/* ---- TAKEAWAY ---- */
.takeaway-callout{display:flex;gap:1rem;padding:1.5rem;border:2px solid var(--accent);margin:2.5rem 0}
.takeaway-icon{font-size:1.25rem;flex-shrink:0;margin-top:2px}
.takeaway-title{font-family:var(--font-mono);font-size:.65rem;font-weight:700;text-transform:uppercase;letter-spacing:.12em;color:var(--accent);display:block;margin-bottom:.5rem}
.takeaway-callout p{font-size:var(--text-base);line-height:1.7;margin:0}

/* ---- STEP CARDS ---- */
.step-cards{display:flex;flex-direction:column;gap:0;margin:2rem 0;border:1px solid var(--ink-20)}
.step-card{display:flex;align-items:flex-start;gap:1.25rem;padding:1.25rem 1.5rem;border-bottom:1px solid var(--ink-10)}
.step-card:last-child{border-bottom:none}
.step-num{width:28px;height:28px;background:var(--ink);color:var(--bg);font-family:var(--font-mono);font-weight:700;font-size:var(--text-xs);display:flex;align-items:center;justify-content:center;flex-shrink:0}
.step-body strong{display:block;font-size:var(--text-sm);font-weight:600;letter-spacing:.01em}
.step-body p{margin:.25rem 0 0;color:var(--ink-60);font-size:var(--text-sm);line-height:1.5}

/* ---- QUIZ ---- */
.quiz-container{margin:2.5rem 0;padding:2rem;border:2px solid var(--ink)}
.quiz-header{font-family:var(--font-mono);font-size:var(--text-xs);font-weight:700;text-transform:uppercase;letter-spacing:.15em;margin-bottom:2rem;padding-bottom:.75rem;border-bottom:1px solid var(--ink-20)}
.quiz-question{font-size:var(--text-base);font-weight:500;margin-bottom:1.5rem;line-height:1.5}
.quiz-options{display:flex;flex-direction:column;gap:.5rem;margin-bottom:.5rem}
.quiz-option{display:flex;align-items:center;gap:.75rem;padding:.75rem 1rem;border:1.5px solid var(--ink-20);background:transparent;cursor:pointer;width:100%;font-family:var(--font-sans);font-size:var(--text-sm);text-align:left;transition:all .15s}
.quiz-option:hover{border-color:var(--ink-60)}
.quiz-option.selected{border-color:var(--accent);background:var(--surface-warm)}
.quiz-option.correct{border-color:var(--success);background:var(--surface-warm)}
.quiz-option.incorrect{border-color:var(--error);background:var(--surface-warm)}
.quiz-option-radio{width:14px;height:14px;border:1.5px solid var(--ink-20);flex-shrink:0;transition:all .15s}
.quiz-option.selected .quiz-option-radio{border-color:var(--accent);background:var(--accent);box-shadow:inset 0 0 0 2px var(--bg)}
.quiz-option.correct .quiz-option-radio{border-color:var(--success);background:var(--success);box-shadow:inset 0 0 0 2px var(--bg)}
.quiz-feedback{max-height:0;overflow:hidden;opacity:0;transition:max-height .3s,opacity .3s,padding .3s}
.quiz-feedback.show{max-height:300px;opacity:1;padding:.75rem 1rem;margin-top:.75rem;font-size:var(--text-sm);line-height:1.6}
.quiz-feedback.success{background:var(--surface-warm);color:var(--success);border-left:3px solid var(--success)}
.quiz-feedback.error{background:var(--surface-warm);color:var(--error);border-left:3px solid var(--error)}
.quiz-check-btn{margin-top:1.5rem;padding:.6rem 2rem;background:transparent;color:var(--ink);border:1.5px solid var(--ink);font-family:var(--font-mono);font-weight:700;font-size:var(--text-xs);text-transform:uppercase;letter-spacing:.1em;cursor:pointer;border-radius:99px;transition:all .2s}
.quiz-check-btn:hover{background:var(--ink);color:var(--bg)}
.scenario-context{background:var(--surface-warm);border-left:3px solid var(--accent);padding:1.25rem 1.5rem;margin-bottom:1.5rem}
.scenario-label{font-family:var(--font-mono);font-size:.6rem;font-weight:700;text-transform:uppercase;letter-spacing:.12em;color:var(--accent);display:block;margin-bottom:.5rem}

/* ---- GLOSSARY ---- */
.term{border-bottom:1.5px dashed var(--accent);cursor:pointer}
.term:hover{color:var(--accent)}
.term-tooltip{position:fixed;background:var(--ink);color:var(--bg);padding:.75rem 1rem;font-size:var(--text-sm);font-family:var(--font-sans);line-height:1.5;width:max(200px,min(300px,80vw));pointer-events:none;opacity:0;transition:opacity .15s;z-index:10000}
.term-tooltip::after{content:'';position:absolute;top:100%;left:50%;transform:translateX(-50%);border:5px solid transparent;border-top-color:var(--ink)}
.term-tooltip.visible{opacity:1}
.term-tooltip.flip::after{top:auto;bottom:100%;border-top-color:transparent;border-bottom-color:var(--ink)}

/* ---- ELMR / CHAIN ---- */
.elmr-chain{display:flex;align-items:stretch;gap:0;margin:2rem 0}
.elmr-step{flex:1;padding:1.5rem 1rem;border:2px solid var(--ink-20);text-align:center;position:relative;transition:all .4s;border-right:none}
.elmr-step:last-child{border-right:2px solid var(--ink-20)}
.elmr-step.lit{border-color:var(--accent);background:var(--surface-warm)}
.elmr-step .elmr-letter{font-family:var(--font-mono);font-size:var(--text-3xl);font-weight:700;color:var(--ink-20);transition:color .4s}
.elmr-step.lit .elmr-letter{color:var(--accent)}
.elmr-step .elmr-name{font-size:var(--text-xs);font-weight:600;letter-spacing:.03em;margin-top:.25rem}
.elmr-step .elmr-desc{font-size:var(--text-xs);color:var(--ink-60);margin-top:.5rem;line-height:1.4}
.elmr-step::after{content:'→';position:absolute;right:-9px;top:50%;transform:translateY(-50%);font-size:1rem;color:var(--ink-20);z-index:1;background:var(--bg);padding:2px 0;transition:color .4s}
.elmr-step:last-child::after{display:none}
.elmr-step.lit::after{color:var(--accent)}
.elmr-controls{text-align:center;margin-top:1.5rem}
.elmr-controls button{padding:.5rem 1.5rem;border:1.5px solid var(--ink);background:transparent;font-family:var(--font-mono);font-size:var(--text-xs);text-transform:uppercase;letter-spacing:.1em;cursor:pointer;border-radius:99px;margin:0 .25rem;transition:all .2s}
.elmr-controls button:hover{background:var(--ink);color:var(--bg)}

/* ---- WATERFALL ---- */
.waterfall-chart{margin:2.5rem 0}
.wf-row{display:flex;align-items:center;gap:1rem;margin-bottom:4px}
.wf-label{font-family:var(--font-mono);font-size:var(--text-xs);width:120px;text-align:right;flex-shrink:0;letter-spacing:.03em}
.wf-track{flex:1;height:32px;background:var(--ink-10);position:relative}
.wf-bar{height:100%;display:flex;align-items:center;padding:0 .75rem;color:var(--bg);font-family:var(--font-mono);font-size:var(--text-xs);font-weight:700;width:0;transition:width .8s cubic-bezier(.16,1,.3,1)}
.wf-bar.animated{width:var(--w)}

/* ---- CALCULATOR ---- */
.calc-container{margin:2.5rem 0;padding:2rem;border:2px solid var(--ink)}
.calc-title{font-family:var(--font-mono);font-size:var(--text-xs);font-weight:700;text-transform:uppercase;letter-spacing:.15em;margin-bottom:1.5rem;padding-bottom:.75rem;border-bottom:1px solid var(--ink-20)}
.calc-input{margin-bottom:1.25rem}
.calc-input label{display:block;font-size:var(--text-sm);margin-bottom:.5rem}
.calc-input label span{font-family:var(--font-mono);font-weight:700}
.calc-input input[type=range]{width:100%;accent-color:var(--accent);height:4px;-webkit-appearance:none;appearance:none;background:var(--ink-20);outline:none;border-radius:2px}
.calc-input input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;width:16px;height:16px;background:var(--accent);border-radius:0;cursor:pointer}
.calc-result{font-size:var(--text-2xl);font-weight:700;margin-top:1.5rem;padding-top:1rem;border-top:2px solid var(--ink)}
.calc-result-label{font-family:var(--font-mono);font-size:var(--text-xs);text-transform:uppercase;letter-spacing:.1em;color:var(--ink-60)}
.calc-result-value{font-family:var(--font-mono)}
.calc-threshold{font-family:var(--font-mono);font-size:var(--text-sm);margin-top:.5rem;transition:opacity .2s}

/* ---- CASCADE ---- */
.cascade-container{margin:2.5rem 0;padding:2rem;border:2px solid var(--ink)}
.cascade-bars{margin-top:1rem}
.cascade-row{display:flex;align-items:center;gap:.75rem;margin-bottom:3px}
.cascade-label{font-family:var(--font-mono);font-size:var(--text-xs);width:60px;text-align:right;flex-shrink:0;color:var(--ink-60)}
.cascade-track{flex:1;height:28px;background:var(--ink-10)}
.cascade-bar{height:100%;background:var(--accent);display:flex;align-items:center;padding:0 .75rem;color:var(--bg);font-family:var(--font-mono);font-size:var(--text-xs);font-weight:700;transition:width .5s}
.cascade-total{margin-top:1rem;padding-top:1rem;border-top:2px solid var(--ink);font-size:var(--text-base);font-family:var(--font-mono)}

/* ---- COMPLETION ---- */
.completion{text-align:center;padding:4rem 0;border-top:2px solid var(--ink);margin-top:3rem}
.completion h2{font-size:var(--text-3xl);font-weight:500;letter-spacing:.01em}
.completion p{font-size:var(--text-base);color:var(--ink-60);margin-top:1rem;max-width:50ch;margin-left:auto;margin-right:auto}

/* ---- RESPONSIVE ---- */
@media(max-width:768px){
  :root{--text-4xl:1.75rem;--text-3xl:1.5rem}
  .spotlight-block,.comparison-cards{grid-template-columns:1fr}
  .comparison-vs{text-align:center}
  .flow-steps,.elmr-chain{flex-direction:column}
  .flow-step{border-right:1px solid var(--ink-20);border-bottom:none}
  .flow-step:last-child{border-bottom:1px solid var(--ink-20)}
  .flow-step::after{display:none}
  .elmr-step{border-right:2px solid var(--ink-20);border-bottom:none}
  .elmr-step:last-child{border-bottom:2px solid var(--ink-20)}
  .elmr-step::after{display:none}
  .wf-label{width:80px;font-size:.6rem}
}
@media(max-width:480px){
  .module{padding:3rem 1.25rem}
  .concept-cards{grid-template-columns:1fr}
}
```

## Color Adaptation

Default accent is deep purple (`#6C4AB6`). To adapt per content personality, change these three values:

| Content type | Accent | Light | Dark |
|---|---|---|---|
| Business / Finance | `#6C4AB6` | `#EDE8F5` | `#4a337e` |
| Science / Tech | `#2A7B9B` | `#E4F2F7` | `#1D5A73` |
| Creative / Arts | `#D94F30` | `#FDEEE9` | `#C4432A` |
| Nature / Health | `#2D8B55` | `#E8F5EE` | `#1E6B3E` |
| Strategy / Ops | `#D4A843` | `#FBF3E0` | `#B08C2F` |

## Typography Rules

- **Module titles**: `--text-4xl`, weight 500, title case. No uppercase.
- **Screen headings**: `--text-xl`, weight 500, sentence case. No uppercase.
- **Body text**: `--text-base`, line-height 1.7, max 60ch.
- **Mono labels** (module numbers, step tags, quiz headers): `--text-xs`, uppercase, letter-spacing 0.1em+. These are the ONLY elements that may be uppercase.
- **Concept card titles**: `--text-xs`, mono, weight 700. No forced uppercase; acronyms are naturally uppercase in HTML.

## Alternating Module Backgrounds

Even modules: `var(--bg)` (`#E4DFD0`)
Odd modules: `var(--surface-warm)` (`#F0EDE4`)

Apply via inline style on the `<section>`:
```html
<section class="module" id="module-2" style="background:var(--surface-warm)">
```
