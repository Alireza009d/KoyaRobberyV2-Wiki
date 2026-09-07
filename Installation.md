# Installation

## Requirements

- Paper or Spigot, **1.13 or newer** (the plugin only calls standard
  Bukkit/Spigot API, so it runs on either)
- [WorldGuard](https://enginehub.org/worldguard) - hard dependency, every
  robbery is tied to a WorldGuard region
- Java 17 or newer on the server

Optional, all soft dependencies (the plugin runs fine without any of them,
the related feature is just unavailable):

| Plugin | Unlocks |
|---|---|
| [Vault](https://www.spigotmc.org/resources/vault.34315/) + an economy plugin | Loot auto-sell (see [Economy](Economy.md)) |
| [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) | `%koyarobbery_*%` placeholders |
| [Citizens](https://www.spigotmc.org/resources/citizens.13811/) | NPC-triggered robbery start menu |

## Building from source

```
mvn clean package
```

The shaded jar is written to `target/KoyaRobbery-2.0.0.jar`. Drop it into
`plugins/` like any other plugin.

## First run

On first startup the plugin creates `plugins/KoyaRobbery/` with:

```
plugins/KoyaRobbery/
├── config.yml
├── gui.yml
├── storage.yml
├── players.yml
├── lang/
│   ├── en.yml
│   └── fa.yml
└── robberies/
    ├── central_bank.yml
    └── gun_store.yml
```

The two example robberies are copied in only on a fresh install (an empty
`robberies/` folder) - they won't overwrite anything on later updates, and
they reference a WorldGuard region (`bank_region_name`,
`gunshop_region_name`) that doesn't exist on your server yet. Either
rename an existing region to match, or edit `Region-Id` in the file to
point at one you already have. Read them fully before setting up your own
- every field has a one-line comment explaining what it does.

## Setting up your first robbery

1. Create a WorldGuard region around the building.
2. Stand inside it and run `/robbery create <id>` - this creates
   `robberies/<id>.yml` and fills in the region automatically.
3. Open the file and set `Robbery-Time`, `Required-Crew-Size`, and any
   optional features (see [Robberies](Robberies.md)).
4. Run `/robbery structure` as an admin to get the table/safe/jewelry/vault
   door blocks, and place them inside the region.
5. Run `/robbery editor <id>` to fill in loot for each container type
   in-game - see [Loot Tables](Loot-Tables.md).
6. If the robbery has a vault door, give yourself the drill with
   `/robbery give drill <player>`.

You're ready to test with `/robbery start <id>`.
