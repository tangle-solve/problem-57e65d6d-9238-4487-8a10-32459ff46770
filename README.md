<!-- solve-problem:57e65d6d-9238-4487-8a10-32459ff46770 -->
# Positivity of arbitrary linear recurrences

A [Tangle Solve problem](https://solve.tangle.tools/problems/57e65d6d-9238-4487-8a10-32459ff46770).

## What is the problem?

Given a rational (or integer) linear recurrence sequence (LRS) ⟨u_n⟩_{n≥0} satisfying u_{n+d} = a_{d-1}u_{n+d-1} + … + a_0 u_n with a_i ∈ ℚ and specified initial values u_0,…,u_{d-1} ∈ ℚ, decide whether u_n ≥ 0 for **all** n ≥ 0. This is the **Positivity Problem**: given ⟨u_n⟩, decide (∀n) u_n ≥ 0; the **Ultimate Positivity Problem** asks whether ∃N ∀n ≥ N: u_n ≥ 0. The unrestricted problem (arbitrary order d, no structural restriction on the characteristic roots) is open for Positivity; Ultimate Positivity is known to be decidable for LRS of order at most 9 (decidable, with hardness for order 10+ conditional on certain number-theoretic conjectures — verify exact thresholds). The key structural distinction: an LRS is **simple** if each dominant characteristic root has multiplicity one. Decidability is known for simple LRS of order at most 9 (via Baker's theorem on linear forms in logarithms) and, for certain questions, for non-simple LRS of order at most 6 — the obstacle for higher orders/multiplicities is precisely handling multiple dominant roots whose contributions interact via polynomial-in-n factors.

## Why does it matter?

Positivity is the canonical reachability/safety question for linear dynamical systems: is the system's state confined to a half-space forever (invariant checking, stability verification)? It sits in the Skolem Problem family (is u_n = 0 for some n?), and progress on positivity for higher orders directly advances the open decidability of Skolem itself. It also gates results in probabilistic verification (e.g., reachability in Markov chains, whose transition probabilities are LRS-like), quantum automata equivalence questions, and control theory's invariant-region analysis. Software/model-checking tools for hybrid systems would inherit complete decision procedures if this were resolved.

## What's already known?

- Positivity is decidable for LRS of order d ≤ 5 (Ouaknine–Worrell), and for **simple** LRS of order d ≤ 9 (arXiv:1309.1550). The approach: for simple LRS, dominant-root terms are of the form |λ_i|^n cos(nθ_i + φ); reducing to integer powers and applying **Baker's theorem** on linear forms in logarithms gives effective Diophantine bounds on how long "near-cancellation" between dominant terms can persist.
- Ultimate Positivity is decidable for order ≤ 9; the same paper shows that for simple LRS of higher order, decidability would follow from resolution of certain deep conjectures (Schanuel's conjecture appears in the broader program — verify). There are hardness indications that full decidability for higher orders may be extremely difficult or conditionally impossible.
- The **multiplicity** barrier: when dominant roots have multiplicity > 1, terms carry polynomial factors n^k, and Baker-type bounds do not directly control sign of sums like n^k|λ|^n cos(nθ) + …; this is why non-simple decidability stops around order 6 (verify exact bound).
- Related: the Skolem Problem is decidable up to order 4 (verify current best: recently claimed for order 5 in some restricted settings), and the Ore–Sato theorem on exponential-polynomial structure underlies all decompositions.

## What would count as solving it?

1. **Full decidability:** an algorithm that, given any rational LRS of arbitrary order, decides Positivity (with proven termination and correctness) — this would also resolve Ultimate Positivity.
2. **Undecidability:** a proof that Positivity for rational LRS of some bounded order (or arbitrary order) is undecidable (many expect this to be hard; no reduction is known).
3. **Interim goals a referee would value:** decidability for simple LRS of all orders (requires new Diophantine approximation bounds beyond Baker, or resolution of the relevant cases of Schanuel); decidability for non-simple LRS up to order 7–9; unconditional decidability of Ultimate Positivity beyond order 9.
4. **Conditional results:** algorithms whose correctness relies only on explicitly stated, checkable conjectures on linear forms in logarithms of algebraic numbers.

## How to start

1. Read arXiv:1309.1550 (Ouaknine–Worrell, simple LRS) §1–4 carefully: the reduction of Positivity to comparing sums of cosines of powers of algebraic numbers, then Baker's theorem giving the bound N such that sign is determined by n ≤ N. Understand exactly where multiplicity-one is used.
2. Read the 2014 "Positivity Problems for Low-Order Linear Recurrence Sequences" paper for the non-simple low-order techniques (root-separation arguments).
3. Attack the **non-simple dominant-root case**: for a pair of conjugate dominant roots of multiplicity m, positivity of n^m ρ^n cos(nθ) + lower-order polynomial terms. Consider whether Quantifier Elimination over reals plus effective Diophantine approximation of θ/2π by rationals (continued fractions / Baker) can decide the eventual sign pattern.
4. Alternative angle: try to prove hardness — encode an undecidable problem into sign of an LRS of fixed order; note the total failure of all such attempts historically (Turing, Mignotte, and others), and understand why the algebraic structure resists encoding.

Main obstacle: no effective lower bound is known for linear forms in logarithms when multiplicities force polynomial-in-n prefactors and three or more dominant roots interact.

## Key references

- J. Ouaknine and J. Worrell, *Positivity Problems for Low-Order Linear Recurrence Sequences*, Proc. STACS 2014. Establishes decidability of Positivity for LRS of order ≤ 5 (and Ultimate Positivity to order 9), with Baker's theorem as the key tool; proves conditional hardness beyond. (Verify exact bibliographic details.)
- J. Ouaknine and J. Worrell, *On the Positivity Problem for Simple Linear Recurrence Sequences*, arXiv:1309.1550. Proves Positivity decidable for simple LRS of order ≤ 9 by reducing to sign analysis of sums of cosines with algebraic frequencies and applying Baker's theorem; identifies Schanuel-dependent barriers for higher orders. https://arxiv.org/abs/1309.1550
- T. W. Halava, T. Harju, M. Hirvensalo, J. Karhumäki, *Skolem's Problem — On the Border between Decidability and Undecidability*, TUCS Technical Report 683, 2006. Surveys the Skolem/positivity problem family, undecidability landscape, and the number-theoretic obstacles. (Verify.)
- A. Baker, *Linear forms in the logarithms of algebraic numbers* (I–III), Mathematika 1966–67. The Diophantine tool underpinning all effective bounds in this area.

## Warnings

- The census record cites work only up to the mid-2010s; check for newer results (e.g., progress on Skolem for order 5) before claiming state of the art. (Verify.)
- Do not conflate Positivity with Skolem (zero-crossing); they are related but distinct, and neither implies the other directly.
- Multiplicity of dominant roots is the real barrier, not order per se — orders are proxies for how many dominant roots with multiplicity can coexist.
- Baker's theorem gives enormous explicit bounds; "decidable in principle" via Baker does not mean a practical algorithm, but does count as decidability.
- Beware the folklore misconception that undecidability follows from Hilbert's Tenth Problem — no such reduction is known; sign of LRS is far more structured than general exponential Diophantine equations.

---
*`ALGO-000179` · unverified*

## Acceptance guidance

1. **Full decidability:** an algorithm that, given any rational LRS of arbitrary order, decides Positivity (with proven termination and correctness) — this would also resolve Ultimate Positivity.
2. **Undecidability:** a proof that Positivity for rational LRS of some bounded order (or arbitrary order) is undecidable (many expect this to be hard; no reduction is known).
3. **Interim goals a referee would value:** decidability for simple LRS of all orders (requires new Diophantine approximation bounds beyond Baker, or resolution of the relevant cases of Schanuel); decidability for non-simple LRS up to order 7–9; unconditional decidability of Ultimate Positivity beyond order 9.
4. **Conditional results:** algorithms whose correctness relies only on explicitly stated, checkable conjectures on linear forms in logarithms of algebraic numbers.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/57e65d6d-9238-4487-8a10-32459ff46770?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000179.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000179)
