# `0x08` EndGame

### Host-to-Game

This message is sent from the host of a game to all clients when the host determines that the game has ended.

> **Note**: The [game state](../01_packet_structure/06_enums.md#gamestate) is set to `Ended` when this message is sent, and the list of clients in the game will be cleared.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `byte` | Game Over Reason | The ID of the [game over reason](../01_packet_structure/06_enums.md#gameoverreason) for why the game came to an end |
| `boolean` | Show Ad | Whether or not an ad should be displayed to mobile clients |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
01ba            # Nonce
060008          # Hazel message (tag of 0x08 = EndGame)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    00          # Game Over Reason: 0 (CREWMATES_BY_VOTE)
    01          # Show Ad: True
```
</details>

---

> Previous section: [`0x07` JoinedGame](07_joinedgame.md)<br>
> Next section: [`0x09` GetGameList](09_getgamelist.md)
