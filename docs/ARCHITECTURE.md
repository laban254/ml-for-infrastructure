# Architecture & Project Structure

Understand the organization and design of the SRE Intelligence Hub.

## Directory Structure

```
sre-intelligence-hub/
├── docs/                           # Documentation
│   ├── SETUP.md                   # Installation & setup guide
│   ├── ARCHITECTURE.md            # This file
│   ├── DEVELOPMENT.md             # Developer guide
│   └── CONTRIBUTING.md            # Contribution guidelines
│
├── 01_foundations/                 # Core data science concepts
│   ├── numpy/                     # Numerical computing
│   │   ├── numpy.ipynb            # Main notebook
│   │   ├── README.md
│   │   ├── requirements.txt
│   │   └── GOTCHAS.md            # Common pitfalls
│   ├── pandas/                    # Data manipulation
│   │   ├── Pandas.ipynb
│   │   └── README.md
│   └── distributed_data/          # BigData processing
│       └── pyspark_log_processing.ipynb
│
├── 02_visualization/              # Data visualization
│   ├── matplotlib/                # Static plots
│   │   ├── matplotlib.ipynb
│   │   └── README.md
│   └── seaborn/                   # Statistical visualization
│       ├── seaborn.ipynb
│       └── README.md
│
├── 03_machine_learning/           # ML algorithms & pipelines
│   └── scikit-learn/
│       ├── ensemble-methods/      # Bagging, boosting, stacking
│       ├── model-evaluation-and-selection/  # Metrics, CV, GridSearch
│       ├── model-pipelines/       # Production pipelines
│       ├── preprocessing/         # Encoding, scaling, imputation
│       ├── supervised-learning-algorithms/  # Classification, regression
│       ├── tools-for-working-with-data/     # Dataset utilities
│       └── unsupervised-learning-algorithms/  # Clustering, dim reduction, anomaly
│
├── 04_deep_learning/              # Neural networks
│   ├── keras/                     # Keras/TensorFlow
│   │   └── Basic_Keras_MNIST_Practice.ipynb
│   └── pytorch/                   # PyTorch
│       └── 05_timeseries_lstm.ipynb
│
├── 05_sre_applications/           # Infrastructure & operations ML
│   ├── anomaly_detection/         # Detect infrastructure anomalies
│   ├── llm_finetuning/            # LLM fine-tuning for ops
│   ├── log_analysis/              # Log clustering & analysis
│   ├── mlops_tracking/            # ML experiment tracking (MLflow)
│   └── model_monitoring/          # Data drift detection
│
├── tools/
│   ├── fetch_data.py              # Centralized data fetching with verification
│   └── notebook_toggle.py         # Quick/Full mode toggling
│
├── README.md                       # Main project overview
├── requirements.txt                # Unified dependencies
├── CONTRIBUTING.md                 # (moved to docs/)
├── AGENTS.md                       # (moved to docs/DEVELOPMENT.md)
├── .github/                        # GitHub workflows & templates
└── .gitignore                      # Git ignore patterns
```

## Design Principles

### 1. **Progressive Complexity**
Content flows from foundations (NumPy, Pandas) → visualization → ML algorithms → deep learning → SRE applications.

### 2. **Topic Isolation**
Each topic directory is self-contained with its own:
- Notebooks (explanatory + exercises + solutions)
- `README.md` (learning objectives)
- `requirements.txt` (topic-specific packages)
- `.gitignore` (output files)

### 3. **Reproducibility**
- All code uses `random_state=42` for deterministic results
- `fetch_data.py` verifies data integrity via MD5 hashes
- `notebook_toggle.py` enables consistent quick/full modes
- Output files are gitignored to keep repos clean

### 4. **Fast Iteration & Production Ready**
- **Quick Mode**: 100 samples, 10 iterations, single-threaded (for teaching)
- **Full Mode**: 1000 samples, 100 iterations, parallel processing (for real work)
- Mode controlled via environment variables or CLI

### 5. **Observability-First**
05_sre_applications teaches ML for infrastructure:
- Anomaly detection (Isolation Forest for DDoS, DB locks)
- Log clustering (unsupervised grouping of production logs)
- Model monitoring (drift detection with KS-test)
- Operational metrics (precision over accuracy)

## Data Flow

```
┌─────────────────────┐
│ fetch_data.py       │  ← Centralized data management
├─────────────────────┤
│ Verification: MD5   │  ← Hash check for integrity
├─────────────────────┤
│ Quick/Full modes    │  ← Sample size & iteration control
├─────────────────────┤
│ Notebooks load data │  ← Reproducible training
└─────────────────────┘
```

## Execution Modes

| Aspect | Quick Mode | Full Mode |
|--------|-----------|-----------|
| **Samples** | 100 | 1000 |
| **Iterations** | 10 | 100 |
| **CV Folds** | 2 | 5 |
| **Parallel Jobs** | 1 | -1 (all cores) |
| **Use Case** | Teaching, debugging | Production training |
| **Set via** | `NOTEBOOK_MODE=quick` | `NOTEBOOK_MODE=full` |

## Key Files

### Configuration & Tools
- `fetch_data.py`: Downloads datasets with hash verification
- `notebook_toggle.py`: Switches notebook execution modes
- `requirements.txt`: Unified Python dependencies
- `.gitignore`: Excludes outputs, data, virtual environments

### Documentation
- `README.md`: Main project overview (in root)
- `docs/SETUP.md`: Installation & configuration
- `docs/ARCHITECTURE.md`: This file
- `docs/DEVELOPMENT.md`: Developer & agent guidance
- `docs/CONTRIBUTING.md`: Contribution standards
- Topic `README.md` files: Learning objectives for each module

## Typical Notebook Structure

Each notebook follows this pattern:

1. **Imports & Configuration**: Load libraries, set seeds, configure mode
2. **Learning Objectives**: Clear goals for the section
3. **Dataset Loading**: Using `fetch_data.py` for consistency
4. **Explanatory Cells**: Markdown + code demonstrating concepts
5. **Visualizations**: Charts & plots with matplotlib/seaborn
6. **Exercises**: Challenges for learners
7. **Solutions**: Answer keys (often in separate `-solution.ipynb`)

## CI/CD & Quality

- **Output Policy**: Clear all notebook outputs before committing
- **Testing**: `jupyter nbconvert --execute` for smoke tests
- **Formatting**: Follow PEP 8 style guide
- **Reproducibility**: MD5 hashes, fixed seeds, version pins

## Adding New Content

### To Add a New Topic:

```bash
# Create topic directory
mkdir 03_machine_learning/my-topic

# Create structure
touch 03_machine_learning/my-topic/README.md
touch 03_machine_learning/my-topic/requirements.txt
touch 03_machine_learning/my-topic/.gitignore
```

### To Add a New Notebook:

1. Follow naming: `{topic}.ipynb` or `{topic}-exercise.ipynb`
2. Use template from `CONTRIBUTING.md`
3. Set `random_state=42` everywhere
4. Test in both quick and full modes
5. Clear outputs: `jupyter nbconvert --clear-output --inplace notebook.ipynb`

## Philosophy

**Precision over Accuracy**: The hub prioritizes practical, operational metrics (precision, recall) over simple accuracy metrics. This prevents "alert fatigue" in production monitoring systems.
