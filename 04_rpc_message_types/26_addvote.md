# `0x1a` AddVote

This message is sent by the [`VoteBanSystem`](../05_innernetobject_types/08_votebansystem.md) component when a player votes to kick another player.

> **Note**: This message is sent to and from all players in a game via [`0x05` GameData](../02_root_message_types/05_gamedata.md). It is **never** sent from the host of a game as the host will immediately kick the player without the need to vote.

| Type | Name | Description |
| --- | --- | --- |
| `uint32` | Voting Client ID | The client ID of the player who cast the vote |
| `uint32` | Target Client ID | The client ID of the player that was voted to be kicked |

<details>
    <summary>Click here to view an example packet</summary>

```
01                # Reliable packet
003e              # Nonce
120005            # Hazel message (tag of 0x05 = GameData)
    d3503f8a      # Game ID: -1975562029 (REDSUS)
    0b0002        # Hazel message (tag of 0x02 = RPC)
      ac01        # Sender (VoteBanSystem) Net ID: 172
      1a          # RPC Call ID: 26 (AddVote)
      7b750400    # Voting Client ID: 2071266304
      5c750400    # Target Client ID: 1551172608
```
</details>

---

> Previous section: [`0x19` ClearVote](25_clearvote.md)<br>
> Next section: [`0x1b` CloseDoorsOfType](27_closedoorsoftype.md)
