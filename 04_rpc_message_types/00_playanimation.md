# `0x00` PlayAnimation

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a game and tells other clients to play an animation associated with a visual [task](../01_packet_structure/06_enums.md#tasktype).

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md) inside a [`0x00` Normal](../01_packet_structure/05_packet_types.md#0x00-normal) packet.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Task ID | The ID of the [task](../01_packet_structure/06_enums.md#tasktype) whose animation should be played |

<details>
    <summary>Click here to view an example packet</summary>

```
00              # Normal packet
0b0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    040002      # Hazel message (tag of 0x02 = RPC)
        c706    # Sender (PlayerControl) Net ID: 839
        00      # RPC Call ID: 0 (PlayAnimation)
        06      # Task ID: 6 (Clear Asteroids; this is the cannon animation for shooting the asteroids)
```
</details>

---

> Next section: [`0x01` CompleteTask](01_completetask.md)<br>
