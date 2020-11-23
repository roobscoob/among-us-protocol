# `0x03` RemoveGame

### Server-to-Client

This message is sent from the server to the client in order to close down a game.

| Type | Name | Message |
| --- | --- | --- |
| `byte` (*Optional*) | Disconnect Reason | The ID of the [disconnect reason](../01_packet_structure/06_enums.md#disconnectreason) for why the game was removed<br><br>If this field is not present, it will default to `19` (`SERVER_REQUEST`) |

<details>
    <summary>Click here to view an example packet</summary>

```
01        # Reliable packet
00f6      # Nonce
000003    # Hazel message (tag of 0x03 = RemoveGame)
```
</details>

---

> Previous section: [`0x02` StartGame](02_startgame.md)<br>
> Next section: [`0x04` RemovePlayer](04_removeplayer.md)
