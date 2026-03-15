# Time-Series Neural Network from Scratch

A production-grade neural network implementation built entirely in C++ for financial time-series prediction. This project demonstrates core deep learning concepts including backpropagation, optimization algorithms, and normalization techniques—implemented from first principles without external ML libraries.

## Overview

This project implements a fully-connected neural network for regression tasks on financial time-series data (e.g., EUR/USD, XAU/USD). It is designed to be lightweight, reproducible, and suitable for quantitative trading research.

## Key Features

- **Custom Neural Network Core**: Full implementation of forward propagation, backpropagation, and gradient descent in pure C++
- **Optimization**: Mini-batch SGD with Momentum and L2 weight decay
- **Regularization**: Dropout and Layer Normalization
- **Data Pipeline**: CSV parsing, Min-Max normalization, chronological time-series splits
- **Early Stopping**: Configurable patience and minimum delta for validation-based early stopping
- **Reproducibility**: Fixed random seed (42) for deterministic results

## Technical Implementation

### Architecture
- Fully-connected layers with configurable sizes
- Activation functions: ReLU, Sigmoid, Linear
- Layer Normalization (for hidden layers)
- Output layer: Linear activation for regression

### Training
- Mini-batch Stochastic Gradient Descent
- Momentum-based optimization
- L2 regularization (weight decay)
- Early stopping with validation monitoring

### Metrics
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- Mean Absolute Error (MAE)
- R² (Coefficient of Determination)

## Building the Project

```bash
# Create build directory
mkdir build && cd build

# Configure with CMake
cmake ..

# Compile
cmake --build . -j4
```

## Running the Model

```bash
# Execute from build directory
./Predicting_Close_Price_Using_NN
```

## Configuration

Modify the `run_main_training_pipeline` function in [`src/main.cpp`](src/main.cpp) to adjust:

| Parameter | Description |
|-----------|-------------|
| `input_csv_filename` | Source data file (default: XAUUSD.csv) |
| `target_column_idx` | Column index for target variable |
| `layer_sizes` | Network architecture (e.g., {64, 32, 16, 1}) |
| `activations` | Activation functions per layer |
| `learning_rate` | Learning rate (default: 0.001) |
| `num_epochs` | Training epochs |
| `batch_size` | Mini-batch size |
| `dropout_rate` | Dropout probability |
| `momentum_coeff` | Momentum coefficient |
| `weight_decay_coeff` | L2 regularization strength |
| `early_stopping_patience` | Epochs to wait before early stop |
| `validation_split_ratio` | Train/validation split (default: 0.2) |

## Project Structure

```
.
├── include/              # Header files
│   ├── NeuralNetwork.h   # Core network implementation
│   ├── Layer.h           # Layer definitions
│   ├── LayerNormLayer.h  # Layer normalization
│   ├── Activations.h     # Activation functions
│   ├── Loss.h            # Loss functions
│   └── CSVReader.h       # Data loading
├── src/                  # Implementation files
│   ├── main.cpp          # Training pipeline
│   ├── NeuralNetwork.cpp
│   ├── Layer.cpp
│   └── ...
├── CMakeLists.txt        # Build configuration
└── *.csv                 # Data files
```

## Output

The model generates:
- **Console**: Training progress, epoch metrics (MSE, RMSE, MAE, R²)
- **`validation_predictions.csv`**: Actual vs. predicted prices (both normalized and denormalized)

## Requirements

- C++20 compatible compiler (GCC 12+)
- CMake 3.10+

## Design Decisions for Quant Trading

1. **Reproducibility**: Fixed random seed ensures consistent results across runs
2. **Chronological Split**: Time-series data is split chronologically to prevent look-ahead bias
3. **Layer Normalization**: Chosen over Batch Normalization for stability in small batch sizes
4. **Early Stopping**: Prevents overfitting and reduces unnecessary computation

## License

MIT License
