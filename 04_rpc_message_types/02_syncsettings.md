# `0x02` SyncSettings

This message is sent by the host's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a lobby to sync the game settings with all other clients.

> **Note**: This message is sent from the host of a game to all players via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| [`GameOptionsData`](../07_miscellaneous/01_the_structure_of_the_gameoptionsdata_object.md) | Game Options Data | The settings for the game<br><br>**Note**: The map ID in this Game Options Data is the ID of the [`Map`](../01_packet_structure/06_enums.md#map) |

<details>
    <summary>Click here to view an example packet</summary>

```
01                  # Reliable packet
00ec                # Nonce
380005              # Hazel message (tag of 0x05 = GameData)
    d3503f8a        # Game ID: -1975562029 (REDSUS)
    310002          # Hazel message (tag of 0x02 = RPC)
        04          # Sender (PlayerControl) Net ID: 4
        02          # RPC Call ID: 2 (SyncSettings)
        2e          # Game Options Data Length: 46
        04          # Game Optiona Data Version: 4
        0a          # Max Number of Players: 10
        01000000    # Keywords: 1 (Other)
        01          # Map: 1 (Mira HQ)
        0000803f    # Player Speed Modifier: 1.0x
        0000803f    # Crewmate Light Modifier: 1.0x
        0000c03f    # Impostor Light Modifier: 1.5x
        00003442    # Kill Cooldown: 45s
        01          # Number of Common Tasks: 1
        01          # Number of Long Tasks: 1
        02          # Number of Short Tasks: 2
        01000000    # Number of Emergency Meetings: 1
        01          # Number of Impostors: 1
        01          # Kill Distance: 1 (MEDIUM)
        0f000000    # Discussion Time: 15s
        78000000    # Voting Time: 120s
        01          # Is Defaults: True
        0f          # Emergency Cooldown: 15s
        01          # Confirm Ejects: True
        01          # Visual Tasks: True
        00          # Anonymous Votes: False
        00          # Task Bar Updates: 0 (ALWAYS)
```
</details>

---

> Previous section: [`0x01` CompleteTask](01_completetask.md)<br>
> Next section: [`0x03` SetInfected](03_setinfected.md)
