# ETL Parser Project — Build Plan

A learning project: a data pipeline that ingests Electric Vehicle Population
Data (WA State DOL) from **either** an uploaded CSV **or** the Socrata API,
transforms/filters it, and loads it into a database — with a UI that triggers
each path and shows live progress.

> **Note to self:** This document stays at the level of *phases and decisions*.
> The architecture — class structure, interfaces, signatures — is mine to design.
> AI is the reviewer, not the author.

---

## Framing

This is not "a parser." It's an **ETL pipeline**: Extract → Transform → Load.
Parsing is only part of T. Thinking in ETL terms makes the structure fall out
on its own.

The two-source idea (CSV or API) is the core architectural exercise: two
implementations of the same Extract contract, with Transform and Load blind to
which one ran. If I can swap CSV for API without touching T or L, the layering
is real. If I can't, it was never separated.

**Data source:** Electric Vehicle Population Data (Washington State DOL),
~200k+ rows, ODbL 1.0 license. Same dataset exposed two ways:
- Full CSV download
- Socrata API (`data.wa.gov/api/views/f6w7-q2d2`) with `$limit`/`$offset` pagination

---

## Technology Stack

### Backend (known territory)
- **Java + Spring Boot** — core app
- **Spring Data JPA + PostgreSQL** — Load layer (my strong area; don't over-invest here)
- **JUnit 5 + Mockito** — tests

### New / rarely-used (the growth areas)
- **Spring Batch** *(optional, Phase 2.5)* — purpose-built ETL: reader → processor →
  writer, chunking, restart, progress tracking out of the box. Structurally enforces
  clean E/T/L separation. Introduce as a *rewrite* of a working engine, not the start.
- **Server-Sent Events (`SseEmitter`)** — one-way server→browser progress stream.
  Simpler than WebSocket and fits the progress-bar use case exactly.
- A **CSV parsing library** (e.g. a mature one) rather than hand-rolling — hand-rolled
  CSV parsing is the "write your own JSON parser" trap: complexity in the wrong place.

### Frontend (known territory)
- **React + TypeScript** — two buttons (Upload CSV / Parse from API), file upload control, progress bar
- **SSE client** — the one genuinely new piece on the frontend

### Tooling
- HTTP client for the Socrata API (Spring's `RestClient`/`WebClient`)
- Postgres locally (Docker is fine)

---

## Phase Plan

Ordered so each phase *proves something* before the next builds on it.

### Phase 0 — Paper (no code)
Define the **one contract** both sources satisfy and the **single type** they hand
downstream. Everything hangs off this. Skipping it means rewriting Phase 2.

### Phase 1 — CSV path, end to end, no UI
File → parse rows → one transform/filter → write to Postgres. Run from a test or
`main`. Goal: E→T→L working through the interface, on the simpler source.

### Phase 2 — API path as a second implementation
Add the Socrata client behind the **same** interface. Pagination lives here.
The test: wired in *without touching T or L*. If T/L had to change, Phase 0 was
wrong — fix the abstraction, don't patch around it.

### Phase 2.5 — (Optional) Spring Batch rewrite
Swap the hand-built engine for Batch if I want chunking/restart for free.
Deliberately *after* the architecture decisions are made by hand.

### Phase 3 — Orchestration + progress
A service that drives the pipeline and emits progress **without knowing about the
UI**. Decide how progress leaves the orchestrator (the SSE bridge).

### Phase 4 — UI
Two buttons (Upload CSV / Parse from API), file upload control, progress bar over
SSE. Frontend is familiar; new part is the SSE client and upload handling.

### Phase 5 — Hardening
Error handling (bad rows, API timeout, partial failure), tests, polish.

---

## Build Discipline

- **Build one source end-to-end first (CSV), then add the API.** Building both at
  once lets the interface bend to whatever I'm writing. The learning is in adding the
  *second* implementation and discovering whether the abstraction holds.
- **Sketch before code, every phase.** Rough design on paper, then AI as reviewer.

---

## Time Estimate

> Caveat: this estimate should really be mine to make — it's a separate skill, and
> it depends heavily on my pace on unfamiliar Socrata/SSE/Batch. Treat as a rough
> orientation, not a promise. Chop into 50–60 min focus blocks.

| Phase | Description | Estimate |
|------|--------------|----------|
| 0 | Paper: contract + shared type | 0.5–1h |
| 1 | CSV path, E→T→L, no UI | 6–10h |
| 2 | API path + pagination | 5–9h |
| 3 | Orchestration + progress plumbing | 4–7h |
| 4 | UI: 2 buttons, upload, SSE bar | 6–11h |
| 5 | Hardening, tests, polish | 8–14h |
| **Total** | **to a fully working version** | **~30–50h** |

Spring Batch (Phase 2.5) is extra and not in the total — it's a rewrite, not a
required step.

---

**Highest-leverage step: Phase 0.** Do it on paper, get the contract and shared
type right, and the rest of the build is mostly execution.

