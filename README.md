# 🌱 Productivity Garden

A frontend-only productivity app where tasks are seeds you plant in a virtual garden. Each plant grows over time based on its deadline. Complete your tasks before they expire — or watch them wither.

> No backend. No build tools. No dependencies. Just open the file and start planting.

---

## 🚀 Getting Started

No installation required.

1. Download `productivity-garden.html`
2. Open it in any modern browser
3. Click anywhere in the garden to plant your first seed

---

## 🌿 How It Works

- **Click** anywhere on the garden canvas to create a task
- **Name** your task and choose a deadline: 15, 30, or 60 minutes
- **Watch** your plant grow through 5 stages as time passes
- **Complete** the task before the deadline → plant blooms at full stage
- **Miss** the deadline → plant withers and turns grey (never deleted)

All data is saved to `localStorage` — refresh the page and your garden is exactly as you left it.

---

## 🌱 Plant Types

Each task is randomly assigned one of four plant forms:

| Type | Description |
|------|-------------|
| Sprout | A simple leafy stem |
| Flower | Petals emerge, blooms gold at completion |
| Tree | Layered canopy that fills out over time |
| Cactus | Arms extend, flowers at full stage |

---

## 📦 Data Model
```json
{
  "id": "string",
  "type": "sprout | flower | tree | cactus",
  "title": "string",
  "growthStage": 0,
  "plantedAt": 1711800000000,
  "deadline": 1711801800000,
  "isDead": false,
  "isCompleted": false,
  "position": { "x": 42.5, "y": 67.3 }
}
```

---

## 🏗 Architecture

Single HTML file. No bundler, no `node_modules`, no config.
```
App
├── Plant           (one per task, absolutely positioned)
│     └── PlantSVG  (SVG rendering by type + stage)
├── PlantModal      (create dialog)
├── DetailPanel     (task detail + complete button)
└── StatusBar       (live counts at the bottom)
```

**State** lives entirely in `App` — no globals, no context, no external store.  
**Growth** is computed from `(now - plantedAt) / (deadline - plantedAt)` on every 4-second tick.  
**Persistence** is handled by serialising the `plants` array to `localStorage` on every state update.

---

## 🛠 Tech Stack

| | |
|---|---|
| React 18 | Via CDN, functional components + hooks only |
| Babel Standalone | JSX transpilation in the browser |
| SVG | All plant graphics, inline and hand-drawn |
| localStorage | Client-side persistence |
| CSS Custom Properties | Theming and layout |
| Google Fonts | Fraunces + DM Mono |

---

## ⚠️ Known Limitations

- Preset durations only (15 / 30 / 60 min) — no custom input
- Plants are never deleted, only marked dead
- Requires internet on first load for CDN scripts and fonts
- Babel runtime transpilation — not optimised for production scale

---

## 📄 License

MIT
