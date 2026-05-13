# Architecture Overview · Idle RPG

This document describes the structural design decisions for the Idle RPG project. It is a living document — updated as systems are finalized.

---

## Core Design Principles

1. **Signal-driven**: systems communicate via Godot signals, not direct references. This keeps modules loosely coupled and testable in isolation.
2. **Data-first**: game data (zones, heroes, professions, items) lives in Resources or JSON, separated from logic. Changing a zone's difficulty does not require touching any script.
3. **Single source of truth**: one GameState autoload holds runtime state. Nothing writes to game state outside of this node.
4. **Offline-safe**: every time-based system is designed around elapsed time, not frame ticks. The game calculates what happened while you were away, not what is happening right now.

---

## Node & Scene Structure

```
Root
├── GameState (Autoload)        ← global runtime state
├── EventBus (Autoload)         ← global signal hub
├── SaveManager (Autoload)      ← serialization/deserialization
│
├── UI/
│   ├── HUD                     ← persistent overlays
│   ├── HeroPanel               ← hero list + detail view
│   ├── ZonePanel               ← zone selection + combat log
│   └── ProfessionPanel         ← profession queues + output
│
└── Systems/
    ├── CombatSystem            ← tick-based damage resolution
    ├── ProgressionSystem       ← XP, leveling, milestones
    ├── ProfessionSystem        ← resource loops
    └── OfflineSystem           ← elapsed time catch-up
```

---

## Data Layer

All game content is defined as Godot `Resource` files (`.tres` / `.res`) or JSON configs loaded at startup.

- `HeroData` — archetype, base stats, unlock condition
- `ZoneData` — enemy table, loot pool, entry requirements, offline yield rate
- `ProfessionData` — resource inputs/outputs, cycle time, level thresholds
- `ItemData` — type, stats, rarity, source

No hardcoded values in scripts. Tuning happens in data files only.

---

## Offline Calculation Flow

```
1. On game load → read last_save_timestamp
2. Calculate delta_seconds = now - last_save_timestamp
3. For each active system (combat zones, profession queues):
   a. Determine cycles that would have completed in delta_seconds
   b. Apply results (XP, loot, resources) to GameState
   c. Log summary for player feedback
4. Clamp max offline time (configurable cap, default 8h)
5. Save updated state
```

This runs once per session open, before the UI initializes.

---

## Save System

- Serialized to JSON via a custom `SaveManager` autoload
- Each system exposes `to_dict()` and `from_dict()` methods
- Save file versioned — migration logic handles outdated saves
- Auto-save on: app focus lost, major milestone reached, every N minutes

---

## AI Tooling Integration

Claude Code is used throughout development for:
- Architecture review before implementing a new system
- Catching signal dependency cycles early
- Auditing GDScript for anti-patterns (direct node paths, missing null checks)
- Smoke testing scene tree consistency

The AI does not write the game — it validates decisions and flags drift from the master plan.

---

## Known Design Constraints

- Godot 4.x threading is limited: heavy offline calculations run in a deferred call on the main thread to avoid race conditions
- GDScript reflection is limited: `to_dict()` methods are written manually per Resource type
- No multiplayer scope — architecture is deliberately single-player only

---

*Last updated: 2026*
