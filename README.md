# BattleSim.io

A high-performance 2D army simulation engine. Two factions — the Red Legion and the Blue Alliance — battle in real time using steering behaviors and a spatial-partitioning grid, all driven by a custom, zero-dependency Entity Component System (ECS) for handling large unit counts. Spawn soldiers, tanks, and archers, deploy hordes, and watch the simulation unfold on a PixiJS-rendered battlefield.

## Features

- Real-time 2D battle simulation with a fixed-timestep animation loop and live, throttled stat updates.
- Custom, zero-dependency ECS (`services/ecs.ts`) with worlds, entities, components, and queries (up to 10,000 entities).
- Spatial-partitioning grid for efficient neighbor lookups, enabling steering behaviors at scale (`services/simulation.ts`).
- Three unit types — Soldier, Tank, and Archer — each with distinct health, damage, attack speed, movement speed, range, and radius (`constants.ts`, `UNIT_STATS`).
- Deployment controls to spawn units in batches (e.g. +5 Soldiers, +1 Tank, +5 Archers, +50 Horde) for either team.
- Adjustable ally-overlap tolerance, pause/resume, and reset controls.
- Stats panel and a casualties/charting view (Recharts) for tracking the battle.
- Error boundary wrapping the canvas to survive runtime/library failures.
- Strategic Battle Advisor chat panel (note: the AI backend is currently offline/mocked — the `@google/genai` dependency has been removed, so advisor responses are placeholder text).

## Tech Stack

- React 18 + TypeScript
- Vite (dev server, build, preview)
- PixiJS for 2D rendering
- Recharts for battle statistics charts
- Custom in-repo ECS (no external ECS library)

## Getting Started

### Prerequisites

- Node.js

### Installation

```bash
npm install
```

### Run

```bash
npm run dev      # start the dev server (http://localhost:3000)
npm run build    # production build
npm run preview  # preview the production build
```

## Project Structure

```
.
├── App.tsx                       # Root component: engine init, render loop, UI wiring
├── index.tsx                     # React entry point
├── components/
│   ├── BattleCanvas.tsx          # PixiJS battlefield renderer
│   ├── ControlPanel.tsx          # Deployment / spawn / pause / reset controls
│   ├── StatsPanel.tsx            # Live battle stats
│   ├── BattleAdvisor.tsx         # Strategic advisor chat panel
│   └── ErrorBoundary.tsx         # Crash guard around the canvas
├── services/
│   ├── simulation.ts             # SimulationEngine: steering, spatial grid, combat
│   └── ecs.ts                    # Custom zero-dependency ECS
├── constants.ts                  # Canvas size, unit stats, team colors, ECS mappings
├── types.ts                      # Interfaces (UnitView, Particle, GameStats, ...)
└── metadata.json
```
