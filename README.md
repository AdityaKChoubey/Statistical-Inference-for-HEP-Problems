# Statistical Inference for High Energy Physics Problems

**Author:** Aditya Kumar Choubey  
**Course:** Statistical Inference for High Energy Physics  
**Dataset:** CERN Open Data — CMS DoubleMuon Primary Dataset (Run 2016G, $\sqrt{s} = 13\text{ TeV}$, NanoAOD, [Record 30522](https://opendata.cern.ch/record/30522))

---

## Repository Structure

```
├── Assignment1/
│   ├── Assingment1_HEPSTATISTICAL.ipynb        # Chi2 distribution, non-Gaussian toy tests, 1D & 2D NLL scans
│   ├── GM_Counting_Experiment.ipynb            # Profile likelihood & Poisson tests for radiation counting
│   ├── background_Tl204_observations(1)(1).xlsx # Raw Geiger-Müller counter observations
│   └── readme.md
├── Assignment2/
│   ├── Assignment2.ipynb                     # Cowan KMI maximum likelihood fit exercises (1a - 1e)
│   └── ml_fit_exercise.pdf                   # Problem set specification (G. Cowan, RHUL Physics)
├── Project _DiMuon_Resonances/
│   └── CMS_Dimuon_Four_Resonances_Inference.ipynb # Term Project: Comprehensive multi-resonance statistical inference
├── .gitignore
└── README.md
```

---

## Term Project: Statistical Analysis of Four Dimuon Resonances in CMS Open Data
📁 **[`Project _DiMuon_Resonances/CMS_Dimuon_Four_Resonances_Inference.ipynb`](./Project%20_DiMuon_Resonances/CMS_Dimuon_Four_Resonances_Inference.ipynb)**

This term project performs rigorous likelihood-based statistical inference across dimuon resonances spanning nearly two orders of magnitude in invariant mass:
* **$J/\psi$** ($m \approx 3.097\text{ GeV}$, $\Gamma = 93\text{ keV}$)
* **$\psi(2S)$** ($m \approx 3.686\text{ GeV}$, $\Gamma = 294\text{ keV}$)
* **$\Upsilon(1S, 2S, 3S)$** ($m \approx 9.460, 10.023, 10.355\text{ GeV}$, $\Gamma \sim 20\text{--}50\text{ keV}$)
* **$Z$ Boson** ($m \approx 91.188\text{ GeV}$, $\Gamma_Z = 2.4952\text{ GeV}$)

### Key Analysis Highlights

1. **Detector Geometry & Resolution Partitioning:**
   * Classifies muon pairs into geometric sub-categories based on pseudorapidity: Barrel-Barrel (BB), Barrel-Endcap (BE), and Endcap-Endcap (EE).
   * Models the degradation of momentum resolution in the endcaps via floating resolution scale factors ($r_{\text{BE}}, r_{\text{EE}}$) fitted simultaneously.

2. **Advanced Signal Line Shape Modeling:**
   * **Narrow states ($J/\psi, \psi(2S), \Upsilon$):** Parameterized using a Double Crystal Ball (DCB) distribution featuring asymmetric power-law tails to account for final-state radiation (FSR), bremsstrahlung, and tracker multiple scattering.
   * **$Z$ Boson:** High-precision numerical convolution of a relativistic Breit-Wigner (accounting for the non-negligible natural width $\Gamma_Z$) with the detector resolution response.

3. **Unbinned Extended Maximum Likelihood Estimation:**
   * Implemented using `iminuit` and custom vectorised PDF evaluators.
   * Unbiased parameter and uncertainty extraction for yields, physical resonance masses, detector resolutions, and background parameters across three disjoint invariant mass windows ($2.7\text{--}4.1\text{ GeV}$, $8.6\text{--}11.4\text{ GeV}$, $70\text{--}110\text{ GeV}$).

4. **Hypothesis Testing & Discovery Significance:**
   * **Background-Only Null Hypothesis ($H_0: N_S = 0$):** Evaluated via the profile likelihood ratio test statistic $q_0 = -2\Delta\ln L$, achieving overwhelming discovery significance exceeding $5\sigma$ across all channels.
   * **Mass Compatibility Tests ($H_0: m = m_{\text{PDG}}$):** Profile likelihood scans comparing fitted mass positions against world-average PDG values.
   * **$Z$ Natural Width Test:** Profiled hypothesis test of $H_0: \Gamma_Z = 2.4952\text{ GeV}$.

5. **Bottomonium Mass Splitting Extraction:**
   * Evaluated $\Delta m_{21} = m(\Upsilon(2S)) - m(\Upsilon(1S))$ and $\Delta m_{31} = m(\Upsilon(3S)) - m(\Upsilon(1S))$ using both the full Minuit error covariance matrix and profile likelihood scans.
   * Provides clean cancellation of common momentum-scale systematic shifts.

6. **Toy Monte Carlo Pseudo-Experiments:**
   * Empirical validation of coverage, pull distributions, and Wilks' theorem compliance using ensemble pseudo-experiments.

7. **Multidimensional Profile Likelihood Geometry:**
   * Construction of 2D joint confidence contours ($\Delta q = 2.30, 6.18, 11.83$ corresponding to $1\sigma, 2\sigma, 3\sigma$) in the $(m, \sigma_{\text{det}})$ plane.
   * 3D profile likelihood surface rendering highlighting parameter correlations and local curvature.

8. **Goodness-of-Fit & Binned Cross-Checks:**
   * Independent verification via Poisson binned maximum likelihood fits.
   * Evaluation of saturated Poisson deviance ($D$) to assess overall goodness-of-fit.

9. **Systematic Uncertainty Quantification:**
   * Comprehensive evaluation of background modeling systematics by comparing exponential backgrounds against higher-order quadratic exponentials and Bernstein polynomial bases.

10. **Global Energy Scale & Resolution Scaling:**
    * Evaluation of relative mass offsets $(m - M_{\text{PDG}})/M_{\text{PDG}}$ across 3 to 91 GeV to probe momentum scale calibrations.
    * Characterization of fractional resolution $\sigma/M$ behavior demonstrating the transition from multiple-scattering-dominated regimes to tracker curvature-measurement regimes.

---

## Assignments

### Assignment 1: Fundamental Statistical Tests & GM Counter Analysis
* **Notebooks:** [`Assingment1_HEPSTATISTICAL.ipynb`](./Assignment1/Assingment1_HEPSTATISTICAL.ipynb), [`GM_Counting_Experiment.ipynb`](./Assignment1/GM_Counting_Experiment.ipynb)
* Non-Gaussian toy experiments, empirical $\chi^2$ distributions, 1D and 2D negative log-likelihood (NLL) profile scans.
* Poisson counting statistics and profile likelihood ratio test on laboratory Geiger-Müller radiation observations ($^{204}\text{Tl}$).

### Assignment 2: Maximum Likelihood Estimation & Limit Setting
* **Notebook:** [`Assignment2.ipynb`](./Assignment2/Assignment2.ipynb)
* Solutions to Glen Cowan's KMI Maximum Likelihood Fit exercise series (parts 1a through 1e), covering signal fraction extraction, asymptotic confidence intervals, and profile likelihood ratio bounds.

---

## Setup and Reproduction

### Prerequisites
* Python 3.10+
* Required packages: `uproot`, `awkward`, `iminuit`, `scipy`, `numpy`, `matplotlib`, `aiohttp`, `fsspec`

### Instructions

Activate your environment and start Jupyter:

```bash
# Activate conda environment (WSL / Linux)
conda activate ml

# Navigate to the repository
cd ~/Statistical-Inference-for-HEP-Problems

# Launch Jupyter Lab
jupyter lab
```
