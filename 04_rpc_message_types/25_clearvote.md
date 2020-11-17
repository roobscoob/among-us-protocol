# `0x19` ClearVote

This *empty* message is sent by the [`MeetingHud`](../05_innernetobject_types/01_meetinghud.md) object when a player that is still alive disconnects from the game during the voting phase. This allows players that already voted for the disconneting player to vote again.

> **Note**: This message is sent from the host of a game to all affected players via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0156            # Nonce
0f0006          # Hazel message (tag of 0x06 = GameDataTo)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    a5cd11      # Target Client ID: 288421
    050002      # Hazel message (tag of 0x02 = RPC)
        d901    # Sender (MeetingHud) Net ID: 217
        19      # RPC Call ID: 25 (ClearVote)
```
</details>

---

> Previous section: [`0x18` CastVote](24_castvote.md)<br>
> Next section: [`0x1a` AddVote](26_addvote.md)
