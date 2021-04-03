# `0x0c` WaitForHost

### Client-to-Host

This message is sent from the server to a client after the client clicks the "*Play Again*" button to rejoin a game that has just finished.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `uint32` | Rejoining Client ID | The ID of the client that is rejoining the game |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
01bc            # Nonce
08000c          # Hazel message (tag of 0x0c = WaitForHost)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    7b750400    # Rejoining Client ID: 292219
```
</details>

---

> Previous section: [`0x0b` KickPlayer](11_kickplayer.md)<br>
> Next section: [`0x0d` Redirect](13_redirect.md)
