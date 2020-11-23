# `0x1b` CloseDoorsOfType

This message is sent by the [`ShipStatus`](../05_innernetobject_types/00_shipstatus.md) object when doors are closed by an impostor.

> **Note**: This message is sent from a player to the host of a game via [`0x06` GameDataTo](../02_root_message_types/06_gamedatato.md). It is **never** sent from the host of a game.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | System ID | The ID of the room ([`SystemType`](../01_packet_structure/06_enums.md#systemtype)) whose doors were closed |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0087            # Nonce
0d0006          # Hazel message (tag of 0x06 = GameDataTo)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    bd920f      # Target Client ID: 248125
    030002      # Hazel message (tag of 0x02 = RPC)
        6d      # Sender (ShipStatus) Net ID: 109
        1b      # RPC Call ID: 27 (CloseDoorsOfType)
        0a      # System ID: 10 (MEDBAY; closed doors to Medbay)
```
</details>

---

> Previous section: [`0x1a` AddVote](26_addvote.md)<br>
> Next section: [`0x1c` RepairSystem](28_repairsystem.md)
