# ✅ Pre-Launch Checklist

A final, no-nonsense validation guide before you ship a website or web app to production.  
Run through this list to ensure **performance, accessibility, security, and quality** are all ready.

---

## ⚡ Performance

- [ ] **Lighthouse Score ≥ 90** (Desktop & Mobile)
- [ ] **Core Web Vitals** in green (LCP < 2.5s, CLS < 0.1, INP < 200ms)
- [ ] Assets minified and compressed (CSS, JS, HTML)
- [ ] **Images optimized** (next-gen formats: AVIF/WebP)
- [ ] **Lazy loading** for below-the-fold images
- [ ] Proper caching strategy (`Cache-Control`, `ETag`)
- [ ] Avoid render-blocking scripts & CSS
- [ ] Use CDN for static assets
- [ ] Critical CSS inlined for above-the-fold content

### 🔍 Tools
- [PageSpeed Insights](https://pagespeed.web.dev/)
- [WebPageTest](https://www.webpagetest.org/)
- [GTmetrix](https://gtmetrix.com/)
- [Chrome Lighthouse](https://developer.chrome.com/docs/lighthouse/)

---

## ♿ Accessibility (a11y)

- [ ] Meets **WCAG 2.2 AA** standards
- [ ] **Keyboard navigation** fully functional
- [ ] **Color contrast** ratio ≥ 4.5:1
- [ ] All images have `alt` attributes
- [ ] ARIA roles & labels correctly used
- [ ] Forms have accessible labels and validation
- [ ] Focus states visible and clear
- [ ] Tested with screen reader (NVDA, VoiceOver)

### 🔍 Tools
- [Axe DevTools](https://www.deque.com/axe/devtools/)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Accessibility Insights](https://accessibilityinsights.io/)
- [Wave Tool](https://wave.webaim.org/)

---

## 🔒 Security & SEO

- [ ] HTTPS enabled and enforced
- [ ] Security headers configured (`Content-Security-Policy`, `X-Frame-Options`, etc.)
- [ ] No mixed content (HTTP resources on HTTPS pages)
- [ ] Form data validated and sanitized
- [ ] No exposed API keys or secrets
- [ ] **Sitemap** and **robots.txt** present
- [ ] **Meta tags** (title, description, viewport) defined
- [ ] **Open Graph / Twitter Cards** configured
- [ ] **Structured data (JSON-LD)** validated

### 🔍 Tools
- [SecurityHeaders.com](https://securityheaders.com/)
- [Google Search Console](https://search.google.com/search-console/)
- [OpenGraph.xyz](https://www.opengraph.xyz/)
- [Schema.org Validator](https://validator.schema.org/)

---

## 🧪 Functionality

- [ ] All navigation and internal links work
- [ ] No broken images or 404 pages
- [ ] Forms submit successfully with validation
- [ ] Third-party scripts load correctly
- [ ] Error boundaries implemented (for SPAs)
- [ ] Responsive at all breakpoints (320px → 1440px+)
- [ ] Dark/light mode works (if applicable)

### 🔍 Tools
- [Responsively App](https://responsively.app/)
- [BrowserStack](https://www.browserstack.com/)
- [Pesticide for Chrome](https://chrome.google.com/webstore/detail/pesticide-for-chrome/)

---

## 🧰 Deployment

- [ ] Build pipeline tested (CI/CD)
- [ ] Version bump and changelog updated
- [ ] Environment variables configured correctly
- [ ] 404 and 500 error pages present
- [ ] Favicons and app icons verified
- [ ] Analytics & monitoring (GA, Sentry, etc.) integrated
- [ ] Backup or rollback plan in place

---

### 🏁 Final Check
Run one last full test in **incognito mode**, **mobile viewport**, and **slow network (3G)** to catch performance and layout regressions before launch.

---

**Ship with confidence 🚀**
**Last updated:** October, 2025