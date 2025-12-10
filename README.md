# DevOps Slide Decks & Workshop

This repository contains **PowerPoint slide decks** and guidance to run a practical DevOps workshop. It currently includes:

- `1_Introduction_to_DevOps.pptx` — overview of DevOps principles, culture, lifecycle, and benefits.
- `2_Basics_of_VCS_with_Git.pptx` — fundamentals of Git and version control.
- `3_Advanced_Git_Concepts.pptx` — branching strategies, rebasing, tags, and release workflows.

> Use these decks with the hands‑on labs below to help participants move from concepts to practice.

---

## Audience
- Software Engineers, SREs, QA, Ops/Platform Engineers, and Security Engineers.

## Prerequisites
- Basic command‑line familiarity.
- A GitHub account (or any Git server) with personal access token (PAT) if needed.
- **Git** and **VS Code** (or any editor) installed locally.
- Optional for labs: Docker Desktop.

## Tooling (recommended)
- **Version Control:** Git
- **Code Hosting:** GitHub
- **CI/CD:** GitHub Actions (can be adapted to GitLab CI or Azure DevOps)
- **Quality/Security (optional labs):** SonarQube, Trivy, OWASP Dependency‑Check
- **Observability (optional labs):** Prometheus, Grafana, OpenTelemetry

---

## Workshop Agenda

### One‑Day (6–7 hours)

**Module 1 — Foundations (60 min)**
- What & why of DevOps: culture, automation, feedback loops
- CALMS, DORA metrics, value stream thinking

**Module 2 — Git Basics (90 min)**
- Repos, commits, diffs, branching, merging
- Local/remote workflows; pull requests

**Lab 1 (45 min)**
- Initialize repo, write README, commit history
- Create feature branch, make changes, open a PR

**Lunch (45–60 min)**

**Module 3 — Advanced Git (60 min)**
- Rebase vs merge, tags & releases, trunk‑based dev vs GitFlow

**Lab 2 (45 min)**
- Resolve conflicts, squash merges, release tag

**Module 4 — CI/CD Primer (60 min)**
- Pipelines, artifacts, gates, progressive delivery (feature flags/canary)

**Lab 3 (45 min)**
- Add a simple CI workflow (build/test) with GitHub Actions

> Optional add‑ons if time remains: quick demo of DevSecOps checks and basic monitoring.

---

### Two‑Day (expanded)

**Day 1:** Foundations, Git Basics, Advanced Git, CI/CD Primer + Labs 1–3.

**Day 2:**
- **Module 5 — DevSecOps Intro (60 min)**: supply chain (SBOM), secrets hygiene, policy‑as‑code
- **Lab 4 (60–90 min)**: SAST/SCA in pipeline; generate SBOM; sign artifacts
- **Module 6 — Observability (60 min)**: logs/metrics/traces, SLOs & error budgets
- **Lab 5 (60–90 min)**: instrument a demo app; set simple alerts
- **Wrap‑up (30 min)**: measure outcomes, next steps

---

## Hands‑on Labs

### Lab 3 — Minimal CI Workflow (GitHub Actions)
Create `.github/workflows/ci.yml`:

```yaml
name: CI
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'

      - name: Install
        run: npm ci

      - name: Test
        run: npm test -- --ci

      - name: Archive test report
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: test-report
          path: coverage/**
```

> Replace Node.js steps with your stack (Java/Maven, Python/pytest, .NET, etc.).

### Lab 4 — Security Checks (optional)
- **SAST:** run static analysis (e.g., ESLint/flake8/CodeQL).
- **SCA:** scan dependencies (e.g., Trivy or OWASP Dependency‑Check).
- **SBOM:** generate SBOM (e.g., CycloneDX) and store as artifact.
- **Secrets:** enable secret scanning; use a vault and short‑lived tokens.

### Lab 5 — Observability (optional)
- Instrument app with metrics and traces; export to Prometheus/Grafana or OpenTelemetry collector.
- Define SLOs; track error budgets.

---

## How to Use These Decks
- Present decks in order: **Intro → Git Basics → Advanced Git**.
- Leave time after each module for Q&A and quick exercises.
- Encourage small, frequent commits and PRs throughout the day.

## Repository Structure
- Slide decks live in the root for quick access.
- Add lab materials under `labs/` (e.g., sample app, pipeline templates, SBOM scripts).

## Contributing
1. Open an issue describing the improvement or new deck.
2. Submit a PR with clear commit messages.
3. For new decks, use the naming pattern: `<sequence>_<short_topic_name>.pptx`
   - Examples: `4_CI_CD_Fundamentals.pptx`, `5_DevSecOps_Intro.pptx`.

## Roadmap
- `4_CI_CD_Fundamentals.pptx` — pipelines, artifacts, gates, progressive delivery.
- `5_DevSecOps_Intro.pptx` — SAST/DAST/SCA, SBOM, policy‑as‑code.
- `6_Observability_SLOs.pptx` — logs/metrics/traces, SLOs & error budgets.
- `7_Cloud_Native_DevOps.pptx` — containers, Kubernetes, GitOps.

## License
No license file is present yet. Add a `LICENSE` (e.g., MIT or Apache‑2.0) if you want others to reuse/modify these materials.

## Acknowledgments
Thanks to the DevOps community for concepts and examples that inform these materials.
