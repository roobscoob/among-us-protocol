# `0xcd` ClientInfo

### Client-to-Server

This message is sent by the client to the server when joining the game and is used to identify the platform that the client is playing on.

| Type | Name | Description |
| --- | --- | --- |
| `packed uint32` | Client ID | The ID of the client |
| `packed uint32` | Platform ID | The ID of the platform that the client is playing on |

<details>
    <summary>Click here to view an example packet</summary>

```
01                # Reliable packet
0069              # Nonce
090005            # Hazel message (tag of 0x05 = GameData)
    d3503f8a      # Game ID: -1975562029 (REDSUS)
    0200cd        # Hazel message (tag of 0xcd = ClientInfo)
        05        # Client ID: 5
        02        # Platform ID: 2 (WindowsPlayer)
```
</details>

### The Unity `RuntimePlatform` Enum

The `Platform ID` field corresponds to a platform in Unity's `RuntimePlatform` enum, whose values are listed in the table below.

| ID | Name |
| --- | --- |
| `0` | OSXEditor |
| `1` | OSXPlayer |
| `2` | WindowsPlayer |
| `7` | WindowsEditor |
| `8` | IPhonePlayer |
| `11` | Android |
| `13` | LinuxPlayer |
| `16` | LinuxEditor |
| `17` | WebGLPlayer |
| `18` | WSAPlayerX86 |
| `19` | WSAPlayerX64 |
| `20` | WSAPlayerARM |
| `25` | PS4 |
| `27` | XboxOne |
| `31` | tvOS |
| `32` | Switch |
| `33` | Lumin |
| `34` | Stadia |
| `35` | CloudRendering |
| `36` | PS5 |

---

> Previous section: [`0x08` ChangeSettings](08_changesettings.md)
