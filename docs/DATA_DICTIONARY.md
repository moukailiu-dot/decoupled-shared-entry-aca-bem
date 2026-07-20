# Data dictionary and measurement boundaries

## Primary tables

| File | Role |
|---|---|
| `data/tables/all_formal_runs.csv` | One row per formal process run; master source for timing, memory, accuracy, rank, and convergence |
| `data/tables/timing_repeat_summary.csv` | Mean and sample standard deviation for three independent 14,118-DOF processes per mode |
| `data/tables/comsol_same_mesh_comparison.csv` | 19,608-DOF same-mesh custom-solver and COMSOL comparison |
| `data/tables/farfield_energy_consistency.csv` | Boundary power versus 194-direction offline far-field integration |
| `data/tables/figure1_scaling_source_data.csv` | System-size scaling subset |
| `data/tables/figure2_geometry_source_data.csv` | Sphere, cube, nonconvex, and near-gap subset |
| `data/tables/figure3_frequency_source_data.csv` | 100:100:3000 Hz analytical sphere sweep |
| `data/tables/figure4_*_source_data.csv` | ACA tolerance, near correction, cache policy, and hot-cache ablations |
| `data/tables/figure6_surface_pressure_source_data.csv` | Nodal nonconvex surface-pressure comparison |
| `data/tables/summary_metrics.json` | Headline values extracted from the tables |

`data/figure_source_data/` contains manuscript-versioned copies, including the
four-geometry mesh metadata used by `figure2_mesh_suite`.

## Timing fields

| Field | Definition |
|---|---|
| `operator_build_seconds` | Active pass constructing the three H-matrices; excludes geometry, sparse surface matrices, and near correction |
| `assembly_equivalent_seconds` | Geometry-independent operator stage plus sparse/correction work as defined by the analysis script |
| `gmres_seconds` | Iterative linear-solve stage measured inside the executable |
| `internal_total_seconds` | Solver-side timer from input through postprocessing |
| `external_wall_seconds` | Process start-to-exit elapsed time measured by the Python monitor |
| `peak_rss_gib` | Maximum resident set size of the process tree sampled by the monitor |
| `average_effective_cores` | Integrated process-tree CPU time divided by external elapsed time |

External wall time is the common end-to-end boundary for cross-program
comparisons. COMSOL's progress-derived assembly interval and the custom
operator-build timer are not identical software stages and are labeled as an
engineering comparison.

## Compression and cache fields

- `base_evaluations`: executed support-pair integrations, including racing misses.
- `entry_requests`: scalar coefficient requests issued by H-matrix controllers.
- `cache_hit_rate`: successful cache returns divided by recorded accesses.
- `cache_evictions`: shard-local LRU removals; zero for the full policy.
- `cache_estimated_gib`: internal payload/container estimate, not process RSS.
- `hmatrix_gib`: combined dense and low-rank payload of `V`, `K`, and `W`.
- `V/K/W_mean_rank`, `V/K/W_max_rank`: ranks over low-rank blocks.
- `V/K/W_entry_queries`: controller requests attributed to one scalar operator.

## Accuracy and acceptance fields

- `gmres_relative_residual` is recomputed from the unpreconditioned system after
  a solution update. Formal acceptance requires at most `1e-7`.
- `converged` records that true-residual acceptance, not only the inner GMRES
  recurrence estimate.
- Sphere `efficiency_error_percent`, `power_error_percent`,
  `surface_pressure_relative_l2_error`, field amplitude error, and phase error
  use the analytical pulsating-sphere solution.
- Non-spherical geometries have no analytical solution in this archive. They
  are used for mode equivalence, convergence, rank, storage, and energy
  consistency tests.
- The common-pivot cube run reached 400 iterations with a true residual above
  tolerance. Its physical outputs are not treated as converged evidence.

## Units

Times are seconds, memory is GiB (`2^30` bytes), frequencies are Hz, lengths are
metres unless a figure explicitly labels millimetres, pressure is Pa, sound
power is W, phase is degrees, and relative acoustic errors are percentages
unless the field name states a unitless fraction.
