# covid-behaviour-modelling
# COVID Behavior–Policy–Epidemic Dynamics Model

## Overview

This project explores how **human behavior**, **government policy**, and **epidemic dynamics** interact over time using a **dynamical systems approach** combined with **Kalman filtering**.

The goal is not to build a perfect epidemiological model, but to understand:

* How behavior responds to deaths and policy
* How behavior feeds back into epidemic outcomes
* How system parameters evolve over time

---

## Key Idea

We model the system as a feedback loop:

[
\text{Deaths} \rightarrow \text{Behavior} \leftarrow \text{Policy}, \quad \text{Behavior} \rightarrow \text{Deaths}
]

Where:

* Behavior decreases with higher deaths and stricter policy
* Reduced behavior suppresses deaths
* Policy acts as an external forcing signal

---

## Model Components

### Behavior Dynamics

[
B(t) = \rho B(t-1) + (1-\rho)(b_0 - \alpha D(t-\tau) - \eta P(t))
]

* ( \alpha ): sensitivity to deaths
* ( \eta ): sensitivity to policy
* ( \rho ): behavioral inertia
* ( \tau ): response delay

---

### Death Dynamics

[
D(t) = W(t) \cdot (1 - \delta B(t))
]

* ( W(t) ): baseline epidemic curve
* ( \delta ): effect of behavior on deaths

---

## Methodology

### 1. Data Sources

* COVID deaths (global aggregate)
* Google mobility (behavior proxy)
* Oxford stringency index (policy proxy)

### 2. Preprocessing

* Time alignment across datasets
* Rolling smoothing (7–14 day windows)
* Normalization

### 3. Modeling Progression

1. Behavior modeled from deaths
2. Added delay (( \tau ))
3. Added inertia (( \rho ))
4. Added policy forcing (( P(t) ))
5. Introduced feedback into deaths
6. Applied Kalman filtering
7. Extended to Unscented Kalman Filter (UKF)
8. Performed joint state + parameter estimation

---

## Kalman Filtering Approach

We treat the system as a **nonlinear state-space model**:

* Hidden state: ( [B_t, D_t] ) (and parameters)
* Observations: noisy measurements of behavior and deaths

### Why UKF?

* Handles nonlinear dynamics better than EKF
* Avoids explicit linearization
* Uses sigma points to approximate uncertainty propagation

---

## Key Findings

* **Deaths alone explain low-frequency behavioral trends**, but not sharp changes
* **Policy explains abrupt behavioral shifts (lockdowns, reopening)**
* **Inertia has limited impact once smoothing is applied**
* **Feedback stabilizes epidemic peaks**
* **Parameters drift over time**, suggesting changing behavioral response (e.g., fatigue)

---

## Limitations

* Not a full epidemiological (SIR-type) model
* Uses proxy variables (mobility ≠ true behavior)
* Identifiability issues in parameter estimation
* Feedback structure is simplified
* Baseline epidemic curve is derived from observed data

---


## Future Work

* Add explicit fatigue/compliance state
* Move to full epidemiological (SIR) dynamics
* Improve identifiability via constraints or priors
* Compare across countries
* Explore particle filtering

---

## Takeaway

This project demonstrates how **complex social–epidemiological systems** can be modeled as:

> nonlinear dynamical systems with feedback and uncertainty

and how **Kalman filtering** can be used to:

* infer hidden states
* adapt model parameters
* integrate noisy real-world data

---

## License

MIT License
