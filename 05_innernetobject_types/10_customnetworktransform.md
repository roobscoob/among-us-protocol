# `CustomNetworkTransform`

The `CustomNetworkTransform` object is spawned for each player that joins a game lobby and despawned at the end of the game. It is responsible for a player's movement. It has two sibling objects: the [`PlayerControl`](04_playercontrol.md) and [`PlayerPhysics`](09_playerphysics.md) objects.

### Serialize

When the `CustomNetworkTransform` object is being spawned, as well as when it is sending data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `uint16` | Last Sequence ID | The ID of this data packet |
| `Vector2` | Target Position | The current position of the player (see [The `Vector2` Type](../01_packet_structure/04_the_vector2_type.md)) |
| `Vector2` | Target Velocity | The current velocity of the player (see [The `Vector2` Type](../01_packet_structure/04_the_vector2_type.md)) |

Refer to the pseudocode below for an example.

```java
writer.writePackedUInt32(customNetworkTransformNetId);

if (isSpawning) {
    writer.startMessage(0);
}

writer.writeUInt16(lastSequenceId);
Vector2.writeVector2(writer, targetPosition);
Vector2.writeVector2(writer, targetVelocity);

if (isSpawning) {
    writer.endMessage();
}
```

### Deserialize

When the `CustomNetworkTransform` has been spawned, as well as when it is receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `uint16` | Last Sequence ID | The ID of this data packet |
| `Vector2` | Target Position | The new position of the player (see [The `Vector2` Type](../01_packet_structure/04_the_vector2_type.md)) |
| `Vector2` | Target Velocity | The new velocity of the player (see [The `Vector2` Type](../01_packet_structure/04_the_vector2_type.md)) |

Refer to the pseudocode below for an example.

```java
long customNetworkTransformNetId = reader.readPackedUInt32();

if (isSpawning) {
    reader = reader.readMessage();
}

int lastSequenceId = reader.readUInt16();
Vector2 targetPosition = Vector2.readVector2(reader);
Vector2 targetVelocity = Vector2.readVector2(reader);
```

---

> Previous section: [`PlayerPhysics`](09_playerphysics.md)<br>
