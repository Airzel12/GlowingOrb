# GlowingOrbMod

[![Thunderstore Downloads](https://img.shields.io/thunderstore/dt/Airzel12/GlowingOrb?style=for-the-badge&logo=thunderstore)](https://thunderstore.io/c/lethal-company/p/Airzel12/GlowingOrb)
[![GitHub release](https://img.shields.io/github/v/release/Airzel12/GlowingOrb?style=for-the-badge)](https://github.com/Airzel12/GlowingOrb/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

> A BepInEx plugin for Lethal Company that adds a networked, AI-driven support drone. Reverse-engineered game systems to extend core gameplay without source access.

### **Demo**
[Replace this with your GIF link](https://i.imgur.com/your-gif-here.gif)
*Press Q to toggle navigation mode. Ascended state activates at 120s, auto-disabling hazards.*

---

## **Technical Implementation**

This project demonstrates runtime patching, networked AI behavior, and NavMesh integration in a commercial Unity/IL2CPP title.

### **Core Systems**
* **Harmony Transpilers & Prefixes**: Hooked into `GrabbableObject`, `EnemyAI`, and `RoundManager` to inject custom behavior without modifying game DLLs.
* **Custom State Machine**: Orb operates in 3 states - `Follow`, `Navigate`, `Ascended`. Transitions managed via `MonoBehaviour` lifecycle and `Update()` ticks.
* **Network Synchronization**: Implemented custom RPCs using Lethal Company’s built-in networking to sync orb position, target, and ascended state across all clients in P2P sessions. Prevents desync and ghost lasers.
* **Pathfinding**: Utilizes Unity's NavMesh system. Added fallback logic for maps with incomplete navmesh data to prevent softlocks.
* **Hazard Interaction**: Spherecasts on `Update` cycle to detect and interface with `Turret` and `Landmine` instances. Disables hazards by invoking their native shutdown methods.

### **Performance & Compatibility**
* **Patch Resilience**: Maintained compatibility through Lethal Company v45-v60+ IL2CPP updates by updating Harmony signatures and testing against breaking changes.
* **Profiling**: Laser system capped at 0.8s attack rate with 0.5s scan interval to minimize per-frame CPU cost. No GC alloc in `Update()` loop.
* **Bug Handling**: Current build logs but does not engage `EnemyType` instances flagged as `isImmortal`. Full targeting blacklist planned for v1.3.

| **State** | **Damage** | **Attack Rate** | **Special** |
| --- | --- | --- | --- |
| Standard | 3 HP/hit | 0.8s | Laser tracking |
| Ascended | 20 HP/hit | 0.8s | + 12m hazard disable aura |

---

## **Features**
* **Luminous Follower**: Dynamic light source attached to player transform.
* **Autonomous Defense**: Scans for and engages hostile entities using raycast + spherecast checks.
* **Navigation Assist [Q]**: Toggles between follow mode and A* pathfinding to nearest `EntranceTeleport` or ship.
* **Ascension Mechanic**: After 120s, orb enters empowered state with increased damage and gains ability to disable environmental hazards.

## **Installation**
1. Requires [BepInEx](https://thunderstore.io/c/lethal-company/p/BepInExPack/) v5.4+
2. Download `GlowingOrb.dll` from [Releases](https://github.com/Airzel12/GlowingOrb/releases)
3. Place in `/BepInEx/plugins/` folder
4. Host or join a lobby. All clients should install for full visual sync.

## **Controls**
* **[Q]** - Toggle Navigation Mode: Switches between following the player and pathfinding to the facility entrance/main exit.

## **Known Issues**
* **NavMesh Dependency**: Orb navigation requires a properly baked NavMesh. Some custom moons may cause pathfinding failure if the creator did not generate AI navigation data.
* **Targeting Logic**: Currently targets all `EnemyAI` instances. A whitelist to ignore invincible entities like Ghost Girl is in development.

---

### **Building from Source**
1. Clone repo and open in IDE
2. Reference `Assembly-CSharp.dll`, `UnityEngine.dll`, etc from your Lethal Company Managed folder
3. Build as `Class Library` targeting.NET Framework 4.7.2
4. Output `GlowingOrb.dll` to `BepInEx/plugins`

**Tools Used**: C#, Unity 2022.3, BepInEx 5, HarmonyX, Git, Visual Studio
