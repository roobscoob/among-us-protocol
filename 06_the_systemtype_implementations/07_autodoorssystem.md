# `AutoDoorsSystem`

The `AutoDoorsSystem` is responsible for storing the open state of all doors around the map.

> **Note**: This only applies to *The Skeld*. For *Polus*, see [`DoorsSystem`](11_doorssystem.md).

> **Note**: *The Skeld* has 13 doors, and this value is looped over whenever data is serialized or deserialized.

##### Serialize

When sending data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Doors Mask | A bitfield mask used to tell the game which doors are receiving data |

When the `ShipStatus` is being spawned, as well as when it is sending data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `boolean[n]` | Doors | A list of each door's open state |

Refer to the pseudocode below for an example.

```java
// If the ShipStatus is being spawned
if (isSpawning) {
    // Loop through all 13 doors on The Skeld
    for (int i = 0; i < 13) {
        writer.writeBoolean(skeld.doors[i].isOpen);
    }
} else {
    // Write the dirty bits which tell the receiver which doors are included in the data update
    writer.writePackedUInt32(dirtyBits);

    // Loop through all 13 doors on The Skeld
    for (int i = 0; i < 13; i++) {
        // If the current door needs to be updated
        if ((dirtyBits & (1 << i)) != 0) {
            writer.writeBoolean(skeld.doors[i].isOpen);
        }
    }
}
```

##### Deserialize

When receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Doors Mask | A bitfield mask used to tell the game which doors are receiving data |

When the `ShipStatus` has been spawned, as well as when it is receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `boolean[n]` | Doors | A list of each door's open state |

Refer to the pseudocode below for an example.

```java
long mask;

// If the ShipStatus is receiving a data update
if (!isSpawning) {
    // Read the dirty bits which tell the receiver which doors are included in the data update
    mask = reader.readPackedUInt32();
}

// Loop through all 13 doors on The Skeld
for (int i = 0; i < 13; i++) {
    // If the ShipStatus has been spawned or this door needs to be updated
    if (isSpawning || (mask & (1 << i)) != 0) {
        skeld.doors[i].isOpen = reader.readBoolean();
    }
}
```

---

> Previous section: [`HudOverrideSystem`](06_hudoverridesystem.md)<br>
> Next section: [`SabotageSystem`](08_sabotagesystem.md)
