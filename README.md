# Malicious-Image-Creator

A lightweight proof-of-concept project for embedding and extracting payloads inside image files. The repository demonstrates how a malicious or otherwise hidden binary payload can be appended to a target file and then recovered later using companion extraction tools.

> Warning: This project is intended for authorized security research, malware analysis, and defensive testing only. Use it only in environments where you have explicit permission to test and analyze payload delivery techniques.

## Overview

The repository includes:

- `payload-embedder.py` — a Python script that appends a binary payload to a target file, such as a PNG image.
- `code/payload-extractor/` — multiple C++ extraction utilities that demonstrate recovering the hidden payload from the combined file using different methods.

This project is meant to illustrate the mechanics of payload embedding and extraction rather than provide a turnkey malicious toolchain.

## Features

- Simple binary payload stitching into any target file
- Works with image files as a practical demonstration target
- Companion extraction programs for file-based and resource-based recovery
- Example combined files included for testing and demonstration purposes

## Repository Structure

```text
Malicious-Image-Creator/
├── LICENSE
├── README.md
├── payload-embedder.py
└── code/
    └── payload-extractor/
        ├── payload-extractor.sln
        ├── payload-extractor.vcxproj
        ├── payload-extractor-from-file/
        │   ├── payload-extractor-from-file.cpp
        │   ├── payload-extractor-from-file.vcxproj
        │   └── combined_file.png
        ├── payload-extractor-from-rsrc/
        │   ├── payload-extractor-from-rsrc.cpp
        │   ├── payload-extractor-from-rsrc.vcxproj
        │   ├── Resource.rc
        │   └── combined_file.png
        └── payload-extractor-from-rsrc-via-peb/
            ├── payload-extractor-from-rsrc-via-peb.cpp
            ├── payload-extractor-from-rsrc-via-peb.vcxproj
            ├── PEB_Structs.h
            ├── Resource.rc
            └── combined_file.png
```

## Usage

### Embed a payload

```bash
python payload-embedder.py original.png payload.bin embedded.png
```

This command reads:

- `original.png` as the target file
- `payload.bin` as the binary payload to hide
- `embedded.png` as the output file containing the combined data

The script writes a new file by concatenating the payload to the selected target file.

### Extract a payload

The extractor programs under `code/payload-extractor/` are Windows C++ projects designed to recover the embedded payload from the combined file. They demonstrate different extraction strategies:

- `payload-extractor-from-file` — reads the payload from the end of the file
- `payload-extractor-from-rsrc` — extracts embedded data from a resource-backed file structure
- `payload-extractor-from-rsrc-via-peb` — extracts data using a PEB-assisted method

## Requirements

### Python embedder

- Python 3
- Standard library only

### C++ extractor samples

- Microsoft Visual Studio / MSVC
- Windows development environment

## Example Workflow

1. Prepare a benign target file, for example `original.png`
2. Create a payload binary such as `payload.bin`
3. Run the Python embedder to generate `embedded.png`
4. Use one of the extraction programs to recover the hidden payload for analysis

## Notes

- The implementation is intentionally simple and educational.
- It does not include robust anti-forensics, encryption, or production-ready packaging.
- The focus is on investigating how payloads can be appended to files and recovered.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Disclaimer

Use of this project for unauthorized access, malware deployment, or malicious activity is illegal and unethical. This repository is intended for learning, defensive research, and authorized security evaluation only.
