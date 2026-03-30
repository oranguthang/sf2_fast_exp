# SF2 Fast EXP

`sf2_fast_exp` is a gameplay-focused fork of [ShiningForceCentral/SF2DISASM](https://github.com/ShiningForceCentral/SF2DISASM).

This repository tracks the upstream `build/standard` branch and applies a fast EXP tweak on top of it, while keeping the normal split/build workflow from the base disassembly project.

## What Changed

This fork changes battle EXP gain behavior to speed up leveling:

- healing spells now use a 20 EXP floor instead of 10,
- status/support spell actions now award 10 EXP per target instead of 5,
- healing actions can accumulate up to 50 EXP instead of 25,
- damage actions and kills now resolve to the 50 EXP cap,
- the per-action EXP cap is now 50 instead of 49.

## Upstream Base

- Upstream repository: [ShiningForceCentral/SF2DISASM](https://github.com/ShiningForceCentral/SF2DISASM)
- Base branch used here: `build/standard`

## Quick Start

1. Put the original US ROM in `rom/` as `sf2.bin`.
2. Run `split\split.bat` to extract the binary assets into the disassembly tree.
3. Run `build\buildstandard.bat` to assemble the standard build with the fast EXP changes.

## Project Structure

```text
sf2_fast_exp/
|-- .github/            # Upstream workflow files
|-- build/              # Build scripts and output files
|-- disasm/             # Main disassembly source tree
|-- rom/                # Original source ROM (sf2.bin)
|-- split/              # Split scripts and split definition list
|-- tools/              # Assemblers and helper tools
`-- README.md
```

## Build Workflow

### Split

`split\split.bat`:

- reads `rom\sf2.bin`,
- uses `tools\splitrom`,
- extracts required binary chunks into the `disasm/` tree.

### Standard Build

`build\buildstandard.bat`:

- assembles the CUBEWIZ driver, music banks, and SFX bank,
- assembles the main game with `STANDARD_BUILD=1`,
- writes output files into `build/`,
- copies the latest successful build to `build\standardbuild-last.bin`.

### Other Build Scripts

- `build\build.bat` builds the vanilla configuration
- `build\buildstandard-test.bat` builds the standard test configuration

## Notes

- This fork is not intended to stay bit-perfect with the original ROM, because it deliberately changes EXP behavior.
- The split/build process remains the same as upstream; only the gameplay EXP logic is changed here.
- If you want the unmodified maintained baseline with all standard fixes/features but without this EXP tweak, use upstream `build/standard`.

## Credits

- Base disassembly: [ShiningForceCentral/SF2DISASM](https://github.com/ShiningForceCentral/SF2DISASM)
- Original game rights belong to Sega and Climax/Sonic! Software Planning
