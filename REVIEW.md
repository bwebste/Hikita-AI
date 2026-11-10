# Review of `Hikita-rewrite.tex`

Date: 2026-11-10.  Target: `Hikita-rewrite.tex` and `bps-proof.tex` at
commit `a997223`.  Brief: check that the paper (i) gives the
Botta–Tamagni argument for the existence of the surjection
`B^ν(A) → H^*(X_ν)`, and (ii) gives the two dimension arguments in
parallel; and check the mathematics.

Status vocabulary as in `NOTES.md`: [proved] / [checked] / [plausible] /
[unknown].  Sources consulted beyond the repository: the arXiv HTML of
Botta–Tamagni 2608.29400v1 (introduction and Part I; the HTML stops
partway through Part I) and of Teleman 1801.10124v4 (appendix), and the
OpenAI preprint source in `openai-preprint/build/sections/`.

## Verdict in one paragraph

The mathematics that is in the paper is correct as far as I can check:
I reworked every step of §§2–4 and the deduction in §5 and found no
error (details in §3 below).  The paper does **not** yet do the two
things the brief asks for.  (i) The Botta–Tamagni argument is not given
at all: the introduction promises to "briefly summarize this
construction", §2 then says "We use it without giving a proof", and the
citation `[Thm. E, §0.1.6.4]` is imprecise, because Theorem E of
Botta–Tamagni is an action on *based* quasimaps (a Verma-type module),
while the version over `X` that would produce the Hikita map is only
announced in their §0.1.6.4 as forthcoming work.  (ii) The two
dimension arguments exist (§3+§4 and §5) but are not presented in
parallel: they prove differently phrased statements, the reduction
lemmas they share live inside the first proof, and the introduction
describes only the first.  Both are fixable by restructuring, without
new mathematics, except that the sketch of the Botta–Tamagni argument
has to be written and its sign convention pinned down.  Concrete
recommendations are in §5.

## 1. The surjection: what the paper says, what the sources say

### 1.1 What the paper says

- Introduction: "The existence of a surjective map ... follows
  immediately from work of Botta and Tamagni.  ... We only briefly
  summarize this construction."  No summary follows anywhere.
- §2, after Theorem `thm:map`: "This is announced in [Thm. E, §0.1.6.4],
  as a consequence of the Coulomb branch action on the critical
  cohomology of based quasimaps constructed there.  We use it without
  giving a proof."
- Status item 1: "Theorem `thm:map` is announced in [Thm. E]; we do not
  give a proof."

### 1.2 What Botta–Tamagni state (arXiv HTML, v1)

- **Theorem E** [checked against the HTML]: the critical cohomology of
  `QM^ξ(P^1, X)` carries an action of the quantized, flavor-deformed
  BFN Coulomb branch.  Here `QM^ξ` is the space of quasimaps whose
  evaluation at `∞` is a *fixed point* `ξ ∈ X` (their §0.1.2).  Its
  degree-zero component is a point, not `X`.  This is the Verma-module
  picture of Bullimore et al., which they mention in §0.1.6.3.
- **§0.1.6.3 "Vertex functions and Hikita conjecture"** is about the
  *quantum* Hikita conjecture of Dinkins–Karpov–Krylov via vertex
  functions and twisted traces.  It does not state a map
  `B^ν(A) → H^*(X)`.
- **§0.1.6.4 "Relative version over X"**: the stack of quasimaps
  nonsingular at `∞`, fibered over `X` by evaluation, a `(−1)`-shifted
  symplectic fibration; its cohomology (with the relative DT sheaf of
  Kan–Kinjo–Park–Safronov as coefficients) should carry a left action by
  Hecke modifications.  Verbatim: "These statements will be clarified
  by a forthcoming work by the authors."

So Theorem `thm:map` rests on the forthcoming relative version, not on
Theorem E.  The paper's word "announced" is right; the pointer to
Theorem E and the phrase "follows immediately" are not.  The Status
item should say precisely: the surjection needs the relative version of
§0.1.6.4, which is announced, not proved, in 2608.29400v1.

### 1.3 What the OpenAI preprint does

The preprint does not cite Botta–Tamagni for the surjection.  Its §§3–4
(`correspondences.tex`, `stable-pairs.tex`) prove the kernel inclusion
`ker(R → B_F) ⊆ ker(R → H^*_F(X))` at `ħ = 0`, for every flavor torus
and every regular stability, by a finite-dimensional vanishing-cycle
test, and say explicitly (introduction, paragraph on related work) that
this "does not require their entire Coulomb-action construction".
`VERIFICATION.md` §§3–4 found that argument correct.  Its key geometric
input is Lemma 4.1 there: for a `G`-bundle on `P^1` with a section of
the associated `T^*N`-bundle whose value at `∞` is `ν`-stable, the
character line bundle `L_ν` has degree `≥ 0`, and degree `0` forces the
bundle to be trivial.  That lemma is exactly the statement that decides
*which* B-algebra (`ν` or `−ν`) maps to `H^*(X_ν)`.

Whether the preprint "effectively rewrote" Botta–Tamagni is a judgment
I cannot make from the sources: the preprint's test is a
finite-dimensional shadow of the quasimap construction, and the
Botta–Tamagni paper does not contain the Hikita map.  The sentence in
the introduction making this accusation should at least be checked
against the relative version when it appears.

### 1.4 What should be written

A subsection "The comparison map, after Botta–Tamagni" with the
following content would satisfy the brief.  Everything below is
[plausible]: it is how the forthcoming construction must work, but I
have not seen it.

1. *The module.*  Let `QM^d` be the quasimaps `P^1 ⇢ X_ν` of degree
   `d ∈ π_1(G) = Z^{Q_0}` that are nonsingular at `∞`, with
   `ev_∞ : QM^d → X_ν`, and let `M_d` be its critical cohomology,
   equivariant for `F` and for the loop rotation `C^×_ħ` fixing
   `0, ∞ ∈ P^1`.  Then `QM^0 = X_ν` and `M_0 = H^*_{F×C^×_ħ}(X_ν)`.
2. *The action.*  Hecke modifications at `0 ∈ P^1` make
   `M = ⊕_d M_d` a graded module over `A_{F,ħ}`: an element of charge
   `c` maps `M_d → M_{d+c}`.  The subalgebra `R_ħ` of classes over the
   base point acts on `M_0` by the equivariant Chern classes of the
   tautological bundles, that is, through the Kirwan map `κ`.
3. *Stability.*  If `QM^d ≠ ∅` then `deg L_ν ≥ 0` on it, with equality
   only for `d = 0` (the preprint's Lemma 4.1).  Writing `deg L_ν` as a
   linear function of `d` in the paper's conventions pins down the sign:
   one of `deg_ν(d) ≥ 0` or `deg_ν(d) ≤ 0` holds for all `d` with
   `M_d ≠ 0`.
4. *The B-algebra.*  Hence for `k > 0` one of the two products
   `A_{[-k]}A_{[k]}` or `A_{[k]}A_{[-k]}` kills `M_0`, so `A_{[0]}` acts
   on `M_0` through `B^{±ν}`.  The paper's convention (`B^ν` of
   Hilburn–Kamnitzer–Weekes §5.7) must come out with the `+` sign; this
   is the one place where the sign convention of the whole paper is
   decided, and it should be shown, not asserted.
5. *The map.*  `Φ(b) = b · 1` for `1 ∈ H^0(X_ν)`.  Then `Φ[f] = κ(f)`
   for `f ∈ R_ħ`, and `Φ` is onto because `κ` is (McGerty–Nevins).  The
   content of Theorem `thm:map` is therefore the inclusion of kernels
   `ker(R_ħ → B^ν) ⊆ ker κ`; stating it in that form makes clear what
   is being imported.

Alternative, which would make Theorem `thm:classical` unconditional:
include the preprint's §§3–4 argument (about six pages after
compression), which proves exactly `ker(R → B_F) ⊆ ker κ` at `ħ = 0`
with flavor.  With Lemma `lem:generic` (`B^ν_F = B_F`) this gives
`Φ : B^ν_F → H^*_F(X_ν)` for all generic `ν`, which is all that
Lemma `lem:flavor` (first map), Proposition `prop:loopremoval` (for
`Q^+` with flavor `C^×_u`) and Theorem `thm:classical` use.  Only the
quantized statement would then depend on Botta–Tamagni.  Given that the
paper's purpose is a checkable proof, I would do this and present the
quasimap picture as the conceptual explanation.

## 2. The two dimension arguments: are they parallel?

### 2.1 What is there

| | Route A (§3 + §4) | Route B (§5) |
|---|---|---|
| Statement proved | `Φ : B_0 → H^*(X_{ν_det})` is an isomorphism (Prop. `prop:loopremoval`), via Thm. `thm:loops` for `Q^+` | `dim B_0 ≤ dim H^*(X_{ν_det})` (Thm. `thm:bps`), then Cor. `cor:bps` |
| Uses `Φ` inside the count? | Yes: `F'_L = Φ(F_L)`, and Prop. `prop:top` uses `Φ` onto `H^{2d_max}(X)`; again for `Q^+` with flavor in loop removal | No; `Φ` enters only in Cor. `cor:bps` |
| External inputs | Teleman's abelianization, Hausel–Sturmfels, Greene–Zaslavsky, hyperkähler rotation, Brion's localization, Botta–Tamagni for `Q^+` with flavor | Jindal–Neguț (H1)–(H2), Botta–Davison, Davison–Hennecart–Schlegel Mejia, preprint Lemma 8.1 |
| Status | complete given cited results | conditional on sketched proofs |
| Extra output | Poincaré polynomial, filtration by Levi subgroups, decomposition theorem for `χ` (§6) | none |

Both routes are correct as deductions (see §3).  They are not parallel
in presentation:

- They target different statements.  Route A never isolates the
  inequality the introduction says is "all we need"; Route B proves the
  inequality and then re-derives the isomorphism.
- The reduction from Theorem `thm:main` to the inequality at
  `(Q, ν_det, F = 1, ħ = 0)` uses Lemma `lem:generic` (§2),
  Lemma `lem:betti` and Lemma `lem:flavor` (§4, after Route A) and the
  surjectivity of `Φ`.  It is carried out only inside the proof of
  Theorem `thm:classical`, at the end of Route A, and then re-used by
  Corollary `cor:bps` with the sentence "the proof of Theorem
  `thm:classical` goes through".
- The introduction describes Route A in detail (items (1), (2)) and
  Route B in one sentence at the end of §1.2.  Item (2) is phrased as a
  statement about `X` alone, `H(Q,v,w) ≤ dim H^*(X_ν)`, but the proof
  uses `Φ` essentially (Lemma `lem:reduction` works with
  `F'_L = Φ(F_L)`); Status item 4 says so, the introduction does not.
- The paragraph in the introduction beginning "Together with the
  localization theorem, this lemma gives us a useful reduction" asserts
  that Theorem `thm:main` for `(Q, v, w, F, ν)` implies it for the fixed
  components of a flavor cocharacter.  This is neither proved nor used.
  It is the idea behind Proposition `prop:loopremoval`, but as stated
  (for a general cocharacter, with several fixed components) it would
  need a Coulomb-side identification at each component, which the paper
  does not have.  Either tie it to `prop:loopremoval` or drop it.

### 2.2 Suggested structure

1. §2 *The comparison map and the reduction.*  Lemmas `lem:generic`,
   `lem:qsurj`; the Botta–Tamagni sketch (§1.4 above) and Theorem
   `thm:map`; then move Lemmas `lem:betti` and `lem:flavor` here and
   state

   > **Proposition (reduction).**  Suppose `dim B_0 ≤ dim H^*(X_{ν_det})`
   > for every quiver, with `B_0` computed at `F = 1`, `ħ = 0`.  Then
   > Theorem `thm:main` holds for every `Q, v, w, F, ν` generic.

   with the proof now in Theorem `thm:classical`.
2. §3 *First proof of the dimension bound: loops and Levi subgroups.*
   Theorem `thm:loops`, then Proposition `prop:loopremoval` restated as
   the bound (its proof gives equality of kernels, which is more; keep
   that as a corollary).
3. §4 *Second proof: BPS cohomology.*  Theorem `thm:bps` as is.
4. A short *Comparison* subsection (expanding Remark
   `rem:bps-compare`) with the table above, saying where `Φ` enters in
   each route and what each route gives beyond the dimension.
5. §5 *The quiver variety side* (current §6), unchanged.
6. Rewrite the introduction's "The argument" paragraph to match.

## 3. Mathematical check

I re-derived every step below by hand.  Nothing marked otherwise is
[checked].

### §1–§2

- Genericity ⇒ semistable = stable with trivial stabilizer: the
  `details` argument is right (subrepresentations of dimension `(b,0)`
  and `(b,1)`).
- `ν_det`-stability = images of `W` generate `V` (I5): right, with
  `θ̂ = (ν, −ν·v)` as defined.
- **Lemma `lem:generic`**: right.  The step "every charge component
  `A^{(c)}` with `c ≠ 0` and `deg_ν(c) = 0` lies in `J_ν`" is needed and
  is justified.  Uses Weekes's generation (I1) at `ħ = 0`.
- **Lemma `lem:qsurj`**: right, but the sentence "`c` lies in the same
  filtered piece as `[m_i, m_j]`, because the subquotients of the
  filtration are free over `C[ħ]`" compresses an argument: the support
  filtration is indexed by closed `G_O`-stable subsets, every quotient
  `A_{≤Z}/A_{≤Z'}` has a finite filtration with free subquotients and is
  therefore `ħ`-torsion-free, so `ħc ∈ A_{≤Λ'}` forces `c ∈ A_{≤Λ'}`.
  One sentence would do.  The induction is on cohomological degree,
  which drops by `2` when `ħ` is divided out; say so.
- **Theorem `thm:map`**: see §1.  As stated ("the surjective maps ...
  induce a surjective homomorphism") the content is an inclusion of
  kernels; state it that way.

### §3 (loops at every vertex)

- **Proposition `prop:teleman`** [checked against Teleman's appendix]:
  Theorem 6 there reads `C(G; E) ≅ C(H; E ⊖ (g/h)^{⊕2})/W` for any
  representation whose weights contain the roots, "compatibly with the
  embeddings of §6.2".  This is what the paper uses, including the
  compatibility.  Two remarks.  (a) This theorem is **load-bearing**
  and is not in the input list (I1)–(I12): the definition of `F_L`,
  the derivation `η_{k,j}` preserving `A`, and the expansion of the cut
  relation into dressed monopoles all need `A` to be *all* of
  `(⊕ S r_λ)^W`, not just contained in it.  It should be input (I0) or
  similar, with the statement quoted.  (b) The compatibility of
  Teleman's embeddings with BFN's `ι_*^{-1}` is argued only in §4
  ("the weights of the chosen loops contribute `±eu_λ` to `r_λ` for
  minuscule `λ`"); put a forward reference at `prop:teleman`.  Teleman's
  Remark 8.1 concerns extensions beyond the root hypothesis and does
  not restrict Theorem 6.
- *Degrees* (§3.2): for charge-zero `λ`, `deg r_λ = Σ_{B'}(−⟨β,λ⟩)_+`
  is right in either of the two BFN gradings (they differ by a function
  of the charge; `VERIFICATION.md` §2).  Only charge-zero degrees are
  used (for `λ_m`), so Status item "degree of `r_λ`" could be closed by
  this remark.
- **Proposition `prop:toric`**: right.  Cocircuits = bonds, cuts =
  disjoint unions of bonds, unimodularity, level, top degree
  `= T_Γ(1,0)`.  The disconnected case (`q_I = 1`, empty hypertoric
  variety) is handled.  Checked on Example `ex:A2loops`: `J_m = (a,b,c)^2`,
  top degree `3 = T_{C_4}(1,0)`, minimal resolution of `C^2/(Z/4)`.
- **Example `ex:A2loops`**: `dim X = 8`, `P_X = 1 + 2q + q^2`,
  `d_max = 2`; arithmetic checks.  Gieseker formula: `r = n = 2` gives
  `1 + q + 2q^2 + q^3`, which agrees with Nakajima–Yoshioka.
- **Proposition `prop:filt`**: right in every step.  In particular:
  `η_{k,j}` is a derivation, `W`-equivariant, preserves `A` and `I_B`,
  and is zero on `B`; `σ_{k,j} = P^m_{k,j} − P_{k,j}`; `S^H` is
  generated over `(S^f)^{H_1}` by the `P_{k,j}`; the degree count gives
  `δ_m` (arrow by arrow, loops of `Q'` included with `c_{kk}` counting
  twice); in the cut relation the exponent of `g` is `min(s_D,s_E)` on
  edges across the cut and `1` on framing edges of parts in `I`, zero
  otherwise, so `g = ±q̃_I`; the pairs with `wa + w'b = s` are the
  `H`-orbit of `(a,b)` with stabilizer `H_I`; the averaging produces
  `J_m^{W_m}`.
- **Lemma `lem:restr`**: right.  (3) uses Proposition `prop:filt`(2)
  for `Q_{M_m}`, which is legitimate since `prop:filt` is proved for
  every quiver with a loop at every vertex.
- **Lemma `lem:ind`**: right.  `μ ∘ ι̃ = μ_M` by the Sylvester
  correction; `U = U_M` both ways; `τ_ζ` preserves `μ_M` and stability
  and is homotopic to the identity; the core lies in `X(M)^∘` after
  translation.
- **Proposition `prop:detect`**, **Lemma `lem:socle`**,
  **Proposition `prop:top`**: right.  Note that `prop:top` is where `Φ`
  (surjective) is used to bound `dim 𝔏 ≤ d_max`; the by-hand
  construction of Lemma `lem:comp` only gives `≥`.
- **Lemma `lem:comp`**: right.  `dim 𝔸 − Σ_k C(v_k−1,2) − dim B_o = d_max`
  via `2C(v,2) − C(v−1,2) − C(v+1,2) = −1`; `μ(p_0) = 0`; stability of
  `p_0` by descending induction along `≺`; fibers of `Y^∘ → 𝔏_o` are
  free `B_o`-orbits; distinctness of the `𝔏_o`.
- **Corollary `cor:topclass`**, **§3.7**, **Corollary `cor:cusp`**:
  right, including the case `S_G/J_G = 0`.
- **Remark `rem:hausel`**: the factorization `A_fr = A_0 H` from
  Remark `rem:kirwan`(4) is right (`d_m = d_{m_I} + d_{m'} + e`,
  `deg q_I = e + w·l(m_I)`).

### §4 (deformations)

- **Lemma `lem:flavor`**: right.
- **Lemma `lem:betti`**: right; the real ball around `−iθ` meets the
  Zariski open `U` because `iR^{Q_0}` is Zariski dense.
- **Proposition `prop:loopremoval`**: right in every step.  Quiver side:
  `H^*_u(Y_ρ)_𝔫 = 0` for `ρ ≠ 1` because `f − u^2Σn_d^2` is a unit at `𝔫`
  acting nilpotently; `Y_1 = X`.  Coulomb side: `r^+_λ = g_λ r_λ`,
  `S^+_λ(p) = S_λ(g_λ p)`, `σ_λ ∉ 𝔫`, so `A^+_𝔫 = A[u]_𝔫`.  Conclusion by
  graded Nakayama on `E = (K_B + K_X)/K_B`.  The localization theorem is
  cited as Brion Thm. 3; I could not check the number (Status lists it
  implicitly; `VERIFICATION.md` had the same problem with the preprint's
  "Lemma 4").
- **Theorem `thm:classical`**: right.

### §5 (BPS)

- **Lemma `lem:bps-split`**: right (`r̂_{(μ,k)} = r_{μ−k1} e^{k1̂}`,
  `eu` unchanged, the generation argument, `Σx̂ = b + Dx_∞`).
- `Θ`: right; (Θ1)–(Θ3) right; `−b/D` is forced by (Θ2).
- **Theorem `thm:bps`**: the deduction from (H1)–(H3) and Lemma
  `lem:hall-coulomb` is right, including the cases `v = 0` and
  `w = 0`.  Lemma `lem:hall-coulomb` is a sketch resting on the
  preprint's Lemma 8.1, as the paper says.  Status item 3 is accurate.
- The `% COMMENT` at the top of `bps-proof.tex` says credit for this
  section "is still to be settled".  That must be resolved before the
  paper circulates.

### §6 (quiver variety side)

Read, not reworked line by line; it is not used in the proof.  The
local model, the stalk computation via `K_M ≅ Q ⊠ K^𝔰_M` and the
contraction to `0`, and the support argument are consistent with §3.
Lemma `lem:localmodel`'s inverse uses the Chinese remainder theorem
and Sylvester as in `lem:ind`.

## 4. Citations and inputs

- Add Teleman's Theorem 6 to the input list (see §3).
- Replace `[Thm. E, §0.1.6.4]` by a precise description (see §1.2).
- The introduction says "slop dump of Oct. 7, 2026" and "preprint dated
  24 September 2026"; `NOTES.md` says the release is of 24 September.
  Make the dates consistent.
- Status item 2 is a good list; add Brion's theorem number and the form
  of Teleman's compatibility statement.
- `VERIFICATION.md` items 1–16 for the preprint have been absorbed where
  relevant (grading convention, `w = 0`, finitely many cones are no
  longer needed in this write-up).

## 5. Recommended changes, in priority order

1. Write the Botta–Tamagni sketch (§1.4), with the sign convention
   derived from the degree of `L_ν`, and restate Theorem `thm:map` as an
   inclusion of kernels.  Correct the citation and Status item 1.
2. Decide whether to include the preprint's finite-dimensional proof of
   the kernel inclusion at `ħ = 0`.  Doing so makes Theorem
   `thm:classical` unconditional and confines the dependence on
   Botta–Tamagni to the quantization.
3. Restructure §§2–5 as in §2.2: reduction proposition in §2, two proofs
   of one stated bound, comparison subsection.  Rewrite §1.2 and the
   introduction's items (1)–(2) accordingly, saying where `Φ` is used in
   Route A.
4. Remove or justify the introduction's paragraph on reduction to
   fixed components of a flavor cocharacter.
5. Add Teleman's theorem to the inputs with a forward reference to the
   `±eu_λ` remark; add the one-sentence torsion-freeness argument to
   Lemma `lem:qsurj`.
6. Settle the attribution of §5.
7. Resolve the `\Ben{...}` note once a human check is complete; this
   review is a machine check and does not discharge it.

## Explicit computations performed

| Check | Result |
|---|---|
| Exponent of `g` in the cut relation, all four cases of `(D ∈ I, E ∈ I)` and framing | `min(s_D,s_E)` across the cut, `1` on framing edges of `I`, else `0` ✓ |
| Degree count `Σ(−⟨β,λ_m⟩)_+ = δ_m`, arrows and framing | ✓ |
| `σ_{k,j} = P^m_{k,j} − P_{k,j}` and `H`-invariance | ✓ |
| `S^H` generated over `(S^f)^{H_1}` by `P_{k,j}` | ✓ |
| `dim 𝔸 − Σ C(v_k−1,2) − dim B_o = d_max` | ✓ |
| `μ(p_0) = 0`, stability of `p_0` | ✓ |
| Example `ex:A2loops`: `J_m`, top degree `3`, `dim X = 8`, `P_X` | ✓ |
| Gieseker `r = n = 2` | `1 + q + 2q^2 + q^3` ✓ |
| `r̂_{(μ,k)} = r_{μ−k1} e^{k1̂}`, `Σx̂ = b + Dx_∞` | ✓ |
| `(Θ1)`–`(Θ3)` | ✓ |
| `w = 0` case: `1 ∈ I_B` | ✓ |
| Teleman Thm. 6 statement and compatibility clause | matches citation ✓ |
| Botta–Tamagni Thm. E, §0.1.6.3, §0.1.6.4 | Thm. E is the based-quasimap action; Hikita map only announced in §0.1.6.4 |
