# Map-Specific IDs for Vents and Tasks

All vents in the tables below include an X and Y coordinate which can be used in conjunction with the [`0x15` SnapTo](../04_rpc_message_types/21_snapto.md) message to determine if a player is moving between vents. The tasks in the tables below are used when the game sets each player's tasks via the [`0x1d` SetTasks](../04_rpc_message_types/29_settasks.md) message.

#### Table of Contents

1. [The Skeld](#the-skeld)
    1. [Vents](#vents)
    1. [Tasks](#tasks)
1. [Mira HQ](#mira-hq)
    1. [Vents](#vents-1)
    1. [Tasks](#tasks-1)
1. [Polus](#polus)
    1. [Vents](#vents-2)
    1. [Tasks](#tasks-2)

### The Skeld

##### Vents

| ID | Location | Coordinates `(x, y)` |
| --- | --- | --- |
| `0` | In Admin | `2.543373`, `-9.59182` |
| `1` | In the right hallway | `9.38308`, `-6.0749207` |
| `2` | In the Cafeteria | `4.2584915`, `0.08728027` |
| `3` | In Electrical | `-9.777372`, `-7.6704063` |
| `4` | In the Upper Engine | `-15.288929`, `2.8827324` |
| `5` | In Security | `-12.534981`, `-6.586403` |
| `6` | In Medbay | `-10.608683`, `-3.8129234` |
| `7` | In Weapons | `8.819103`, `3.687191` |
| `8` | In Lower Reactor | `-20.796825`, `-6.590065` |
| `9` | In the Lower Engine | `-15.251087`, `-13.293049` |
| `10` | In Shields | `9.52224`, `-13.974211` |
| `11` | In Upper Reactor | `-21.877165`, `-2.6886406` |
| `12` | In Upper Navigation | `16.007935`, `-2.8046074` |
| `13` | In Lower Navigation | `16.007935`, `-6.0212097` |

##### Tasks

| ID | Description | [`TaskType`](../01_packet_structure/06_enums.md#tasktype) | Length | Is Visual |
| --- | --- | --- | --- | --- |
| `0` | Admin: Swipe Card | `SWIPE_CARD` | Common | &#x2716; |
| `1` | Electrical: Fix Wiring | `FIX_WIRING` | Common | &#x2716; |
| `2` | Weapons: Clear Asteroids | `CLEAR_ASTEROIDS` | Long | &#x2714; |
| `3` | Engines: Align Engine Output | `ALIGN_ENGINE_OUTPUT` | Short | &#x2716; |
| `4` | Medbay: Submit Scan | `SUBMIT_SAN` | Long | &#x2714; |
| `5` | Medbay: Inspect Sample | `INSPECT_SAMPLE` | Long | &#x2716; |
| `6` | Storage: Fuel Engines | `FUEL_ENGINES` | Long | &#x2716; |
| `7` | Reactor: Start Reactor | `START_REACTOR` | Long | &#x2716; |
| `8` | O2: Empty Chute | `EMPTY_CHUTE` | Long | &#x2714; |
| `9` | Cafeteria: Empty Garbage | `EMPTY_GARBAGE` | Long | &#x2714; |
| `10` | Communications: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `11` | Electrical: Calibrate Distributor | `CALIBRATE_DISTRIBUTOR` | Short | &#x2716; |
| `12` | Navigation: Chart Course | `CHART_COURSE` | Short | &#x2716; |
| `13` | O2: Clean O2 Filter | `CLEAN_O2_FILTER` | Short | &#x2716; |
| `14` | Reactor: Unlock Manifolds | `UNLOCK_MANIFOLDS` | Short | &#x2716; |
| `15` | Electrical: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `16` | Navigation: Stabilize Steering | `STABILIZE_STEERING` | Short | &#x2716; |
| `17` | Weapons: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `18` | Shields: Prime Shields | `PRIME_SHIELDS` | Short | &#x2714; |
| `19` | Cafeteria: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `20` | Navigation: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `21` | Electrical: Divert Power to Shields | `DIVERT_POWER` | Short | &#x2716; |
| `22` | Electrical: Divert Power to Weapons | `DIVERT_POWER` | Short | &#x2716; |
| `23` | Electrical: Divert Power to Communications | `DIVERT_POWER` | Short | &#x2716; |
| `24` | Electrical: Divert Power to Upper Engine | `DIVERT_POWER` | Short | &#x2716; |
| `25` | Electrical: Divert Power to O2 | `DIVERT_POWER` | Short | &#x2716; |
| `26` | Electrical: Divert Power to Navigation | `DIVERT_POWER` | Short | &#x2716; |
| `27` | Electrical: Divert Power to Lower Engine | `DIVERT_POWER` | Short | &#x2716; |
| `28` | Electrical: Divert Power to Security | `DIVERT_POWER` | Short | &#x2716; |

### Mira HQ

##### Vents

> **Note**: *Mira HQ* vent IDs start at `1`.

| ID | Location | Coordinates `(x, y)` |
| --- | --- | --- |
| `1` | On the Balcony | `23.769283`, `-1.576561` |
| `2` | In the Cafeteria | `23.899899`, `7.5434494` |
| `3` | In the Reactor | `0.4791336`, `11.0603485` |
| `4` | In the Laboratory | `11.60479`, `14.179291` |
| `5` | In the Office | `13.279617`, `20.492867` |
| `6` | In Admin | `22.38987`, `17.59243` |
| `7` | In the Greenhouse | `17.848782`, `25.59304` |
| `8` | In Medbay | `15.409779`, `-1.4569321` |
| `9` | In Decontamination | `6.8293304`, `3.5077438` |
| `10` | In the Locker Room | `4.289009`, `0.8929596` |
| `11` | At the Launchpad | `-6.1811256`, `3.9227905` |

##### Tasks

| ID | Description | [`TaskType`](../01_packet_structure/06_enums.md#tasktype) | Length | Is Visual |
| --- | --- | --- | --- | --- |
| `0` | Hallway: Fix Wiring | `FIX_WIRING` | Common | &#x2716; |
| `1` | Admin: Enter ID Code | `ENTER_ID_CODE` | Common | &#x2716; |
| `2` | Medbay: Submit Scan | `SUBMIT_SAN` | Long | &#x2714; |
| `3` | Balcony: Clear Asteroids | `CLEAR_ASTEROIDS` | Long | &#x2716; |
| `4` | Electrical: Divert Power to Admin | `DIVERT_POWER` | Short | &#x2716; |
| `5` | Electrical: Divert Power to Cafeteria | `DIVERT_POWER` | Short | &#x2716; |
| `6` | Electrical: Divert Power to Communications | `DIVERT_POWER` | Short | &#x2716; |
| `7` | Electrical: Divert Power to Launchpad | `DIVERT_POWER` | Short | &#x2716; |
| `8` | Electrical: Divert Power to Medbay | `DIVERT_POWER` | Short | &#x2716; |
| `9` | Electrical: Divert Power to Office | `DIVERT_POWER` | Short | &#x2716; |
| `10` | Storage: Water Plants | `WATER_PLANTS` | Long | &#x2716; |
| `11` | Reactor: Start Reactor | `START_REACTOR` | Long | &#x2716; |
| `12` | Electrical: Divert Power to Greenhouse | `DIVERT_POWER` | Short | &#x2716; |
| `13` | Admin: Chart Course | `CHART_COURSE` | Short | &#x2716; |
| `14` | Greenhouse: Clean O2 Filter | `CLEAN_O2_FILTER` | Short | &#x2716; |
| `15` | Launchpad: Fuel Engines | `FUEL_ENGINES` | Short | &#x2716; |
| `16` | Laboratory: Assemble Artifact | `ASSEMBLE_ARTIFACT` | Short | &#x2716; |
| `17` | Laboratory: Sort Samples | `SORT_SAMPLES` | Short | &#x2716; |
| `18` | Admin: Prime Shields | `PRIME_SHIELDS` | Short | &#x2716; |
| `19` | Cafeteria: Empty Garbage | `EMPTY_GARBAGE` | Short | &#x2716; |
| `20` | Balcony: Measure Weather | `MEASURE_WEATHER` | Short | &#x2716; |
| `21` | Electrical: Divert Power to Laboratory | `DIVERT_POWER` | Short | &#x2716; |
| `22` | Cafeteria: Buy Beverage | `BUY_BEVERAGE` | Short | &#x2716; |
| `23` | Office: Process Data | `PROCESS_DATA` | Short | &#x2716; |
| `24` | Launchpad: Run Diagnostics | `RUN_DIAGNOSTICS` | Long | &#x2716; |
| `25` | Reactor: Unlock Manifolds | `UNLOCK_MANIFOLDS` | Short | &#x2716; |

### Polus

##### Vents

| ID | Location | Coordinates `(x, y)` |
| --- | --- | --- |
| `0` | By Security | `1.9281311`, `-9.195087` |
| `1` | Outside Electrical | `6.8989105`, `-14.047455` |
| `2` | In O2 | `3.5089645`, `-16.216679` |
| `3` | Outside Communications | `12.303043`, `-18.53483` |
| `4` | In the Office | `16.377811`, `-19.235523` |
| `5` | In Admin | `20.088806`, `-25.153582` |
| `6` | In the Laboratory | `32.96254`, `-9.163349` |
| `7` | By the Lava Pool | `30.906845`, `-11.497368` |
| `8` | In Storage | `21.999237`, `-11.826963` |
| `9` | By the right Seismic Stabilizer | `24.019531`, `-8.026855` |
| `10` | By the left Seismic Stabilizer | `9.639431`, `-7.356678` |
| `11` | Outside Admin | `18.929123`, `-24.487068` |

##### Tasks

| ID | Description | [`TaskType`](../01_packet_structure/06_enums.md#tasktype) | Length | Is Visual |
| --- | --- | --- | --- | --- |
| `0` | Office: Swipe Card | `SWIPE_CARD` | Common | &#x2716; |
| `1` | Dropship: Insert Keys | `INSERT_KEYS` | Common | &#x2716; |
| `2` | Office: Scan Boarding Pass | `SCAN_BOARDING_PASS` | Common | &#x2716; |
| `3` | Electrical: Fix Wiring | `FIX_WIRING` | Common | &#x2716; |
| `4` | Weapons: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `5` | Office: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `6` | Electrical: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `7` | Specimen Room: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `8` | O2: Download Data | `UPLOAD_DATA` | Short | &#x2716; |
| `9` | Specimen Room: Start Reactor | `START_REACTOR` | Long | &#x2716; |
| `10` | Storage: Fuel Engines | `FUEL_ENGINES` | Long | &#x2716; |
| `11` | Boiler Room: Open Waterways | `OPEN_WATERWAYS` | Long | &#x2716; |
| `12` | Medbay: Inspect Sample | `INSPECT_SAMPLE` | Long | &#x2716; |
| `13` | Boiler Room: Replace Water Jug | `REPLACE_WATER_JUG` | Long | &#x2716; |
| `14` | Outside: Fix Weather Node Node_GI | `ACTIVATE_WEATHER_NODES` | Long | &#x2716; |
| `15` | Outside: Fix Weather Node Node_IRO | `ACTIVATE_WEATHER_NODES` | Long | &#x2716; |
| `16` | Outside: Fix Weather Node Node_PD | `ACTIVATE_WEATHER_NODES` | Long | &#x2716; |
| `17` | Outside: Fix Weather Node Node_TB | `ACTIVATE_WEATHER_NODES` | Long | &#x2716; |
| `18` | Communications: Reboot WiFi | `REBOOT_WIFI` | Long | &#x2716; |
| `19` | O2: Monitor Tree | `MONITOR_O2` | Short | &#x2716; |
| `20` | Specimen Room: Unlock Manifolds | `UNLOCK_MANIFOLDS` | Short | &#x2716; |
| `21` | Specimen Room: Store Artifacts | `STORE_ARTIFACTS` | Short | &#x2716; |
| `22` | O2: Fill Canisters | `FILL_CANISTERS` | Short | &#x2716; |
| `23` | O2: Empty Garbage | `EMPTY_GARBAGE` | Short | &#x2716; |
| `24` | Dropship: Chart Course | `CHART_COURSE` | Short | &#x2716; |
| `25` | Medbay: Submit Scan | `SUBMIT_SAN` | Short | &#x2714; |
| `26` | Weapons: Clear Asteroids | `CLEAR_ASTEROIDS` | Short | &#x2714; |
| `27` | Outside: Fix Weather Node Node_CA | `ACTIVATE_WEATHER_NODES` | Long | &#x2716; |
| `28` | Outside: Fix Weather Node Node_MLG | `ACTIVATE_WEATHER_NODES` | Long | &#x2716; |
| `29` | Laboratory: Align Telescope | `ALIGN_TELESCOPE` | Short | &#x2716; |
| `30` | Laboratory: Repair Drill | `REPAIR_DRILL` | Short | &#x2716; |
| `31` | Laboratory: Record Temperature | `RECORD_TEMPERATURE` | Short | &#x2716; |
| `32` | Outside: Record Temperature | `RECORD_TEMPERATURE` | Short | &#x2716; |

---

> Previous section: [Reading the Client Version](03_reading_the_client_version.md)
