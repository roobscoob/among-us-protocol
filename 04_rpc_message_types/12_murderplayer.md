# `0x0c` MurderPlayer

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a game when killing another player.

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Victim Net ID | The net ID of the victim who was murdered |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
018d            # Nonce
0a0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    030002      # Hazel message (tag of 0x02 = RPC)
        61      # Sender (PlayerControl) Net ID: 97
        0c      # RPC Call ID: 12 (MurderPlayer)
        64      # Victim Net ID: 100
```
</details>

---

> Previous section: [`0x0b` ReportDeadBody](11_reportdeadbody.md)<br>
> Next section: [`0x0d` SendChat](13_sendchat.md)
