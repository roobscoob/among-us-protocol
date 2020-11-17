# `0x0e` ReselectServer

### Server-to-Client

This message is sent from the server to a client when loading the game list, creating a game, and joining a game, and tells the client which servers the games are hosted on.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | *Unknown* | An unknown value that has so far been observed to always be `0x01` |
| `byte` | Master Servers Length | The number of master servers in this message |
| `Message[n]` | Master Servers | A list of [Hazel messages](../01_packet_structure/03_the_structure_of_a_hazel_message.md), each containing one master server for the selected region, where length `n` is defined in the previous field |

### The `Master Servers` Message Structure

This is the structure of each [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) in the `Master Servers` field.

| Type | Name | Description |
| --- | --- | --- |
| `String` | Name | The name of the master server |
| `IP Address` | IP Address | The IP address of the server |
| `uint16` | Port | The port that the server is listening on |
| `packed uint32` | Number of Players | The number of players currently connected to the server |

<details>
    <summary>Click here to view an example packet</summary>

```
00                                # Normal packet
79000e                            # Hazel message (tag of 0x0e = ReselectServer)
    01                            # Unknown
    06                            # Master Servers Length: 6
        110000                    # Hazel message (master server)
            084d61737465722d35    # Name: Master-5
            c63a6347              # IP Address: 198.58.99.71
            0756                  # Port: 22023
            a536                  # Number of Players: 6949
        110000                    # Hazel message (master server)
            084d61737465722d36    # Name: Master-6
            2d4f0506              # IP Address: 45.79.5.6
            0756                  # Port: 22023
            9b35                  # Number of Players: 6811
        100000                    # Hazel message (master server)
            084d61737465722d34    # Name: Master-4
            2d4f284b              # IP Address: 45.79.40.75
            0756                  # Port: 22023
            2b                    # Number of Players: 43
        110000                    # Hazel message (master server)
            084d61737465722d33    # Name: Master-3
            2d4f284b              # IP Address: 45.79.40.75
            0756                  # Port: 22023
            ed5c                  # Number of Players: 11885
        110000                    # Hazel message (master server)
            084d61737465722d32    # Name: Master-2
            68ed87ba              # IP Address: 104.237.135.186
            0756                  # Port: 22023
            b332                  # Number of Players: 6451
        110000                    # Hazel message (master server)
            084d61737465722d31    # Name: Master-1
            68ed87ba              # IP Address: 104.237.135.186
            0756                  # Port: 22023
            9a02                  # Number of Players: 282
```
</details>

---

> Previous section: [`0x0d` Redirect](13_redirect.md)<br>
> Next section: [`0x10` GetGameListV2](16_getgamelistv2.md)
