# Statistical Inference for High Energy Physics Problems

Repository containing coursework assignments and a comprehensive term project notebook applying maximum-likelihood estimation, profile likelihood scans, hypothesis testing, multidimensional likelihood geometry, and Monte Carlo pseudo-experiments to real CERN CMS collision data.

---

## Repository Structure

```
├── Assignment1/
│   ├── Assingment1_HEPSTATISTICAL.ipynb    # Chi2 distribution, non-Gaussian toy tests, 1D & 2D NLL scans
│   ├── GM_Counting_Experiment.ipynb        # Profile likelihood & Poisson tests for radiation counting
│   ├── background_Tl204_observations.xlsx  # Raw observations from Geiger-Müller counter experiment
│   └── readme.md
├── Assignment2/
│   ├── StatisticsLEC.ipynb                 # Cowan KMI mlFit exercises (1a - 1e)
│   └── ml_fit_exercise.pdf                 # Reference problem set (G. Cowan, RHUL Physics)
├── CMS_Z_Dimuon_Likelihood_Inference.ipynb  # Term Project: Signal Discovery, 15-Mass Scan, 3D/2D Geometry & Toys
└── README.md
```

---

## Project Overview

* **Dataset:** 2016 CMS DoubleMuon Primary Dataset (Run 2016G, $\sqrt{s} = 13\text{ TeV}$, NanoAODv9, CERN Open Data Record [30522](https://opendata.cern.ch/record/30522)).
* **Remote Streaming Protocol:** Direct HTTP range streaming with `uproot` without local multi-GB downloads.
* **Analysis Packages:** `uproot`, `iminuit`, `scipy`, `numpy`, `matplotlib`.

---

## Project Notebook: Likelihood-Based Signal Extraction & Hypothesis Testing
📄 **[`CMS_Z_Dimuon_Likelihood_Inference.ipynb`](./CMS_Z_Dimuon_Likelihood_Inference.ipynb)**

### 1. Unbinned Extended Maximum Likelihood Fit:
* Modeled relativistic Voigtian signal (Breit-Wigner natural width $\Gamma_Z = 2.4952\text{ GeV}$ convoluted with Gaussian detector resolution $\sigma_{\text{det}}$) + normalized exponential background ($\lambda$).
* Measured parameters:
  * **$Z$ Mass:** $\hat{m}_Z = 90.7714 \pm 0.0360\text{ GeV}$
  * **Detector Resolution:** $\hat{\sigma}_{\text{det}} = 1.5221 \pm 0.0492\text{ GeV}$
  * **Signal Yield:** $\hat{N}_S = 6502.3 \pm 89.8\text{ events}$
  * **Background Yield:** $\hat{N}_B = 344.8 \pm 43.7\text{ events}$
  * **Background Slope:** $\hat{\lambda} = 0.0370 \pm 0.0087\text{ GeV}^{-1}$

### 2. Hypothesis Test I: The Background-Only Hypothesis ($H_0: N_S = 0$) & Discovery:
* Formulated the profile likelihood ratio test statistic $q_0 = -2 \ln(L_0 / L_{\text{MLE}})$ comparing the background-only null hypothesis against the signal-plus-background alternative.
* **Test Statistic:** $q_0 = 12103.37$
* **Frequentist $p$-value:** $p_0 \ll 10^{-300}$
* **Discovery Significance:** $Z_0 = 110.02\,\sigma$ (overwhelmingly exceeding the $5\sigma$ discovery threshold).
* Dual-panel figure comparing the Signal+Background fit against the Background-Only fit with pull distributions.

### 3. Hypothesis Test II: 15 Discrete Mass Hypotheses ($H_0(m_0): m_Z = m_0$):
* Profiled nuisance parameters $(N_S, N_B, \sigma_{\text{det}}, \lambda)$ across 15 candidate masses $m_0 \in [88.0, 93.0]\text{ GeV}$.
* Evaluated test statistic $q(m_0)$, $p$-values, and exclusion significance $Z(m_0) = \sqrt{q(m_0)}\sigma$.
* Near-peak resolution: $m_0 = 90.75\text{ GeV}$ is fully compatible ($Z = 0.59\sigma$), while $m_0 = 90.50\text{ GeV}$ ($7.45\sigma$) and $m_0 = 91.00\text{ GeV}$ ($6.36\sigma$) are strongly excluded.
* Generated an 80-point continuous profile likelihood scan with $1\sigma, 2\sigma, 3\sigma$ confidence bands and PDG reference line ($91.1876\text{ GeV}$).
* Visual overlay of all 15 hypothesis PDFs against the CMS collision data peak.

### 4. Advanced 3D & 2D Statistical Visualizations:
* **3D Likelihood Surface:** Mapped the parabolic bowl $-2\Delta \ln L(m_Z, \sigma_{\text{det}})$ with contour floor projections and $1\sigma, 2\sigma, 3\sigma$ level rings.
* **Simultaneous 2D Confidence Contours:** 2-d.o.f. joint confidence regions ($\Delta q = 2.30, 6.18, 11.83$) for $(m_Z, \sigma_{\text{det}})$ and $(m_Z, N_S)$.
* **Exclusion Bar Chart & $p$-value Log-Scale Scan:** Color-coded significance levels and log-scale $p$-value drop.

### 5. Frequentist Validation via 150 Monte Carlo Pseudo-Experiments:
* 150 converged toys generated from the unconditional MLE parameters.
* **Pull Mean:** $-0.049 \approx 0$ (unbiased estimator).
* **Pull Standard Deviation:** $1.009 \approx 1.0$ (accurate error quantification).
* **Empirical $68.3\%$ Coverage:** $66.0\% \approx 68.3\%$.

---

## Instructions for Reproduction

Activate the conda environment in WSL:

```bash
conda activate ml
cd /mnt/c/Users/Aditya\ Kr\ Choubey/Desktop/Z_mass

# To launch Jupyter Lab / Notebook:
jupyter lab
```
