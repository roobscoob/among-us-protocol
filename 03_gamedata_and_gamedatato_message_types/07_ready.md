# `0x07` Ready

### Client-to-Host

This message is sent by the client to the host of a game as a response to the [`0x02` StartGame](../02_root_message_types/02_startgame.md) packet and is used to indicate that the client is synchronized and ready to play. If the client is not ready in time, they will be disconnected due to an error.

| Type | Name | Description |
| --- | --- | --- |
| `packed int32` | Ready Client ID | The ID of the client that is ready |

<details>
    <summary>Click here to view an example packet</summary>

```
01                # Reliable packet
0069              # Nonce
0a0005            # Hazel message (tag of 0x05 = GameData)
    d3503f8a      # Game ID: -1975562029 (REDSUS)
    030007        # Hazel message (tag of 0x07 = Ready)
        828c13    # Ready Client ID: 312834
```
</details>

---

> Previous section: [`0x06` SceneChange](06_scenechange.md)<br>
> Next section: [`0x08` ChangeSettings](08_changesettings.md)
