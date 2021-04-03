# `0x11` ReportPlayer

### Request: Client-to-Server

This message is sent from the client to the server when reporting a player.

| Type | Name | Description |
| --- | --- | --- |
| `int32` | Game ID | The ID ([code](../07_miscellaneous/02_converting_game_ids_to_and_from_game_codes.md)) of the game |
| `packed uint32` | Reported Client ID | The ID of the reported client |
| `byte` | Report Reason | The reason for why the client was reported (see [`ReportReason`](../01_packet_structure/06_enums.md#reportreason)) |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
01a4            # Nonce
080010          # Hazel message (tag of 0x11 = ReportPlayer)
    d3503f8a    # Game ID: -1975562029 (REDSUS)
    828c13      # Reported Client ID: 312834
    00          # Report Reason: 0 (INAPPROPRIATE_NAME)
```
</details>

### Response: Server-to-Client

This message is sent from the server to the client after reporting a player.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Reported Client ID | The ID of the reported client |
| `uint32` | Report Reason | The reason for why the client was reported (see [`ReportReason`](../01_packet_structure/06_enums.md#reportreason)) |
| `byte` | Report Outcome | The result of the report (see [`ReportOutcome`](../01_packet_structure/06_enums.md#reportoutcome)) |
| `string` | Reported Player Name | The name of the player that was reported |

<details>
    <summary>Click here to view an example packet</summary>

```
01                    # Reliable packet
01a4                  # Nonce
0f0010                # Hazel message (tag of 0x11 = ReportPlayer)
    828c13            # Reported Client ID: 312834
    00000000          # Report Reason: 0 (INAPPROPRIATE_NAME)
    04                # Report Outcome: 4 (REPORTED)
    06776565776f6f    # Reported Player Name: "weewoo is better"
```
</details>

---

> Previous section: [`0x10` GetGameListV2](16_getgamelistv2.md)
