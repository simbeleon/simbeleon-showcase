# Idle RPG · Godot 4.x

A fully designed idle RPG built in Godot 4.x — solo project, designed and developed from the ground up by Simbeleon.

This is not a prototype or jam game. It's a structured long-term project with a proper master plan, documented systems, and a deliberate architecture that scales.

---

## What It Is

An idle RPG where players manage heroes, explore zones, and run professions — all driven by offline-capable progression loops. The game is designed to be deep without being demanding: you set things in motion, come back, and the world has moved.

The design philosophy: **systems over content**. Build the right foundations first, then fill them.

---

## Systems Overview

### Hero System
- Hero creation with role-based archetypes
- Attribute progression tied to activity and equipment
- Party composition with synergy bonuses

### Zone Builder
- Zone definitions with enemy tables, loot pools, and difficulty scaling
- Heroes assigned to zones for autonomous combat
- Zone unlock progression linked to player milestones

### Profession Mechanics
- Gathering, crafting, and support professions
- Each profession runs on a resource loop (gather → process → output)
- Professions level independently and unlock new recipes/zones

### Progression Loop
- Offline time calculation for all active systems
- Catch-up mechanics to prevent stagnation after absence
- Milestone triggers for narrative events and unlocks

---

## Project Approach

| Area | Approach |
|------|----------|
| Engine | Godot 4.x (GDScript) |
| Architecture | Modular scene tree, signal-driven communication |
| Planning | Master plan document before any code |
| Tooling | Claude Code for architecture review and code audits |
| Scope control | Feature-locked iterations — finish before expanding |

---

## Status

Active development. Core systems designed; implementation ongoing.

Architecture documentation: [architecture-overview.md](./architecture-overview.md)

---

> *Built solo. Designed seriously.*
