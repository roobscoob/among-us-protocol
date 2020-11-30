# `0x12` SetStartCounter

This message is sent by the host's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object in a lobby when another client joins (to stop and reset the timer) or while counting down to start the game.

> **Note**: This message is sent from the host of a game to all clients via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Sequence ID | A nonce used to prevent older messages from causing desynchronization |
| `sbyte` | Time Remaining | The time remaining in seconds before the game starts, or `0xff` to reset the timer |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
005f            # Nonce
0b0005          # Hazel message (tag of 0x05 = GameData)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    040002      # Hazel message (tag of 0x02 = RPC)
      5a        # Sender (PlayerControl) Net ID: 90
      12        # RPC Call ID: 16 (SetStartCounter)
      11        # Sequence ID: 17
      05        # Time Remaining: 5 seconds
```
</details>

---

> Previous section: [`0x11` SetPet](17_setpet.md)<br>
> Next section: [`0x13` EnterVent](19_entervent.md)
