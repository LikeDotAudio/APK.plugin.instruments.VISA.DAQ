# SDK — INSTRUMENT.DAQ

Every DAQ model this library drives, and how to drive it. Each model answers the same five verbs over HTTP (its own port), WebSocket, a Unix socket and the bus; one page per model below lists its routes and every command.

← [Manual and Artifacts](INDEX.md)

| Verb | What it does |
|---|---|
| `get` | reads one value |
| `set` | writes one value |
| `nab` | reads more than one thing (observation, telemetry) |
| `rig` | configures several arguments at once |
| `do` | executes an action; takes no value |

| Model | Maker | get | set | nab | rig | do | Port |
|---|---|---:|---:|---:|---:|---:|---:|
| [34970A](SDK/34970A.md) | HP / Agilent / Keysight | 7 | 8 | 7 | 2 | 6 | 16000 |
| [34972A](SDK/34972A.md) | HP / Agilent / Keysight | 7 | 8 | 7 | 2 | 6 | 16001 |
| [34980A](SDK/34980A.md) | HP / Agilent / Keysight | 7 | 8 | 7 | 2 | 6 | 16002 |
| [DAQ970A](SDK/DAQ970A.md) | HP / Agilent / Keysight | 7 | 8 | 7 | 2 | 6 | 16003 |
