---

# PUSHK Compression Benchmark

This repository contains benchmark results for compressing a structured data file using multiple popular compression algorithms and the experimental **PUSHK** pipeline.

---

## 📊 Benchmark: `backobjs.cells`

| File                     | Size (bytes) | % of original | Compression (%) | Δ vs best (bytes) |
| ------------------------ | -----------: | ------------: | --------------: | ----------------: |
| backobjs.cells           |        16384 |       100.00% |           0.00% |            +14900 |
| backobjs.cells.bz2       |         3688 |        22.51% |          77.49% |             +2204 |
| backobjs.cells.arj       |         3419 |        20.87% |          79.13% |             +1935 |
| backobjs.cells.zip       |         3350 |        20.45% |          79.55% |             +1866 |
| backobjs.cells.gz        |         3205 |        19.56% |          80.44% |             +1721 |
| backobjs.cells.rar       |         2323 |        14.18% |          85.82% |              +839 |
| backobjs.cells.xz        |         1848 |        11.28% |          88.72% |              +364 |
| backobjs.cells.lzma      |         1803 |        11.00% |          89.00% |              +319 |
| backobjs.cells.7z        |         1569 |         9.58% |          90.42% |               +85 |
| **backobjs.cells.pushk** |     **1484** |     **9.06%** |      **90.94%** |      **0 (best)** |

---

## 📌 Notes

* Original file size: **16384 bytes**
* **Best result: PUSHK**
* PUSHK compressed data:

  * **1458 bytes (pure compressed stream)**
  * **+26 bytes container header**
* Final size:

  * **1484 bytes total**

### Header includes:

* File ID
* Format version
* Data type
* CRC checksum
* Other minimal metadata

---

## 🧠 About PUSHK

PUSHK is not a traditional compressor in the classical sense.

Instead of directly encoding the input stream, it applies a **preprocessing pipeline** that:

* Reorders data blocks
* Clusters structures by entropy and similarity
* Extracts repeating patterns (tile-aware)
* Reduces entropy before final encoding

Final stage uses standard techniques (e.g. RLE + Huffman), but on **transformed data**.

---

## ⚖️ Key Insight

> PUSHK does not just compress data — it makes data more compressible.

This allows it to outperform general-purpose compressors on structured inputs.

---

## ⚠️ Disclaimer

* Results are **data-dependent**
* PUSHK is optimized for **structured / tile-like data**
* Performance may vary on:

  * random data
  * already compressed files
  * high-entropy inputs

