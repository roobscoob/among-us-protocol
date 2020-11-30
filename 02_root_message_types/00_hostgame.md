# `0x00` HostGame

### Request: Client-to-Server

This message is sent from the client to the server when attempting to create a game.

| Type | Name | Description |
| --- | --- | --- |
| [`GameOptionsData`](../07_miscellaneous/01_the_structure_of_the_gameoptionsdata_object.md) | Game Options Data | The settings used when creating the game<br><br>**Note**: The map ID in this Game Options Data is the ID of the [`Map`](../01_packet_structure/06_enums.md#map) |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0002            # Nonce
2b0000          # Hazel message (tag of 0x00 = HostGame)
    2a          # Game Options Data Length: 42
    02          # Game Optiona Data Version: 2
    0a          # Max Number of Players: 10
    00010000    # Keywords: 256 (English)
    02          # Map: 2 (Polus)
    0000803f    # Player Speed Modifier: 1.0x
    0000003f    # Crewmate Light Modifier: 0.5x
    0000c03f    # Impostor Light Modifier: 1.5x
    0000f041    # Kill Cooldown: 30s
    02          # Number of Common Tasks: 2
    01          # Number of Long Tasks: 1
    05          # Number of Short Tasks: 5
    01000000    # Number of Emergency Meetings: 1
    02          # Number of Impostors: 2
    00          # Kill Distance: 0 (Short)
    0f000000    # Discussion Time: 15s
    78000000    # Voting Time: 120s
    00          # Is Defaults: False
    0f          # Emergency Cooldown: 15s
```
</details>

### Response: Server-to-Client

This message is sent from the server to the client after creating a game and tells the client the ID of the newly created game.

With this game ID, the client will immediately send a [`0x01` JoinGame](01_joingame.md) packet.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0001            # Nonce
040000          # Hazel message (tag of 0x00 = HostGame)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
```
</details>

---

> Next section: [`0x01` JoinGame](01_joingame.md)
