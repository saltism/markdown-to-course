---
name: markdown-to-course
description: "Turn any markdown file or folder of markdown files into a beautiful, interactive single-page HTML course for visual learning. Use this skill when someone wants to convert long-form markdown content (articles, notes, course materials, documentation) into a scroll-based course with progress tracking, concept cards, interactive quizzes, framework visualizations, and glossary tooltips. Trigger phrases: 'turn this markdown into a course', 'make a course from these notes', 'visualize this document', 'I want to learn this interactively', 'convert these files to a course'."
---

# Markdown-to-Course

Transform any markdown file — or a folder of markdown files — into a stunning, interactive single-page HTML course optimized for visual learning. The output is a single self-contained HTML file (no dependencies except Google Fonts) with scroll-based modules, animated concept cards, framework diagrams, embedded quizzes, and glossary tooltips.

## First-Run Welcome

When the skill is first triggered and the user hasn't specified content yet, introduce yourself:

> **I can turn any markdown into an interactive visual course — so you never have to grind through a wall of text again.**
>
> Point me at your content:
> - **A single file** — e.g., "turn product-fundamentals.md into a course"
> - **A folder** — e.g., "make a course from the growth-engineering-course/ folder"
> - **Paste content** — paste markdown directly and say "make this a course"
>
> I'll read through the content, identify the key concepts and structure, and generate a self-contained HTML course with visual concept breakdowns, framework diagrams, interactive quizzes, and progress tracking. Opens in any browser, works offline.

## Input Modes

### Mode A: Single File

One markdown file becomes one course. The file's heading structure (H1/H2/H3) maps to modules and sections:

- **H1** → Course title (if only one) or Module boundary (if multiple)
- **H2** → Module boundary or Section within a module
- **H3** → Sub-section / screen within a section

If a file has one H1 and multiple H2s, each H2 becomes a module. If a file has multiple H1s, each H1 becomes a module and H2s become sections within it. Use judgment — the goal is 4–8 modules of roughly balanced depth.

### Mode B: Folder of Files

A folder of markdown files becomes one cohesive course. Each file becomes a major module (chapter).

**Ordering rules:**
1. Numeric prefixes sort first: `01-intro.md`, `02-loops.md`, `03-channels.md`
2. If no numeric prefixes, sort alphabetically
3. If a file named `README.md`, `index.md`, or `00-*.md` exists, it becomes the course introduction
4. Ignore non-markdown files in the folder

**Within each file**, H1 is the module title, H2s become sections, H3s become sub-sections — same as single-file mode.

**Cross-file references**: If content in file B references a concept introduced in file A, add a brief "As we covered in Module N..." callback. The course should feel like one continuous narrative, not disjointed chapters.

## Who This Is For

The target learner is **anyone with a long markdown document they want to actually absorb** — not skim, not ctrl-F, but understand and retain. This includes:

- People taking online courses (Reforge, Maven, Coursera) who export or copy notes into markdown
- Self-learners who collect articles, book notes, or research in markdown vaults
- Professionals who need to internalize strategy docs, playbooks, or frameworks
- Anyone who thinks "this is 900 lines, I'll read it later" — and never does

**Their goals are practical:**
- Absorb dense material faster through visual structure
- Test their understanding with embedded quizzes (not just passive reading)
- Return to specific concepts quickly via module navigation
- Actually finish the document instead of abandoning it halfway

## Why This Works

Long markdown is linear and monotonous. Every paragraph looks the same. The eye has no anchor points, no visual hierarchy beyond heading sizes. Fatigue sets in fast.

An interactive course fixes this by:
- **Chunking**: one concept per screen, generous whitespace, visual breathing room
- **Multi-modal encoding**: the same idea as text + diagram + quiz = three memory passes
- **Active recall**: quizzes force retrieval, which is proven to beat re-reading
- **Progress feedback**: the progress bar and module dots create momentum ("I'm 60% through")
- **Visual anchors**: concept cards, framework diagrams, and callout boxes give each idea a distinct visual shape — you remember *where* you learned something, not just *what*

---

## The Process (4 Phases)

### Phase 1: Content Analysis

Before writing any HTML, deeply understand the source material. Read every file, trace the argument structure, identify the key concepts, frameworks, and examples.

**What to extract:**
- The central thesis or learning objective of the entire document/folder
- Key concepts and their definitions (these become glossary tooltips)
- Frameworks, models, and mental models (these become visual diagrams)
- Concrete examples, case studies, and data points (these become highlight cards)
- Sequences and processes (these become flow diagrams or step cards)
- Comparisons and contrasts (these become side-by-side cards)
- Expert quotes or notable statements (these become quote callouts)
- The logical flow: what depends on what, what builds on what

**For folders**: map the narrative arc across files. Which file introduces foundational concepts? Which builds on them? Is there a natural climax or synthesis?

### Phase 2: Curriculum Design

Structure the course as **4–8 modules**. Each module should take 3–5 minutes to scroll through. The arc should feel like a journey with clear progression.

**Module design principles:**

| Module Position | Purpose |
|---|---|
| 1 | Set the stage: why does this topic matter? What will you walk away with? |
| 2–3 | Core concepts: the foundational ideas everything else builds on |
| 4–5 | Application: how these concepts play out in real scenarios |
| 6–7 | Advanced patterns: nuances, edge cases, expert-level insights |
| Last | Synthesis: how everything connects, what to do next |

Not every source needs all positions. A 300-line file might yield 4 modules. A 900-line course folder might yield 7–8. Adapt to the content's actual depth.

**Each module should contain:**
- 3–6 screens (sub-sections that flow within the module)
- At least one **Concept Spotlight** (key term or framework, visually highlighted)
- At least one **interactive element** (quiz, drag-and-drop, or scenario question)
- At least one **visual element** (framework diagram, flow chart, concept cards, or data highlight)
- A **Key Takeaway** callout at the end summarizing the module's core insight

**Mandatory interactive elements (every course must include ALL of these):**
- **Concept Spotlight blocks** — at least one per module. The signature teaching element: a key concept or framework presented with visual emphasis, a plain-language explanation, and a concrete example.
- **Framework/Process Visualizations** — at least one per course. Any model, loop, funnel, matrix, or multi-step process from the source must be visualized, not left as text.
- **Quizzes** — at least one per module (multiple-choice, scenario-based, or drag-and-drop matching).
- **Glossary Tooltips** — on every technical or domain-specific term, first use per module.
- **Key Takeaway Callouts** — one per module, at the module's end.

**Do NOT present the curriculum for approval — just build it.** The user wants a course, not a planning document.

### Phase 3: Build the Course

Generate a single HTML file with embedded CSS and JavaScript. Read `references/design-system.md` for CSS tokens. Read `references/components.md` for the component library.

**CRITICAL: Use the component system. Do NOT write raw SVG, complex HTML structures, or interactive JS by hand.**

The component library (`MTC.*` functions) handles:
- All visual elements (concept cards, loop diagrams, funnels, matrices, comparisons)
- All interactive elements (quizzes, chains, calculators, waterfalls)
- All infrastructure (scroll reveal, progress bar, nav dots, keyboard nav, tooltips)
- Icon rendering via Lucide Icons CDN

**Build order:**

1. **Foundation** — HTML shell: `<head>` with fonts + Lucide CDN + CSS from design-system.md. Module `<section>` skeletons with `<div id="m1-xxx"></div>` placeholders for components. Navigation bar. At the end: `<script>` with component library from components.md.

2. **Component calls** — In a final `<script>` block, call `MTC.*` functions to populate each placeholder with data. The AI's job: parse the markdown, choose which component fits each concept, and provide the data. End with `MTC.init()`.

3. **Polish pass** — Check mobile responsiveness, verify all glossary terms have tooltips, ensure quiz questions test application not recall.

**What the AI writes for each content block:**
```
// Instead of 30 lines of SVG:
MTC.loop('#m3-viral-loop', {
  nodes: [
    { label: 'Sign up' },
    { label: 'Invite' },
    { label: 'Click' },
    { label: 'New user' }
  ]
});
```

**Icons: use Lucide, never raw SVG.** See the icon reference table in components.md. The AI picks an icon name; `MTC.init()` renders them all via `lucide.createIcons()`.

**When NO component exists for a visual:** write simple HTML with design-system CSS classes. This should be rare — check components.md first.

**Critical implementation rules:**
- External dependencies: Google Fonts CDN + Lucide CDN (both lightweight, cached)
- Use CSS `scroll-snap-type: y proximity` (NOT `mandatory`)
- Use `min-height: 100dvh` with `100vh` fallback
- Only animate `transform` and `opacity` for GPU performance
- `MTC.init()` handles all observers, listeners, and icon rendering — call it once at the end

### Phase 4: Review and Open

After generating the HTML, open it in the browser for review. Walk the user through what was built and invite feedback.

---

## Content Philosophy

### Aggressively Visual

The course should feel closer to an infographic than a textbook.

**Screen-level text limits:**
- Max **2–3 sentences** per body paragraph. Fourth sentence? Convert to a visual.
- Every screen must be **at least 50% visual** (diagrams, cards, callouts — anything that isn't a paragraph).

**Per-component text limits — non-negotiable:**

| Component | Max text per item |
|---|---|
| Concept card (`.concept-desc`) | 1 sentence. If you need more, you need two cards. |
| Spotlight explanation | 2 sentences. Example block: 1 sentence. |
| Step card description | 1 sentence. |
| Flow step detail | 1 sentence, ideally a noun phrase. |
| Data highlight context | ≤ 8 words. |
| Quote callout | Exact quote only — don't pad it. |
| Takeaway | 1–2 sentences max. The key insight, nothing else. |

**The rule**: if you're writing a third sentence inside any single component, stop. Either cut, or split into two components, or switch to a different visual type. A long concept card description is a wall of text in a frame — it doesn't become visual just because it has a border.

**Convert text to visuals:**
- A list of 3+ items → **concept cards with icons**
- A sequence of steps → **flow diagram** or **numbered step cards**
- A framework or model → **visual diagram** (loop, matrix, funnel)
- "X is like Y" comparisons → **side-by-side comparison cards**
- Key definitions → **Concept Spotlight block**
- Statistics or data points → **data highlight cards**
- Expert quotes → **quote callout with attribution**
- Processes → **animated flow visualization**

### Concept Spotlight Blocks

The signature element of markdown-to-course (replaces code↔English from codebase-to-course). Every key concept or framework gets a visually distinct treatment:

- Left/top: the concept name, large and bold
- Right/bottom: plain-language explanation (1–2 sentences) + a concrete example from the source or a relatable scenario
- Visual treatment: accent-colored border, card surface, geometric decoration (auto-generated by `MTC.spotlight`)

This is the single most valuable element for comprehension. When a reader encounters "Contribution Margin" in 14px body text buried in a paragraph, their eyes glaze over. When they see it as a distinct card with an explanation and example, it sticks.

### Respect the Source

Unlike codebase-to-course, the input is already polished prose — not raw code. The job is to restructure and visualize, not to rewrite.

**Rules:**
- Preserve the author's key arguments, examples, and data points faithfully
- Don't add claims or data not present in the source
- When simplifying for a visual, ensure the simplification is accurate
- If the source has a great analogy or example, use it directly — don't invent a worse one
- Attribute quotes to the people named in the source

### One Concept Per Screen

Each screen within a module teaches exactly one idea. If you need more space, add another screen — don't cram.

### Quizzes That Test Application

**What to quiz:**
1. **Scenario questions** — "Your company's gross margin is 15%. Based on what you learned, what should the growth team prioritize?" Tests whether concepts were understood, not memorized.
2. **Framework application** — "Which type of growth loop does this example describe?" Tests pattern recognition.
3. **Decision-making** — "Given X situation, which metric should you focus on and why?" Tests practical judgment.
4. **Connections** — "How does concept A from Module 2 relate to concept B from Module 4?" Tests synthesis.

**What NOT to quiz:**
- Definitions ("What does CAC stand for?") — that's what glossary tooltips are for
- Recall of specific numbers from the text — that tests memory, not understanding
- Anything answerable by scrolling up

**Quiz tone:**
- Wrong answers: encouraging, teach something new. "Not quite — here's the distinction..."
- Correct answers: brief reinforcement. "Exactly. This matters because..."
- Never punitive. No "You got 3/5!" scorekeeping.

### Glossary Tooltips

Every domain-specific term gets a dashed-underline tooltip on first use per module. The reader should never need to Google a term.

**Be aggressive with tooltips.** Marketing, finance, and strategy content is full of jargon that even experienced people mix up. Tooltip these:
- Acronyms: CAC, LTV, ARPU, COGS, EBITDA, SG&A, MQL, SQL, CPC, CPM, ROAS
- Framework names: growth loops, flywheels, contribution margin, unit economics
- Implied knowledge: "top of funnel," "activation rate," "cohort analysis"

**Each tooltip should make the reader smarter**, not just define the word. Bad: "CAC = Customer Acquisition Cost." Good: "CAC (Customer Acquisition Cost) — the total you spend to acquire one new customer. If your CAC is $50 and each customer pays $30/month, you need almost two months just to break even on acquisition."

---

## Design Identity

Read `references/design-system.md` for the full token system. Non-negotiable principles:

- **Warm neutral palette**: parchment background (`#E4DFD0`), near-black text (`#080808`), high contrast. NO cold whites or blues.
- **One bold accent**: deep purple (`#6C4AB6`) as default. Can be adapted per content personality, but always a single confident hue.
- **Swiss typography**: Helvetica Neue for body, Space Mono for labels/data. Clean, no decorative display fonts.
- **Sharp geometry**: minimal border-radius. Borders instead of shadows. 1px-gap grids. Pill buttons on actions only.
- **Generous whitespace**: modules breathe. Max 3–4 short paragraphs per screen.
- **Alternating backgrounds**: even/odd modules alternate between two warm tones.
- **No full-caps fatigue**: UPPERCASE only for tiny mono labels (module numbers, step tags, quiz headers). All headings use title case or sentence case.

---

## Gotchas — Common Failure Points

### Tooltip Clipping
Concept Spotlight blocks and other containers with `overflow: hidden` will clip tooltips. **Fix:** tooltips must use `position: fixed` and be appended to `document.body`. Calculate from `getBoundingClientRect()`.

### Walls of Text
The #1 failure mode — and it happens at two levels:

**Screen level**: If a screen has more than 2–3 sentences of body text without a visual break, stop. Convert to cards, diagrams, or callouts.

**Component level**: Long descriptions inside concept cards, spotlight blocks, or step cards are walls of text in disguise. A concept card with three sentences is not visual — it's a paragraph with a border. Apply the per-component limits from the Content Philosophy section ruthlessly. When in doubt: split into two components, or switch to a more appropriate visual type.

### Passive Content
A module with only text, no interactivity. Every module needs at least one of: quiz, scenario question, drag-and-drop, or clickable element. These aren't decorations — they're how active learning works.

### Losing the Narrative Thread (Folder Mode)
When processing multiple files, the course can feel like disconnected chapters. **Fix:** add brief transitions between modules: "Now that we understand X, let's see how it drives Y." Refer back to earlier concepts. The course should feel like one continuous conversation.

### Over-Simplifying
The source material may be dense for a reason. Don't dumb down — restructure. A complex framework is still complex in the course; the difference is that it's now visual, chunked, and has a quiz to test understanding.

### Quiz Questions That Test Memory
Asking "What percentage did the author mention?" tests recall, not understanding. Every quiz question should present a situation the reader hasn't seen and ask them to apply what they learned.

### Scroll-Snap Mandatory
Using `scroll-snap-type: y mandatory` traps users in long modules. Always use `proximity`.

### Module Quality Degradation
Building all modules in one pass causes later ones to be thin. Build one at a time.

---

## Reference Files

Read these when you reach the relevant phase:

- **`references/design-system.md`** — CSS custom properties, color palette, typography, layout. Copy the CSS into the generated HTML's `<style>` block.
- **`references/components.md`** — **Primary reference.** Full component library (JS), API documentation for every component, Lucide icon name reference. Copy the JS into a `<script>` block and call `MTC.*` functions with content data.
- **`references/interactive-elements.md`** — Legacy reference for element design patterns. Use components.md instead for implementation; consult this only for design intent or quiz-writing guidance.
