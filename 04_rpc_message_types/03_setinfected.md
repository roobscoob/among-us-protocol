# `0x03` SetInfected

This message is sent by the host's [`PlayerControl`](../05_innernetobject_types/04_playercontrol.md) object at the start of a game to choose the impostors.

> **Note**: This message will set each player in the list as an impostor. It **will not** set an impostor back to crewmate if they are not included in the list.

> **Note**: This message is sent from the host of a game to all players via [`0x05` GameData](../02_root_message_types/05_gamedata.md).

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Impostors Length | The number of players that were selected to be an impostor |
| `byte[n]` | Impostors | A list of each impostor's player ID, where length `n` is defined in the previous field |

<details>
    <summary>Click here to view an example packet</summary>

```
01                # Reliable packet
0079              # Nonce
0c0005            # Hazel message (tag of 0x05 = GameData)
    d3503f8a      # Game ID: -1975562029 (REDSUS)
    050002        # Hazel message (tag of 0x02 = RPC)
        5a        # Sender (PlayerControl) Net ID: 90
        03        # RPC Call ID: 3 (SetInfected)
        02        # Impostors Length: 2
            04    # Impostors[0] = player 4
            01    # Impostors[1] = player 1
```
</details>

---

> Previous section: [`0x02` SyncSettings](02_syncsettings.md)<br>
> Next section: [`0x04` Exiled](04_exiled.md)
