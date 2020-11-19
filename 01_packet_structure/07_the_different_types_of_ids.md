# The Different Types of IDs

Every [`InnerNetObject`](../05_innernetobject_types/README.md) that can be spawned has two IDs associated with it: an `owner ID` and a `net ID`.

### Owner ID / Client ID

Once a player connects to the server their UDP connection is given a unique and incrementing ID referred to as the `client ID`.

For every type of [`InnerNetObject`](../05_innernetobject_types/README.md) that can be spawned, this ID is instead referred to as the `owner ID`. This `owner ID` is primarily used to assign a `PlayerControl` to a given player's UDP connection (i.e. `PlayerControl#OwnerID === Connection#ClientID`). For all other `InnerNetObject` types, their `owner ID` is set to `-2` as it is globally "owned" by the game that it was spawned in.

### Net ID

When spawned, an [`InnerNetObject`](../05_innernetobject_types/README.md) is assigned a unique and incrementing `net ID`. Since the host of a game is the one responsible for spawning in these objects, it too is responsible for managing the `net ID`. As a result of the host client managing these objects, this ID is unique to every game

### Player ID

Every player in a game has a third ID known as their `player ID`. This `player ID`, like the `net ID`, is managed by the host of a game. When a player leaves a game, their `player ID` becomes avaiable for the next player who joins. These IDs do not get shuffled around and the game will always assign a new player the first available ID starting from `0`. Since the `player ID` is stored as a 4-bit integer in [`0x17` VotingComplete](../04_rpc_message_types/23_votingcomplete.md#the-vote-states-bitfield), the technical limit for this ID and how many players a game can have (without modifying the client and protocol) is `15`.

---

> Previous section: [Enums](06_enums.md)
