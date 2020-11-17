# `0x06` SceneChange

### Client-to-Host

This message is sent by the client to the host of a game when changing the game scene that is being displayed to the client.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Player Client ID | The client ID of the player that is changing scenes |
| `String` | Scene Name | The name of the scene that the client is changing to |

<details>
    <summary>Click here to view an example packet</summary>

```
01                                # Reliable packet
0003                              # Nonce
150005                            # Hazel message (tag of 0x05 = GameData)
    d3503f8a                      # Game ID: -1975562029 (REDSUS)
    0e0006                        # Hazel message (tag of 0x06 = SceneChange)
        fda810                    # Player Client ID: 267389
        0a4f6e6c696e6547616d65    # Scene Name: OnlineGame
```
</details>

---

> Previous section: [`0x05` Despawn](05_despawn.md)<br>
> Next section: [`0x07` Ready](07_ready.md)
