## 🎯 Research Objective

The central research question is:

> **How can AI-based renewable-energy forecasting, battery degradation modelling, multi-objective PV–BESS sizing and uncertainty analysis be integrated to identify economically attractive and reliable renewable-energy configurations for Jabalpur?**

The framework investigates the interaction between:

☀️ Solar Resource
       ↓
📊 PV Generation
       ↓
🤖 AI Forecasting
       ↓
🔋 Battery Energy Management
       ↓
🧓 Battery Degradation
       ↓
💰 Lifecycle Economics
       ↓
⚖️ NSGA-II Optimization
       ↓
🎲 Monte Carlo Uncertainty
       ↓
🏆 Robust PV–BESS Design

🧩 Integrated Research Architecture
┌─────────────────────────────────────────────┐
│          JABALPUR CASE STUDY                │
│     Madhya Pradesh, India                   │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│          NASA POWER DATA LAYER              │
│ GHI │ DNI │ DHI │ Temperature │ Wind │ RH  │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│          PV PERFORMANCE MODEL               │
│                  pvlib                      │
│ Solar Position → POA → PV Generation       │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│          MACHINE LEARNING LAYER             │
│                                             │
│ Random Forest │ XGBoost │ LSTM              │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│       FORECAST-DRIVEN ENERGY MANAGEMENT     │
│                                             │
│ PV → Load → BESS → Grid → Curtailment       │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│          BATTERY DEGRADATION                │
│                                             │
│ SOC │ SOH │ Calendar Aging │ Cycle Aging   │
│             │ Replacement                   │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│         TECHNO-ECONOMIC ANALYSIS            │
│                                             │
│ CAPEX │ O&M │ NPV │ LCOE │ Payback         │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│             NSGA-II OPTIMIZATION            │
│                                             │
│       Cost  ↔  Reliability                  │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│          PARETO-OPTIMAL DESIGNS             │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│          MONTE CARLO ANALYSIS               │
│              1,000 Iterations               │
│                                             │
│ CAPEX │ Tariff │ Load │ Resource │ Aging   │
└──────────────────────┬──────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────┐
│       ROBUSTNESS & DECISION SUPPORT         │
│                                             │
│ NPV │ LCOE │ Reliability │ Risk │ KPI       │
└─────────────────────────────────────────────┘

🔬 Key Research Components
☀️ 1. Solar Resource Modelling
Hourly solar and meteorological data are obtained from NASA POWER for Jabalpur.
Variables
- Global Horizontal Irradiance (GHI)
- Direct Normal Irradiance (DNI)
- Diffuse Horizontal Irradiance (DHI)
- Air Temperature
- Wind Speed
- Relative Humidity
The framework converts the resource data into a photovoltaic generation profile using pvlib.
⚡ 2. PV System Modelling
The PV model incorporates:
- Solar position
- Plane-of-array irradiance
- Temperature effects
- PVWatts-based DC generation
- Inverter conversion
- System losses
- PV capacity variation
Investigated PV range
5 kW ───────────────────────────── 40 kW

🤖 3. Machine-Learning Forecasting
Three machine-learning approaches are compared:
Model	Main Strength
🌲 Random Forest	Robust nonlinear benchmark
🚀 XGBoost	High-performance tree boosting
🧠 LSTM	Sequential and temporal learning


Forecast variables
The framework can use:
- Solar irradiance
- Temperature
- Wind
- Relative humidity
- Time-of-day
- Day-of-year
- Lagged variables
Evaluation metrics
RMSE
RMSE = √[(1/n) Σ(yₜ − ŷₜ)²]

MAE
MAE = (1/n) Σ|yₜ − ŷₜ|

MAPE
MAPE = (100/n) Σ|(yₜ − ŷₜ)/yₜ|

The forecasting models are evaluated using a chronological train-validation-test methodology to reduce temporal data leakage.
🔋 4. Battery Energy Storage Model
The BESS model represents:
- State of Charge (SOC)
- State of Health (SOH)
- Charge efficiency
- Discharge efficiency
- Maximum charge/discharge power
- Equivalent cycles
- Calendar degradation
- Cycle-related degradation
- End-of-life threshold
- Battery replacement
Investigated BESS range
20 kWh ─────────────────────────── 200 kWh

SOC equation
SOCₜ₊₁ =
SOCₜ
+ ηc Pc,ₜ Δt / Enom
− Pd,ₜ Δt / (ηd Enom)

🧓 5. Battery Degradation
Battery degradation is represented through two principal components:
Total Degradation
       │
       ├── Calendar Degradation
       │
       └── Cycle-related Degradation

The remaining usable battery capacity is represented through SOH.
When the simulated SOH falls below the defined end-of-life threshold, a battery replacement event is incorporated into the lifecycle economic model.
⚠️ The current integrated implementation uses a parameterized empirical calendar/equivalent-cycle degradation representation. It should not be interpreted as a chemistry-specific electrochemical aging model.

⚙️ 6. Energy Management System
The dispatch strategy follows a renewable-priority hierarchy.
             PV Generation
                  │
                  ▼
             Serve Load
             /         \
        Surplus       Deficit
          │              │
          ▼              ▼
     Charge BESS      Discharge BESS
          │              │
          ▼              ▼
   Export/Curtailed    Grid Import

The model tracks:
- PV generation
- Battery charging
- Battery discharging
- Grid import
- Grid export
- Curtailment
- Unserved energy
📊 7. System Performance Indicators
The framework calculates multiple energy-system KPIs.
KPI	Purpose
⚡ Reliability	Fraction of demand served
🔋 Self-Sufficiency	Reduction in grid dependence
☀️ Self-Consumption	PV used locally
♻️ Renewable Utilization	Renewable energy effectively used
🧓 SOH	Remaining battery capacity
🔄 Equivalent Cycles	Battery cycling intensity
💰 NPV	Lifecycle financial value
📉 LCOE	Lifecycle cost per useful energy
⏱️ Payback	Investment recovery period
🌐 Grid Import	Residual electricity requirement
🔌 Grid Export	Excess renewable electricity


⚖️ 8. NSGA-II Multi-Objective Optimization
The framework uses NSGA-II to identify a set of nondominated PV-BESS configurations.
Objectives
Objective 1 → Minimize LCOE
Objective 2 → Maximize Reliability

The optimization explores different combinations of:
- PV capacity
- BESS capacity
and evaluates their lifecycle performance.
Why NSGA-II?
PV-BESS design is inherently multi-objective.
A larger battery may:
↑ Reliability
↑ Renewable utilization
↓ Grid dependence

but may also:
↑ CAPEX
↑ Replacement cost
↑ Lifecycle cost

Therefore, a single "best" design may not exist.
The Pareto frontier provides multiple technically and economically defensible solutions.
🎯 Pareto Frontier
The optimization produces:
                 Reliability
                      ↑
                      │           ●
                      │        ●
                      │     ●
                      │   ●
                      │ ●
                      └──────────────────→
                              LCOE

Each Pareto-optimal point represents a different trade-off between cost and reliability.
A post-Pareto compromise selection can then be used to identify a representative design for further robustness analysis.
💰 9. Techno-Economic Analysis
The economic model considers:
Capital Costs
- PV CAPEX
- BESS CAPEX
Operating Costs
- O&M
- Grid electricity purchases
Revenue
- Electricity export
Lifecycle Effects
- Battery degradation
- Battery replacement
- Discounting
Financial Indicators
Net Present Value
NPV = −C₀ + Σ [CFₜ / (1+r)ᵗ]

Levelized Cost of Energy
LCOE =
Σ [Cₜ / (1+r)ᵗ]
────────────────────
Σ [Eₜ / (1+r)ᵗ]

Payback Period
The first year in which cumulative project savings recover the initial investment.
🎲 10. Monte Carlo Uncertainty Analysis
The framework performs:
1,000 Monte Carlo iterations
Uncertain parameters include:
- PV CAPEX
- BESS CAPEX
- Electricity tariff
- Export tariff
- Annual load
- Renewable resource
- Battery degradation
- Discount rate
Each iteration generates a new lifecycle outcome.
Reported outputs
- Median NPV
- NPV P5
- NPV P95
- Median LCOE
- LCOE P5
- LCOE P95
- Median reliability
- Probability of satisfying the reliability threshold
This converts the optimization from a deterministic design exercise into a risk-aware decision-support framework.
🧪 Experimental Design
The integrated framework evaluates progressively more realistic system configurations.
Scenario	Configuration	Purpose
🟦 S1	PV Only	Baseline
🟩 S2	PV + Idealized BESS	Quantify storage benefit
🟨 S3	PV + Degradation-aware BESS	Quantify battery aging effects
🟧 S4	Forecast-driven Degradation-aware BESS	Assess forecast/control interaction
🟥 S5	NSGA-II PV-BESS	Identify Pareto-optimal designs
🟪 S6	Optimized Design + Monte Carlo	Assess robustness


🗂️ Integration of Previous Research Projects
This project consolidates computational capabilities developed in previous projects.
Previous Project	Integrated Contribution
🇩🇪 Munich PV-BESS	SOC, DOD, degradation, replacement, LCOE, payback and sizing
☀️ Solardach Energie Dashboard	NASA POWER, PV-BESS dispatch, tariffs, savings and visualization
🏙️ Freiburg Degradation-Aware MPC	Forecast-informed dispatch and battery-aging concepts
🇮🇳 Jabalpur Hydro-PV-Wind-BESS	Renewable dispatch, reserve and stability concepts
🌐 Spatial-Temporal Storage Optimization	Future location-aware storage-planning extension
📊 Data-Driven Optimization	Future extension subject to substantive implementation


These projects are treated as prior computational building blocks. The present repository integrates selected capabilities into a common Jabalpur case-study framework.

🧪 Reproducibility
The project is designed for reproducible computational experiments.
The framework records:
- 📍 Case-study coordinates
- 📅 Analysis period
- 🌐 Data source
- ⚙️ PV parameters
- 🔋 Battery parameters
- 💰 Economic assumptions
- 📈 Optimization bounds
- 🎲 Monte Carlo parameters
- 🤖 Forecasting configuration
Machine-learning and Monte Carlo experiments can use fixed random seeds where deterministic reproducibility is required.
