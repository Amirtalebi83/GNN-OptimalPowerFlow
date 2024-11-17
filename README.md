# GNN-OptimalPowerFlow

## Overview

This repository contains the implementation of **Graph Neural Networks (GNNs)** for efficient prediction of **Optimal Power Flow (OPF)** solutions in power systems. The project explores multiple GNN architectures (GCN, GAT, SAGEConv) for modeling power grids using IEEE standard test systems (14-bus, 30-bus, 57-bus, and 118-bus configurations).

The main goal of this project is to leverage GNNs to predict AC power flow variables (voltage magnitude and phase angle) efficiently, reducing computation time compared to traditional OPF solvers like Newton-Raphson and IPOPT.

## Key Features

- **Comprehensive GNN Models**: Includes implementations of GCN, GAT, and SAGEConv architectures using PyTorch Geometric.
- **Standard IEEE Test Systems**: Supports datasets for IEEE 14-bus, 30-bus, 57-bus, and 118-bus configurations with realistic load variations.
- **Pandapower Integration**: Utilizes Pandapower for dataset generation and AC power flow simulations, allowing accurate ground truth data for training and evaluation.
- **Scalable and Efficient**: Demonstrates improved scalability and efficiency for large power systems using graph-based learning methods.

## Datasets

The datasets were generated using Pandapower with realistic load variations to simulate both daily and seasonal demand patterns. Each dataset consists of:
- Input features: Active power (P), Reactive power (Q), Voltage magnitude (V), and Voltage angle (δ).
- Output targets: Predicted Voltage magnitude (V) and Voltage angle (δ).

The data is saved in Excel format (`.xlsx`), with separate files for each dataset and bus configuration.

## Methodology

1. **Dataset Generation**:
   - Uses Pandapower to generate load flow datasets with random variations in load demands.
   - Solves AC power flow equations using the Newton-Raphson method for ground truth data.
   - Each dataset contains 2000 samples with realistic load variations for training, validation, and testing.

2. **GNN Architectures**:
   - **GCN**: A simple graph convolutional network for baseline performance.
   - **GAT**: Incorporates attention mechanisms to prioritize influential nodes (e.g., generator buses).
   - **SAGEConv**: Designed for inductive learning and scalability to larger grids.

3. **Training and Evaluation**:
   - Uses PyTorch Geometric for model implementation and training.
   - Evaluates the models based on Mean Squared Error (MSE), Normalized Root Mean Squared Error (NRMSE), and \( R^2 \) scores.
   - Compares GNN models against traditional OPF solvers for performance benchmarking.

## Installation

### Prerequisites

- Python 3.8 or higher
- Pandapower
- PyTorch
- PyTorch Geometric
- Matplotlib
- Pandas

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/Amirtalebi83/GNN-OptimalPowerFlow.git
   cd GNN-OptimalPowerFlow
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Usage

### Dataset Generation

Run the dataset generation script for the IEEE 30-bus system:
```bash
python generate_datasets.py
```

This will generate 10 Excel files containing load flow data for training and testing.

### Training the GNN Model

To train the GNN model on the 30-bus dataset using the GAT architecture:
```bash
python train_model.py --dataset "datasets_30Bus" --model "GAT"
```

### Evaluation

Evaluate the trained model and visualize the results:
```bash
python evaluate_model.py --model_path "saved_models/gat_30bus.pth"
```

## Results

The performance of each GNN architecture was evaluated using the following metrics:
- **Normalized Root Mean Squared Error (NRMSE)**: Consistently below 0.05 for all models across different bus systems.
- **\( R^2 \) Score**: High \( R^2 \) scores indicate strong predictive performance, especially for the GAT and SAGEConv models.
- **Average Test Loss**: Lower average test loss for SAGEConv, indicating strong generalization and scalability.

| Model     | NRMSE (30-bus) | \( R^2 \) Score (30-bus) | Average Test Loss |
|-----------|----------------|--------------------------|-------------------|
| GCN       | 0.042          | 0.92                     | 0.015             |
| GAT       | 0.025          | 0.97                     | 0.008             |
| SAGEConv  | 0.018          | 0.98                     | 0.005             |

## Visualization

Training and evaluation results, including loss curves and performance metrics, are available in the `results/` folder.

## Contributing

Feel free to submit issues or pull requests if you have suggestions or improvements.


## Acknowledgments

Special thanks to the PyTorch Geometric and Pandapower communities for providing excellent tools for graph-based machine learning and power flow analysis.
