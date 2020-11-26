# `0x04` Spawn

### Host-to-Game

This message is sent by the host of a game to all clients in a game to spawn an [`InnerNetObject`](../05_innernetobject_types/README.md).

Every `Spawn` message starts out with the same data, outlined in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Spawn Type | The [`SpawnType`](../01_packet_structure/06_enums.md#spawntype) of the spawned object |
| `packed int32` | Owner ID | The ID of the owner that spawned the object |
| `byte` | Spawn Flags | The [`SpawnFlag`s](../01_packet_structure/06_enums.md#spawnflag) for the spawned object |
| `packed uint32` | Components Length | The number of components associated with the spawned object |
| `Component[n]` | Components | The components associated with the spawned object, where length `n` is defined in the previous field |

### The `Component` Structure

Every component of an `InnerNetObject` that is spawned starts out with the same data, outlined in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Net ID | The net ID of the component |
| `Message` | Component Data | A [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) that contains the spawn data for the component<br><br>**Note**: A component will **always** have a Hazel message for its spawn data, but the message won't always contain data |

When a component of an `InnerNetObject` is receiving a data update (via [`0x01` Data](01_data.md)), the structure is slightly different and is outlined in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Net ID | The net ID of the component |
| `byte[n]` | Component Data | The raw bytes of the data for the component<br><br>**Note**: The length is not specified as the data is deserialized on the component |

See [`InnerNetObject` Types](../05_innernetobject_types/README.md) for details on each possible `Component` that may be spawned from this message type, taking note that the data described in the tables above is omitted from the breakdown of those objects.

> **Note**: When an object is spawned, the first component will always be the type being spawned. For example, the first component on a spawned `ShipStatus` *is* a `ShipStatus`. This might seem counterintuitive but think of the first component as the actual data for the object.

---

> Previous section: [`0x02` RPC](02_rpc.md)<br>
> Next section: [`0x05` Despawn](05_despawn.md)
