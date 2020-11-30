# Packet Types

Below you will find a section for each type of packet that could be sent over the network. In each section is a short description of the packet's use case, a declaration on whether or not a packet of that type needs to be acknowleged, the structure of the packet, and an example packet that has been broken down and annotated. Every packet starts with a `byte` identifying its type, and so it will be omitted from the packet structure tables found below.

> **Note**: Internally, these types are referred to as a `SendOption`.

#### Table of Contents

1. [`0x00` Normal](#0x00-normal)
1. [`0x01` Reliable](#0x01-reliable)
1. [`0x08` Hello](#0x08-hello)
1. [`0x09` Disconnect](#0x09-disconnect)
1. [`0x0a` Acknowledgement](#0x0a-acknowledgement)
1. [`0x0b` Fragment](#0x0b-fragment)
1. [`0x0c` Ping](#0x0c-ping)

### `0x00` Normal

A `Normal` packet is primarily used to transmit updates to various [`InnerNetObject`s](../05_innernetobject_types/README.md).

`Normal` packets **do not** need to be acknowledged.

The `Normal` packet structure is as follows:

| Type | Name | Description |
| --- | --- | --- |
| `Message[n]` | Payload | One or more [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) containing the packet's payload<br><br>The message tag is the [Message Type](../02_root_message_types/README.md) |

For a list of all messages that could be sent using this packet type, as well as example packets for each, see [Root Message Types](../02_root_message_types/README.md).

> **Note**: A `Normal` packet may have more than one [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) in its payload. You should encapsulate your logic for reading these messages in a loop that checks if there are more bytes to be read. An example implementation might look similar to the following pseudocode:

```java
void parseNormal(MessageReader payload) {
    MessageReader child;

    // This while loop attempts to read another message and, if successful (not null), continues the loop
    while ((child = payload.readMessage()) != null) {
        // We can now read each sub-message individually according to its type
    }
}
```

### `0x01` Reliable

A `Reliable` packet is used to transmit game state changes and various client actions such as joining a game, completing a task, entering a vent, repairing a sabotage, and more.

`Reliable` packets **do** need to be acknowledged.

The `Reliable` packet structure is as follows:

| Type | Name | Description |
| --- | --- | --- |
| `uint16` (*Big Endian*) | Nonce | The ID of this packet so that the receiver can acknowledge it upon receipt |
| `Message[n]` | Payload | One or more [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) containing the packet's payload<br><br>The message tag is the [Message Type](../02_root_message_types/README.md) |

For a list of all messages that could be sent using this packet type, as well as example packets for each, see [Root Message Types](../02_root_message_types/README.md).

> **Note**: A `Reliable` packet may have more than one [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) in its payload. You should encapsulate your logic for reading these messages in a loop that checks if there are more bytes to be read. An example implementation might look similar to the following pseudocode:

```java
void parseReliable(MessageReader payload, int nonce) {
    MessageReader child;

    // This while loop attempts to read another message and, if successful (not null), continues the loop
    while ((child = payload.readMessage()) != null) {
        // We can now read each sub-message individually according to its type
    }

    sendAck(nonce);
}
```

### `0x08` Hello

The `Hello` packet is sent upon loading the game list, creating a game, and joining a game, and is used to initiate a connection with the game servers.

`Hello` packets **do** need to be acknowledged.

The `Hello` packet structure is as follows:

| Type | Name | Description |
| --- | --- | --- |
| `uint16` (*Big Endian*) | Nonce | The ID of this packet so that the receiver can acknowledge it upon receipt |
| `byte` | Hazel Version | The version of Hazel that the client is using |
| `int32` | Client Version | The version of the game that the client is connecting from (see [Reading the Client Version](../07_miscellaneous/03_reading_the_client_version.md)) |
| `String` | Username | The client's username |

<details>
    <summary>Click here to view an example packet</summary>
<pre>
08  00  01  00  46  d2  02  03  08  55  73  65  72  6e  61  6d  65
|/  |----/  |/  |------------/  |--------------------------------/
|   |       |   |               |
|   |       |   |               Length-prefixed string containing the client's name, "Username" in this case
|   |       |   |
|   |       |   Client version: 2020.9.7.0
|   |       |
|   |       Hazel version
|   |
|   Nonce
|
Packet type
</pre>
</details>

### `0x09` Disconnect

The `Disconnect` packet is sent upon the client's connection to the game servers being terminated. This packet's size can range from 1 byte long (e.g. clicking "Back" on the game list screen) or several bytes long in the case of a custom disconnect message.

`Disconnect` packets **do not** need to be acknowledged.

The `Disconnect` packet structure, when containing a [Disconnect Reason](06_enums.md#disconnectreason), is as follows:

| Type | Name | Description |
| --- | --- | --- |
| `byte` | Is Forced | While this `byte` is similar to a `boolean`, it has different conditions:<br><ul><li>If this value is **exactly** `1` then the `Disconnect Reason` below will be parsed and displayed</li><li>If this value is **anything but** `1` then the `Disconnect Reason` below will not be read and the game will display the message *"Forcibly disconnected from the server"*</li></ul> |
| `Message` | Disconnect Reason | A [Hazel message](../01_packet_structure/03_the_structure_of_a_hazel_message.md) describing why the client was disconnected<br><br><table><thead><tr><th>Type</th><th>Name</th><th>Description</th></tr></thead><tbody><tr><td>`byte`</td><td>[Disconnect Reason](06_enums.md#disconnectreason)</td><td>The reason for the disconnection</td></tr><tr><td>`String` (*Optional*)</td><td>Custom Message</td><td>A custom disconnect message</td></tr></tbody></table> |

<details>
    <summary>Click here to view an example packet</summary>
<pre>
        Hazel Message
        |
        |------------------------------------\
09  01  07  00  00  08  05  48  65  6c  6c  6f
|/  |/  |----/  |/  |/  |--------------------/
|   |   |       |   |   |
|   |   |       |   |   Length-prefixed string containing a custom message, "Hello" in this case
|   |   |       |   |
|   |   |       |   Disconnect Reason: 8 (CUSTOM)
|   |   |       |
|   |   |       Message tag
|   |   |
|   |   Message length: 7 bytes
|   |
|   Is Forced: false
|
Packet type
</pre>
</details>

### `0x0a` Acknowledgement

The `Acknowledgement` packet is sent upon receipt of a packet that requires acknowledgement.

`Acknowledgement` packets **do not** need to be acknowledged as this would create an infinite loop.

The `Acknowledgement` packet structure is as follows:

| Type | Name | Description |
| --- | --- | --- |
| `uint16` (*Big Endian*) | Nonce | The ID of the packet that is being acknowledged |
| `byte` | Missing Packets | A bitfield describing whether or not each of the last eight reliable packets sent have been acknowledged |

When sending an acknowledgement packet, the sender will attach a `byte` representing the eight most recent reliable packets sent. Starting with the previous packet (`n - 1` where `n` is the ID of the packet currently being acknowledged) and ending with the 8th most recent packet (`n - 8`) a bit will either be set or unset (from bit `1` to `8` respectively) representing whether or not the sender received an acknowledgement for that packet.

Given the example `0b11110101` (`0xf5`) we can see that the second and fourth packets have not yet been acknowledged by the receiver.

<details>
    <summary>Click here to view an example packet</summary>
<pre>
0c  00  07  ff
|/  |----/  |/
|   |       |
|   |       Missing Packets (none, all have been acknowledged)
|   |
|   Nonce
|
Packet type
</pre>
</details>

### `0x0b` Fragment

The `Fragment` packet, although never used in Among Us (and not yet implemented in Hazel), would be used to send larger payloads across multiple smaller packets.

`Fragment` packets **do not** need to be acknowledged.

### `0x0c` Ping

The `Ping` packet is sent periodically to check the status of the network connection.

`Ping` packets **do** need to be acknowledged.

The `Ping` packet structure is as follows:

| Type | Name | Description |
| --- | --- | --- |
| `uint16` (*Big Endian*) | Nonce | The ID of this packet so that the receiver can acknowledge it upon receipt |

<details>
    <summary>Click here to view an example packet</summary>
<pre>
0c  00  07
|/  |----/
|   |
|   Nonce
|
Packet type
</pre>
</details>

---

> Previous section: [The `Vector2` Type](04_the_vector2_type.md)<br>
> Next section: [Enums](06_enums.md)
