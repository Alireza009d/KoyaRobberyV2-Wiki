# GUI Customization

Every GUI in the plugin is customizable, split across two files by what
kind of thing is being changed:

- **`gui.yml`** - layout: materials, slots, row counts, border blocks.
  Nothing here is text.
- **`lang/<locale>.yml`, under the `GUI` section** - every title, item
  name, and lore line. Since this lives in the language file, GUI text is
  translated the same way chat messages are - see [Localization](Localization.md).

## gui.yml

```yaml
Crew:
  Rows: 4
  Border-Material: GRAY_STAINED_GLASS_PANE
  Info-Slot: 4
  Member-Start-Slot: 20
  Action-Slot: 8
  Empty-Material: BARRIER
  Invite-Material: LIME_DYE

Lockpick:
  Border-Material: GRAY_STAINED_GLASS_PANE
  Center-Material: CONDUIT
  Pending-Material: RED_STAINED_GLASS_PANE
  Progress-Material: ORANGE_STAINED_GLASS_PANE
  Done-Material: GREEN_STAINED_GLASS_PANE

StructureAdmin:
  Border-Material: GRAY_STAINED_GLASS_PANE

LootEditor:
  Border-Material: GRAY_STAINED_GLASS_PANE
  Add-Material: LIME_STAINED_GLASS_PANE
  Save-Material: EMERALD_BLOCK
```

Change any material to reskin that slot - Bukkit `Material` enum names
only, no custom item support here (the loot/required-item icons themselves
show the actual configured item, this only covers the surrounding menu
chrome).

## The GUI section of lang/<locale>.yml

Every piece of text a GUI shows lives here, grouped by GUI:

```yaml
GUI:
  Crew:
    Title: "&8Crew Menu"
    Info-Name: "&6&lCrew Info"
    Empty-Name: "&7Empty Slot"
    Invite-Name: "&a&lInvite Player"
    Invite-Lore:
      - "&7Click, then type a player's"
      - "&7name in chat within &f%seconds%s"
    # ...
  Lockpick:
    Title: "&8Lock Picking..."
  StructureAdmin:
    Title: "&8Structures"
  LootEditor:
    Title-Prefix: "&8Editing: "
    Item-Lore: [...]
  RequiredItems:
    Title-Prefix: "&8Required Items: "
  StartRobbery:
    Title-Prefix: "&8Start: "
```

Placeholders (`%seconds%`, `%chance%`, `%price%`, etc.) are documented
inline in the bundled files - each one is filled in with live data when
the GUI renders. Colour codes use the standard `&` format.

## Which GUIs exist

| GUI | Opened by |
|---|---|
| Crew Menu | `/robbery crew` |
| Lock Picking | Interacting with a safe |
| Structures | `/robbery structure` (admin) |
| Loot Editor | `/robbery editor <id>` (admin) |
| Required Items | `/robbery reqeditor <id>` (admin), or a button inside the Loot Editor |
| Start Robbery | Right-clicking a linked Citizens NPC (see [Robberies](Robberies.md)) |
