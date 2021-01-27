# `0x10` GetGameListV2

### Request: Client-to-Server

This message is sent from the client to the server when searching for public games.

| Type | Name | Description |
| --- | --- | --- |
| `packed int32` | *Unknown* | An unknown value that is hardcoded to be `0x00`<br><br>In the previous version of this message, [`0x09` GetGameList](09_getgamelist.md), this field was a `boolean` that when set to `true` would tell the server to include private games in the search results |
| [`GameOptionsData`](../07_miscellaneous/01_the_structure_of_the_gameoptionsdata_object.md) | Game Options Data | The settings used when searching for public games<br><br>**Note**: The map ID in this Game Options Data is a bitfield containing the IDs of each [`Map`](../01_packet_structure/06_enums.md#map) that the client is searching for |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0002            # Nonce
2c0010          # Hazel message (tag of 0x10 = GetGameListV2)
    00          # Hardcoded 0
    2a          # Game Options Data Length: 42
    02          # Game Optiona Data Version: 2
    0a          # Max Number of Players: 10
    00010000    # Keywords: 256 (English)
    05          # Maps: The Skeld or Polus
    0000803f    # Player Speed Modifier: 1.0x
    0000803f    # Crewmate Light Modifier: 1.0x
    0000c03f    # Impostor Light Modifier: 1.5x
    00007041    # Kill Cooldown: 15s
    01          # Number of Common Tasks: 1
    01          # Number of Long Tasks: 1
    02          # Number of Short Tasks: 2
    01000000    # Number of Emergency Meetings: 1
    02          # Number of Impostors: 2
    01          # Kill Distance: 1 (Medium)
    0f000000    # Discussion Time: 15s
    78000000    # Voting Time: 120s
    01          # Is Defaults: False
    0f          # Emergency Cooldown: 15s
```
</details>

### Response: Server-to-Client

This message is sent from the server to the client after searching for public games that match the client's search criteria.

| Type | Name | Description |
| --- | --- | --- |
| `Message` (*Optional*) | Game Counts | An optional [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) with a tag of `0x01` that contains the number of games for each map<br><br><table><thead><tr><th>Type</th><th>Name</th><th>Description</th></tr></thead><tbody><tr><td>`uint32`</td><td>The Skeld</td><td>The number of games being played on *The Skeld*</td></tr><tr><td>`uint32`</td><td>MIRA HQ</td><td>The number of games being played on *MIRA HQ*</td></tr><tr><td>`uint32`</td><td>Polus</td><td>The number of games being played on *Polus*</td></tr></tbody></table> |
| `Message` (*Optional*) | Game List | An optional [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) with a tag of `0x00` that contains multiple nested Hazel messages (one for each public game) |

### The `Game List` Message Structure

The `Game List` field is a [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) that contains a variable number of child Hazel messages (one for each game that matches the search criteria).

This is the structure of each child [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) in the `Game List` field.

> **Note**: The tag for each child [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) is meaningless and so any value will work.

| Type | Name | Description |
| --- | --- | --- |
| `IP Address` | IP Address | The IP address of the server that the game is hosted on |
| `uint16` | Port | The port that the server is listening on |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `String` | Host Name | The name of the current host of the game |
| `byte` | Number of Players | The number of players currently in the game |
| `packed uint32` | Age | The age, in seconds, of the game since it was first created |
| `byte` | Map ID | The ID of the [`Map`](../01_packet_structure/06_enums.md#map) that the game is being played on |
| `byte` | Number of Impostors | The number of impostors in the game |
| `byte` | Max Number of Players | The maximum number of players allowed in the game |

<details>
    <summary>Click here to view an example packet</summary>

```
01                          # Reliable packet
0001                        # Nonce
fa0010                      # Hazel message (tag of 0x10 = GetGameListV2)
    f70000                  # Hazel message (Game List)
        150000              # Hazel message (game listing)
            c09b519e        # IP Address: 192.155.81.158
            0756            # Port: 22023
            12613080        # Game ID: -2144313070 (UDXJTQ)
            05416c696365    # Host Name: Alice
            01              # Number of Players: 1
            13              # Age: 19 seconds
            00              # Map ID: 0 (The Skeld)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        160000              # Hazel message (game listing)
            c09b57b6        # IP Address: 192.155.87.182
            0756            # Port: 22023
            d5993680        # Game ID: -2143905323 (WODTYQ)
            054a616d6573    # Host Name: James
            03              # Number of Players: 3
            b401            # Age: 3 minutes
            00              # Map ID: 0 (The Skeld)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        160000              # Hazel message (game listing)
            2d21732a        # IP Address: 45.33.115.42
            0756            # Port: 22023
            17094080        # Game ID: -2143287017 (CDKWLQ)
            054461766964    # Host Name: David
            03              # Number of Players: 3
            c421            # Age: 1 hour 11 minutes 32 seconds
            00              # Map ID: 0 (The Skeld)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        160000              # Hazel message (game listing)
            2d4f6fb1        # IP Address: 45.79.111.177
            0756            # Port: 22023
            784e3580        # Game ID: -2143990152 (EMYWYQ)
            055361726168    # Host Name: Sarah
            04              # Number of Players: 4
            bb0c            # Age: 26 minutes 35 seconds
            00              # Map ID: 0 (The Skeld)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        160000              # Hazel message (game listing)
            adffdc9d        # IP Address: 173.255.220.157
            0756            # Port: 22023
            1dfe0c80        # Game ID: -2146632163 (BVAYWQ)
            0543696e6479    # Host Name: Cindy
            06              # Number of Players: 6
            ac4a            # Age: 2 hours 38 minutes 36 seconds
            00              # Map ID: 0 (The Skeld)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        160000              # Hazel message (game listing)
            42e43486        # IP Address: 66.228.52.134
            0756            # Port: 22023
            b9f00580        # Game ID: -2147094343 (RPKUQQ)
            054c61757261    # Host Name: Laura
            06              # Number of Players: 6
            bc08            # Age: 18 minutes 4 seconds
            02              # Map ID: 2 (Polus)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        160000              # Hazel message (game listing)
            adffc207        # IP Address: 173.255.194.7
            0756            # Port: 22023
            496a0380        # Game ID: -2147259831 (HIDEQQ)
            05536861756e    # Host Name: Shaun
            05              # Number of Players: 5
            d622            # Age: 1 hour 13 minutes 58 seconds
            00              # Map ID: 0 (The Skeld)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        150000              # Hazel message (game listing)
            2d4f5977        # IP Address: 45.79.89.119
            0756            # Port: 22023
            ea0d4680        # Game ID: -2142892566 (IOFKLQ)
            054c6f67616e    # Host Name: Logan
            02              # Number of Players: 2
            72              # Age: 1 minute 54 seconds
            00              # Map ID: 0 (The Skeld)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        150000              # Hazel message (game listing)
            2d213379        # IP Address: 45.33.51.121
            0756            # Port: 22023
            b3144680        # Game ID: -2142890829 (NLHKLQ)
            0548656e7279    # Host Name: Henry
            02              # Number of Players: 2
            59              # Age: 1 minute 29 seconds
            02              # Map ID: 2 (Polus)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
        160000              # Hazel message (game listing)
            17ef16fb        # IP Address: 23.239.22.251
            0756            # Port: 22023
            c1011880        # Game ID: -2145910335 (PZXPXQ)
            054d6567616e    # Host Name: Megan
            03              # Number of Players: 3
            8328            # Age: 1 hour 25 minutes 23 seconds
            00              # Map ID: 0 (The Skeld)
            02              # Number of Impostors: 2
            0a              # Max Number of Players: 10
```
</details>

---

> Previous section: [`0x0e` ReselectServer](14_reselectserver.md)
