# `0x15` SnapTo

This message is sent by a client's [`CustomNetworkTransform`](../05_innernetobject_types/10_customnetworktransform.md) component when moving between [vents](../07_miscellaneous/04_map_specific_ids_for_interactables.md) and when selecting a spawn point on *The Airship*. The player's velocity is set to zero as a side effect of this message.

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `Vector2` | Position | The new position of the player (see [The `Vector2` Type](../01_packet_structure/04_the_vector2_type.md)) |
| `uint16` | Last Sequence ID | The ID of the player's last movement sequence |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
00fa            # Nonce
100005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    090002      # Hazel message (tag of 0x02 = RPC)
        be01    # Sender (CustomNetworkTransform) Net ID: 190
        15      # RPC Call ID: 21 (SnapTo)
        65c6    # X Coordinate: ~ 21.999
        275a    # Y Coordinate: ~ -11.826
        8701    # Last Sequence ID: 391
```
</details>

---

> Previous section: [`0x14` ExitVent](20_exitvent.md)<br>
> Next section: [`0x16` Close](22_close.md)
