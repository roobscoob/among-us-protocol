# `HqHudSystem`

The `HqHudSystem` is responsible for storing whether or not Communications is sabotaged, which players have a communications panel open, and which panels are completed.

> **Note**: This only applies to *MIRA HQ*. For *The Skeld* and *Polus*, see [`HudOverrideSystem`](06_hudoverridesystem.md).

When spawned, as well as when sending or receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game (de)serializes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Active Consoles Length | The number of players who have a communications panel open in an attempt to repair the sabotage |
| `UserConsolePair[n]` | Active Consoles | A list of each player that has a communications panel open, and which console they have open, where length `n` is defined in the previous field |
| `packed uint32` | Completed Consoles Length | The number of consoles that had a correct code entered |
| `byte[n]` | Completed Consoles | A list of consoles that had a correct code entered (see [MIRA HQ Communications Consoles](../04_rpc_message_types/28_repairsystem.md#mira-hq-communications-consoles) for a mapping of IDs to consoles) |

##### The `UserConsolePair` Structure

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Player ID | The ID of the player |
| `byte` | Console ID | The ID of the console that the player has open (see [MIRA HQ Communications Consoles](../04_rpc_message_types/28_repairsystem.md#mira-hq-communications-consoles) for a mapping of IDs to consoles) |

---

> Previous section: [`SabotageSystem`](08_sabotagesystem.md)<br>
> Next section: [`DeconSystem`](10_deconsystem.md)
