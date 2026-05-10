# 📐 A Theoretical Dive into Copulas
### Deriving Copula Structures, Kendall's Tau, and Concordance Indices

![Language](https://img.shields.io/badge/Language-Mathematical%20Statistics-9B59B6?style=flat)
![Theory](https://img.shields.io/badge/Type-Statistical%20Theory-blue?style=flat)
![Course](https://img.shields.io/badge/Course-STAT%20590%20Survival%20Analysis-navy?style=flat)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

## Overview

This project provides a rigorous theoretical treatment of **copula theory**, deriving copula structures, Kendall's tau, concordance indices, copula densities, and maximum likelihood estimators for five distinct copula families. Starting from first principles — Sklar's Theorem and the Laplace transform — each copula is built from the ground up and its dependence properties are fully characterized.

The paper demonstrates how vastly different dependence structures can arise even when marginal distributions are identical, and why measures like Kendall's tau and the concordance index are more informative than standard Pearson correlation for capturing complex, nonlinear, or tail-driven dependence.

---

## Copulas Covered

| Copula | Family | Dependence Range | Tail Dependence |
|--------|--------|-----------------|-----------------|
| Independence | Archimedean | None (τ = 0) | None |
| Fréchet-Hoeffding Lower Bound | — | Perfect negative (τ = −1) | Lower |
| Fréchet-Hoeffding Upper Bound | — | Perfect positive (τ = 1) | Upper |
| **Gumbel** | Archimedean | Positive only (0 ≤ τ < 1) | Upper tail |
| **Clayton** | Archimedean | Positive only (0 ≤ τ < 1) | Lower tail |
| **Gaussian** | Elliptical | Full range (−1 ≤ τ ≤ 1) | None |

---

## Key Results

### Kendall's Tau (τ) and Concordance Index (κ)

| Copula | τ | κ | Parameter Range |
|--------|---|---|-----------------|
| Independence | 0 | 1/2 | — |
| Fréchet Lower | −1 | 0 | — |
| Fréchet Upper | 1 | 1 | — |
| Gumbel | 1 − 1/θ | 1 − 1/(2θ) | θ ≥ 1 |
| Clayton | θ/(θ+2) | (θ+1)/(θ+2) | θ > 0 |
| Gaussian | (2/π) arcsin(ρ) | (1/π) arcsin(ρ) + 1/2 | −1 ≤ ρ ≤ 1 |

The concordance index κ and Kendall's tau τ are directly related for all continuous copulas via:

```
κ = (τ + 1) / 2
```

### MLE Estimators

| Copula | MLE | Tau-Based Quick Estimator |
|--------|-----|--------------------------|
| Gumbel | argmax Σ ln c(uᵢ, vᵢ), solved numerically | θ̂ = 1/(1 − τ̂) |
| Clayton | argmax Σ ln c(uᵢ, vᵢ), solved numerically | θ̂ = 2τ̂/(1 − τ̂) |
| Gaussian | nρ³ − Bρ² + (A−n)ρ − B = 0 (Cardano's formula) | ρ̂ = sin(πτ̂/2) |

---

## Mathematical Background

### Sklar's Theorem
The backbone of copula theory: for any joint CDF H(x₁, x₂) with continuous marginals F₁ and F₂, there exists a unique copula C such that:

```
H(x₁, x₂) = C(F₁(x₁), F₂(x₂))
```

This allows any joint distribution to be decomposed into its marginals and a copula that captures the full dependence structure independently of the marginal forms.

### Archimedean Copulas
Gumbel, Clayton, and Independence copulas are all Archimedean — they share the structure:

```
C(u₁, ..., uₐ; θ) = φ⁻¹(φ(u₁; θ) + ... + φ(uₐ; θ); θ)
```

where φ is the generator function, derived via the Laplace transform of a non-negative random variable.

| Copula | Generator φ(t) | Inverse Generator φ⁻¹(t) | Source Distribution |
|--------|---------------|--------------------------|---------------------|
| Independence | −ln(t) | e^(−t) | Degenerate (S ≡ 1) |
| Gumbel | (−ln t)^θ | exp{−t^(1/θ)} | Positive Stable(1/θ) |
| Clayton | t^(−θ) − 1 | (1 + t)^(−1/θ) | Gamma(1/θ, 1) |

### Kendall's Tau Formula
Derived from concordance probability:

```
τ = 4∫∫ C(u,v) dC(u,v) − 1
```

For Archimedean copulas this simplifies to:

```
τ = 1 + 4∫₀¹ φ(t)/φ'(t) dt
```

---

## Paper Structure

```
1. Introduction        — Motivation and overview of copula theory
2. Background          — Sklar's Theorem, Kendall's tau, concordance index
3. Derivations         — Full mathematical derivations for all 6 copulas:
   ├── Independence Copula
   ├── Fréchet-Hoeffding Bounds (Upper & Lower)
   ├── Gumbel Copula (+ MLE)
   ├── Clayton Copula (+ MLE)
   └── Gaussian Copula (+ MLE)
4. Results             — Summary tables of all copulas, densities, and metrics
5. Conclusion          — Synthesis and practical implications
6. References
```

---

## Key Insights

**Gumbel vs. Clayton:** Both model only positive dependence, but they differ critically in *where* that dependence concentrates. Gumbel is suited for variables that are most concordant in the upper tail (e.g., extreme co-movements); Clayton models lower tail concordance (e.g., simultaneous low-value events). This distinction is critical in risk and survival modeling.

**Why the Gaussian Copula Fails at Tails:** The Gaussian copula can model symmetric dependence across the full range of ρ, but it cannot model tail dependence due to the thin tails of the underlying normal distribution. This property was at the heart of its catastrophic misuse in CDO pricing models before the 2008 financial crisis.

**Kendall's Tau over Pearson's r:** Pearson's correlation only captures linear dependence between raw values. Kendall's tau operates on ranks and can capture nonlinear, asymmetric, and tail-driven dependence — making it far more appropriate for copula-based modeling.

---

## Applications

Copulas derived in this project have direct applications in:

- **Survival Analysis** — frailty models using Gumbel and Clayton copulas
- **Finance & Risk** — joint default modeling, portfolio risk, credit derivatives
- **Insurance** — modeling correlated claim events
- **Environmental Science** — joint modeling of correlated extreme weather events
- **Reliability Engineering** — dependence modeling in failure time analysis

---

## Repository Structure

```
copula-theory/
├── STAT590FinalProjectCostello.pdf    # Full written report with derivations
└── README.md
```

---

## References

- Sklar, A. (1959). *Fonctions de répartition à n dimensions et leurs marges.* Publications de l'Institut de Statistique de l'Université de Paris.
- Haugh, M. (2016). *An Introduction to Copulas.* Columbia University IEOR E4602.
- Embrechts, P. (2009). *Copulas: A Personal View.* ETH Zurich.
- Roncalli, T. (2020). *Copulas and Dependence Modeling.* Handbook of Financial Risk Management.
- Nematrian. *Archimedean Copulas.* www.nematrian.com/ArchimedeanCopulas
- Chang, B. (2019). *Copula: A Very Short Introduction.* bochang.me

---

## Author

**John Costello**  
M.S. Applied Statistics candidate, California State University Long Beach  
[github.com/bulbajohn](https://github.com/bulbajohn) | jcost2015@gmail.com

---

*May 2026 — STAT 590: Survival Analysis, California State University Long Beach*  
*Submitted to Dr. Olga Korosteleva*
