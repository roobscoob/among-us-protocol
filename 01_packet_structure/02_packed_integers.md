# Packed Integers

Packed integers, also known as variable integers (or `VarInt`), are numbers that have been encoded in such a way that they take up as few bytes as possible, with a maximum length of 5 bytes. The value of the number is encoded in the seven least-significant bits while the most-significant bit is used to tell the reader whether or not it needs to read another byte. The Hazel (C#) implementation, as used in Among Us, can be found below.

#### [`MessageReader.cs`](https://github.com/willardf/Hazel-Networking/blob/9dc6afef033a36a27e2d3d35f18c3b0bb8bfac87/Hazel/MessageReader.cs#L234-L266)

```c#
public int ReadPackedInt32()
{
    return (int)this.ReadPackedUInt32();
}

public uint ReadPackedUInt32()
{
    bool readMore = true;
    int shift = 0;
    uint output = 0;

    while (readMore)
    {
        if (this.BytesRemaining < 1) throw new InvalidDataException($"Read length is longer than message length.");

        byte b = this.ReadByte();
        if (b >= 0x80)
        {
            readMore = true;
            b ^= 0x80;
        }
        else
        {
            readMore = false;
        }

        output |= (uint)(b << shift);
        shift += 7;
    }

    return output;
}
```

#### [`MessageWriter.cs`](https://github.com/willardf/Hazel-Networking/blob/9dc6afef033a36a27e2d3d35f18c3b0bb8bfac87/Hazel/MessageWriter.cs#L266-L285)

```c#
public void WritePacked(int value)
{
    this.WritePacked((uint)value);
}

public void WritePacked(uint value)
{
    do
    {
        byte b = (byte)(value & 0xFF);
        if (value >= 0x80)
        {
            b |= 0x80;
        }

        this.Write(b);
        value >>= 7;
    } while (value > 0);
}
```

---

> Previous section: [Protocol Data Types](01_protocol_data_types.md)<br>
> Next section: [The Structure of a Hazel Message](03_the_structure_of_a_hazel_message.md)
