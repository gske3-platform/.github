# GSKE³ Platform

**Internal platform for KGSK / Grün.Stadt.Klima e³** — five federated tools sharing one identity, one project record, one event bus.

> 🇩🇪 Regelkonforme Solar-Gründach-Planung von der Adresse bis zur Übergabe.
> Sovereign Hetzner hosting · German regulation citations · DGUV / DIN / FLL aware.

---

## 🧭 Start here

📘 **[platform-docs](https://github.com/gske3-platform/platform-docs)** — architecture, spine spec, rollout plan. Read this first.

---

## 🛠️ The five tools

| Repo | Role | Stack | Live |
|---|---|---|---|
| **[sgp](https://github.com/gske3-platform/sgp)** | Host application — feasibility planning, fall-protection, PV layout, ballast, report. Hosts the L1 spine. | FastAPI · React · Postgres + PostGIS | [sgp.kgsk.de](https://sgp.kgsk.de) |
| **[kgsk-brain](https://github.com/gske3-platform/kgsk-brain)** | Knowledge core — RAG, HOAI calculator, Fördercheck, draft generator, project memory, audit log | Next.js · Cloudflare Pages · D1 · Vectorize | [kgsk-brain.pages.dev](https://kgsk-brain.pages.dev) |
| **[gske3-heatstress](https://github.com/gske3-platform/gske3-heatstress)** | Per-building heat scoring (GPS) for ~5 M buildings, NRW + HH | FastAPI · React · Postgres + PostGIS | (Phase 3.3) |
| **[kgsk-foerdercheck](https://github.com/gske3-platform/kgsk-foerdercheck)** | Public lead-gen funding finder | Next.js · Cloudflare Pages | [foerdercheck.kgsk.de](https://foerdercheck.kgsk.de) |
| **[gske3-foerdercheck](https://github.com/gske3-platform/gske3-foerdercheck)** | Extraction bundle — source for the AI Greening Visualizer | Next.js | (archives in Phase 3.5) |

---

## 🔌 The L1 spine

Every tool talks to **four shared services** hosted at `sgp.kgsk.de/api/bus/*`:

- **Events** — append-only log: `project.created`, `project.feasibility_evaluated`, `geocode.seeded`, …
- **Geocode cache** — Photon-resolved addresses, shared across all tools
- **Building alias** — `sgp_building_id ↔ alkis_id` translation for cross-tool joins
- **Identity** — Entra OIDC (stub `amin@kgsk.de` until Peter completes the App registration)

Spec: [platform-docs/decisions/SPINE-2026-05-01-shared-services.md](https://github.com/gske3-platform/platform-docs/blob/main/decisions/SPINE-2026-05-01-shared-services.md)

---

## 📍 State of play (2026-05-01)

- ✅ **Live** — SGP at `sgp.kgsk.de` hosting the L1 spine; KGSK Brain at `kgsk-brain.pages.dev` emitting `project.created` events; Förder-Check at `foerdercheck.kgsk.de` as a satellite.
- 🔜 **Next** — Phase 3.1: Brain serves canonical Fördercheck JSON; the public Förder-Check switches to read from it. ~1 day.
- ⏸️ **Blocked on Peter** — Microsoft Entra App registration; the spine runs in stub-identity mode meanwhile.
- 🚧 **Not yet on a server** — GründachHeatStress (laptop-only; deploys in Phase 3.3 to `heatstress.kgsk.de`).

---

## 🏛️ Brand hierarchy

```
GSKE³ Platform   ← the umbrella (this org)
├── SGP                  Solar-Gründach Planner (the host app)
├── KGSK Brain           knowledge / drafts / regulation library
├── GründachHeatStress   per-building heat scoring
└── KGSK Förder-Check    public lead-gen
```

The **platform brand** (umbrella, what staff see) is *GSKE³ Platform*.
The **knowledge sub-tool inside it** is *KGSK Brain*. Don't merge them.

---

## 🤝 Contact

Maintainer: **Minka "Amin" Aduse-Poku** — [ma@kgsk.de](mailto:ma@kgsk.de)
Product owner: Peter Küsters · KGSK GmbH
