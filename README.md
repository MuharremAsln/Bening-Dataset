# Windows Benign Executable Dataset

This repository contains a benign Windows executable-like dataset for static
binary analysis, malware-detection research, and machine learning experiments.
The files are labeled as the benign class and stored with anonymized sequential
names using the `.train` extension.

## Dataset Overview

| Field | Value |
| --- | --- |
| Class label | Benign |
| Sample count | 8,900 |
| Total sample size | ~4.0 GB |
| Maximum sample size | < 20 MB |
| File naming | `benign_000000.train`, `benign_000001.train`, ... |
| Main directory | `Exetuble Files/` |
| Source environment | Clean Windows 11 environment |

## How The Dataset Was Prepared

The benign samples were collected from a clean Windows 11 environment. The
collection includes original operating system files and application executable
files that represent normal, non-malicious desktop software.

During preparation, files were selected using executable-like Windows formats
such as `.exe`, `.dll`, `.sys`, `.com`, `.scr`, `.cpl`, `.msi`, `.msp`, `.bat`,
`.cmd`, and `.ps1`. The files were also filtered by readability and size so that
very small files and files larger than the preprocessing limit were excluded.

After collection and filtering, the samples were renamed into a consistent
sequence and stored with the `.train` extension. The extension is used for
dataset organization; the files should still be treated as raw executable or
executable-like binary content.

## Structure

```text
.
|-- Exetuble Files/
|   |-- benign_000000.train
|   |-- benign_000001.train
|   |-- benign_000002.train
|   `-- ...
`-- README.md
```

The directory name is kept as it exists in the original project files.

## Intended Use

This dataset can be used as a benign class for:

- static executable analysis
- byte-level feature extraction
- executable-to-image or executable-to-volume representation pipelines
- malware detection model training and evaluation
- benign-versus-malware binary classification experiments

This repository contains only the benign side of a binary classification setup.
Malware samples, if needed, should be collected, verified, and labeled
separately.

## Working With The Files

Count the samples:

```bash
find "Exetuble Files" -type f -name "*.train" | wc -l
```

Inspect a sample:

```bash
file "Exetuble Files/benign_000000.train"
```

Read a file as raw bytes in Python:

```python
from pathlib import Path

sample = Path("Exetuble Files/benign_000000.train")
data = sample.read_bytes()
print(len(data))
```

Depending on the sample, file-identification tools may report PE32, PE32+,
DLL, console or GUI executable types, scripts, or generic binary data. This is
expected for a renamed executable-like dataset.

## Safety Note

The files are labeled as benign, but they are still executable or
executable-like files. Do not run samples directly on a production machine. Use
an isolated virtual machine, sandbox, or offline analysis environment when
inspecting or processing the dataset.

## Notes

- Filenames are anonymized and sequential.
- The `.train` extension is a dataset convention, not the original Windows file
  extension.
- The dataset is intended for static analysis; runtime behavior is not included.
- Antivirus or endpoint security tools may warn about large executable
  collections during scanning or upload.
- Because the dataset is several gigabytes, Git LFS or an external release
  artifact may be required when publishing it on GitHub.
