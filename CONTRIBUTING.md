# Contributing to aocdev.org

Thank you for taking the time to look at the source code of [aocdev.org](https://aocdev.org)!

This is a personal website, but it is open source on purpose: if you find a typo, a broken link, an
accessibility problem or a way to make the site better, your help is welcome.

## Code of Conduct

This project adheres to the [Contributor Covenant v2.1](https://www.contributor-covenant.org/version/2/1/code_of_conduct/).
By participating, you are expected to uphold this code. Please report unacceptable behaviour via
[GitHub Issues](https://github.com/aocdev/aocdev.org/issues).

## What Kind of Contributions Are Welcome?

| Welcome                                                     | Please discuss first                         |
| ----------------------------------------------------------- | -------------------------------------------- |
| Typos, grammar and wording fixes                            | Redesigns or changes to the visual style     |
| Broken or outdated links                                    | New sections or pages                        |
| Accessibility improvements (contrast, semantics, alt texts) | Adding JavaScript, frameworks or build tools |
| Responsive / cross-browser layout fixes                     | Adding third-party scripts or services       |
| HTML validation and CSS cleanups                            |                                              |

> **Contributions to the projects themselves** (JDocusaurus, JRuntime-Inspector, AuthFromZero...)
> belong in their own repositories on [github.com/aocdev](https://github.com/aocdev), not here.
> This repository only contains the website that presents them.

## Reporting Issues

Before opening an issue, please check the [existing issues](https://github.com/aocdev/aocdev.org/issues)
to avoid duplicates.

When reporting a problem, include:

- **Page** where it happens (e.g. `jdocusaurus.html`)
- **Browser and OS** (e.g. Firefox 130 on Fedora, Safari on iOS 18)
- **Expected vs. actual** behaviour
- A **screenshot** if it is a visual issue

## Development Setup

The site is plain static HTML and CSS. There are no dependencies and no build step.

```bash
git clone https://github.com/aocdev/aocdev.org.git
cd aocdev.org

# Option 1: open index.html directly in your browser

# Option 2: serve it locally (closer to production)
python3 -m http.server 8080
```

Then open <http://localhost:8080>.

## Style Guidelines

The site intentionally imitates **classic Javadoc** (Java 1.4–1.6 era). Please keep that spirit:

- **Keep it static.** Plain HTML5 and CSS3. No JavaScript unless it has been agreed in an issue first.
- **Reuse the existing components.** Use the classes already defined in `style.css`
  (`.section-bar`, `.project-card`, `.meta-badge`, `.feature-list`, `.annot-table`, `.code-block`...) before
  creating new ones.
- **One stylesheet.** All styles live in `style.css`. Inline `style` attributes are not allowed
  (the HTML check fails).
- **Respect the page skeleton.** Every page follows the same structure:
  `.topnav` → `.page-header` → `.content` → `.page-footer`.
- **Formatting.** Handled by [Prettier](https://prettier.io/) (see `.prettierrc`). Run
  `npx prettier@3.9.9 --write .` before committing instead of formatting by hand.
- **Content language.** The site content is written in English.
- **Check your changes** in at least two browsers and at a mobile width before opening a PR.

## Automated Checks

Every pull request runs the [CI workflow](.github/workflows/ci.yml) on GitHub Actions. A PR can
only be merged when all checks pass:

| Check      | Tool                                        | What it validates                                         |
| ---------- | ------------------------------------------- | --------------------------------------------------------- |
| Formatting | [Prettier](https://prettier.io/)            | HTML, CSS, Markdown and YAML follow the project format    |
| HTML       | [html-validate](https://html-validate.org/) | Valid, well-formed markup (rules in `.htmlvalidate.json`) |
| Links      | [lychee](https://lychee.cli.rs/)            | No broken links in pages or documentation                 |

You can run the first two locally before opening a PR. Only Node.js is needed; nothing is
installed in the project:

```bash
npx prettier@3.9.9 --check .        # use --write to fix formatting
npx html-validate@11.16.1 "*.html"
```

## Branching Strategy (GitHub Flow)

1. **`main`** always reflects what is (or can be) published on aocdev.org.
2. Create a **branch** from `main`.
3. Open a **Pull Request** when ready.
4. After review, it is merged into `main`.

### Branch Naming

```
feat/short-description      # New page, section or component
fix/short-description       # Bug or layout fix
docs/short-description      # README, CONTRIBUTING, etc.
style/short-description     # Visual / CSS-only changes
```

Examples:

```
feat/authfromzero-page
fix/footer-overlap-on-mobile
docs/update-backlog
style/improve-table-contrast
```

## Commit Convention

We follow [Conventional Commits v1.0.0](https://www.conventionalcommits.org/en/v1.0.0/).

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

### Types

| Type       | Description                                                   |
| ---------- | ------------------------------------------------------------- |
| `feat`     | New page, section or visible feature                          |
| `fix`      | Bug fix (broken link, layout issue, wrong content)            |
| `docs`     | Repository documentation only (README, CONTRIBUTING, LICENSE) |
| `style`    | Visual changes in CSS that don't change content or structure  |
| `refactor` | Markup / CSS restructuring without visible changes            |
| `perf`     | Loading or rendering performance improvements                 |
| `chore`    | Maintenance (`.gitignore`, config files...)                   |
| `revert`   | Reverts a previous commit                                     |

### Scopes (optional)

- `home`: `index.html`
- `jdocusaurus`: `jdocusaurus.html`
- `jruntime-inspector`: `jruntime-inspector.html`
- `css`: `style.css`
- `analytics`: analytics integration

### Examples

```
feat(home): add AuthFromZero project card

fix(jdocusaurus): correct broken link to Docusaurus docs

style(css): increase contrast of section bars

docs: add analytics item to backlog
```

## Pull Request Process

1. **Open an issue first** for anything in the "Please discuss first" column above.
2. **Branch from `main`** and keep the PR focused on a single change.
3. **Follow the commit convention** described above.
4. **Describe your change** in the PR: what, why, and screenshots (before/after) for visual changes.
5. **Verify** that the pages render correctly and that all links work.

### PR Checklist

```markdown
## Summary

Brief description of the change.

## Related Issue

Closes #123

## Checklist

- [ ] Tested in at least two browsers
- [ ] Tested at mobile width
- [ ] No new JavaScript or external dependencies (or agreed in an issue)
- [ ] Existing CSS classes reused where possible
- [ ] Conventional Commits followed
- [ ] CI checks pass (formatting, HTML, links)
- [ ] Screenshots attached (visual changes)
```

## License

By contributing, you agree that your contributions will be licensed under the
[Apache License 2.0](LICENSE.md), the same license that covers this project.

Thank you for contributing!
