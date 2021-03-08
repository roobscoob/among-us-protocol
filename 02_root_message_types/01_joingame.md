# `0x01` JoinGame

### Client-to-Server

This message is sent from the client to the server when attempting to join a game.

This message has two main flows that depend on the state of the game:

- **Join Game Flow**: if the client is joining a game that has not started...
    - ...and the client joins successfully, the server will do the following:
        1. Add the client to the list of clients in the game
        1. Send the client a [`0x07` JoinedGame](07_joinedgame.md) packet
        1. Broadcast a [Server-to-Game](#server-to-game) packet for the client that just joined to *every other* client
    - ...and the client fails to join, the server will send the client an [Error](#error-server-to-client) response packet
        - A client may fail to join for multiple reasons, including but not limited to:
            - The game already started
            - The game was closed
            - The game was full
            - The code was incorrect
            - The client was banned
        - If multiple clients try to join a game with fewer spots open than required to let them all join, the *host* of the game will disconnect the last clients to join with a [`0x04` RemovePlayer](04_removeplayer.md#server-to-game) packet
- **Rejoin Game Flow**: if a client tries to rejoin a game by clicking the "*Play Again*" button...
    - ...and the client *is not the host*, the server will do the following:
        - If the [game state](../01_packet_structure/06_enums.md#gamestates) is `Ended` (the host has not yet rejoined)...
            1. Add the client to the list of clients in the game (the list is cleared when the game ends)
            1. Put the client in the `WaitingForHost` [limbo state](../01_packet_structure/06_enums.md#limbostates)
            1. Send the client a [`0x0c` WaitForHost](12_waitforhost.md) packet
            1. Broadcast a [Server-to-Game](#server-to-game) packet for the client that just rejoined to *every other* client
        - If the [game state](../01_packet_structure/06_enums.md#gamestates) is `NotStarted` (the host has already rejoined)...
            1. The client will go through the **Join Game Flow** above
    - ...and the client *is the host*, the server will do the following:
        1. Set the [game state](../01_packet_structure/06_enums.md#gamestates) to `NotStarted`
        1. Add the client to the list of clients in the game (the list is cleared when the game ends)
        1. Put the client in the `NotLimbo` [limbo state](../01_packet_structure/06_enums.md#limbostates)
        1. Send the client a [`0x07` JoinedGame](07_joinedgame.md) packet
        1. Broadcast a [Server-to-Game](#server-to-game) packet for the client that just rejoined to *every other* client
        1. Send each client in the `WaitingForHost` [limbo state](../01_packet_structure/06_enums.md#limbostates) a [`0x07` JoinedGame](07_joinedgame.md) packet

> **Note**: If the host of a game leaves at the end of the game, regardless of whether or not there are any clients in the `WaitingForHost` [limbo state](../01_packet_structure/06_enums.md#limbostates), the first client to click "*Play Again*" becomes the new host of the game.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0003            # Nonce
040001          # Hazel message (tag of 0x01 = JoinGame)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
```
</details>

### Server-to-Game

This message is sent from the server to all clients in a game when another client joins the game.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `uint32` | Joining Client ID | The ID of the joining client |
| `uint32` | Host Client ID | The ID of the client that is the current host of the game |

<details>
    <summary>Click here to view an example success packet</summary>

```
01              # Reliable packet
001b            # Nonce
0c0001          # Hazel message (tag of 0x01 = JoinGame)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    58c90400    # Joining Client ID: 313688
    4ec20400    # Host Client ID: 311886
```
</details>

### Error: Server-to-Client

This message is sent from the server to a client that failed to join a game.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Disconnect Reason | The ID of the [disconnect reason](../01_packet_structure/06_enums.md#disconnectreason) for why the game could not be joined |

<details>
    <summary>Click here to view an example error packet</summary>

```
01              # Reliable packet
0001            # Nonce
040001          # Hazel message (tag of 0x01 = JoinGame)
    01000000    # Disconnect Reason: 1 (GAME_FULL)
```
</details>

---

> Previous section: [`0x00` HostGame](00_hostgame.md)<br>
> Next section: [`0x02` StartGame](02_startgame.md)
