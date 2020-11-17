# `0x16` Close

This *empty* message is sent by the [`MeetingHud`](../05_innernetobject_types/01_meetinghud.md) object to close the meeting screen.

> **Note**: This message is sent from the host of a game to all players via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
00ae            # Nonce
090005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    020002      # Hazel message (tag of 0x02 = RPC)
        6e      # Sender (MeetingHud) Net ID: 110
        16      # RPC Call ID: 22 (Close)
```
</details>

---

> Previous section: [`0x15` SnapTo](21_snapto.md)<br>
> Next section: [`0x17` VotingComplete](23_votingcomplete.md)
