# `0x0a` SetSkin

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object when joining a game or when customizing their [`Skin`](../01_packet_structure/06_enums.md#skin) in the lobby.

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Skin ID | The ID of the player's new [`Skin`](../01_packet_structure/06_enums.md#skin) |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0043            # Nonce
210005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    030002      # Hazel message (tag of 0x02 = RPC)
        4b      # Sender (PlayerControl) Net ID: 75
        0a      # RPC Call ID: 10 (SetSkin)
        0e      # Skin ID: 14 (WINTER)
```
</details>

---

> Previous section: [`0x09` SetHat](09_sethat.md)<br>
> Next section: [`0x0b` ReportDeadBody](11_reportdeadbody.md)
