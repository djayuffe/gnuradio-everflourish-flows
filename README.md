# GNU Radio EverFlourish SDR Flows

Modern GNU Radio Companion flows for EverFlourish 433 MHz remote-control receive, capture, and analysis.

EverFlourish remote-control receive/analysis graphs with UHD and osmocom SDR input variants. The repository is modern-only: runnable GNU Radio Companion files live in `modern/`, use repo-local paths, and validate with GNU Radio Companion 3.8.5.0.

## Features

- Modern GNU Radio Companion XML only; outdated source XML was removed from the public repo.
- Qt GUI blocks replace old WX GUI patterns where applicable.
- Machine-specific paths were replaced with repo-local `samples/` and `captures/` paths.
- `tools/audit_flows.py` and `tools/validate_grc.py` provide repeatable checks.
- `SHA256SUMS.txt` tracks committed-file integrity.

## Flowgraphs

- `modern/EverFlourish.grc`
- `modern/EverFlourish.grc.1`
- `modern/EverFlourish_uber.grc`

## Technical Inventory

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `EverFlourish.grc` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | uhd_usrp_source_0 (uhd_usrp_source); audio_sink_0 (audio_sink) | - |
| `EverFlourish.grc.1` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | uhd_usrp_source_0 (uhd_usrp_source); audio_sink_0 (audio_sink) | - |
| `EverFlourish_uber.grc` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | audio_sink_0 (audio_sink); osmosdr_source_0 (osmosdr_source) | - |

## Standards and Frequencies

- GNU Radio Companion target validated locally: 3.8.5.0.
- Frequency, sample-rate, and mode values are shown in the inventory table above from the actual `.grc` XML.
- Transmit-capable repositories include explicit RF safety text and keep transmit examples isolated.

## Repo-Local File Paths

- `EverFlourish.grc`: blocks_file_sink_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_source_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_sink_1.file=captures/everflourish_magsquared.float32
- `EverFlourish.grc.1`: blocks_file_sink_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_source_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_sink_1.file=captures/everflourish_magsquared.float32
- `EverFlourish_uber.grc`: blocks_file_sink_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_source_0.file=captures/everflourish_remote_control_recording.cfile; blocks_file_sink_1.file=captures/everflourish_magsquared.float32

## Setup Helpers

- No setup scripts needed.

Run setup helpers only if you need placeholder files for local graph loading or non-radiating tests.

## Usage Examples

```sh
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done
shasum -a 256 -c SHA256SUMS.txt
```

Open a flowgraph interactively:

```sh
gnuradio-companion modern/<flowgraph>.grc
```

Inspect generated Python before running it. Confirm hardware, frequency, gain, sample rate, and paths every time.

## Safety

Receive/analysis flows. Repo-local `captures/` paths replace machine-specific paths.

## Audit Status

- Modern flowgraph audit: `AUDIT.md`.
- GNU Radio validation: `VALIDATION.md`.
- Generation summary: `COMPILE.md`.
- Technical review: `TECHNICAL_AUDIT.md`.

## License

No new license is asserted for the original flowgraph design lineage. Review provenance before redistribution in other projects.
