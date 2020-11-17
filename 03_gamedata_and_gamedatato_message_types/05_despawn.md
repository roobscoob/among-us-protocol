# `0x05` Despawn

### Host-to-Game

This message is sent by the host of a game to all clients in a game to despawn an [`InnerNetObject`](../05_innernetobject_types/README.md).

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Net ID | The net ID of the object that is being despawned |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0009            # Nonce
170005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    010005      # Hazel message (tag of 0x05 = Despawn)
        45      # Net ID: 69
    010005      # Hazel message (tag of 0x05 = Despawn)
        46      # Net ID: 70
    010005      # Hazel message (tag of 0x05 = Despawn)
        47      # Net ID: 71
```
</details>

---

> Previous section: [`0x04` Spawn](04_spawn.md)<br>
> Next section: [`0x06` SceneChange](06_scenechange.md)
