# Loot Tables

Each robbery has three independent loot tables - one each for `Table`,
`Safe`, and `Jewelry` containers. Every entry rolls independently each
time a container is filled.

## Editing in-game

```
/robbery editor <id>
```

Opens the loot editor for that robbery, starting on the `Table` tab. Every
existing item is shown as its own icon; each click type controls a
different stat so there's no sub-menu to dig through:

| Action | Effect |
|---|---|
| Left-click | Chance +5% |
| Right-click | Chance -5% |
| Shift + Left-click | Amount Per Container +1 |
| Shift + Right-click | Amount Per Container -1 |
| Drop (Q) | Stack Size +1 |
| Ctrl + Drop | Stack Size -1 |
| Swap Hand (F) | Sell Price + `Economy.Editor-Price-Step` |
| Middle-click | Sell Price - `Economy.Editor-Price-Step` |
| Press 1-9 while hovering | Remove the item |

Bottom row:

- **Add Item** - adds whatever's in your hand as a new entry (100%
  chance, 1 roll per container, sell price 0)
- **Table / Safe / Jewelry** - switch tabs
- **Required Items** - jumps to that robbery's [required items](Required-Items.md) editor
- **Save & Close** - writes every change back to the robbery's yml file

Nothing is saved until you click **Save & Close** - closing the GUI any
other way (Esc, running `/robbery editor` again) discards changes.

## yml reference

```yaml
Loot:
  Table:
    Opening-Tool: NOTHING   # item required in hand to open this container type, or NOTHING for none
    Items:
      1:
        Item: PAPER              # material given
        Name: "&aCash Bundle"    # display name
        Amount-Per-Container: 6  # how many times this entry is rolled per fill
        Item-Amount: 32          # stack size given per successful roll
        Chance: 100              # chance out of 100 that each roll succeeds
        Sell-Price: 25           # money given per stack when economy selling is on, 0 = not sellable
```

`Safe` and `Jewelry` follow the same shape. `Safe` additionally always
requires the lockpick minigame (a short GUI sequence) in addition to
whatever `Opening-Tool` it's set to.

## Sell price and item lore

Any item with `Sell-Price` above 0 gets an extra lore line showing its
value (e.g. `(+$10,000)`, comma-formatted) - both in the loot editor and
on the actual item once it's rolled during a robbery, so players know
what's worth grabbing before selling it. See [Economy](Economy.md) for how
the sale itself works.
