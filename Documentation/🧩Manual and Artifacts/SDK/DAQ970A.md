# DAQ970A — DAQ

← [SDK](../SDK.md)

**HP / Agilent / Keysight** — Data Acq System (Next Gen)

| | |
|---|---|
| Channels |  |
| HTTP | `:16003/api/instrument/DAQ/DAQ970A` |
| `spec` | `/api/instrument/DAQ/DAQ970A/DAQ970A.api.json` |
| `health` | `/api/instrument/DAQ/DAQ970A/health` |
| `get` | `/api/instrument/DAQ/DAQ970A/get/<command>` |
| `set` | `/api/instrument/DAQ/DAQ970A/set/<command>` |
| `nab` | `/api/instrument/DAQ/DAQ970A/nab/<command>` |
| `rig` | `/api/instrument/DAQ/DAQ970A/rig/<command>` |
| `do` | `/api/instrument/DAQ/DAQ970A/do/<command>` |
| socket `ws` | `/ws/instrument/DAQ/DAQ970A` |
| socket `readings` | `/ws/instrument/DAQ/DAQ970A/readings` |
| socket `unix` | `/run/apk/instruments/DAQ.DAQ970A.sock` |

## `get` — reads one value (7)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Read_IDN` | `*IDN?` |  | IEEE 488.2 Common |  |
| `Query_Scan_Size` | `:DATA:POINts?` |  | Memory System |  |
| `Fetch_Scan` | `:FETCh?` |  | Data Acquisition |  |
| `Read_Next` | `:READ?` |  | Data Acquisition |  |
| `Read_Monitor_Data` | `:ROUTe:MONItor:DATA?` |  | Channel Monitor |  |
| `Read_Scan_List` | `:ROUTe:SCAN?` |  | Route Configuration |  |
| `Query_Error` | `:SYSTem:ERRor?` |  | System Utilities |  |

## `set` — writes one value (8)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Set_Channel_Delay` | `:ROUTe:CHANnel:DELay <seconds>, (@<channels>)` | none | Scan Timing |  |
| `Set_Monitor_Channel` | `:ROUTe:MONItor (@<channel>)` | none | Channel Monitor |  |
| `Set_Monitor_State` | `:ROUTe:MONItor:STATe <state>` | OFF · ON | Channel Monitor |  |
| `Set_Scan_List` | `:ROUTe:SCAN (@<channels>)` | string | Route Configuration |  |
| `Set_Scan_Interval` | `:ROUTe:SCAN:TIMer <seconds>` | numeric | Scan Timing |  |
| `Set_Integration_NPLC` | `:SENSe:VOLTage:DC:NPLC <nplc>, (@<channels>)` | none | Measurement Parameters |  |
| `Set_Trigger_Count` | `:TRIGger:COUNt <count>` | numeric | Trigger Setup |  |
| `Set_Trigger_Source` | `:TRIGger:SOURce <source>` | IMMediate · TIMer · EXTernal · BUS · ALARm1 · ALARm2 | Trigger Setup |  |

## `nab` — reads more than one thing (observation, telemetry) (7)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Read_IDN` | `*IDN?` |  | IEEE 488.2 Common |  |
| `Query_Scan_Size` | `:DATA:POINts?` |  | Memory System |  |
| `Fetch_Scan` | `:FETCh?` |  | Data Acquisition |  |
| `Read_Next` | `:READ?` |  | Data Acquisition |  |
| `Read_Monitor_Data` | `:ROUTe:MONItor:DATA?` |  | Channel Monitor |  |
| `Read_Scan_List` | `:ROUTe:SCAN?` |  | Route Configuration |  |
| `Query_Error` | `:SYSTem:ERRor?` |  | System Utilities |  |

## `rig` — configures several arguments at once (2)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Configure_Temperature_Scan` | `:CONFigure:TEMPerature <type>, <transducer>, (@<channels>)` | none | Measurement Configuration |  |
| `Configure_Voltage_Scan` | `:CONFigure:VOLTage:DC <range>, <resolution>, (@<channels>)` | none | Measurement Configuration |  |

## `do` — executes an action; takes no value (6)

| Command | SCPI | Argument | Group | |
|---|---|---|---|---|
| `Clear_Status` | `*CLS` |  | IEEE 488.2 Common |  |
| `Reset` | `*RST` |  | IEEE 488.2 Common |  |
| `Abort` | `:ABORt` |  | Trigger System |  |
| `Clear_Memory` | `:DATA:CLEar` |  | Memory System |  |
| `Start_Scan` | `:INITiate` |  | Trigger System |  |
| `Open_All` | `:ROUTe:OPEN:ALL` |  | Route Configuration |  |
