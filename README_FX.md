# Triangular Arbitrage System for Forex Markets

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![NumPy](https://img.shields.io/badge/NumPy-Latest-orange.svg)](https://numpy.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Latest-150458.svg)](https://pandas.pydata.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-Latest-green.svg)](https://matplotlib.org/)

## 📋 Project Overview

This project is a **group project** developed as part of a **Mathematical Finance course**. It implements a comprehensive triangular arbitrage detection and simulation system for foreign exchange (FX) markets, focusing on the EUR/USD, USD/JPY, and EUR/JPY currency pairs.

The system models exchange rate dynamics using stochastic processes, identifies arbitrage opportunities based on cross-rate mispricing, and analyzes profitability considering realistic transaction costs.

### 👥 Course Context
- **Course**: Mathematical Finance
- **Type**: Group Project
- **Focus**: Quantitative modeling and statistical analysis of FX markets
- **Application**: Arbitrage detection and risk-free profit opportunities

## 🎯 Objectives

- Model exchange rate dynamics using geometric Brownian motion
- Simulate mispricing in cross-exchange rates
- Detect triangular arbitrage opportunities
- Analyze profitability under realistic transaction costs
- Visualize exchange rate evolution and arbitrage patterns
- Estimate statistical parameters from exchange rate data

## 📊 Key Features

### 1. Exchange Rate Modeling
- Synthetic exchange rate generation with correlated returns
- Geometric Brownian motion simulation
- Logarithmic return calculations
- Support for multiple currency pairs

### 2. Parameter Estimation
- Volatility estimation for EUR/USD and USD/JPY
- Correlation coefficient estimation between currency pairs
- Mispricing volatility (σ_ε) estimation
- Rolling window analysis for parameter stability

### 3. Mispricing Simulation
- Implied cross-rate calculation
- Normally distributed mispricing term generation
- Actual exchange rate calculation incorporating mispricing

### 4. Arbitrage Detection
- Identification of arbitrage opportunities
- Theoretical profit calculation
- Transaction cost analysis
- Feasibility assessment for real-world trading

### 5. Comprehensive Visualizations
- Exchange rate time series plots
- Implied vs actual cross-rate comparison
- Arbitrage opportunity indicators
- Profit distribution histograms
- Parameter stability analysis
- Interactive dashboards

## 🔬 Mathematical Model

### Exchange Rate Notation

- **R_EUR/USD**: Price of 1 EUR in USD
- **R_USD/JPY**: Price of 1 USD in JPY
- **R_EUR/JPY**: Price of 1 EUR in JPY

### Implied Cross Rate

The no-arbitrage condition implies:

```
R_EUR/JPY^implied = R_EUR/USD × R_USD/JPY
```

### Arbitrage Condition

An arbitrage opportunity exists when:

```
R_EUR/JPY^actual ≠ R_EUR/JPY^implied
```

### Profit Factor

The profit factor Π (multiplier of initial capital) is:

```
Π = max{ R_EUR/JPY^actual / (R_EUR/USD × R_USD/JPY), 
         (R_EUR/USD × R_USD/JPY) / R_EUR/JPY^actual }
```

### Stochastic Model

Short-term logarithmic returns follow correlated normal distributions:

```
Δr_EUR/USD ~ N(0, σ²_EU)
Δr_USD/JPY ~ N(0, σ²_UJ)
Corr(Δr_EUR/USD, Δr_USD/JPY) = ρ
```

### Mispricing Term

The actual rate includes a small random mispricing:

```
R_EUR/JPY^actual = R_EUR/JPY^implied × (1 + ε)
ε ~ N(0, σ²_ε)
```

where σ_ε is typically very small (e.g., 0.001 or 0.1%).

### Transaction Costs

Arbitrage is only profitable when:

```
Profit(ε) > Total Transaction Costs
```

## 🚀 Installation

### Prerequisites

- Python 3.8 or higher
- Jupyter Notebook or Google Colab

### Dependencies

Install required packages:

```bash
pip install numpy pandas matplotlib scipy ipywidgets
```

Or use the provided `requirements.txt`:

```bash
pip install -r requirements.txt
```

## 💻 Usage

### Running the Simulation

1. Clone the repository:
```bash
git clone https://github.com/[your-username]/triangular-arbitrage-fx.git
cd triangular-arbitrage-fx
```

2. Launch Jupyter Notebook:
```bash
jupyter notebook FX_Simulation.ipynb
```

3. Run all cells to execute the complete simulation

### Basic Example

```python
from main import run_triangular_arbitrage_simulation

# Run simulation with custom parameters
exchange_data, estimator, simulator, detector, visualizer = run_triangular_arbitrage_simulation(
    num_periods=1000,
    transaction_cost=0.0005,  # 0.05% per trade
    output_pdf="arbitrage_report.pdf"
)

# Display results
fig = visualizer.create_exchange_rate_dashboard()
plt.show()
```

### Parameter Sensitivity Analysis

```python
from main import test_with_different_parameters

# Test various scenarios
test_with_different_parameters()
```

## 📈 System Components

### 1. ExchangeRateData
Manages exchange rate data generation and storage

**Key Methods:**
- `get_rates()`: Returns DataFrame of exchange rates
- `get_returns()`: Calculates logarithmic returns
- `plot_rates()`: Visualizes exchange rate evolution

### 2. ParameterEstimator
Estimates statistical parameters from market data

**Estimated Parameters:**
- Volatility (σ_EUR/USD, σ_USD/JPY)
- Correlation coefficient (ρ)
- Mispricing volatility (σ_ε)

### 3. MispricingSimulator
Simulates cross-rate mispricing

**Functions:**
- Calculate implied cross rates
- Generate mispricing terms
- Compute actual rates with mispricing

### 4. ArbitrageDetector
Identifies and analyzes arbitrage opportunities

**Capabilities:**
- Detect arbitrage windows
- Calculate theoretical profits
- Assess feasibility with transaction costs
- Generate profitability statistics

### 5. Visualizer
Creates comprehensive analytical visualizations

**Plots:**
- Exchange rate time series
- Mispricing evolution
- Arbitrage opportunity markers
- Profit distribution histograms
- Parameter stability over time

## 📊 Key Parameters

| Parameter | Description | Default Value |
|-----------|-------------|---------------|
| `num_periods` | Number of simulation periods | 1000 |
| `transaction_cost` | Cost per trade (as decimal) | 0.0005 (0.05%) |
| `volatility_epsilon` | Mispricing volatility | 0.001 (0.1%) |
| `correlation` | EUR/USD and USD/JPY correlation | -0.84 |
| `initial_rates` | Starting exchange rates | EUR/USD: 1.13<br>USD/JPY: 143.0<br>EUR/JPY: 161.5 |
| `volatilities` | Exchange rate volatilities | EUR/USD: 0.004<br>USD/JPY: 0.0043 |

## 🔍 Sample Results

### Typical Output

The system generates:

1. **Arbitrage Detection Summary**
   - Number of arbitrage opportunities detected
   - Percentage of profitable opportunities
   - Average profit per arbitrage trade
   - Maximum observed profit

2. **Statistical Analysis**
   - Parameter estimates with confidence intervals
   - Correlation structure between currency pairs
   - Volatility stability over time

3. **Visual Reports**
   - Multi-panel dashboards
   - Time series with arbitrage markers
   - Profit distribution analysis

## 🧪 Validation

The system includes validation against:
- Historical FX market data patterns
- Excel-based reference calculations
- Theoretical no-arbitrage conditions

## 🎓 Learning Outcomes

This project demonstrates:

- Stochastic modeling in finance
- Time series analysis and simulation
- Parameter estimation techniques
- Risk-free arbitrage principles
- Market microstructure considerations
- Computational finance methods

## 📚 References

### Academic Literature
- **Triangular Arbitrage**: Theory and practice in FX markets
- **Covered Interest Parity**: Relationship between exchange rates and interest rates
- **Market Microstructure**: Transaction costs and arbitrage limits

### Key Concepts
- Geometric Brownian Motion (GBM)
- No-arbitrage pricing
- Cross-rate relationships
- Transaction cost impact on profitability

## 📝 Project Structure

```
triangular-arbitrage-fx/
├── FX_Simulation.ipynb              # Main notebook
├── README.md                        # This file
├── requirements.txt                 # Python dependencies
├── triangular_arbitrage_implementation.py
├── parameter_estimation.py
├── mispricing_calculation.py
├── arbitrage_detection.py
├── visualization.py
└── main.py                          # Main integration script
```

## 🛠️ Future Enhancements

Potential improvements:
- Real-time data integration (e.g., via APIs)
- Machine learning for arbitrage prediction
- Multi-currency arbitrage chains (beyond triangular)
- High-frequency trading considerations
- Risk management strategies
- Portfolio optimization with arbitrage opportunities

## 🤝 Contributing

This is an educational project. Feedback and suggestions for improvement are welcome!

## 📄 License

This project is developed for educational purposes as part of a Mathematical Finance course.

## 👥 Authors

**Group Project Contributors**
- Laura Cohen
- [Add other team members]

**Course**: Mathematical Finance  
**Institution**: [Your University/School]

## 🙏 Acknowledgments

- Course instructors and teaching assistants
- Mathematical Finance course materials
- Python scientific computing community
- FX market data providers

---

**Note**: This is a simulation for educational purposes. Real-world arbitrage trading involves additional complexities including:
- Market impact and slippage
- Execution speed requirements
- Regulatory constraints
- Capital requirements
- Real-time data feeds
