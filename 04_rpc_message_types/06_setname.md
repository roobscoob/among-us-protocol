# `0x06` SetName

This message is sent by the host's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a lobby to set a joining client's name after receiving a [`0x05` CheckName](05_checkname.md) message from the client.

> **Note**: This message is sent from the host of a game to all players via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `String` | Name | The player's new name |

<details>
    <summary>Click here to view an example packet</summary>

```
01                              # Reliable packet
000e                            # Nonce
130005                          # Hazel message (tag of 0x05 = GameData)
    d3503f8a                    # Game ID: -1975562029 (REDSUS)
    0c0002                      # Hazel message (tag of 0x02 = RPC)
        4b                      # Sender (PlayerControl) Net ID: 75
        06                      # RPC Call ID: 6 (SetName)
        09636f647970686f6265    # Name: codyphobe
```
</details>

---

> Previous section: [`0x05` CheckName](05_checkname.md)<br>
> Next section: [`0x07` CheckColor](07_checkcolor.md)
