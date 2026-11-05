# INSTRUMENT.Generator

**Wiki:** [Documentation/README.md](Documentation/README.md) — principles, architecture, delivery, and the [SDK](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK.md).

The **Generator** instruments of the APK.audio bench, as one thing: 24 models, their command tables and the family's panel. Function and arbitrary waveform generators.

| | |
|---|---|
| **Is** | **source** — puts something out — a stimulus, a supply or a load<br>**monitoring** — shows — a trace, a waveform or a display you watch |
| **Inputs** | each model's BIM part: /api/bim/parts?full=1&id=<part> — ports where side is "input" and domain is not "power" |
| **Recipe** | none — data, not a container: read in place by the stacks that bake `INSTRUMENTS` |
| **Source** | this repository (https://github.com/LikeDotAudio/APK.plugin.instruments.VISA.Generator.git), a submodule of [APK.plugin.instruments.VISA](https://github.com/LikeDotAudio/APK.plugin.instruments.VISA) at `INSTRUMENT.Generator/` |
| **Family name** | `Generator` — the device type, the topic segment and the `manifest.json` key; the `INSTRUMENT.` prefix belongs to the folder only |

## Models

| Model | Maker | What | Commands | Table | API |
|---|---|---|---:|:---:|---|
| [33120A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33120A.md) | HP / Agilent / Keysight | 15 MHz Function/Arb (Classic) | 262 |  | :15300 |
| [33210A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33210A.md) | HP / Agilent / Keysight | 10 MHz Function/Arb | 258 | ✅ | :15301 |
| [33220A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33220A.md) | HP / Agilent / Keysight | 20 MHz Function/Arb | 262 | ✅ | :15302 |
| [33250A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33250A.md) | HP / Agilent / Keysight | 80 MHz Function/Arb | 262 |  | :15303 |
| [33509B](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33509B.md) | HP / Agilent / Keysight | 20 MHz 1-Ch Trueform | 262 |  | :15304 |
| [33510B](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33510B.md) | HP / Agilent / Keysight | 20 MHz 2-Ch Trueform | 262 |  | :15305 |
| [33511B](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33511B.md) | HP / Agilent / Keysight | 20 MHz 1-Ch Trueform (with Arbitrary) | 262 |  | :15306 |
| [33512B](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33512B.md) | HP / Agilent / Keysight | 20 MHz 2-Ch Trueform (with Arbitrary) | 262 |  | :15307 |
| [33519B](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33519B.md) | HP / Agilent / Keysight | 30 MHz 1-Ch Trueform (without Arbitrary) | 262 |  | :15308 |
| [33520B](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33520B.md) | HP / Agilent / Keysight | 30 MHz 2-Ch Trueform (without Arbitrary) | 262 |  | :15309 |
| [33521B](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33521B.md) | HP / Agilent / Keysight | 30 MHz 1-Ch Trueform | 262 |  | :15310 |
| [33522B](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33522B.md) | HP / Agilent / Keysight | 30 MHz 2-Ch Trueform | 262 |  | :15311 |
| [33611A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33611A.md) | HP / Agilent / Keysight | 80 MHz 1-Ch Trueform | 262 |  | :15312 |
| [33612A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33612A.md) | HP / Agilent / Keysight | 80 MHz 2-Ch Trueform | 262 |  | :15313 |
| [33619A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33619A.md) | HP / Agilent / Keysight | 80 MHz 1-Ch Trueform (without Arbitrary) | 262 |  | :15314 |
| [33620A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33620A.md) | HP / Agilent / Keysight | 80 MHz 2-Ch Trueform (without Arbitrary) | 262 |  | :15315 |
| [33621A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33621A.md) | HP / Agilent / Keysight | 120 MHz 1-Ch Trueform | 262 |  | :15316 |
| [33622A](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/33622A.md) | HP / Agilent / Keysight | 120 MHz 2-Ch Trueform | 262 |  | :15317 |
| [AFG1022](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/AFG1022.md) | Tektronix | 25 MHz 2 Ch Arbitrary | 262 |  | :15318 |
| [AFG31000](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/AFG31000.md) | Tektronix | Advanced High Perf Arb Gen | 262 |  | :15319 |
| [AFG3102](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/AFG3102.md) | Tektronix | 100 MHz 2 Ch Dual (Classic) | 262 |  | :15320 |
| [DG1022Z](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/DG1022Z.md) | Rigol | 25 MHz 2 Ch Arbitrary | 262 |  | :15321 |
| [DG4102](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/DG4102.md) | Rigol | 100 MHz 2 Ch Arbitrary | 262 |  | :15322 |
| [DG812](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SDK/DG812.md) | Rigol | 10 MHz 1 Ch (Basic) | 262 |  | :15323 |

## Layout

```
INSTRUMENT.Generator/
  thing.json            what this thing is on the bench (authored)
  gui/                  the family panel, stamped once per discovered box
    Generator.cad.json
    Generator.dxf
    Generator.json
    Generator.probe.json
    Generator_N.json
  <Model>/              <Model>.komand (the command table), <Model>.gui,
                        <Model>.api.json (generated), commands_tree.md, SOURCES.md
  Documentation/        the wiki; SDK/ is generated by _komand/family_sdk_docs.py
```

Generated by `_komand/family_sdk_docs.py` in the parent repository; edit `thing.json` or the
models, not this page.

<!-- wiki:smoke -->
**Smoke test** — ❌ FAIL 0/1 since 2026-11-04 20:50 EST — [results](Documentation/%F0%9F%A7%A9Manual%20and%20Artifacts/SMOKE.md)
<!-- /wiki:smoke -->
