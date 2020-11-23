# `LifeSuppSystem`

The `LifeSuppSystem` is responsible for storing whether or not the Oxygen is sabotaged, and which consoles have been completed.

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `float` | Countdown | The time remaining before the O2 has been depleted and the impostors win |
| `packed uint32` | Consoles Length | The number of O2 consoles that have been completed |
| `packed uint32[n]` | Consoles | A list of O2 consoles that have been completed, where length `n` is defined in the previous field (see [`O2`](../04_rpc_message_types/28_repairsystem.md#o2) for a mapping of IDs to consoles) |

---

> Previous section: [`SwitchSystem`](02_switchsystem.md)<br>
> Next section: [`MedScanSystem`](04_medscansystem.md)
