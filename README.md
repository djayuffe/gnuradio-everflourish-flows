# GNU Radio EverFlourish SDR Flows

Modern GNU Radio Companion flows for EverFlourish 433 MHz remote-control receive, capture, and analysis.

This public repository is split from the audited `modern-gnuradio-sdr-flows` workspace. It keeps a focused GNU Radio Companion flow family with archived originals in `flows/` and validated modern ports in `modern/`.

## Features

- 433.92 MHz receive/analysis chains
- UHD and osmocom SDR input variants
- Magnitude-squared analysis and threshold visualization paths
- Audio monitoring path
- File capture/replay path preserved from the original work

## Standards and Signal Context

- ASK/OOK-style 433.92 MHz remote-control analysis
- GNU Radio Companion XML validated with GNU Radio 3.8.5.0

## Flowgraph Inventory

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `EverFlourish.grc` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | uhd_usrp_source_0 (uhd_usrp_source); audio_sink_0 (audio_sink) | - |
| `EverFlourish.grc.1` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | uhd_usrp_source_0 (uhd_usrp_source); audio_sink_0 (audio_sink) | - |
| `EverFlourish_uber.grc` | 28 | 18 | usrp_samp_rate=5e6; samp_rate=usrp_samp_rate/decimation; rx_gain=15; freq=433.92e6 | audio_sink_0 (audio_sink); osmosdr_source_0 (osmosdr_source) | - |

## File and Capture Paths

- `EverFlourish.grc`: blocks_file_sink_0.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/remote_control_recording; blocks_file_source_0.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/remote_control_recording; blocks_file_sink_1.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/magsquared
- `EverFlourish.grc.1`: blocks_file_sink_0.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/remote_control_recording; blocks_file_source_0.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/remote_control_recording; blocks_file_sink_1.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/magsquared
- `EverFlourish_uber.grc`: blocks_file_sink_0.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/remote_control_recording; blocks_file_source_0.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/remote_control_recording; blocks_file_sink_1.file=/home/alex/dev/sdr/ever-flourish-remote-control-plug/magsquared

Update these paths before running graphs on a different machine. Generated files, captures, recordings, and raw samples are intentionally ignored by git.

## Usage Examples

```sh
# Validate modernized flowgraphs
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md

# Generate Python without running RF hardware
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done

# Verify committed file integrity
shasum -a 256 -c SHA256SUMS.txt
```

To open a graph interactively:

```sh
gnuradio-companion modern/<flowgraph>.grc
```

To run generated Python, inspect the generated script first and confirm hardware, frequency, gain, sample rate, and file paths. Do not run transmit-capable graphs directly from generated code without RF isolation and legal authorization.

## Safety

Receive/analysis flows. Update old absolute capture paths before running replay or recording blocks.

## Audit Status

- Archived originals parse as XML. See `AUDIT.md`.
- Modernized flowgraphs validate OK. See `VALIDATION.md`.
- Python generation was verified with GNU Radio Companion Compiler 3.8.5.0. See `COMPILE.md`.
- Checksums are tracked in `SHA256SUMS.txt`.

## Repository Layout

- `flows/` - archived original flowgraphs and related data files.
- `modern/` - modernized GNU Radio Companion flowgraphs for normal use.
- `tools/` - repeatable audit and validation helpers.
- `README.md` - usage and technical overview.
- `DESCRIPTION.md` - short project description.
- `AUDIT.md`, `VALIDATION.md`, `COMPILE.md` - generated audit/verification reports.

## License

No new license is asserted for the archived flowgraphs. Preserve original ownership/history before redistribution or publication.
