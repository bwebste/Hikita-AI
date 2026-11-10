# Hikita-AI

A reader's guide to the OpenAI preprint
[*The equivariant cohomological Hikita conjecture for arbitrary quivers*](https://github.com/openai/math/blob/main/preprints/The-equivariant-cohomological-Hikita-conjecture-for-arbitrary-quivers-September-24-2026/main.pdf)
(family 044 of the `openai/math` release, 24 September 2026), prepared for
participants in the SLMath program on quantum field theory.

- [`hikita-summary.pdf`](hikita-summary.pdf) — the guide (7 pages).
- [`VERIFICATION.md`](VERIFICATION.md) — section-by-section verification notes: what was checked, what passed, what should be expanded.
- [`REVIEW.md`](REVIEW.md) — review of `Hikita-rewrite.tex`: whether it gives the Botta–Tamagni argument for the surjection and the two dimension arguments in parallel, plus a step-by-step mathematical check.
- [`comments-questions.md`](comments-questions.md) — comments, questions and requests about the summary or the proof.
- [`openai-preprint/`](openai-preprint/) — the preprint itself (PDF and LaTeX source), copied verbatim from `openai/math` under its Apache-2.0 license; see `SOURCE.md` there.

The preprint is unrefereed and has no Lean formalization.  The guide was
drafted by Claude at Ben Webster's request from the LaTeX source; it
reorganizes the argument for readability and does **not** verify the proofs.
