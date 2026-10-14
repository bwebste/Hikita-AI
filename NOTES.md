# Notes on the OpenAI Hikita preprint

Source: family 044 of the `openai/math` release (24 Sep 2026),
`preprints/The-equivariant-cohomological-Hikita-conjecture-for-arbitrary-quivers-September-24-2026/`.
Local clone: `~/GitHub/openai-math`.  No Lean formalization for this family.

Status vocabulary: [proved] / [checked] / [plausible] / [hope] / [unknown],
as in research-mode.  Nothing below has been verified against the proofs;
"the paper claims" throughout.

## What the paper does (2026-10-06)

- Proves the equivariant cohomological Hikita conjecture (Dumanski–Krylov
  Conj. 2.1, eq. (2.3)) for every finite quiver, loops and multiple arrows
  included, any flavor torus, any *regular* stability (semistable = stable,
  free action).  Keeps nilpotents; includes the empty case.
- Previously known: Jordan quiver (Krylov–Shlykov), finite type ADE with
  E7/E8 framing restrictions (Dumanski–Krylov).
- Not covered: quantized version, non-GL gauge groups, K-theory.  Paper
  cites Hoang–Krylov–Matvieievskyi Ex. 6.7 for a failure outside the quiver
  setting — **not yet read; check which hypothesis fails there.**

## Structure of the proof

Chain `C[Y^ν] → B_F → H*_F(X)`, where `B_F` = coordinate ring of the
full-topological-torus fixed scheme.  Two independent halves:

1. `B_F ≅ H*_F(X)` (§§3–7):
   - stable-pair vanishing-cycle test gives `B_F ↠ H*_F(X)` for all data;
   - add a loop at every vertex, no flavor, det stability: Laurent model
     (loop weights cancel Grassmannian Euler denominators), multipartition
     filtration, cut ideals, Hilbert series matched to Hausel's formula →
     equality;
   - remove loops by giving them mass z, localize at (x,z)=(0,1), descend
     homogeneous ideals; other regular stabilities by Betti constancy;
     flavor by graded Nakayama.
2. `C[Y^ν] ≅ B_F` (§8): adjoin a rank-1 framing vertex; central monopole z
   gives `M^+_b = z M^-_{d-b}`; polynomial CoHA (Jindal–Neguț, Tsymbaliuk)
   decomposes surviving monopoles into Kac-support charges of weight 0;
   Crawley-Boevey lifting + direct sum gives a semistable point with
   positive-dimensional stabilizer, contradicting regularity.

## Verification (2026-10-06)

Seven independent adversarial readings, one per section; see
`VERIFICATION.md`.  [checked] No error or load-bearing gap found; ~15
explicit computations agree; external citations that were fetched (BFN18,
Weekes, Hoskins, MN18, Tsymbaliuk, Jindal–Neguț) say what the paper says.
Issues are all presentational (16 listed).  Hausel's formula was checked
from memory, pinned by the Jordan v=1 sign check.  The one convergent flag
(degree convention in Prop 2.2) resolved: it is BFN Lemma 2.6's grading,
differing from 2Δ(λ) by ⟨det N, λ⟩ — charge-dependent only, harmless.

## Precedent for the added-loop step

The paper does not claim the trick is new and cites no direct precedent.
It cites Krylov–Shlykov Rem. 1.15 for "deformation arguments" and
Dumanski–Krylov Prop. 2.3 for prequotient localization.  The denominator
cancellation itself is attributed only to the Grassmannian tangent-weight
calculation (cf. Weekes Lemma 2.10).  [unknown] whether anyone has used
loops this way for Hikita before — not searched.

## Ben's suggestion: general (G,N) via a copy of the adjoint (2026-10-06)

- [plausible] Massless adjoint summand contributes
  `∏_α α^{(−⟨α,λ⟩)_+}` to the abelianized monopole of *any* coweight λ, which
  cancels `eu(T_{t^λ} Gr^λ)` up to sign (tangent weights of Gr^λ at t^λ are
  roots α with ⟨α,λ⟩>0, multiplicity ⟨α,λ⟩, at ħ=0 — recalled, not checked).
  So the Laurent-model step works for all λ, not just minuscule.
- [plausible] Mass-deformation removal (§7) is not quiver-specific.
- Quiver-specific as written, no replacement in hand:
  - minuscule generation (Weekes) — many G have no minuscule coweights;
  - Kirwan surjectivity (McGerty–Nevins is for quiver varieties);
  - cut-ideal count vs Hausel (GL/S_n combinatorics);
  - Part II entirely (Kac support, CoHA).
- [proved] Semisimple G has no nontrivial characters, so regularity needs
  a big center: interesting cases are products of GL's with non-quiver N
  (Sym², Λ², tensors), or GL×Sp mixtures.
- Next: read HKM24 Ex. 6.7; try GL₂, N = Sym²C² ⊕ C², det stability by hand.

## The BPS route to the dimension bound (2026-10-14)

Source: `hikita_bps_only_proof.pdf` (9 Oct 2026, 7pp) and
`hall_coulomb_comparison.pdf` (14 Oct 2026, 4pp), both unattributed.  The
second isolates the part of preprint Lemma 8.1 that the first uses.

**Claim.**  `dim B_0 ≤ dim H*(X)` for every quiver, directly, with no added
loops, filtration, cut ideals or Hausel.  Together with `B_0 ↠ H*(X)` this
gives the isomorphism.

**Set-up.**  `Q̂` = `Q` plus a vertex `∞` with `w_i` arrows `i → ∞`,
`d = (v,1)`.  `Ĝ ≅ G × C^×` via `((g_i),c) ↦ ((c g_i), c)`, the `C^×`
acting trivially, so `Â = A ⊗ C[ξ, ζ^{±1}]`, `x̂_{ia} = y_{ia} + ξ`,
`x̂_∞ = ξ`, and Ĝ-charge `(γ,k)` is G-charge `γ − kv`.
`Θ : Â → B_0`, `ξ ↦ −b/D` (`b = Σ y_{ia}`, `D = |v|+1`), `ζ ↦ 1`.
`H` = loop-nilpotent CoHA of the tripled quiver of `Q̂`, over
`S = C[ħ,u_a]`, specialized abstractly at `m = (ħ,u_a)`.
`T_d` = proper products, `C_d` = mult. by `Σ z` (total determinant).
Chain: `G_d (BPS) ↠ H_d/(T_d + C_d H_d) ↠ B_0`, `dim G_d = dim H*(X)`.

**Internal logic, step by step.**
- [proved] `Ĝ ≅ G × C^×` intertwines the actions, with `C^×` trivial on `N`;
  Ĝ-charge `(γ,k)` ↦ G-charge `γ − kv`; `x̂ = y + ξ`.
- [proved] `Θ` is an algebra map (everything commutative at ħ=0) killing
  every `Â_{(γ,k)}` with `γ ≠ kv`, and `Θ(Σ x̂) = b + Dξ ↦ 0`.
- [proved] Step 2: a proper `0 < (γ,k) < (v,1)` has `k ∈ {0,1}` and
  `γ ≠ kv`, so `Θ∘Ψ` kills `T_d`.
- [proved, given (I1)+(3.3)] Step 1 (`ψ(e_{d,g}) = c·p` for
  `g = p(z_{ia} − z_∞)`, so onto since `R ↠ B_0`) and Step 3
  (`C_d e_{d,g} = e_{d,C_d g}`; `C_d` is a derivation for the Hall product
  because `det` is multiplicative in extensions, so `C_d T_d ⊆ T_d`).
- [proved, given (I2)] Step 4: words of length ≥ 2 lie in `T_d`.
- [checked] Coulomb side of the chain in two small cases, from the
  Hall–Coulomb formula `E_n(g)`: Kronecker `Q̂` (A₁, v=1, w=2):
  `Ψ(T_d) = (x_1 − x_∞)² C[x] ζ`, image `C[x]/((x_1−x_∞)², x_1+x_∞)` =
  `C[y]/(y²)` = `B_0` ✓.  Jordan v=w=1: image `C` ✓.
- [checked] The numerology of (I3) — Kac polynomial of `Q̂` at `(v,1)`, at
  `q = 1`, equals `dim H*(X)` — by hand for A₁ w=1,2; Jordan v=1,w=1
  (`a = q`); Jordan v=2,w=1 (`a = q² + q`).
- Caution from a failed toy model: a naive guess of the Hall side
  (origin class `[0]` and extension-locus classes in one BM module) puts
  `e_{d,1}` inside `T_d`, contradicting Step 1.  [plausible] The fix is the
  virtual Euler factors of the critical/dimensionally reduced CoHA (cf. the
  note's "abstract specialization" warning; JN: every `e_{n,g}` is
  divisible by `ħ^{|n|}` in the shuffle algebra, so the specialized shuffle
  map is zero in positive degree).  The Hall side can't be reconstructed
  casually; it rests on JN.
- [plausible] Step 3 does not need polynomial generation: at ħ=0 the GKLO
  image of `h·F` (h symmetric) multiplies the `D^λ` term by `h` at the
  progression points, so `Ψ(C_d F) = δΨ(F)` with `δ = −{½Σx̂², −}`, and
  `Θ∘δ = 0` on `Â_d` (`δζ = (Σx̂)ζ`; on `A_0 = R + Σ A_{−c}A_c` (Lemma
  `generic`) δ kills `R` and preserves `I_B`).  This is the preprint's §5
  derivation `D_{i,k}`.  Not checked against Tsymbaliuk's formula.  Then JN's
  polynomial generation is needed only for *integrality* (`Ψ(H) ⊆ Â`, used
  in Step 2), and JN Thm 3.5 (injectivity of `ι`) only through Prop 3.14.

**Citation checks (2026-10-14, two agents, against arXiv sources).**
- JN 2607.23544v1 (PDF numbering; HTML is shifted by 2 in §3):
  - (I1) Thm 2.4 is a *shuffle* statement, integral over `R = Z[Lie T]`,
    loops allowed; proof only sketched ("completely analogous" to their
    K-theory paper).  Transfer to the CoHA needs Prop 3.7 (sketched),
    Lemma 3.6 `ι(ε_{n,g}) = e_{n,g}` (no proof; misprint g ∈ R), Thm 3.5
    injectivity (proof omitted).  `e_{n,g} = g·e_{n,1}` ✓ ((98)).
  - (I2) PBW for the loop-nilpotent CoHA is (109), stated only as a
    vector-space iso; generation is Cor 3.15, whose proof cites Thm 3.10
    (full CoHA) where (109) is needed.  `L_n` is defined in (110).  JN never
    write `Σz`; total determinant confirmed from Davison A² (18)–(19).
  - (I3) Prop 3.14 `s(g^{ω-nilp}) = ħ g^T`: proof complete (Gysin by
    `eu = ħ` + dimension count via Thm 3.5).  Freeness of `g^T` imported
    from Davison, not proved in JN.
  - Three JN misprints logged to NotePlan "Inconsistencies".
- Botta–Davison 2312.14008v4: Lemma 3.1, Prop 3.4 (strictly: pushforward
  comparison, via Toda), Def 3.6, Prop 3.8, Prop 3.11, Cor 3.12–3.13 all as
  the note says; v1–v2 numbering is off by one from Def 3.6.  Loops and
  multiple arrows allowed; assumes `w ≠ 0` (note handles `w = 0`).
  Stability `δ_∞` = framing images generate ✓.  [checked] Proof of
  Cor 3.13 is purely sheaf-theoretic — no Kac polynomials, point counts,
  Hausel or Hua.  Prop 3.11 cites a variant (Dav20 Prop 6.3, no `ω_∞`) —
  logged as citation imprecision.
- DHSM 2303.12592v5: Prop 11.9 / Cor 11.10 correct (= 11.8 / 11.9 in v4);
  allowed group `G_arr × C^*` covers the `(ħ, u_a)` torus.
- Davison A² 2209.05971v6 (18)–(19): `u` acts by `c_1(⊗_i det V_i)` ✓;
  Prop 4.1 is the per-vertex derivation.
- DM 1601.02479: generation follows from Thm C (not A); DM is
  non-equivariant, so the equivariant PBW should be cited from DHSM
  Thm 11.7 / Davison A² Thm 3.4 / BD Cor 3.3.

**Draft (2026-10-14).**  `bps-proof.tex`, `\input` into
`Hikita-rewrite.tex` as §5 "A second proof of the dimension bound"
(`sec:bps`), with a pointer in §1.2 and an item in the Status section; bib
entries merged by hand into `references.bib`.  Conditional on (H1)–(H3) = JN
polynomial generation, BPS generation, framed BPS rank.  Written in the
rewrite's abelianized notation: the splitting `Â = A_0[x_∞, e^{±1̂}]` is
proved there from Weekes generation (Lemma 5.1) instead of cited.  The two
source PDFs are kept out of the (public) repository.

**Verdict.**  [proved] The deduction is correct given its inputs, and the
inputs are cited accurately (small omissions above).  The BPS/sheaf side
is solid.  The weak link is JN's Hall side (Thm 2.4, Prop 3.7, Lemma 3.6,
Thm 3.5, Cor 3.15): sketched or omitted proofs, deferring to their
K-theoretic paper.

**Comparison with `Hikita-rewrite.tex`.**
- Would replace: §3 entirely (Thm 3.1 and everything feeding it, lines
  ~577–1780), the "abelianization with root denominators" paragraph and
  Prop `loopremoval` in §4, and inputs (I6)–(I10).  Roughly 1350 lines →
  ~200.  Unchanged: Lemmas `generic`, `qsurj`, Thm `map`, Lemmas `flavor`,
  `betti`, Thm `classical` (with `loopremoval` ↦ the BPS bound).
- Costs: reintroduces Jindal–Neguț (July 2026, unrefereed; Thm 2.4 only
  sketched there) and Tsymbaliuk via preprint Lemma 8.1 — dependencies the
  rewrite had shed by proving `B^ν = B_F` elementarily (Lemma `generic`).
  Adds DM integrality, Botta–Davison, DHSM.  Loses the Poincaré polynomial
  formula and the multipartition/Levi picture (BPS gives only dimension).
- Both routes avoid Hausel's formula.

## Files

- `hikita-summary.tex/.pdf` — reader's guide for SLMath QFT participants.
- `openai-preprint/` — verbatim copy of the preprint directory (PDF, source,
  OpenAI's README with BibTeX, the CONTENTS.md entry, Apache-2.0 LICENSE).
