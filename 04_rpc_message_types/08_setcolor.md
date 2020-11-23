# `0x08` SetColor

This message is sent by the host's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a lobby to set a joining client's [`Color`](../01_packet_structure/06_enums.md#color) after receiving a [`0x07` CheckColor](07_checkcolor.md) message from the client.

> **Note**: This message is sent from the host of a game to all players via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Color ID | The ID of the player's new [`Color`](../01_packet_structure/06_enums.md#color) |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
003b            # Nonce
210005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    030002      # Hazel message (tag of 0x02 = RPC)
        4b      # Sender (PlayerControl) Net ID: 75
        08      # RPC Call ID: 8 (SetColor)
        08      # Color ID: 8 (PURPLE)
```
</details>

---

> Previous section: [`0x07` CheckColor](07_checkcolor.md)<br>
> Next section: [`0x09` SetHat](09_sethat.md)
