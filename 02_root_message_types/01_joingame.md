# `0x01` JoinGame

### Request: Client-to-Server

This message is sent from the client to the server when attempting to join a gamem.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `byte` | Owned Maps | A bitfield containing the IDs of the [maps](../01_packet_structure/06_enums.md#map) that the player owns<br><br>Since all maps are now free, this will always be `0x07` |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0003            # Nonce
050001          # Hazel message (tag of 0x01 = JoinGame)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    07          # Owned Maps: The Skeld, Mira HQ, Polus
```
</details>

### Response: Server-to-Client

This message is sent from the server to the client after attempting to join a game.

If the client joined the game successfully, the message will follow this structure:

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `uint32` | Player Client ID | The client ID of the joining player |
| `uint32` | Host Client ID | The client ID of the player that is the current host of the game |

<details>
    <summary>Click here to view an example success packet</summary>

```
01              # Reliable packet
001b            # Nonce
0c0001          # Hazel message (tag of 0x01 = JoinGame)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    58c90400    # Player Client ID: 313688
    4ec20400    # Host Client ID: 311886
```
</details>

If the client could not join the game, the message will follow this structure:

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Disconnect Reason | The ID of the [disconnect reason](../01_packet_structure/06_enums.md#disconnectreason) for why the game could not be joined |

<details>
    <summary>Click here to view an example error packet</summary>

```
01              # Reliable packet
0001            # Nonce
040001          # Hazel message (tag of 0x01 = JoinGame)
    01000000    # Disconnect reason: 1 (GAME_FULL)
```
</details>

---

> Previous section: [`0x00` HostGame](00_hostgame.md)<br>
> Next section: [`0x02` StartGame](02_startgame.md)
