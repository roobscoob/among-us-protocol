# `DoorsSystem`

The `DoorsSystem` is responsible for storing the open state of all doors around the map, as well as a timer to prevent impostors from closing a door immediately after another player opens it.

> **Note**: This only applies to *Polus*. For *The Skeld*, see [`AutoDoorsSystem`](07_autodoorssystem.md).

> **Note**: *Polus* has `16` doors (`12` manual doors and `4` decontamination doors), and this value is looped over whenever data is serialized or deserialized.

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Door Cooldowns Length | The number of doors that have an impostor cooldown |
| `DoorCooldown[n]` | Door Cooldowns | A list of doors that have an impostor cooldown, where length `n` is defined in the previous field |
| `boolean[n]` | Doors | A list of each door's open state |

##### The `DoorCooldown` Structure

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Door ID | The ID of the door (see [Polus Doors](../04_rpc_message_types/28_repairsystem.md#polus-doors) for a mapping of IDs to doors) |
| `float` | Door Cooldown | The amount of time that impostors must wait before being able to close the door again |

---

> Previous section: [`DeconSystem`](10_deconsystem.md)
