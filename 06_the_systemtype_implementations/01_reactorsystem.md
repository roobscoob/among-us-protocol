# `ReactorSystem`

The `ReactorSystem` is responsible for storing whether or not the Reactor (on *The Skeld* and *MIRA HQ*) or Laboratory (on *Polus*) is sabotaged, and which players have their hand on which console.

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `float` | Timer | The time remaining before the Reactor has a meltdown or the Seismic Stabilizers fail and the impostors win |
| `packed uint32` | Players Length | The number of players who have their hand on a console in an attempt to repair the sabotage |
| `UserConsolePair[n]` | Players | A list of each player that has their hand on a console, and which console their hand is on, where length `n` is defined in the previous field |

##### The `UserConsolePair` Structure

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Player ID | The ID of the player |
| `byte` | Console ID | The ID of the console that the player's hand is on (see [`REACTOR` and `LABORATORY`](../04_rpc_message_types/28_repairsystem.md#reactor-and-laboratory) for a mapping of IDs to consoles) |

---

> Next section: [`SwitchSystem`](02_switchsystem.md)
