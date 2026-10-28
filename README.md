**English** | [Português](README.pt-BR.md)

# StockFlow

![StockFlow logo](assets/stockflow-logo.png)

![Next.js](https://img.shields.io/badge/Next.js-16-000000?logo=next.js&logoColor=white)
![React](https://img.shields.io/badge/React-19-149ECA?logo=react&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL%2017-3ECF8E?logo=supabase&logoColor=white)
![Electron](https://img.shields.io/badge/Electron-43-47848F?logo=electron&logoColor=white)

StockFlow is a desktop system I built to run the day-to-day operation of a small retail store. It brings point of sale, products, inventory, customers, store credit, exchanges, stock counts and NF-e (Brazilian electronic invoice) intake into a single Windows app.

This repository exists only to present the project in my portfolio. The source code, installer, database configuration and store data live in a private repository. The images on this page use empty fields or sample text.

## What the system does

- opens and closes the cash register each day;
- records sales with multiple payment methods, discounts and change;
- handles products sold by unit or by fraction;
- imports products and costs from NF-e XML files;
- calculates profit margins and lets you change the target margin in bulk;
- registers customers, purchases, store credit and payments;
- tracks exchanges, returns, stock counts and inventory movements;
- separates admin and cashier access;
- builds an installer and a portable version for Windows.

## Tech stack

| Area | Technology |
|---|---|
| Desktop app | Electron 43 |
| Interface | Next.js 16, React 19 and TypeScript 5 |
| Database and auth | Supabase and PostgreSQL 17 |
| Validation | Zod |
| Local state | Zustand |
| Animations | Framer Motion |
| Charts | Recharts |
| Tests | Vitest, Testing Library and Playwright |
| Packaging | electron-builder |

## Architecture

```mermaid
flowchart LR
    U[Windows user] --> E[Electron app]
    E --> N[Next.js interface]
    N --> A[Authentication]
    N --> D[PostgreSQL database]
    N --> S[File storage]

    subgraph Supabase
        A
        D
        S
    end
```

Electron opens the application in a desktop window, while Next.js renders the screens and handles user actions. Supabase is responsible for accounts, permissions and data. Operations that change sales or inventory run inside transactions to avoid half-written records.

A longer explanation is in [docs/architecture.md](docs/architecture.md) and more diagrams are in [docs/diagrams.md](docs/diagrams.md) (both in Portuguese).

## Project numbers

The numbers below come from the internal baseline of version 1.0.27.

| Item | Result |
|---|---:|
| TypeScript and TSX files | 236 |
| TypeScript and TSX lines, excluding tests | about 21.8k |
| Exported Server Actions | 67 |
| App Router screens | 16 |
| Vitest tests | 562 across 74 files |
| Playwright scenarios | 19 |
| Authenticated routes in the Electron smoke test | 12 |
| Visual matrix configurations | 5 |
| Applied migrations | 22 |
| Known vulnerabilities in `npm audit` | 0 |
| Commits scanned with Gitleaks during QA | 223 |

## Screens

These screenshots were taken on version 1.0.27. Empty states avoid exposing store information.

| Dashboard | POS with register closed |
|---|---|
| ![StockFlow dashboard](screenshots/dashboard.png) | ![POS with register closed](screenshots/pdv-caixa-fechado.png) |

| Catalog | Pricing and margins |
|---|---|
| ![Product catalog](screenshots/catalogo.png) | ![Pricing screen](screenshots/precificacao.png) |

| NF-e intake | Stock count and movements |
|---|---|
| ![NF-e import](screenshots/entradas-nfe.png) | ![Stock count and inventory](screenshots/inventario.png) |

| Customers | Store credit |
|---|---|
| ![Customer management](screenshots/clientes.png) | ![Store credit management](screenshots/fiados.png) |

| Sales history | Exchanges and returns |
|---|---|
| ![Sales history](screenshots/historico-vendas.png) | ![Exchanges and returns](screenshots/trocas.png) |

| Profile | Store settings |
|---|---|
| ![User profile](screenshots/perfil.png) | ![Store settings](screenshots/configuracoes.png) |

### One component across themes and sizes

| Dark theme | Light theme |
|---|---|
| ![Customer modal, dark theme](screenshots/modal-cliente-escuro.png) | ![Customer modal, light theme](screenshots/modal-cliente-claro.png) |

| Compact window | Wide screen |
|---|---|
| ![Modal in a compact window](screenshots/modal-cliente-compacto.png) | ![Modal on a wide screen](screenshots/modal-cliente-tela-ampla.png) |

The [screenshots](screenshots/) folder also includes the 150% scale check and the visual identity sheet.

## Decisions I made

- Price, stock and payments are validated in the database, not only in the interface.
- Operations that change several records run inside transactions.
- Shared components for buttons, forms, alerts and modals.
- Light and dark themes, keyboard navigation, focus management and reduced motion.
- Role-based permissions, with checks on the server and in the database.
- Next.js packaged together with Electron to deliver a native-feeling Windows app.

## Testing

On version 1.0.27 the project went through lint, TypeScript, build, unit tests, component tests and Playwright scenarios. Authenticated routes were also tested inside Electron, and the interface was checked across resolutions, scales and themes.

This version went beyond automated tests. Sales, cancellations, store credit, exchanges, stock counts and permissions were exercised against the real database, always inside a rolled-back transaction, and customer registration, opening and closing the register and NF-e import were walked through in the interface with a real browser. Two bugs showed up that would not have appeared otherwise: the checkout modal did not fit the height of a 15-inch laptop screen, and the register balance field appended to the existing value instead of replacing it, which blocked opening the register without saying why.

The summary is in [docs/quality.md](docs/quality.md). Operational details and full evidence stay in the private repository.

## Documentation (in Portuguese)

- [Architecture](docs/architecture.md)
- [Diagrams](docs/diagrams.md)
- [Interface and design system](docs/design-system.md)
- [Quality and testing](docs/quality.md)
- [Security decision](docs/security.md)

## About this repository

There is no executable code, credentials, migrations, installers or real data here. The material was separated to show the process and technical decisions without exposing the store's operation.

The project is proprietary. The images, brand and documentation are not licensed for reuse.
