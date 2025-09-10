# About Ecology Populations
Interactive simulations of Logistic Growth, Predator-Prey, and Interspecific Competition models
Ecological Models Simulation — User & Developer Manual

This manual explains what the tool does, how to use every control, how to read the outputs, and how the code works under the hood—including the equations, numerical methods, and design decisions.

1) What this tool is

An interactive, single-file HTML app for exploring three foundational ecological models:

Logistic Growth — population growth with carrying capacity.

Lotka–Volterra Predator–Prey — coupled consumer–resource oscillations.

Interspecific Competition — two species competing for shared resources.

The page renders sliders and inputs for parameters, draws time-series charts for populations and their rates of change, and lets you download results as CSV.

Tech stack: Pure HTML/CSS/JS + [Chart.js] (via CDN). No build tools, no server required.

2) Quick start (for users)

Open the file in any modern browser (Chrome, Edge, Firefox, Safari).

Use the tabs to select a model.

Adjust parameters with sliders or number inputs (they stay in sync).

Click Run Simulation to recompute and update the charts.

Inspect the two charts:

Left: populations over time.

Right: rate of change (e.g., 
𝑑
𝑁
/
𝑑
𝑡
dN/dt, 
𝑑
𝑥
/
𝑑
𝑡
dx/dt, 
𝑑
𝑦
/
𝑑
𝑡
dy/dt).

Read current values in the Changing Rate / K box below the charts.

Click Download Data to export a CSV of the most recent run.

Tips

Start with the default parameters to see “typical” dynamics.

For Predator–Prey and Competition, keep Δt small (e.g., 0.01) for smoother curves.

Use Time range to zoom into short transients or long-term behavior.

3) Interface reference (control → meaning → effect)
A. Logistic Growth

Growth rate (r)
Per-capita growth at low density. Larger 
𝑟
r → faster approach to 
𝐾
K.

Carrying capacity (K)
Long-run ceiling for population 
𝑁
N.

Initial population (N₀)
Starting value at 
𝑡
=
0
t=0.

Time range
How long (in arbitrary time units) to simulate.

Outputs

Population size chart: 
𝑁
(
𝑡
)
N(t) is sigmoidal if 
𝑁
0
<
𝐾
N
0
	​

<K.

Growth rate chart: 
𝑑
𝑁
/
𝑑
𝑡
=
𝑟
𝑁
(
1
−
𝑁
/
𝐾
)
dN/dt=rN(1−N/K); peaks at 
𝑁
=
𝐾
/
2
N=K/2.

Current K and Current dN/dt box: last-step values.

B. Predator–Prey (Lotka–Volterra)

Prey growth (α)
Intrinsic prey growth rate without predators.

Predation rate (β)
Encounter/capture effect of predators on prey.

Conversion efficiency (δ)
Prey eaten → predator births (efficiency).

Predator mortality (γ)
Predator loss without prey.

Initial prey / predator
Starting 
𝑥
(
0
)
x(0), 
𝑦
(
0
)
y(0).

Time range and Δt
Simulation horizon and Euler time step.

Outputs

Population time series: 
𝑥
(
𝑡
)
,
𝑦
(
𝑡
)
x(t),y(t) often oscillate.

Rate chart: 
𝑑
𝑥
/
𝑑
𝑡
dx/dt, 
𝑑
𝑦
/
𝑑
𝑡
dy/dt over time.

Current rates: last-step 
𝑑
𝑥
/
𝑑
𝑡
dx/dt, 
𝑑
𝑦
/
𝑑
𝑡
dy/dt.

C. Interspecific Competition

𝑟
1
,
𝑟
2
r
1
	​

,r
2
	​


Intrinsic growth rates of species 1 and 2.

𝐾
1
,
𝐾
2
K
1
	​

,K
2
	​


Carrying capacities in isolation.

Competition coefficients (α, β)
Effect of the other species in units of “self.”

In 
𝑑
𝑁
1
/
𝑑
𝑡
dN
1
	​

/dt, the effective load is 
𝑁
1
+
𝛼
𝑁
2
N
1
	​

+αN
2
	​

.

In 
𝑑
𝑁
2
/
𝑑
𝑡
dN
2
	​

/dt, it’s 
𝑁
2
+
𝛽
𝑁
1
N
2
	​

+βN
1
	​

.

Initial populations, Time range, Δt.

Outputs

Population time series: 
𝑁
1
(
𝑡
)
,
𝑁
2
(
𝑡
)
N
1
	​

(t),N
2
	​

(t).

Rate chart: 
𝑑
𝑁
1
/
𝑑
𝑡
dN
1
	​

/dt, 
𝑑
𝑁
2
/
𝑑
𝑡
dN
2
	​

/dt.

Current rates box.

Download buttons (all tabs)

Export a CSV of exactly what you see on the charts for your last run.

Columns are model-specific (see §7).

4) Model equations & solutions
A. Logistic Growth

Differential equation

𝑑
𝑁
𝑑
𝑡
=
𝑟
 
𝑁
(
1
−
𝑁
𝐾
)
.
dt
dN
	​

=rN(1−
K
N
	​

).

Analytical solution used in the code:

𝑁
(
𝑡
)
=
𝐾
1
+
(
𝐾
−
𝑁
0
𝑁
0
)
𝑒
−
𝑟
𝑡
.
N(t)=
1+(
N
0
	​

K−N
0
	​

	​

)e
−rt
K
	​

.

From this, the app also computes

𝑑
𝑁
𝑑
𝑡
(
𝑡
)
=
𝑟
 
𝑁
(
𝑡
)
(
1
−
𝑁
(
𝑡
)
𝐾
)
.
dt
dN
	​

(t)=rN(t)(1−
K
N(t)
	​

).

Implications

𝑁
(
𝑡
)
N(t) is S-shaped when 
𝑁
0
<
𝐾
N
0
	​

<K, monotone decreasing when 
𝑁
0
>
𝐾
N
0
	​

>K.

The maximum 
𝑑
𝑁
/
𝑑
𝑡
dN/dt occurs at 
𝑁
=
𝐾
/
2
N=K/2.

B. Lotka–Volterra Predator–Prey
𝑑
𝑥
𝑑
𝑡
	
=
𝛼
𝑥
−
𝛽
𝑥
𝑦
,




𝑑
𝑦
𝑑
𝑡
	
=
𝛿
𝛽
𝑥
𝑦
−
𝛾
𝑦
.
dt
dx
	​

dt
dy
	​

	​

=αx−βxy,
=δβxy−γy.
	​


𝑥
x: prey, 
𝑦
y: predator.

Equilibrium (nontrivial): 
𝑥
∗
=
𝛾
/
(
𝛿
𝛽
)
,
  
𝑦
∗
=
𝛼
/
𝛽
x
∗
=γ/(δβ),y
∗
=α/β.

Qualitative behavior: neutrally stable cycles in the idealized (undamped) version; in practice, step size and parameters can dampen or amplify numerically (see §6).

Numerical method used: Forward Euler with step 
Δ
𝑡
Δt (user-controlled).

C. Lotka–Volterra Competition
𝑑
𝑁
1
𝑑
𝑡
	
=
𝑟
1
𝑁
1
(
1
−
𝑁
1
+
𝛼
𝑁
2
𝐾
1
)
,




𝑑
𝑁
2
𝑑
𝑡
	
=
𝑟
2
𝑁
2
(
1
−
𝑁
2
+
𝛽
𝑁
1
𝐾
2
)
.
dt
dN
1
	​

	​

dt
dN
2
	​

	​

	​

=r
1
	​

N
1
	​

(1−
K
1
	​

N
1
	​

+αN
2
	​

	​

),
=r
2
	​

N
2
	​

(1−
K
2
	​

N
2
	​

+βN
1
	​

	​

).
	​


Isoclines (where growth = 0):

For species 1: 
𝑁
1
+
𝛼
𝑁
2
=
𝐾
1
N
1
	​

+αN
2
	​

=K
1
	​

.

For species 2: 
𝑁
2
+
𝛽
𝑁
1
=
𝐾
2
N
2
	​

+βN
1
	​

=K
2
	​

.

Outcomes depend on relative positions of isoclines and initial conditions (coexistence, competitive exclusion, or bistability).

Numerical method used: Forward Euler with 
Δ
𝑡
Δt.

5) Numerical methods, stability, and accuracy
Why two approaches?

Logistic uses the closed-form solution (no numerical error for 
𝑁
(
𝑡
)
N(t) beyond floating-point).

Predator–Prey and Competition have no simple closed-form; the app uses Euler for simplicity.

Euler integration

For a system 
𝑧
˙
=
𝑓
(
𝑧
,
𝑡
)
z
˙
=f(z,t), Euler updates:

𝑧
𝑛
+
1
=
𝑧
𝑛
+
Δ
𝑡
 
𝑓
(
𝑧
𝑛
,
𝑡
𝑛
)
.
z
n+1
	​

=z
n
	​

+Δtf(z
n
	​

,t
n
	​

).

Pros: simple, fast, easy to read/teach.
Cons: conditionally stable; can introduce numerical damping or growth.

Best practices in this app

Keep Δt small (e.g., 0.001–0.02) when dynamics are fast (large α, β, γ, r, or tight K).

If you see negative populations, the code clamps to zero after each step to avoid nonphysical values (a standard, practical safeguard).

If oscillations blow up or vanish suspiciously, reduce Δt or shorten the Time range.

Why not RK4?
The original version emphasizes simplicity and transparency for learners. Euler’s method is enough to demonstrate qualitative behavior and responds immediately to parameter changes. (If you want higher accuracy and stability, RK4 is a natural upgrade.)

6) Reading the charts & interpreting dynamics
Logistic

Population chart: Classic S-curve to 
𝐾
K.

Rate chart: A hump peaking near 
𝑁
=
𝐾
/
2
N=K/2; returns to 0 as 
𝑁
→
𝐾
N→K.

Experiments

Set 
𝑁
0
≪
𝐾
N
0
	​

≪K: slow–fast–slow rise.

Set 
𝑁
0
>
𝐾
N
0
	​

>K: decline back to 
𝐾
K.

Increase r: reach 
𝐾
K faster; rate peak is higher and earlier.

Predator–Prey

Population chart: prey and predator oscillate with a phase lag (predators peak after prey).

Rate chart: zero crossings align with prey/predator maxima/minima.

Experiments

Increase γ (predator mortality): predators struggle; prey can boom.

Increase β (predation rate): stronger coupling; larger amplitude oscillations (but watch Δt).

Competition

Population chart: outcomes include coexistence or exclusion.

Rate chart: helps diagnose who is currently winning or losing.

Experiments

Set α and β > 1 with unequal 
𝐾
K: often leads to exclusion of the weaker competitor.

Make α and β < 1 and 
𝐾
1
≈
𝐾
2
K
1
	​

≈K
2
	​

: coexistence is more likely.

7) CSV output format
Logistic
Time,Population,GrowthRate
t0,N(t0),dNdt(t0)
...
tN,N(tN),dNdt(tN)

Predator–Prey
Time,PreyPopulation,PredatorPopulation,PreyRate,PredatorRate
t0,x(t0),y(t0),dxdt(t0),dydt(t0)
...

Competition
Time,Species1,Species2,Species1Rate,Species2Rate
t0,N1(t0),N2(t0),dN1dt(t0),dN2dt(t0)
...


Open the file in Excel, Numbers, or Python/R for further analysis and plotting.

8) Code architecture (how it works)
Files & libraries

Single HTML file (your code block).

Chart.js via CDN:

Creates six line charts: one population and one rate chart per model.

Structure

Tabs & panels:
Buttons with data-tab toggle matching #<tab>-content sections.

Controls:

Each parameter has a range and a number input.

syncInputAndSlider() keeps them synchronized and updates the inline value readout.

Charts:

Pre-instantiated Chart.js line charts with empty datasets.

Each Run updates .data.labels and .data.datasets[i].data, then calls .update().

Model calculators:

calculateLogisticGrowth()

Loops over integer times 
𝑡
=
0
,
1
,
…
,
𝑇
t=0,1,…,T.

Uses the closed-form 
𝑁
(
𝑡
)
N(t) and computes 
𝑑
𝑁
/
𝑑
𝑡
dN/dt.

Updates charts and “Current K/dNdt” box.

calculatePredatorPrey()

Reads parameters & Δt, sets steps = time / dt.

Euler updates for 
𝑥
,
𝑦
x,y; clamps negatives to 0.

Stores 
𝑥
,
𝑦
,
𝑑
𝑥
/
𝑑
𝑡
,
𝑑
𝑦
/
𝑑
𝑡
x,y,dx/dt,dy/dt for charts & CSV.

calculateCompetition()

Same pattern as Predator–Prey with two logistic-competition equations.

Download helpers

downloadCSV(data, filename) builds a data: URI, creates a hidden <a>, clicks it, and removes it.

Autostart

On window.load, runs all three calculators so charts are populated.

Styling choices

Responsive CSS grid for controls and chart columns.

Subtle shadows, rounded cards, and consistent color palette for visual clarity.

Monospace readouts for rates and 
𝐾
K.

9) Parameter guidelines & common pitfalls

Keep Δt small for Predator–Prey and Competition when:

α, β, γ, r are large, or

populations are near zero (fast relative changes), or

you want crisp oscillations without numerical blow-up.

Unrealistic negatives:
Euler can step below zero when rates are very negative; the code clamps back to 0.

Time range vs Δt:
Large time ranges with very small Δt mean many steps. That’s fine for modern browsers, but if you notice lag, either shorten the range or increase Δt modestly.

10) Suggested classroom activities

Logistic “maximum growth” demo

Show that 
𝑑
𝑁
/
𝑑
𝑡
dN/dt peaks when 
𝑁
≈
𝐾
/
2
N≈K/2.

Vary 
𝐾
K to demonstrate the peak’s location scaling.

Predator–Prey phase lag

Identify that predator peaks follow prey peaks.

Ask students to explain biologically.

Competition outcomes

Systematically vary α and β to discover regions of coexistence vs exclusion.

Tie back to isoclines: 
𝑁
1
+
𝛼
𝑁
2
=
𝐾
1
N
1
	​

+αN
2
	​

=K
1
	​

, 
𝑁
2
+
𝛽
𝑁
1
=
𝐾
2
N
2
	​

+βN
1
	​

=K
2
	​

.

11) Extensions you can add (while keeping the original spirit)

Phase-plane plots & nullclines (prey–predator; 
𝑁
1
N
1
	​

–
𝑁
2
N
2
	​

).

Higher-order integrators (e.g., RK4) for smoother, more stable trajectories.

Time-varying 
𝐾
(
𝑡
)
K(t) to mimic environmental change.

Harvesting / stocking terms (e.g., 
−
ℎ
−h, 
+
𝑠
+s).

Stochasticity (random environmental noise) to study variability.

Parameter presets buttons for common scenarios.

12) Troubleshooting

“My predator goes negative.”
Reduce Δt; ensure δ isn’t too high relative to γ and β; note the code clamps to 0 after each step to stay physical.

“Curves look jagged or blow up.”
Lower Δt; reduce time range; moderate parameter magnitudes.

“Download didn’t work.”
Some locked-down browsers block data: downloads—try a different browser or allow pop-ups for local files.

13) Reference summary (at a glance)

Logistic

𝑑
𝑁
/
𝑑
𝑡
=
𝑟
𝑁
(
1
−
𝑁
/
𝐾
)
dN/dt=rN(1−N/K) — closed-form solution used.

Pred–Prey

𝑑
𝑥
/
𝑑
𝑡
=
𝛼
𝑥
−
𝛽
𝑥
𝑦
,
  
𝑑
𝑦
/
𝑑
𝑡
=
𝛿
𝛽
𝑥
𝑦
−
𝛾
𝑦
dx/dt=αx−βxy,dy/dt=δβxy−γy — Euler.

Competition

𝑑
𝑁
1
/
𝑑
𝑡
=
𝑟
1
𝑁
1
(
1
−
(
𝑁
1
+
𝛼
𝑁
2
)
/
𝐾
1
)
dN
1
	​

/dt=r
1
	​

N
1
	​

(1−(N
1
	​

+αN
2
	​

)/K
1
	​

)

𝑑
𝑁
2
/
𝑑
𝑡
=
𝑟
2
𝑁
2
(
1
−
(
𝑁
2
+
𝛽
𝑁
1
)
/
𝐾
2
)
dN
2
	​

/dt=r
2
	​

N
2
	​

(1−(N
2
	​

+βN
1
	​

)/K
2
	​

) — Euler.

14) Credits

You (original design & implementation).

Chart.js (plotting library via CDN).
