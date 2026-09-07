# Commands and Permissions

Base command: `/robbery` (aliases: `/rob`, `/kr`)

## Player commands

Require `robbery.use` (default: everyone).

| Command | Description |
|---|---|
| `/robbery help` | Shows this list in-game |
| `/robbery start <id>` | Start a robbery as your crew's leader |
| `/robbery list` | List every configured robbery |
| `/robbery crew` | Open (or create) your crew menu |
| `/robbery invite <player>` | Invite a player - leader only |
| `/robbery accept` / `decline` | Respond to a pending invite |
| `/robbery kick <player>` | Remove a member - leader only |
| `/robbery leave` | Leave your current crew |
| `/robbery disband` | Disband your crew - leader only |
| `/robbery top` | Show the robbery leaderboard |

Crews can also be invited to from the Crew GUI directly: the leader clicks
an empty slot's invite icon, then types a name in chat within
`Crew.Invite-Prompt-Seconds`.

## Admin commands

Require `robbery.admin` (default: op).

| Command | Description |
|---|---|
| `/robbery give drill <player>` | Give the vault drill |
| `/robbery getstick` | Get the structure removal stick |
| `/robbery structure` | Get the table/safe/jewelry/vault door placement blocks |
| `/robbery editor <id>` | Edit a robbery's loot tables |
| `/robbery reqeditor <id>` | Edit a robbery's required items |
| `/robbery create <id>` | Create a new robbery at your current location |
| `/robbery delete <id>` | Delete a robbery |
| `/robbery reload` | Reload every config file |

## Permissions

| Node | Default | Effect |
|---|---|---|
| `robbery.use` | everyone | Access to any `/robbery` subcommand |
| `robbery.admin` | op | Access to the admin subcommands above |
| `robbery.bypass.cooldown` | op | Ignore a robbery's cooldown |
| `robbery.bypass.crewsize` | op | Ignore a robbery's `Required-Crew-Size` |
