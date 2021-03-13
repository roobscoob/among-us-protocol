# The `Vector2` Type

Each `Vector2`, when sent over the network, has a pair of `uint16` fields: one for the X axis and one for the Y axis. Each of these values should be divided by `65535.0f` and passed in to a `Lerp` function, clamped between `0.0f` and `1.0f`, on a range of floats from `-50.0f` to `50.0f`. The result of the `Lerp` function will be the `float` value representing either the X or Y value of the `Vector2`.

**Note:** previously (I guess [Client Version](../07_miscellaneous/03_reading_the_client_version.md) < 50530650 or more old) game using `-40.0f` to `40.0f` for float ranges instead of `-50.0f` to `50.0f`.

Below is an example implementation in Java:

```java
// Usage example

private static FloatRange rangeX = new FloatRange(-50.0f, 50.0f);
private static FloatRange rangeY = new FloatRange(-50.0f, 50.0f);

public static Vector2 readVector2(MessageReader reader) {
    float x = (float) reader.readUInt16() / 65535.0f;
    float y = (float) reader.readUInt16() / 65535.0f;

    return new Vector2(rangeX.lerp(x), rangeY.lerp(y));
}

public static void writeVector2(MessageWriter writer, Vector2 vec) {
    // These are uint16, but we declare them as an int since Java has no unsigned primitives
    int x = (int) rangeX.reverseLerp(vec.x) * 65535.0f;
    int y = (int) rangeY.reverseLerp(vec.y) * 65535.0f;

    writer.writeUInt16(x);
    writer.writeUInt16(y);
}

// Class definitions

public class Vector2 {
    public float x;
    public float y;

    public Vector2(float x, float y) {
        this.x = x;
        this.y = y;
    }
}

public class FloatRange {
    public float min;
    public float max;

    public FloatRange(float min, float max) {
        this.min = min;
        this.max = max;
    }

    /*
     * Used when reading a Vector2
     */
    public float lerp(float value) {
        if (0.0 > value) {
            value = 0.0f;
        } else if (1.0 < value) {
            value = 1.0f;
        }

        return this.min + ((this.max - this.min) * value);
    }

    /*
     * Used when writing a Vector2
     */
    public float reverseLerp(float value) {
        value = (value - this.min) / (this.max - this.min);

        if (0.0 > value) {
            value = 0.0f;
        } else if (1.0 < value) {
            value = 1.0f;
        }

        return value;
    }
}
```

---

> Previous section: [The Structure of a Hazel Message](03_the_structure_of_a_hazel_message.md)<br>
> Next section: [Packet Types](05_packet_types.md)
