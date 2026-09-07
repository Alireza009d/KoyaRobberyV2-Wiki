# Required Items

A robbery can require a crew leader to be carrying any number of specific
items before `/robbery start` lets them through - a lockpick, a keycard,
whatever fits your server. Every item on the list must be present; there's
no "any one of" option.

## Editing in-game

```
/robbery reqeditor <id>
```

(or click **Required Items** from inside the [loot editor](Loot-Tables.md))

| Action | Effect |
|---|---|
| Left-click | Toggle Consume On Use |
| Press 1-9 while hovering | Remove the item |

- **Add Item** - adds whatever's in your hand as a new required item
  (Consume On Use starts off)
- **Save & Close** - writes changes back to the robbery's file
- **Back To Loot Editor** - returns to the loot editor without leaving the
  robbery

## yml reference

```yaml
Required-Items:
  1:
    Material: TRIPWIRE_HOOK    # item type required
    Name: "&bMaster Lockpick"  # custom name to match, blank = match any item of that Material
    Consume-On-Use: false      # whether one is taken from the leader's inventory on a successful start
```

An empty list (`Required-Items: {}`) means no requirement at all - the
robbery starts as soon as every other condition (crew size, cooldown,
online players, region) is met.

If a leader is missing an item, they get a message naming it and the
robbery doesn't start. Nothing is consumed unless the start actually
succeeds - a leader missing a required item never loses items they did
have.
