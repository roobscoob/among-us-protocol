# `0x01` CompleteTask

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a game when they complete a task.

> **Note**: Each map has its own set of tasks and associated IDs, found [here](../07_miscellaneous/04_map_specific_ids_for_vents_and_tasks.md), that are used when setting a player's tasks.

> **Note**: This message is sent to and from all clients in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Task Index | The index of the player's task list (zero-indexed) for the task that was completed<br><br>The player's task list is provided via the [`0x1d` SetTasks](29_settasks.md) RPC message |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0184            # Nonce
0b0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    040002      # Hazel message (tag of 0x02 = RPC)
        d401    # Sender (PlayerControl) Net ID: 212
        01      # RPC Call ID: 1 (CompleteTask)
        02      # Task Index: 2 (the player's 3rd task)
```
</details>

---

> Previous section: [`0x00` PlayAnimation](00_playanimation.md)<br>
> Next section: [`0x02` SyncSettings](02_syncsettings.md)
