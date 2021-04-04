# `MiraShipStatus`

The `MiraShipStatus` object (which is a variant of the [`SkeldShipStatus`](00_skeldshipstatus.md) object) is spawned at the start of a game on *MIRA HQ* and despawned at the end of the game. It holds the map for *MIRA HQ* and is responsible for controlling the interactive systems throughout the map.

> **Note**: See [`SkeldShipStatus`](00_skeldshipstatus.md) for *The Skeld*, or [`PolusShipStatus`](06_polusshipstatus.md) for *Polus*.

### All `SystemType`s for MIRA HQ

The table below lists every [`SystemType`](../01_packet_structure/06_enums.md#systemtype) used on *MIRA HQ* and each should be handled when being spawned, serialized, and deserialized.

| Type | Implementation | On Spawn | On Data |
| --- | --- | --- | --- |
| `REACTOR` | [`ReactorSystem`](../06_the_systemtype_implementations/01_reactorsystem.md) | &#x2714; | &#x2714; |
| `ELECTRICAL` | [`SwitchSystem`](../06_the_systemtype_implementations/02_switchsystem.md) | &#x2714; | &#x2714; |
| `O2` | [`LifeSuppSystem`](../06_the_systemtype_implementations/03_lifesuppsystem.md) | &#x2714; | &#x2714; |
| `MEDBAY` | [`MedScanSystem`](../06_the_systemtype_implementations/04_medscansystem.md) | &#x2714; | &#x2714; |
| `COMMUNICATIONS` | [`HqHudSystem`](../06_the_systemtype_implementations/09_hqhudsystem.md) | &#x2714; | &#x2714; |
| `SABOTAGE` | [`SabotageSystem`](../06_the_systemtype_implementations/08_sabotagesystem.md) | &#x2714; | &#x2714; |
| `DECONTAMINATION` | [`DeconSystem`](../06_the_systemtype_implementations/10_deconsystem.md) | &#x2716; | &#x2714; |

### Serialize

> **Note**: Because `MiraShipStatus` is an extension of [`SkeldShipStatus`](00_skeldshipstatus.md) specific to *MIRA HQ*, the `serialize` method is identical to that of `SkeldShipStatus` except for the system types.

When the `MiraShipStatus` is being spawned, the game loops over all [`SystemType`s](../01_packet_structure/06_enums.md#systemtype) in order and checks if the type is part of *MIRA HQ*. For each type that is a part of *MIRA HQ*, the Hazel message writer containing the [component data](../03_gamedata_and_gamedatato_message_types/04_spawn.md#the-component-structure) is passed in to the type's `serialize` method.

When sending data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Systems Mask | A bitfield used to tell the game which [`SystemType`s](../01_packet_structure/06_enums.md#systemtype) are receiving data |

After writing the mask, the game loops over all [`SystemType`s](../01_packet_structure/06_enums.md#systemtype) in order and checks if the type's ID is set on the mask. For each type that does have its ID set on the mask, the Hazel message writer containing the update data is passed in to the type's `serialize` method. Refer to the pseudocode below for an example.

```java
writer.writePackedUInt32(shipStatusNetId);

if (isSpawning) {
    writer.startMessage(0);
}

// Loop through all SystemTypes
for (SystemType system : SystemType.values()) {
    // If the ShipStatus is being spawned
    if (isSpawning) {
        // If MIRA HQ has this SystemType...
        if (miraSystems.containsKey(system)) {
            // ...then we should write (serialize) the data from the system
            miraSystems.get(system).serialize(writer);
        }
    // If the ShipStatus is receiving data updates
    } else {
        writer.writePackedUInt32(systemsMask);

        // If this system is set on the systemsMask...
        if ((systemsMask & (1 << system.id())) != 0) {
            // ...then we should write (serialize) the data from the system
            miraSystems.get(system).serialize(writer);
        }
    }
}

if (isSpawning) {
    writer.endMessage();
}
```

### Deserialize

> **Note**: Because `MiraShipStatus` is an extension of [`SkeldShipStatus`](00_skeldshipstatus.md) specific to *MIRA HQ*, the `deserialize` method is identical to that of `SkeldShipStatus` except for the system types.

When the `MiraShipStatus` has been spawned, the game loops over all [`SystemType`s](../01_packet_structure/06_enums.md#systemtype) in order and checks if the type is part of *MIRA HQ*. For each type that is a part of *MIRA HQ*, the Hazel message containing the [component data](../03_gamedata_and_gamedatato_message_types/04_spawn.md#the-component-structure) is passed in to the type's `deserialize` method.

When receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Systems Mask | A bitfield used to tell the game which [`SystemType`s](../01_packet_structure/06_enums.md#systemtype) are receiving data |

After reading the mask, the game loops over all [`SystemType`s](../01_packet_structure/06_enums.md#systemtype) in order and checks if the type's ID is set on the mask. For each type that does have its ID set on the mask, the Hazel message containing the update data is passed in to the type's `deserialize` method. Refer to the pseudocode below for an example.

```java
long shipStatusNetId = reader.readPackedUInt32();

if (isSpawning) {
    reader = reader.readMessage();
}

// Loop through all SystemTypes
for (SystemType system : SystemType.values()) {
    // If the ShipStatus is being spawned
    if (isSpawning) {
        // If MIRA HQ has this SystemType...
        if (miraSystems.containsKey(system)) {
            // ...then we should read (deserialize) the data from the component message
            miraSystems.get(system).deserialize(reader);
        }
    // If the ShipStatus is receiving data updates
    } else {
        long systemsMask = reader.readPackedUInt32();

        // If this system is set on the systemsMask...
        if ((systemsMask & (1 << system.id())) != 0) {
            // ...then we should read (deserialize) the data from the component message
            miraSystems.get(system).deserialize(reader);
        }
    }
}
```

---

> Previous section: [`PlayerControl`](04_playercontrol.md)<br>
> Next section: [`PolusShipStatus`](06_polusshipstatus.md)
