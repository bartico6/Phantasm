# Phantasm AntiCheat

#####Last update: 3rd June 2019

Phantasm is a Terraria Anti-Cheat plugin that aims to stop all forms of cheating (and other harmful activity such as crash exploits and lag machines) in their tracks.

Phantasm is unique amongst other anti-cheat projects in that it is **completely** lag-aware and lag-tolerant (may cause harmless warnings for lagging players but will __***never***__ ban an innocent) and it **blocks** detected cheats rather than just report them.

This means you can leave Phantasm running on your server while you and/or your staff are away, and still be protected.

Phantasm also sanitizes network traffic and removes malicious packets aimed to exploit a crash vulnerability in Terraria or the underlying modding engine.

If enabled in the configuration, Phantasm will also **return** items from canceled events. This means that if the player consumed an item to summon an NPC, and the summoning event was blocked, the item will be refunded. Neither the game, nor any publicly available server engine currently offer this.

### Disclaimer

This repository contains no code. Phantasm is currently a private plugin in development.
The goal of this repository is to serve as an issue tracker for servers that have access to the plugin, as an advertisement of my services for anyone interested, as well as a progress tracker for myself.

*Don't ask for a copy, you ain't getting one.*

### How to make your plugin compatible with Phantasm

* Ensure your NetGetData hooks return out of callbacks that have args.Handled = true. You must **NEVER** un-handle already handled NetGetData hooks, as this will render the anti-cheat completely useless.
* Never register your handlers with border priority values (`int.MinValue` and `int.MaxValue`) - those are "reserved" by Phantasm, and required to function properly. Use `int.MinValue + 1` or `int.MaxValue - 1` instead.

## Implementation status

### Generic:
* Impersonation: Blocked
* Packet exploits (invalid values etc.): Blocked

### NPCs:
* Instakill all: Blocked
* Invalid buff/debuff application: Queued
* Teleportation: Queued

### Tile: 
* Unobtainable and nonexistent tiles: Blocked
* Range hacks: Blocked
* Tool checks: Queued

### Projectiles:
* Spam: Blocked
* Spawn hacks: In progress, largely done.
* Damage hacks: Queued
* Projectile origin (offsets): Queued

### Movement:
* Teleportation exploits: In progress (rewriting)

### Items:
* Inventory editing: Blocked
* Drophacks (spawn items from thin air): Blocked
* Vacuum (pick up items across the map): In progress
* Shop coin bypass: Blocked