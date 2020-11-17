# `SecurityCameraSystem`

The `SecurityCameraSystem` is responsible for storing whether or not the security cameras are in use, and which players are viewing them.

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Players Length | The number of players viewing the security cameras |
| `byte[n]` | Players | The ID of each player viewing the security cameras, where length `n` is defined in the previous field |

---

> Previous section: [`MedScanSystem`](04_medscansystem.md)<br>
> Next section: [`HudOverrideSystem`](06_hudoverridesystem.md)
