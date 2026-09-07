# Resource Pack

KoyaRobbery ships an optional resource pack (`Resoursepack/` in the plugin
repo, packaged as `KoyaRobbery-Resourcepack-v2.zip`) that gives the
structure blocks and the vault drill their own look instead of appearing
as plain vanilla blocks/tools. The plugin works perfectly fine without it -
it's a cosmetic layer, not a requirement.

## Installing it

You can download the packaged `KoyaRobbery-Resourcepack-v2.zip` from the
**#Resourcepack** channel on our Discord: https://discord.gg/sKvGYQUypK

Serve it to players however you already distribute resource packs on your
network - a server-resource-pack entry pointing at a hosted copy of
`KoyaRobbery-Resourcepack-v2.zip` (via `server.properties`'
`resource-pack`/`resource-pack-sha1`, or a resource pack management plugin)
is the usual approach.

## Version support

The pack declares `pack_format: 4` (Minecraft 1.13) with a
`supported_formats` range extending well past current versions, so clients
on 1.20.2+ (which understand that field) accept it across the whole range
without a warning. Clients older than that only compare against the bare
`pack_format`, so very old (1.13-1.14.4) and very new clients both accept
it cleanly; clients in between may show a dismissible "may not work
correctly" notice, which is cosmetic only - the actual block/item model
schema this pack uses hasn't changed since 1.13, so the pack functions
identically regardless of that notice.

## How structures are reskinned

Tables, safes, jewelry tables, and vault doors are all built from ordinary
vanilla blocks (see `storage.yml`'s `Blocks` section) - the resource pack
replaces those specific blocks' vanilla models with custom ones. This is
simple and needs no special per-item tagging, but it comes with one
trade-off worth knowing:

> **Any block of that same vanilla type, anywhere on the map, renders with
> the custom model too** - not just the ones placed by the plugin. The
> pack currently reskins white/black/brown/gray/light-gray/orange/red
> glazed terracotta. If your build team already uses any of those blocks
> decoratively, either avoid that colour elsewhere or change the
> corresponding entry in `storage.yml`'s `Blocks` section to a rarer block
> before placing structures.

## How the vault drill is reskinned

The drill is handled differently, and correctly avoids the block problem
above: it's a `DIAMOND_PICKAXE` (configurable in `config.yml`) tagged with
`Custom-Model-Data: 1001`. The resource pack overrides the *default*
diamond pickaxe model with a predicate:

```json
{
  "parent": "item/handheld",
  "textures": { "layer0": "item/diamond_pickaxe" },
  "overrides": [
    { "predicate": { "custom_model_data": 1001 }, "model": "item/koya_robbery/vault_drill" }
  ]
}
```

Only an item stack with that exact custom model data value shows the
custom drill mesh - every other diamond pickaxe on your server (including
ones players mine and craft normally) still looks and behaves like a
normal diamond pickaxe. If you change `Vault-Drill.Material` in
`config.yml` to something other than `DIAMOND_PICKAXE`, update this
override file (`assets/minecraft/models/item/<your material>.json`) to
match, or the custom model won't show.

Setting `Vault-Drill.Custom-Model-Data: 0` disables this entirely - the
drill is then just a plain named/lored item, which is the right call on
1.13 (custom model data was added in 1.14).

## Known global reskins to be aware of

A couple of textures in the pack replace a *vanilla* texture path
directly rather than being tied to a specific plugin item, which means
they affect that item everywhere on your server, not just in robberies:

- `textures/item/emerald.png` (with an animation `.mcmeta`) restyles every
  emerald in the game, since the "Emerald Credit" loot item is a plain
  vanilla `EMERALD` with no model-data tagging.

If you'd rather emeralds stay vanilla-looking everywhere except robbery
loot, delete `assets/minecraft/textures/item/emerald.png` and its
`.mcmeta`, or swap that loot entry to a less common material.

## Editing the pack

The unpacked source lives in `Resoursepack/assets/...` alongside the built
zip. After changing anything, rebuild the zip from the `Resoursepack/`
folder:

```
cd Resoursepack
zip -r KoyaRobbery-Resourcepack-v2.zip pack.mcmeta pack.png assets
```
