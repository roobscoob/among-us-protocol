# `0x01` Data

### Host-to-Game

This message is sent by the host of a game to all clients in a game. It is sent from inside the host client's `FixedUpdate` method in order to keep all clients in sync by updating every [`InnerNetObject`](../05_innernetobject_types/README.md) that has changed since the last call to `FixedUpdate`.

Every `Data` message starts out with the same data, outlined in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Net ID | The net ID of the `InnerNetObject` that the data in this message belongs to |

See [`InnerNetObject` Types](../05_innernetobject_types/README.md) for details on each possible `InnerNetObject`, and its components, that may receive updates from this message type, taking note that the data described in the table above is omitted from the breakdown of those objects.

---

Next section: [`0x02` RPC](02_rpc.md)
