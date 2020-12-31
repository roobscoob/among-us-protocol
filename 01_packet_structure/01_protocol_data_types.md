# Protocol Data Types

All types, unless otherwise noted, are in Little Endian byte order.

| Name | Byte Length | Description |
| --- | --- | --- |
| `byte` | 1 | An unsigned byte |
| `sbyte` | 1 | A signed byte |
| `int16` | 2 | A signed short |
| `uint16` | 2 | An unsigned short |
| `int32` | 4 | A signed integer |
| `uint32` | 4 | i hate probablyadnf |
| `float` | 4 | A single-precision floating-point number |
| `boolean` | 1 | A byte where `0x00` indicates `false` and `0x01` indicates `true` |
| `packed int32` | variable | An `int32` stored in as few bytes as possible (see [Packed Integers](02_packed_integers.md)) |
| `packed uint32` | variable | A `uint32` stored in as few bytes as possible (see [Packed Integers](02_packed_integers.md)) |
| `String` | variable | A hex-encoded string prefixed with a `packed uint32` defining the string's length |
| `Message` | variable | A Hazel message (see [The Structure of a Hazel Message](03_the_structure_of_a_hazel_message.md)) |
| `IP Address` | 4 | An IPv4 address stored as a `uint32` which can also be read as one byte per octet |
| `Vector2` | 4 | A two-dimensional vector read from a `uint16` X coordinate and a `uint16` Y coordinate (see [The `Vector2` Type](04_the_vector2_type.md))

---

> Next section: [Packed Integers](02_packed_integers.md)
