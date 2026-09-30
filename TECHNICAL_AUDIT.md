# Technical Audit

This audit covers the modern-only public repository `gnuradio-everflourish-flows`.

## Scope

- Modern flowgraphs audited: 3.
- Outdated public XML removed from the repo.
- Repo-local file paths used for samples/captures.
- GNU Radio Companion validation target: 3.8.5.0.

## Tooling Review

- `tools/audit_flows.py` parses GRC XML, hashes each file, reports block/connection counts, hardware endpoints, transmit-capable sinks, file paths, duplicate IDs, and exact duplicate payloads.
- `tools/validate_grc.py` uses GNU Radio Companion's Python API to load, rewrite, and validate each modern `.grc`; it does not rely on ad hoc text matching.
- Setup scripts, where present, create safe placeholder local files only. They do not run SDR hardware.

## Feature and Parameter Coverage

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `EverFlourish.grc` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | uhd_usrp_source_0 (uhd_usrp_source); audio_sink_0 (audio_sink) | - |
| `EverFlourish.grc.1` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | uhd_usrp_source_0 (uhd_usrp_source); audio_sink_0 (audio_sink) | - |
| `EverFlourish_uber.grc` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | audio_sink_0 (audio_sink); osmosdr_source_0 (osmosdr_source) | - |

## File Path Coverage

- `EverFlourish.grc`: blocks_file_sink_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_source_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_sink_1.file=captures/everflourish_magsquared.float32
- `EverFlourish.grc.1`: blocks_file_sink_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_source_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_sink_1.file=captures/everflourish_magsquared.float32
- `EverFlourish_uber.grc`: blocks_file_sink_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_source_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_sink_1.file=captures/everflourish_magsquared.float32

## Remaining Runtime Responsibilities

- GRC validation and `grcc` generation do not prove connected SDR/audio hardware behavior.
- Users must configure local devices, antennas, sample files, and gains.
- Transmit-capable graphs require RF isolation and authorization before any runtime use.

## Verification Checklist

- `VALIDATION.md` contains no `Result: FAILED` entries.
- `SHA256SUMS.txt` verifies all committed files.
- Generated Python and runtime captures remain ignored by git.
