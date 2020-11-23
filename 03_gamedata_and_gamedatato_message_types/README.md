# `GameData` and `GameDataTo` Message Types

> **Note**: A `GameData` or `GameDataTo` message may have more than one of these sub-messages in its body. You should encapsulate your logic for reading these sub-messages in a loop that checks if there are more bytes to be read. An example implementation might look similar to the following pseudocode:

```java
// After checking that the parent is a GameData message, we defer the parser to this method
void parseGameData(MessageReader gameData) {
    MessageReader child;

    // This while loop attempts to read another message and, if successful (not null), continues the loop
    while ((child = gameData.readMessage()) != null) {
        // We can now read each sub-message individually according to its type
    }
}
```

#### Table of Contents

1. [`0x01` Data](01_data.md)
1. [`0x02` RPC](02_rpc.md)
1. [`0x04` Spawn](04_spawn.md)
1. [`0x05` Despawn](05_despawn.md)
1. [`0x06` SceneChange](06_scenechange.md)
1. [`0x07` Ready](07_ready.md)
1. [`0x08` ChangeSettings](08_changesettings.md)

---

> Previous section: [Root Message Types](../02_root_message_types/README.md)<br>
> Next section: [`RPC` Message Types](../04_rpc_message_types/README.md)
