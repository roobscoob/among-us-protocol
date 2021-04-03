# `0x20` UsePlatform

This *empty* message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object when using a floating platform.

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
01a4            # Nonce
090005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    020002      # Hazel message (tag of 0x02 = RPC)
        4b      # Sender (PlayerControl) Net ID: 75
        20      # RPC Call ID: 32 (UsePlatform)
```
</details>

---

> Previous section: [`0x1f` ClimbLadder](31_climbladder.md)
