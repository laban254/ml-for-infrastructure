# Setup & Installation Guide

Get started with the SRE Intelligence Hub in minutes.

## Prerequisites

- **Python 3.10+**
- **pip** (Python package manager)
- **git** (for cloning the repository)

## Installation Steps

### 1. Clone the Repository

```bash
git clone https://github.com/laban254/ml-for-infrastructure.git
cd ml-for-infrastructure
```

### 2. Create a Virtual Environment (Recommended)

```bash
# Using venv
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Or using conda
conda create -n sre-hub python=3.10
conda activate sre-hub
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

This installs the lightweight core stack:
- **Data Science**: NumPy, Pandas, SciPy
- **Visualization**: Matplotlib, Seaborn
- **Machine Learning**: Scikit-learn
- **Jupyter + interactivity**: Jupyter, IPython, ipywidgets

For the deep-learning and MLOps notebooks (`04_deep_learning/`, `pyspark`, `mlflow`,
`llm_finetuning`), also install the heavier stack:

```bash
pip install -r requirements-deep.txt
```

This adds TensorFlow, PyTorch, PySpark (needs a JDK on your PATH), MLflow, and the
Hugging Face fine-tuning libraries (GPU recommended for `llm_finetuning`).

### 4. Verify Installation

```bash
python -c "import numpy, pandas, sklearn, tensorflow; print('✓ All packages installed successfully')"
```

### 5. Start Jupyter

```bash
# Jupyter Notebook
jupyter notebook

# Or Jupyter Lab (recommended)
jupyter lab
```

Then navigate to a notebook like `01_foundations/numpy/numpy.ipynb`.

## Data Setup

### Quick Start (Recommended for First Run)

```bash
python fetch_data.py --quick
```

This downloads small sample datasets for fast iteration.

### Full Datasets

```bash
python fetch_data.py --full
```

This downloads complete datasets for production-grade training.

### Verify Data

```bash
python fetch_data.py --verify
```

Checks data integrity against known hashes.

## Execution Modes

### Toggle Mode from CLI

```bash
# Show current mode
python notebook_toggle.py --show

# Set quick mode (fast iterations, 100 samples)
python notebook_toggle.py --mode quick

# Set full mode (complete datasets, 1000 samples)
python notebook_toggle.py --mode full
```

### Set Mode via Environment Variable

```bash
export NOTEBOOK_MODE=quick   # or "full"
jupyter notebook
```

## Troubleshooting

### Issue: Package not found
**Solution**: Ensure virtual environment is activated and requirements are installed.
```bash
source venv/bin/activate
pip install -r requirements.txt
```

### Issue: Jupyter not found
**Solution**: Install jupyter explicitly:
```bash
pip install jupyter jupyterlab
```

### Issue: Data download fails
**Solution**: Check internet connection or use alternative:
```bash
python fetch_data.py --status  # Check current data status
```

### Issue: CUDA/GPU errors (for GPU users)
The project works with CPU by default. For GPU support:
```bash
pip install tensorflow-gpu
```

## Next Steps

1. **Start with Foundations**: Begin with `01_foundations/numpy/numpy.ipynb` or `01_foundations/pandas/Pandas.ipynb`
2. **Read Topic READMEs**: Each topic folder has a README.md with learning objectives
3. **Try Quick Mode**: Run notebooks in quick mode to understand concepts
4. **Run Full Mode**: Switch to full mode for complete training runs
5. **Check CONTRIBUTING.md**: Learn about best practices for adding new content

## Resources

- [NumPy Documentation](https://numpy.org/doc/)
- [Pandas Documentation](https://pandas.pydata.org/)
- [Scikit-learn Documentation](https://scikit-learn.org/)
- [TensorFlow/Keras Documentation](https://www.tensorflow.org/)
- [Matplotlib Documentation](https://matplotlib.org/)
- [Seaborn Documentation](https://seaborn.pydata.org/)

## Getting Help

- Check the relevant topic's README.md for learning objectives
- Look for `GOTCHAS.md` files (e.g., in numpy/) for common pitfalls
- See `CONTRIBUTING.md` for coding standards and best practices
- Open an issue on GitHub for bugs or feature requests
