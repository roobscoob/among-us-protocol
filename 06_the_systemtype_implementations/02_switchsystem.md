# `SwitchSystem`

The `SwitchSystem` is responsible for storing whether or not lights are sabotaged, and keeping flipped switches in sync across all clients.

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Expected Switches | A bitfield (with five bits&mdash;one per switch) used to tell the game which switches need to be flipped up or down in order to fix the lights |
| `byte` | Actual Switches | A bitfield (with five bits&mdash;one per switch) used to tell the game the current up/down state of each switch |
| `byte` | Value | The percentage displayed next to the task on a client's task list when the lights are sabotaged |

---

> Previous section: [`ReactorSystem`](01_reactorsystem.md)<br>
> Next section: [`LifeSuppSystem`](03_lifesuppsystem.md)
