# Sources — 33210A.komand

Every change to this table that a vendor manual confirms, with where the manual says it (AUDIO.komand `check-tables --strict` research, 2026-10-31). A finding no manual confirmed is listed under *Not confirmed* with what was searched, and the table is left as it was.

## Agilent 33210A 10 MHz Function/Arbitrary Waveform Generator User's Guide (33210-90001)

Edition 1, August 2008, Chapter 3 Amplitude Modulation (AM) — <https://engineering.purdue.edu/~dionysis/EE452/Lab3/Lab3_Supporting_Materials/33210A_Function_Generator_Users_Guide.pdf>

| Command | Change | Manual |
|---|---|---|
| `rig/Setup_AM` | arg = `{"kind": "multi", "parameters": {"shape": {"kind": "enum", "values": ["SIN", "SQU", "RAMP", "NRAM", "TRI", "NOIS", "USER"], "default": "SIN"}, "freq": {"kind": "numeric", "unit": "Hz", "min": 0.002, "max": 20000}, "depth": {"kind": "numeric", "unit": "%", "min": 0, "max": 120}}}` | AM:INTernal:FUNCtion and AM:INTernal:FREQuency pp. 74-75; AM:DEPTh p. 75 — shape {SINusoid|SQUare|RAMP|NRAMp|TRIangle|NOISe|USER}; modulating frequency (internal) 2 mHz to 20 kHz, default 100 Hz; depth 0% to 120%, default 100% |

## The bench — 33210A Certify, 2026-11-06

What the 33210A itself answered (MY48000299, `TCPIP0::44.44.44.172::5025::SOCKET`), from the instrument
page's per-command Certify, each re-asked alone with a plain Send and the error queue read after.

| Command | Change | Evidence |
|---|---|---|
| `nab/Get_Attribute_{Average,Cfactor,Points,Ptpeak}` (`:ATTRibute:*?`) | removed | `-113,"Undefined header"`; scraper truncations of `DATA:ATTRibute:*`, which stay and pass |
| `set/Set_Beeper_State`, `nab/Get_Beeper_State` (`:BEEPer:STATe`) | removed | `-113`; the real `SYSTem:BEEPer:STATe?` → `1` stays (`Get_System_Beeper_State`) |
| `nab/Get_Deviation_Dcycle` (`:DEV:DCYC?`), `set/Set_Deviation_Dcycle` (`DEV:DCYC <value>`) | removed | `-113`; the real `PWM:DEViation:DCYCle?` → `+2.0E+00` stays (`Get_Pwm_Deviation_Dcycle`) |
| `FSKey:*` (4 set, 4 nab) | removed | `-113` for every query: the 33210A has no FSK (the 33220A does) |
| `nab/Get_Data_Attribute_Average` | returns `NR3` (was `NR1`, `dB`) | `DATA:ATTRibute:AVERage?` → `+6.7156300000000E-01` |
| `nab/Get_Data_Attribute_{Cfactor,Points,Ptpeak}` | no `dB` unit | statistics of the arb's normalised points, not levels |
| `nab/Get_Function_Pulse_Hold` | returns `CRD` WIDT\|DCYC (was `NR3`) | `FUNCtion:PULSe:HOLD?` → `WIDT` |
| `PM:*` (4 set, 2 do, 4 nab) | removed | `-113` for every query: the 33210A has no phase modulation |
| `:QUEStionable:*` (1 set, 3 nab) | removed | `-113`; truncations of `STATus:QUEStionable:*`, which stay and pass |
| `:SECure:*` (`Set_Secure_State`, `Do_Secure_Code`, `Get_Secure_State`) | removed | `-113`; truncations of `CAL:SECure:*`, which stay |
| `nab/Get_Square_Dcycle` (`SQUare:DCYCle?`) | removed | `-113`; the real `FUNCtion:SQUare:DCYCle?` → `+5.0E+01` stays |

Asked with the link in step: each phantom answered `-113` and the next `*IDN?` came back as itself.
(A first pass at these read answers one or two questions late — see ROAD-3610 — and was thrown away.)

`OUTPut:TRIGger?` answers `0` and is kept: its Certify timeout was the certifier's own 8 s limit, since raised above the agent's deadline.

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

## SCPI paths — every header against the model's own tree (scpi_paths.py, 2026-11-11)

The tree: `33210A.scpi.json`, read off Agilent 33210A User's Guide 33210-90002, Chapter 4 SCPI Command Summary (the 33220A's tree without PM and FSKey, which the 33210A answers -113 to on the bench, 2026-11-07). Each entry's `notes` / `retired_because` carries the full reason and page; the 33220A's Certify of 2026-11-11 (199 tries) and the GUI-certificate book are the bench evidence. Nothing was sent to verify.

| Command | Change | Was |
|---|---|---|
| `do/Do_Text_Clear` | scpi → `DISPlay:TEXT:CLEar` | was `:TEXT:CLEar` |
| `do/Do_Gate_Polarity` | retired — Was `GATE:POLarity`: the table generator cut the `BURSt` parent off, so the unit heard a root `GATE` it does not have (-113 "Undefined header"). Full path from the 33210A/33220A SCPI Command Summary (33220-90002 Ch. 4) (scpi_paths.py, 2026-11-11). Retired as a `do`: the manual gives this node only with a value (BURSt:GATE:POLarity {NORMal\|INVerted}), so a bare send is -109 "Missing parameter"; the set/nab of the same node stay. | was `GATE:POLarity` |
| `do/Do_Internal_Period` | retired — Was `INTernal:PERiod`: the table generator cut the `BURSt` parent off, so the unit heard a root `INTernal` it does not have (-113 "Undefined header"). Full path from the 33210A/33220A SCPI Command Summary (33220-90002 Ch. 4) (scpi_paths.py, 2026-11-11). Retired as a `do`: the manual gives this node only with a value (BURSt:INTernal:PERiod {<seconds>\|MINimum\|MAXimum}), so a bare send is -109 "Missing parameter"; the set/nab of the same node stay. | was `INTernal:PERiod` |
| `do/Do_Unlock_Error_State` | retired — Was `UNLock:ERRor:STATe`: the table generator cut the `PHASe` parent off, so the unit heard a root `UNLock` it does not have (-113 "Undefined header"). Full path from the 33210A/33220A SCPI Command Summary (33220-90002 Ch. 4) (scpi_paths.py, 2026-11-11). Retired as a `do`: the manual gives this node only with a value (PHASe:UNLock:ERRor:STATe {OFF\|ON}), so a bare send is -109 "Missing parameter"; the set/nab of the same node stay. | was `UNLock:ERRor:STATe` |
| `rig/Setup_AM` | scpi → `AM:INTernal:FUNCtion <shape>;:AM:INTernal:FREQuency <freq>;:AM:DEPTh <depth>` | was `AM:INTernal:FUNCtion <shape>;AM:INTernal:FREQuency <freq>;AM:DEPTh <depth>` |
| `set/Set_Unit_Angle` | arg = `{"kind": "enum", "values": ["DEG", "RAD"], "default": "DEG"}` |  |
| `set/Set_Pwm_Internal_Frequency` | arg = `{"kind": "numeric", "unit": "Hz", "min": 0.002, "max": 20000, "default": 10, "limits": "query"}` |  |
| `set/Set_Pwm_Deviation` | arg = `{"kind": "numeric", "unit": "s", "min": 0, "default": 1e-05, "limits": "query", "before": ["FUNCtion PULSe"], "limits_depend_on": ["FUNCtion:PULSe:WIDTh", "FUNCtion:PULSe:PERiod", "FUNCtion:PULSe:TRANsition"]}` |  |
| `set/Set_Pwm_Deviation_Dcycle` | arg = `{"kind": "numeric", "unit": "%", "limits": "query", "before": ["FUNCtion PULSe"], "limits_depend_on": ["FUNCtion:PULSe:DCYCle", "FUNCtion:PULSe:PERiod", "FUNCtion:PULSe:TRANsition"]}` |  |
| `set/Set_Pwm_State` | arg = `{"kind": "bool", "values": ["OFF", "ON"], "before": ["FUNCtion PULSe"]}` |  |
| `set/Set_State_Questionable_Enable` | arg = `{"kind": "integer", "min": 0, "max": 32767, "limits": "query"}` |  |
