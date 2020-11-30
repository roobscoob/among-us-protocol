# `0x04` Exiled

This *empty* message, though it is never sent in-game, will kill the player that it was sent to as if they were voted off during a meeting meaning it *will not* spawn a dead body for the player.

> **Note**: This message is sent from the host of a game to a client via [`0x06` GameDataTo](../02_root_message_types/06_gamedatato.md).

<details>
    <summary>Click here to view an example packet</summary>

```
01                              # Reliable packet
0004                            # Nonce
0c0006                          # Hazel message (tag of 0x06 = GameDataTo)
    d3503f8a                    # Game ID: -1975562029 (REDSUS)
    84a210                      # Target Client ID: 266500
    0c0002                      # Hazel message (tag of 0x02 = RPC)
        4b                      # Sender (PlayerControl) Net ID: 75
        04                      # RPC Call ID: 4 (Exiled)
```
</details>

---

> Previous section: [`0x03` SetInfected](03_setinfected.md)<br>
> Next section: [`0x05` CheckName](05_checkname.md)
