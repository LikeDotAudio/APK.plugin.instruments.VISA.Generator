# Sources — 33220A.komand

Every change to this table that a vendor manual confirms, with where the manual says it (AUDIO.komand `check-tables --strict` research, 2026-10-31). A finding no manual confirmed is listed under *Not confirmed* with what was searched, and the table is left as it was.

## Agilent 33220A 20 MHz Function/Arbitrary Waveform Generator User's Guide (33220-90002)

Edition 4, May 2007, Chapter 3 Amplitude Modulation (AM) — <https://ite.unison.mx/wp-content/uploads/2020/09/33220_Manual.pdf>

| Command | Change | Manual |
|---|---|---|
| `rig/Setup_AM` | arg = `{"kind": "multi", "parameters": {"shape": {"kind": "enum", "values": ["SIN", "SQU", "RAMP", "NRAM", "TRI", "NOIS", "USER"], "default": "SIN"}, "freq": {"kind": "numeric", "unit": "Hz", "min": 0.002, "max": 20000}, "depth": {"kind": "numeric", "unit": "%", "min": 0, "max": 120}}}` | AM:INTernal:FUNCtion and AM:INTernal:FREQuency p. 76; AM:DEPTh p. 77 — shape {SINusoid|SQUare|RAMP|NRAMp|TRIangle|NOISe|USER}; modulating frequency (internal) 2 mHz to 20 kHz, default 100 Hz; depth 0% to 120%, default 100% |

## The bench — 33220A certificate, 2026-11-05

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

The tree: `33220A.scpi.json`, read off Agilent 33220A User's Guide 33220-90002 Ed. 4 (May 2007), Chapter 4 Remote Interface Reference, SCPI Command Summary pp. 155-169. Each entry's `notes` / `retired_because` carries the full reason and page; the 33220A's Certify of 2026-11-11 (199 tries) and the GUI-certificate book are the bench evidence. Nothing was sent to verify.

| Command | Change | Was |
|---|---|---|
| `set/Set_Beeper_State` | scpi → `SYSTem:BEEPer:STATe <value>` | was `:BEEPer:STATe <value>` |
| `set/Set_Deviation_Dcycle` | scpi → `PWM:DEViation:DCYCle <value>` | was `DEViation:DCYCle <value>` |
| `set/Set_Questionable_Enable` | scpi → `STATus:QUEStionable:ENABle <value>` | was `:QUEStionable:ENABle <value>` |
| `set/Set_Secure_State` | scpi → `CALibration:SECure:STATe <value>` | was `:SECure:STATe <value>` |
| `do/Do_Secure_Code` | scpi → `CALibration:SECure:CODE` | was `:SECure:CODE` |
| `nab/Get_Attribute_Average` | scpi → `DATA:ATTRibute:AVERage?` | was `:ATTRibute:AVERage?` |
| `nab/Get_Attribute_Cfactor` | scpi → `DATA:ATTRibute:CFACtor?` | was `:ATTRibute:CFACtor?` |
| `nab/Get_Attribute_Points` | scpi → `DATA:ATTRibute:POINts?` | was `:ATTRibute:POINts?` |
| `nab/Get_Attribute_Ptpeak` | scpi → `DATA:ATTRibute:PTPeak?` | was `:ATTRibute:PTPeak?` |
| `nab/Get_Beeper_State` | scpi → `SYSTem:BEEPer:STATe?` | was `:BEEPer:STATe?` |
| `nab/Get_Deviation_Dcycle` | scpi → `PWM:DEViation:DCYCle?` | was `:DEV:DCYC?` |
| `nab/Get_Questionable_Condition` | scpi → `STATus:QUEStionable:CONDition?` | was `:QUEStionable:CONDition?` |
| `nab/Get_Questionable_Enable` | scpi → `STATus:QUEStionable:ENABle?` | was `:QUEStionable:ENABle?` |
| `nab/Get_Questionable_Event` | scpi → `STATus:QUEStionable:EVENt?` | was `:QUEStionable:EVENt?` |
| `nab/Get_Secure_State` | scpi → `CALibration:SECure:STATe?` | was `:SECure:STATe?` |
| `nab/Get_Square_Dcycle` | scpi → `FUNCtion:SQUare:DCYCle?` | was `SQUare:DCYCle?` |
| `do/Do_Text_Clear` | scpi → `DISPlay:TEXT:CLEar` | was `:TEXT:CLEar` |
| `do/Do_Gate_Polarity` | retired — Was `GATE:POLarity`: the table generator cut the `BURSt` parent off, so the unit heard a root `GATE` it does not have (-113 "Undefined header"). Full path from 33220-90002 Ch. 4 SCPI Command Summary (scpi_paths.py, 2026-11-11). Retired as a `do`: the manual gives this node only with a value (BURSt:GATE:POLarity {NORMal\|INVerted}), so a bare send is -109 "Missing parameter"; the set/nab of the same node stay. | was `GATE:POLarity` |
| `do/Do_Internal_Period` | retired — Was `INTernal:PERiod`: the table generator cut the `BURSt` parent off, so the unit heard a root `INTernal` it does not have (-113 "Undefined header"). Full path from 33220-90002 Ch. 4 SCPI Command Summary (scpi_paths.py, 2026-11-11). Retired as a `do`: the manual gives this node only with a value (BURSt:INTernal:PERiod {<seconds>\|MINimum\|MAXimum}), so a bare send is -109 "Missing parameter"; the set/nab of the same node stay. | was `INTernal:PERiod` |
| `do/Do_Unlock_Error_State` | retired — Was `UNLock:ERRor:STATe`: the table generator cut the `PHASe` parent off, so the unit heard a root `UNLock` it does not have (-113 "Undefined header"). Full path from 33220-90002 Ch. 4 SCPI Command Summary (scpi_paths.py, 2026-11-11). Retired as a `do`: the manual gives this node only with a value (PHASe:UNLock:ERRor:STATe {OFF\|ON}), so a bare send is -109 "Missing parameter"; the set/nab of the same node stay. | was `UNLock:ERRor:STATe` |
| `rig/Setup_AM` | scpi → `AM:INTernal:FUNCtion <shape>;:AM:INTernal:FREQuency <freq>;:AM:DEPTh <depth>` | was `AM:INTernal:FUNCtion <shape>;AM:INTernal:FREQuency <freq>;AM:DEPTh <depth>` |
| `set/Set_Unit_Angle` | arg = `{"kind": "enum", "values": ["DEG", "RAD"], "default": "DEG"}` |  |
| `set/Set_Pwm_Internal_Frequency` | arg = `{"kind": "numeric", "unit": "Hz", "min": 0.002, "max": 20000, "default": 10, "limits": "query"}` |  |
| `set/Set_Pwm_Deviation` | arg = `{"kind": "numeric", "unit": "s", "min": 0, "default": 1e-05, "limits": "query", "before": ["FUNCtion PULSe"], "limits_depend_on": ["FUNCtion:PULSe:WIDTh", "FUNCtion:PULSe:PERiod", "FUNCtion:PULSe:TRANsition"]}` |  |
| `set/Set_Pwm_Deviation_Dcycle` | arg = `{"kind": "numeric", "unit": "%", "limits": "query", "before": ["FUNCtion PULSe"], "limits_depend_on": ["FUNCtion:PULSe:DCYCle", "FUNCtion:PULSe:PERiod", "FUNCtion:PULSe:TRANsition"]}` |  |
| `set/Set_Pwm_State` | arg = `{"kind": "bool", "values": ["OFF", "ON"], "before": ["FUNCtion PULSe"]}` |  |
| `set/Set_State_Questionable_Enable` | arg = `{"kind": "integer", "min": 0, "max": 32767, "limits": "query"}` |  |
| `set/Set_Questionable_Enable` | arg = `{"kind": "integer", "min": 0, "max": 32767, "limits": "query"}` | was `:QUEStionable:ENABle <value>` |

### Return formats and argument kinds (same audit, 2026-11-11)

| Command | Change |
|---|---|
| `nab/Get_Data_Attribute_Average`, `nab/Get_Attribute_Average` | returns NR3, no unit (was NR1 dB) — -1…+1 average, p. 244; the unit answered +6.7156300000000E-01 |
| `nab/Get_Data_Attribute_Cfactor`, `…_Ptpeak` and their aliases | returns NR3, no unit (was dB) — a ratio and 0…+1.0 |
| `nab/Get_Function_Pulse_Hold` | returns CRD WIDT\|DCYC (was NR3), p. 193; the unit answered WIDT |
| `set/Set_Pwm_Deviation_Dcycle` | state-dependent upper bound recorded (`before`, `limits_depend_on`); -222 clipped to the UPPER limit at the queried MAX 49.999999 |
