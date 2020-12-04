# `0x11` SetPet

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object when joining a game or when customizing their [`Pet`](../01_packet_structure/06_enums.md#pet) in the lobby.

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Pet ID | The ID of the player's new [`Pet`](../01_packet_structure/06_enums.md#pet) |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0041            # Nonce
210005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    030002      # Hazel message (tag of 0x02 = RPC)
        4b      # Sender (PlayerControl) Net ID: 75
        11      # RPC Call ID: 17 (SetPet)
        02      # Pet ID: 2 (MINI_CREWMATE)
```
</details>

---

> Previous section: [`0x10` SendChatNote](16_sendchatnote.md)<br>
> Next section: [`0x12` SetStartCounter](18_setstartcounter.md)
