# KoyaRobbery

KoyaRobbery is a Paper/Spigot plugin that turns a WorldGuard region into a
crew-based heist: break vault doors, crack safes, and loot tables and
jewelry displays under a timer, with an optional escape phase, alarm/heat
pressure, and per-item economy payouts.

Every part of the plugin is file-based and hot-reloadable: each robbery
location lives in its own file, every player-facing message lives in a
language file, and every GUI's materials/titles come from `gui.yml` - a
server owner can hand off translation or menu styling work without
touching plugin behavior, and most of it can be edited in-game through the
loot and required-items editors instead of by hand.

## Pages

- [Installation](Installation.md) — requirements, first run, folder layout
- [Configuration](Configuration.md) — `config.yml` reference
- [Robberies](Robberies.md) — writing robbery entries under `robberies/`
- [Loot Tables](Loot-Tables.md) — container loot, chances, the in-game editor
- [Required Items](Required-Items.md) — gating a robbery behind held items
- [Economy](Economy.md) — per-item sell prices, Vault integration
- [Discord](Discord.md) — per-robbery started/success/failed webhook embeds
- [Resource Pack](Resource-Pack.md) — the bundled pack, version support, custom drill/structure models
- [GUI Customization](GUI-Customization.md) — `gui.yml`, layouts, text
- [Commands and Permissions](Commands-and-Permissions.md)
- [Localization](Localization.md) — translating the plugin, adding a language
- [FAQ and Troubleshooting](FAQ-and-Troubleshooting.md)

## At a glance

| Feature | Details |
|---|---|
| Storage | Flat yml files - one per robbery, plus lang/gui/player-stats files |
| Economy | Vault, per-loot-item sell price, set live in the loot editor GUI |
| Crew system | Leader-driven crews with in-game or chat-prompt invites |
| Structures | Table, safe (with a lockpick minigame), jewelry table, vault door |
| Optional integrations | Vault, PlaceholderAPI, Citizens (NPC-triggered start menu) |
| Animations | Per-robbery choice of `NONE`, `BLOCK_REVEAL`, `PARTICLE`, `COMBINED` |
| Version | Paper/Spigot 1.13+ — see [Installation](Installation.md) |
