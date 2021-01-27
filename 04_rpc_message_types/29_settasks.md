# `0x1d` SetTasks

This message is sent by the [`GameData`](../05_innernetobject_types/03_gamedata.md) object when a game starts to set the tasks for each player.

> **Note**: Each map has its own set of tasks and associated IDs, found [here](../07_miscellaneous/04_map_specific_ids_for_vents_and_tasks.md), that are used when setting a player's tasks.

> **Note**: This message is sent from the host of a game to all clients via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Player ID | The ID of the player whose tasks are being set |
| `packed uint32` | Tasks Length | The number of tasks |
| `byte[n]` | Tasks | A list of the map-specific task IDs, where length `n` is defined in the previous field |

<details>
    <summary>Click here to view an example packet from a game on <i>Polus</i></summary>

```
01                # Reliable packet
0079              # Nonce
1c0005            # Hazel message (tag of 0x05 = GameData)
    d3503f8a      # Game ID: -1975562029 (REDSUS)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        00        # Player ID: 0
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            07    # Tasks[1]: 7 (Specimen Room: Download Data)
            13    # Tasks[2]: 19 (O2: Monitor Tree)
            19    # Tasks[3]: 25 (Medbay: Submit Scan)
            20    # Tasks[4]: 32 (Outside: Record Temperature)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        01        # Player ID: 1
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            0b    # Tasks[1]: 11 (Boiler Room: Open Waterways)
            15    # Tasks[2]: 21 (Specimen Room: Store Artifacts)
            1e    # Tasks[3]: 30 (Laboratory: Repair Drill)
            1b    # Tasks[4]: 27 (Outside: Fix Weather Node Node_CA)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        03        # Player ID: 3
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            04    # Tasks[1]: 4 (Weapons: Download Data)
            18    # Tasks[2]: 24 (Dropship: Chart Course)
            1c    # Tasks[3]: 28 (Outside: Fix Weather Node Node_MLG)
            1a    # Tasks[4]: 26 (Weapons: Clear Asteroids)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        02        # Player ID: 2
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            06    # Tasks[1]: 6 (Electrical: Download Data)
            16    # Tasks[2]: 22 (O2: Fill Canisters)
            1d    # Tasks[3]: 29 (Laboratory: Align Telescope)
            17    # Tasks[4]: 23 (O2: Empty Garbage)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        04        # Player ID: 4
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            05    # Tasks[1]: 5 (Office: Download Data)
            1f    # Tasks[2]: 31 (Laboratory: Record Temperature)
            14    # Tasks[3]: 20 (Specimen Room: Unlock Manifolds)
            19    # Tasks[4]: 25 (Medbay: Submit Scan)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        05        # Player ID: 5
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            09    # Tasks[1]: 9 (Specimen Room: Start Reactor)
            1d    # Tasks[2]: 29 (Laboratory: Align Telescope)
            1c    # Tasks[3]: 28 (Outside: Fix Weather Node Node_MLG)
            16    # Tasks[4]: 22 (O2: Fill Canisters)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        08        # Player ID: 8
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            0e    # Tasks[1]: 14 (Outside: Fix Weather Node Node_GI)
            20    # Tasks[2]: 32 (Outside: Record Temperature)
            13    # Tasks[3]: 19 (O2: Monitor Tree)
            15    # Tasks[4]: 21 (Specimen Room: Store Artifacts)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        09        # Player ID: 9
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            08    # Tasks[1]: 8 (O2: Download Data)
            18    # Tasks[2]: 24 (Dropship: Chart Course)
            1e    # Tasks[3]: 30 (Laboratory: Repair Drill)
            17    # Tasks[4]: 23 (O2: Empty Garbage)
    090002        # Hazel message (tag of 0x02 = RPC)
        58        # Sender (GameData) Net ID: 88
        1d        # RPC Call ID: 29 (SetTasks)
        07        # Player ID: 7
        05        # Tasks Length: 5
            01    # Tasks[0]: 1 (Dropship: Insert Keys)
            10    # Tasks[1]: 16 (Outside: Fix Weather Node Node_PD)
            14    # Tasks[2]: 20 (Specimen Room: Unlock Manifolds)
            19    # Tasks[3]: 25 (Medbay: Submit Scan)
            16    # Tasks[4]: 22 (O2: Fill Canisters)
```
</details>

---

> Previous section: [`0x1c` RepairSystem](28_repairsystem.md)<br>
> Next section: [`0x1e` UpdateGameData](30_updategamedata.md)
