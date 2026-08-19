# Nexus BI

Institutional hospitality business intelligence — a sprawling "Financial Analyzer" Excel workbook reverse-engineered into a **multi-tenant SaaS platform**. Power-BI-class dashboards, an upload-anything ingestion pipeline with AI-assisted document extraction, built for hotel owners, management companies, and asset managers.

> Next.js 15 · React 19 · TypeScript · Supabase (Postgres + RLS) · Drizzle ORM. A unit-tested KPI engine ported straight from the source workbook's formula chains.

## Technologies

- `Next.js 15` (App Router)
- `React 19` + `TypeScript`
- `Tailwind CSS v4`
- `TanStack Table` + `Recharts`
- `Supabase` (Postgres, Auth, Storage, Edge Functions, RLS)
- `Drizzle ORM`
- `Zod` (validation) + `React Hook Form`
- `Vercel`

## 🚀 Features

- **Power-BI-class dashboards** — KPIs, revenue and RevPAR trends, market-segment mix, and benchmarks, built with composable widgets
- **Upload-anything ingestion** — PDFs, images, and spreadsheets are parsed into normalized rows, with period and scenario detection; documents get **AI-assisted extraction** via an edge function
- **A tested KPI engine** — the source workbook's formula chains rebuilt as pure functions, with a self-check test suite that verifies the output against known-good workbook numbers
- **Inbound email ingestion** — financial statements emailed in are auto-routed to the right property via plus-tag address parsing
- **Account mapping** — messy source labels are resolved to a canonical chart of accounts through aliases and patterns
- **Multi-tenant by design** — every table is organization-scoped and enforced with Postgres Row Level Security, not just hidden in the UI
- **Labor analytics** — daily labor facts carried against budget

## 🧭 Architecture

- **SQL migrations are canonical**; Drizzle provides fully typed queries on top of the same schema.
- **Row Level Security** scopes every row to its organization at the database layer, so tenant isolation holds no matter how the data is queried.
- **Edge Functions** handle AI document extraction server-side, keeping the model key off the client.
- **The KPI layer is pure, testable functions** — `kpi.ts` mirrors the workbook's formulas, and `kpi.test.ts` proves it matches the original numbers.

## 📍 The Process

The business ran its entire financial picture through one enormous Excel "Financial Analyzer" workbook — powerful, but a single file that couldn't scale past one analyst. I set out to turn it into a real product.

I reverse-engineered the workbook sheet by sheet, documenting every formula chain and mapping it to a proper relational schema (that mapping lives in the docs). The most satisfying part was rebuilding those formulas as a pure, unit-tested KPI engine that reproduces the workbook's numbers exactly — so I could trust the platform matched the spreadsheet it replaced. From there I built the ingestion pipeline: upload a PDF, an image, a spreadsheet, or even email a statement in, and it gets extracted, normalized, and mapped to the right accounts. The whole thing is multi-tenant from the ground up, with Postgres RLS enforcing organization isolation at the database.

## 📚 What I Learned

**🧮 Reverse-engineering domain logic:** Extracting years of embedded business rules from a spreadsheet and re-expressing them as tested, maintainable code.

**🔐 Multi-tenant data modeling:** Designing organization isolation with Postgres Row Level Security so it's enforced at the database, not the application.

**🤖 AI-assisted ingestion:** Building a pipeline that turns unstructured documents into normalized financial data behind a server-side edge function.

**✅ Correctness by construction:** Using a test suite that checks the KPI engine against known-good workbook outputs, so a refactor can never silently drift from the source of truth.

## 🚦 Running the Project

1. Clone the repository
2. Install dependencies: `npm install`
3. Copy `.env.example` to `.env.local` and fill in your own Supabase and API values
4. Run the dev server: `npm run dev`
5. Run the KPI test suite: `npm test`

## 🎬 Preview

<!-- Drag a screen recording (.mp4) or dashboard screenshots here. Use demo data only — no real property financials on screen. -->
