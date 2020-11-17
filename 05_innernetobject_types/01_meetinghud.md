# `MeetingHud`

The `MeetingHud` object is spawned at the start of a meeting and despawned at the end of the meeting. It is responsible for storing player states in a meeting such as which players are dead, which voted, and who they voted for.

##### Serialize

When the `MeetingHud` is being spawned, the game loops over all players in order (starting from ID `0`) and passes the Hazel message writer containing the [component data](../03_gamedata_and_gamedatato_message_types/04_spawn.md#the-component-structure) in to the state's `serialize` method.

When sending data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first writes the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | States Mask | A bitfield mask used to tell the game which player states were updated |

After writing the mask, the game loops over all players in order (starting from ID `0`) and checks if the player's ID is set on the mask. For each player that does have its ID set on the mask, the Hazel message writer containing the update data is passed in to the states's `serialize` method. Refer to the pseudocode below for an example.

```java
writer.writePackedUInt32(meetingHudNetId);
writer.startMessage(0);

// Loop through all player states
for (int i = 0; i < playerStates.length; i++) {
    // If the MeetingHud is being spawned
    if (isSpawning) {
        // Write (serialize) the data from the player state
        playerStates[i].serialize(writer);
    // If the MeetingHud is receiving data updates
    } else {
        writer.writePackedUInt32(statesMask);

        // If this player state is set on the systemsMask...
        if ((statesMask & (1 << i)) != 0) {
            // ...then we should write (serialize) the data from the player state
            playerStates[i].serialize(writer);
        }
    }
}

write.endMessage();
```

##### Deserialize

When the `MeetingHud` has been spawned, the game loops over all players in order (starting from ID `0`) and passes the Hazel message containing the [component data](../03_gamedata_and_gamedatato_message_types/04_spawn.md#the-component-structure) in to the state's `deserialize` method.

When receiving data (via [`0x01` Data](../03_gamedata_and_gamedatato_message_types/01_data.md)), the game first reads the information in the table below.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | States Mask | A bitfield mask used to tell the game which player states were updated |

After reading the mask, the game loops over all players in order (starting from ID `0`) and checks if the player's ID is set on the mask. For each player that does have its ID set on the mask, the Hazel message containing the update data is passed in to the state's `deserialize` method. Refer to the pseudocode below for an example.

```java
long meetingHudNetId = reader.readPackedUInt32();
MessageReader meetingHud = reader.readMessage();

// Loop through all player states
for (int i = 0; i < playerStates.length; i++) {
    // If the MeetingHud is being spawned
    if (isSpawning) {
        // Read (deserialize) the data from the component message
        playerStates[i].deserialize(meetingHud);
    // If the MeetingHud is receiving data updates
    } else {
        long statesMask = meetingHud.readPackedUInt32();

        // If this player state is set on the statesMask...
        if ((statesMask & (1 << system.id())) != 0) {
            // ...then we should read (deserialize) the data from the component message
            playerStates[i].deserialize(meetingHud);
        }
    }
}
```

### Reading the `States Mask`

Each player state is itself a bitfield indicating how the game should display a player and their votes on the meeting HUD. To read the information in each player's state, see [The `Vote States` Bitfield](../04_rpc_message_types/23_votingcomplete.md#the-vote-states-bitfield).

---

> Previous section: [`ShipStatus`](00_shipstatus.md)<br>
> Next section: [`LobbyBehaviour`](02_lobbybehaviour.md)
