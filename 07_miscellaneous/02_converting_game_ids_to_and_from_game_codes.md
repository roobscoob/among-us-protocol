# Converting Game IDs to and from Game Codes

Among Us uses six-letter codes to identify games and allow players to invite others to their game. Previous versions were four letters long but with the rise in popularity came the frequent issue of collisions. The four-letter variants were simply the ASCII uppercase letter in hexadecimal. Six-letter codes use a special encoding to maintain backwards-compatibility with a size of four bytes.

##### Converting an ID to a String Code

An example implementation in Java can be found below for converting a game's ID into a human-readable game code.

```java
import java.nio.ByteBuffer;
import java.nio.ByteOrder;
import java.nio.charset.StandardCharsets;
import java.util.stream.Collectors;
import java.util.stream.Stream;

private static final char[] CHAR_SET = "QWXRTYLPESDFGHUJKZOCVBINMA".toCharArray();

public static String intToCode(long gameId) {
    if (gameId < -1) {
        // Version 2 codes will always be negative
        int firstTwo = (int) (gameId & 0x3FF);
        int lastFour = (int) ((gameId >> 10) & 0xFFFFF);

        return Stream.of(
            CHAR_SET[firstTwo % 26],
            CHAR_SET[firstTwo / 26],
            CHAR_SET[lastFour % 26],
            CHAR_SET[(lastFour /= 26) % 26],
            CHAR_SET[(lastFour /= 26) % 26],
            CHAR_SET[lastFour / 26 % 26]
        ).map(String::valueOf).collect(Collectors.joining());
    } else {
        // Version 1 codes will always be positive
        return new String(
            ByteBuffer.allocate(4).order(ByteOrder.LITTLE_ENDIAN).putInt(Math.toIntExact(gameId)).array(),
            StandardCharsets.UTF_8
        );
    }
}

// Some simple tests
public static void main(String... args) {
    assert intToCode(1312905539) == "CYAN";
    assert intToCode(-1975562029) == "REDSUS";
}
```

##### Converting a String Code to an ID

An example implementation in Java can be found below for converting a human-readable game code into a game's ID.

```java
import java.nio.ByteBuffer;
import java.nio.ByteOrder;

private static final int[] CHAR_MAP = { 25, 21, 19, 10, 8, 11, 12, 13, 22, 15, 16, 6, 24, 23, 18, 7, 0, 3, 9, 4, 14, 20, 1, 2, 5, 17 };

public static int codeToInt(String gameCode)
throws IllegalArgumentException {
    gameCode = gameCode.toUpperCase();

    if (gameCode.chars().anyMatch(character -> !Character.isLetter(character))) {
        throw new IllegalArgumentException("Invalid code, expected letters only: " + gameCode);
    }

    if (gameCode.length() == 4) {
        return ByteBuffer.wrap(gameCode.getBytes()).order(ByteOrder.LITTLE_ENDIAN).getInt();
    }

    if (gameCode.length() != 6) {
        throw new IllegalArgumentException("Invalid code length, expected 4 or 6 characters: " + gameCode);
    }

    int first = CHAR_MAP[(int) gameCode.charAt(0) - 65];
    int second = CHAR_MAP[(int) gameCode.charAt(1) - 65];
    int third = CHAR_MAP[(int) gameCode.charAt(2) - 65];
    int fourth = CHAR_MAP[(int) gameCode.charAt(3) - 65];
    int fifth = CHAR_MAP[(int) gameCode.charAt(4) - 65];
    int sixth = CHAR_MAP[(int) gameCode.charAt(5) - 65];

    int firstTwo = (first + 26 * second) & 0x3FF;
    int lastFour = (third + 26 * (fourth + 26 * (fifth + 26 * sixth)));

    return firstTwo | ((lastFour << 10) & 0x3FFFFC00) | 0x80000000;
}

// Some simple tests
public static void main(String... args) {
    assert codeToInt("CYAN") == 1312905539;
    assert codeToInt("REDSUS") == -1975562029;
}
```

---

> Previous section: [The Structure of the `GameOptionsData` Object](01_the_structure_of_the_gameoptionsdata_object.md)<br>
> Next section: [Reading the Client Version](03_reading_the_client_version.md)
