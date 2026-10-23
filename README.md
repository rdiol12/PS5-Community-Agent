<p align="center"><a href="https://www.buymeacoffee.com/rdiol12" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" height="60" width="217"></a></p>

# PS5 Community Agent

> **Alpha software:** this build is experimental. Multiplayer is still under development and may fail, hang, or require an updated profile. Use it only on a console and game copy you own.

PS5 Community Agent connects a jailbroken PS5 to the PS5 Community master service. It identifies supported games exposed by ShadowMount Plus, downloads only a signed compatibility profile, verifies the local game files, prepares the required overlay, and requests short-lived connection details when a supported game starts.

The agent does not include game files, does not emulate PSN, and does not route gameplay traffic through itself. After authorization, a supported game communicates with its assigned game backend directly.

## First connection

The first run creates a console identity and begins pairing with the master service. The connection remains **pending until a master-server administrator approves it**. A console cannot download profiles or obtain game-server access before approval.

Approval is currently manual while the project is in Alpha.

## How it works

1. The agent loads its local configuration and saved console credential.
2. It connects to the Community Master over HTTPS.
3. On first use, it starts the pairing and administrator-approval flow.
4. Once approved, it asks the master for the list of supported title IDs.
5. It reads the local game inventory from ShadowMount Plus.
6. For a matching game, it verifies the title, content ID, version, executable hash, and signed profile.
7. It prepares the minimal ShadowMount overlay without distributing the full game.
8. When the game starts, the agent obtains short-lived backend credentials and starts the game session.
9. When the game closes, the session is closed and game-specific work stops.

## Supported games

| Game | Title ID | Content ID | Supported version | Status |
| --- | --- | --- | --- | --- |
| RoadCraft | `PPSA09845` | `UP4133-PPSA09845_00-ROADBUILDERGAME0` | `01.009.610` | Alpha |

Other editions, regions, versions, or executable hashes are rejected unless the master service publishes a matching signed profile.

## Requirements

- A jailbroken PS5 supported by the required homebrew environment
- ShadowMount Plus running and able to report the installed game
- Network access to the configured Community Master
- A configuration provisioned by the project administrator
- A legally owned copy of the supported game and version

This binary is not a standalone game server. RoadCraft backend functionality is provided separately by the Community service.

## Binary

File: `ps5-community-agent.elf`

- Size: `8,425,448` bytes
- SHA-256: `4ec9e1ec3b3618edaef21e059fe84bca17d37067d0530e9fcf64d2f089b03509`

Verify the hash before loading the ELF. Do not use binaries redistributed under a different hash.

## Current limitations

- Alpha testing is restricted to administrator-approved consoles.
- Only the RoadCraft build listed above is supported.
- Stable end-to-end multiplayer has not yet been declared complete.
- The agent currently depends on ShadowMount Plus for game discovery and overlay loading.
- No source code or copyrighted game content is distributed in this repository.
