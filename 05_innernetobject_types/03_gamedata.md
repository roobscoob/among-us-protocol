# `GameData`

The `GameData` object is spawned when joining a game lobby and despawned at the end of the game. It is responsible for storing the metadata for players such as their name, cosmetics, tasks, and more. It has one sibling object: the [`VoteBanSystem`](08_votebansystem.md) object.

### Serialize

When the `GameData` object is being spawned, as well as when it is sending data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first writes the information in the table below.

| Type | Name | Description | On Spawn | On Data |
| --- | --- | --- | --- | --- |
| `packed uint32` | Players Length | The number of players in the game | &#x2714; | &#x2716; |
| `byte` | Players Length | The number of players being updated | &#x2716; | &#x2714; |

After writing the length, the game loops over all players. For each player in the loop, the game writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Player ID | The ID of the player |
| `String` | Name | The player's name |
| `packed uint32` | Color ID | The ID of the player's color (see [`Color`](../01_packet_structure/06_enums.md#color)) |
| `packed uint32` | Hat ID | The ID of the player's hat (see [`Hat`](../01_packet_structure/06_enums.md#hat)) |
| `packed uint32` | Pet ID | The ID of the player's pet (see [`Pet`](../01_packet_structure/06_enums.md#pet)) |
| `packed uint32` | Skin ID | The ID of the player's skin (see [`Skin`](../01_packet_structure/06_enums.md#skin)) |
| `byte` | Flags | A bitfield containing the player's character states |
| `byte` | Tasks Length | The number of tasks that the player has |
| `TaskInfo[n]` | Tasks | A list of the player's tasks and their completion state, where length `n` is defined in the previous field |

Refer to the pseudocode below for an example.

```java
writer.writePackedUInt32(gameDataNetId);

if (isSpawning) {
    writer.startMessage(0);
    writer.writePackedUInt32(players.length);
}

// Loop through all players
for (int i = 0; i < players.length; i++) {
    Player player = players[i];
    TaskInfo[] tasks = player.tasks;

    // Only iterate over the player if the GameData is being spawned or,
    // in the case of a data update, if the player needs to be updated
    if (!isSpawning && (dirtyBits & (1 << i)) != 0) {
        continue;
    }

    if (!isSpawning) {
        writer.startMessage(player.id);
    } else {
        writer.writeByte(player.id);
    }

    writer.writeString(player.name);
    writer.writePackedUInt32(player.color);
    writer.writePackedUInt32(player.hat);
    writer.writePackedUInt32(player.pet);
    writer.writePackedUInt32(player.skin);

    if (isSpawning) {
        writer.endMessage();
    }

    byte flags = 0;

    if (player.isDisconnected) {
        flags |= 1
    }

    if (player.isImpostor) {
        flags |= 2
    }

    if (player.isDead) {
        flags |= 4
    }

    writer.writeByte(flags);
    writer.writeByte(tasks.length);

    for (int j = 0; j < tasks.length; j++) {
        writer.writePackedUInt32(tasks[j].id);
        writer.writeBoolean(tasks[j].isCompleted);
    }

    updatedPlayers++;
}

if (isSpawning) {
    writer.endMessage();
}
```

### Deserialize

When the `GameData` has been spawned, as well as when it is receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first reads the information in the table below.

| Type | Name | Description | On Spawn | On Data |
| --- | --- | --- | --- | --- |
| `packed uint32` | Players Length | The number of players in the game | &#x2714; | &#x2716; |
| `byte` | Players Length | The number of players being updated | &#x2716; | &#x2714; |

After reading the length, the game loops over the provided number of players. For each player in the loop, the game reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Player ID | The ID of the player |
| `String` | Name | The player's name |
| `packed uint32` | Color ID | The ID of the player's color (see [`Color`](../01_packet_structure/06_enums.md#color)) |
| `packed uint32` | Hat ID | The ID of the player's hat (see [`Hat`](../01_packet_structure/06_enums.md#hat)) |
| `packed uint32` | Pet ID | The ID of the player's pet (see [`Pet`](../01_packet_structure/06_enums.md#pet)) |
| `packed uint32` | Skin ID | The ID of the player's skin (see [`Skin`](../01_packet_structure/06_enums.md#skin)) |
| `byte` | Flags | A bitfield containing the player's character states |
| `byte` | Tasks Length | The number of tasks that the player has |
| `TaskInfo[n]` | Tasks | A list of the player's tasks and their completion state, where length `n` is defined in the previous field |

Refer to the pseudocode below for an example.

```java
long gameDataNetId = reader.readPackedUInt32();

if (isSpawning) {
    reader = reader.readMessage();

    long playerCount = reader.readPackedUInt32();

    // Loop through all player states
    for (int i = 0; i < playerCount; i++) {
        readPlayer(child, child.readByte());
    }
} else {
    while ((child = reader.readMessage()) != null) {
        readPlayer(child, child.getTag());
    }
}

Player readPlayer(MessageReader reader, byte id) {
    Player player = Game.getOrCreatePlayerById(id);

    player.name = child.readString();
    player.color = child.readPackedUInt32();
    player.hat = child.readPackedUInt32();
    player.pet = child.readPackedUInt32();
    player.skin = child.readPackedUInt32();

    byte flags = child.readByte();

    player.isDisconnected = (flags & 1) != 0
    player.isImpostor = (flags & 2) != 0
    player.isDead = (flags & 4) != 0

    byte tasksLength = child.readByte();

    player.tasks = new TaskInfo[tasksLength];

    for (int j = 0; j < tasksLength; j++) {
        TaskInfo task = new TaskInfo();

        task.id = child.readPackedUInt32();
        task.isCompleted = child.readBoolean();

        player.tasks[j] = task;
    }

    return player;
}
```

##### The `Flags` Bitfield

To read the information in each player's `Flags`, use the following bitwise operations.

| Name | Description | Operation |
| --- | --- | --- |
| Is Disconnected | Whether or not the player has disconnected from the game | `(flags & 1) != 0` |
| Is Impostor | Whether or not the player is an impostor | `(flags & 2) != 0` |
| Is Dead | Whether or not the player is dead | `(flags & 4) != 0` |

##### The `TaskInfo` Structure

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Task ID | The ID (index) of the task |
| `boolean` | Is Completed | Whether or not the player has completed the task |

<details>
    <summary>Click here to view an example packet</summary>

---

> Previous section: [`LobbyBehaviour`](02_lobbybehaviour.md)<br>
> Next section: [`PlayerControl`](04_playercontrol.md)
