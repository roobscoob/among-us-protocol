# `0x02` StartGame

### Host-to-Game

This message is sent from the host of a game to all clients when the host starts the game. Clients must respond with a [`0x07` Ready](../03_gamedata_and_gamedatato_message_types/07_ready.md) packet or they will be disconnected.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0067            # Nonce
040002          # Hazel message (tag of 0x02 = StartGame)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
```
</details>

---

> Previous section: [`0x01` JoinGame](01_joingame.md)<br>
> Next section: [`0x03` RemoveGame](03_removegame.md)
