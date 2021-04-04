# `PlayerControl`

The `PlayerControl` object is spawned for each player that joins a game lobby and despawned at the end of the game. It is responsible for a player's character interacting with the game and its other players. It has two sibling objects: the [`PlayerPhysics`](09_playerphysics.md) and [`CustomNetworkTransform`](10_customnetworktransform.md) objects.

### Serialize

When the `PlayerControl` is being spawned, the game first writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `boolean` | Is New | Whether or not the `PlayerControl` object already existed before sending a spawn message for it<br><br>**Note**: This will be `true` on the `PlayerControl` object of a joining player as seen from the clients that are already in a game lobby, and `false` on the `PlayerControl` objects of the clients already in the game lobby as seen from the joining player |

When the `PlayerControl` object is being spawned, as well as when it is sending data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game also writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Player ID | The ID of the player that is being spawned |

Refer to the pseudocode below for an example.

```java
writer.writePackedUInt32(playerControlNetId);

if (isSpawning) {
    writer.startMessage(0);
    writer.writeBoolean(isNew);
}

writer.writeByte(playerId);

if (isSpawning) {
    writer.endMessage();
}
```

### Deserialize

When the `PlayerControl` has been spawned, the game first reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `boolean` | Is New | Whether or not the `PlayerControl` object already existed before receiving a spawn message for it<br><br>**Note**: This will be `true` on the `PlayerControl` object of a joining player as seen from the clients that are already in a game lobby, and `false` on the `PlayerControl` objects of the clients already in the game lobby as seen from the joining player |

When the `PlayerControl` object has been spawned, as well as when it is receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game also reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Player ID | The ID of the player that is being spawned |

Refer to the pseudocode below for an example.

```java
long playerControlNetId = reader.readPackedUInt32();

if (isSpawning) {
    reader = reader.readMessage();
    boolean isNew = reader.readBoolean();
}

byte playerId = reader.readByte();
```

---

> Previous section: [`GameData`](03_gamedata.md)<br>
> Next section: [`MiraShipStatus`](05_mirashipstatus.md)
