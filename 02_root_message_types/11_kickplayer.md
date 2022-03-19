# `0x0b` KickPlayer

### Host-to-Game

This message is sent from the host of a game to all clients when the host kicks or bans a client from the game.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `packed int32` | Kicked Client ID | The ID of the client that was kicked |
| `boolean` | Is Banned | Whether or not the client was also banned |
| `byte` (*Optional*) | Disconnect Reason | The ID of the [disconnect reason](../01_packet_structure/06_enums.md#disconnectreason) for why the client was kicked |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
01dc            # Nonce
09000b          # Hazel message (tag of 0x0b = KickPlayer)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    fbea11      # Kicked Client ID: 292219
    00          # Is Banned: False
    07          # Disconnect Reason: 7 (KICKED)
```
</details>

---

> Previous section: [`0x0a` AlterGame](10_altergame.md)<br>
> Next section: [`0x0c` WaitForHost](12_waitforhost.md)
