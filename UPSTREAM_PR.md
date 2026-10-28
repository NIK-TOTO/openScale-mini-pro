PICOOC Mini Pro advertises as `PICOOC-CQ` and sends a 13-byte `0x39` result. The current handler acknowledges it but rejects it as too short, so the weighing is never saved.

Recognize the layout by its declared length (`0x0D`) and decode weight, impedance, pounds and display unit using the existing scaling and pound mask. This variant has neither phase angle nor a separate completion flag; treat it as a completed result, using the existing disconnect/settle publication path. A truncated 16-byte frame is still rejected. Weight and impedance retain their 0.05 kg / 0.1 ohm protocol resolution, and body composition continues through the existing `StandardImpedanceLib` and `ScaleMeasurement` infrastructure.

Add six regression tests covering both reported packets, fractional resolution, truncation, repeated packets and reconnects, settle fallback, and weight-only readings without impedance. Update the catalog remark for the shared `PICOOC-CQ` name.

## Validation

- 68 selected tests passed (including the six new tests), covering the PICOOC handlers/libraries, `StandardImpedanceLibTest` and `ScaleMeasurementTest`: [successful test/build run](https://github.com/NIK-TOTO/openScale-mini-pro/actions/runs/40773470173).
- Full debug unit-test suite: **1049 passed**, no failures or skipped tests (includes the selected 68 tests above).
- `:app:compileDebugAndroidTestKotlin` and `:app:assembleDebug` succeeded.
- Also verified with a physical PICOOC Mini Pro on a Google Pixel 7 running Android 16.
- `git diff --check` passes.

## Relation to #1565

#1565 is already merged and covers the 10-byte (`0x0A`) PICOOC-CC/S3 format, which ends immediately after impedance. Mini Pro uses a different 13-byte (`0x0D`) format that also contains pounds and the display unit. This PR extends that existing handler without replacing the 10-byte path or changing the 16-byte layout, BLE infrastructure, or measurement model.

Only the handler, its tests and the catalog remark are changed; no APKs, raw Bluetooth logs or MAC addresses are included.
