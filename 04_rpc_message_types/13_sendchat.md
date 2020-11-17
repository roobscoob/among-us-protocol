# `0x0d` SendChat

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a game or lobby when sending a chat message.

> **Note**: This message is sent to and from all players in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md). The InnerSloth servers currently relay chat messages to every player in a game, even if the sender is dead and the receiver is still alive. This means that players who *are* still alive can read chat messages sent by a dead player by means of packet sniffing, patching the game, or reading the game's memory.

| Type | Name | Description |
| --- | --- | --- |
| `String` | Message | The message that was sent in chat |

<details>
    <summary>Click here to view an example packet</summary>

```
01                                    # Reliable packet
0193                                  # Nonce
160005                                # Hazel message (tag of 0x05 = GameData)
    d3503f8a                          # Game ID: -1975562029 (REDSUS)
    0f0002                            # Hazel message (tag of 0x02 = RPC)
        4b                            # Sender (PlayerControl) Net ID: 75
        0d                            # RPC Call ID: 13 (SendChat)
        0c48656c6c6f2c20776f726c64    # Message: "Hello, world"
```
</details>

---

> Previous section: [`0x0c` MurderPlayer](12_murderplayer.md)<br>
> Next section: [`0x0e` StartMeeting](14_startmeeting.md)
