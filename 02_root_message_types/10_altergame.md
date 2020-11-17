# `0x0a` AlterGame

### Host-to-Game

This message is sent from the host of a game to all clients when the host changes a [game tag](../01_packet_structure/06_enums.md#altergametag).

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `byte` | Tag ID | The ID of the game tag that was altered |
| `byte` | Tag Value | The new value of the game tag |

As there is currently only one game tag, whose value is of type `boolean`, the tag value may be coerced into a `boolean`. Do note that this may change in the future.

<details>
    <summary>Click here to view an example packet</summary>

```
made private
01              # Reliable packet
0098            # Nonce
06000a          # Hazel message (tag of 0x0a = AlterGame)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    01          # Tag ID: 1 (CHANGE_PRIVACY)
    00          # Tag Value: 0 (False; private game)
```
</details>

---

> Previous section: [`0x09` GetGameList](09_getgamelist.md)<br>
> Next section: [`0x0b` KickPlayer](11_kickplayer.md)
