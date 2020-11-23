# `0x04` RemovePlayer

### Host-to-Client

This message is sent from the host of a game to a client that is attempting to join the game when it is already full.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `packed uint32` | Player Client ID | The client ID of the player that was disconnected |
| `byte` | Disconnect Reason | The ID of the [disconnect reason](../01_packet_structure/06_enums.md#disconnectreason) for why the player was disconnected |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0085            # Nonce
080004          # Hazel message (tag of 0x04 = RemovePlayer)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    bdff0b      # Player Client ID: 196541
    01          # Disconnect Reason: 1 (GAME_FULL)
```
</details>

### Server-to-Game

This message is sent from the server to all clients in a game when another player leaves the game.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `uint32` | Player Client ID | The client ID of the player that was disconnected |
| `uint32` | Host Client ID | The client ID of the player that is now the current host of the game |
| `byte` (*Optional*) | Disconnect Reason | The ID of the [disconnect reason](../01_packet_structure/06_enums.md#disconnectreason) for why the player was disconnected |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0016            # Nonce
0d0004          # Hazel message (tag of 0x04 = RemovePlayer)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    bdff0200    # Player Client ID: 196541
    48ff0200    # Host Client ID: 196424
    00          # Disconnect Reason: 0 (EXIT_GAME)
```
</details>

---

> Previous section: [`0x03` RemoveGame](03_removegame.md)<br>
> Next section: [`0x05` GameData](05_gamedata.md)
