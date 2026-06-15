## ❗Environment and setup❗

Reproducible environments are provided via `environment.yml` (Conda). Create and activate the environment, install the Jupyter kernel, then launch JupyterLab:
```bash
conda env create -f environment.yml
conda activate biotech2026
python -m ipykernel install --user --name=biotech2026
jupyter lab
```

If you prefer a pip-based virtualenv, create a `requirements.txt` with the main dependencies and install into a virtual environment:
```bash
python -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install numpy scipy matplotlib seaborn pandas jupyterlab ipykernel
python -m ipykernel install --user --name=biotech2026
jupyter lab
```
# Biotechnology 2026 Final Exam Answer

## Question 1: Choosing the Right Modelling Framework
🌟 Scenario 1: *Constraint-Based Modeling (Flux Balance Analysis / FBA)*

FBA simulates cellular metabolism and calculates metabolite fluxes using genome-scale metabolic network reconstructions, enabling predictions of organism growth or metabolite production rates. This framework is appropriate for calculating the maximum theoretical yield, as it focuses on what is achievable at the steady state of a metabolic network.
   
🌟 Scenario 2: *Kinetic Modeling (ODE-based)*

Scenario 2 requires detailed tracking of intermediate B production over a 48‑hour run in order to determine when toxicity levels become dangerous and adjust the process. ODE-based kinetic modeling allows the simulation of real-time metabolite concentration dynamics, enabling the prediction of toxic accumulation over the fermentation cycle.

🌟 Scenario 3: *Network Topology / Graph Theory*

Network topology / graph theory algorithms (like degree centrality) is the modeling of network topologies as mathematical graphs and computation of various metrics that describe its characteristics. This framework identifies highly connected nodes (HUBS) in the arrangement of metabolic networks, helping avoid unintended disruption of essential pathways when designing knockouts. 

## Question 2
**Q2A. Construct the Stoichiometric Matrix (S)**
|    | v1 | v2 | v3 | v4 |
|----|----|----|----|----|
|**A**| 1 | -1 | 0 | -1 |
|**B**| 0 | 1 | -1 | 0 |
|**P**| 0 | 0 | 1 | 0 |

**Q2B. Formulate the Kinetic Differential Equations**

```math
\frac{d[A]}{dt} = v_1 - v_2 - v_4 = \frac{V_{1,max} \cdot [X]}{K_{m1} + [X]} - k_2[A] - k_4[A]
```

```math
\frac{d[B]}{dt} = v_2 - v_3 = k_2[A] - k_3[B]
```

```math
\frac{d[P]}{dt} = v_3 = k_3[B]
```

**Q2C. Simulate the Kinetic Model**
| Parameter	| Meaning                     | Value |
|-----------|-----------------------------|-----------|
| *V*1max   | Max rate of *V*1            | 5.0       |
| *K*m1     | Michaelis constant for *V*1 |	2.0       |
| *K*i      | Inhibition constant	        | 3.0       |
| *X*       | External substrate concentration | 10 |
| *k*2 | First-order rate constant for A → B  |	1.0 |
| *k*3 | First-order rate constant for B → P | 0.8 |
| *k*4 | First-order rate constant for A → *byproduct* | 0.3 |

Run the code here at 🌟 [💾 **CODING**](coding.ipynb) 🌟

🌟 **Simulation Figure** 🌟
<img width="1052" height="671" alt="image" src="https://github.com/user-attachments/assets/a32d6335-2cef-4ab1-9fc6-e30b91123771" />

