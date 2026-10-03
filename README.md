# aocdev.org

Source code of **[aocdev.org](https://aocdev.org)**, the personal website and project catalogue of
Albert Ortells ([@aocdev](https://github.com/aocdev)).

The site is the public showcase of the open source Java tools and libraries I maintain. It has a
page for each project that explains what the project does, why it exists, and how to start using it.

---

## Table of Contents

- [Purpose](#purpose)
- [Featured Projects](#featured-projects)
- [Design Philosophy](#design-philosophy)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Running Locally](#running-locally)
- [Adding a New Project Page](#adding-a-new-project-page)
- [Backlog](#backlog)
- [Contributing](#contributing)
- [License](#license)

---

## Purpose

The website has three goals:

1. **Centralise** all my open source work in one place, so each project doesn't depend only on its
   GitHub README to be discovered.
2. **Explain** every project in depth: its motivation, main features, and how it fits into a real
   backend developer's workflow.
3. **Connect** the projects with each other and with the content I publish around them. Many of
   the tools are designed to work together.

---

## Featured Projects

| Project                | Description                                                                                                                                             | Repository                                                                |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| **JDocusaurus**        | Java annotation processor (APT) that generates deep microservice documentation in Docusaurus format at compile time. Zero runtime overhead.             | [aocdev/JDocusaurus](https://github.com/aocdev/JDocusaurus)               |
| **JRuntime-Inspector** | Lightweight, framework-agnostic runtime profiling library for the JVM. It produces a hierarchical Markdown report that shows where execution time goes. | [aocdev/jruntime-inspector](https://github.com/aocdev/jruntime-inspector) |

Each project has its own detail page on the site (`jdocusaurus.html`, `jruntime-inspector.html`).

---

## Design Philosophy

The site deliberately uses the look of **classic Javadoc** (roughly Java 1.4–1.6): navy section
bars, dense summary tables, serif body text and monospaced identifiers.

The choice is intentional:

- **It fits the audience.** Java developers recognise the style immediately.
- **It is content first.** No hero images, animations or trackers competing for attention; just
  structured information.
- **It is light and durable.** Plain HTML and CSS load instantly, work in any browser and need no
  maintenance to keep a build chain alive.

---

## Tech Stack

- **HTML5**: static pages, no templating engine.
- **CSS3**: a single shared stylesheet (`style.css`), with Flexbox for the page layout (so the
  footer stays at the bottom of the viewport).
- **No JavaScript, no build step, no dependencies.**
- **CI**: GitHub Actions checks formatting (Prettier), HTML validity (html-validate) and broken
  links (lychee) on every pull request. The tools run with `npx`, so the project stays
  dependency-free.

---

## Project Structure

```
aocdev.org/
├── .github/workflows/ci.yml  # CI: format, HTML and link checks
├── .github/dependabot.yml    # Weekly updates for GitHub Actions
├── index.html                # Home: About the author + project summary
├── jdocusaurus.html          # JDocusaurus detail page
├── jruntime-inspector.html   # JRuntime-Inspector detail page
├── style.css                 # Shared Javadoc-style stylesheet
├── README.md
├── CONTRIBUTING.md           # Contribution guidelines
├── LICENSE.md                # Apache License 2.0
├── .editorconfig             # Shared editor settings
├── .prettierrc               # Prettier formatting rules
├── .prettierignore           # Files excluded from formatting
├── .htmlvalidate.json        # HTML validation rules
└── .lycheeignore             # URLs excluded from the link check
```

Every page has the same skeleton:

```
<body>                  → flex column, min-height: 100vh
  .topnav               → top navigation bar
  .page-header          → title + subtitle
  .content              → main content (grows to fill the available space)
  .page-footer          → footer, always at the bottom of the page
</body>
```

---

## Running Locally

Because the site is fully static, you can open `index.html` directly in a browser.

To get behaviour closer to production (relative links, caching headers), serve the folder with any
static HTTP server, for example:

```bash
# Python 3
python3 -m http.server 8080

# Node.js
npx serve .
```

Then open <http://localhost:8080>.

---

## Adding a New Project Page

1. Copy one of the existing detail pages (e.g. `jruntime-inspector.html`) as a template.
2. Update the title, header, badges (`.meta-badge`), description and feature tables.
3. Add a new `.project-card` to the **Project Summary** section in `index.html` that links to the
   new page.
4. Reuse the existing CSS classes. Only add new rules to `style.css` when an existing component
   doesn't fit.

---

## Backlog

### 1. New project: AuthFromZero

**[AuthFromZero](https://github.com/aocdev/AuthFromZero)** will get its own detail page and card on
the site.

AuthFromZero is a production-grade **user management and authentication backend in Java**, built
from scratch using **Test-Driven Development (TDD)**. The whole development process is recorded and
explained as an educational content series.

Highlights, based on its Architecture Decision Records (ADRs):

- **Architecture:** modular monolith with Hexagonal Architecture (Ports & Adapters), DDD and
  Spring Modulith; modules communicate through domain events.
- **Authentication:** stateless JWT (short-lived access token + persisted refresh token), social
  login with Google and Facebook through Spring Security OAuth2, account linking, and `USER` / `ADMIN`
  roles.
- **Subscriptions & payments:** Free / Premium / Pro plans with monthly or yearly billing, trials,
  upgrades and downgrades; webhook-driven integration with Stripe, PayPal and Redsys, with
  idempotent event handling.
- **Data:** PostgreSQL with one schema per module and Flyway migrations; soft delete with
  GDPR-friendly permanent removal after 30 days.
- **Observability:** logs (ELK + Loki), metrics (Prometheus), dashboards (Grafana) and tracing
  (OpenTelemetry).
- **Dogfooding:** it is the real-world testbed for the other aocdev libraries:
    - **JDocusaurus** generates its documentation from annotations on controllers, entities, events
      and use cases.
    - **JRuntime-Inspector** profiles key use cases (registration, login, token refresh, plan
      changes, payment webhooks).

Tasks:

- [ ] Create `authfromzero.html` following the existing detail-page layout.
- [ ] Add the AuthFromZero card to the Project Summary in `index.html`.
- [ ] Link to the repository and, once available, the content series.

### 2. Web analytics for aocdev.org

Add analytics to **aocdev.org** to measure whether the open source projects are getting any
traction: visits, the most viewed project pages, traffic sources, and clicks through to the GitHub
repositories.

The goal is to make data-driven decisions about where to invest effort (which projects to
prioritise, what content to create).

Tasks:

- [ ] Choose an analytics solution, preferably lightweight and privacy-friendly to keep the
      spirit of the site.
- [ ] Add the tracking snippet to every page.
- [ ] Track outbound clicks to GitHub repositories as events.
- [ ] Review GDPR / cookie consent requirements for the chosen solution.

---

## Contributing

This is a personal website, but suggestions and corrections are welcome. Feel free to open an
issue or a pull request. Please read [CONTRIBUTING.md](CONTRIBUTING.md) first; it explains the
style guidelines, the branching strategy and the commit convention.

For contributions to the projects themselves, please go to their own repositories on
[github.com/aocdev](https://github.com/aocdev).

---

## License

This project is licensed under the [Apache License 2.0](LICENSE.md), the same license used by the
aocdev open source projects.
