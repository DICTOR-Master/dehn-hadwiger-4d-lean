# The Dehn–Hadwiger invariant in four dimensions (Lean 4 + Mathlib)

Author: DICTO.

The Dehn–Hadwiger invariant `dehnHadwiger P` is defined from the set `P` alone, in every finite-dimensional real inner
product space. At a point of `P` the directions that stay in `P` form a cone; where the directions `v` with `v` and `-v`
in the cone span a subspace of codimension 2 (a ridge point), the class there is the angle of the cone in the
orthogonal plane, modulo rational multiples of π. `dehnHadwiger P` adds, over the classes θ, the (n − 2)-dimensional
Hausdorff measure of the ridge points of class θ, tensored with θ, in ℝ ⊗[ℚ] (ℝ/ℚπ). In ℝ⁴ this is Hadwiger's sum of
area ⊗ dihedral angle over the 2-faces (Hadwiger, Math. Ann. 127, 1954). The Challenge proves:

1. **The bridge** (`dehnHadwiger_eq_of_scissorsCongruent`, `dehnHadwigerSum_eq_of_scissors`): scissors-congruent
   convex polytopes, and finite unions of them, have the same invariant, in every dimension.
2. **The six regular 4-polytopes**: the tesseract, the 16-cell, the 24-cell and the 120-cell have invariant 0; the
   5-cell has A₅ ⊗ arccos(1/4) and the 600-cell A₆₀₀ ⊗ (4π/3 − arccos(1/4)), with A₅, A₆₀₀ > 0 the areas of the ridge
   points; arccos(1/4) is not a rational multiple of π.
3. **Non-congruence**: no similar copy of the 5-cell or of the 600-cell is scissors congruent to a similar copy of the
   tesseract, the 16-cell, the 24-cell or the 120-cell; no similar copy of the 5-cell is scissors congruent to a
   similar copy of the 600-cell (the 600-cell's dihedral angle is 4π/3 minus the 5-cell's, so the two invariants have
   opposite signs).

Pieces of a dissection are convex polytopes, finitely many, moved by isometries, reflections included. Jessen's
converse in ℝ⁴ is not stated.

- `Challenge.lean`: the definitions and the fourteen statements, every proof `sorry`; Mathlib only; every definition and
  statement copied, character for character, from the development by a script.
- `Solution.lean`: the Challenge word for word, with proofs that transfer the theorems of the development.
- `DehnHadwiger/`: the development. `DehnHadwiger/Canon/` holds the modules of the Dehn Canon entry
  (PALOMAR-2026-11-20-000003) that it uses: convex polytopes, tangent cones, wedge angles, cuts and dissections. The
  modules `DH1Def` to `DH15Results600` add the codimension-2 invariant, its cut identity and the bridge, scaling, the
  angle of a cone of constraints, and the six polytopes; the 600-cell's facet data are exact ℤ[φ] lists checked by
  `decide +kernel`.

Toolchain `leanprover/lean4:v4.35.0-rc2`, Mathlib `v4.35.0-rc2`. All fourteen theorems depend only on the axioms
`propext`, `Classical.choice` and `Quot.sound`. Neither `sorry` nor `native_decide` is used. Every Lean file uses the
module system.

## How it was made

DICTO posed the formalization and directed it; the Lean code was written by a Claude Code agent (Claude, Anthropic).
See `formalization.yaml` for the sources, the related formalizations and the checks.

## How to cite and reuse

### How to cite

- **The paper.** DICTO, *The Dehn–Hadwiger invariant in four dimensions — Machine-checked for the six regular
  polytopes, and one 600-cell balanced by 120 regular 5-cells* (paper #116), Zenodo, 2026. DICTO DOI:
  [10.5281/zenodo.24393967](https://doi.org/10.5281/zenodo.24393967) (all versions; Version 1:
  10.5281/zenodo.24393968). Its Theorem 1 is the fourteen statements of the Challenge.
- **The Palomar entry.** Prepared for the Palomar registry (not yet submitted).
- **The repository commit.** github.com/DICTOR-Master/dehn-hadwiger-4d-lean: the commit submitted to Palomar. The Lean
  files are those of commit `16062109a7f9b1780b4b81ac703e80920b877e19`; later commits change only metadata and
  documentation, not the Lean files.

`CITATION.cff` holds the same data in machine-readable form (GitHub shows it under "Cite this repository").

### What the library offers

The fourteen theorems of the Challenge are listed above (namespace `DehnHadwiger4D`). The development in
`DehnHadwiger/` (namespace `DehnHadwiger`, with the Dehn Canon modules in `DehnHadwiger/Canon/`, namespace `DehnCanon`)
can be used on its own.

- The invariant, in every finite-dimensional real inner product space. `thetaH` (the angle class at a point),
  `ridgeAngle` and `dehnHadwiger` (the invariant of a set) in `DH1Def.lean`, on `ratPi`, `Angle` (ℝ/ℚπ) and
  `DehnSpace` (ℝ ⊗[ℚ] Angle) of `Canon/DehnCanon1.lean` and `tcone`, `linSpace`, `wedgeAngle` of `Canon/Dehn2Local.lean`.
- Properties of `dehnHadwiger`. `dehnHadwiger_cut` (the hyperplane-cut identity, `DH2Cut.lean`); `dehnHadwiger_image`
  (invariance under affine isometries), `dehnHadwiger_dissection`, `dehnHadwiger_eq_of_scissorsCongruent`,
  `not_scissorsCongruent_of_dehnHadwiger_ne`, `dehnHadwigerSum_eq_of_scissors` (`DH3Bridge.lean`);
  `dehnHadwiger_smul_set`, `dehnHadwiger_similarCopy`, `not_scissorsCongruent_similarCopies` (`DH5Scale.lean`).
- Polytopes given by facet normals. `thetaH_pair` and `wedgeAngle_two_planes'` (the angle at a point where two facets
  are tight, from their normals), `dehnHadwiger_sol_eq_single` and `dehnHadwiger_sol_eq_zero_of_rational`
  (`DH4Pair.lean`); `dehnHadwiger_sol_eq_single_ridge`, `eq_of_mem_span_pair` and `facet_bary` (`DH10Ridge.lean`).
- The six regular 4-polytopes. `tesseract`, `cell16`, `cell24` (`DH6Cells.lean`), `cell5` (`DH7Cell5.lean`), `cell120`
  (`DH8Cell120.lean`) and `cell600` (`DH11Cell600Defs.lean`), each with `isPoly_…` and its invariant; `adj_class` and
  `cell600_pair` (`DH13Cell600.lean`).
- Angles and exact arithmetic. `arccos_quarter_not_ratPi` (arccos(1/4) is not a rational multiple of π, from Mathlib's
  `niven`, `DH7Cell5.lean`); `gval`, `gvec`, `gdot` (ℤ[φ] vectors in ℝ⁴) and `mem_ratPi_of_cos_five`
  (`DH8Cell120.lean`); `area_pos_of_patch` (positive area from a small square on a ridge, `DH14Cell600Area.lean`).
- From the Dehn Canon: `sol`, `IsPoly` (`Canon/Dehn2Poly.lean`), `ScissorsCongruent` (`Canon/DehnCanon2.lean`) and
  `IsSimilarCopy` (`Canon/Dehn4Similar.lean`).

### How to import it

The library builds with `leanprover/lean4:v4.35.0-rc2` and Mathlib `v4.35.0-rc2`; a project that requires it should use
the same toolchain and Mathlib. In `lakefile.toml`:

```toml
[[require]]
name = "DehnHadwiger4D"
git = "https://github.com/DICTOR-Master/dehn-hadwiger-4d-lean.git"
rev = "16062109a7f9b1780b4b81ac703e80920b877e19"
```

Then import the modules you need, for example:

```lean
import DehnHadwiger.DH3Bridge
import DehnHadwiger.DH15Results600
```

### Licence

The Lean code: Apache-2.0 (see `LICENSE`). Copyright 2026 DICTO. The paper #116: CC BY-SA 4.0.

## Other work by DICTO

- The Dehn Canon (paper #113, DICTO DOI: 10.5281/zenodo.24383552) and its Lean entry
  [DICTOR-Master/dehn-canon-lean](https://github.com/DICTOR-Master/dehn-canon-lean) (PALOMAR-2026-11-20-000003).
- ORCID (all works): https://orcid.org/0009-0001-2620-2036
- Website: https://dictospheres.com
