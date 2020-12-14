# Enums

#### Table of Contents

1. [`AlterGameTag`](#altergametag)
1. [`ChatNoteType`](#chatnotetype)
1. [`DisconnectReason`](#disconnectreason)
1. [`GameKeywords`](#gamekeywords)
1. [`GameOverReason`](#gameoverreason)
1. [`Map`](#map)
1. [`Color`](#color)
1. [`Hat`](#hat)
1. [`Pet`](#pet)
1. [`Skin`](#skin)
1. [`SystemType`](#systemtype)
1. [`TaskType`](#tasktype)
1. [`TaskBarUpdate`](#taskbarupdate)
1. [`SpawnType`](#spawntype)
1. [`SpawnFlag`](#spawnflag)
1. [`KillDistances`](#killdistances)
1. [`GameStates`](#gamestates)
1. [`LimboStates`](#limbostates)

### `AlterGameTag`

This refers to the types of tags associated with a game.

| ID | Name |
| --- | --- |
| `1` | `CHANGE_PRIVACY` |

### `ChatNoteType`

This refers to the types of special chat bubbles that may be sent.

| ID | Name |
| --- | --- |
| `0` | `DID_VOTE` |

### `DisconnectReason`

This refers to the condition that caused a player to be disconnected from a game.

| ID | Name |
| --- | --- |
| `0` | `EXIT_GAME` |
| `1` | `GAME_FULL` |
| `2` | `GAME_STARTED` |
| `3` | `GAME_NOT_FOUND` |
| `4` | `CUSTOM_MESSAGE_1` |
| `5` | `INCORRECT_VERSION` |
| `6` | `BANNED` |
| `7` | `KICKED` |
| `8` | `CUSTOM` |
| `9` | `INVALID_NAME` |
| `10` | `HACKING` |
| `16` | `DESTROY` |
| `17` | `ERROR` |
| `18` | `INCORRECT_GAME` |
| `19` | `SERVER_REQUEST` |
| `20` | `SERVER_FULL` |
| `207` | `FOCUS_LOST_BACKGROUND` |
| `208` | `INTENTIONAL_LEAVING` |
| `209` | `FOCUS_LOST` |
| `210` | `NEW_CONNECTION` |

### `GameKeywords`

This refers to the primary language that a game's players will be speaking.

| ID | Name |
| --- | --- |
| `0` | `ALL` |
| `1` | `OTHER` |
| `2` | `SPANISH` |
| `4` | `KOREAN` |
| `8` | `RUSSIAN` |
| `16` | `PORTUGUESE` |
| `32` | `ARABIC` |
| `64` | `FILIPINO` |
| `128` | `POLISH` |
| `256` | `ENGLISH` |

### `GameOverReason`

This refers to the condition that caused a game to finish.

| ID | Name |
| --- | --- |
| `0` | `CREWMATES_BY_VOTE` |
| `1` | `CREWMATES_BY_TASK` |
| `2` | `IMPOSTORS_BY_VOTE` |
| `3` | `IMPOSTORS_BY_KILL` |
| `4` | `IMPOSTORS_BY_SABOTAGE` |
| `5` | `IMPOSTOR_DISCONNECT` |
| `6` | `CREWMATE_DISCONNECT` |

### `Map`

This refers to the available maps that games can be played on.

When used in a bitfield, shift `1` to left by the map's ID.

Example:

```java
// Searching for games on The Skeld (0) or Polus (2)

(1 << 0) | (1 << 2) == 5
```

| ID | Name |
| --- | --- |
| `0` | `THE_SKELD` |
| `1` | `MIRA_HQ` |
| `2` | `POLUS` |

### `Color`

This refers to the customizable colors that a player can play as.

| ID | Name | RGB Value | Shaded RGB Value |
| --- | --- | --- | --- |
| `0` | `RED` | `198, 17, 17` | `122, 8, 56` |
| `1` | `BLUE` | `19, 46, 210` | `9, 21, 142` |
| `2` | `GREEN` | `17, 128, 45` | `10, 77, 46` |
| `3` | `PINK` | `238, 84, 187` | `172, 43, 174` |
| `4` | `ORANGE` | `240, 125, 13` | `180, 62, 21` |
| `5` | `YELLOW` | `246, 246, 87` | `195, 136, 34` |
| `6` | `GREY` | `63, 71, 78` | `30, 31, 38` |
| `7` | `WHITE` | `215, 225, 241` | `132, 149, 192` |
| `8` | `PURPLE` | `107, 47, 188` | `59, 23, 124` |
| `9` | `BROWN` | `113, 73, 30` | `94, 38, 21` |
| `10` | `CYAN` | `56, 255, 221` | `36, 169, 191` |
| `11` | `LIGHT_GREEN` | `80, 240, 57` | `21, 168, 66` |

### `Hat`

This refers to the customizable hats that a player can wear.

| ID | Name |
| --- | --- |
| `0` | `NONE` |
| `1` | `ASTRONAUT` |
| `2` | `BASEBALL_CAP` |
| `3` | `BRAIN_SLUG` |
| `4` | `BUSH_HAT` |
| `5` | `CAPTAIN_HAT` |
| `6` | `DOUBLE_TOP_HAT` |
| `7` | `FLOWERPOT` |
| `8` | `GOGGLES` |
| `9` | `HARD_HAT` |
| `10` | `MILITARY_HAT` |
| `11` | `PAPER_HAT` |
| `12` | `PARTY_HAT` |
| `13` | `POLICE_HAT` |
| `14` | `STETHOSCOPE` |
| `15` | `TOP_HAT` |
| `16` | `TOWEL_WIZARD` |
| `17` | `USHANKA` |
| `18` | `VIKING` |
| `19` | `WALL_GUARD_CAP` |
| `20` | `SNOWMAN` |
| `21` | `REINDEER_ANTLERS` |
| `22` | `CHRISTMAS_LIGHTS` |
| `23` | `SANTA_HAT` |
| `24` | `CHRISTMAS_TREE` |
| `25` | `CHRISTMAS_PRESENT` |
| `26` | `CANDY_CANES` |
| `27` | `ELF_HAT` |
| `28` | `NEW_YEARS_2018` |
| `29` | `WHITE_HAT` |
| `30` | `CROWN` |
| `31` | `EYEBROWS` |
| `32` | `HALO` |
| `33` | `HERO_CAP` |
| `34` | `PIP_CAP` |
| `35` | `PLUNGER` |
| `36` | `SCUBA_MASK` |
| `37` | `HENRY_STICKMIN` |
| `38` | `STRAW_HAT` |
| `39` | `TEN_GALLON_HAT` |
| `40` | `THIRD_EYE` |
| `41` | `TOILET_PAPER` |
| `42` | `TOPPAT_CLAN_LEADER` |
| `43` | `BLACK_FEDORA` |
| `44` | `SKI_GOGGLES` |
| `45` | `HEARING_PROTECTION` |
| `46` | `HAZMAT_MASK` |
| `47` | `FACE_MASK` |
| `48` | `SECURITY_HAT_GLASSES` |
| `49` | `SAFARI_HAT` |
| `50` | `BANANA` |
| `51` | `BEANIE` |
| `52` | `BEAR_EARS` |
| `53` | `CHEESE` |
| `54` | `CHERRY` |
| `55` | `EGG` |
| `56` | `GREEN_FEDORA` |
| `57` | `FLAMINGO` |
| `58` | `FLOWER` |
| `59` | `KNIGHT_HELMET` |
| `60` | `PLANT` |
| `61` | `BAT_EYES` |
| `62` | `BAT_WINGS` |
| `63` | `HORNS` |
| `64` | `MOHAWK` |
| `65` | `PUMPKIN` |
| `66` | `SCARY_PAPER_BAG` |
| `67` | `WITCH_HAT` |
| `68` | `WOLF_EARS` |
| `69` | `PIRATE_HAT` |
| `70` | `PLAGUE_DOCTOR` |
| `71` | `MACHETE` |
| `72` | `HOCKEY_MASK` |
| `73` | `MINER_HELMET` |
| `74` | `WINTER_CAP` |
| `75` | `ARCHAEOLOGIST_HAT` |
| `76` | `ANTENNA` |
| `77` | `BALLOON` |
| `78` | `BIRD_NEST` |
| `79` | `BLACK_BELT` |
| `80` | `CAUTION_SIGN` |
| `81` | `CHEF_HAT` |
| `82` | `COP_HAT` |
| `83` | `DO_RAG` |
| `84` | `DUM_STICKER` |
| `85` | `FEZ` |
| `86` | `GENERAL_HAT` |
| `87` | `POMPADOUR_HAIR` |
| `88` | `HUNTER_HAT` |
| `89` | `JUNGLE_HAT` |
| `90` | `MINI_CREWMATE` |
| `91` | `NINJA_MASK` |
| `92` | `RAM_HORNS` |
| `93` | `MINI_CREWMATE_SNOWMAN` |
| `94` | `GEOFF_KEIGHLEY_MASK` |

### `Pet`

This refers to the customizable pets that a player can be accompanied by.

| ID | Name |
| --- | --- |
| `0` | `NONE` |
| `1` | `ALIEN` |
| `2` | `MINI_CREWMATE` |
| `3` | `DOG` |
| `4` | `HENRY_STICKMIN` |
| `5` | `HAMSTER` |
| `6` | `ROBOT` |
| `7` | `UFO` |
| `8` | `ELLIE_ROSE` |
| `9` | `SQUIG` |
| `10` | `BEDCRAB` |
| `11` | `GLITCH` |

### `Skin`

This refers to the customizable skins that a player can wear.

| ID | Name |
| --- | --- |
| `0` | `NONE` |
| `1` | `ASTRONAUT` |
| `2` | `CAPTAIN` |
| `3` | `MECHANIC` |
| `4` | `MILITARY` |
| `5` | `POLICE` |
| `6` | `SCIENTIST` |
| `7` | `SUIT_BLACK` |
| `8` | `SUIT_WHITE` |
| `9` | `WALL_GUARD` |
| `10` | `HAZMAT` |
| `11` | `SECURITY_GUARD` |
| `12` | `TARMAC` |
| `13` | `MINER` |
| `14` | `WINTER` |
| `15` | `ARCHAEOLOGIST` |

### `SystemType`

This refers to the various rooms and systems found throughout each map.

| ID | Name |
| --- | --- |
| `0` | `HALLWAY` |
| `1` | `STORAGE` |
| `2` | `CAFETERIA` |
| `3` | `REACTOR` |
| `4` | `UPPER_ENGINE` |
| `5` | `NAVIGATION` |
| `6` | `ADMIN` |
| `7` | `ELECTRICAL` |
| `8` | `O2` |
| `9` | `SHIELDS` |
| `10` | `MEDBAY` |
| `11` | `SECURITY` |
| `12` | `WEAPONS` |
| `13` | `LOWER_ENGINE` |
| `14` | `COMMUNICATIONS` |
| `15` | `SHIP_TASKS` |
| `16` | `DOORS` |
| `17` | `SABOTAGE` |
| `18` | `DECONTAMINATION` |
| `19` | `LAUNCHPAD` |
| `20` | `LOCKER_ROOM` |
| `21` | `LABORATORY` |
| `22` | `BALCONY` |
| `23` | `OFFICE` |
| `24` | `GREENHOUSE` |
| `25` | `DROPSHIP` |
| `26` | `DECONTAMINATION_2` |
| `27` | `OUTSIDE` |
| `28` | `SPECIMENS` |
| `29` | `BOILER_ROOM` |

### `TaskType`

This refers to the various types of tasks that a player can be assigned.

For a list of all tasks on each map, see [Map-Specific IDs for Vents and Tasks](../07_miscellaneous/04_map_specific_ids_for_vents_and_tasks.md).

| ID | Name |
| --- | --- |
| `0` | `SUBMIT_SAN` |
| `1` | `PRIME_SHIELDS` |
| `2` | `FUEL_ENGINES` |
| `3` | `CHART_COURSE` |
| `4` | `START_REACTOR` |
| `5` | `SWIPE_CARD` |
| `6` | `CLEAR_ASTEROIDS` |
| `7` | `UPLOAD_DATA` |
| `8` | `INSPECT_SAMPLE` |
| `9` | `EMPTY_CHUTE` |
| `10` | `EMPTY_GARBAGE` |
| `11` | `ALIGN_ENGINE_OUTPUT` |
| `12` | `FIX_WIRING` |
| `13` | `CALIBRATE_DISTRIBUTOR` |
| `14` | `DIVERT_POWER` |
| `15` | `UNLOCK_MANIFOLDS` |
| `16` | `RESET_REACTOR` |
| `17` | `FIX_LIGHTS` |
| `18` | `CLEAN_O2_FILTER` |
| `19` | `FIX_COMMS` |
| `20` | `RESTORE_O2` |
| `21` | `STABILIZE_STEERING` |
| `22` | `ASSEMBLE_ARTIFACT` |
| `23` | `SORT_SAMPLES` |
| `24` | `MEASURE_WEATHER` |
| `25` | `ENTER_ID_CODE` |
| `26` | `BUY_BEVERAGE` |
| `27` | `PROCESS_DATA` |
| `28` | `RUN_DIAGNOSTICS` |
| `29` | `WATER_PLANTS` |
| `30` | `MONITOR_O2` |
| `31` | `STORE_ARTIFACTS` |
| `32` | `FILL_CANISTERS` |
| `33` | `ACTIVATE_WEATHER_NODES` |
| `34` | `INSERT_KEYS` |
| `35` | `RESET_SEISMIC` |
| `36` | `SCAN_BOARDING_PASS` |
| `37` | `OPEN_WATERWAYS` |
| `38` | `REPLACE_WATER_JUG` |
| `39` | `REPAIR_DRILL` |
| `40` | `ALIGN_TELESCOPE` |
| `41` | `RECORD_TEMPERATURE` |
| `42` | `REBOOT_WIFI` |

### `TaskBarUpdate`

This refers to the `Task Bar Updates` field in the [`GameOptionsData`](../07_miscellaneous/01_the_structure_of_the_gameoptionsdata_object.md) object.

| ID | Name |
| --- | --- |
| `0` | `ALWAYS` |
| `1` | `MEETINGS` |
| `2` | `NEVER` |

### `SpawnType`

This refers to the various [`InnerNetObject`s](../05_innernetobject_types/README.md) that may be spawned.

| ID | Name |
| --- | --- |
| `0` | `SHIP_STATUS` |
| `1` | `MEETING_HUD` |
| `2` | `LOBBY_BEHAVIOUR` |
| `3` | `GAME_DATA` |
| `4` | `PLAYER_CONTROL` |
| `5` | `HEADQUARTERS` |
| `6` | `PLANET_MAP` |
| `7` | `APRIL_SHIP_STATUS` |

### `SpawnFlag`

This refers to the various flags that an [`InnerNetObject`](../05_innernetobject_types/README.md) may have associated with it when spawned.

| ID | Name |
| --- | --- |
| `0` | `NONE` |
| `1` | `IS_CLIENT_CHARACTER` |

### `KillDistances`

This refers to the `Kill Distance` field in the [`GameOptionsData`](../07_miscellaneous/01_the_structure_of_the_gameoptionsdata_object.md) object. Each unit has a corresponding `float` representing the magnitude ![magnitude of vector K to vector V](https://render.githubusercontent.com/render/math?math=\overrightarrow{\text{KV}}), or distance, between the killer and victim

| ID | Name | Magnitude |
| --- | --- | --- |
| `0` | `SHORT` | `1.0f` |
| `1` | `NORMAL` | `1.8f` |
| `2` | `LONG` | `2.5f` |

### `GameStates`

| ID | Name |
| --- | --- |
| `0` | `NOT_STARTED` |
| `1` | `STARTED` |
| `2` | `ENDED` |
| `3` | `DESTROYED` |

### `LimboStates`

| ID | Name |
| --- | --- |
| `0` | `PRE_SPAWN` |
| `1` | `NOT_LIMBO` |
| `2` | `WAITING_FOR_HOST` |

---

> Previous section: [Packet Types](05_packet_types.md)<br>
> Next section: [The Different Types of IDs](07_the_different_types_of_ids.md)
