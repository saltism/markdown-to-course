# Markdown to Course

A Claude Code / Cursor skill that turns any markdown file — or a folder of markdown files — into an interactive single-page HTML course.

Point it at a `.md` file or a folder. Get back a self-contained course with scroll-based navigation, animated diagrams, embedded quizzes, glossary tooltips, and progress tracking. 

One HTML file, no setup, works offline.

## The problem

You have 900 lines of course notes, a strategy doc, a podcast transcript, or a reading compilation sitting in your vault. You know it’s valuable. You keep telling yourself you'll read it later.

Long markdown is a wall: every paragraph looks the same, there’s no visual hierarchy beyond heading sizes, and fatigue sets in fast.

## What this does

The skill reads your markdown, identifies the structure and key concepts, and generates an HTML course that:

- **Chunks** content into scroll-based modules (one concept per screen, generous whitespace)
- **Visualizes** frameworks as interactive diagrams — loops with animated orbits, funnels with scroll-triggered animations, 2×2 matrices, waterfall charts for formula breakdowns
- **Tests** understanding with scenario-based quizzes (not “what does CAC stand for” — that’s what the glossary tooltips handle)
- **Highlights** key terms as Concept Spotlight blocks with plain-language explanations
- **Tracks** progress with a nav bar, module dots, and keyboard navigation (arrow keys)

The output gives you a framework to understand what the content is about. For deeper details, go back to the source.

## How to use

### As a Claude Code skill

```
cp -r markdown-to-course ~/.claude/skills/
```

Then: *“Turn product-fundamentals.md into a course”*

### As a Cursor skill

Copy `markdown-to-course/` into `.cursor/skills/` in your project.

Then: *“Make a course from the product-course/ folder”*

### Input modes

**Single file:**

```
Turn product-fundamentals.md into a course
```

**Folder of files:**

```
Make a course from the product-course/ folder
```

Files with numeric prefixes (`01-`, `02-`) sort automatically. Each file becomes a module. A `README.md` or `00-intro.md` becomes the course introduction.

## How it works

The skill follows a 4-phase process:

1. **Content analysis** — read the markdown, extract concepts, frameworks, examples, data points, and the logical flow
2. **Curriculum design** — structure 4–8 modules, assign visual treatments, write quiz questions
3. **Build** — generate HTML using the component library (`MTC.`* functions) and Lucide Icons. The AI calls component functions with data; the functions handle all rendering, animation, and interactivity
4. **Review** — open in browser, walk through the result

### Component system

The course uses a reusable JS component library to keep generation lightweight. Instead of writing 30 lines of SVG for a loop diagram, the AI writes:

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

17 component types cover concept cards, loop diagrams, funnels, matrices, comparisons, waterfalls, interactive calculators, quizzes, and more. Icons come from [Lucide](https://lucide.dev) via CDN.

## Skill structure

```
markdown-to-course/
├── SKILL.md                              # Main skill instructions
├── README.md
├── ai-growth-playbook-sample.html        # Optional demo page (open in browser)
└── references/
    ├── components.md                     # JS component library + API docs (primary reference)
    ├── design-system.md                  # CSS tokens, typography, colors, layout
    └── interactive-elements.md           # Element design patterns and quiz-writing guidance
```

## Design

- Warm parchment background (`#E4DFD0`), near-black text, high contrast
- Helvetica Neue + Space Mono typography
- Sharp geometry: borders over shadows, minimal border-radius, 1px-gap grids
- Accent color as line detail only (default: deep purple `#6C4AB6`), never as large background fills
- Uppercase restricted to tiny mono labels; all headings in title/sentence case

## License

MIT — use it, fork it, sell it, break it. See [LICENSE](LICENSE).

## Credits

Inspired by [zarazhangrui/codebase-to-course](https://github.com/zarazhangrui/codebase-to-course), which turns codebases into visual courses for learning code.

This project adapts the idea for a different input (markdown) and audience (anyone with long-form text they want to absorb faster).

---

Built by [saltism](https://github.com/saltism)