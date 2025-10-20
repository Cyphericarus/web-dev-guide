# 🧠 Code Quality Checklist

Maintain clean, consistent, and maintainable code throughout your project lifecycle.  
Use this list for **code reviews, pre-commit validation, and CI/CD enforcement**.

---

## 🧹 Code Hygiene

- [ ] Code follows agreed style (ESLint, Prettier)
- [ ] No unused imports, variables, or functions
- [ ] No console logs, `debugger`, or commented-out code
- [ ] Proper indentation and line spacing
- [ ] No inline styles (unless intentional)
- [ ] Code modularized — each function/component has one responsibility
- [ ] File/folder naming consistent (lowercase-kebab-case for assets, PascalCase for components)
- [ ] Avoid hard-coded constants (use config/env files)

### 🔍 Tools
- [ESLint](https://eslint.org/)
- [Prettier](https://prettier.io/)
- [EditorConfig](https://editorconfig.org/)

---

## 🧱 HTML & Accessibility

- [ ] Semantic HTML elements used appropriately (`header`, `main`, `nav`, `footer`)
- [ ] Headings follow a logical hierarchy (`h1` → `h6`)
- [ ] All interactive elements are keyboard-accessible
- [ ] `aria-*` attributes used only when necessary
- [ ] Forms have `label` or `aria-label`
- [ ] Image `alt` text descriptive and relevant
- [ ] No duplicate IDs in DOM

---

## 🎨 CSS & Styling

- [ ] Consistent naming convention (BEM, CUBE, or Tailwind)
- [ ] Variables used for colors, typography, and spacing
- [ ] Avoid deep nesting (>3 levels)
- [ ] Use utility classes when appropriate
- [ ] Responsive design tested on all breakpoints
- [ ] CSS reset or normalize applied
- [ ] No unused or duplicate selectors
- [ ] Animations performant (use `transform`, not layout-affecting properties)

### 🔍 Tools
- [Stylelint](https://stylelint.io/)
- [CSS Stats](https://cssstats.com/)
- [PurgeCSS](https://purgecss.com/)

---

## ⚙️ JavaScript / TypeScript

- [ ] Variables and functions named descriptively
- [ ] Functions are pure and reusable where possible
- [ ] No implicit type conversions
- [ ] Proper error handling (`try...catch`, fallback UI)
- [ ] Async operations handled (Promises, async/await)
- [ ] Code DRY — avoid repetition
- [ ] Use `const` and `let` appropriately
- [ ] API calls centralized (e.g., `/services` or `/api` folder)

### 🔍 Tools
- [SonarLint](https://www.sonarlint.org/)
- [TypeScript](https://www.typescriptlang.org/)
- [JS Hint](https://jshint.com/)

---

## 🧪 Testing

- [ ] Unit tests for core logic
- [ ] Integration tests for API and components
- [ ] End-to-end tests for user flows
- [ ] Mock data for consistent testing
- [ ] Test coverage ≥ 80%
- [ ] All tests pass in CI
- [ ] Use descriptive test names

### 🔍 Tools
- [Jest](https://jestjs.io/)
- [React Testing Library](https://testing-library.com/)
- [Cypress](https://www.cypress.io/)
- [Playwright](https://playwright.dev/)

---

## 🚀 CI/CD & Git Practices

- [ ] Pre-commit hooks enforce lint/test
- [ ] Conventional commit messages (`feat:`, `fix:`, etc.)
- [ ] Feature branches follow naming pattern (`feature/`, `bugfix/`)
- [ ] Pull requests reviewed before merge
- [ ] Automated tests & lint run in CI
- [ ] Deployment environment variables secured
- [ ] Changelog and version bump in each release

### 🔍 Tools
- [Husky](https://typicode.github.io/husky/)
- [Lint-Staged](https://github.com/okonet/lint-staged)
- [Commitlint](https://commitlint.js.org/)
- [GitHub Actions](https://github.com/features/actions)
- [GitLab CI/CD](https://docs.gitlab.com/ee/ci/)

---

### 🏁 Final Review

✅ All lint/test checks green  
✅ Code readable without explanations  
✅ Pull Request reviewed by a peer  
✅ Code ready to deploy or merge safely  

---

**Write clean. Test often. Ship confidently.** 🚀

**Last updated:** October, 2025
