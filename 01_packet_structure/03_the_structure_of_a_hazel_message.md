# The Structure of a Hazel Message

A Hazel message is always prefixed with a `uint16` to define the message's length in bytes. Immediately following the length is a single byte known as the tag and is often used to identify the type of data contained within the message. Understanding this basic construct which is used throughout the Among Us protocol is key to understanding how to manually read and dissect packets and further your overall understanding of the game's netcode.

> **Note**: The length **never** includes the tag as part of the payload, and the tag does not always have a meaning behind it.

Take the following message for example:

```
06  00  01  05  48  65  6c  6c  6f
|----/  |/  |--------------------/
|       |   |
|       |   Payload with a length of 6 as previously defined (in this case it's a string that says "Hello")
|       |
|       Message tag (arbitrarily chosen to be 1 for this example)
|
Message length (this message therefore has a body whose length is 6 bytes long)
```

---

> Previous section: [Packed Integers](02_packed_integers.md)<br>
> Next section: [The `Vector2` Type](04_the_vector2_type.md)
