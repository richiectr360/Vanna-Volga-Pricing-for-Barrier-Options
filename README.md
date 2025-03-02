# Vanna-Volga Pricing for Barrier Options

## Overview
This project implements the **Vanna-Volga method** for pricing **FX barrier options**, incorporating volatility adjustments to improve accuracy compared to the standard Black-Scholes model. The approach provides closed-form solutions for **Delta, Vega, Vanna, and Volga**, ensuring more precise pricing in the FX derivatives market.

## Features
- Pricing for **vanilla European options** (call/put)
- Pricing for **barrier options** (up-in, up-out, down-in, down-out)
- Implementation of **Black-Scholes model** for base calculations
- **Vanna-Volga adjustments** to refine option pricing
- **Visualization of option pricing** for comparative analysis

## Methodology
### 1. Black-Scholes Foundation
The model first calculates vanilla option prices using the **Black-Scholes formula**:

\[ C = S e^{-r_f T} \Phi(d_1) - K e^{-r_d T} \Phi(d_2) \]

where:
- \( S \) = Spot price
- \( K \) = Strike price
- \( T \) = Time to maturity
- \( r_f, r_d \) = Foreign & domestic risk-free rates
- \( \Phi(d) \) = Standard normal cumulative distribution function
- \( d_1 \) and \( d_2 \) computed using the Black-Scholes model

### 2. Barrier Option Adjustments
For **barrier options**, pricing is adjusted based on the option type:
- **Up-In**: Activated only if the price rises above the barrier level
- **Up-Out**: Expires worthless if the price exceeds the barrier level
- **Down-In**: Activated only if the price falls below the barrier level
- **Down-Out**: Expires worthless if the price drops below the barrier level

### 3. Vanna-Volga Correction
The **Vanna-Volga method** corrects standard Black-Scholes pricing by incorporating second-order sensitivity to volatility:
- **Vanna**: Sensitivity to changes in volatility & spot price correlation
- **Volga**: Sensitivity to changes in volatility itself

The adjustment refines the implied volatility surface, aligning the pricing model with market quotes.

## Code Implementation
The implementation is structured using an **object-oriented approach** with a class-based design.

### `FXBarrierOption` Class
This class models FX barrier options with the following parameters:
- **spot_price**: Current price of the underlying asset
- **strike_price**: Option's strike price
- **time_to_maturity**: Time to maturity (in years)
- **volatility**: Annualized volatility
- **domestic_rate**: Domestic risk-free interest rate
- **foreign_rate**: Foreign risk-free interest rate
- **barrier_level**: Barrier threshold (for barrier options)
- **barrier_type**: Type of barrier option (up-in, up-out, down-in, down-out)

### Key Methods
#### `compute_d1(spot_price=None)`
Computes the Black-Scholes \( d_1 \) value.

#### `compute_d2(d1=None)`
Computes the Black-Scholes \( d_2 \) value.

#### `calculate_vanilla_price(option_type='call')`
Calculates the price of a **vanilla European option** (call/put).

#### `calculate_barrier_price()`
Computes the price of a **barrier option** based on its type.

#### Private Methods
- **`_down_and_in_call_price()`**: Computes the price of a down-and-in call option.

## Visualization
A **plotting function** visualizes the price comparison between vanilla and barrier options as the **spot price varies**. This helps illustrate the impact of barriers on option prices.

## Conclusion
This implementation provides an efficient method to price **FX barrier options** using the **Vanna-Volga approach**. By integrating market-based volatility adjustments, it improves accuracy over traditional Black-Scholes models.

## Dependencies
- Python 3.x
- NumPy
- SciPy
- Matplotlib

## Usage
```python
from fx_barrier_option import FXBarrierOption

# Define an up-and-in barrier option
option = FXBarrierOption(
    spot_price=100,
    strike_price=105,
    time_to_maturity=1,
    volatility=0.2,
    domestic_rate=0.03,
    foreign_rate=0.01,
    barrier_level=110,
    barrier_type='up-in'
)

# Compute prices
vanilla_price = option.calculate_vanilla_price()
barrier_price = option.calculate_barrier_price()

print(f"Vanilla Option Price: {vanilla_price}")
print(f"Barrier Option Price: {barrier_price}")
```

## License
MIT License
