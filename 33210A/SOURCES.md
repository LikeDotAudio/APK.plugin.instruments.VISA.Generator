# Sources — 33210A.komand

Every change to this table that a vendor manual confirms, with where the manual says it (AUDIO.komand `check-tables --strict` research, 2026-10-31). A finding no manual confirmed is listed under *Not confirmed* with what was searched, and the table is left as it was.

## Agilent 33210A 10 MHz Function/Arbitrary Waveform Generator User's Guide (33210-90001)

Edition 1, August 2008, Chapter 3 Amplitude Modulation (AM) — <https://engineering.purdue.edu/~dionysis/EE452/Lab3/Lab3_Supporting_Materials/33210A_Function_Generator_Users_Guide.pdf>

| Command | Change | Manual |
|---|---|---|
| `rig/Setup_AM` | arg = `{"kind": "multi", "parameters": {"shape": {"kind": "enum", "values": ["SIN", "SQU", "RAMP", "NRAM", "TRI", "NOIS", "USER"], "default": "SIN"}, "freq": {"kind": "numeric", "unit": "Hz", "min": 0.002, "max": 20000}, "depth": {"kind": "numeric", "unit": "%", "min": 0, "max": 120}}}` | AM:INTernal:FUNCtion and AM:INTernal:FREQuency pp. 74-75; AM:DEPTh p. 75 — shape {SINusoid|SQUare|RAMP|NRAMp|TRIangle|NOISe|USER}; modulating frequency (internal) 2 mHz to 20 kHz, default 100 Hz; depth 0% to 120%, default 100% |

## The bench — 33210A certificate, 2026-11-05

What the unit itself answered (33220A MY44044028, firmware 2.07-2.06-22-2, GUI certificate 2026-11-05 04:24); the 33210A shares the command set.

| Command | Change | Evidence |
|---|---|---|
| `get+nab/Get_Error_Queue` | returns `ERROR` (was `NR2`) | `SYSTem:ERRor?` → `+0,"No error"`: a code and its text |
| `nab/Get_Phase_Unlock_Error_State` | returns `BOOL` (was `ERROR`) | a state, 0 or 1 — not an error-queue answer |
| `:KLOCk:*`, `LAN:*`, `:TELNet:*`, `:NVOLatile:*` (16 get/set/do) | removed | `-113,"Undefined header"` for every query; scraper truncations of `SYSTem:KLOCk`, `SYSTem:COMMunicate:LAN`, `DATA:NVOLatile`, which stay and pass |
| `nab/Get_Memory_State_Name`, `nab/Get_Memory_State_Value` | take `<state>` 0–4 (default 1); VALid? returns `BOOL` | bare query → `-109,"Missing parameter"` |
| `set/Set_Burst_Ncycles` | arg integer, limits from the unit | was `unknown`; the unit answers `BURS:NCYC? MIN\|MAX` |
| `set/Set_Fm_Deviation`, `set/Set_Fm_Internal_Frequency` | arg numeric Hz, limits from the unit | was `unknown` |
| `set/Set_Function_Ramp_Symmetry` | arg numeric %, limits from the unit | was `unknown` |
