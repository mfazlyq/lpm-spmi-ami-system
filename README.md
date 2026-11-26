# LPM & SPMI Quality Assurance System

A Laravel 11 + Vue 3/Inertia research and development prototype for higher-education internal quality assurance (SPMI), PPEPP monitoring, and internal quality audits (AMI).

> **Status:** Active development prototype. Not production-ready and not for official institutional records until security, privacy, authorization, backup, and policy requirements have been reviewed and tested.

## Main modules

- **PPEPP dashboard:** monitoring of Penetapan, Pelaksanaan, Evaluasi, Pengendalian, and Peningkatan.
- **AMI Prodi and Unit:** audit cycles, auditee self-evaluation (LED), auditor verification, assessment scoring, and status tracking.
- **Findings and corrective actions:** KTS and Observasi, root cause, corrective-action plan, responsible person, due date, and follow-up.
- **Master data:** study programs, work units, SPMI instruments, weights, target types, and rubrics.
- **Administration:** users, departments, roles, permissions, and activation state.

## Technology

| Layer | Stack |
|---|---|
| Backend | Laravel 11, PHP 8.2+ |
| Frontend | Vue 3, Inertia.js 2 |
| Styling | Tailwind CSS 4 |
| Build | Vite 5, Node.js 22 |
| Database | SQLite for local demo; Laravel database connection is configurable |
| Authorization | Laravel Auth, Spatie Laravel Permission |
| Tests | PHPUnit / Laravel feature tests |

## Run locally

Requirements: PHP 8.2+, Composer 2, Node.js 22+, npm, and PHP extensions required by Laravel including PDO SQLite.

```bash
git clone https://github.com/mfazlyq/lpm-spmi-ami-system.git
cd lpm-spmi-ami-system
composer install
cp .env.example .env
php artisan key:generate
```

On PowerShell, use `Copy-Item .env.example .env` instead of `cp`.

Create the local SQLite database file:

```bash
# macOS/Linux
touch database/database.sqlite
```

```powershell
# Windows PowerShell
New-Item -ItemType File -Path database/database.sqlite -Force
```

Run migrations and synthetic demo seeders:

```bash
php artisan migrate --seed
npm ci
npm run build
```

For local demo shortcuts only, set these values in `.env`:

```dotenv
APP_ENV=local
APP_DEBUG=true
APP_DEMO_MODE=true
INSTITUTION_EMAIL_DOMAIN=example.test
LPM_DEMO_PASSWORD=Choose-A-Strong-Local-Password
```

Never enable demo mode in a public or production environment, and never reuse the sample password for real accounts. If `LPM_DEMO_PASSWORD` is unset, the local seeder generates a random password and prints it once to the console.

Start the application in two terminals:

```bash
php artisan serve
npm run dev
```

Open `http://127.0.0.1:8000`.

## Demo roles

- **Super Admin LPM:** master data, users, instruments, and audit cycles.
- **Pimpinan:** quality workspace and leadership-level follow-up information.
- **Auditor Internal:** audit review, verification, and findings.
- **Auditee:** self-evaluation, evidence, and corrective-action responses.

Demo identities are synthetic role-based placeholders and are seeded only in `local` and `testing` environments.

## Data and security

- `.env`, application keys, database snapshots, logs, dependency folders, build artifacts, and original Git history are excluded.
- The sample institution is labelled **Universitas Demo**. Demo records use synthetic names and omit personal NIDN/NIP and phone values.
- Demo bypass and user switching are restricted to local/testing and require `APP_DEMO_MODE=true`.
- Never commit real user records, assessment data, audit evidence, accreditation documents, database snapshots, or credentials.
- This prototype has not undergone a full penetration test, privacy review, or production-readiness assessment.

## Tests

```bash
php artisan test
```

The GitHub Actions workflow installs PHP and Node dependencies, builds assets, prepares a temporary SQLite database, and runs Laravel tests. Review the Actions tab for the actual CI result.

## Project structure

```text
app/                 Laravel controllers, models, providers
bootstrap/           Laravel bootstrap configuration
config/              Application and service configuration
database/            Migrations and synthetic local demo seeders
resources/js/        Vue pages, layouts, and application interface
resources/css/       Application styling
resources/views/     Inertia root view and landing page
routes/              Web and console routes
tests/               Feature and unit tests
```

## Author

**M. Fazly Qusyairy**  
GitHub: https://github.com/mfazlyq
