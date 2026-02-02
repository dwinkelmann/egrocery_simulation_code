# Inventory Optimization for Perishable Goods

This repository contains the implementation for the article: **"Managing inventories for perishable e-groceries: The value of probabilistic information"**.

The code simulates an inventory management system with various uncertain parameters (demand, spoilage, supply). I uses a stochastic lookahead policy  to determine orders that minimize the total expected cost, including holding, spoilage, and stockout (underage) costs.


## Getting Started

### Prerequisites

You will need Python 3.7+ and the dependencies listed in `requirements.txt`.

```bash
pip install -r requirements.txt
```

### Running the Experiments

The core of the experiments is contained in the Jupyter notebook `Inventory_Code_final.ipynb`.

1. **Open the Notebook**:
   ```bash
   jupyter notebook Inventory_Code_final.ipynb
   ```

### Parameter Definitions

The simulation is configured using the following parameters in the **"Simulation Parameters"** cell:

| Parameter | Description |
| :--- | :--- |
| `h` | Spoilage cost per unit of product. |
| `v` | Inventory holding cost per unit per period. |
| `b` | Underage (out-of-stock) cost per unit. |
| `lambda_mu` | Mean of the Poisson-distributed demand parameter. |
| `lambda_omega` | Variance-related parameter for the demand distribution. |
| `tau` | Lead time (delay between placing an order and its arrival). |
| `nu` | Planning/look-ahead horizon for the optimization algorithm. |
| `rho` | Discount factor for future costs within the planning horizon. |
| `number_of_simulation_periods` | Total number of periods to simulate for the evaluation run. |
| `number_of_optimisation_paths` | Number of Monte Carlo paths used during each optimization step. |
| `seed` | Random seed for reproducibility. |

#### Assessing the Value of Probabilistic Information

The following parameters allow you to assess the **Value of Probabilistic Information** by comparing the stochastic model against deterministic benchmarks:

- `demand_is_deterministic`: If `True`, the model assumes future demand is fixed at the mean value.
- `supply_is_deterministic`: If `True`, the model assumes future supply is fixed at its stationary average.
- `spoilage_is_deterministic`: If `True`, spoilage occurs according to expected rates rather than stochastically.

By toggling these flags, you can quantify how much cost reduction is achieved by accurately modeling the underlying probabilistic distributions compared to using simple average values.

3. **Run Simulation**:
   Execute the cell containing `run_experiment()`. This will:
   - Generate evaluation data paths.
   - Run the optimization-based simulation loop.
   - Output summary statistics (Average Cost, Service Level, etc.).

4. **Run Newsvendor Benchmark**:
   At the end of the notebook, you can run the `run_newsvendor_benchmark()` function to see how a static base-stock policy compares to the optimized model.

### Programmatic Parameter Sweeps

You can run multiple experiments by calling the functions in a loop. A commented-out example is provided at the end of the simulation section:

```python
# Example: Varying the underage cost 'b'
b_values = [1, 2, 5, 10]
for b_val in b_values:
    results = run_experiment(b=b_val)
    print(f"Results for b={b_val}: {results[1]}") # Print avg cost
```

## Project Structure

- `Inventory_Code_final.ipynb`: Main implementation and experimental notebook.
- `requirements.txt`: Python dependencies.

