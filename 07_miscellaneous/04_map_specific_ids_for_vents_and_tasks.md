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

| ID | Description |
| --- | --- |
| `0` | Admin: Swipe Card |
| `1` | Electrical: Fix Wiring |
| `2` | Weapons: Clear Asteroids |
| `3` | Engines: Align Engine Output |
| `4` | Medbay: Submit Scan |
| `5` | Medbay: Inspect Sample |
| `6` | Storage: Fuel Engines |
| `7` | Reactor: Start Reactor |
| `8` | O2: Empty Chute |
| `9` | Cafeteria: Empty Garbage |
| `10` | Communications: Download Data |
| `11` | Electrical: Calibrate Distributor |
| `12` | Navigation: Chart Course |
| `13` | O2: Clean O2 Filter |
| `14` | Reactor: Unlock Manifolds |
| `15` | Electrical: Download Data |
| `16` | Navigation: Stabilize Steering |
| `17` | Weapons: Download Data |
| `18` | Shields: Prime Shields |
| `19` | Cafeteria: Download Data |
| `20` | Navigation: Download Data |
| `21` | Electrical: Divert Power to Shields |
| `22` | Electrical: Divert Power to Weapons |
| `23` | Electrical: Divert Power to Communications |
| `24` | Electrical: Divert Power to Upper Engine |
| `25` | Electrical: Divert Power to O2 |
| `26` | Electrical: Divert Power to Navigation |
| `27` | Electrical: Divert Power to Lower Engine |
| `28` | Electrical: Divert Power to Security |

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

| ID | Description |
| --- | --- |
| `0` | Hallway: Fix Wiring |
| `1` | Admin: Enter ID Code |
| `2` | Medbay: Submit Scan |
| `3` | Balcony: Clear Asteroids |
| `4` | Electrical: Divert Power to Admin |
| `5` | Electrical: Divert Power to Cafeteria |
| `6` | Electrical: Divert Power to Communications |
| `7` | Electrical: Divert Power to Launchpad |
| `8` | Electrical: Divert Power to Medbay |
| `9` | Electrical: Divert Power to Office |
| `10` | Storage: Water Plants |
| `11` | Reactor: Start Reactor |
| `12` | Electrical: Divert Power to Greenhouse |
| `13` | Admin: Chart Course |
| `14` | Greenhouse: Clean O2 Filter |
| `15` | Launchpad: Fuel Engines |
| `16` | Laboratory: Assemble Artifact |
| `17` | Laboratory: Sort Samples |
| `18` | Admin: Prime Shields |
| `19` | Cafeteria: Empty Garbage |
| `20` | Balcony: Measure Weather |
| `21` | Electrical: Divert Power to Laboratory |
| `22` | Cafeteria: Buy Beverage |
| `23` | Office: Process Data |
| `24` | Launchpad: Run Diagnostics |
| `25` | Reactor: Unlock Manifolds |

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

| ID | Description |
| --- | --- |
| `0` | Office: Swipe Card |
| `1` | Dropship: Insert Keys |
| `2` | Office: Scan Boarding Pass |
| `3` | Electrical: Fix Wiring |
| `4` | Weapons: Download Data |
| `5` | Office: Download Data |
| `6` | Electrical: Download Data |
| `7` | Specimen Room: Download Data |
| `8` | O2: Download Data |
| `9` | Specimen Room: Start Reactor |
| `10` | Storage: Fuel Engines |
| `11` | Boiler Room: Open Waterways |
| `12` | Medbay: Inspect Sample |
| `13` | Boiler Room: Replace Water Jug |
| `14` | Outside: Fix Weather Node Node_GI |
| `15` | Outside: Fix Weather Node Node_IRO |
| `16` | Outside: Fix Weather Node Node_PD |
| `17` | Outside: Fix Weather Node Node_TB |
| `18` | Communications: Reboot WiFi |
| `19` | O2: Monitor Tree |
| `20` | Specimen Room: Unlock Manifolds |
| `21` | Specimen Room: Store Artifacts |
| `22` | O2: Fill Canisters |
| `23` | O2: Empty Garbage |
| `24` | Dropship: Chart Course |
| `25` | Medbay: Submit Scan |
| `26` | Weapons: Clear Asteroids |
| `27` | Outside: Fix Weather Node Node_CA |
| `28` | Outside: Fix Weather Node Node_MLG |
| `29` | Laboratory: Align Telescope |
| `30` | Laboratory: Repair Drill |
| `31` | Laboratory: Record Temperature |
| `32` | Outside: Record Temperature |

---

> Previous section: [Reading the Client Version](03_reading_the_client_version.md)
