# The Structure of the `GameOptionsData` Object

| Type | Name | Since Version | Default Value | Description |
| --- | --- | --- | --- | --- |
| `packed uint32` | Length | &mdash; | &mdash; | The length, in bytes, of the `GameOptionsData` object |
| `byte` | Version | &mdash; | &mdash; | The version of the `GameOptionsData` object |
| `byte` | Max Number of Players | 1 | `10` | The maximum number of players |
| `uint32` | Keywords | 1 | `1` | A bitfield for the languages (see [`GameKeywords`](../01_packet_structure/06_enums.md#gamekeywords)) |
| `byte` | Map(s) | 1 | `1` | For the [client-to-server `0x10` GetGameListV2](../02_root_message_types/16_getgamelistv2.md#request-client-to-server) message, this is a bitfield<br><br>For all other uses, this is the ID of the map (see [`Map`](../01_packet_structure/06_enums.md#map)) |
| `float` | Player Speed Modifier | 1 | `1.0` | A multiplicative number for the speed at which players will move |
| `float` | Crewmate Light Modifier | 1 | `1.0` | A multiplicative number for the size of the fog-of-war ring encircling crewmates |
| `float` | Impostor Light Modifier | 1 | `1.5` | A multiplicative number for the size of the fog-of-war ring encircling impostors |
| `float` | Kill Cooldown | 1 | `45` | The number of seconds after the game starts, between kills, and after a meeting ends, that an impostor must wait before being able to kill |
| `byte` | Number of Common Tasks | 1 | `1` | The number of common tasks each crewmate will have |
| `byte` | Number of Long Tasks | 1 | `1` | The number of long tasks each crewmate will have |
| `byte` | Number of Short Tasks | 1 | `2` | The number of short tasks each crewmate will have |
| `uint32` | Number of Emergency Meetings | 1 | `1` | The number of emergency meetings each player will be able to call |
| `byte` | Number of Impostors | 1 | `1` | The maximum number of impostors |
| `byte` | Kill Distance | 1 | `1` | How far of a reach an impostor has when killing crewmates (see [`KillDistances`](../01_packet_structure/06_enums.md#killdistances)) |
| `uint32` | Discussion Time | 1 | `15` | How many seconds before voting starts during a meeting |
| `uint32` | Voting Time | 1 | `120` | How many seconds players will have to cast a vote during a meeting |
| `boolean` | Is Defaults | 1 | `true` | Whether or not the `GameOptionsData` object is using the default options |
| `byte` | Emergency Cooldown | 2 | `15` | How many seconds crewmates must wait between emergency meetings |
| `boolean` | Confirm Ejects | 3 | `true` | Whether or not the game will say if the ejected player was or wasn't an impostor |
| `boolean` | Visual Tasks | 3 | `true` | Whether or not tasks which play animations (e.g. Clear Asteroids) will play those animations to other players |
| `boolean` | Anonymous Votes | 4 | `false` | Whether or not the votes on the meeting HUD will show the color of the players who voted |
| `byte` | Task Bar Updates | 4 | `0` | When, if at all, the task bar will update to show how many tasks have been completed (see [`TaskBarUpdate`](../01_packet_structure/06_enums.md#taskbarupdate)) |

---

> Next section: [Converting Game IDs to and from Game Codes](02_converting_game_ids_to_and_from_game_codes.md)
