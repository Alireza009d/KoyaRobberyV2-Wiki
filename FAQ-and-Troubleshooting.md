# FAQ and Troubleshooting

**"This region isn't registered for robbery" when placing a structure**

The WorldGuard region you're standing in doesn't match any robbery's
`Region-Id`. Check the id with your WorldGuard region tool and make sure
it's spelled exactly the same in the robbery's yml (or run
`/robbery create <id>` while standing inside the region so it's filled in
automatically).

**A container won't open / nothing happens on right-click**

- Check `Check-Vault-Doors` - if it's `true`, every vault door in the
  region has to be drilled open first.
- Check the container's `Opening-Tool` in [Loot Tables](Loot-Tables.md) - you
  need to be holding that exact item.
- Make sure your crew's robbery is actually active (`/robbery start`
  succeeded) - containers only respond during an active robbery for your
  crew.

**Players can't start a robbery even with a full crew**

Check, in order: `Minimum-Online-Players`, `Required-Crew-Size`, the
robbery's cooldown (`/robbery list` doesn't show cooldowns, but a leader
trying to start gets told the remaining time), and
[Required Items](Required-Items.md) if any are set.

**The vault drill doesn't do anything**

It only works on a placed vault door structure, and only one drill can run
per door at a time. Make sure the door was placed with
`/robbery structure` (the vault door block) and not just built by hand.

**Economy selling isn't working**

Both switches need to be on: `Economy.Enabled: true` in `config.yml` *and*
`Economy.Enable: true` in that specific robbery's yml. Also confirm Vault
is installed with a working economy provider (`/vault-info` from Vault
itself is the quickest check), and that the item actually has a
`Sell-Price` above 0 - see [Economy](Economy.md).

**The Citizens NPC doesn't open anything**

- Confirm Citizens is actually installed - the console logs "Hooked into
  Citizens" on startup if it detected it.
- Double check the robbery's `Npc.Id` matches the NPC's actual id
  (`/npc id` in Citizens).
- If `Npc.Require-Shift: true`, you have to be sneaking when you click it.

**Messages are showing up as their raw key name (e.g. "NEED_PERMISSION") instead of real text**

That means the active locale file is missing that key entirely (not just
untranslated - actually absent). Compare against a fresh copy of
`lang/en.yml` from the plugin jar and add whatever's missing; the fallback
only works if the key exists in `en.yml` at all.

**I edited a robbery's yml by hand and the loot editor shows something different**

The plugin caches everything in memory and only re-reads yml files on
`/robbery reload` (or full startup). Run `/robbery reload` after any
manual yml edit.

**Can I run this on 1.12.2?**

No - see [Installation](Installation.md). 1.12.2 predates Minecraft's block
flattening and uses a materially different item/block API; supporting it
alongside modern versions isn't practical without maintaining two separate
codebases.

**Players see "this resource pack may not work correctly" for the bundled pack**

Cosmetic only - see [Resource Pack](Resource-Pack.md) for exactly which
client versions show this and why it's safe to dismiss. The pack still
functions identically regardless.

**A vanilla block/item looks different everywhere, not just in robberies**

That's an inherent trade-off of how the bundled resource pack reskins
plain vanilla blocks/materials (glazed terracotta, emeralds) - see
[Resource Pack](Resource-Pack.md) for exactly which ones and how to change or
remove them.
