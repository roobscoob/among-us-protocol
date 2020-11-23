# `0x10` SendChatNote

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a game when sending a [chat note](../01_packet_structure/06_enums.md#chatnotetype).

> **Note**: This message is sent to and from all players in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Player ID | The ID of the player who sent the note |
| `byte` | Chat Note Type | The ID of the chat note type that the player sent |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
008c            # Nonce
130005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    050002      # Hazel message (tag of 0x02 = RPC)
        ad01    # Sender (PlayerControl) Net ID: 173
        10      # RPC Call ID: 16 (SendChatNote)
        04      # Player ID: 4
        00      # Chat Note Type: 0 (DID_VOTE)
```
</details>

---

> Previous section: [`0x0f` SetScanner](15_setscanner.md)<br>
> Next section: [`0x11` SetPet](17_setpet.md)
