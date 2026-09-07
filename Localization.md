# Localization

Every player-facing string in the plugin - chat messages, action bar text,
and every GUI title/name/lore - lives in `lang/<locale>.yml`. Nothing is
hardcoded in the plugin's code.

## Switching language

Set `Locale` in `config.yml` to the file name (without `.yml`) you want
active:

```yaml
Locale: en   # or: fa
```

Ships with `en.yml` (English) and `fa.yml` (Finglish - Persian written in
Latin script). Run `/robbery reload` after changing it.

## How lookups work

If a key is missing from the active locale's file, the plugin falls back
to `en.yml` for that one key rather than showing a blank message - so a
partial translation never breaks anything, it just shows English for
whatever hasn't been translated yet.

## File layout

Two top-level sections:

- Everything **outside** `GUI:` - chat messages, action bar text,
  economy/leaderboard/editor feedback. These automatically get the
  `Prefix` value prepended.
- **`GUI:`** - every GUI's text, grouped by GUI name (see
  [GUI Customization](GUI-Customization.md)). Never gets the chat prefix,
  since it's shown inside item lore/titles, not the chat log.

```yaml
Prefix: "&8[&6KoyaRobbery&8]&r "

NEED_PERMISSION: "&7You don't have permission to do that."
# -> shown as: [KoyaRobbery] You don't have permission to do that.

GUI:
  Crew:
    Title: "&8Crew Menu"
    # -> shown as the GUI title, no prefix
```

## Adding a new language

1. Copy `lang/en.yml` to `lang/<your-locale>.yml` inside
   `plugins/KoyaRobbery/lang/`.
2. Translate every value (the keys/paths on the left must stay exactly as
   they are - only the text on the right changes).
3. Keep every `%placeholder%` token exactly as written; the plugin
   substitutes those with live data.
4. Set `Locale: <your-locale>` in `config.yml` and `/robbery reload`.

Colour codes use the standard `&` format (`&a`, `&c`, `&l`, ...) and work
identically in every locale.
