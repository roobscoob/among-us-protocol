# `DeconSystem`

The `DeconSystem` is responsible for storing the timer of a decontamination room's doors as well as the state that the doors are in.

When sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

> **Note**: The `DeconSystem` is **never** included in a spawn packet.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Timer | How long before the decontamination doors open |
| `byte` | State | A bitfield describing which state the doors in, or which direction a player is heading through decontamination |

##### The `State` Bitfield

To read the `State` of the decontamination room's doors, use the following bitwise operations.

| Name | Description | Operation |
| --- | --- | --- |
| `Idle` | Whether or not the doors are idle and waiting to be opened by a player | `state == 0` |
| `Enter` | Whether or not a player is heading through decontamination | `(flags & 1) != 0` |
| `Closed` | Whether or not the doors are closed | `(flags & 2) != 0` |
| `Exit` | Whether or not a player is leaving decontamination | `(flags & 4) != 0` |
| `HeadingUp` | Whether or not a player is heading through decontamination into a cleanroom (i.e. Reactor or Specimens) | `(flags & 8) != 0` |

When looking at [`DECONTAMINATION` and `DECONTAMINATION_2`](../04_rpc_message_types/28_repairsystem.md#decontamination-and-decontamination_2), the `amount` can be translated to the following states.

| Amount | `State` Bitwise Equivalent |
| --- | --- |
| `1` | `States.Enter | States.HeadingUp` |
| `2` | `States.Enter` |
| `3` | `States.Exit | States.HeadingUp` |
| `4` | `States.Exit` |

---

> Previous section: [`HqHudSystem`](09_hqhudsystem.md)<br>
> Next section: [`DoorsSystem`](11_doorssystem.md)
