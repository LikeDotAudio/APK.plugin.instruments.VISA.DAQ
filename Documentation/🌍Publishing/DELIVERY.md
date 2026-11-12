# Delivery — INSTRUMENT.DAQ

← [Publishing](INDEX.md)

A submodule of [APK.plugin.instruments.VISA](https://github.com/LikeDotAudio/APK.plugin.instruments.VISA) at `INSTRUMENT.DAQ/`, origin `https://github.com/LikeDotAudio/APK.plugin.instruments.VISA.DAQ.git`. It ships inside every image that bakes `INSTRUMENTS`; after a change here, regenerate (`python3 _komand/generate_device_apis.py`, `python3 _komand/family_sdk_docs.py` in the parent), commit here, bump the parent's pointer, and rebuild NODE.BareMetal, DISCOVERY.Engine and WEB.OsApi.

## Delivered 2026-11-11 – 2026-11-12

From this repository's own commits (the commit message is the record):

- docs: SDK pages regenerated (ROAD-3683) (`a5c5119`)
- wiki: lanes, README and smoke result refreshed (wiki.py + smoke.py) (`e53d270`)

## Releases
- **Released `2.0.0`, tag `v2.0.0`** (2026-11-05, ROAD-3452, the owner's V2) — no SDK pin; every manifest says 2.0.0; GitHub release `v2.0.0`.
