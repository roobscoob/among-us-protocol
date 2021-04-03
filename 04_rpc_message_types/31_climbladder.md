# `0x1f` ClimbLadder

This message is sent by a client's [`PlayerPhysics`](../05_innernetobject_types/09_playerphysics.md) component when climbing a ladder.

> **Note**: Each map has its own set of ladders and associated IDs that can be found [here](../07_miscellaneous/04_map_specific_ids_for_interactables.md).

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Ladder ID | The ID of the ladder on which the player is climbing |
| `byte` | Sequence ID | A nonce used to prevent older messages from causing desynchronization |

<details>
    <summary>Click here to view an example packet from a game on <i>The Airship</i></summary>

```
01              # Reliable packet
01a4            # Nonce
0c0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    050002      # Hazel message (tag of 0x02 = RPC)
        bd01    # Sender (PlayerPhysics) Net ID: 189
        1f      # RPC Call ID: 31 (ClimbLadder)
        05      # Ladder ID: 5 (Electrical to Main Hall)
        02      # Sequence ID: 2
```
</details>

---

> Previous section: [`0x1d` SetTasks](29_settasks.md)<br>
> Next section: [`0x20` UsePlatform](32_useplatform.md)
