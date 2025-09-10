# Ecological Models Simulation Tool - Comprehensive Manual
Interactive simulations of Logistic Growth, Predator-Prey, and Interspecific Competition models
Ecological Models Simulation — User & Developer Manual

## Introduction

The Ecological Models Simulation Tool is an interactive web application designed to help students, educators, and researchers visualize and understand three fundamental ecological models: Logistic Growth, Predator-Prey (Lotka-Volterra), and Interspecific Competition. This tool provides real-time simulations with adjustable parameters, detailed visualizations, and data export capabilities.

## Models Overview

### 1. Logistic Growth Model
The logistic growth model describes how populations grow in limited resource environments, incorporating the concept of carrying capacity (K) as a limiting factor.

**Equation**: dN/dt = rN(1 - N/K)

**Analytical Solution**: N(t) = K / [1 + ((K - N₀)/N₀)e^(-rt)]

### 2. Predator-Prey Model (Lotka-Volterra)
This model describes the dynamics between predator and prey populations, showing how they influence each other's growth rates.

**Equations**:
- Prey: dx/dt = αx - βxy
- Predator: dy/dt = δβxy - γy

### 3. Interspecific Competition Model
This model describes competition between two species for limited resources, based on the Lotka-Volterra competition equations.

**Equations**:
- Species 1: dN₁/dt = r₁N₁ (1 − (N₁ + αN₂)/K₁)
- Species 2: dN₂/dt = r₂N₂ (1 − (N₂ + βN₁)/K₂)

## How to Use the Tool

### Interface Overview

The interface is organized into three main tabs, one for each model. Each tab contains:

1. **Parameter Controls**: Sliders and input fields to adjust model parameters
2. **Visualization Area**: Two charts showing population dynamics and growth rates
3. **Rate Display**: Current values of key parameters and rates
4. **Action Buttons**: To run simulations and download data

### Adjusting Parameters

Each model has specific parameters that can be adjusted:

#### Logistic Growth Model:
- Growth rate (r): Intrinsic per capita growth rate
- Carrying capacity (K): Maximum population size the environment can sustain
- Initial population (N₀): Starting population size
- Time range: Duration of the simulation

#### Predator-Prey Model:
- Prey growth rate (α): How quickly prey reproduce in absence of predators
- Predation rate (β): How effectively predators capture prey
- Conversion efficiency (δ): How efficiently predators convert consumed prey into new predators
- Predator mortality rate (γ): Natural death rate of predators
- Initial populations: Starting sizes of prey and predator populations
- Time parameters: Duration and step size of simulation

#### Interspecific Competition Model:
- Growth rates (r₁, r₂): Intrinsic growth rates for each species
- Carrying capacities (K₁, K₂): Maximum population sizes for each species
- Competition coefficients (α, β): Effect of one species on the other
- Initial populations: Starting sizes for both species
- Time parameters: Duration and step size of simulation

### Running Simulations

1. Select the model tab you want to explore
2. Adjust parameters using sliders or direct input fields
3. Click the "Run Simulation" button to update the charts
4. Observe the population dynamics in the left chart and growth rates in the right chart
5. Check the "Changing Rate Values" section to see current parameter values and rates

### Interpreting Results

- **Population Charts**: Show how population sizes change over time
- **Rate Charts**: Show how growth rates (dN/dt) change over time
- **Rate Displays**: Show current values of key parameters and instantaneous growth rates

### Downloading Data

Click the "Download Data" button to export the simulation results as a CSV file. This file contains all time points, population sizes, and growth rates for further analysis.

## Design and Algorithms

### Interface Design

The interface follows a clean, responsive design with:

1. **Tab-based Navigation**: Easy switching between models
2. **Dual-panel Layout**: Simultaneous view of population dynamics and growth rates
3. **Interactive Controls**: Sliders with synchronized numeric inputs for precise parameter adjustment
4. **Real-time Feedback**: Immediate visual updates when parameters change
5. **Responsive Design**: Adapts to different screen sizes

### Algorithm Implementation

#### Logistic Growth Model

The logistic growth model uses the analytical solution:

```javascript
N(t) = K / [1 + ((K - N₀)/N₀)e^(-rt)]
```

This provides exact values at each time point without numerical approximation.

#### Predator-Prey and Competition Models

These models use Euler's method for numerical integration:

```javascript
// For each time step
dPreyDt = alpha * prey - beta * prey * predator;
prey += dPreyDt * dt;

dPredatorDt = delta * beta * prey * predator - gamma * predator;
predator += dPredatorDt * dt;
```

The time step (Δt) is customizable, with smaller values providing more accurate results at the cost of computational intensity.

#### Growth Rate Calculation

For all models, growth rates are calculated using the model equations:

- Logistic: dN/dt = rN(1 - N/K)
- Predator-Prey: 
  - Prey: dx/dt = αx - βxy
  - Predator: dy/dt = δβxy - γy
- Competition:
  - Species 1: dN₁/dt = r₁N₁ (1 − (N₁ + αN₂)/K₁)
  - Species 2: dN₂/dt = r₂N₂ (1 − (N₂ + βN₁)/K₂)

### Visualization

The tool uses Chart.js for creating interactive, responsive charts. Each model has two charts:

1. **Population Chart**: Shows population sizes over time
2. **Rate Chart**: Shows growth rates over time

Charts are updated in real-time as parameters change, with smooth transitions for better user experience.

### Data Export

The download function generates CSV data with the following structure:

```
Time,Population/GrowthRate...
```

For example, the Predator-Prey model generates:
```
Time,PreyPopulation,PredatorPopulation,PreyRate,PredatorRate
0,100,8,40,-16
0.01,100.4,7.84,39.84,-15.68
...
```

## Educational Applications

This tool supports learning about:

1. **Population Ecology**: How populations grow under different conditions
2. **Modeling Concepts**: The relationship between differential equations and population dynamics
3. **Parameter Effects**: How changing parameters affects system behavior
4. **Numerical Methods**: How differential equations are solved computationally
5. **Data Analysis**: How to interpret and export simulation results

## Technical Considerations

- The tool runs entirely in the browser using HTML, CSS, and JavaScript
- No server-side processing is required
- All calculations are performed client-side for immediate feedback
- The interface is responsive and works on various device sizes

## Conclusion

The Ecological Models Simulation Tool provides an interactive platform for exploring fundamental ecological models. Its intuitive interface, real-time visualizations, and data export capabilities make it valuable for both education and research. By allowing users to manipulate parameters and immediately see the effects, it helps build intuition about complex ecological dynamics.

For further exploration, users are encouraged to:
- Experiment with extreme parameter values
- Compare results across different models
- Export data for additional analysis
- Relate simulation results to real-world ecological systems
