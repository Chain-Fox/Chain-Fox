# Solana Anchor Static Analysis Tools Evaluation Brief

**Tools Evaluated**: Fender, Eloizer, X-Ray  
**Benchmarks**: `sealevel-attacks` synthetic dataset (35 cases) + real-world Anchor dataset (201 buggy commits)  
**Date**: April 2026  

---

## 1. Tool Overview

| Tool | Language | Analysis Level | Key Characteristics |
|------|----------|----------------|----------------------|
| **Fender** | Rust | Anchor AST | Deep integration, aggressive pattern matching, prioritizes recall over precision |
| **Eloizer** | Rust | `syn` + `anchor-syn` (AST-only) | 7 rules, function-name dependent, no dataflow analysis |
| **X-Ray** | Go + C++ | LLVM IR | ANTLR → MLIR → LLVM IR pipeline, supports cross-function analysis in theory, but demo version has ~15 rules |

---

## 2. Synthetic Benchmark: `sealevel-attacks`

| Tool | Recall | Precision | F1 | Key Observations |
|------|--------|-----------|----|------------------|
| **Fender** | 100% | 48.15% | 65.0% | Detects all vulnerabilities but produces many false positives on safe code |
| **Eloizer** | 76.92% | 47.62% | 58.8% | All 10 TP come from a single rule (`missing-signer-check`); other rules underperform |
| **X-Ray** | 53.85% | 70.00% | 60.9% | `BumpSeedNotValidated` and `MissingSignerCheck` reach 100% precision; major blind spots remain |

---

## 3. Real-World Dataset Results (201 Buggy Commits)

### 3.1 Detection Rate (Recall Proxy)

| Tool | Detected Cases | Detection Rate | Avg Alerts per Case |
|------|----------------|----------------|---------------------|
| **Fender** | 198 / 201 | **98.5%** | 5.0 |
| **Eloizer** | 179 / 201 | **89.1%** | 14.0 |
| **X-Ray** | 134 / 201 | **66.7%** | 9.5 |

---

### 3.2 Detection by Vulnerability Type

| Type | Fender | Eloizer | X-Ray |
|------|--------|---------|-------|
| signer_authorization (31) | 100% | 90.3% | 83.9% |
| integer_overflow (8) | 100% | 100% | 100% |
| missing_owner_check (8) | 100% | 75.0% | 62.5% |
| closing_accounts (6) | 100% | 100% | **33.3%** |
| type_cosplay (2) | 100% | 50.0% | 50.0% |
| generic_security (144) | 97.9% | 88.9% | **63.2%** |

---

### 3.3 Key Finding: Precision Collapse in Real-World

Proxy Precision is computed by comparing buggy vs fixed versions:

| Tool | Synthetic Precision | Real-World Proxy Precision | **Drop** |
|------|---------------------|-----------------------------|----------|
| **Fender** | 48.15% | **~6.2%** | **-87%** |
| **Eloizer** | 47.62% | **~6.4%** | **-87%** |
| **X-Ray** | 70.00% | **~7.5%** | **-89%** |

**Alert disappearance after fix**:  
- Fender: **0%**  
- Eloizer: **1.1%**  
- X-Ray: **3.0%**

> In practice: **10–15 alerts must be reviewed to find 1 relevant issue**

---

## 4. Why Synthetic vs Real-World Gap Is So Large

1. **Code Scale**
   - Synthetic: small programs  
   - Real-world: full repositories (state, tests, utils, CPI, etc.)

2. **Fix Strategy**
   - Synthetic: vulnerabilities are fully removed  
   - Real-world: fixes are localized (add checks), patterns remain elsewhere  

3. **Granularity Mismatch**
   - Tools scan **entire repositories**  
   - Fixes affect **only a few files**  

4. **Overly Broad Rules**
   - Fender: `Signer Authorization Check` triggers almost everywhere  
   - X-Ray: `UnvalidatedAccount` fires on many legitimate usages  

5. **Real Bugs Are Simpler**
   - Mostly missing checks → easier to detect  
   - Leads to higher recall but worse precision  

---

## 5. Conclusions

### Key Conclusions

1. **`sealevel-attacks` validates capability, not real-world usability**  
2. **High recall ≠ practical tool** (Fender suffers from extreme noise)  
3. **X-Ray’s precision comes at the cost of recall** (misses ~1/3 of bugs)  
4. **No tool is production-ready alone**  

---

## 6. Recommendations

### For Security Auditing

Adopt a layered approach:

**Fender (broad scan) → LLM filtering → Human review**

- Fender ensures **maximum coverage**
- LLM evaluates **context relevance**
- Humans focus on **high-confidence findings**

---

### For Tool Developers

- Move beyond **pattern matching**
- Build:
  - **Diff-aware analysis**
  - **Semantic reasoning**
  - **AI-assisted detection**

---

### For Researchers

The dataset of **209 buggy/fixed pairs** (plus 52 high-confidence samples) enables:

- Training **LLM-based vulnerability detectors**
- Building **real-world benchmarks**
- Studying **code-change → vulnerability relationships**

---
