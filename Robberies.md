# Robberies

Every robbery location is one file under `robberies/<id>.yml`. The file
name (without `.yml`) is its id, used in `/robbery start <id>`,
`/robbery editor <id>`, etc.

Create one in-game with `/robbery create <id>` while standing inside its
WorldGuard region - this fills in `Region-Id` automatically. From there,
either edit the yml directly or use the in-game editors
([Loot Tables](Loot-Tables.md), [Required Items](Required-Items.md)) for the
loot/requirement sections.

## Top-level fields

| Key | Description |
|---|---|
| `Display-Name` | Shown in messages, the boss bar, and both GUI editors. |
| `Region-Id` | The WorldGuard region this robbery is tied to. |
| `Robbery-Time` | Duration in seconds. |
| `Robbery-Cooldown` | Seconds before this robbery can be started again. |
| `Required-Crew-Size` | Minimum crew members to start (bypassed by `robbery.bypass.crewsize`). |
| `Minimum-Online-Players` | Minimum players online on the whole server to start. |
| `Check-Vault-Doors` | If true, containers can't be looted until every vault door in the region is open. |
| `Restore-Structures-On-End` | Resets every block/loot state in the region once the robbery ends. |
| `Teleport-Robbers-On-End.Enable` / `.Location` | Optional teleport for crew members still in the region when it ends. Location format: `world;x;y;z;yaw;pitch`. |
| `Robbery-Start-Command-List` / `Robbery-End-Command-List` | Console commands run once on start/end. `%leader%` is available in both. |
| `Opening-Animation` | `NONE`, `BLOCK_REVEAL`, `PARTICLE`, or `COMBINED` - how tables/safes/jewelry displays open. |

## Optional Citizens NPC

Only does anything if Citizens is installed - ignored entirely otherwise.

```yaml
Npc:
  Id: -1              # Citizens NPC id, -1 = no NPC linked
  Require-Shift: false # if true, only a shift+right-click opens the start menu
```

Find an NPC's id in-game with Citizens' own `/npc id`. Right-clicking a
linked NPC opens a small start menu for that robbery instead of requiring
`/robbery start <id>`.

## Escape phase

```yaml
Escape:
  Enable: true
  Time-Limit: 45   # seconds the crew has to leave the region once the timer ends
  Point: ""        # optional fixed escape point (same format as teleport), blank = just leave the region
```

If enabled, reaching `Robbery-Time` doesn't end the robbery immediately -
the crew has `Time-Limit` seconds to get out of the region (or reach
`Point`, if set) or the robbery is marked failed.

## Heat / alarm

```yaml
Heat:
  Enable: true
  Stages:
    1:
      At-Second: 120
      Message: "&cSirens are approaching in the distance..."
      Sound: "block.bell.use"
    2:
      At-Second: 240
      Message: "&4The police are almost here!"
      Sound: "entity.wither.spawn"
```

Purely cosmetic pressure - each stage fires once, sending its message and
sound to every crew member. Pair it with `Robbery-Start-Command-List` and
a wanted-level plugin for actual consequences.

## Boss bar

```yaml
BossBar:
  Enable: true
```

Shows a per-player countdown boss bar while the robbery runs. If `false`,
falls back to an action-bar countdown instead.

## Discord notifications

Each robbery can post its own started/success/failed embeds to Discord,
with full control over title, description, color, thumbnail, image,
author, and footer - see [Discord](Discord.md) for the full `Discord:`
section reference and every available placeholder.

## Loot and required items

These have their own pages since both are best edited in-game:

- [Loot Tables](Loot-Tables.md) - what's in the table/safe/jewelry containers,
  drop chance, and sell price
- [Required Items](Required-Items.md) - what a crew leader must be carrying
  to start
