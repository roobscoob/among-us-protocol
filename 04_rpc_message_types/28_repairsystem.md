# `0x1c` RepairSystem

This message is sent by the [`ShipStatus`](../05_innernetobject_types/00_shipstatus.md) object when a [`SystemType`](../01_packet_structure/06_enums.md#systemtype) is interacted with by a player or sabotaged by an impostor.

> **Note**: This message is sent from a client to the host of a game via [`0x06` GameDataTo](../02_root_message_types/06_gamedatato.md). It is **never** sent from the host of a game.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | System ID | The ID of the [`SystemType`](../01_packet_structure/06_enums.md#systemtype) that is being repaired |
| `packed uint32` | PlayerControl Net ID | The net ID of the [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object for the player who repaired/sabotaged the system |
| `byte` | Amount | A value which holds various information about the state of the system |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
00f2            # Nonce
120006          # Hazel message (tag of 0x06 = GameDataTo)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    b3bf8e01    # Target Client ID: 2334643
    070002      # Hazel message (tag of 0x02 = RPC)
        c601    # Sender (ShipStatus) Net ID: 198
        1c      # RPC Call ID: 28 (RepairSystem)
        08      # System ID: 8 (O2)
        c001    # PlayerControl Net ID: 192
        41      # Amount: 41 (player completed O2 console 1)
```
</details>

## The `Amount` Field

How the `Amount` is read depends on the `System ID`. Below is a list of every [`SystemType`](../01_packet_structure/06_enums.md#systemtype) that can be interacted with using this RPC message as well as pseudocode, when necessary, on how to parse the `Amount` for that system.

#### `ELECTRICAL`

The `System ID` will be that of `SystemType.ELECTRICAL` when a player flips a switch during a light sabotage, and the `amount` is the zero-indexed position, from left to right, of the switch that was flipped.

#### `MEDBAY`

The `System ID` will be that of `SystemType.MEDBAY` when a player starts, stops, or finishes a medbay scan, or when they try to scan while another player is already scanning.

```java
// The ID of the player
int playerId = amount & 0x1f;

if ((amount & 0x80) != 0) {
    // Player queued up for medbay scan
} else if ((amount & 0x40) != 0) {
    // Player left queue for medbay scan
}
```

#### `O2`

The `System ID` will be that of `SystemType.O2` when a player finishes an O2 console.

```java
// The ID of the O2 console that was completed
int consoleId = amount & 3;

if ((amount & 0x40) != 0) {
    // O2 console {consoleId} was completed by the player
} else if ((amount & 0x10) != 0) {
    // O2 was fully repaired by the player
}
```

###### The Skeld O2 Consoles

| ID | Location |
| --- | --- |
| `0` | Admin |
| `1` | O2 |

###### Mira HQ O2 Consoles

| ID | Location |
| --- | --- |
| `0` | Greenhouse |
| `1` | Hallway |

#### `REACTOR` and `LABORATORY`

The `SystemType` will be that of `SystemType.REACTOR` (for *Reactor* on *The Skeld* and *Mira HQ*) or `SystemType.LABORATORY` (for *Seismic* on *Polus*) when a player interacts with a console.

```java
// The ID of the reactor/seismic console
int consoleId = amount & 3;

if ((amount & 0x40) != 0) {
    // The player placed their hand on console {consoleId}
} else if ((amount & 0x20) != 0) {
    // The player removed their hand from console {consoleId}
} else if ((amount & 0x10) != 0) {
    // Reactor/seismic was fully repaired by the player
}
```

###### The Skeld Reactor Consoles

| ID | Location |
| --- | --- |
| `0` | Top Reactor |
| `1` | Bottom Reactor |

###### Mira HQ Reactor Consoles

| ID | Location |
| --- | --- |
| `0` | Left Reactor |
| `1` | Right Reactor |

###### Polus Seismic Consoles

| ID | Location |
| --- | --- |
| `0` | Left Seismic Stabilizer |
| `1` | Right Seismic Stabilizer |


#### `SECURITY`

The `System ID` will be that of `SystemType.SECURITY` when a player starts or stops watching security cameras.

```java
if (amount == 1) {
    // The player is viewing security cameras
} else {
    // The player is no longer viewing security cameras
}
```

#### `DOORS`

The `System ID` will be that of `SystemType.DOORS` when a player opens a door on *Polus*, and only on *Polus*.

```java
// The ID of the door that was opened
int doorId = amount & 0x1f;
```

###### Polus Doors

| ID | Description |
| --- | --- |
| `0` | Outside to Electrical |
| `1` | Inside Electrical |
| `2` | O2-to-Electrical Hallway (Top) |
| `3` | O2-to-Electrical Hallway (Bottom) |
| `4` | Outside to O2 |
| `5` | Weapons |
| `6` | Communications |
| `7` | Office (Right) |
| `8` | Office (Left) |
| `9` | Drill |
| `10` | Outside to Medbay |
| `11` | Storage |

#### `COMMUNICATIONS`

The `System ID` will be that of `SystemType.COMMUNICATIONS` when a player repairs communications on any of the maps, as well as when the player opens or closes a communications console on *Mira HQ*.

```java
switch (currentMap) {
    case THE_SKELD:
    case POLUS:
        if (amount == 0) {
            // Communications was repaired by the player
        }

        break; // Don't forget this, it might cost you $750
    case MIRA_HQ:
        // The ID of the communications console
        int consoleId = amount & 0xf;

        if ((amount & 0x40) != 0) {
            // The player opened the communications console
        } else if ((amount & 0x20) != 0) {
            // The player closed the communications console
        } else if ((amount & 0x10) != 0) {
            // The player entered the correct code in the communications console
        }

        break;
}
```

###### Mira HQ Communications Consoles

| ID | Location |
| --- | --- |
| `0` | Communications |
| `1` | Office |

#### `DECONTAMINATION` and `DECONTAMINATION_2`

The `System ID` will be that of `SystemType.DECONTAMINATION` when a player opens one of the doors to decontamination. Since *Polus* has two decontamination rooms, a second type (`SystemType.DECONTAMINATION_2`) is used for the other room. More specifically, `SystemType.DECONTAMINATION` on *Polus* connects *Office* to *Specimens* while `SystemType.DECONTAMINATION_2` connects *Laboratory* to *Specimens*. Using the tables below, you can tell which direction a player is heading through decontamination by comparing the value of `amount` along with the map and `SystemType`.

**Note**: The conditions which describe a decontamination door being opened from inside decontamination are only ever sent if a player manually opens a decontamination door from the inside. It will not be sent if a player opens a decontamination door from the outside, enters decontamination, and exits through the other door after it opens on its own, because the player only ever opened one door.

###### Mira HQ: `SystemType.DECONTAMINATION`

| Value of `amount` | Condition |
| --- | --- |
| `1` | Opened decontamination from outside (from Locker Room) |
| `2` | Opened decontamination from outside (from Reactor) |
| `3` | Opened decontamination from inside (to Reactor) |
| `4` | Opened decontamination from inside (to Locker Room) |

###### Polus: `SystemType.DECONTAMINATION` (Office-to-Specimens)

| Value of `amount` | Condition |
| --- | --- |
| `1` | Opened decontamination from outside (from Office) |
| `2` | Opened decontamination from outside (from Specimens) |
| `3` | Opened decontamination from inside (to Specimens) |
| `4` | Opened decontamination from inside (to Office) |

###### Polus: `SystemType.DECONTAMINATION_2` (Laboratory-to-Specimens)

| Value of `amount` | Condition |
| --- | --- |
| `1` | Opened decontamination from outside (from Specimens) |
| `2` | Opened decontamination from outside (from Laboratory) |
| `3` | Opened decontamination from inside (to Laboratory) |
| `4` | Opened decontamination from inside (to Specimens) |

#### `SABOTAGE`

The `System ID` will be that of `SystemType.SABOTAGE` when a system is sabotaged by an impostor, and the `amount` is the ID of the [`SystemType`](../01_packet_structure/06_enums.md#systemtype) that was sabotaged.

---

> Previous section: [`0x1b` CloseDoorsOfType](27_closedoorsoftype.md)<br>
> Next section: [`0x1d` SetTasks](29_settasks.md)
