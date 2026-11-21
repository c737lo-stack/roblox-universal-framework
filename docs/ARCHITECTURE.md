# System Architecture & Engineering Decisions

This document details the core engineering principles, runtime patterns, security controls, and automated build/validation pipelines powering the **Roblox Universal Framework**.

---

## 1. Architectural Layers

The framework is structured around **3 runtime layers** backed by an **offline Python & Rojo build pipeline**:

1. **Core Infrastructure (`Core_Systemes_De_Base/`)**
   Provides shared foundational services (persistence, monetization, notifications, audio, UI theming). Higher-level modules depend downward on Core services via clean interfaces and player attributes.
2. **Gameplay, Economy & Retention (`Gameplay_Mecaniques/`)**
   Implements modular game loops (Tycoon progression curves, Case Opening odds/mutations, 0–20 min onboarding hooks, 7-day retention calendars, boosts, playtime gifts).
3. **World & Environment (`Monde_Et_Environnement/`)**
   Encapsulates spatial and interactive world elements (`CollectionService`-tagged doors, portals, leaderboards, day/night cycles, procedural 3D factories).

---

## 2. Key Engineering Patterns

### Server-Authoritative Security & Rate-Limiting
- All state mutations (currency, purchases, rewards, inventory, teleports) are validated strictly on the server.
- Every `OnServerEvent` handler enforces per-player cooldowns/rate-limiting and cleans up per-player memory state on `PlayerRemoving`.
- Automated compliance is verified on every commit by `validate_luau.py`.

### Fault-Tolerant Persistence (`UniversalDataStore`)
- Uses `UpdateAsync` with exponential retry logic instead of blind `SetAsync` overwrites.
- Tracks explicit load-success guards (`canSaveFlags`) so a transient DataStore outage never overwrites valid player profiles with default values upon disconnect.
- Runs periodic 120s autosaves alongside `game:BindToClose` graceful flush hooks.

### Zero-Boilerplate Integration (`CollectionService`)
- Interactive systems (`UniversalTycoon`, `UniversalCheckpoints`, `UniversalCollectible`, `UniversalPadsHazards`, `UniversalGlobalLeaderboard`, `UniversalTeleporter`, `UniversalDoor`) attach dynamically via Roblox `CollectionService` tags and instance `Attributes`.
- Designers can place or duplicate assets in Studio without editing scripts.

### Phased Packaging & Race-Condition Prevention (`MasterAutoDeploy`)
- Standalone `.rbxmx` modules and the unified `AllUniversalAssets.rbxmx` bundle are compiled programmatically by `build_rbxmx.py`.
- All packaged `Script` and `LocalScript` instances are flagged `Disabled = true` inside the XML archive so Studio never executes them prematurely during drag-and-drop.
- `MasterAutoDeploy` orchestrates deterministic initialization order:
  1. **Phase 1**: Shared modules & configs (`ReplicatedStorage`)
  2. **Phase 2**: Core infrastructure (`UniversalDataStore`, `UniversalGamepassShop`, etc.)
  3. **Phase 3**: Gameplay, World & Client scripts (with client double-execution guards)

### Economy & Retention Modeling
- **Unified Currency & Multiplier Bridge**: Cross-system multipliers (`UniversalBoost_Cash`, `UniversalBoost_Luck`, `UniversalNewcomerCashMult`, `Gamepass_DoubleCash`, `Gamepass_DoubleLuck`) propagate cleanly across Tycoon income, Case Opening odds, and offline revenue.
- **Mathematical Progression**: `UniversalTycoon` separates economy balancing into a dedicated `ProgressionCurve.luau` module for predictable ROI and Rebirth scaling.

---

## 3. Automated Static Analysis (`validate_luau.py`)

Every push and pull request runs a zero-dependency Python CI check enforcing:
- `--!strict` type-checking header on 100% of `.luau` files
- Zero deprecated Roblox globals (`wait`, `spawn`, `delay`) in favor of `task.*`
- Performance best practice: no 2-argument `Instance.new(class, parent)`
- Balanced syntax delimiters (`()`, `[]`, `{}`)
- Presence of rate-limiting and `PlayerRemoving` cleanup wherever `OnServerEvent` is used
- Valid XML structure and `Disabled=true` safety flag on all packaged `.rbxmx` scripts
- Valid JSON schema for `default.project.json` (Rojo)
