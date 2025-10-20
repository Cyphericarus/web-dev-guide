# Advanced Web Development: Best Practices & Resources

Focused, no-fluff guide to modern web development with battle-tested practices and essential resources.

---

## Table of Contents

1. [CSS Architecture](#-css-architecture)
2. [Performance Optimization](#-performace-optimization)
3. [Web Accessibility](#-web-accessibility)
4. [JavaScript Best Practices](#-javascript-best-practices)
5. [Testing & Quality](#-testing-&-quality)
6. [Developer Workflow](#-developer-workflow)
7. [SEO & Security](#-seo-&-security)
8. [Design Systems](#-design-systems)

---

## CSS Architecture

### Methodologies

**CUBE CSS** - Cascade-first, utilities + components. Best for modern projects.

**BEM** - Block, Element, Modifier. Clear naming, scalable to large teams.

**Tailwind** - Utility-first. High productivity, smaller unused code with PurgeCSS.

Pick one and stay consistent. CUBE and BEM scale best; Tailwind has steepest learning curve but highest velocity.

### Key Principles

- **Variables first:** `--color-primary`, `--space-unit`, `--font-family`
- **Single responsibility:** One component = one job
- **Minimize specificity:** Avoid selector wars
- **Performance:** CSS Grid/Flexbox over floats, lazy-load stylesheets

### Quick Example

```css
:root {
  --color-primary: #3b82f6;
  --space-unit: 1rem;
}

.card {
  background: white;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.card--featured {
  border: 2px solid var(--color-primary);
}
```

### Practice & Resources

- [Flexbox Froggy](https://flexboxfroggy.com/) - Game: master flexbox
- [CSS Grid Garden](https://cssgridgarden.com/) - Game: master grid
- [CUBE CSS](https://cube.fyi/) - Modern CSS architecture
- [Tailwind Docs](https://tailwindcss.com/docs) - Utility-first framework

---

## Performance Optimization

### Core Web Vitals (Google's metrics)

- **LCP (Largest Contentful Paint):** < 2.5s - optimize hero images, critical JS
- **FID (First Input Delay):** < 100ms - reduce main thread work
- **CLS (Cumulative Layout Shift):** < 0.1 - set image dimensions, avoid late-loading content

### Implementation

**Images:** Use WebP/AVIF with fallbacks, lazy-load below fold, use srcset for responsive images

**JavaScript:** Code split by route, defer non-critical scripts, tree-shake unused code

**Fonts:** Self-host (covered in main guide), use `font-display: swap`, subset characters

**Caching:** HTTP caching headers, service workers, CDN for static assets

### Audit & Resources

- [PageSpeed Insights](https://pagespeed.web.dev/) - Automated scoring
- [WebPageTest](https://www.webpagetest.org/) - Detailed waterfall analysis
- [Web.dev Performance](https://web.dev/performance/) - Complete guide with checklists

---

## Web Accessibility

### WCAG 2.1 Standards (AA level = minimum)

**Perceivable:** Alt text, sufficient color contrast (4.5:1 for text)

**Operable:** Keyboard navigation, focus visible, no seizure triggers

**Understandable:** Clear language, predictable navigation, error messages

**Robust:** Valid HTML, semantic markup, screen reader support

### Implementation

```html
<!-- Semantic first -->
<header>
  <nav aria-label="Main">
    <a href="/" aria-current="page">Home</a>
  </nav>
</header>

<!-- ARIA only when needed -->
<button aria-label="Close menu">✕</button>

<!-- Alt text describes purpose, not "image of" -->
<img src="hero.jpg" alt="Team celebrating project launch">
```

**Keyboard:** Tab order logical, interactive elements focusable, visible focus indicator

**Color:** Never rely on color alone, check contrast with tools

### Testing & Resources

- [Axe DevTools](https://www.deque.com/axe/devtools/) - Automated a11y audit
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) - WCAG compliance
- [NVDA Screen Reader](https://www.nvaccess.org/) - Free testing
- [WebAIM](https://webaim.org/) - Practical accessibility guides

---

## JavaScript Best Practices

### Code Quality

**Linting + Formatting:** ESLint catches bugs, Prettier enforces style. Non-negotiable.

**Comments:** Explain _why_, not _what_. Code should be self-documenting.

**Error Handling:** Try-catch async, never swallow errors silently.

```javascript
async function fetchData(url) {
  try {
    const res = await fetch(url);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    return await res.json();
  } catch (error) {
    console.error('Fetch failed:', error);
    throw error; // Let caller decide
  }
}
```

### Modern Patterns

**Destructuring, spread operator, template literals** - Use them.

**Promises/async-await** - Async-await for readability, handle rejections.

**Pure functions** - No side effects, easier to test and reason about.

**Const-first** - Use const, then let, never var.

### Resources

- [JavaScript.info](https://javascript.info/) - Interactive deep dive
- [MDN JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript) - Reference
- [Patterns.dev](https://www.patterns.dev/) - Design patterns

---

## Testing & Quality

### Coverage Strategy

**Unit tests:** 80%+ for critical logic. Use Jest or Vitest.

**Integration tests:** Test components + features together. 50-70% coverage.

**E2E tests:** Critical user paths only (20-30%). Use Cypress or Playwright.

```javascript
// Good test: tests behavior, not implementation
test('displays user name after data loads', () => {
  render(<UserCard user={mockUser} />);
  expect(screen.getByText(mockUser.name)).toBeInTheDocument();
});
```

### Best Practices

- Write testable code: small functions, separate logic from UI
- Test behavior, not implementation details
- Keep tests readable and maintainable
- Use test doubles (mocks/stubs) sparingly

### Resources

- [Testing Library](https://testing-library.com/) - Test behavior, not code
- [Jest Docs](https://jestjs.io/) - Unit testing framework
- [Cypress Docs](https://www.cypress.io/app) - E2E testing

---

## Developer Workflow

### Version Control

**Commits:** Follow [Conventional Commits](https://www.conventionalcommits.org/) format.

```
feat(auth): add JWT refresh token

Auto-refresh tokens to prevent session timeout.

Fixes #123
```

**Branching:** GitHub Flow (simple) or Git Flow (complex projects). Keep branches short-lived.

**Code Review:** Small PRs, meaningful descriptions, constructive feedback.

### Setup & Tools

**Package Manager:** npm, yarn, or pnpm. Use lock files.

**Build Tool:** Vite (fast dev, modern) or Webpack (flexible, learning curve).

**Environment:** Separate .env for dev/test/prod. Never commit secrets.

```bash
# .env.local (git-ignored)
VITE_API_URL=http://localhost:3000
DATABASE_PASSWORD=secret
```

### Resources

- [Git Docs](https://git-scm.com/doc) - Version control
- [Vite Docs](https://vitejs.dev/) - Next-gen build tool
- [npm Docs](https://docs.npmjs.com/) - Package management

---

## SEO & Security

### SEO Essentials

**Meta tags:** Title (50-60 chars), description (150-160 chars), canonical URLs

**Structured data:** Use Schema.org for rich snippets (articles, products, etc.)

**Semantics:** Proper heading hierarchy, descriptive link text, alt text for images

**Performance:** Page speed is a ranking factor. See Performance Optimization section.

```html
<head>
  <title>Best React Patterns (55 chars)</title>
  <meta name="description" content="Learn React patterns for scalable apps">
  <link rel="canonical" href="https://example.com/patterns">
</head>
```

### Security

**Prevent XSS:** Sanitize inputs, use CSP headers, avoid innerHTML with user data

**Prevent CSRF:** Use CSRF tokens, set SameSite cookies

**Dependency security:** `npm audit`, keep packages updated, use dependabot

**HTTPS:** Always. Use Let's Encrypt for free certificates.

**Headers:** Set Content-Security-Policy, X-Frame-Options, Strict-Transport-Security

```
Content-Security-Policy: default-src 'self'
X-Frame-Options: DENY
Strict-Transport-Security: max-age=31536000
```

### Resources

- [Google Search Central](https://developers.google.com/search) - SEO fundamentals
- [OWASP Top 10](https://owasp.org/www-project-top-ten/) - Security vulnerabilities
- [MDN Security](https://developer.mozilla.org/en-US/docs/Web/Security) - Security best practices

---

## Design Systems

### What & Why

Design systems ensure consistency across products. Core: components, tokens, patterns, guidelines.

**Design tokens:** Colors, spacing, typography, borders as CSS variables or JSON.

**Components:** Buttons, cards, modals—single responsibility, well-documented.

**Tools:** Figma (design), Storybook (development), Chromatic (visual testing).

### Building It

1. **Audit:** Document existing UI patterns, identify inconsistencies
2. **Tokens:** Define and export design tokens
3. **Components:** Build reusable, isolated components
4. **Document:** Storybook for showcase, do's/don'ts, accessibility notes

```css
/* Design tokens */
:root {
  --color-primary: #3b82f6;
  --color-danger: #ef4444;
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --font-family: system-ui, sans-serif;
}
```

### Resources

- [Storybook Docs](https://storybook.js.org/) - Component showcase + testing
- [Design Systems 101](https://www.nngroup.com/articles/design-systems-101/) - NN Group guide
- [Ant Design](https://ant.design/) - Enterprise design system example

---

## Quick Checklists

### Pre-Launch

- [ ] Lighthouse score > 90
- [ ] Mobile responsive (all breakpoints tested)
- [ ] WCAG AA compliance (contrast, keyboard, screen readers)
- [ ] Images optimized & lazy-loaded
- [ ] Unit tests > 80% coverage
- [ ] Security headers configured
- [ ] Sitemap & robots.txt created
- [ ] Analytics set up
- [ ] Error monitoring active
- [ ] Cross-browser testing done

### Code Quality

- [ ] ESLint clean
- [ ] Prettier formatted
- [ ] No console errors/warnings
- [ ] No debugger statements
- [ ] Error handling implemented
- [ ] No hardcoded values
- [ ] Comments explain "why"
- [ ] DRY principle followed

---

## Essential Resources

|Category|Resource|
|---|---|
|**Docs**|[MDN Web Docs](https://developer.mozilla.org/), [web.dev](https://web.dev/)|
|**Tools**|[Can I Use](https://caniuse.com/), [Chrome DevTools](https://developer.chrome.com/docs/devtools/)|
|**Community**|[Stack Overflow](https://stackoverflow.com/), [Dev.to](https://dev.to/)|
|**Practice**|[Frontend Mentor](https://www.frontendmentor.io/), [Codewars](https://www.codewars.com/)|

---

## Topics to Explore Next

TypeScript, React Hooks, Vue 3, Progressive Web Apps, Web Components, API design, CI/CD pipelines, Docker, headless CMS

---

**Last Updated:** October 2025 | _Keep learning, stay curious_ 🚀