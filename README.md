# SDL Repository Index

This directory contains the complete SDL Formulation Lab split into independent repositories.

## Repositories

| Repository | Description | Dependencies |
|------------|-------------|--------------|
| `sdl-core` | Simulation infrastructure (surrogates, noise, validation) | numpy, pandas, scikit-learn |
| `sdl-strategies` | Optimization strategies (BO, meta-optimization) | sdl-core |
| `sdl-orchestration` | Rules, planning, governance (ALCOA+) | sdl-core, sdl-strategies |
| `sdl-benchmarks` | Datasets and data loaders | numpy, pandas |
| `sdl-analysis` | Metrics, statistics, visualization | numpy, pandas, matplotlib |
| `sdl-experiments` | Experiment runners and scenarios | all above |
| `sdl-formulation-lab` | Meta-package with CLI and dashboard | all above |

## Dependency Graph

```
sdl-formulation-lab (meta)
    │
    ├── sdl-experiments
    │       │
    │       ├── sdl-analysis
    │       │
    │       ├── sdl-orchestration
    │       │       │
    │       │       ├── sdl-strategies
    │       │       │       │
    │       │       │       └── sdl-core
    │       │       │
    │       │       └── sdl-core
    │       │
    │       ├── sdl-benchmarks
    │       │
    │       └── sdl-core
    │
    └── (all packages)
```

## Installation Order

For development, install in this order:

```bash
cd sdl-core && pip install -e ".[dev]"
cd ../sdl-strategies && pip install -e ".[dev]"
cd ../sdl-orchestration && pip install -e ".[dev]"
cd ../sdl-benchmarks && pip install -e ".[dev]"
cd ../sdl-analysis && pip install -e ".[dev]"
cd ../sdl-experiments && pip install -e ".[dev]"
cd ../sdl-formulation-lab && pip install -e ".[dev]"
```

Or install the meta-package which pulls all dependencies:

```bash
pip install sdl-formulation-lab[all]
```

## Quick Start

After installation:

```python
from sdl_lab import (
    FormulationSimulator,
    load_ros_dataset,
    ExperimentRunner,
)

# Load data and run optimization
data = load_ros_dataset()
simulator = FormulationSimulator.fit(data)
runner = ExperimentRunner(simulator=simulator, strategy="batch_bo", budget=256)
results = runner.run()
```
