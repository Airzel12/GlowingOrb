# GlowingOrbMod

A high-tech protective orb designed to assist employees in the field. The orb follows the player, provides light, and engages hostile entities.

## Features

* **Luminous Follower:** Provides a cyan light source that stays by your side.
* **Laser Defense System:** Automatically scans for and attacks nearby enemies.
* **Navigation Support:** Press **'Q'** to toggle the orb's navigation. It will attempt to find the nearest exit or lead you back toward the ship.
* **Ascension Mechanic:** After 120 seconds, the orb enters an **Ascended State**, significantly increasing its laser damage and allowing it to automatically disable turrets and landmines in a 12m radius.

## Controls

* **[Q]**: Toggle Navigation Mode (Switch between following you and pathfinding to the building entrance/ship).

## Known Issues & Bugs

* **Targeting:** The orb currently attempts to shoot "unkillable" monsters (such as Ghost Girl or Spore Lizards). While it deals no damage to them, it may waste its focus on these targets. A fix to ignore invincible entities is planned for a later date.
* **NavMesh Constraints:** In some custom moons, the orb may struggle to find a path if the NavMesh is not properly baked by the map creator.

## Technical Details

* **Damage (Standard):** 3 damage per hit.
* **Damage (Ascended):** 20 damage per hit.
* **Attack Rate:** 0.8 seconds.
* **Hazard Detection:** Scans every 0.5 seconds when Ascended.

## Installation

1. Ensure you have **BepInEx** installed.
2. Place the `GlowingOrbMod.dll` into your `BepInEx/plugins` folder.
3. Launch the game as the Server Host.
