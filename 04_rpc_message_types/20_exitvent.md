# `0x14` ExitVent

This message is sent by a client's [`PlayerPhysics`](../05_innernetobject_types/09_playerphysics.md) component when exiting a vent.

> **Note**: Each map has its own set of vents and associated IDs that can be found [here](../07_miscellaneous/04_map_specific_ids_for_vents_and_tasks.md).

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Vent ID | The ID of the vent that the player exited |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
00fc            # Nonce
0b0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    040002      # Hazel message (tag of 0x02 = RPC)
        bd01    # Sender (PlayerPhysics) Net ID: 189
        14      # RPC Call ID: 20 (ExitVent)
        08      # Vent ID: 8
```
</details>

---

> Previous section: [`0x13` EnterVent](19_entervent.md)<br>
> Next section: [`0x15` SnapTo](21_snapto.md)
