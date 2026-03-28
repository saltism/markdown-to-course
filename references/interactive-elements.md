# Interactive Elements Reference

Implementation patterns for every interactive element type used in markdown-to-course. Pick the elements that best serve each module's teaching goal.

## Table of Contents
1. [Concept Spotlight Blocks](#concept-spotlight-blocks)
2. [Multiple-Choice Quizzes](#multiple-choice-quizzes)
3. [Scenario Quizzes](#scenario-quizzes)
4. [Drag-and-Drop Matching](#drag-and-drop-matching)
5. [Framework Diagram — Loop](#framework-diagram--loop)
6. [Framework Diagram — Funnel](#framework-diagram--funnel)
7. [Framework Diagram — Matrix (2×2)](#framework-diagram--matrix-2x2)
8. [Flow Diagrams](#flow-diagrams)
9. [Comparison Cards](#comparison-cards)
10. [Data Highlight Cards](#data-highlight-cards)
11. [Quote Callouts](#quote-callouts)
12. [Key Takeaway Callouts](#key-takeaway-callouts)
13. [Concept/Pattern Cards](#conceptpattern-cards)
14. [Numbered Step Cards](#numbered-step-cards)
15. [Glossary Tooltips](#glossary-tooltips)
16. [Animated Process Flow](#animated-process-flow)

---

## Concept Spotlight Blocks

The signature teaching element. Highlights a key concept or framework with visual emphasis, a plain-language explanation, and a concrete example. This replaces codebase-to-course's "Code ↔ English Translation" as the primary comprehension tool.

**HTML:**
```html
<div class="spotlight-block animate-in">
  <div class="spotlight-concept">
    <span class="spotlight-label">KEY CONCEPT</span>
    <h3 class="spotlight-term">Contribution Margin</h3>
    <div class="spotlight-icon">💰</div>
  </div>
  <div class="spotlight-explanation">
    <span class="spotlight-label">IN PLAIN LANGUAGE</span>
    <p class="spotlight-text">How much money you keep from each sale after covering the direct costs of making that sale — including marketing spend. It answers: "If we sell one more unit, how much richer are we?"</p>
    <div class="spotlight-example">
      <span class="spotlight-example-label">Example</span>
      <p>You sell a subscription for $100/month. It costs $5 in server hosting and $40 in ads to acquire that customer. Your contribution margin is $55 — the money left to cover salaries, rent, and profit.</p>
    </div>
  </div>
</div>
```

**CSS:**
```css
.spotlight-block {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 0;
  border-radius: var(--radius-md);
  overflow: hidden;
  box-shadow: var(--shadow-md);
  margin: var(--space-8) 0;
}
.spotlight-concept {
  background: var(--color-bg-code);
  color: #CDD6F4;
  padding: var(--space-8) var(--space-6);
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
}
.spotlight-term {
  font-family: var(--font-display);
  font-size: var(--text-2xl);
  font-weight: 700;
  color: #FFFFFF;
  margin: var(--space-2) 0;
  line-height: var(--leading-tight);
}
.spotlight-icon {
  font-size: 2rem;
  margin-top: var(--space-4);
  opacity: 0.7;
}
.spotlight-explanation {
  background: var(--color-surface-warm);
  padding: var(--space-6);
  border-left: 3px solid var(--color-accent);
  position: relative;
}
.spotlight-label {
  font-size: var(--text-xs);
  font-family: var(--font-mono);
  text-transform: uppercase;
  letter-spacing: 0.1em;
  opacity: 0.5;
  display: block;
  margin-bottom: var(--space-2);
}
.spotlight-text {
  font-size: var(--text-base);
  line-height: var(--leading-normal);
  color: var(--color-text);
  margin-bottom: var(--space-4);
}
.spotlight-example {
  background: var(--color-accent-light);
  border-radius: var(--radius-sm);
  padding: var(--space-3) var(--space-4);
}
.spotlight-example-label {
  font-size: var(--text-xs);
  font-weight: 600;
  color: var(--color-accent);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
.spotlight-example p {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  margin-top: var(--space-1);
}

@media (max-width: 768px) {
  .spotlight-block { grid-template-columns: 1fr; }
  .spotlight-concept { padding: var(--space-6) var(--space-4); }
  .spotlight-explanation { border-left: none; border-top: 3px solid var(--color-accent); }
}
```

**Rules:**
- Use for every major concept, framework, or term that the reader must understand to progress
- The explanation should be conversational — imagine explaining it to a smart friend over coffee
- The example should be concrete and specific, ideally from the source material
- One Concept Spotlight per screen maximum — they're meant to stand out

---

## Multiple-Choice Quizzes

For testing understanding with instant feedback. Each question has options, one correct answer, and per-question explanations.

**HTML:**
```html
<div class="quiz-container">
  <div class="quiz-question-block" data-question="q1" data-correct="option-b">
    <h3 class="quiz-question">A SaaS company has 80% gross margin but is losing money. Based on what you learned, which cost area is most likely the problem?</h3>
    <div class="quiz-options">
      <button class="quiz-option" data-value="option-a" onclick="selectOption(this)">
        <div class="quiz-option-radio"></div>
        <span>Cost of goods sold (COGS)</span>
      </button>
      <button class="quiz-option" data-value="option-b" onclick="selectOption(this)">
        <div class="quiz-option-radio"></div>
        <span>Sales & marketing (SG&A)</span>
      </button>
      <button class="quiz-option" data-value="option-c" onclick="selectOption(this)">
        <div class="quiz-option-radio"></div>
        <span>Server infrastructure costs</span>
      </button>
    </div>
    <div class="quiz-feedback" id="q1-feedback"
         data-correct-text="Exactly. With 80% gross margin, COGS isn't the issue — the company keeps $0.80 of every dollar after direct costs. The bleed is likely in customer acquisition or sales team expenses."
         data-incorrect-text="Not quite. With 80% gross margin, direct costs are well controlled. The money is disappearing somewhere between gross margin and the bottom line — likely in how much they're spending to acquire and support customers.">
    </div>
  </div>

  <button class="quiz-check-btn" onclick="checkQuiz(this)">Check answer</button>
</div>
```

**JS pattern:**
```javascript
window.selectOption = function(btn) {
  const block = btn.closest('.quiz-question-block');
  block.querySelectorAll('.quiz-option').forEach(o => o.classList.remove('selected'));
  btn.classList.add('selected');
};

window.checkQuiz = function(btn) {
  const container = btn.closest('.quiz-container');
  const questions = container.querySelectorAll('.quiz-question-block');

  questions.forEach(q => {
    const selected = q.querySelector('.quiz-option.selected');
    const feedback = q.querySelector('.quiz-feedback');
    const correctValue = q.dataset.correct;

    if (!selected) {
      feedback.textContent = 'Pick an answer first.';
      feedback.className = 'quiz-feedback show warning';
      return;
    }

    if (selected.dataset.value === correctValue) {
      selected.classList.add('correct');
      feedback.innerHTML = '<strong>Correct.</strong> ' + feedback.dataset.correctText;
      feedback.className = 'quiz-feedback show success';
    } else {
      selected.classList.add('incorrect');
      q.querySelector(`[data-value="${correctValue}"]`).classList.add('correct');
      feedback.innerHTML = '<strong>Not quite.</strong> ' + feedback.dataset.incorrectText;
      feedback.className = 'quiz-feedback show error';
    }

    q.querySelectorAll('.quiz-option').forEach(o => o.disabled = true);
  });
};
```

**CSS:**
```css
.quiz-option {
  display: flex; align-items: center; gap: var(--space-3);
  padding: var(--space-3) var(--space-4);
  border: 2px solid var(--color-border);
  border-radius: var(--radius-sm);
  background: var(--color-surface);
  cursor: pointer; width: 100%;
  font-family: var(--font-body);
  font-size: var(--text-base);
  text-align: left;
  transition: border-color var(--duration-fast), background var(--duration-fast);
  margin-bottom: var(--space-2);
}
.quiz-option:hover { border-color: var(--color-accent-muted); }
.quiz-option.selected { border-color: var(--color-accent); background: var(--color-accent-light); }
.quiz-option.correct { border-color: var(--color-success); background: var(--color-success-light); }
.quiz-option.incorrect { border-color: var(--color-error); background: var(--color-error-light); }
.quiz-option-radio {
  width: 18px; height: 18px; border-radius: 50%;
  border: 2px solid var(--color-border);
  flex-shrink: 0;
  transition: all var(--duration-fast);
}
.quiz-option.selected .quiz-option-radio {
  border-color: var(--color-accent);
  background: var(--color-accent);
  box-shadow: inset 0 0 0 3px white;
}
.quiz-feedback {
  max-height: 0; overflow: hidden; opacity: 0;
  transition: max-height var(--duration-normal), opacity var(--duration-normal);
}
.quiz-feedback.show {
  max-height: 200px; opacity: 1;
  padding: var(--space-3) var(--space-4);
  margin-top: var(--space-3);
  border-radius: var(--radius-sm);
  font-size: var(--text-sm);
  line-height: var(--leading-normal);
}
.quiz-feedback.success { background: var(--color-success-light); color: var(--color-success); }
.quiz-feedback.error { background: var(--color-error-light); color: var(--color-error); }
.quiz-feedback.warning { background: var(--color-info-light); color: var(--color-info); }
.quiz-check-btn {
  margin-top: var(--space-4);
  padding: var(--space-2) var(--space-6);
  background: var(--color-accent);
  color: white;
  border: none;
  border-radius: var(--radius-sm);
  font-family: var(--font-body);
  font-weight: 600;
  cursor: pointer;
  transition: background var(--duration-fast);
}
.quiz-check-btn:hover { background: var(--color-accent-hover); }
```

---

## Scenario Quizzes

Extended version of multiple-choice with a situational context block. Tests application, not recall.

```html
<div class="scenario-block">
  <div class="scenario-context">
    <span class="scenario-label">📋 Scenario</span>
    <p>You're the growth lead at a SaaS startup. Monthly revenue is $500K with 78% gross margin, but you're burning $200K/month. The CEO asks you to cut spend. You discover 60% of SG&A goes to a paid ads channel with $180 CAC but only $120 first-year LTV.</p>
  </div>
  <div class="quiz-question-block" data-question="scenario-1" data-correct="option-b">
    <h3 class="quiz-question">What's your first move?</h3>
    <!-- quiz-options here, same pattern as multiple-choice -->
  </div>
</div>
```

```css
.scenario-context {
  background: var(--color-info-light);
  border-left: 3px solid var(--color-info);
  border-radius: var(--radius-sm);
  padding: var(--space-4) var(--space-5);
  margin-bottom: var(--space-4);
}
.scenario-label {
  font-size: var(--text-xs);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: var(--color-info);
  display: block;
  margin-bottom: var(--space-2);
}
.scenario-context p {
  font-size: var(--text-base);
  line-height: var(--leading-normal);
  color: var(--color-text);
}
```

---

## Drag-and-Drop Matching

For matching concepts to descriptions or categories. Mouse + touch support.

**HTML:**
```html
<div class="dnd-container">
  <p class="dnd-instruction">Match each margin type to its definition:</p>
  <div class="dnd-chips">
    <div class="dnd-chip" draggable="true" data-answer="gross">Gross Margin</div>
    <div class="dnd-chip" draggable="true" data-answer="contribution">Contribution Margin</div>
    <div class="dnd-chip" draggable="true" data-answer="net">Net Margin</div>
  </div>
  <div class="dnd-zones">
    <div class="dnd-zone" data-correct="gross">
      <p class="dnd-zone-label">Revenue minus cost of goods sold</p>
      <div class="dnd-zone-target">Drop here</div>
    </div>
    <div class="dnd-zone" data-correct="contribution">
      <p class="dnd-zone-label">Revenue minus COGS and sales/marketing</p>
      <div class="dnd-zone-target">Drop here</div>
    </div>
    <div class="dnd-zone" data-correct="net">
      <p class="dnd-zone-label">Revenue minus all expenses including taxes</p>
      <div class="dnd-zone-target">Drop here</div>
    </div>
  </div>
  <button class="quiz-check-btn" onclick="checkDnD(this)">Check matches</button>
  <button class="quiz-reset-btn" onclick="resetDnD(this)" style="display:none">Try again</button>
</div>
```

**JS (mouse + touch):**
```javascript
document.querySelectorAll('.dnd-chip').forEach(chip => {
  chip.addEventListener('dragstart', (e) => {
    e.dataTransfer.setData('text/plain', chip.dataset.answer);
    chip.classList.add('dragging');
  });
  chip.addEventListener('dragend', () => chip.classList.remove('dragging'));
});

document.querySelectorAll('.dnd-zone-target').forEach(target => {
  target.addEventListener('dragover', (e) => { e.preventDefault(); target.classList.add('drag-over'); });
  target.addEventListener('dragleave', () => target.classList.remove('drag-over'));
  target.addEventListener('drop', (e) => {
    e.preventDefault();
    target.classList.remove('drag-over');
    const answer = e.dataTransfer.getData('text/plain');
    const chip = document.querySelector(`[data-answer="${answer}"]`);
    target.textContent = chip.textContent;
    target.dataset.placed = answer;
    chip.classList.add('placed');
  });
});

// Touch support (HTML5 drag doesn't work on mobile)
document.querySelectorAll('.dnd-chip').forEach(chip => {
  chip.addEventListener('touchstart', (e) => {
    e.preventDefault();
    const touch = e.touches[0];
    const clone = chip.cloneNode(true);
    clone.classList.add('touch-ghost');
    clone.style.cssText = `position:fixed;z-index:1000;pointer-events:none;
      left:${touch.clientX-40}px;top:${touch.clientY-20}px;`;
    document.body.appendChild(clone);
    chip._ghost = clone;
    chip._answer = chip.dataset.answer;
  }, { passive: false });

  chip.addEventListener('touchmove', (e) => {
    e.preventDefault();
    const touch = e.touches[0];
    if (chip._ghost) {
      chip._ghost.style.left = (touch.clientX - 40) + 'px';
      chip._ghost.style.top = (touch.clientY - 20) + 'px';
    }
    document.querySelectorAll('.dnd-zone-target').forEach(z => z.classList.remove('drag-over'));
    const el = document.elementFromPoint(touch.clientX, touch.clientY);
    if (el && el.closest('.dnd-zone-target')) el.closest('.dnd-zone-target').classList.add('drag-over');
  }, { passive: false });

  chip.addEventListener('touchend', (e) => {
    if (chip._ghost) { chip._ghost.remove(); chip._ghost = null; }
    const touch = e.changedTouches[0];
    const el = document.elementFromPoint(touch.clientX, touch.clientY);
    if (el && el.closest('.dnd-zone-target')) {
      const target = el.closest('.dnd-zone-target');
      target.textContent = chip.textContent;
      target.dataset.placed = chip._answer;
      chip.classList.add('placed');
    }
  });
});
```

**CSS:**
```css
.dnd-chips { display: flex; flex-wrap: wrap; gap: var(--space-2); margin-bottom: var(--space-4); }
.dnd-chip {
  padding: var(--space-2) var(--space-4);
  background: var(--color-accent);
  color: white;
  border-radius: var(--radius-full);
  font-weight: 600;
  font-size: var(--text-sm);
  cursor: grab;
  transition: opacity var(--duration-fast), transform var(--duration-fast);
}
.dnd-chip.dragging { opacity: 0.5; }
.dnd-chip.placed { opacity: 0.3; pointer-events: none; }
.dnd-zone { margin-bottom: var(--space-3); }
.dnd-zone-label { font-size: var(--text-sm); color: var(--color-text-secondary); margin-bottom: var(--space-1); }
.dnd-zone-target {
  border: 2px dashed var(--color-border);
  border-radius: var(--radius-sm);
  padding: var(--space-3) var(--space-4);
  min-height: 44px;
  display: flex;
  align-items: center;
  color: var(--color-text-muted);
  font-size: var(--text-sm);
  transition: border-color var(--duration-fast), background var(--duration-fast);
}
.dnd-zone-target.drag-over { border-color: var(--color-accent); background: var(--color-accent-light); }
.dnd-zone-target.correct { border-color: var(--color-success); background: var(--color-success-light); color: var(--color-success); border-style: solid; }
.dnd-zone-target.incorrect { border-color: var(--color-error); background: var(--color-error-light); color: var(--color-error); border-style: solid; }
```

---

## Framework Diagram — Loop

For visualizing growth loops, feedback loops, or any cyclical process from the source content.

**HTML:**
```html
<div class="loop-diagram animate-in">
  <div class="loop-title">Habit Loop</div>
  <div class="loop-ring">
    <div class="loop-node" style="--angle: 0deg; --color: var(--color-topic-1)">
      <div class="loop-node-icon">⚡</div>
      <div class="loop-node-label">Trigger</div>
      <div class="loop-node-desc">External cue prompts action</div>
    </div>
    <div class="loop-arrow" style="--angle: 60deg">→</div>
    <div class="loop-node" style="--angle: 120deg; --color: var(--color-topic-2)">
      <div class="loop-node-icon">🎯</div>
      <div class="loop-node-label">Action</div>
      <div class="loop-node-desc">User performs desired behavior</div>
    </div>
    <div class="loop-arrow" style="--angle: 180deg">→</div>
    <div class="loop-node" style="--angle: 240deg; --color: var(--color-topic-3)">
      <div class="loop-node-icon">🎁</div>
      <div class="loop-node-label">Reward</div>
      <div class="loop-node-desc">Positive outcome reinforces habit</div>
    </div>
    <div class="loop-arrow" style="--angle: 300deg">↩</div>
  </div>
</div>
```

**CSS:**
```css
.loop-diagram {
  text-align: center;
  padding: var(--space-8);
  margin: var(--space-8) 0;
}
.loop-title {
  font-family: var(--font-display);
  font-size: var(--text-2xl);
  font-weight: 700;
  margin-bottom: var(--space-8);
}
.loop-ring {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: var(--space-4);
  flex-wrap: wrap;
  max-width: 700px;
  margin: 0 auto;
}
.loop-node {
  background: var(--color-surface);
  border-radius: var(--radius-md);
  padding: var(--space-5);
  box-shadow: var(--shadow-md);
  border-top: 4px solid var(--color);
  width: 160px;
  text-align: center;
}
.loop-node-icon { font-size: 1.5rem; margin-bottom: var(--space-2); }
.loop-node-label { font-family: var(--font-display); font-weight: 700; font-size: var(--text-base); }
.loop-node-desc { font-size: var(--text-xs); color: var(--color-text-secondary); margin-top: var(--space-1); }
.loop-arrow {
  font-size: var(--text-2xl);
  color: var(--color-accent);
  font-weight: 700;
}
```

---

## Framework Diagram — Funnel

For visualizing conversion funnels, marketing funnels, or any narrowing process.

**HTML:**
```html
<div class="funnel-diagram animate-in">
  <div class="funnel-stage" style="--width: 100%; --color: var(--color-topic-1)">
    <div class="funnel-bar">
      <span class="funnel-label">Awareness</span>
      <span class="funnel-metric">100K visitors</span>
    </div>
  </div>
  <div class="funnel-stage" style="--width: 60%; --color: var(--color-topic-2)">
    <div class="funnel-bar">
      <span class="funnel-label">Sign-up</span>
      <span class="funnel-metric">12K (12%)</span>
    </div>
  </div>
  <div class="funnel-stage" style="--width: 30%; --color: var(--color-topic-3)">
    <div class="funnel-bar">
      <span class="funnel-label">Activation</span>
      <span class="funnel-metric">3.6K (30%)</span>
    </div>
  </div>
  <div class="funnel-stage" style="--width: 15%; --color: var(--color-topic-5)">
    <div class="funnel-bar">
      <span class="funnel-label">Paid</span>
      <span class="funnel-metric">540 (15%)</span>
    </div>
  </div>
</div>
```

**CSS:**
```css
.funnel-diagram {
  max-width: 600px;
  margin: var(--space-8) auto;
}
.funnel-stage {
  display: flex;
  justify-content: center;
  margin-bottom: var(--space-2);
}
.funnel-bar {
  width: var(--width);
  background: var(--color);
  color: white;
  padding: var(--space-3) var(--space-4);
  border-radius: var(--radius-sm);
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: width var(--duration-slow) var(--ease-out);
}
.funnel-label { font-weight: 600; font-size: var(--text-sm); }
.funnel-metric { font-family: var(--font-mono); font-size: var(--text-xs); opacity: 0.9; }
```

---

## Framework Diagram — Matrix (2×2)

For any 2×2 framework (BCG matrix, Eisenhower matrix, etc.).

**HTML:**
```html
<div class="matrix-diagram animate-in">
  <div class="matrix-y-label">High Margin →</div>
  <div class="matrix-grid">
    <div class="matrix-cell" style="background: var(--color-success-light)">
      <strong>Stars</strong>
      <p>High growth, high margin — invest heavily</p>
    </div>
    <div class="matrix-cell" style="background: var(--color-info-light)">
      <strong>Question Marks</strong>
      <p>High growth, low margin — decide fast</p>
    </div>
    <div class="matrix-cell" style="background: var(--color-accent-light)">
      <strong>Cash Cows</strong>
      <p>Low growth, high margin — harvest</p>
    </div>
    <div class="matrix-cell" style="background: var(--color-error-light)">
      <strong>Dogs</strong>
      <p>Low growth, low margin — divest</p>
    </div>
  </div>
  <div class="matrix-x-label">← Low Growth &nbsp;&nbsp;&nbsp; High Growth →</div>
</div>
```

**CSS:**
```css
.matrix-diagram { max-width: 500px; margin: var(--space-8) auto; text-align: center; }
.matrix-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-2);
}
.matrix-cell {
  padding: var(--space-5);
  border-radius: var(--radius-md);
  text-align: center;
}
.matrix-cell strong { font-family: var(--font-display); font-size: var(--text-base); display: block; margin-bottom: var(--space-1); }
.matrix-cell p { font-size: var(--text-sm); color: var(--color-text-secondary); }
.matrix-y-label, .matrix-x-label {
  font-size: var(--text-xs);
  color: var(--color-text-muted);
  font-family: var(--font-mono);
  text-transform: uppercase;
  letter-spacing: 0.05em;
}
.matrix-y-label { margin-bottom: var(--space-2); }
.matrix-x-label { margin-top: var(--space-2); }
```

---

## Flow Diagrams

Horizontal step-by-step flow. Arrows rotate to vertical on mobile.

```html
<div class="flow-steps animate-in">
  <div class="flow-step">
    <div class="flow-step-num">1</div>
    <p><strong>Trigger occurs</strong></p>
    <p class="flow-step-detail">User sees ad, friend shares, need arises</p>
  </div>
  <div class="flow-arrow">→</div>
  <div class="flow-step">
    <div class="flow-step-num">2</div>
    <p><strong>User takes action</strong></p>
    <p class="flow-step-detail">Signs up, downloads, makes first purchase</p>
  </div>
  <div class="flow-arrow">→</div>
  <div class="flow-step">
    <div class="flow-step-num">3</div>
    <p><strong>Reward delivered</strong></p>
    <p class="flow-step-detail">Value experienced, problem solved, delight</p>
  </div>
</div>
```

```css
.flow-steps {
  display: flex;
  align-items: center;
  gap: var(--space-3);
  margin: var(--space-6) 0;
  flex-wrap: wrap;
  justify-content: center;
}
.flow-step {
  background: var(--color-surface);
  border-radius: var(--radius-md);
  padding: var(--space-4) var(--space-5);
  box-shadow: var(--shadow-sm);
  border-left: 3px solid var(--color-accent);
  flex: 1;
  min-width: 150px;
}
.flow-step-num {
  width: 28px; height: 28px; border-radius: 50%;
  background: var(--color-accent); color: white;
  font-weight: 700; font-family: var(--font-display);
  display: flex; align-items: center; justify-content: center;
  font-size: var(--text-sm);
  margin-bottom: var(--space-2);
}
.flow-step-detail { font-size: var(--text-xs); color: var(--color-text-secondary); margin-top: var(--space-1); }
.flow-arrow { font-size: var(--text-xl); color: var(--color-accent); font-weight: 700; }

@media (max-width: 480px) {
  .flow-steps { flex-direction: column; }
  .flow-arrow { transform: rotate(90deg); }
}
```

---

## Comparison Cards

Side-by-side cards for contrasting two concepts, approaches, or states.

```html
<div class="comparison-cards animate-in">
  <div class="comparison-card comparison-a">
    <span class="comparison-label" style="background: var(--color-error)">Low Margin</span>
    <h4>Physical Retail</h4>
    <ul>
      <li>10–20% gross margin</li>
      <li>Priority: optimize supply chain</li>
      <li>Growth team ROI is harder to justify</li>
    </ul>
  </div>
  <div class="comparison-vs">vs</div>
  <div class="comparison-card comparison-b">
    <span class="comparison-label" style="background: var(--color-success)">High Margin</span>
    <h4>SaaS</h4>
    <ul>
      <li>70–90% gross margin</li>
      <li>Priority: acquire and retain customers</li>
      <li>Growth team is a core investment</li>
    </ul>
  </div>
</div>
```

```css
.comparison-cards {
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  gap: var(--space-4);
  align-items: start;
  margin: var(--space-6) 0;
}
.comparison-card {
  background: var(--color-surface);
  border-radius: var(--radius-md);
  padding: var(--space-5);
  box-shadow: var(--shadow-sm);
}
.comparison-label {
  display: inline-block;
  color: white;
  font-size: var(--text-xs);
  font-weight: 700;
  padding: var(--space-1) var(--space-3);
  border-radius: var(--radius-full);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: var(--space-3);
}
.comparison-card h4 { font-family: var(--font-display); font-size: var(--text-lg); margin-bottom: var(--space-3); }
.comparison-card ul { list-style: none; padding: 0; }
.comparison-card li {
  font-size: var(--text-sm);
  color: var(--color-text-secondary);
  padding: var(--space-2) 0;
  border-bottom: 1px solid var(--color-border-light);
}
.comparison-card li:last-child { border: none; }
.comparison-vs {
  font-family: var(--font-display);
  font-weight: 800;
  font-size: var(--text-xl);
  color: var(--color-text-muted);
  align-self: center;
}

@media (max-width: 768px) {
  .comparison-cards { grid-template-columns: 1fr; }
  .comparison-vs { text-align: center; }
}
```

---

## Data Highlight Cards

For making statistics and metrics from the source pop visually.

```html
<div class="data-highlights animate-in stagger-children">
  <div class="data-card animate-in" style="border-top: 3px solid var(--color-topic-1)">
    <span class="data-value">50%</span>
    <span class="data-label">Minimum gross margin</span>
    <p class="data-context">The floor for physical product businesses to be viable</p>
  </div>
  <div class="data-card animate-in" style="border-top: 3px solid var(--color-topic-2)">
    <span class="data-value">$0</span>
    <span class="data-label">Marginal cost of software</span>
    <p class="data-context">Why SaaS margins can reach 80–90%</p>
  </div>
  <div class="data-card animate-in" style="border-top: 3px solid var(--color-topic-5)">
    <span class="data-value">3:1</span>
    <span class="data-label">Healthy LTV:CAC ratio</span>
    <p class="data-context">Below this, acquisition economics don't work</p>
  </div>
</div>
```

```css
.data-highlights {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: var(--space-4);
  margin: var(--space-6) 0;
}
.data-card {
  background: var(--color-surface);
  border-radius: var(--radius-md);
  padding: var(--space-5);
  box-shadow: var(--shadow-sm);
  text-align: center;
}
.data-value {
  font-family: var(--font-mono);
  font-size: var(--text-3xl);
  font-weight: 700;
  color: var(--color-text);
  display: block;
}
.data-label {
  font-size: var(--text-sm);
  font-weight: 600;
  color: var(--color-text);
  display: block;
  margin-top: var(--space-2);
}
.data-context {
  font-size: var(--text-xs);
  color: var(--color-text-secondary);
  margin-top: var(--space-1);
}
```

---

## Quote Callouts

For expert quotes or notable statements from the source material.

```html
<div class="quote-callout animate-in">
  <blockquote>
    "If you define open and click rates as your performance metric, that might lead you to send even more emails without considering the tradeoffs, like unsubscribe rates."
  </blockquote>
  <cite>— Stephanie Kwok, EIR at Reforge</cite>
</div>
```

```css
.quote-callout {
  border-left: 4px solid var(--color-accent);
  padding: var(--space-6);
  margin: var(--space-6) 0;
  background: var(--color-surface-warm);
  border-radius: 0 var(--radius-md) var(--radius-md) 0;
}
.quote-callout blockquote {
  font-family: var(--font-display);
  font-size: var(--text-lg);
  font-weight: 500;
  font-style: italic;
  line-height: var(--leading-normal);
  color: var(--color-text);
  margin: 0;
}
.quote-callout cite {
  display: block;
  margin-top: var(--space-3);
  font-size: var(--text-sm);
  font-style: normal;
  color: var(--color-text-muted);
}
```

---

## Key Takeaway Callouts

One per module, placed at the end. Summarizes the module's core insight.

```html
<div class="takeaway-callout animate-in">
  <div class="takeaway-icon">🔑</div>
  <div class="takeaway-content">
    <strong class="takeaway-title">Key Takeaway</strong>
    <p>At a high-margin business, the growth team is a core investment, not a luxury. The more margin you have above COGS, the more room you have to spend on acquisition — and the more a growth team's work directly impacts the bottom line.</p>
  </div>
</div>
```

```css
.takeaway-callout {
  display: flex;
  gap: var(--space-4);
  padding: var(--space-5);
  background: var(--color-accent-light);
  border: 2px solid var(--color-accent);
  border-radius: var(--radius-md);
  margin: var(--space-8) 0;
}
.takeaway-icon { font-size: 1.5rem; flex-shrink: 0; }
.takeaway-title {
  font-family: var(--font-display);
  font-size: var(--text-base);
  color: var(--color-accent);
  display: block;
  margin-bottom: var(--space-1);
}
.takeaway-callout p {
  font-size: var(--text-base);
  line-height: var(--leading-normal);
  color: var(--color-text);
  margin: 0;
}
```

---

## Concept/Pattern Cards

Grid of cards for related concepts, features, or categories.

```html
<div class="concept-cards animate-in stagger-children">
  <div class="concept-card animate-in" style="border-top: 3px solid var(--color-topic-1)">
    <div class="concept-icon" style="background: var(--color-topic-1)">📈</div>
    <h4 class="concept-title">Acquisition Loops</h4>
    <p class="concept-desc">Channels that bring new users: paid ads, SEO, referrals, content marketing.</p>
  </div>
  <div class="concept-card animate-in" style="border-top: 3px solid var(--color-topic-2)">
    <div class="concept-icon" style="background: var(--color-topic-2)">🔄</div>
    <h4 class="concept-title">Retention Loops</h4>
    <p class="concept-desc">Mechanisms that keep users coming back: habits, notifications, social connections.</p>
  </div>
  <div class="concept-card animate-in" style="border-top: 3px solid var(--color-topic-3)">
    <div class="concept-icon" style="background: var(--color-topic-3)">💰</div>
    <h4 class="concept-title">Monetization Loops</h4>
    <p class="concept-desc">Patterns that extract value: upsells, usage-based pricing, network effects.</p>
  </div>
</div>
```

```css
.concept-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: var(--space-4);
  margin: var(--space-6) 0;
}
.concept-card {
  background: var(--color-surface);
  border-radius: var(--radius-md);
  padding: var(--space-5);
  box-shadow: var(--shadow-sm);
  transition: transform var(--duration-normal) var(--ease-out), box-shadow var(--duration-normal);
}
.concept-card:hover {
  transform: translateY(-4px);
  box-shadow: var(--shadow-md);
}
.concept-icon {
  width: 40px; height: 40px; border-radius: var(--radius-sm);
  display: flex; align-items: center; justify-content: center;
  font-size: 1.25rem; margin-bottom: var(--space-3);
}
.concept-title { font-family: var(--font-display); font-size: var(--text-base); font-weight: 700; margin-bottom: var(--space-2); }
.concept-desc { font-size: var(--text-sm); color: var(--color-text-secondary); line-height: var(--leading-normal); }
```

---

## Numbered Step Cards

For sequential processes.

```html
<div class="step-cards animate-in stagger-children">
  <div class="step-card animate-in">
    <div class="step-num">1</div>
    <div class="step-body">
      <strong>Define your growth model</strong>
      <p>Identify the core loop that drives your product's growth</p>
    </div>
  </div>
  <div class="step-card animate-in">
    <div class="step-num">2</div>
    <div class="step-body">
      <strong>Map input metrics to the loop</strong>
      <p>Break the loop into measurable stages</p>
    </div>
  </div>
  <div class="step-card animate-in">
    <div class="step-num">3</div>
    <div class="step-body">
      <strong>Build audience strategies per stage</strong>
      <p>Create targeted approaches for each segment at each loop stage</p>
    </div>
  </div>
</div>
```

```css
.step-cards { display: flex; flex-direction: column; gap: var(--space-3); margin: var(--space-6) 0; }
.step-card {
  display: flex; align-items: flex-start; gap: var(--space-4);
  padding: var(--space-4) var(--space-5);
  background: var(--color-surface);
  border-radius: var(--radius-md);
  border-left: 3px solid var(--color-accent);
  box-shadow: var(--shadow-sm);
}
.step-num {
  width: 32px; height: 32px; border-radius: 50%;
  background: var(--color-accent); color: white;
  font-weight: 700; font-family: var(--font-display);
  display: flex; align-items: center; justify-content: center;
  flex-shrink: 0;
}
.step-body strong { display: block; font-family: var(--font-display); }
.step-body p { margin: var(--space-1) 0 0; color: var(--color-text-secondary); font-size: var(--text-sm); }
```

---

## Glossary Tooltips

Every domain-specific term gets a dashed-underline tooltip on first use per module.

**HTML — inline markup:**
```html
<p>Understanding your
  <span class="term" data-definition="CAC (Customer Acquisition Cost) — the total you spend to get one new paying customer. Include ad spend, sales salaries, tools, and any other cost directly tied to winning that customer. If your CAC is $200, you need each customer to generate at least $200 in lifetime value just to break even on acquiring them.">CAC</span>
  is the first step to evaluating channel economics.
</p>
```

**CSS:**
```css
.term {
  border-bottom: 1.5px dashed var(--color-accent-muted);
  cursor: pointer;
  position: relative;
}
.term:hover, .term.active {
  border-bottom-color: var(--color-accent);
  color: var(--color-accent);
}

.term-tooltip {
  position: fixed;
  background: var(--color-bg-code);
  color: #CDD6F4;
  padding: var(--space-3) var(--space-4);
  border-radius: var(--radius-sm);
  font-size: var(--text-sm);
  font-family: var(--font-body);
  line-height: var(--leading-normal);
  width: max(200px, min(320px, 80vw));
  box-shadow: var(--shadow-lg);
  pointer-events: none;
  opacity: 0;
  transition: opacity var(--duration-fast);
  z-index: 10000;
}
.term-tooltip::after {
  content: '';
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%);
  border: 6px solid transparent;
  border-top-color: var(--color-bg-code);
}
.term-tooltip.visible { opacity: 1; }
.term-tooltip.flip::after {
  top: auto; bottom: 100%;
  border-top-color: transparent;
  border-bottom-color: var(--color-bg-code);
}
```

**JS — position: fixed tooltips appended to body:**
```javascript
let activeTooltip = null;

function positionTooltip(term, tip) {
  const rect = term.getBoundingClientRect();
  const tipWidth = 300;
  let left = rect.left + rect.width / 2 - tipWidth / 2;
  left = Math.max(8, Math.min(left, window.innerWidth - tipWidth - 8));

  document.body.appendChild(tip);
  const tipHeight = tip.offsetHeight;
  if (rect.top - tipHeight - 8 < 0) {
    tip.style.top = (rect.bottom + 8) + 'px';
    tip.classList.add('flip');
  } else {
    tip.style.top = (rect.top - tipHeight - 8) + 'px';
    tip.classList.remove('flip');
  }
  tip.style.left = left + 'px';
}

document.querySelectorAll('.term').forEach(term => {
  const tip = document.createElement('span');
  tip.className = 'term-tooltip';
  tip.textContent = term.dataset.definition;

  term.addEventListener('mouseenter', () => {
    if (activeTooltip && activeTooltip !== tip) {
      activeTooltip.classList.remove('visible');
      activeTooltip.remove();
    }
    positionTooltip(term, tip);
    requestAnimationFrame(() => tip.classList.add('visible'));
    activeTooltip = tip;
  });
  term.addEventListener('mouseleave', () => {
    tip.classList.remove('visible');
    setTimeout(() => { if (!tip.classList.contains('visible')) tip.remove(); }, 150);
    activeTooltip = null;
  });
  term.addEventListener('click', (e) => {
    e.stopPropagation();
    if (activeTooltip && activeTooltip !== tip) {
      activeTooltip.classList.remove('visible');
      activeTooltip.remove();
    }
    if (tip.classList.contains('visible')) {
      tip.classList.remove('visible'); tip.remove(); activeTooltip = null;
    } else {
      positionTooltip(term, tip);
      requestAnimationFrame(() => tip.classList.add('visible'));
      activeTooltip = tip;
    }
  });
});

document.addEventListener('click', () => {
  if (activeTooltip) {
    activeTooltip.classList.remove('visible');
    activeTooltip.remove();
    activeTooltip = null;
  }
});
```

**Rules:**
- Tooltip EVERY domain-specific term on first use per module
- Definitions: 1–2 sentences, plain language, practical framing
- Use `position: fixed` + `document.body` append — never `position: absolute` inside containers (causes clipping)
- `cursor: pointer` (not `cursor: help`)

---

## Animated Process Flow

Step-by-step visualization where user clicks "Next Step" to advance. For any multi-step process from the source content.

**HTML:**
```html
<div class="process-flow">
  <div class="process-actors">
    <div class="process-actor" id="actor-1">
      <div class="process-actor-icon" style="background: var(--color-topic-1)">👤</div>
      <span>Customer</span>
    </div>
    <div class="process-actor" id="actor-2">
      <div class="process-actor-icon" style="background: var(--color-topic-2)">📢</div>
      <span>Marketing</span>
    </div>
    <div class="process-actor" id="actor-3">
      <div class="process-actor-icon" style="background: var(--color-topic-3)">💻</div>
      <span>Product</span>
    </div>
  </div>

  <div class="process-label" id="process-label">Click "Next Step" to trace the journey</div>

  <div class="process-controls">
    <button onclick="processNext(this)">Next Step</button>
    <button onclick="processReset(this)">Restart</button>
    <span class="process-progress">Step 0 / N</span>
  </div>
</div>
```

**JS pattern:**
```javascript
function initProcessFlow(container) {
  const steps = JSON.parse(container.dataset.steps);
  let currentStep = 0;

  container.querySelector('[onclick*="processNext"]').addEventListener('click', function() {
    if (currentStep >= steps.length) return;
    const step = steps[currentStep];

    container.querySelectorAll('.process-actor').forEach(a => a.classList.remove('active'));
    document.getElementById(step.highlight).classList.add('active');
    container.querySelector('.process-label').textContent = step.label;

    currentStep++;
    container.querySelector('.process-progress').textContent = `Step ${currentStep} / ${steps.length}`;
  });
}
```

```css
.process-actor.active {
  box-shadow: 0 0 0 3px var(--color-accent), 0 0 20px rgba(217, 79, 48, 0.2);
  transform: scale(1.05);
  transition: all var(--duration-normal) var(--ease-out);
}
.process-actors {
  display: flex;
  justify-content: space-around;
  margin-bottom: var(--space-6);
}
.process-actor {
  text-align: center;
  transition: all var(--duration-normal);
}
.process-actor-icon {
  width: 56px; height: 56px; border-radius: 50%;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.5rem; margin: 0 auto var(--space-2);
}
.process-label {
  text-align: center;
  font-size: var(--text-base);
  color: var(--color-text);
  padding: var(--space-4);
  background: var(--color-surface);
  border-radius: var(--radius-md);
  margin-bottom: var(--space-4);
  min-height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.process-controls {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: var(--space-3);
}
.process-controls button {
  padding: var(--space-2) var(--space-5);
  border: 2px solid var(--color-accent);
  background: white;
  color: var(--color-accent);
  font-weight: 600;
  border-radius: var(--radius-sm);
  cursor: pointer;
  font-family: var(--font-body);
  transition: all var(--duration-fast);
}
.process-controls button:first-child { background: var(--color-accent); color: white; }
.process-controls button:hover { opacity: 0.85; }
.process-progress { font-size: var(--text-sm); color: var(--color-text-muted); font-family: var(--font-mono); }
```
