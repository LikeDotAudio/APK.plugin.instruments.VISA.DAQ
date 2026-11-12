# DAQ970A — DAQ

← [SDK](../SDK.md)

**HP / Agilent / Keysight** — Data Acq System (Next Gen)

| | |
|---|---|
| Family | `DAQ` |
| Channels |  |
| Spec | `GET /api/instrument/DAQ/DAQ970A` |
| Default transport | `raw_socket` |

<!-- sdk:io -->
## Inputs and outputs — the box

From the BIM part [`keysight/daq970a`](/api/bim/parts?full=1&id=keysight/daq970a) — DAQ970A user's guide / datasheet, front and rear panel — declared, not measured. Size is rack (W×H×D); power is the 75 VA max. GPIB is DAQ973A only.

### Inputs

| Terminal | Connector | Domain | Count | Signal |
|---|---|---|---:|---|
| SLOTS 100, 200, 300 | MODULE-SLOT | signal | 3 | plug-in module slot (e.g. DAQM901A 20-channel multiplexer) |

### Connections (control and network)

| Terminal | Connector | Domain | Count | Signal |
|---|---|---|---:|---|
| EXT TRIG / ALARMS |  | control | 1 | Ext Trig input, 4 TTL alarm outputs, Channel Advance input, Channel Closed output — one rear connector |
| LAN | RJ45 | network | 1 | Gigabit LAN, web interface |
| USB |  | control | 1 | rear-panel USB 2.0 interface |
| USB MEMORY | USB-A | usb | 1 | front-panel USB port — log / copy data to a flash drive |
| CHASSIS GROUND | SCREW-TERMINAL | power | 1 | chassis ground screw |

**Power:** MAINS IN (IEC-INLET)

<!-- /sdk:io -->

## Driving it

Three doors, all on the bench's own services — none of them is a per-model process.

1. **The bus, through KOMAND** (what a panel and the touch pad do). Teach the topic its handler, then send the value; never retained — KOMAND ignores a retained value on purpose. `target` is the box's Write topic (`GET /api/instrument/status?protocol=visa&resource=…` → `write_topic`); a DO/NAB fires on a truthy value.

```sh
T=APK.audio/Gui/MyPanel/Set_Channel_Delay
mosquitto_pub -t "$T/config" -m '{"komand_handler": {"enable": true, "komand_type": "set", "command": "Set_Channel_Delay", "model": "DAQ970A", "input_name": "seconds", "target": "<box>/Write"}}'
mosquitto_pub -t "$T" -m '{"value": <value>}'
```

2. **Raw SCPI** — `POST /api/instrument/send` with `{"protocol": "visa", "resource": "<VISA resource>", "command": "<SCPI>"}`; the answer comes back in the reply and on `<box>/Read`.

3. **The spec, over HTTP** — `GET /api/instrument/DAQ/DAQ970A` (this model's whole `api.json`), `GET /api/instrument/DAQ/DAQ970A/<verb>/<command>` (one command's entry), `GET …/health`. These describe; they do not send anything to the box.

A read's answer is published on `<box>/Reading/<command>` (the **Out** column below); `<box>` is `APK.audio/System/Protocols/visa/Device/<Family>/<Model>/<Dev…>`.

## Commands (30) — inputs and outputs of the API

**In** is what the command takes; **Out** is what it gives back and where. Every command arrives on `APK.audio/Gui/Komands/DAQ/<Command>`.

### `get` — reads one value (7)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Read_IDN` | `*IDN?` | — | → `…/Reading/Read_IDN` | IEEE 488.2 Common |  |
| `Query_Scan_Size` | `:DATA:POINts?` | — | → `…/Reading/Query_Scan_Size` | Memory System |  |
| `Fetch_Scan` | `:FETCh?` | — | → `…/Reading/Fetch_Scan` | Data Acquisition |  |
| `Read_Next` | `:READ?` | — | → `…/Reading/Read_Next` | Data Acquisition |  |
| `Read_Monitor_Data` | `:ROUTe:MONItor:DATA?` | — | → `…/Reading/Read_Monitor_Data` | Channel Monitor |  |
| `Read_Scan_List` | `:ROUTe:SCAN?` | — | → `…/Reading/Read_Scan_List` | Route Configuration |  |
| `Query_Error` | `:SYSTem:ERRor?` | — | → `…/Reading/Query_Error` | System Utilities |  |

### `set` — writes one value (8)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Set_Channel_Delay` | `:ROUTe:CHANnel:DELay <seconds>, (@<channels>)` | `seconds`, `channels` | — | Scan Timing |  |
| `Set_Monitor_Channel` | `:ROUTe:MONItor (@<channel>)` | `channel` | — | Channel Monitor |  |
| `Set_Monitor_State` | `:ROUTe:MONItor:STATe <state>` | `state`: `OFF` · `ON` | — | Channel Monitor |  |
| `Set_Scan_List` | `:ROUTe:SCAN (@<channels>)` | `channels`: string | — | Route Configuration |  |
| `Set_Scan_Interval` | `:ROUTe:SCAN:TIMer <seconds>` | `seconds`: numeric 0.0…359999.0 s | — | Scan Timing |  |
| `Set_Integration_NPLC` | `:SENSe:VOLTage:DC:NPLC <nplc>, (@<channels>)` | `nplc`, `channels` | — | Measurement Parameters |  |
| `Set_Trigger_Count` | `:TRIGger:COUNt <count>` | `count`: numeric 1…50000 | — | Trigger Setup |  |
| `Set_Trigger_Source` | `:TRIGger:SOURce <source>` | `source`: `IMMediate` · `TIMer` · `EXTernal` · `BUS` · `ALARm1` · `ALARm2` | — | Trigger Setup |  |

### `nab` — reads more than one thing (observation, telemetry) (7)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Read_IDN` | `*IDN?` | — | → `…/Reading/Read_IDN` | IEEE 488.2 Common |  |
| `Query_Scan_Size` | `:DATA:POINts?` | — | → `…/Reading/Query_Scan_Size` | Memory System |  |
| `Fetch_Scan` | `:FETCh?` | — | → `…/Reading/Fetch_Scan` | Data Acquisition |  |
| `Read_Next` | `:READ?` | — | → `…/Reading/Read_Next` | Data Acquisition |  |
| `Read_Monitor_Data` | `:ROUTe:MONItor:DATA?` | — | → `…/Reading/Read_Monitor_Data` | Channel Monitor |  |
| `Read_Scan_List` | `:ROUTe:SCAN?` | — | → `…/Reading/Read_Scan_List` | Route Configuration |  |
| `Query_Error` | `:SYSTem:ERRor?` | — | → `…/Reading/Query_Error` | System Utilities |  |

### `rig` — configures several arguments at once (2)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Configure_Temperature_Scan` | `:CONFigure:TEMPerature <type>, <transducer>, (@<channels>)` | `type`, `transducer`, `channels` | — | Measurement Configuration |  |
| `Configure_Voltage_Scan` | `:CONFigure:VOLTage:DC <range>, <resolution>, (@<channels>)` | `range`, `resolution`, `channels` | — | Measurement Configuration |  |

### `do` — executes an action; takes no value (6)

| Command | SCPI | In | Out | Group | |
|---|---|---|---|---|---|
| `Clear_Status` | `*CLS` | — | — | IEEE 488.2 Common |  |
| `Reset` | `*RST` | — | — | IEEE 488.2 Common |  |
| `Abort` | `:ABORt` | — | — | Trigger System |  |
| `Clear_Memory` | `:DATA:CLEar` | — | — | Memory System |  |
| `Start_Scan` | `:INITiate` | — | — | Trigger System |  |
| `Open_All` | `:ROUTe:OPEN:ALL` | — | — | Route Configuration |  |
