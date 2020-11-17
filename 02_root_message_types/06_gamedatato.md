# `0x06` GameDataTo

Every `GameDataTo` message starts out with the same data, outlined in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `packed uint32` | Target Client ID | The client ID of the player that the message is being sent to |

See [`GameData` and `GameDataTo` Message Types](../03_gamedata_and_gamedatato_message_types/README.md) for details on each possible message that may be contained in this message type, taking note that the data described in the table above is omitted from the breakdown of those messages.

---

> Previous section: [`0x05` GameData](05_gamedata.md)<br>
> Next section: [`0x07` JoinedGame](07_joinedgame.md)
