# Biotechnology 2026 Final Exam

You are a metabolic engineer optimizing a microbial host to produce a high-value biochemical. Your R&D team has mapped out a critical 4-reaction pathway branch point where central metabolism is diverted toward your target product, modeled by the structural topology shown below:
<img width="772" height="422" alt="image" src="https://github.com/user-attachments/assets/76891ae0-90fe-4fdb-83d0-c17f15454895" />

• Substrate *X* is maintained at a constant external concentration.
• Internal pools include intermediates *A*, *B*, and the final target Product *P*.
• Reaction v4 represents an endogenous escape pathway pulling flux into an unwanted byproduct.
• The target Product *P* loops back to exert allosteric, non-competitive feedback inhibition on the initial commitment step (v1).

## Question 1
*As the lead engineer, you must assign computational tasks based on three distinct troubleshooting scenarios. For each scenario below, choose the most appropriate modeling approach from the options provided and provide a 1-sentence justification.*

Available Frameworks:
A.	Kinetic Modeling (ODE-based)
B.	Constraint-Based Modeling (Flux Balance Analysis / FBA)
C.	Network Topology / Graph Theory

Scenario 1: You need to calculate the maximum theoretical yield of your product across the entire genome-scale metabolic network to see if this strain is commercially viable.

Scenario 2: Your bioreactor runs are failing because intermediate B is highly toxic. You need to simulate the exact, real-time dynamic pooling of metabolite B over a 48-hour fermentation cycle to prevent cell death.

Scenario 3: You want to identify structural ”hubs” or highly connected metabolite nodes in a newly sequenced host organism to ensure your gene knockouts don't accidentally disrupt essential survival pathways

## Question 2
**Q2A. Construct the Stoichiometric Matrix (S)**
Fill out the stoichiometric matrix representing this system. Ensure rows represent internal metabolites and columns represent flux rates.

**Q2B. Formulate the Kinetic Differential Equations**
Write down the baseline Ordinary Differential Equations (ODEs) representing the dynamic changes over time for all three internal pools:	*d*[A]/*dt*, *d*[B]/*dt*, and *d*[P]/*dt*.
Hint: Ignore the allosteric inhibition.

**Q2C. Simulate the Kinetic Model**
In non-competitive inhibition, the inhibitor (*P*) binds to an allosteric site, reducing the effective *V*1max, without affecting substrate binding affinity (Km1). The inhibition factor (1 + [*P*]*K*i) multiplies the denominator, reducing the overall reaction velocity as [*P*] increases. When [*P*] = 0, the expression reduces to standard Michaelis-Menten kinetics.
<img width="248" height="80" alt="image" src="https://github.com/user-attachments/assets/46b4d590-02b1-4cec-9310-02a241b89ac8" />
Combine the inhibition model with the baseline ODEs to simulate the system dynamics using these parameters:
| **Parameter**	| **Meaning**             | **Value** |
| *V*1max   | Max rate of *V*1            | 5.0       |
| *K*m1     | Michaelis constant for *V*1 |	2.0       |
| *K*i      | Inhibition constant	      | 3.0       |
| *X*       | External substrate concentration | 10 |
| *k*2 | First-order rate constant for A → B  |	1.0 |
| *k*3 | First-order rate constant for B → P | O.8 |
| *k*4 | First-order rate constant for A → *byproduct* | 0.3 |

Hint: You can utilize the example in: [**https://github.com/lab-biotek-bio-ugm/S1_BISB211605_Biotechnology**] <https://github.com/lab-biotek-bio-ugm/S1_BISB211605_Biotechnology/tree/main>
