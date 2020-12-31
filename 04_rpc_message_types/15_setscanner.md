# `0x0f` SetScanner

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a game when starting or stopping a Medbay scan, or when being killed by an impostor.

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `boolean` | Is Scanning | Whether or not the player is currently being scanned |
| `byte` | Sequence ID | This value is incremented per-player every time this message is sent, and is used to keep the scanning animation in sync across all clients |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0036            # Nonce
0c0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    050002      # Hazel message (tag of 0x02 = R{C})
        bf01    # Sender (PlayerControl) Net ID: 191
        0f      # RPC Call ID: 15 (SetScanner)
        00      # Is Scanning: False
        01      # Count: 1
```
</details>

---

> Previous section: [`0x0e` StartMeeting](14_startmeeting.md)<br>
> Next section: [`0x10` SendChatNote](16_sendchatnote.md)
