# `0x0e` StartMeeting

This message is sent by the host's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a game after receiving a [`0x0b` ReportDeadBody](11_reportdeadbody.md) message from a client.

> **Note**: This message is sent from the host of a game to all clients via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Victim Player ID | The ID of the player whose body was found<br><br>**Note**: This will be 255 (`0xff`) if pressing the emergency meeting button |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
017d            # Nonce
0b0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    040002      # Hazel message (tag of 0x02 = RPC)
        bf01    # Sender (PlayerControl) Net ID: 191
        0b      # RPC Call ID: 14 (StartMeeting)
        ff      # Victim Player ID: 255 (no body was found)
```
</details>

---

> Previous section: [`0x0d` SendChat](13_sendchat.md)<br>
> Next section: [`0x0f` SetScanner](15_setscanner.md)
