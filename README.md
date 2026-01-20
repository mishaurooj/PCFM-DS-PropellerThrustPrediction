# 🚀 PCFM-DS: Physics-Compressed Dual-Scale Propeller Thrust Prediction

```{=html}
<p align="center">
```
`<img src="Results/PCFM-DS.png" width="720"/>`{=html}
```{=html}
</p>
```
> **IEEE Q1--ready research repository** for\
> **Physics-Compressed Cascaded Feature Micro-Models (Dual Scale)**\
> enabling **cross-scale, interpretable, and data-efficient propeller
> thrust prediction**.

------------------------------------------------------------------------

## 🔍 Research Motivation & Gaps

Accurate propeller thrust modeling is critical for **Advanced Air
Mobility (AAM)** and **Distributed Electric Propulsion (DEP)** systems.\
However, existing approaches suffer from:

-   ❌ **CFD dependency** → high computational cost\
-   ❌ **Pure black-box ML** → poor extrapolation & interpretability\
-   ❌ **Dimensional learning** → scale sensitivity\
-   ❌ **Lack of cross-scale validation**\
-   ❌ **Poor data efficiency**

### 🧩 Research Gap Addressed

PCFM-DS fills the missing link between **physics-based scaling** and
**data-driven learning** by: - Explicitly separating **deterministic
physics** from **learned aerodynamics** - Learning only in a
**low-dimensional nondimensional space** - Enabling **cross-scale
transfer** from small UAV propellers to large AAM propellers

------------------------------------------------------------------------

## ✨ Key Novelty (Why PCFM-DS is New)

✔ Physics-compressed **cascaded learning formulation**\
✔ Explicit **thrust reconstruction using analytical scaling laws**\
✔ **Dual-scale micro-models** without added complexity\
✔ **Millisecond training**, constant-time inference\
✔ Robust under **90% data reduction**\
✔ First framework validated on **heterogeneous small + large propeller
datasets**

------------------------------------------------------------------------

## 🧠 Core Idea: Physics-Compressed Cascade

Instead of learning thrust directly: \[ (V, D, RPM)
`\rightarrow `{=tex}T \]

PCFM-DS reformulates the task as:

\[ (V, D, RPM) `\rightarrow `{=tex}J `\rightarrow `{=tex}C_T
`\rightarrow `{=tex}T \]

Where: - **J**: Advance ratio (physics-normalized operating point) -
**C`<sub>`{=html}T`</sub>`{=html}**: Thrust coefficient (learned
aerodynamics) - **T**: Dimensional thrust (analytically reconstructed)

------------------------------------------------------------------------

## 🧩 Model Architecture (PCFM-DS)

```{=html}
<p align="center">
```
`<img src="Results/Figures/PCFM_DS_architecture.png" width="760"/>`{=html}
```{=html}
</p>
```
### Module M1 -- Operating Point Normalization

\[ J = `\frac{V}{nD}`{=tex}, `\quad `{=tex}n = `\frac{RPM}{60}`{=tex} \]

### Module M2 -- Dual-Scale Aerodynamic Micro-Models

Separate polynomial micro-models: \[ C_T = a_0 + a_1 J + a_2 J\^2 \]

### Module M3 -- Physics-Constrained Reconstruction

\[ T = C_T `\rho `{=tex}n\^2 D\^4 \]

✔ No learned scaling\
✔ Guaranteed dimensional consistency

------------------------------------------------------------------------

## 📊 Datasets & Experimental Setup

### Paired Dataset Statistics

```{=html}
<p align="center">
```
`<img src="Results/paired_2xN_dataset_stats.png" width="720"/>`{=html}
```{=html}
</p>
```
### Large-Scale Experimental Validation

```{=html}
<p align="center">
```
`<img src="Results/big_propeller_experimental_setup.png" width="340"/>`{=html}
`<img src="Results/CT_vs_J.png" width="420"/>`{=html}
```{=html}
</p>
```

------------------------------------------------------------------------

## 🧪 Capability-Based Comparison (Literature Gap)

  --------------------------------------------------------------------------------------
  Domain /      Dataset /   ML         ND         Phys       XS         Key Limitations
  Application   Scale                                                   
  ------------- ----------- ---------- ---------- ---------- ---------- ----------------
  Electric      Lab-scale   ✓          ✗          ✗          ✗          Scale-specific
  thrusters                                                             

  UAV fault     UAV sensors ✓          ✗          ✗          ✗          No thrust model
  diagnosis                                                             

  Marine        Marine      ✗          ✓          ✓          ✗          No transfer
  propellers                                                            

  CFD propeller CFD         ✓          ✗          ✗          ✗          High cost
  design                                                                

  ML-assisted   CFD         ✓          ✗          ✗          ✗          No XS
  design                                                                

  Performance   UAV tests   ✗          ✓          ✓          ✗          Manual
  maps                                                                  

  Noise         Acoustic    ✓          ✗          ✗          ✗          No thrust
  prediction                                                            

  UUV control   Simulated   ✓          ✗          ✗          ✗          App-specific

  **PCFM-DS     Small +     ✓          ✓          ✓          ✓          ---
  (This work)** Large                                                   
  --------------------------------------------------------------------------------------

**ML**: machine learning, **ND**: nondimensional, **Phys**: physics
scaling, **XS**: cross-scale

------------------------------------------------------------------------

## 📈 Architecture Ablation (Why Each Component Matters)

  -------------------------------------------------------------------------------
  Model         R²          MAE         NTE         PCE         Remarks
  ------------- ----------- ----------- ----------- ----------- -----------------
  Raw-ML        0.60        290         0.030       0.60        Scale-sensitive
  (Ridge)                                                       

  Random Forest 0.79        186         0.018       0.79        Overfits

  PCFM-Base     0.50        225         0.023       0.61        No scale
                                                                separation

  **PCFM-DS**   **0.80**    **143**     **0.015**   **0.92**    **Robust &
                                                                interpretable**

  PCFM-DS (No   0.43        320         0.033       \~0         Physics broken
  Cascade)                                                      
  -------------------------------------------------------------------------------

➡ Cascading + physics compression are **essential**.

------------------------------------------------------------------------

## 📉 Data Efficiency (Limited Data Regime)

  Training Data   R²      MAE
  --------------- ------- -------
  100%            0.799   142.9
  25%             0.799   142.8
  10%             0.799   142.5
  Raw-ML (10%)    0.599   290.7

➡ **90% data reduction with no performance loss**

------------------------------------------------------------------------

## ⚡ Computational Efficiency

  Model           Training Time (ms)   Parameters
  --------------- -------------------- ------------
  Random Forest   540                  100+
  Ridge           225                  10+
  **PCFM-DS**     **1.2**              **3**

✔ Real-time ready\
✔ Edge-deployable

------------------------------------------------------------------------

## 🧠 Feature Efficiency & Physics Alignment

  Feature                 R²         Dim     PAES
  ----------------------- ---------- ------- ----------
  Diameter                0.45       1       0.33
  RPM                     0.65       1       0.47
  PCA (6)                 0.65       6       0.29
  **Advance Ratio (J)**   **0.65**   **1**   **0.47**

➡ Physics-derived features outperform statistical compression

------------------------------------------------------------------------

## ⚖️ Ethics, Safety & Explainability

  Metric                PCFM-DS
  --------------------- ---------
  Ethical Simplicity    Low
  Fail-through Safety   Yes
  FLOPs                 O(1)
  Decision Robustness   4 / 4
  Feature Count         1

------------------------------------------------------------------------

## 📚 Comparison with State-of-the-Art

  Method        Physics   Cost           Generalization
  ------------- --------- -------------- -----------------
  CFD           ✓         High           High
  Pure ML       ✗         Low            Poor
  **PCFM-DS**   ✓         **Very Low**   **Cross-scale**

------------------------------------------------------------------------

## 📂 Repository Structure

    PCFM-DS-PropellerThrustPrediction/
    ├── Code/
    ├── Dataset/
    ├── Results/
    │   ├── Figures/
    │   ├── Tables/
    │   ├── logs/
    │   ├── models/
    │   └── predictions/
    └── README.md

------------------------------------------------------------------------

## 📌 Citation

``` bibtex
@article{PCFMDS2025,
  title={Physics-Compressed Cascaded Micro-Models for Cross-Scale Propeller Thrust Prediction},
  author={Alam, M. I. and Khan, M. U. and Suleman, A. and Kaleem, Z.},
  journal={IEEE},
  year={2026}
}
If you find this work useful, **please star ⭐ the repository**.
