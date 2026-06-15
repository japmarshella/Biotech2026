import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt

# Parameters from the exam table
V1max = 5.0
Km1   = 2.0
Ki    = 3.0
X     = 10      # constant external substrate
k2    = 1.0
k3    = 0.8
k4    = 0.3

def model(t, y):
    A, B, P = y

    # v1: Michaelis-Menten WITH non-competitive inhibition by P
    v1 = (V1max * X) / ((Km1 + X) * (1 + P / Ki))

    # v2, v3, v4: simple first-order kinetics
    v2 = k2 * A
    v3 = k3 * B
    v4 = k4 * A

    dA = v1 - v2 - v4   # A: produced by v1, consumed by v2 and v4
    dB = v2 - v3         # B: produced by v2, consumed by v3
    dP = v3              # P: produced by v3 only

    return [dA, dB, dP]

# Initial conditions: everything starts at zero
y0     = [0, 0, 0]
t_span = (0, 50)
t_eval = np.linspace(0, 50, 500)

sol = solve_ivp(model, t_span, y0, t_eval=t_eval, method='RK45')

# Plot
plt.figure(figsize=(9, 5))
plt.plot(sol.t, sol.y[0], label='[A]', color='steelblue',  linewidth=2)
plt.plot(sol.t, sol.y[1], label='[B]', color='darkorange', linewidth=2)
plt.plot(sol.t, sol.y[2], label='[P]', color='seagreen',   linewidth=2)
plt.xlabel('Time (h)')
plt.ylabel('Concentration (mM)')
plt.title('Kinetic simulation — with allosteric feedback inhibition on v₁')
plt.legend()
plt.tight_layout()
plt.show()
