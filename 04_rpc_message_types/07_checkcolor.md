# `0x07` CheckColor

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object when joining a game to check with the host if the [`Color`](../01_packet_structure/06_enums.md#color) is available for use. If the color is already being used, the host updates the client's color to the next available color.

> **Note**: This message is sent from a client to the host of a game via [`0x06` GameDataTo](../02_root_message_types/06_gamedatato.md). It is **never** sent from the host of a game.

Example:

```
Client #1 joins with color RED
Client #1 sends CheckColor
Host sends SetColor for Client #1 with color RED
Client #2 joins with color RED
Client #2 sends CheckColor
Host sends SetColor for Client #2 with color BLUE
```

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Color ID | The ID of the player's [`Color`](../01_packet_structure/06_enums.md#color) |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0005            # Nonce
0d0006          # Hazel message (tag of 0x06 = GameDataTo)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    84a210      # Target Client ID: 266500
    030002      # Hazel message (tag of 0x02 = RPC)
        4b      # Sender (PlayerControl) Net ID: 75
        07      # RPC Call ID: 7 (CheckColor)
        08      # Color ID: 8 (PURPLE)
```
</details>

---

> Previous section: [`0x06` SetName](06_setname.md)<br>
> Next section: [`0x08` SetColor](08_setcolor.md)
