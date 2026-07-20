# COMSOL 6.4 same-mesh reference

## Model contract

| Item | Archived setting |
|---|---|
| model | `comsol_sphere_n33_p11_3000Hz.mph` |
| COMSOL version | 6.4.0.293 |
| physics | Pressure Acoustics, Boundary Elements |
| field discretization | `p11` |
| imported mesh | 6,536 nodes and 6,534 CQUAD4 elements |
| expected reported field DOFs | 19,608 |
| frequency | 3000 Hz |
| sphere radius | 0.1 m |
| density and sound speed | 1.21 kg m^-3 and 343 m s^-1 |
| excitation | unit outward normal velocity |

The BDF file is generated from `meshes/sphere_n33`. Its node, element, and BDF
SHA-256 hashes are recorded in the release checksum manifest. The archived
model retains the exterior-void selection, surface normal-velocity excitation,
acoustic material properties, solved study, and result definitions needed to
inspect the same-mesh comparison.

## Open the solved model

Open `comsol_sphere_n33_p11_3000Hz.mph` in COMSOL 6.4. The imported mesh and
solved study are retained. The model is supplied for configuration inspection
and same-mesh verification; COMSOL software and a license are not included.

`comsol_raw_eval.csv` is the exported numerical result from the formal run, and
`comsol_process_samples.csv` contains the corresponding external process
samples. No COMSOL Java builder or other source code is distributed in this
archive.

## Archived resource measurements

The monitored formal process used 22 configured threads. Its external
start-to-exit time was 79.175 s and sampled peak RSS was 4.029 GiB. The COMSOL
study call took 61.047 s inside Java, while the progress-derived assembly
interval was 53.191 s. These are different measurement boundaries; the paper
uses external wall time for the end-to-end cross-program comparison and labels
the internal stage comparison accordingly.
