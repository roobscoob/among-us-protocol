# `0x0b` ReportDeadBody

This message is sent by a client's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a game when reporting a dead body or calling an emergency meeting.

> **Note**: This message is sent from a client to the host of a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md). It is **never** sent from the host of a game. When the host reports a dead body or calls an emergency meeting, the host sends a [`0x0e` StartMeeting](14_startmeeting.md) message to all clients. It is therefore more reliable to listen for a `StartMeeting` message in an event-based protocol implementation.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Victim Player ID | The ID of the player whose body was found<br><br>**Note**: This will be 255 (`0xff`) if pressing the emergency meeting button |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
003c            # Nonce
0b0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    040002      # Hazel message (tag of 0x02 = RPC)
        d101    # Sender (PlayerControl) Net ID: 209
        0b      # RPC Call ID: 11 (ReportDeadBody)
        08      # Victim Player ID: 8 (the body of player 8 was found)
```
</details>

---

> Previous section: [`0x0a` SetSkin](10_setskin.md)<br>
> Next section: [`0x0c` MurderPlayer](12_murderplayer.md)
