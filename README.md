# Phantasm AntiCheat

Phantasm is a Terraria Anti-Cheat plugin that aims to stop all forms of cheating (and other harmful activity such as crash exploits and lag machines) in their tracks.

### Disclaimer

This repository contains no code. Phantasm is currently a private plugin in development.
The goal of this repository is to serve as an issue tracker for servers that have access to the plugin, as well as a progress tracker for myself.

*Don't ask for a copy, you ain't getting one.*

### How to make your plugin compatible with Phantasm

* Ensure your NetGetData hooks return out of callbacks that have args.Handled = true. You must **NEVER** un-handle already handled NetGetData hooks, as this will cause duplication glitches and other unintended behavior.
* Never register your handlers with border priority values (`int.MinValue` and `int.MaxValue`) - those are "reserved" by Phantasm, and required to function properly. Use `int.MinValue + 1` or `int.MaxValue - 1` instead.

## Implementation status

### Generic:
* Crash exploits: Complete
* Impersonation: Complete

### Tile: 
* Unobtainable and nonexistent tiles: Complete
* Range hacks: Complete
* Tool checks: Queued

### Projectile:
* Spam prevention: Complete
* Explosives: Complete
* Spawn hacks: In progress, largely done.
* Damage hacks: Queued
* Projectile origin (offsets): Queued

### Movement:
* Teleportation exploits: Complete

### Inventory:
* Inventory operations: Complete
* Item pickups/drops: In progress
* NPC interactions: In progress
