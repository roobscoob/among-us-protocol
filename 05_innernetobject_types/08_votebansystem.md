# `VoteBanSystem`

The `VoteBanSystem` object is spawned when joining a game lobby and despawned at the end of the game. It is responsible for managing votes to kick a player as well as the host banning a player. It has one sibling object: the [`GameData`](03_gamedata.md) object.

##### Serialize

When the `VoteBanSystem` object is being spawned, as well as when it is sending data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Players Length | The number of players in the game |

After writing the length, the game loops over all players. For each player in the loop, an array of 3 `packed uint32` client IDs is written, which tells the game the client IDs of the players that voted to kick the player. Refer to the pseudocode below for an example.

```java
writer.writePackedUInt32(voteBanSystemNetId);
writer.startMessage(0);
writer.writeByte(players.length);

// Loop through all players
for (int i = 0; i < players.length; i++) {
    // Write the client ID of the player
    writer.writeUInt32(player.clientId);

    for (int j = 0; j < 3; j++) {
        // Write the client ID of all 3 players that voted to kick the player
        // The votesToKick array would have default client IDs of 0
        writer.writePackedUInt32(players.votesToKick[j]);
    }
}

write.endMessage();
```

##### Deserialize

When the `VoteBanSystem` has been spawned, as well as when it is receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Players Length | The number of players in the game |

After reading the length, the game loops over all players based on the length defined above. For each player in the loop, an array of 3 `packed uint32` client IDs are read, which tells the game the client IDs of the players that voted to kick the player. Refer to the pseudocode below for an example.

```java
long voteBanSystemNetId = reader.readPackedUInt32();
MessageReader voteBanSystem = reader.readMessage();
byte playersLength = voteBanSystem.readByte();

// Loop through all players
for (int i = 0; i < playersLength; i++) {
    // Read the client ID of the player
    long clientId = voteBanSystem.readUInt32();

    for (int j = 0; l < 3; j++) {
        // Read the client ID of all 3 players that voted to kick the player, with a default value of 0
        voteBanSystem.readUInt32();
    }
}
```

---

> Previous section: [`AprilShipStatus`](07_aprilshipstatus.md)<br>
> Next section: [`PlayerPhysics`](09_playerphysics.md)
