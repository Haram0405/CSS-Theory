# 🎨 CSS Theory Assignment
### MERN Stack + AI Engineering Bootcamp — Week 2
**TechnerLab Academy** | Total Marks: 80

---

## Table of Contents
- [Q1 — What is CSS?](#q1--what-is-css-and-how-do-you-add-it-to-an-html-page)
- [Q2 — CSS Selectors](#q2--css-selectors)
- [Q3 — CSS Box Model](#q3--css-box-model)
- [Q4 — CSS Colors](#q4--css-colors)
- [Q5 — CSS Units](#q5--css-units)
- [Q6 — CSS Specificity & the Cascade](#q6--css-specificity-and-the-cascade)
- [Q7 — CSS Flexbox](#q7--css-flexbox)
- [Q8 — Pseudo-classes & Pseudo-elements](#q8--css-pseudo-classes-and-pseudo-elements)
- [Q9 — Transitions & Animations](#q9--css-transitions-and-animations)
- [Q10 — Responsive Web Design](#q10--responsive-web-design)

---

## Q1 — What is CSS and how do you add it to an HTML page?

### What is CSS?

**CSS** stands for **Cascading Style Sheets**. It is the language used to control how HTML elements look on a webpage — things like colors, fonts, spacing, layout, and sizes.

**The problem CSS solves:** HTML alone only defines the *structure* of a page (headings, paragraphs, images). Without CSS, every webpage would look like plain black text on a white background. CSS separates *design* from *content*, making websites visually appealing and easier to maintain.

---

### Three Ways to Add CSS

| Method | Where it goes | Best for |
|---|---|---|
| **External** | Separate `.css` file linked via `<link>` | Real projects ✅ |
| **Internal** | Inside a `<style>` tag in the `<head>` | Single-page demos |
| **Inline** | Directly on an element via `style=""` | Quick one-off overrides |

---

### ✅ Recommended Method: External CSS

External CSS is preferred because:
- One `.css` file can style **hundreds of HTML pages**
- Changing a color or font only requires editing **one file**
- The browser **caches** the CSS file, making the site load faster on repeat visits
- It keeps HTML clean and readable (separation of concerns)

---

### Code Examples

**1. External CSS** — link a separate file

```html
<!-- index.html -->
<head>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <h1>Hello World</h1>
</body>
```

```css
/* styles.css */
h1 {
  color: tomato;
  font-family: sans-serif;
}
```

---

**2. Internal CSS** — style tag inside `<head>`

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    h1 {
      color: steelblue;
      font-family: sans-serif;
    }
  </style>
</head>
<body>
  <h1>Hello World</h1>
</body>
</html>
```

---

**3. Inline CSS** — style attribute directly on an element

```html
<h1 style="color: green; font-size: 32px;">Hello World</h1>
```

> ⚠️ Inline CSS is hard to maintain and overrides other styles — avoid it in real projects.

---

## Q2 — CSS Selectors

### What are CSS Selectors?

A CSS **selector** is the part of a CSS rule that tells the browser *which HTML element(s) to style*. Different selector types let you target elements in very specific ways.

---

### Class vs ID

| | Class (`.`) | ID (`#`) |
|---|---|---|
| **Reusable?** | ✅ Yes — use on many elements | ❌ No — must be unique per page |
| **Specificity** | Lower | Higher |
| **Use case** | Styling groups of elements | Targeting one specific element |

> **Rule:** IDs have higher specificity than classes. Prefer classes for styling; use IDs for JavaScript or anchor links.

---

### The 7 Selector Types

```css
/* 1. Element Selector — targets all <p> tags */
p {
  color: #333;
}

/* 2. Class Selector — targets any element with class="card" */
.card {
  background: white;
  border-radius: 8px;
}

/* 3. ID Selector — targets the ONE element with id="header" */
#header {
  background: navy;
  color: white;
}

/* 4. Group Selector — applies same style to multiple elements */
h1, h2, h3 {
  font-family: Georgia, serif;
}

/* 5. Descendant Selector — targets <a> anywhere inside <nav> (any depth) */
nav a {
  text-decoration: none;
  color: white;
}

/* 6. Child Selector — targets ONLY direct <li> children of <ul> */
ul > li {
  list-style: square;
}

/* 7. Universal Selector — targets every single element on the page */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

---

### Child vs Descendant — Key Difference

```html
<div class="parent">
  <p>Direct child ← targeted by both</p>
  <section>
    <p>Nested deeper ← targeted by descendant only</p>
  </section>
</div>
```

```css
/* Descendant — matches BOTH paragraphs above */
.parent p { color: red; }

/* Child — matches ONLY the first paragraph */
.parent > p { color: blue; }
```

---

## Q3 — CSS Box Model

### What is the Box Model?

Every HTML element is rendered as a **rectangular box**. The CSS Box Model describes the four layers that make up this box, from the inside out:

```
┌──────────────────────────────┐  ← Margin (outside space)
│  ┌────────────────────────┐  │
│  │  Border                │  │
│  │  ┌──────────────────┐  │  │
│  │  │  Padding         │  │  │
│  │  │  ┌────────────┐  │  │  │
│  │  │  │  Content   │  │  │  │
│  │  │  └────────────┘  │  │  │
│  │  └──────────────────┘  │  │
│  └────────────────────────┘  │
└──────────────────────────────┘
```

| Layer | Description |
|---|---|
| **Content** | The innermost layer — where text, images, and child elements live |
| **Padding** | Space *inside* the border — between the content and the border |
| **Border** | A line that wraps around the padding and content |
| **Margin** | Space *outside* the border — pushes the element away from others |

---

### `content-box` vs `border-box`

```css
/* content-box (default) — padding and border ADD to the width */
/* A 300px box with 20px padding = 340px total width */
.box-default {
  box-sizing: content-box;
  width: 300px;
  padding: 20px; /* adds 40px extra */
}

/* border-box (professional standard) — padding and border are INCLUDED in the width */
/* A 300px box with 20px padding = still 300px total width */
.box-border {
  box-sizing: border-box;
  width: 300px;
  padding: 20px; /* included in 300px */
}
```

> ✅ **`border-box` is used in all professional projects** because it makes sizing predictable. You set a width and it stays that width.

**`margin: 0 auto`** centers a block-level element horizontally by splitting the available space equally on the left and right sides.

---

### Code Task — `.box` Component

```css
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid #333;
  margin: 16px;
  box-sizing: border-box;
  /* Total rendered width = exactly 300px */
  /* Content area = 300px - (20px × 2 padding) - (2px × 2 border) = 256px */
}
```

---

## Q4 — CSS Colors

### Five Ways to Define Color in CSS

| Format | Example | Notes |
|---|---|---|
| **Named** | `color: orange` | 140+ built-in color names |
| **HEX** | `color: #F97316` | Most common — 6 hex digits |
| **RGB** | `color: rgb(249, 115, 22)` | Red, Green, Blue (0–255) |
| **RGBA** | `color: rgba(249, 115, 22, 1)` | RGB + **Alpha** (transparency 0–1) |
| **HSL** | `color: hsl(24, 95%, 53%)` | Hue, Saturation, Lightness |

> 💡 **HEX** is the most commonly used format by developers because it's compact and universally supported by design tools like Figma.

---

### `opacity` vs `rgba` — What's the Difference?

```css
/* opacity: affects the ENTIRE element AND all its children */
.overlay {
  background: orange;
  opacity: 0.5; /* text inside also becomes semi-transparent */
}

/* rgba: affects ONLY the color property — children stay fully visible */
.overlay-rgba {
  background: rgba(249, 115, 22, 0.5); /* only background is transparent */
  /* text inside is still 100% opaque */
}
```

> **Key rule:** `opacity` fades everything including child elements. `rgba` only fades that specific color value — children are unaffected.

---

### Code Task — Orange `#F97316` in All 5 Formats

```css
.color-named   { color: orangered; }              /* closest named color */
.color-hex     { color: #F97316; }                /* HEX */
.color-rgb     { color: rgb(249, 115, 22); }      /* RGB */
.color-rgba    { color: rgba(249, 115, 22, 1); }  /* RGBA — A=1 means fully opaque */
.color-hsl     { color: hsl(24, 95%, 53%); }      /* HSL */
```

---

## Q5 — CSS Units

### CSS Unit Reference

| Unit | Relative to | Practical Use Case |
|---|---|---|
| `px` | Fixed — screen pixels | Borders, shadows, min-widths |
| `%` | Parent element's size | Fluid widths, responsive columns |
| `rem` | Root `<html>` font-size (default: **16px**) | Font sizes, spacing |
| `em` | **Parent** element's font-size | Nested components, buttons |
| `vh` | **V**iewport **H**eight (1vh = 1% of screen height) | Full-screen hero sections |
| `vw` | **V**iewport **W**idth (1vw = 1% of screen width) | Fluid typography |

---

### Golden Rules

- 🔤 **Font sizes** → use `rem` (scales with user's browser settings — better accessibility)
- 📐 **Widths** → use `%` or `rem` (flexible and predictable)
- 🖥️ **Full-screen sections** → use `vh` (always fills exactly the viewport)

> **Why `rem` over `px` for fonts?** If a user increases their browser's base font size (e.g., for accessibility), `rem` values scale up automatically. `px` stays fixed and ignores the user's preference.

---

### Code Task — Hero Section

```css
/* Hero Section */
.hero {
  height: 100vh;              /* full viewport height */
  max-width: 72rem;           /* max-width in rem — scales with root font size */
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
}

.hero h1 {
  font-size: clamp(2rem, 5vw, 4rem); /* scales with viewport width, min 2rem, max 4rem */
  line-height: 1.2;
}

.hero p {
  font-size: clamp(1rem, 2vw, 1.25rem);
}
```

---

## Q6 — CSS Specificity and the Cascade

### What is Specificity?

**Specificity** is the scoring system the browser uses to decide which CSS rule wins when multiple rules target the same element. Think of it as a point system.

### Specificity Score Table

| Selector Type | Score |
|---|---|
| Inline style (`style=""`) | **1000** |
| ID (`#id`) | **100** |
| Class (`.class`), attribute, pseudo-class | **10** |
| Element (`div`, `p`) and pseudo-element | **1** |
| Universal (`*`) | **0** |

> ⚠️ **`!important`** overrides everything, even inline styles. It bypasses the entire cascade. Use it as a last resort because it makes debugging very difficult.

---

### How the Cascade Works

The browser applies styles using three rules in order:

1. **Specificity** — Higher score wins
2. **Source Order** — If scores are equal, the rule written *later* in the CSS wins
3. **Inheritance** — Some properties (like `color`, `font-family`) are inherited by child elements automatically

---

### Code Task — Which Color Wins?

```html
<p id="intro" class="text">Hello</p>
```

```css
/* Rule 1 — Element selector: specificity = 1 */
p {
  color: gray;
}

/* Rule 2 — Class selector: specificity = 10 */
.text {
  color: blue;
}

/* Rule 3 — ID selector: specificity = 100 */
#intro {
  color: tomato;
}
```

**Winner: `color: tomato`** — because the ID selector has the highest specificity score (100 > 10 > 1).

> If two rules have the **same specificity**, the one that appears **last in the stylesheet** wins.

---

## Q7 — CSS Flexbox

### What is Flexbox?

**Flexbox** (Flexible Box Layout) is a **1-dimensional** layout system — it arranges items along either a row or a column. When you write `display: flex` on a container, it becomes a **flex container** and all its direct children become **flex items** that can be easily aligned, distributed, and sized.

**Block layout vs Flexbox:**
- Block layout stacks elements vertically and gives no easy way to align them
- Flexbox gives you precise control over direction, spacing, and alignment with just a few properties

---

### Core Flexbox Properties

```css
.container {
  display: flex;

  /* flex-direction — which axis items are placed on */
  flex-direction: row;          /* left to right (default) */
  /* flex-direction: column;    top to bottom */

  /* justify-content — alignment along the MAIN axis (horizontal in row) */
  justify-content: space-between; /* spread items with space between */
  /* other values: flex-start | flex-end | center | space-around | space-evenly */

  /* align-items — alignment along the CROSS axis (vertical in row) */
  align-items: center;          /* vertically center all items */
  /* other values: flex-start | flex-end | stretch | baseline */

  /* flex-wrap — allow items to wrap onto a new line */
  flex-wrap: wrap;              /* items wrap if they don't fit */

  /* gap — space between items (no need for margins!) */
  gap: 1rem;
}

/* flex: 1 — item grows to fill available space equally */
.flex-item {
  flex: 1; /* shorthand for flex-grow: 1, flex-shrink: 1, flex-basis: 0 */
}
```

---

### Centering Horizontally AND Vertically

```css
.center-everything {
  display: flex;
  justify-content: center; /* horizontal center */
  align-items: center;     /* vertical center */
  height: 100vh;
}
```

---

### Real-World Use Cases

1. **Navbar** — logo on the left, links on the right
2. **Card rows** — equal-height cards side by side that wrap on mobile

---

### Code Task — Flexbox Navbar

```html
<nav class="navbar">
  <div class="logo">MyBrand</div>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Projects</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

```css
.navbar {
  display: flex;
  justify-content: space-between; /* logo left, links right */
  align-items: center;            /* vertically centered */
  padding: 1rem 2rem;
  background: #1e1e2e;
}

.logo {
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
}

.nav-links {
  display: flex;
  gap: 2rem;           /* space between links */
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links a {
  color: #cdd6f4;
  text-decoration: none;
  font-size: 1rem;
  transition: color 0.2s;
}

.nav-links a:hover {
  color: #89b4fa;
}
```

---

## Q8 — CSS Pseudo-classes and Pseudo-elements

### The Difference

| | Pseudo-class | Pseudo-element |
|---|---|---|
| **Syntax** | Single colon `:` | Double colon `::` |
| **Purpose** | Style based on element **state** or **position** | Style a **virtual part** of an element |
| **Examples** | `:hover`, `:focus`, `:nth-child()` | `::before`, `::after`, `::placeholder` |

> `::before` and `::after` do **not** add real HTML elements — they are visual-only, generated by CSS. They require the **`content`** property to appear (even `content: ""` for decorative uses).

---

### Pseudo-classes

```css
/* :hover — when the user's mouse is over the element */
button:hover {
  background: orange;
  cursor: pointer;
}

/* :focus — when an element is focused (clicked or tabbed into) */
input:focus {
  outline: 2px solid #89b4fa;
  border-color: #89b4fa;
}

/* :nth-child() — target elements by position */
li:nth-child(2n)   { background: #f0f0f0; } /* every even item */
li:nth-child(3n)   { color: tomato; }        /* every 3rd item */
li:nth-child(odd)  { background: #fafafa; }  /* odd items */

/* :not() — target everything EXCEPT the match */
p:not(.highlight) {
  color: #555;
}
```

---

### Pseudo-elements

```css
/* ::before — inserts content BEFORE the element's content */
.featured::before {
  content: "★ ";
  color: gold;
}

/* ::after — inserts content AFTER the element's content */
.featured::after {
  content: " (Featured)";
  font-size: 0.8em;
  color: gray;
}

/* ::placeholder — styles the placeholder text of an input */
input::placeholder {
  color: #aaa;
  font-style: italic;
}
```

---

### Code Task — Button, Star, Placeholder

```html
<button class="btn">Click Me</button>

<ul>
  <li class="featured">Web Development</li>
  <li>Design</li>
  <li class="featured">JavaScript</li>
</ul>

<input type="text" placeholder="Enter your name...">
```

```css
/* Orange button on hover */
.btn {
  padding: 0.6rem 1.4rem;
  background: #333;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  transition: background 0.2s;
}

.btn:hover {
  background: orange;
}

/* Star before featured list items using ::before */
li.featured::before {
  content: "★ ";
  color: gold;
}

/* Grey placeholder text */
input::placeholder {
  color: #999;
  font-style: italic;
}
```

---

## Q9 — CSS Transitions and Animations

### Transitions vs Animations

| | Transition | Animation |
|---|---|---|
| **Trigger needed?** | ✅ Yes (hover, focus, class change) | ❌ No — plays automatically |
| **Keyframes?** | ❌ No | ✅ Yes (`@keyframes`) |
| **Loops?** | ❌ Not without JS | ✅ Yes (`animation-iteration-count: infinite`) |
| **Best for** | Hover effects, state changes | Page load effects, looping animations |

---

### Transition Shorthand

```css
/* transition: property  duration  timing-function  delay */
.button {
  transition: background 0.3s ease 0s;
}

/* Multiple transitions */
.card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
```

### Timing Functions

| Value | Behavior |
|---|---|
| `ease` | Starts fast, slows down at end (default) |
| `ease-in` | Starts slow, speeds up |
| `ease-out` | Starts fast, ends slow (most natural-feeling) |
| `linear` | Constant speed throughout |

---

### `@keyframes` and Animation Shorthand

```css
/* Define the animation */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Apply the animation */
.card {
  /* animation: name  duration  timing-function  delay  iteration  fill-mode */
  animation: fadeInUp 0.6s ease-out 0s 1 forwards;
}
```

**`animation-fill-mode: forwards`** — keeps the element at the final keyframe state after the animation ends. Without it, the element snaps back to its original style.

**`animation-iteration-count: infinite`** — the animation loops forever (useful for loading spinners, pulsing effects).

---

### Why `transform` and `opacity` are Faster

Animating `transform` and `opacity` only triggers the **compositing** step of the browser's rendering pipeline. Animating properties like `width`, `height`, or `margin` triggers **layout recalculation** — which is far more expensive and causes jank (choppy animation).

> ✅ Always animate `transform` (move/scale/rotate) and `opacity` (fade) for smooth 60fps animations.

---

### Code Task — Card with Hover Lift + Fade-In Animation

```html
<div class="card">
  <h2>Hello World</h2>
  <p>This card lifts on hover and fades in on load.</p>
</div>
```

```css
/* Page-load fade-in animation */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(24px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.card {
  width: 320px;
  padding: 2rem;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);

  /* Smooth hover transition */
  transition: transform 0.3s ease, box-shadow 0.3s ease;

  /* Fade-in on page load */
  animation: fadeInUp 0.6s ease-out forwards;
}

/* Hover: lift up and deepen shadow */
.card:hover {
  transform: translateY(-8px);
  box-shadow: 0 16px 32px rgba(0, 0, 0, 0.15);
}
```

---

## Q10 — Responsive Web Design

### Part A — Media Queries

A **media query** lets you apply CSS rules only when the screen meets a certain condition — like a minimum width. This is how websites adapt their layout for phones, tablets, and desktops.

**Syntax:**
```css
@media (min-width: 768px) {
  /* styles applied when screen is 768px or wider */
}
```

### Standard Breakpoints

| Breakpoint | Width | Device |
|---|---|---|
| Mobile (base) | `< 768px` | Phones |
| Tablet | `768px` | iPad and similar |
| Laptop | `1024px` | Laptops |
| Desktop | `1280px+` | Large screens |

---

### Part B — Mobile-First

**Mobile-First** means you write your **base CSS for mobile** and then use `min-width` media queries to add styles for larger screens.

```css
/* Base styles — mobile (no media query) */
.container { padding: 1rem; }

/* Tablet and up */
@media (min-width: 768px) {
  .container { padding: 2rem; }
}

/* Desktop and up */
@media (min-width: 1024px) {
  .container { padding: 4rem; }
}
```

**Why mobile-first is the industry standard:**
- Most web traffic is on mobile devices
- It forces you to prioritize essential content
- Progressive enhancement — start simple, layer complexity upward
- Smaller CSS files for mobile users (they don't download desktop styles)

**Desktop-First** uses `max-width` and works in reverse — you start with a full layout and strip it down. It often produces messier, heavier CSS.

---

### Part C — CSS Variables (Custom Properties)

**CSS Variables** (also called custom properties) let you store values in one place and reuse them anywhere. They're defined with `--` prefix and accessed via `var()`.

```css
/* Define in :root — globally available */
:root {
  --color-primary: #3b82f6;
  --color-bg: #ffffff;
  --color-text: #1e1e2e;
  var(--color, fallback) /* fallback used if --color is not defined */
}

/* Use anywhere */
.button {
  background: var(--color-primary);
  color: var(--color-bg);
}
```

**`var(--color)`** — uses the variable value.
**`var(--color, #333)`** — uses the variable value; falls back to `#333` if the variable isn't defined.

> ✅ Yes — JavaScript can **read and change** CSS variables:
> ```js
> document.documentElement.style.setProperty('--color-primary', '#f97316');
> ```

---

### Code Task — Design System + Dark Mode + Mobile-First Breakpoints

```css
/* =============================================
   ROOT — Design System Variables
   ============================================= */
:root {
  /* Colors */
  --color-bg: #ffffff;
  --color-surface: #f8fafc;
  --color-text: #1e293b;
  --color-text-muted: #64748b;
  --color-primary: #3b82f6;
  --color-primary-hover: #2563eb;
  --color-border: #e2e8f0;

  /* Typography */
  --font-base: 1rem;
  --font-lg: 1.25rem;
  --font-xl: 1.5rem;
  --font-2xl: 2rem;

  /* Spacing */
  --space-sm: 0.5rem;
  --space-md: 1rem;
  --space-lg: 2rem;
  --space-xl: 4rem;

  /* Border Radius */
  --radius: 8px;
}

/* =============================================
   DARK MODE — triggered by data-theme="dark"
   on the <html> or <body> element
   ============================================= */
[data-theme="dark"] {
  --color-bg: #0f172a;
  --color-surface: #1e293b;
  --color-text: #f1f5f9;
  --color-text-muted: #94a3b8;
  --color-primary: #60a5fa;
  --color-primary-hover: #93c5fd;
  --color-border: #334155;
}

/* =============================================
   BASE STYLES — Mobile First
   ============================================= */
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: var(--color-bg);
  color: var(--color-text);
  font-size: var(--font-base);
  font-family: 'Segoe UI', system-ui, sans-serif;
  line-height: 1.6;
  transition: background 0.3s ease, color 0.3s ease;
}

.container {
  width: 100%;
  padding: 0 var(--space-md); /* mobile: 1rem padding */
  margin: 0 auto;
}

.card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius);
  padding: var(--space-md);
}

h1 { font-size: var(--font-xl); }
h2 { font-size: var(--font-lg); }

.btn {
  background: var(--color-primary);
  color: white;
  padding: var(--space-sm) var(--space-md);
  border: none;
  border-radius: var(--radius);
  cursor: pointer;
  transition: background 0.2s ease;
}

.btn:hover {
  background: var(--color-primary-hover);
}

/* =============================================
   TABLET — 768px and wider
   ============================================= */
@media (min-width: 768px) {
  .container {
    padding: 0 var(--space-lg); /* more padding on tablet */
    max-width: 768px;
  }

  h1 { font-size: var(--font-2xl); }

  .card {
    padding: var(--space-lg);
  }
}

/* =============================================
   DESKTOP — 1024px and wider
   ============================================= */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
    padding: 0 var(--space-xl);
  }

  h1 { font-size: 3rem; }
}

/* =============================================
   SYSTEM DARK MODE — respects OS preference
   ============================================= */
@media (prefers-color-scheme: dark) {
  :root {
    --color-bg: #0f172a;
    --color-surface: #1e293b;
    --color-text: #f1f5f9;
    --color-text-muted: #94a3b8;
    --color-border: #334155;
  }
}
```

**Toggle dark mode with JavaScript:**
```js
// Add data-theme="dark" to <html> to activate dark theme
document.documentElement.setAttribute('data-theme', 'dark');

// Remove it to go back to light
document.documentElement.removeAttribute('data-theme');
```
