# `0x1e` UpdateGameData

This message is sent by the [`GameData`](../05_innernetobject_types/03_gamedata.md) object when the data for a player is updated.

> **Note**: This message is sent from the host of a game to all players via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `Message[n]` | Player Info | One or more [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) each containing the metadata for a player |

### The `Player Info` Message Structure

| Type | Name | Description |
| --- | --- | --- |
| `String` | Name | The player's name |
| `byte` | Color ID | The ID of the player's color |
| `packed uint32` | Hat ID | The ID of the player's hat |
| `packed uint32` | Pet ID | The ID of the player's pet |
| `packed uint32` | Skin ID | The ID of the player's skin |
| `byte` | Flags | A bitfield containing the player's character states |
| `byte` | Tasks Length | The number of tasks that the player has |
| `TaskInfo[n]` | Tasks | A list of the player's tasks and their completion state, where length `n` is defined in the previous field |

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

```
01                          # Reliable packet
0079                        # Nonce
9f0105                      # Hazel message (tag of 0x05 = GameData)
    d3503f8a                # Game ID: -1975562029 (REDSUS)
    e50002                  # Hazel message (tag of 0x02 = RPC)
        58                  # Sender (GameData) Net ID: 88
        1e                  # RPC Call ID: 30 (UpdateGameData)
        160000              # Hazel message (tag of 0x00 = player 0)
            05416c696365    # Name: Alice
            08              # Color ID: 8 (Purple)
            51              # Hat ID: 81 (Chef's Hat)
            00              # Pet ID: 0 (None)
            00              # Skin ID: 0 (None)
            00              # Flags: None
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
        160001              # Hazel message (tag of 0x01 = player 1)
            054a616d6573    # Name: James
            04              # Color ID: 4 (Orange)
            31              # Hat ID: 49 (Safari Hat)
            00              # Pet ID: 0 (None)
            00              # Skin ID: 0 (None)
            02              # Flags: Is Impostor
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
        160003              # Hazel message (tag of 0x03 = player 3)
            054461766964    # Name: David
            00              # Color ID: 0 (Red)
            33              # Hat ID: 51 (Beanie)
            00              # Pet ID: 0 (None)
            00              # Skin ID: 0 (None)
            00              # Flags: None
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
        160002              # Hazel message (tag of 0x02 = player 2)
            055361726168    # Name: Sarah
            05              # Color ID: 5 (Yellow)
            51              # Hat ID: 81 (Chef's Hat)
            00              # Pet ID: 0 (None)
            00              # Skin ID: 0 (None)
            00              # Flags: None
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
        160004              # Hazel message (tag of 0x04 = player 4)
            0543696e6479    # Name: Cindy
            03              # Color ID: 3 (Pink)
            1c              # Hat ID: 28 (New Year's Party Hat)
            00              # Pet ID: 0 (None)
            00              # Skin ID: 0 (None)
            02              # Flags: Is Impostor
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
        160005              # Hazel message (tag of 0x05 = player 5)
            054c61757261    # Name: Laura
            09              # Color ID: 9 (Brown)
            40              # Hat ID: 64 (Mohawk)
            02              # Pet ID: 2 (Mini Crewmate)
            0e              # Skin ID: 14 (Polus Winter Jacket)
            00              # Flags: None
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
        160008              # Hazel message (tag of 0x08 = player 8)
            05536861756e    # Name: Shaun
            07              # Color ID: 7 (White)
            5a              # Hat ID: 90 (Mini Crewmate)
            00              # Pet ID: 0 (None)
            00              # Skin ID: 0 (None)
            00              # Flags: None
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
        160009              # Hazel message (tag of 0x09 = player 9)
            0548656e7279    # Name: Logan
            0b              # Color ID: 11 (Light Green)
            27              # Hat ID: 39 (Ten Gallon Hat)
            00              # Pet ID: 0 (None)
            00              # Skin ID: 0 (None)
            00              # Flags: None
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
        160007              # Hazel message (tag of 0x07 = player 7)
            054d6567616e    # Name: Henry
            0a              # Color ID: 10 (Cyan)
            5d              # Hat ID: 93 (Mini Crewmate Snowman)
            00              # Pet ID: 0 (None)
            00              # Skin ID: 0 (None)
            00              # Flags: None
            05              # Tasks Length: 5
                00  00      # Tasks[0], not completed
                01  00      # Tasks[1], not completed
                02  00      # Tasks[2], not completed
                03  00      # Tasks[3], not completed
                04  00      # Tasks[4], not completed
```
</details>

---

> Previous section: [`0x1d` SetTasks](29_settasks.md)
