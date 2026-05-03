# NovaTech Solutions

Demo project for the **Advanced Claude Code** course on Pluralsight.

NovaTech Solutions is a fictional tech consultancy website built with plain HTML, CSS, and JavaScript — no frameworks. It serves as a hands-on learning environment for advanced Claude Code features including MCP (Model Context Protocol) server integration, subagents, Git worktrees, and Claude Code hooks.

---

## Table of Contents

- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Available Scripts](#available-scripts)
- [Design System](#design-system)
- [JavaScript Modules](#javascript-modules)
- [Code Conventions](#code-conventions)
- [Git Workflow](#git-workflow)
- [API Token Setup](#api-token-setup)
- [Figma Designs](#figma-designs)
- [Course Module Reference](#course-module-reference)
- [View Hidden Files](#view-hidden-files)
- [License](#license)

---

## Prerequisites

- [Node.js](https://nodejs.org/) 18 or higher
- [Git](https://git-scm.com/)
- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- A GitHub account (required for MCP integration modules)

---

## Quick Start

### 1. Clone and Install

```bash
git clone https://github.com/nyisztor/novatech-demo.git
cd novatech-demo
npm install
```

### 2. Start the Development Server

```bash
npm run dev
```

Then open your browser to: `http://localhost:3000/pages/index.html`

### 3. Launch Claude Code

In a separate terminal window, from the project root:

```bash
claude
```

---

## Project Structure

```
novatech-demo/
├── src/
│   ├── pages/                  # HTML pages
│   │   ├── index.html          # Homepage
│   │   ├── services.html       # Services offered
│   │   ├── portfolio.html      # Project portfolio with category filters
│   │   ├── team.html           # Team member profiles
│   │   └── contact.html        # Contact form
│   ├── css/
│   │   ├── variables.css       # Design tokens (colors, spacing, typography)
│   │   ├── base.css            # Global resets and base styles
│   │   ├── components.css      # Shared component styles
│   │   └── pages/              # Page-specific stylesheets
│   │       ├── home.css
│   │       ├── services.css
│   │       ├── portfolio.css
│   │       ├── team.css
│   │       └── contact.css
│   └── js/
│       ├── navigation.js       # Mobile navigation toggle
│       ├── contact-form.js     # Contact form submission and validation
│       ├── portfolio-filters.js # Portfolio category filtering
│       └── validation.js       # Reusable form validation utilities
├── tests/
│   ├── e2e/                    # Playwright end-to-end tests
│   └── unit/                   # Node.js unit tests
├── docs/                       # Design specs and API documentation
├── scripts/                    # Automation scripts (e.g., worktree setup)
├── .claude/
│   ├── agents/                 # Subagent definitions
│   ├── skills/                 # Custom agent skills
│   ├── commands/               # Slash command definitions
│   ├── enterprise-templates/   # Enterprise feature templates
│   └── settings.json           # Hooks configuration
├── .mcp.json                   # MCP server configuration
├── package.json
└── CLAUDE.md                   # Project conventions for Claude Code
```

---

## Tech Stack

| Technology | Purpose |
|---|---|
| HTML5 | Semantic page markup |
| CSS3 custom properties | Design tokens and styling |
| Vanilla JavaScript (ES6+ modules) | Interactive behavior |
| [Playwright](https://playwright.dev/) | End-to-end testing |
| Node.js built-in test runner | Unit testing |
| [ESLint](https://eslint.org/) | JavaScript linting |
| [Prettier](https://prettier.io/) | Code formatting |
| [serve](https://github.com/vercel/serve) | Local development server |

No frontend frameworks are used. The stack is intentionally simple to keep the focus on Claude Code features.

---

## Available Scripts

Run all commands from the project root (`novatech-demo/`).

| Script | Description |
|---|---|
| `npm run dev` | Start local development server on port 3000 |
| `npm run lint` | Lint JavaScript files with ESLint |
| `npm run lint:fix` | Lint and auto-fix JavaScript issues |
| `npm run format` | Format all HTML, CSS, and JS files with Prettier |
| `npm run format:check` | Check formatting without making changes |
| `npm run test` | Run all tests (unit and end-to-end) |
| `npm run test:unit` | Run unit tests with the Node.js test runner |
| `npm run test:e2e` | Run Playwright end-to-end tests |
| `npm run test:e2e:ui` | Run Playwright tests with the interactive UI |

Run tests before committing:

```bash
npm run test
```

---

## Design System

Design tokens are defined as CSS custom properties in `src/css/variables.css` and used across all stylesheets. This keeps visual decisions centralized and easy to update.

**Token categories:**

| Category | Example variables |
|---|---|
| Colors — Primary (Blue) | `--color-primary-500`, `--color-primary-700` |
| Colors — Secondary (Slate) | `--color-secondary-100`, `--color-secondary-800` |
| Colors — Accent (Teal) | `--color-accent-500`, `--color-accent-cyan` |
| Colors — Semantic | `--color-success-500`, `--color-warning-500`, `--color-error-500` |
| Typography | `--font-size-base`, `--font-weight-bold`, `--line-height-normal` |
| Spacing | `--spacing-4`, `--spacing-8`, `--spacing-16` |
| Layout | `--container-max-width`, `--container-padding` |
| Border radius | `--radius-sm`, `--radius-lg`, `--radius-full` |
| Shadows | `--shadow-sm`, `--shadow-md`, `--shadow-xl` |
| Transitions | `--transition-fast`, `--transition-base`, `--transition-slow` |
| Z-index | `--z-dropdown`, `--z-sticky`, `--z-modal` |

Always reference a token instead of a hard-coded value:

```css
/* Correct */
color: var(--color-primary-600);
padding: var(--spacing-4);

/* Avoid */
color: #2563eb;
padding: 1rem;
```

---

## JavaScript Modules

All modules use ES6 named exports and include JSDoc comments on every public function.

| Module | Exports | Description |
|---|---|---|
| `navigation.js` | `initNavigation` | Toggles the mobile nav menu; closes on outside click or Escape key |
| `contact-form.js` | `initContactForm` | Wires up form submission with validation and user feedback |
| `portfolio-filters.js` | `initPortfolioFilters` | Filters project cards by category using `data-filter` attributes |
| `validation.js` | `validateField`, `validateForm`, `isValidEmail`, `isValidPhone` | Reusable validation utilities for required fields, email, phone, and length constraints |

Each module auto-initializes when the DOM is ready, so no manual bootstrap call is needed on most pages.

---

## Code Conventions

### HTML

- Use semantic elements: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- Add ARIA labels to interactive elements for accessibility (targeting WCAG 2.1 AA)
- Keep each page under 200 lines

### CSS

- Follow BEM (Block, Element, Modifier) naming: `.block__element--modifier`
- Use tokens from `variables.css` — never hard-code color or spacing values
- Write styles mobile-first; use `min-width` media queries to scale up

### JavaScript

- Use ES6 modules with named exports — no default exports
- Add JSDoc comments to all public functions
- Declare no global variables

---

## Git Workflow

| Branch pattern | Purpose |
|---|---|
| `main` | Production-ready code |
| `feature/*` | New features |
| `bugfix/*` | Bug fixes |

**Commit message format:** `type: short description`

```
feat: add contact form validation
fix: correct mobile nav toggle
docs: update README setup instructions
chore: add code-review skill
```

**Pre-configured branches** (used in the Git Worktrees module):

- `feature/services-redesign` — Services page layout updates
- `feature/contact-form` — Form validation improvements
- `bugfix/responsive-nav` — Mobile navigation fixes

---

## API Token Setup

The GitHub and Figma MCP servers require API tokens. Set these as environment variables so credentials stay out of version control.

### GitHub Token

1. Go to [https://github.com/settings/tokens](https://github.com/settings/tokens)
2. Click **Generate new token (classic)**
3. Name it `Claude Code MCP` and select the `repo` and `read:org` scopes
4. Copy the generated token

Set the environment variable for your shell:

**macOS (zsh — default shell):**
```bash
echo 'export GITHUB_TOKEN=your_token_here' >> ~/.zshrc
source ~/.zshrc
```

**Linux (bash):**
```bash
echo 'export GITHUB_TOKEN=your_token_here' >> ~/.bashrc
source ~/.bashrc
```

**Windows (Command Prompt):**
```cmd
setx GITHUB_TOKEN "your_token_here"
```
Restart your terminal after running this command.

### Figma Token (Optional)

Required only for the Remote MCP Server integration. The Figma Desktop MCP uses OAuth and does not need a token.

1. Go to [https://www.figma.com/settings](https://www.figma.com/settings)
2. Scroll to **Personal access tokens** and click **Generate new token**
3. Name it `Claude Code MCP` and copy the token

**macOS (zsh):**
```bash
echo 'export FIGMA_ACCESS_TOKEN=your_token_here' >> ~/.zshrc
source ~/.zshrc
```

**Linux (bash):**
```bash
echo 'export FIGMA_ACCESS_TOKEN=your_token_here' >> ~/.bashrc
source ~/.bashrc
```

**Windows:**
```cmd
setx FIGMA_ACCESS_TOKEN "your_token_here"
```

**Verify both tokens are set:**
```bash
echo $GITHUB_TOKEN
echo $FIGMA_ACCESS_TOKEN
```

Once set, these variables persist across terminal sessions and Claude Code picks them up automatically on start.

---

## Figma Designs

For the Figma MCP integration modules, duplicate the NovaTech design file to your own Figma account:

**[NovaTech Solutions — Figma Design File](https://www.figma.com/design/UZ2t3sc5vi2cn9MXHkOfLY/NovaTech-Solutions?node-id=1-2&p=f)**

A free Figma account is all you need. Click the link, inspect the design, or duplicate it to your Drafts for an editable copy.

The file includes:
- Homepage (current design)
- Homepage — Updated (with design changes used in course demos)

This step is optional. You can follow the course videos without opening Figma, or practice MCP integration with your own design files.

---

## Course Module Reference

| Module | Feature | Key Files |
|---|---|---|
| 1 | MCP Server Integration | `.mcp.json` |
| 2 | Subagents | `.claude/agents/` |
| 3 | Git Worktrees | `scripts/setup-worktrees.sh` |
| 4 | Enterprise Features | `.claude/enterprise-templates/` |
| 5 | Agent Skills | `.claude/skills/` |
| 6 | Hooks | `.claude/settings.json` |

**Open pull requests** (used in MCP and GitHub integration demos):
- **PR #1** — Add client testimonials section
- **PR #2** — Update team page with new hires

---

## View Hidden Files

This project uses a `.claude/` directory for Claude Code configurations. It is hidden by default on most operating systems.

| Environment | How to show hidden files |
|---|---|
| macOS Finder | Press `Cmd + Shift + .` |
| Windows File Explorer | View > Show > Hidden items |
| VS Code | Hidden files are visible by default |
| Linux file manager | Press `Ctrl + H` or View > Show Hidden Files |
| Terminal (all platforms) | Use `ls -la` instead of `ls` |

---

## License

Educational project for Pluralsight. MIT licensed — see `package.json` for details.
