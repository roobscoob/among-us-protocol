# `0x0d` Redirect

### Server-to-Client

This message is sent from the server to a client after creating a new game and tells the client which server the game is being hosted on.

| Type | Name | Description |
| --- | --- | --- |
| `IP Address` | IP Address | The IP address of the server that the game is hosted on |
| `uint16` | Port | The port that the server is listening on |

<details>
    <summary>Click here to view an example packet</summary>

```
01              # Reliable packet
0001            # Nonce
06000d          # Hazel message (tag of 0x0d = Redirect)
    c63a7359    # IP Address: 198.58.115.89
    0756        # Port: 22023
```
</details>

---

> Previous section: [`0x0c` WaitForHost](12_waitforhost.md)<br>
> Next section: [`0x0e` ReselectServer](14_reselectserver.md)
