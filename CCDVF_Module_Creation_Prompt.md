# 🧠 CCDV-F Slide Module Creation Prompt

> Paste everything below into your AI, then append the raw course documentation content at the end. That's it.

---

## THE PROMPT

```
You are a senior front-end developer and instructional designer building a slide deck lesson for the CCDV-F (Claude Certified Developer Foundations) curriculum.

I will give you raw course documentation at the end of this prompt. From that content alone, you must autonomously:
  - Determine the lesson title, module context, and all slide topics
  - Invent a production incident story at ApexCorp that makes the content dramatic and engaging
  - Choose the most fitting accent color from the design palette
  - Derive key exam facts from the documentation
  - Design a contextual interactive element (simulator, calculator, or lab)
  - Write a realistic exam-style multiple-choice question with a tricky plausible wrong answer
  - Decide on the incident ID and the specific API error that broke ApexCorp's system

Do NOT ask me any clarifying questions. Make confident creative decisions and produce the full file.

You must produce a complete, single-file HTML slide deck that is:
  1. Visually stunning — dark cyberpunk/terminal aesthetic
  2. Mobile-responsive — works perfectly on phones, tablets, and desktop
  3. Narratively engaging — teaches through a production incident story
  4. Exam-focused — reinforces CCDV-F certification test knowledge
  5. Interactive — includes at least one simulator or interactive element

---

## DESIGN SYSTEM (DO NOT DEVIATE)

### Color Palette
```css
--bg-dark:       #0B0F19;   /* deep space background */
--surface-navy:  #111827;   /* card/panel background */
--surface-card:  #1F2937;   /* elevated card */
--border-cyan:   rgba(6, 182, 212, 0.3);
--accent-blue:   #3B82F6;
--accent-cyan:   #06B6D4;
--alert-amber:   #F59E0B;
--alert-red:     #EF4444;
--success-green: #10B981;
--accent-purple: #8B5CF6;
--text-main:     #F3F4F6;
--text-muted:    #9CA3AF;
--font-mono:     'Fira Code', monospace;
--font-sans:     'Inter', sans-serif;
```

Pick one color as the **primary accent** for this lesson's header, eyebrows, badges, and glow. Choose based on the topic's feel:
- amber → safety, warnings, agents, HITL
- cyan → information, streaming, APIs
- green → success states, caching, efficiency
- purple → reasoning, thinking, advanced concepts
- blue → multimodal, files, batch, data
- red → errors, debugging, critical failures

### Typography
- **Fira Code** — all monospace: code blocks, eyebrows, header/footer labels, counter badges
- **Inter** — body text, card copy, slide titles
- **Font Awesome 6.5.1** — icons

### Slide Anatomy (every content slide has this structure)
```
[ .deck-header ]   — 48px, brand icon + lesson name on left; hub link + badge + topic hint on right
[ .slides-wrapper ]  — flex:1, holds all .slide-container elements stacked absolutely
  [ .slide-container ]  — absolutely positioned, full area, padding 36px 48px
    [ .slide-eyebrow ]  — small mono uppercase label, e.g. "// PRODUCTION PITFALL"
    [ .slide-title ]    — large bold title with fa-icon prefix
    [ content area ]    — grids, cards, code boxes, interactive elements
[ .deck-footer ]   — 52px, lesson label on left; slide counter + prev/next buttons on right
```

### Component Classes

**`.slide-eyebrow`** — `font-mono, 12px, accent-color, uppercase, letter-spacing: 1.5px, mb: 6px`

**`.slide-title`** — `26px, weight-800, white, mb: 20px, display:flex, gap: 12px` for icon alignment

**`.grid-2`** — `display: grid; grid-template-columns: 1fr 1fr; gap: 20px; flex: 1; min-height: 0;`

**`.feature-card`** — `background: var(--surface-card); border: 1px solid rgba(255,255,255,0.08); border-radius: 8px; padding: 16px 20px;`

**`.code-box`** — `background: #060913; border: 1px solid rgba(255,255,255,0.1); border-radius: 8px; padding: 14px 18px; font-mono; font-size: 12px; line-height: 1.6; overflow-x: auto;`

**`.badge-exam`** — small pill badge in primary accent color, used in header and cover slide

**`.nav-btn`** — footer navigation buttons; hover changes bg to accent color

**`.quiz-option`** — clickable answer option; `.selected-correct` → green; `.selected-wrong` → red

### Code Syntax Highlighting (manual inline spans — no library)
- Comments → `color: #6B7280`
- Strings / values → `color: #10B981`
- Keywords (if, while, return, for, raise) → `color: #8B5CF6`
- Object keys / params → `color: #06B6D4`
- Numbers / booleans → `color: #FBBF24`
- Error strings → `color: #EF4444`

### Glow Box Shadows (use on .deck-container to match lesson tone)
```css
box-shadow: 0 0 35px rgba(245, 158, 11, 0.15) /* amber */
box-shadow: 0 0 35px rgba(16, 185, 129, 0.15)  /* green */
box-shadow: 0 0 35px rgba(139, 92, 246, 0.15)  /* purple */
box-shadow: 0 0 35px rgba(6, 182, 212, 0.15)   /* cyan */
box-shadow: 0 0 35px rgba(59, 130, 246, 0.15)  /* blue */
box-shadow: 0 0 35px rgba(239, 68, 68, 0.15)   /* red */
```

---

## STORYTELLING RULES

### The Universe
ApexCorp runs **APEX-AI Engine v3** — their flagship enterprise customer service and operations AI platform, serving 2.4 million enterprise users. Every lesson is a production incident on this system. The student is the **Lead AI Systems Engineer on duty**. High stakes = high engagement.

Incident IDs follow the pattern `#XXX-TAG` (HTTP status code + topic keyword):
- `#404-TOK` — tokenization / context window
- `#502-AGENT` — agentic loop / HITL
- `#429-RATE` — rate limits / retry storms
- `#400-TOOL` — tool schema / validation
- `#500-CACHE` — prompt caching / compaction
- `#503-STREAM` — SSE streaming / event handling
- Invent new ones as needed following the same pattern

Timestamps always use: `2026-XX-XX HH:MM:00 UTC`

### Slide 1 — Mission Briefing (Cover)
Must contain:
- An incident badge: `⚠ CRITICAL INCIDENT #XXX-TAG` with CSS `animate-pulse` in red or amber
- A timestamp line
- A bold `<h1>` explaining the lesson topic in dramatic terms
- 3 Objective cards in a 3-column grid (Objective 01 / 02 / 03), each with a cyber-colored label, a short title, and 1-sentence description
- A role bar at the bottom: `ROLE: Lead AI Systems Engineer | Target Certification: CCDV-F`
- A `PRESS [NEXT →] TO INVESTIGATE ROOT CAUSE` prompt

### Slide 2 — Root Cause Analysis
Must contain:
- 2 or 3 failure cards, each with:
  - A colored mono header (e.g. `Failure 1: Bad Schema`)
  - A `<div class="code-box">` showing the **exact error message or bad code** that caused the incident
  - A 2-3 sentence plain-language explanation of the mistake
- A bottom exam-reality bar: `EXAM REALITY: CCDV-F tests your exact understanding of [specific behavior]...`

### Middle Slides (3–6) — Teaching the Fix
Each slide:
- Has a `// CONCEPT NAME` eyebrow from the reference table below
- Uses `.grid-2` layout: code example or diagram on one side, feature-cards with explanation on the other
- Code examples use the syntax highlighting rules
- Feature cards use left-border or top-border accent colors to signal danger/success/info

### Interactive Lab Slide — `// INTERACTIVE LAB`
- Must include a user-controlled element: a range slider, button sequence, tabbed comparator, or toggle switch
- Output must update in real-time via vanilla JS
- No external dependencies — pure HTML/CSS/JS
- The lab must directly simulate a real API decision from the documentation (e.g., adjusting a parameter, comparing API modes, calculating costs)

### Production Pitfalls Slide — `// PRODUCTION PITFALLS`
- 3 traps in a **3-column grid** (`display: grid; grid-template-columns: repeat(3, 1fr)`)
- Each card has `border-top: 3px solid [color]`: red = fatal, amber = dangerous, cyan = subtle-but-costly
- Each trap has an icon, a bold name, and 2-3 sentence explanation

### Exam Question Slide — `// CCDV-F EXAM SIMULATION`
- One realistic exam question derived from the documentation content
- 4 `.quiz-option` divs (A, B, C, D) with letter labels in accent color
- One correct answer; the wrong answers must be **plausible but subtly incorrect**
- A hidden `#quiz-explanation` div that reveals only on correct answer click
- Clicking a wrong answer shows the div with class `selected-wrong` but does NOT show the explanation

### Summary Slide — `// CERTIFICATION CHEAT SHEET`
- `.grid-2` with 2 feature cards, each containing **2 numbered rules** (4 rules total)
- Each rule: bold title + 1-2 sentence explanation
- Left card uses primary accent border; right card uses secondary accent (cyan or green)
- Ends with a sense of mastery and exam readiness

---

## EYEBROW LABEL REFERENCE

| Slide Role | Eyebrow Label |
|---|---|
| Cover | `// INCIDENT BRIEFING` |
| Root cause | `// ROOT CAUSE ANALYSIS` |
| Core concept A | `// FOUNDATION CONCEPT` |
| Core concept B | `// IMPLEMENTATION PATTERN` |
| Core concept C | `// COST & LATENCY OPTIMIZATION` |
| Core concept D | `// ARCHITECTURAL CLASSIFICATION` |
| Core concept E | `// SAFETY & GOVERNANCE` |
| Interactive lab | `// INTERACTIVE LAB` |
| Fatal traps | `// PRODUCTION PITFALLS` |
| Exam question | `// CCDV-F EXAM SIMULATION` |
| Summary | `// CERTIFICATION CHEAT SHEET` |

---

## NAVIGATION & INTERACTIVITY

### Slide Navigation (use exactly)
```javascript
let currentSlide = 1;
const totalSlides = N; // set to actual slide count

function updateDeckState() {
  document.querySelectorAll('.slide-container').forEach(s => s.classList.remove('active'));
  document.getElementById(`slide-${currentSlide}`).classList.add('active');
  document.getElementById('current-slide-num').innerText = currentSlide;
  document.getElementById('btn-prev').disabled = (currentSlide === 1);
  document.getElementById('btn-next').disabled = (currentSlide === totalSlides);
}

function nextSlide() { if (currentSlide < totalSlides) { currentSlide++; updateDeckState(); } }
function prevSlide() { if (currentSlide > 1) { currentSlide--; updateDeckState(); } }

document.addEventListener('keydown', (e) => {
  if (e.key === 'ArrowRight' || e.key === ' ') nextSlide();
  else if (e.key === 'ArrowLeft') prevSlide();
});

updateDeckState();
```

### Quiz Answer Check (use exactly)
```javascript
function checkAnswer(el, isCorrect) {
  const quizSlide = el.closest('.slide-container');
  quizSlide.querySelectorAll('.quiz-option').forEach(opt => {
    opt.classList.remove('selected-correct', 'selected-wrong');
  });
  if (isCorrect) {
    el.classList.add('selected-correct');
    document.getElementById('quiz-explanation').style.display = 'block';
  } else {
    el.classList.add('selected-wrong');
    document.getElementById('quiz-explanation').style.display = 'none';
  }
}
```

---

## MOBILE RESPONSIVENESS (MANDATORY — USE EXACTLY)

**Responsive container CSS** (no hardcoded 1280×720 anywhere):
```css
body {
  background-color: #030712;
  color: var(--text-main);
  font-family: var(--font-sans);
  min-height: 100vh;
  overflow-x: hidden;
}

.viewport {
  width: 100vw;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
}

.deck-container {
  width: 100%;
  max-width: 1280px;
  aspect-ratio: 16 / 9;
  max-height: calc(100vh - 40px);
  background-color: var(--bg-dark);
  border: 1px solid var(--border-cyan);
  /* use the per-lesson glow color here */
  box-shadow: 0 0 35px rgba(X, X, X, 0.15), inset 0 0 15px rgba(0, 0, 0, 0.8);
  border-radius: 12px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
}

.slides-wrapper {
  flex: 1;
  position: relative;
  overflow: hidden;
  min-height: 0;
}

.slide-container {
  position: absolute;
  top: 0; left: 0; width: 100%; height: 100%;
  padding: 36px 48px;
  display: none;
  flex-direction: column;
  opacity: 0;
  transition: opacity 0.2s ease-in-out;
}

.slide-container.active { display: flex; opacity: 1; }

.grid-2 {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  flex: 1;
  min-height: 0;
}
```

**Mobile media query** (place after all other CSS, inside `<style>`):
```css
/* ─── Mobile Adaptive Layout ─────────────────────────────── */
@media (max-width: 768px), (orientation: portrait) {
  body {
    overflow-y: auto !important;
    user-select: text !important;
  }
  .viewport {
    width: 100% !important;
    min-height: 100dvh !important;
    padding: 0 !important;
    align-items: flex-start !important;
  }
  .deck-container {
    width: 100% !important;
    max-width: 100% !important;
    height: auto !important;
    min-height: 100dvh !important;
    aspect-ratio: auto !important;
    max-height: none !important;
    border-radius: 0 !important;
    border-left: none !important;
    border-right: none !important;
  }
  .slides-wrapper {
    overflow-y: auto !important;
    height: auto !important;
    min-height: calc(100dvh - 100px) !important;
  }
  .slide-container {
    position: relative !important;
    width: 100% !important;
    height: auto !important;
    min-height: calc(100dvh - 100px) !important;
    padding: 20px 16px !important;
    overflow-y: auto !important;
  }
  .slide-container.active {
    display: flex !important;
  }
  .grid-2 {
    grid-template-columns: 1fr !important;
    height: auto !important;
  }
  .slide-title {
    font-size: 18px !important;
    margin-bottom: 12px !important;
  }
  .deck-header {
    height: auto !important;
    padding: 8px 12px !important;
    font-size: 11px !important;
    flex-wrap: wrap;
    gap: 6px;
  }
  .deck-footer {
    height: auto !important;
    padding: 8px 12px !important;
    font-size: 11px !important;
  }
  .deck-header .brand span,
  .deck-header .status span:not(.badge-exam) {
    display: none;
  }
  /* 3-col grids collapse to 1 col */
  [style*="grid-template-columns: repeat(3, 1fr)"] {
    grid-template-columns: 1fr !important;
  }
}
```

---

## REQUIRED DEPENDENCIES (CDN only — no npm, no Tailwind, no React)

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;700&family=Inter:wght@300;400;600;700;800&display=swap" rel="stylesheet">
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">
```

---

## OUTPUT REQUIREMENTS

Produce a **single complete `.html` file**. It must:

- Have NO hardcoded `width: 1280px` or `height: 720px` on `.deck-container`
- Include `viewport-fit=cover` in the `<meta name="viewport">` tag
- Include the mobile media query block exactly as shown above
- Include keyboard navigation (← → and Space bar)
- Include a working interactive element in the lab slide (vanilla JS only)
- Include a working multiple-choice quiz with reveal-on-correct behavior
- Have the footer text: `CCDV-F EXAM PREPARATION • LESSON [X] OF [TOTAL]`
- Have a `<a href="../index.html">` Hub link in the header
- Render with zero layout overflow on any screen size

Name the output file based on the lesson topic in Snake_Case (e.g. `Rate_Limits_and_Retry.html`).

---

## COURSE DOCUMENTATION

[PASTE THE RAW COURSE CONTENT HERE]
```
