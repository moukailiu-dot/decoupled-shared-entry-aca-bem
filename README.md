# Decoupled shared-entry ACA BEM

## Binary and data archive v1.0.0

This repository is the public binary-and-data reproducibility archive for the
study of operator-decoupled shared-entry adaptive cross approximation in a
stabilized Costabel boundary-element solver for exterior acoustics.

**This is not a source-code distribution.** It contains a compiled Windows
executable, benchmark inputs and outputs, manuscript figures and tables, and a
solved COMSOL 6.4 same-mesh reference model. C++, Python, MATLAB, Java, Julia,
Fortran, build-system files, and experiment-generation scripts are not
included.

## Archive contents

| Path | Contents |
|---|---|
| `bin/windows-x86_64/` | Compiled custom BEM executable |
| `meshes/` | Six benchmark surface meshes and field points |
| `validation/` | Small archived smoke-test output |
| `data/` | Formal timing, memory, accuracy, convergence, and figure-source tables |
| `figures/` | Publication figures in raster and vector formats |
| `models/comsol6.4/` | Solved COMSOL 6.4 model, identical BDF mesh, and exported measurements |
| `docs/` | Data dictionary and COMSOL model contract |
| `checksums/` | SHA-256 integrity manifest |

## Run the executable

The executable targets 64-bit Windows. From PowerShell at the archive root, a
small 3000 Hz shared-entry run can be started with:

```powershell
.\bin\windows-x86_64\cpp_costabel_bem.exe `
  .\meshes\sphere_n12 `
  .\run_output\sphere_n12_shared_3000Hz `
  --compression-mode shared `
  --frequency 3000 `
  --threads 4 `
  --aca-tol 1e-4 `
  --near-rings 1 `
  --cache-policy full `
  --max-solution-dofs 20000
```

The general command interface is:

```text
cpp_costabel_bem DATA_DIR OUTPUT_DIR [--compression-mode independent|shared|joint --frequency 3000 --threads 22 --aca-tol 1e-4 --near-rings 1 --cache-policy full|lru --cache-capacity 0 --max-solution-dofs 20000]
```

The archived smoke result is in `validation/smoke_shared`. The formal results
used by the manuscripts are immutable tables under `data`; see
`docs/DATA_DICTIONARY.md` for timing boundaries, units, and acceptance rules.

## COMSOL comparison

Open `models/comsol6.4/comsol_sphere_n33_p11_3000Hz.mph` with COMSOL 6.4 to
inspect the retained mesh, Pressure Acoustics Boundary Elements settings,
solved study, and result definitions. The matching imported mesh is
`sphere_n33_6536_nodes_6534_quads.bdf`. COMSOL software and a license are not
part of this archive. See `docs/COMSOL_MODEL.md` for the full model contract.

## Integrity

`checksums/SHA256SUMS.txt` records the SHA-256 digest of every distributed file
except the checksum file itself. Paths use forward slashes and are relative to
the archive root.

## Distribution terms

Data, meshes, figures, and model artifacts are distributed under CC BY 4.0;
see `LICENSE-DATA`. The Windows executable is governed separately by the
restrictive `LICENSE-BINARY-RESEARCH-ONLY.txt`: it may be used for
non-commercial research, teaching, and evaluation, but may not be
redistributed, commercially deployed, modified, decompiled, or used to create
derivative software. `BINARY-NOTICE.txt` provides the short-form notice.
The unpublished manuscript documents are not included in this archive.

Repository: https://github.com/moukailiu-dot/decoupled-shared-entry-aca-bem
