# `MedScanSystem`

The `MedScanSystem` is responsible for storing which clients are waiting in line to get scanned on the Medbay scanner.

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Players Length | The number of players in line waiting to get scanned |
| `byte[n]` | Players | The ID of each player in line waiting to get scanned, where length `n` is defined in the previous field |

---

> Previous section: [`LifeSuppSystem`](03_lifesuppsystem.md)<br>
> Next section: [`SecurityCameraSystem`](05_securitycamerasystem.md)
