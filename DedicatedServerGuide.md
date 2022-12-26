# Dedicated Server Setup Guide

## Requirements

- Ability to port forward
- An IPv4 network address

## Install

- Install [SteamCMD](https://developer.valvesoftware.com/wiki/SteamCMD) on to the computer hosting the server.
- Launch SteamCMD and install AppId `2261800`
- Quit SteamCMD

## Configure

- In the folder with the dedicated server files, run `SCPLR_rcon` with the arguments `-port <port> -publicport <port> -rconport <port_for_rcon> -rconkey <rcon_password> -publicip <your.public.ipv4>`
- - It's a good idea to save this command as a `.bat` on Windows, and `.sh` (with execute permissions) on Linux
- After the console says something to the effect of `Server online`, type `quit` into the console to shutdown the server
- Two-three files next to the server executable should have been created
- - `bans.json`
- - - Ban database
- - `roles.json`
- - - Role database
- - `server_config.ini`
- - - Server configuration file

### Server config

```ini
ServerName = SERVER NAME HERE
OwnerSteamId = Server Owners SteamId64 Here
Region = World
RegionDirection = None
ServerNumber = -1
Public = False
PastebinId = Pastebin raw Id
MaxPlayers = 5
GameMode = Normal
```

- Do not change the `GameMode` at this time.
- This file is probably going to be changed to `json` in the future

#### Regions

- World
- Africa
- Asia
- Australia
- Canada
- China
- Europe
- Germany
- Japan
- Mexico
- Russia
- UnitedKingdom
- UnitedStates

#### RegionDirections

- None
- Central
- North
- South
- East
- West

### Bans

Example `bans.json` file
```json
{
    "IPBans": {
        "192.168.1.1": {
            "BannedIdentity": "192.168.1.1",
            "BanReason": "Violation of rule X + Local IP spoofing"
        }
    },
    "UserIdBans": {
        "Steam64IdHere@steam": {
            "BannedIdentity": "Steam64IdHere@steam",
            "BanReason": "Violation of rule Y"
        },
        "BezbroGamesAccountId@bbg": {
            "BannedIdentity": "BezbroGamesAccountId@bbg",
            "BanReason": "Violation of rule Z"
        }
    }
}
```

### Roles

Example `roles.json` file
```json
{
    "UserIdRoles": {
        "BezbroGamesAccountId@bbg": "admin",
        "Steam64IdHere@steam": "moderator"
    },
    "Roles": {
        "admin": {
            "Identifier": "admin",
            "DisplayName": "Admin Member",
            "BanPower": 1000,
            "IsVisible": false,
            "Permissions": [
                "kick",
                "ban",
                "tp.player",
                "tp.room",
                "spawn.item",
                "spawn.npc"
            ]
        },
        "moderator": {
            "Identifier": "moderator",
            "DisplayName": "Moderation Team Member",
            "BanPower": 10,
            "IsVisible": true,
            "Permissions": [
                "kick",
                "ban",
                "tp.player"
            ]
        }
    }
}
```
