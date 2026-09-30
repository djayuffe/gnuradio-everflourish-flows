# Technical Audit

This audit summarizes code, functions, and feature coverage for `gnuradio-everflourish-flows`.

## Scope

- Flowgraphs audited: 3 modern files plus archived originals in `flows/`.
- Tools audited: `tools/audit_flows.py` and `tools/validate_grc.py`.
- Reports regenerated locally before publication.

## Code and Function Review

- `tools/audit_flows.py` parses XML with `xml.etree.ElementTree`, hashes each file, lists block counts, connection counts, hardware endpoints, transmit-capable sinks, explicit file paths, duplicate block IDs, and exact duplicate payloads.
- `tools/validate_grc.py` uses the installed GNU Radio Companion core API, not text matching, to load, rewrite, and validate each modern `.grc` file.
- Shell examples avoid executing generated RF graphs automatically; generation and validation are separate from runtime operation.

## Feature Coverage

- 433.92 MHz receive/analysis chains
- UHD and osmocom SDR input variants
- Magnitude-squared analysis and threshold visualization paths
- Audio monitoring path
- File capture/replay path preserved from the original work

## Technical Parameters

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `EverFlourish.grc` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | uhd_usrp_source_0 (uhd_usrp_source); audio_sink_0 (audio_sink) | - |
| `EverFlourish.grc.1` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | uhd_usrp_source_0 (uhd_usrp_source); audio_sink_0 (audio_sink) | - |
| `EverFlourish_uber.grc` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | audio_sink_0 (audio_sink); osmosdr_source_0 (osmosdr_source) | - |

## Known Operational Gaps

- Runtime hardware behavior is not asserted by validation; actual SDR/audio devices must be configured locally.
- External sample/capture files named in legacy graphs are not bundled unless present in `flows/`.
- Transmit-capable graphs require separate RF lab controls and legal authorization.

## Verification

- `VALIDATION.md` has no `Result: FAILED` entries.
- `SHA256SUMS.txt` verifies all committed files.
