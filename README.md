<!-- solve-problem:d8ad12d4-03ad-4865-a829-263f6914a3cb -->
# One-way functions existence

A [Tangle Solve problem](https://solve.tangle.tools/problems/d8ad12d4-03ad-4865-a829-263f6914a3cb).

## What is the problem?

A one-way function (OWF) is a polynomial-time computable function f : {0,1}* → {0,1}* such that no polynomial-time algorithm inverts it on average: for every probabilistic polynomial-time (PPT) adversary A, over random x ← {0,1}^n,

Pr[A(f(x)) ∈ f⁻¹(f(x))] ≤ negl(n).

**Question:** Do OWFs exist? This is a pure mathematics question: either exhibit one (with a proof that no PPT algorithm inverts it on average), or prove that every efficiently computable function can be efficiently inverted on average, implying none exist.

Key equivalences (Impagliazzo–Naor / Impagliazzo; see also Ostrovsky–Wigderson): OWFs exist iff there are "hard-on-average" NP problems; iff pseudorandom generators exist (Håstad–Impagliazzo–Levin–Luby, 1999); iff pseudorandom functions, private-key encryption, commitment schemes, digital signatures, and zero-knowledge for NP exist. OWF existence strictly implies P ≠ NP (a OWF cannot exist if P = NP), but P ≠ NP does not imply OWFs: hardness needed is *average-case*, not worst-case.

Subtlety in the census phrasing: "P = NP ∩ coNP is enough to kill them" — the precise statement is that if every problem in NP ∩ coNP has polynomial-size circuits (or is easy on average), OWFs collapse; the exact implication requires care. Also note Ostrovsky–Wigderson: if no OWFs exist, still a weak form of hardness persists unless MA ⊆ AM ∩ coAM roughly — the "world without OWFs" is not fully trivialized.

## Why does it matter?

OWFs are the weakest standard cryptographic assumption: essentially all of symmetric cryptography, pseudorandomness, and protocol theory is equivalent to them. A proof of existence would give the first unconditionally secure private-key crypto; a proof of nonexistence would collapse all of modern cryptography's foundations and show every efficiently computable process is average-case easy to invert. It sits strictly between circuit lower bounds and P vs NP, so progress likely requires (and would yield) new circuit-lower-bound techniques — a proof that OWFs exist implies explicit functions with exponential-ish average-case hardness, far beyond current techniques.

## What's already known?

- **Håstad–Impagliazzo–Levin–Luby (1999):** OWFs exist ⟺ pseudorandom generators exist (the "HLKL" theorem) — establishing the equivalence web.
- **Impagliazzo (1995):** Five-world taxonomy: Algorithmica (no OWFs, P = NP), Heuristica (P ≠ NP but no average-case hardness), Pessiland (average-case hard NP languages but no OWFs), Minicrypt (OWFs, no public-key), Cryptomania (public-key crypto). The question is: which world do we live in, i.e., Minicrypt-or-higher vs. Pessiland-or-lower?
- **Candidates:** discrete log, integer factorization, subset-sum, lattice problems (SIS/LWE). None proven; factoring is known to be invertible in BQP (Shor), motivating post-quantum candidates.
- **Ostrovsky–Wigderson (1993):** if no OWF exists, one still gets nontrivial hardness unless certain zero-knowledge/AM collapses occur — nonexistence has strong structural consequences.
- **Barrier:** natural proofs (Razborov–Rudich 1997) — any "natural" circuit lower bound proof would break pseudorandomness itself; a OWF existence proof must evade this barrier. Worst-case-to-average-case reductions are known only within self-reducible/structured problems (lattices, Ajtai 1996), never from NP.

## What would count as solving it?

1. **Existence:** an explicit polynomial-time function f plus a proof that no PPT inverter succeeds with non-negligible probability. This would simultaneously yield (via HILL) unconditional PRGs — an enormous, verifiable consequence.
2. **Nonexistence:** a proof that every polynomial-time computable f has a PPT average-case inverter; equivalently, Pessiland and above are impossible. Referee test: which of Impagliazzo's five worlds the proof eliminates, with a formal theorem statement.
3. **Partial/intermediate results worth pursuing:** proving any explicit function in TFNP-related or time-hierarchy-based form is average-case hard against, say, AC⁰ or restricted circuit classes; unconditional hardness of a candidate against all algorithms of size n² — any quantitative average-case lower bound beyond trivial counting (which gives nonuniform hardness of ~2^n-size circuits for most functions but none explicit).

## How to start

1. Read Impagliazzo's 1995 survey (short, foundational) for the five-worlds framing and the precise statement of what each world contains.
2. Read Goldreich, *Foundations of Cryptography*, Vol. 1, Ch. 2 for the exact definitions (various OWF flavors: weak, distributional, non-uniform) and the equivalence web; the definitions' fine print matters enormously.
3. Natural approaches: (a) try to strengthen time-hierarchy-type diagonalization into average-case hardness — the known obstacle is that diagonalization yields functions hard only at infinitely many lengths or in contrived distributions; (b) try worst-case-to-average-case connections à la Ajtai–Dwork lattices; (c) attack natural proofs (Razborov–Rudich) to understand what any viable proof must avoid.
4. Main obstacle: no known technique produces explicit average-case hard functions; counting gives incompressibility nonconstructively, and derandomization hardness-vs-randomness (Impagliazzo–Wigderson) converts worst-case to pseudorandomity only under an assumption we can't prove.

## Key references

- R. Impagliazzo, "A personal view of average-case complexity," Proc. 10th CCC (1995), 134–147. — Defines the five worlds and situates OWF existence among average-case questions.
- O. Goldreich, *Foundations of Cryptography: Basic Tools*, Vol. 1, Cambridge Univ. Press, 2001. — Rigorous treatment of OWF definitions and their cryptographic equivalences.
- J. Håstad, R. Impagliazzo, L. Levin, M. Luby, "A pseudorandom generator from any one-way function," SIAM J. Comput. 28(4), 1999. — Proves OWF ⟺ PRG, the central structural theorem.
- R. Ostrovsky, A. Wigderson, "One-way functions are essential for non-trivial zero-knowledge," ISTCS 1993. — Shows nonexistence of OWFs forces collapse of zero-knowledge/AM structure.
- A. Razborov, S. Rudich, "Natural proofs," JCSS 55(1), 1997. — Identifies the natural-proofs barrier any OWF-existence proof must evade.
- M. Ajtai, "Generating hard instances of lattice problems," STOC 1996. — Prototype worst-case-to-average-case reduction (for lattices, not NP).

## Warnings

- Do not conflate worst-case and average-case hardness: P ≠ NP does not imply OWFs. Many naive attacks fail here.
- The counting argument (most functions are one-way) is nonconstructive and useless — the function must be polynomial-time computable.
- Beware definitional variants: strong vs. weak OWFs, uniform vs. non-uniform adversaries, the input distribution (uniform over {0,1}^n vs. image distribution). Weak OWFs can be amplified to strong ones (Yao), but only with the right definitions.
- Candidates like factoring are quantumly breakable (Shor); "existence" is unconditional and must not rest on unproven assumptions.
- The census line "P = NP ∩ coNP is enough to kill them" should be treated cautiously — verify the exact implication before relying on it.

---
*`ALGO-000003` · unverified*

## Acceptance guidance

1. **Existence:** an explicit polynomial-time function f plus a proof that no PPT inverter succeeds with non-negligible probability. This would simultaneously yield (via HILL) unconditional PRGs — an enormous, verifiable consequence.
2. **Nonexistence:** a proof that every polynomial-time computable f has a PPT average-case inverter; equivalently, Pessiland and above are impossible. Referee test: which of Impagliazzo's five worlds the proof eliminates, with a formal theorem statement.
3. **Partial/intermediate results worth pursuing:** proving any explicit function in TFNP-related or time-hierarchy-based form is average-case hard against, say, AC⁰ or restricted circuit classes; unconditional hardness of a candidate against all algorithms of size n² — any quantitative average-case lower bound beyond trivial counting (which gives nonuniform hardness of ~2^n-size circuits for most functions but none explicit).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/d8ad12d4-03ad-4865-a829-263f6914a3cb?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000003.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000003)
