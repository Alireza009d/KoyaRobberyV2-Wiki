# Discord

KoyaRobbery can post a Discord embed whenever a crew **starts**,
**succeeds**, or **fails** a robbery. Unlike most plugins with a single
hardcoded webhook message, every robbery has its own fully customizable
set of three embeds and can even use its own webhook - a bank heist and a
gun store robbery can post to two different channels with completely
different styling.

## Turning it on

Two switches need to both be on:

1. **`config.yml`** - the master switch and a fallback webhook:

   ```yaml
   Discord:
     Enabled: false
     Webhook-Url: "" # used by any robbery that doesn't set its own
   ```

2. **Each robbery's `Discord.Enabled`** (in `robberies/<id>.yml`) - see below.

If either is `false`/missing, that robbery stays silent.

## Per-robbery config

Every `robberies/<id>.yml` gets its own `Discord:` section:

```yaml
Discord:
  Enabled: true
  Webhook-Url: "" # this robbery's own webhook, blank = use config.yml's

  Started:   # posted the moment a crew starts this robbery
    Enable: true
    Title: "🚨 Robbery Started"
    Description: "**%leader%** just started robbing **%robbery%**!\n**Crew:** %robbers%"
    Color: "#F1C40F"
    Url: ""
    Thumbnail-Url: ""
    Image-Url: ""
    Author-Name: ""
    Author-Icon-Url: ""
    Author-Url: ""
    Footer-Text: "KoyaRobbery • %robbery%"
    Footer-Icon-Url: ""

  Success:   # posted when the crew finishes successfully
    Enable: true
    Title: "✅ Robbery Completed"
    Description: "**%leader%**'s crew successfully robbed **%robbery%**!\n**Crew:** %robbers%"
    Color: "#2ECC71"
    # ... same fields as Started

  Failed:    # posted when the robbery fails (leader left, crew wiped, escape failed...)
    Enable: true
    Title: "❌ Robbery Failed"
    Description: "**%leader%**'s crew failed to rob **%robbery%**.\n**Crew:** %robbers%"
    Color: "#E74C3C"
    # ... same fields as Started
```

`Started`, `Success`, and `Failed` are independent - disable just one with
its own `Enable: false` if, say, you only want failures reported.

## Field reference

| Field | Required | Notes |
|---|---|---|
| `Enable` | - | Turns this specific embed (Started/Success/Failed) on or off. |
| `Title` | no | Embed title. Leave blank to omit it. |
| `Description` | no | Main embed text. Supports `\n` for line breaks. |
| `Url` | no | Makes the title a clickable link. |
| `Color` | no | Hex color for the embed's side bar, e.g. `"#F1C40F"` or `F1C40F`. A plain decimal number (Discord's native format) also works. Blank = Discord's default grey. |
| `Thumbnail-Url` | no | Small image, top-right corner of the embed. |
| `Image-Url` | no | Large image, shown below the description. |
| `Author-Name` | no | Small line above the title - e.g. your server's name. |
| `Author-Icon-Url` | no | Tiny icon next to `Author-Name`. |
| `Author-Url` | no | Makes `Author-Name` a clickable link. |
| `Footer-Text` | no | Small text at the bottom of the embed. |
| `Footer-Icon-Url` | no | Tiny icon next to `Footer-Text`. |

Every text field above (`Title`, `Description`, `Url`, `Author-Name`,
`Author-Url`, `Author-Icon-Url`, `Footer-Text`, `Footer-Icon-Url`,
`Thumbnail-Url`, `Image-Url`) can contain the placeholders below - so, for
example, `Image-Url` could point to a per-robbery banner using `%robbery%`
in the filename if you're hosting your own images.

## Placeholders

| Placeholder | Example |
|---|---|
| `%leader%` | `Test1` |
| `%robbery%` | `Central Bank` |
| `%robbers%` | `Test1, Test2, Test3` - every online crew member, comma-separated |
| `%crew_size%` | `3` |

## Getting a webhook URL

In Discord: **Server Settings → Integrations → Webhooks → New Webhook**,
pick a channel, then **Copy Webhook URL**. Paste that into either
`config.yml`'s `Discord.Webhook-Url` (shared default) or a specific
robbery's own `Discord.Webhook-Url` (that robbery only).

## Troubleshooting

- **Nothing posts at all** - check `Discord.Enabled: true` in *both*
  `config.yml` and the robbery's own yml, and that a webhook URL is set
  somewhere (robbery-specific or the global fallback).
- **Some embeds post, others don't** - each of `Started`/`Success`/`Failed`
  has its own `Enable` flag; check the one that's missing.
- Webhook requests run off the main thread and fail silently into the
  console log (not chat) if Discord is unreachable or the URL is wrong -
  check your server console/log for `Discord webhook failed: ...` if
  messages aren't showing up.
