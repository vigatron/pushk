# PUSHK Archiver

**Representation-First Compression Pipeline**
*Active entropy management through domain-aware preprocessing*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Preprint](https://img.shields.io/badge/Preprint-telegra.ph-blue)](https://telegra.ph/PUSH-Archiver-representation-first-compression-03-23)

> **Important note (March 2026):** The project has been officially renamed from **PUSH** to **PUSHK** to avoid name collisions with legacy archivers and unrelated projects. All documentation, source code, and references have been updated accordingly.

## Abstract: A New Paradigm for Entropy Management

PUSHK is **not** a classical archiver and **not** just an improved coder. It is a complete compression pipeline that moves the heavy lifting to the data-representation stage. Rather than searching for patterns inside fixed data, PUSHK physically transforms the input so that it becomes *inherently* more compressible by itself.

The March 23, 2026 preprint “PUSH Archiver: representation-first compression” (Viktor Glebov) formalizes this idea at a research level. It examines formal boundaries of provability, compares PUSHK to the Burrows-Wheeler Transform (BWT), and explains why this approach represents a genuine paradigm shift: **representation-first compression**.

This README builds directly on our earlier analysis (“PUSH Архиватор: анализ и потенциал”) and integrates the latest preprint findings.

## 1. Can PUSHK’s Effectiveness Be Formally Proven?

**Short answer:** In the general case — no. In a narrow, restricted domain — yes, partially.

Information theory remains inviolable. Shannon’s entropy is unchanged by any reversible transformation:

$$
H(X) = -\sum p(x) \log_2 p(x)
$$

For any bijective transformation \( T \):

$$
H(T(X)) = H(X) \quad (\Delta = 0)
$$

PUSHK reduces **effective entropy** *relative to the downstream coder* (RLE, Huffman, ANS, etc.):

$$
H_{\text{coder}}(T(X)) = H_{\text{coder}}(X) + \Delta_{\text{eff}}, \quad \Delta_{\text{eff}} \leq 0
$$

**Provable properties:**
- The transformation is fully lossless and reversible.
- For structured tiles, repeat counts increase, unique symbols decrease, and RLE run lengths grow.
- Huffman average code length shrinks when symbol distribution becomes more skewed:

$$
L = \sum p(x) \cdot l(x)
$$

**Non-provable claims:**
- Global superiority over 7-Zip / PAQ on arbitrary files.
- Performance on random, encrypted, or already-compressed data (PUSHK may even increase size).

PUSHK shines on domain-specific data — especially 2D graphics and structured blocks — exactly as identified in our previous analysis.

## 2. Comparison with Burrows-Wheeler Transform (BWT)

The preprint explicitly benchmarks PUSHK against BWT (1994), the classic “representation-first” method.

**BWT** performs one global permutation via lexicographic sorting of all cyclic shifts:

$$
\text{BWT}(T) = \text{last column of the sorted matrix of cyclic shifts}
$$

Both techniques leave true entropy unchanged and create low-entropy regions for later coders. However, they differ significantly:

| Parameter              | BWT (1994)                              | PUSHK (2026)                                              |
|------------------------|-----------------------------------------|-----------------------------------------------------------|
| Scope                  | One global permutation (entire block)   | Multi-level: analysis → clustering → tile segmentation    |
| Adaptivity             | Global suffix sorting                   | Local statistics + entropy control per region             |
| Target domain          | Optimal for text (1D streams)           | Designed for graphics and structured 2D data              |
| Entropy management     | Passive (symbol grouping only)          | Active (creates multiple low-entropy zones deliberately)  |
| Coder synergy          | Boosts RLE + MTF                        | Boosts RLE + dictionary + Huffman/ANS simultaneously      |
| Complexity             | \(O(n \log n)\) sorting                 | Analysis + several targeted local permutations            |
| Worst-case degradation | High on random/encrypted data           | Lower thanks to intelligent segmentation                  |

**Conclusion:** BWT proved that “a clever permutation can be more powerful than any coder.” PUSHK goes further by replacing one global sort with domain-aware, multi-level entropy management.

## 3. Where Does “Compression” End and “Preprocessing” Begin?

Classic monolithic approach:

DATA → COMPRESSION → BITSTREAM


PUSHK pipeline:

DATA → PREPROCESSING (analysis + permutation + dictionary) → COMPRESSION (RLE + Huffman/ANS) → BITSTREAM


The boundary is defined by **intent**, not algorithm:
- If the step is reversible and its goal is final size reduction → it is part of compression.
- If you stop at analysis/sorting without encoding → it is pure preprocessing.

PUSHK deliberately lives on this boundary and is best described as a **hybrid compression pipeline**.

**Philosophical inversion:**
- Classic mindset: “We compress data.”
- PUSHK mindset: “We **make** data compressible.”

This inversion is the core of the project’s potential.

## 4. Harsh Engineering Truth + Greatest Potential Areas

The preprint is refreshingly honest:
- PUSHK is a **strong, genuine idea** for domain-specific entropy reduction.
- It is **not** “a new Shannon,” not universal, and not a drop-in replacement for 7-Zip or PAQ.

**Where PUSHK delivers the biggest gains** (updated from our previous analysis):

- Data-aware compression for graphics, tile-based assets, and structured 2D arrays.
- Adaptive preprocessing pipelines with automatic structure detection.
- Hybrid workflows: PUSHK → PAQ (structural reduction + probabilistic modelling).

**Current status (March 2026):**
- Preprint published.
- Full source code expected within 4–6 months (Q3–Q4 2026). Working on table reindexing optimization
- Benchmarks against PNG tiles, game assets, and scientific datasets planned immediately after code release.

## Final Thoughts

PUSHK does not try to beat Shannon’s limit. It redefines the playing field *before* Shannon’s rules apply. By moving from passive pattern hunting to active entropy management through representation-first transformations, PUSHK opens a new chapter in practical data compression — especially for graphics and any data with inherent 2D or block structure.

We remain excited about its potential exactly as outlined in our earlier analysis. Once the source code drops, we will publish detailed benchmarks and integration guides.

---

**Author:** Viktor Glebov
**Project rename note:** PUSH → PUSHK (March 2026)
**Preprint:** [telegra.ph/PUSH-Archiver-representation-first-compression-03-23](https://telegra.ph/PUSH-Archiver-representation-first-compression-03-23)

Contributions, discussions, and early feedback are welcome. Star the repo if you’re interested in representation-first compression!
