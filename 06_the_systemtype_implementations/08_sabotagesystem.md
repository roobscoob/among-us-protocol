# `SabotageSystem`

The `SabotageSystem` is responsible for storing the cooldown of an impostor's sabotage buttons.

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `float` | Cooldown | How long an impostor must wait before they can sabotage another system |

---

> Previous section: [`AutoDoorsSystem`](07_autodoorssystem.md)<br>
> Next section: [`HqHudSystem`](09_hqhudsystem.md)
