# OpenVScan

OpenVScan is a web-based vulnerability scanner that integrates open-source tools with AI to deliver smarter, faster and more reliable pre-production security testing.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![GitHub stars](https://img.shields.io/github/stars/Buddhsen-tripathi/openvscan.svg?style=social\&label=Star)](https://github.com/Buddhsen-tripathi/openvscan)
[![Hacktoberfest](https://img.shields.io/badge/Hacktoberfest-2025-orange.svg)](https://hacktoberfest.com/)
[![GitHub issues](https://img.shields.io/github/issues/Buddhsen-tripathi/openvscan.svg)](https://github.com/Buddhsen-tripathi/openvscan/issues)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)](https://github.com/Buddhsen-tripathi/openvscan/actions)

---

## Planned Architecture

| Tier         | Stack                                 | Responsibilities                                        |
| ------------ | ------------------------------------- | ------------------------------------------------------- |
| UI (`web/`)  | Next.js 15, React 19, Tailwind CSS    | Scan setup, dashboards, reporting, multi-tenant UX      |
| API (`api/`) | NestJS 11, TypeScript, PostgreSQL ORM | Projects, auth, scan orchestration, findings API        |
| Workers      | Containerized runners + message queue | Execute scanners, aggregate artifacts, stream telemetry |
| Storage      | PostgreSQL, object storage, Redis     | Metadata, artifacts, coordination primitives            |
| AI Services  | LLM providers                         | Summaries, deduplication, remediation guidance          |

---

## Repository Layout

```
openvscan/
├── api/                 # NestJS 11 service (REST + background jobs)
├── web/                 # Next.js 15 / React 19 application
├── deploy/              # charts and infra manifests
├── docker/              # Local development containers & scripts
├── packages/            # Shared libraries (future)
├── scripts/             # Tooling, scanner runners, automation
├── pnpm-workspace.yaml  # Workspace config
└── README.md
└── LICENSE
```

---

## Installation

```bash
git clone https://github.com/your-username/openvscan.git
cd openvscan
pnpm install
```

This repository uses **pnpm workspaces**. Use the correct package name when running project-specific commands:

* `openvscan-api` → backend (NestJS)
* `openvscan-web` → frontend (Next.js)

---

## Environment Configuration

1. Duplicate the root environment file:

   ```bash
   cp .env.example .env
   ```
2. Populate service-specific overrides:

   * `api/.env` → NestJS backend
   * `web/.env.local` → Next.js UI

---

## Running Locally

### Full Stack (Docker)

```bash
docker compose up --build
```

* UI → [http://localhost:3000](http://localhost:3000)
* API → [http://localhost:5000](http://localhost:5000)

---

### API Only

```bash
pnpm --filter openvscan-api start:dev
```

* Hot reload via Nest CLI
* Swagger (if enabled) at `/docs`

---

### Web UI Only

```bash
pnpm --filter openvscan-web dev
```

* Next.js dev server proxies API requests to `http://localhost:5000`

---

## Usage (Vision)

1. Upload a target (artifact, URL, or Git connection).
2. Select scanners (static analysis, dependency audit, DAST, container checks).
3. Run the pipeline and let AI triage surface critical issues.
4. Review findings in the dashboard and apply recommended fixes.
5. Export reports (JSON, SARIF, PDF) for stakeholders.

---

## Example Outcomes (Planned)

* Critical findings (SQL injection, XSS, RCE, SSRF).
* Dependency exposure reports (outdated/vulnerable packages).
* Infrastructure misconfiguration insights (Kubernetes, Terraform).
* AI-enhanced remediation with code snippets & context.

---

## Testing & Quality (Planned)

```bash
pnpm lint
pnpm test
pnpm --filter openvscan-api test
pnpm --filter openvscan-web test
pnpm test:e2e
pytest tests/workers
```

Static analysis (`pnpm --filter openvscan-api lint`) and formatting (`pnpm format`) will enforce workspace standards.

---

## Contributing

1. Fork the repository & create a feature branch.
2. Run `pnpm lint` and `pnpm test` before opening a PR.
3. Include screenshots/recordings for UI-facing changes.
4. Reference linked issues and follow the [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md).

---

## License

Licensed under the Apache License 2.0. See [LICENSE](./LICENSE) for terms.

---

## Acknowledgements

OpenVScan builds on trusted open-source security tools (e.g., OWASP ZAP, Nmap, Trivy) and layers AI-driven analysis to make vulnerability scanning more effective and accessible.
