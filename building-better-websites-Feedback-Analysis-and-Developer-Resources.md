# Building Better Websites: Feedback Analysis & Developer Resources

In every section, the concept is divided as example **Current Issue**, **Recommended Approach** and **Additional Points**

## Table of Contents

1. [Self-host Fonts](#self-host-fonts)
    
2. [Layout Shifts & Accessibility](#layout-shifts--accessibility)
    
3. [Semantic HTML](#semantic-html)
    
4. [BEM and Kebab-Style Class Naming](#bem-and-kebab-style-class-naming)
    
5. [CSS Reset](#css-reset)
    
6. [Site Responsiveness](#site-reponsiveness)
    
7. [The Clamp Calculator](#the-clamp-calculator)
    
8. [Design Accuracy](#design-accuracy)

---

## 1. Self-host Fonts

**Current Issue:** You're linking fonts from Google Fonts API using `<link>` tags in HTML. This method raises privacy concerns and may conflict with GDPR regulations.

**Current Implementation:**

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600&display=swap"
  rel="stylesheet"
/>
```

**Recommended Approach:** Self-host fonts using `@font-face` in CSS instead. This protects user privacy since files are 100% under your domain and not from third-party requests. Modern best practice is to explicitly use the woff2 font type.

**Implementation Steps:**

1. Download fonts from [Google Webfonts Helper](https://google-webfonts-helper.herokuapp.com/)
2. Add `@font-face` rules to your CSS:

```css
@font-face {
  font-display: swap;
  font-family: "Outfit";
  font-style: normal;
  font-weight: 300;
  src: url("./fonts/outfit-v15-latin-300.woff2") format("woff2");
}

@font-face {
  font-display: swap;
  font-family: "Outfit";
  font-style: normal;
  font-weight: 400;
  src: url("./fonts/outfit-v15-latin-regular.woff2") format("woff2");
}

@font-face {
  font-display: swap;
  font-family: "Outfit";
  font-style: normal;
  font-weight: 600;
  src: url("./fonts/outfit-v15-latin-600.woff2") format("woff2");
}
```

3. Add `<link rel="preload">` tags in HTML `<head>` for fonts used above the fold to reduce FOUT (Flash of Unstyled Text):

```html
<link
  rel="preload"
  href="./fonts/outfit-v15-latin-300.woff2"
  as="font"
  type="font/woff2"
  crossorigin
/>

<link
  rel="preload"
  href="./fonts/outfit-v15-latin-regular.woff2"
  as="font"
  type="font/woff2"
  crossorigin
/>

<link
  rel="preload"
  href="./fonts/outfit-v15-latin-600.woff2"
  as="font"
  type="font/woff2"
  crossorigin
/>
```

**Benefits:**

- Faster loading and better performance
- User privacy protection
- Reduced FOUT for better visual stability

**Additional Points:**

- While self-hosting requires more setup code, prioritize security and performance over code brevity
- The `font-display: swap` property ensures text remains visible while the font loads

**Useful Resources:**

- [Google Webfonts Helper](https://google-webfonts-helper.herokuapp.com/) - Simplifies font download and @font-face generation
- [Web Font Loader](https://github.com/typekit/webfontloader) - Advanced font loading strategies and optimization
- [GDPR and Web Fonts Guide](https://www.damiensegel.com/google-fonts-gdpr/) - Understanding privacy implications
- [Web.dev Font Loading Best Practices](https://web.dev/optimize-webfont-loading/) - Optimization guide

---

## 2. Layout Shifts & Accessibility

### Images

**Current Issue:** Missing `width` and `height` attributes on `<img>` elements causes cumulative layout shifts (CLS). Alt attributes are also not descriptive enough.

**Current Implementation:**

```html
<img
  src="images/image-equilibrium.jpg"
  class="card__nft-component__img"
  alt="NFT token picture"
/>

<img src="images/image-avatar.png" alt="" />
```

**Recommended Approach:** Add original dimensions to prevent layout shifts, then size with CSS. Use descriptive alt text for meaningful images.

**Implementation:**

```html
<img
  src="images/image-equilibrium.jpg"
  class="card__nft-component__img"
  alt="NFT token picture of Equilibrium #3429."
  width="604"
  height="604"
/>

<img
  src="images/image-avatar.png"
  alt="Profile picture of the NFT owner, Jules Wyvern."
  width="132"
  height="132"
/>
```

**Note:** If an image is purely decorative (e.g., icons), use an empty `alt=""` to hide it from screen readers.

### SVG Icons

**Current Issue:** Inline SVG icons don't have accessibility attributes to hide them from screen readers.

**Current Implementation:**

```html
<svg width="48" height="48" xmlns="http://www.w3.org/2000/svg">
  <!-- your svg code -->
</svg>
```

**Recommended Approach:** Use `aria-hidden="true"` for purely decorative SVG elements.

**Implementation:**

```html
<svg
  aria-hidden="true"
  width="48"
  height="48"
  xmlns="http://www.w3.org/2000/svg"
>
  <!-- your svg code -->
</svg>
```

**Additional Points:**

- Always specify width and height attributes on images to establish aspect ratio for browser rendering
- CLS affects Core Web Vitals, which impacts SEO rankings
- Descriptive alt text improves both accessibility and SEO

**Useful Resources:**

- [PerfectPixel Browser Extension](https://www.welldonecode.com/perfectpixel/) - Visual design-to-code comparison tool
- [Core Web Vitals Guide](https://web.dev/vitals/) - Understanding metrics that affect SEO and user experience
- [WCAG 2.1 Alt Text Guidelines](https://www.w3.org/WAI/tutorials/images/alttext/) - Comprehensive alt text standards
- [WebAIM Image Accessibility](https://webaim.org/articles/alttext/) - Practical alt text writing guide

---

## 3. Semantic HTML

**Current Issues:**

- Missing `<main>` element (required for semantic HTML)
- Using `<div>` instead of semantic tags like `<header>` and `<footer>`
- Incorrect heading hierarchy

**Recommended Changes:**

1. Replace `.section__cards` class with a `<main>` tag
2. Replace `.card__nft-component__container` with `<header>` tag
3. Move `.nft-component__content` inside the `<header>`
4. Wrap "Equilibrium #3429" with `<h1>` tag for correct heading hierarchy
5. Use `<footer>` tag instead of `<div>` for `.nft-component__author` class

**Benefits:**

- Makes HTML more meaningful and easier to understand
- Reduces confusion when inspecting code (especially for future you)
- Improves accessibility for screen readers
- Better SEO

**Additional Points:**

- Semantic HTML provides context to both browsers and developers
- Use semantic tags first; resort to `<div>` only when no semantic equivalent exists

**Useful Resources:**

- [MDN Semantic HTML Guide](https://developer.mozilla.org/en-US/docs/Glossary/Semantics) - Complete semantic elements reference
- [HTML5 Semantic Elements](https://www.w3schools.com/html/html5_semantic_elements.asp) - Interactive examples and use cases
- [WebAIM Semantic HTML for Accessibility](https://webaim.org/articles/semantichtml/) - How semantics improve accessibility
- [HTML Standard Elements Reference](https://html.spec.whatwg.org/multipage/semantics.html) - Official WHATWG specification

---

## 4. BEM and Kebab-Style Class Naming

**Current Status:** You're already using kebab-style naming and BEM approach, but there's room for simplification.

**Current Implementation Issues:**

```css
.section__cards { }
.card__nft-component { }
.card__nft-component__container { }
.card__nft-component__img { }
.nft-component__content a { }
.nft-component__content p { }
hr { }
.nft-component__author img { }
```

**Recommended BEM Structure:**

```css
.main { }
.card { }
.card__header { }
.card__image { }
.card__overlay { }
.card__title-link { }
.card__description { }
.card__divider { }
.card__footer { }
.card__profile-picture { }
```

**Key Improvements:**

- Simpler and easier to read class names
- Naming all elements with class names allows easier CSS targeting
- Avoids mixed targeting (selectors targeting both tags and classes) that can cause specificity issues
- Prevents confusion when scaling projects

**Naming Strategy:** Assign classes to most elements to target them specifically in CSS, rather than relying on tag selectors or descendant combinators.

**Additional Points:**

- BEM isn't about rigid adherence to conventions, but consistent application
- The goal is readability, scalability, and maintainability for long-term project management
- Refer to [this article](https://getbem.com/) for deeper BEM practice
- Also study approaches from creators like [Harry Roberts](https://csswizardry.com/)

**Useful Resources:**

- [BEM Official Documentation](http://getbem.com/) - Complete BEM methodology guide with examples
- [CSS-Tricks Guide to BEM](https://css-tricks.com/bem-101/) - Practical introduction to BEM naming
- [SMACSS Methodology](http://smacss.com/) - Alternative to BEM with focus on categorization
- [Specificity Visualizer](https://specificity.keegan.st/) - Understand CSS specificity issues

---

## 5. CSS Reset

**Current Implementation:**

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

**Recommended Enhanced Reset:**

```css
/* || RESET */
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

img,
picture,
video {
  display: block;
  max-width: 100%;
  height: auto;
}

input,
button,
textarea,
select {
  font: inherit;
  color: inherit;
  background: none;
  border-color: transparent;
}

a {
  text-decoration: none;
  color: inherit;
}

ul,
ol {
  list-style-type: none;
}
```

**What's Added:**

- Pseudo-elements (`::after`, `::before`) included for complete reset
- Media elements (images, videos) set to responsive by default
- Form elements inherit font and color from parent
- Links styled cleanly by default
- Lists stripped of default styling

**Recommended Resources:**

- CSS reset from [Andy Bell](https://www.joshwcomeau.com/css/custom-css-reset/)
- CSS reset from [Josh Comeau](https://www.joshwcomeau.com/css/custom-css-reset/)

**Important:** Understand each line of CSS reset code before implementing to maintain project control and avoid unintended side effects.

**Additional Points:**

- A well-crafted reset provides a consistent baseline across browsers
- Different projects may benefit from different reset levels depending on requirements

**Useful Resources:**

- [Josh Comeau's Custom CSS Reset](https://www.joshwcomeau.com/css/custom-css-reset/) - Modern, well-explained reset with annotations
- [Andy Bell's CUBE CSS](https://cube.fyi/) - Progressive enhancement approach with smart resets
- [Normalize.css](https://necolas.github.io/normalize.css/) - Alternative to reset; preserves useful browser defaults
- [Browser Default Styles](https://browserdefaultstyles.com/) - Visualize default browser styling across elements

---

## 6. Site Responsiveness

**Current Issues:**

1. At 320px viewport, the card appears squished and flushed to the sides
2. Over-reliance on `width` and `height` properties instead of fluid sizing
3. Desktop-first approach (should use mobile-first)

**Recommended Fixes:**

### Spacing Issue

Add padding and adjust spacing properties to provide breathing room on smaller screens.

### Fluid Sizing

Instead of:

```css
width: 300px;
height: 400px;
```

Use:

```css
width: 100%;
max-width: 300px;
height: auto;
```

This allows elements to scale with the viewport while respecting a maximum size.

### Mobile-First Approach

Write base styles for mobile, then add media queries for larger screens. This is cleaner and easier to maintain than desktop-first.

**Your Strengths:** You're already doing a great job with media query transitions and flex usage!

**Recommended Resource:** [Conquering Responsive Layouts: 21 Day Challenge](https://www.kevinpowell.co/courses/) by Kevin Powell - Free course to improve responsive design skills.

**Additional Points:**

- Mobile-first approach aligns with how most users browse (mobile-dominant traffic)
- Using `max-width` with `width: 100%` prevents overflow on small screens while maintaining design intent on large screens
- Flexbox is excellent for responsive layouts; consider also learning CSS Grid for more complex layouts

**Useful Resources:**

- [Web.dev Responsive Web Design Basics](https://web.dev/responsive-web-design-basics/) - Comprehensive guide
- [CSS Media Queries Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries) - MDN complete reference
- [Flexbox Complete Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) - CSS-Tricks interactive reference
- [CSS Grid Complete Guide](https://css-tricks.com/snippets/css/complete-guide-grid/) - CSS-Tricks interactive reference
- [Viewport Meta Tag Explained](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag) - Essential for mobile responsiveness
- [Container Queries](https://web.dev/container-queries/) - Modern alternative to media queries for component-based design

---

## 7. The Clamp Calculator

**Purpose:** Reduce dependency on media queries for responsive font sizing and spacing on larger projects.

**Tool:** [The Clamp Calculator](https://clamp.app/)

**Use Case:** The CSS `clamp()` function creates responsive values that scale smoothly between minimum and maximum sizes without needing multiple breakpoints.

**Application:**

- Font sizes
- Padding and margin
- Any other spacing properties

**Example:** Instead of multiple media queries, use:

```css
font-size: clamp(1rem, 2.5vw, 2rem);
```

**Additional Points:**

- `clamp()` accepts three values: (minimum, preferred, maximum)
- This approach is more elegant than managing numerous breakpoints
- Works well for scalable, fluid layouts across all viewport sizes

**Useful Resources:**

- [The Clamp Calculator](https://clamp.app/) - Visual tool to generate clamp() values
- [MDN clamp() Function](https://developer.mozilla.org/en-US/docs/Web/CSS/clamp) - Official CSS function reference
- [Fluid Typography with clamp()](https://web.dev/min-max-clamp/) - Web.dev guide on fluid sizing
- [clamp() vs Media Queries](https://chrisburnell.com/article/css-custom-properties-and-clamp/) - When to use clamp() vs breakpoints
- [Utopia - Fluid Type Scales](https://utopia.fyi/) - Generate entire fluid typographic scales
- [CSS Relative Units](https://web.dev/viewport-units/) - Understanding vw, vh, and relative units for clamp()

---

## 8. Design Accuracy

**Observation:** Your site is almost pixel-perfect when compared to the intended design. Great eye!

**For Future Projects:** Use [PerfectPixel](https://www.welldonecode.com/perfectpixel/) browser extension to help translate design images to code, even without a Figma file.

**Additional Points:**

- Design accuracy matters for user experience and professional presentation
- Tools like PerfectPixel help bridge the gap between design and implementation
- Even without exact tools, practicing visual comparison improves your eye for detail

**Useful Resources:**

- [PerfectPixel Browser Extension](https://www.welldonecode.com/perfectpixel/) - Visual overlay for pixel-perfect comparison
- [Figma to Code Plugins](https://www.figma.com/plugins/search?query=code) - Automate design-to-code conversion
- [Design Systems Guide](https://www.designsystems.com/) - Build scalable design systems
- [Color Contrast Analyzer](https://www.tpgi.com/color-contrast-checker/) - Ensure accessible color combinations
- [Storybook](https://storybook.js.org/) - Document and test design components

---

**Last Updated:** October 2025 | _Keep learning, stay curious_ 🚀

