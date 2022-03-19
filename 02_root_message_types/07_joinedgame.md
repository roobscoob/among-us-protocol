# `0x07` JoinedGame

### Host-to-Client

This message is sent from the host of a game to a client after the client has successfully joined the game.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `int32` | Joined Client ID | The ID of the client that joined the game |
| `int32` | Host Client ID | The ID of the client that is the current host of the game |
| `packed int32` | Other Client IDs Length | The number of clients in the game excluding the client that just joined |
| `packed int32[n]` | Other Client IDs | A list of the IDs of every other client in the game, where length `n` is defined in the previous field |

<details>
    <summary>Click here to view an example packet</summary>

```
01                  # Reliable packet
0001                # Nonce
210007              # Hazel message (tag of 0x07 = JoinedGame)
    d3503f8a        # Game ID: -1975562029 (REDSUS)
    412d2400        # Joined Client ID: 2370881
    86252400        # Host Client ID: 2368902
    05              # Other Client IDs Length: 5
        86cb9001    # Other Client IDs[0]: 2368902
        fecc9001    # Other Client IDs[1]: 2369150
        f8d99001    # Other Client IDs[2]: 2370808
        86da9001    # Other Client IDs[3]: 2370822
        8fda9001    # Other Client IDs[4]: 2370831
```
</details>

---

> Previous section: [`0x06` GameDataTo](06_gamedatato.md)<br>
> Next section: [`0x08` EndGame](08_endgame.md)
