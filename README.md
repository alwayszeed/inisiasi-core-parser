# DBML Studio

> Bagian dari seri **DBML to Supabase (AI-powered)** — **Day 1** (inti parser DBML → JSON).

Next.js + Node.js project providing a basic parser from **DBML** (Database Markup Language) syntax to **JSON**.


## Structure

```
src/
  app/                    Next.js app router (UI + API routes)
    api/parse-dbml/       POST endpoint: parse DBML input
  lib/dbml/               Core DBML parser module
    tokenizer.ts           Lexer (comments, tokens)
    parser.ts             Recursive-descent parser
    types.ts              TypeScript types for the JSON output
    index.ts              Public exports
scripts/
  test-parse.ts           Example usage of the parser
```

## Usage

### Parser module

```ts
import { parseDBML } from "@/lib/dbml";

const result = parseDBML(`
Table users {
  id integer [pk, increment]
  username varchar(255) [not null, unique]
}
`);
console.log(JSON.stringify(result, null, 2));
```

### Development

```bash
npm install
npm run dev   # http://localhost:3000
npm run build
```

### Parse API

`POST /api/parse-dbml` with JSON body `{ "input": "<dbml>" }`.

## Supported (basic)

- `Table` (including schema-qualified and quoted names)
- Columns with types (`varchar(255)`, etc.) and attributes (`pk`, `not null`, `unique`, `increment`, `default`, `note`, `ref`)
- Inline and standalone `Ref`
- `Enum`
- `TableGroup`
- Comments (`//`, `/* */`)

JSON output includes tables, columns, refs, enums, table groups, and parse errors.

## Seri proyek (DBML to Supabase AI)

| Hari | Fokus | Repo |
|------|-------|------|
| Day 1 | Setup + core parser DBML | **repo ini** |
| Day 2 | Gemini API untuk SQL & RLS | [Integrasi Gemini API untuk SQL & RLS](https://github.com/alwayszeed/Integrasi-Gemini-API-untuk-SQL-RLS) |
| Day 3 | UI split-screen + export SQL | [Interactive Split-Screen UI](https://github.com/alwayszeed/Interactive-Split-Screen-UI) |
| Day 4 | Unit testing, demo GIF, dokumentasi | [Unit Testing, Demo & Dokumentasi](https://github.com/alwayszeed/Unit-Testing-Demo-Dokumentasi) |
