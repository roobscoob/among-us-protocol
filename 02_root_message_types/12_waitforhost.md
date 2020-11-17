# `0x0c` WaitForHost

### Client-to-Host

This message is sent from the client to the host of a game when the client clicks the "Play Again" button to rejoin the game that has just finished.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `uint32` | Player Client ID | The client ID of the player that is rejoining the game |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
01bc            # Nonce
08000c          # Hazel message (tag of 0x0c = WaitForHost)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    7b750400    # Player Client ID: 292219
```
</details>

---

> Previous section: [`0x0b` KickPlayer](11_kickplayer.md)<br>
> Next section: [`0x0d` Redirect](13_redirect.md)
