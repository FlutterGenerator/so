# GitHub Actions: ELF / `.so` analysis with Ghidra

This repository template analyzes a native ELF shared library in GitHub Actions and uploads a ZIP report.

## 1. Add the library

Upload the library you are authorized to analyze to:

`input/libGamerKillshot.so`

Do not commit it to a public repository unless you have permission to distribute it. Prefer a private repository for proprietary or sensitive binaries.

## 2. Create the repository files

Keep these paths exactly:

- `.github/workflows/analyze.yml`
- `scripts/ExportDecompilation.java`
- `input/libGamerKillshot.so` (your own uploaded binary)

The workflow and Ghidra script are included in this template. The `input` folder contains a placeholder README only.

## 3. Run the workflow from a phone

1. Open your repository on GitHub.
2. Open **Actions**.
3. Select **Analyze ELF library**.
4. Tap **Run workflow**.
5. Keep the default path `input/libGamerKillshot.so`, unless you uploaded the file under a different path.
6. Start the run and wait for it to finish.

## 4. Download results

Open the completed run and download the `GamerKillshot-analysis` artifact. Unzip it to inspect:

- `file-info.txt` — file type and architecture
- `elf-header.txt`, `program-headers.txt`, `sections.txt` — ELF layout
- `symbols.txt`, `dynamic-symbols.txt` — symbols
- `dynamic-section.txt`, `relocations.txt` — dependencies and relocations
- `strings.txt` — printable strings
- `decompiled/decompiled.c` — Ghidra-generated C-like pseudocode
- `ghidra.log`, `ghidra-script.log` — analysis logs
- `sha256.txt` — hash of the input library

## Notes and troubleshooting

- Pseudocode is an approximation, not original C/C++ source.
- Stripped symbols, compiler optimizations, obfuscation, and missing type information reduce readability.
- Ghidra headless analysis can be memory-intensive. The workflow has a 90-minute job timeout.
- If the latest Ghidra release changes its Java requirement, check the official Ghidra release notes and adjust the JDK setup step.
- Workflow artifacts are retained for 7 days by this template.
