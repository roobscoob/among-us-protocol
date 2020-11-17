# `0x05` CheckName

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object when joining a game to check with the host if the name is available for use. If the name is already being used, the host updates the client's name by adding an incrementing number from 1 to 99 to the end of their name.

> **Note**: This message is sent from a player to the host of a game via [`0x06` GameDataTo](../02_root_message_types/06_gamedatato.md). It is **never** sent from the host of a game.

Example:

```
Client #1 joins with name "Hodor"
Client #1 sends CheckName
Host sends SetName for Client #1 with name "Hodor"
Client #2 joins with name "Hodor"
Client #2 sends CheckName
Host sends SetName for Client #2 with name "Hodor 1"
```

| Type | Name | Description |
| --- | --- | --- |
| `String` | Name | The player's name |

<details>
    <summary>Click here to view an example packet</summary>

```
01                              # Reliable packet
0004                            # Nonce
160006                          # Hazel message (tag of 0x06 = GameDataTo)
    d3503f8a                    # Game ID: -1975562029 (REDSUS)
    84a210                      # Target Client ID: 266500
    0c0002                      # Hazel message (tag of 0x02 = RPC)
        4b                      # Sender (PlayerControl) Net ID: 75
        05                      # RPC Call ID: 5 (CheckName)
        09636f647970686f6265    # Name: codyphobe
```
</details>

---

> Previous section: [`0x04` Exiled](04_exiled.md)<br>
> Next section: [`0x06` SetName](06_setname.md)
