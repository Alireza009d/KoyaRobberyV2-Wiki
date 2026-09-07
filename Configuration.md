# Configuration

`config.yml` holds every setting that applies server-wide, rather than to
one specific robbery. Robbery locations, loot, and required items live
under [Robberies](Robberies.md) instead.

## Reference

| Key | Default | Description |
|---|---|---|
| `Check-For-Update` | `true` | Checks SpigotMC on startup for a newer version. Never auto-updates. |
| `Locale` | `en` | Which file under `lang/` is active. Must match a file name without `.yml` - `en` for `lang/en.yml`, `fa` for `lang/fa.yml`. |
| `Online-Player-Permission` | `police.online` | Players with this permission always hear `Robbery-Start-Sound`, regardless of distance. |
| `Robbery-Start-Sound` | `custom.robbery` | Sound name played when any robbery starts. |
| `Robbery-Start-Sound-Radius` | `20` | How close (in blocks) a player without the permission above needs to be to hear it. |
| `Crew.Max-Size` | `6` | Maximum members per crew, leader included. |
| `Crew.Invite-Expire-Seconds` | `30` | How long a `/robbery invite` (or GUI invite prompt) stays open before it auto-expires. |
| `Crew.Invite-Prompt-Seconds` | `30` | How long a leader has to type a name in chat after clicking the crew GUI's invite button. |
| `Economy.Enabled` | `false` | Master switch for loot auto-sell. Each robbery also needs its own `Economy.Enable: true` - see [Economy](Economy.md). |
| `Economy.Editor-Price-Step` | `10` | How much the price controls in the loot editor GUI change an item's price by, per click. |
| `Leaderboard.Top-Size` | `10` | How many entries `/robbery top` shows. |
| `Discord.Enabled` | `false` | Master switch for Discord notifications. Each robbery also needs its own `Discord.Enabled: true` - see [Discord](Discord.md). |
| `Discord.Webhook-Url` | *(empty)* | Default webhook URL, used by any robbery that doesn't set its own. |
| `Vault-Drill.Drill-Duration` | `15` | Seconds it takes to drill through a vault door. |
| `Vault-Drill.Material` | `DIAMOND_PICKAXE` | Item type for the drill. |
| `Vault-Drill.Name` / `Lore` | - | Display name/lore, colour codes supported. |
| `Vault-Drill.Glow` | `true` | Adds an enchant glint with no visible enchantment. |
| `Vault-Drill.Custom-Model-Data` | `1001` | For a resource pack custom model. `0` disables it. |
| `Vault-Drill.Consume-On-Use` | `true` | Whether one drill is consumed per door. |

## Reloading

`/robbery reload` re-reads `config.yml`, both `lang/` files, `gui.yml`,
`storage.yml`, and every file under `robberies/`. Active robberies are
left running - nobody gets kicked out mid-heist by a reload.

## storage.yml

Two different things live in this file:

- **`Blocks`** - which block type represents each structure/state
  (`TABLE`, `EMPTY_TABLE`, `SAFE`, `VAULT_DOOR`, ...). Edit these freely,
  ideally paired with the bundled resource pack so each state has its own
  texture.
- **`Structures` / `Builds`** - where every placed table/safe/jewelry
  table/vault door actually is. This is written automatically whenever an
  admin places or removes one with the structure blocks/stick. Don't hand
  -edit it.
