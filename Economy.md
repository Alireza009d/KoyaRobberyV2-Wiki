# Economy

KoyaRobbery doesn't ship its own currency - it hooks into
[Vault](https://www.spigotmc.org/resources/vault.34315/) and whatever
economy plugin you already have registered as Vault's provider (EssentialsX,
CMI, etc). If Vault isn't installed, every economy feature just quietly
does nothing - nothing breaks, loot is simply always given as physical
items.

## Enabling it

Two switches need to both be on:

1. `Economy.Enabled: true` in `config.yml` - the server-wide master switch
2. `Economy.Enable: true` in the specific robbery's yml (or toggle it
   there directly - there's no in-game toggle for this one yet, it's a
   single top-level flag)

## Setting prices

Price lives on the loot item itself, not on the robbery as a whole - two
different items of the same material can have different prices. Set it:

- **In-game (recommended):** open `/robbery editor <id>`, then Swap-Hand
  (F) to raise an item's price or Middle-click to lower it, in steps of
  `Economy.Editor-Price-Step` (from `config.yml`).
- **By hand:** set `Sell-Price` under that item in the robbery's yml (see
  [Loot Tables](Loot-Tables.md)).

An item with `Sell-Price: 0` (the default) is never sellable - taking it
out of a container gives the physical item like normal, economy or not.

## How a sale happens

When economy selling is on for a robbery, taking a sellable item out of
one of its containers deposits money into the player's account instead of
giving them the item. The amount is `Sell-Price × stack size`. This
happens automatically the moment the item is moved out of the container's
inventory - there's no separate "sell" step.

## Item lore

Any item with a price above 0 gets an extra grey lore line showing what
it's worth, e.g.:

```
(+$10,000)
```

formatted with comma separators. This line is added automatically both in
the loot editor and on the actual item during a robbery - you don't add it
yourself in the yml.
