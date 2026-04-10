# Reproducing the EEGPrep Derivative for Zhou2016

This derivative dataset was generated from **Zhou2016** using
[EEGPrep](https://github.com/sccn/eegprep) with minimal preprocessing:
resampling to 100.0 Hz and highpass filtering at 0.5 Hz.

## 1. Download the source data

- **DOI:** 10.82901/nemar.nm000115
- **URL:** https://zenodo.org/records/16534752

## 2. Install Docker

- **macOS:** https://docs.docker.com/desktop/install/mac-install/
- **Windows:** https://docs.docker.com/desktop/install/windows-install/
- **Linux:** https://docs.docker.com/engine/install/

## 3. Reproduce the derivative

### Option A: Use the pre-built Docker image (fastest)

```bash
docker load -i eegprep-minimal.tar.gz
docker run --rm -v /path/to/nm000115:/data eegprep-minimal
```

### Option B: Rebuild from source (any architecture)

```bash
tar xzf eegprep-source.tar.gz
docker build -t eegprep-minimal .
docker run --rm -v /path/to/nm000115:/data eegprep-minimal
```

## Processing details

| Parameter | Value |
|-----------|-------|
| Sampling rate | 100.0 Hz |
| Highpass filter | 0.5 Hz (FIR Kaiser, transition band 0.5--1.0 Hz) |
| Artifact rejection | Disabled |
| ICA / ICLabel | Disabled |
| Re-referencing | Disabled |

## Custom parameters

```bash
docker run --rm -v /path/to/dataset:/data eegprep-minimal --srate 200 --highpass 1.0
docker run --rm eegprep-minimal --help
```

## Reproduce without Docker

```bash
pip install eegprep
python bids_minimal_preproc.py --input /path/to/nm000115
```

## Files in this directory

| File | Purpose |
|------|---------|
| `REPRODUCE.md` | This file |
| `bids_minimal_preproc.py` | Generic processing script |
| `Dockerfile` | Docker build instructions |
| `requirements.txt` | Pinned Python dependencies |
| `eegprep-source.tar.gz` | EEGPrep source code |
| `eegprep-minimal.tar.gz` | Pre-built Docker image |
