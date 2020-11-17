# `0x17` VotingComplete

This message is sent by the [`MeetingHud`](../05_innernetobject_types/01_meetinghud.md) object when voting has ended.

> **Note**: This message is sent from the host of a game to all players via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Vote States Length | The number of player voting states |
| `byte[n]` | Vote States | A list of bitfields for each player's voting state, where length `n` is defined in the previous field |
| `byte` | Exiled Player ID | The ID of the player who was voted off<br><br>**Note**: This will be 255 (`0xff`) if no player was voted off |
| `boolean` | Is Tie | Whether or not the meeting ended with a tie in votes |

##### The `Vote States` Bitfield

To read the information in each player's `Vote State`, use the following bitwise operations.

| Name | Description | Operation |
| --- | --- | --- |
| Did Report | Whether or not the player called the meeting or found the body | `(state & 0x20) != 0` |
| Did Vote | Whether or not the player casted a vote, either to exile a player or to skip | `(state & 0x40) != 0` |
| Is Dead | Whether or not the player is dead | `(state & 0x80) != 0` |
| Voted For | The ID of the player that was voted to be exiled, or -1 if voting to skip | `(state & 0xf) - 1` |

<details>
    <summary>Click here to view an example packet</summary>

```
01                # Reliable packet
00ab              # Nonce
170005            # Hazel message (tag of 0x05 = GameData)
    d3503f8a      # Game ID: -1975562029 (REDSUS)
    100002        # Hazel message (tag of 0x02 = RPC)
        d801      # Sender (MeetingHud) Net ID: 216
        17        # RPC Call ID: 23 (VotingComplete)
        0a        # Vote States Length: 10
            4a    # Vote States[0]: player 0 voted to exile player 9
            4a    # Vote States[1]: player 1 voted to exile player 9
            6a    # Vote States[2]: player 2 called the meeting/found the body, and voted to exile player 9
            4a    # Vote States[3]: player 3 voted to exile player 9
            4a    # Vote States[4]: player 4 voted to exile player 9
            4a    # Vote States[5]: player 5 voted to exile player 9
            4a    # Vote States[6]: player 6 voted to exile player 9
            81    # Vote States[7]: player 7 is dead
            4a    # Vote States[8]: player 8 voted to exile player 9
            43    # Vote States[9]: player 9 voted to exile player 2
        09        # Exiled Player ID: 9
        00        # Is Tie: False
```
</details>

---

> Previous section: [`0x16` Close](22_close.md)<br>
> Next section: [`0x18` CastVote](24_castvote.md)
