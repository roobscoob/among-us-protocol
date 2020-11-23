# `0x02` RPC

This message is sent by an [`InnerNetObject`](../05_innernetobject_types/README.md) to update the state of the client and perform various actions.

Every `RPC` message starts out with the same data, outlined in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Sender Net ID | The net ID of the `InnerNetObject` that sent the RPC message |
| `byte` | RPC Call ID | The ID of the [`RPC` Message Type](../04_rpc_message_types/README.md) |

See [`RPC` Message Types](../04_rpc_message_types/README.md) for details on each possible RPC message that may be contained in this message type, taking note that the data described in the table above is omitted from the breakdown of those messages.

---

> Previous section: [`0x01` Data](01_data.md)<br>
> Next section: [`0x04` Spawn](04_spawn.md)
