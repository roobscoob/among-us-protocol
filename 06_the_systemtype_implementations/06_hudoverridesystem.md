# `HudOverrideSystem`

The `HudOverrideSystem` is responsible for storing whether or not Communications is sabotaged.

> **Note**: This does not apply to *Mira HQ*. For *Mira HQ*, see [`HqHudSystem`](09_hqhudsystem.md).

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `boolean` | Is Sabotaged | Whether or not Communications are currently sabotaged |

---

> Previous section: [`SecurityCameraSystem`](05_securitycamerasystem.md)<br>
> Next section: [`AutoDoorsSystem`](07_autodoorssystem.md)
