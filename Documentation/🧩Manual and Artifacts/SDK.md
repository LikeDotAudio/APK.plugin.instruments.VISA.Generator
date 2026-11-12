# SDK — INSTRUMENT.Generator

Every Generator model this library drives, and how to drive it. Each model answers the same five verbs over HTTP (its own port), WebSocket, a Unix socket and the bus; one page per model below lists its routes and every command.

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
| [33120A](SDK/33120A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15300 |
| [33210A](SDK/33210A.md) | HP / Agilent / Keysight | 83 | 118 | 92 | 5 | 47 | 15301 |
| [33220A](SDK/33220A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15302 |
| [33250A](SDK/33250A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15303 |
| [33509B](SDK/33509B.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15304 |
| [33510B](SDK/33510B.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15305 |
| [33511B](SDK/33511B.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15306 |
| [33512B](SDK/33512B.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15307 |
| [33519B](SDK/33519B.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15308 |
| [33520B](SDK/33520B.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15309 |
| [33521B](SDK/33521B.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15310 |
| [33522B](SDK/33522B.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15311 |
| [33611A](SDK/33611A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15312 |
| [33612A](SDK/33612A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15313 |
| [33619A](SDK/33619A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15314 |
| [33620A](SDK/33620A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15315 |
| [33621A](SDK/33621A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15316 |
| [33622A](SDK/33622A.md) | HP / Agilent / Keysight | 107 | 142 | 112 | 4 | 50 | 15317 |
| [AFG1022](SDK/AFG1022.md) | Tektronix | 107 | 142 | 112 | 4 | 50 | 15318 |
| [AFG31000](SDK/AFG31000.md) | Tektronix | 107 | 142 | 112 | 4 | 50 | 15319 |
| [AFG3102](SDK/AFG3102.md) | Tektronix | 107 | 142 | 112 | 4 | 50 | 15320 |
| [DG1022Z](SDK/DG1022Z.md) | Rigol | 107 | 142 | 112 | 4 | 50 | 15321 |
| [DG4102](SDK/DG4102.md) | Rigol | 107 | 142 | 112 | 4 | 50 | 15322 |
| [DG812](SDK/DG812.md) | Rigol | 107 | 142 | 112 | 4 | 50 | 15323 |
