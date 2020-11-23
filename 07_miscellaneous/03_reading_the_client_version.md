# Reading the Client Version

The [`0x08` Hello](../01_packet_structure/05_packet_types.md#0x08-hello) packet in Among Us contains the client's version number in an encoded format between offsets `4` and `7`.

```
08 00 01 00 46 d2 02 03 08 75 73 65 72 6e 61 6d 65
            |---------/
            |
            Version number (50516550 in this case)
```

This version number is encoded using the following formula:

```java
int version = year * 25000 + month * 1800 + day * 50 + revision

// Example

int version = 2020 * 25000 + 9 * 1800 + 7 * 50 + 0 // = 50516550
```

The values `year`, `month`, `day`, and `revision` are all hardcoded values within the game and are all reflected in the top-left corner of the screen.

To decode the version and retrieve the separate units, use a method similar to the following:

```java
int year = floor(version / 25000)
version %= 25000
int month = floor(version / 1800)
version %= 1800
int day = floor(version / 50)
int revision = version % 50
```

> **Note**: Do not expect the version sent in the [`0x08` Hello](../01_packet_structure/05_packet_types.md#0x08-hello) packet to match the version displayed in the game. There are multiple compatible versions that a client or server may have, the one sent to the server is simply its broadcast vesion.

---

> Previous section: [Converting Game IDs to and from Game Codes](02_converting_game_ids_to_and_from_game_codes.md)<br>
> Next section: [Map-Specific IDs for Vents and Tasks](04_map_specific_ids_for_vents_and_tasks.md)
