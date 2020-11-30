# `0x18` CastVote

This message is sent by the [`MeetingHud`](../05_innernetobject_types/01_meetinghud.md) object when a player either votes to skip or votes to exile another player.

> **Note**: This message is sent from a client to the host of a game via [`0x06` GameDataTo](../02_root_message_types/06_gamedatato.md). It is **never** sent from the host of a game.

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Voting Player ID | The ID of the player who cast the vote |
| `byte` | Suspect Player ID | The ID of the player that was voted to be exiled<br><br>**Note**: This will be 255 (`0xff`) if the player voted to skip |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0156            # Nonce
0f0006          # Hazel message (tag of 0x06 = GameDataTo)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    a5cd11      # Target Client ID: 288421
    050002      # Hazel message (tag of 0x02 = RPC)
        d901    # MeetingHud Net ID: 217
        18      # RPC Call ID: 24 (CastVote)
        06      # Voting Player ID: 6
        05      # Suspect Player ID: 5
```
</details>

---

> Previous section: [`0x17` VotingComplete](23_votingcomplete.md)<br>
> Next section: [`0x19` ClearVote](25_clearvote.md)
