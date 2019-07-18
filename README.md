# Phantasm AntiCheat

##### Last update: July 18th 2019

Phantasm is a Terraria Anti-Cheat plugin that aims to stop all forms of cheating (and other harmful activity such as crash exploits and lag machines) in their tracks.

Phantasm is unique amongst other anti-cheat projects in that it is **completely** lag-aware and lag-tolerant (may cause harmless warnings for lagging players but will __***never***__ ban an innocent) and it **blocks and reverts** detected cheats rather than just report them.

This means Phantasm is essentially an unattended anticheat solution - server staff do not need to be present for the anticheat to be effective - it deals with everything itself.

Phantasm also, optionally, doubles as a **gameplay enhancer**, and **protocol validator**:

* When protocol validation is enabled, Phantasm will sanitize inbound network traffic from connected clients, and prevent various crash exploits including spamming computationally expensive game actions, truncated/malformed packets et cetera.
* When gameplay enhancing is enabled, Phantasm will fix some Multiplayer issues Terraria & tShock have - blocked events not returning items, to name one - for instance, summoning a boss will not consume the summon item if the summon event was blocked by a server plugin. The same applies to block placements and other "item consuming actions".

### Disclaimer

This repository contains no code. Phantasm is currently a private plugin.
The goal of this repository is to serve as an issue tracker for individuals that have access to the plugin, as an advertisement of my services for anyone interested, as well as a progress tracker for myself and said interested parties.

*Don't email/DM me and ask for a copy, I select testers on my own, and much like with becoming a moderator/administrator somewhere - asking will only shrink your chances of being picked*

### How to make your server compatible with Phantasm

* Abandon NetGetData hooks, and use events. This will either be provided by tShock, or by an additional plugin of mine.
* If the event system is a plugin - mod tShock and other plugins to use events instead of NetGetData hooks.
* Use only events (and not NetHooks) unless you're executing packet/protocol hacks:
* * This is because Phantasm handles most packets and runs asynchronous cheat checks on them - this means a packet that is already handled must be ignored as to not interfere with the anticheat check. Later (usually within the same tick) an event corresponding to the handled packet is raised if the cheat check passed - only then should you be performing any game-changing actions such as logging, casting abilities in custom gamemodes et cetera.
* Whenever you're sending data to a client (such as an inventory update) you *must* update the server-side player data as well, otherwise they will rolled back for a cheat violation (or kicked/banned at worst) - in other words, make sure to maintain consistency on both sides (if you're updating inventory, send an update packet AND update the server-side version, etc.
* * Phantasm will provide a "backwards compatibility" mode where it'll catch outgoing update packets and update the server-side model by itself. However, running in backwards compatibility mode comes with a tradeoff: You lose the ability to execute various packet hacks, as they'll get merged into the game state.

The above instructions not only make the server compatible with Phantasm, but also introduce good practices into your codebase, making it easy to fend off various exploits yourself, even if Phantasm never actually releases.

# Implementation status

#### The Anticheat's development is currently blocked by tShock. This is because there is no feasible way to get my code (asynchronous cheat checks) to work with other plugins due to how the plugin ecosystem works (nethooks). I'm waiting for tShock's move on that front. If that doesn't happen in a reasonable timeframe, Phantasm will have an external plugin dependency and require modding tShock to work. *I think it's a small cost for having a cheat-free server though, no?*

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