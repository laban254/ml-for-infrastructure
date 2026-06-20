# Getting Started with ML for Infrastructure

A quick guide to start learning about ML for Infrastructure.

## Zero-install option (fastest)

Don't want to install anything? Open any notebook and click the **Open in Colab** or **Open in Binder** badge at the top — it runs in a free cloud runtime in your browser. Notebooks are committed with their outputs already rendered, so you can also just read them on GitHub.

For hands-on local work, follow the quickstart below.

## 5-Minute Quickstart

### Step 1: Install
```bash
git clone https://github.com/laban254/ml-for-infrastructure.git
cd ml-for-infrastructure
pip install -r requirements.txt           # light core stack (foundations, viz, sklearn)
python fetch_data.py --quick

# Optional — only for 04_deep_learning + pyspark/mlflow notebooks:
pip install -r requirements-deep.txt
```

### Step 2: Launch Jupyter
```bash
jupyter lab
```

### Step 3: Open Your First Notebook
Navigate to: `01_foundations/numpy/numpy.ipynb`

### Step 4: Run Cells
Click the play button or press `Shift + Enter` to execute cells.

---

## Learning Path

### Beginner (Weeks 1-2)
**Goal**: Understand data structures and basic operations

1. **NumPy** (`01_foundations/numpy/numpy.ipynb`)
   - Arrays, broadcasting, linear algebra
   - Read: `01_foundations/numpy/GOTCHAS.md`

2. **Pandas** (`01_foundations/pandas/Pandas.ipynb`)
   - Series, DataFrames, data cleaning
   - Reading/writing data

3. **Matplotlib** (`02_visualization/matplotlib/matplotlib.ipynb`)
   - Line, scatter, bar plots
   - Customization & styling

### Intermediate (Weeks 3-4)
**Goal**: Learn ML algorithms and visualization techniques

1. **Seaborn** (`02_visualization/seaborn/seaborn.ipynb`)
   - Statistical visualization
   - Heatmaps, pair plots, distributions

2. **Preprocessing** (`03_machine_learning/scikit-learn/preprocessing/`)
   - Scaling, encoding, imputation
   - Pipeline concept

3. **Supervised Learning** (`03_machine_learning/scikit-learn/supervised-learning-algorithms/`)
   - Classification (logistic regression, SVM)
   - Regression (linear, ridge, lasso)

### Advanced (Weeks 5-6)
**Goal**: Master model evaluation and production patterns

1. **Model Evaluation** (`03_machine_learning/scikit-learn/model-evaluation-and-selection/`)
   - Cross-validation, metrics
   - GridSearch for hyperparameter tuning

2. **Ensembles** (`03_machine_learning/scikit-learn/ensemble-methods/`)
   - Bagging, boosting, stacking
   - Random forests, gradient boosting

3. **Pipelines** (`03_machine_learning/scikit-learn/model-pipelines/`)
   - Scikit-learn pipelines
   - Production-ready models

### Expert (Weeks 7-8)
**Goal**: Apply ML to infrastructure and operations

1. **Deep Learning** (`04_deep_learning/`)
   - Keras MNIST classification
   - PyTorch LSTM for time series

2. **SRE Applications** (`05_sre_applications/`)
   - Anomaly detection for infrastructure
   - Log clustering and analysis
   - Model monitoring & drift detection

---

## Common Workflows

### Run Notebook in Quick Mode (Fast)
```bash
export NOTEBOOK_MODE=quick
jupyter lab
# Notebook will use 100 samples, 10 iterations
```

### Run Notebook in Full Mode (Complete)
```bash
export NOTEBOOK_MODE=full
jupyter lab
# Notebook will use 1000 samples, 100 iterations
```

### Toggle Mode from Notebook
```python
from notebook_toggle import get_mode, toggle_mode

# Check mode
mode = get_mode()  # "quick" or "full"
print(f"Running in {mode} mode")

# Conditionally set parameters
if mode == "quick":
    n_samples = 100
    n_iter = 10
else:
    n_samples = 1000
    n_iter = 100
```

### Toggle Mode from CLI
```bash
python notebook_toggle.py --show       # Show current
python notebook_toggle.py --mode quick # Set quick
python notebook_toggle.py --mode full  # Set full
```

---

## Tips & Tricks

### 1. Use Jupyter Shortcuts
- `Shift + Enter`: Run cell
- `Ctrl + /`: Comment/uncomment
- `Tab`: Autocomplete
- `Shift + Tab`: Show docstring

### 2. Clear Old Outputs Before Committing
```bash
jupyter nbconvert --clear-output --inplace *.ipynb
```

### 3. Check Data Status
```bash
python fetch_data.py --status
```

### 4. Verify Data Integrity
```bash
python fetch_data.py --verify
```

### 5. Explore Topic READMEs
Each topic has a `README.md` with learning objectives:
```bash
cat 01_foundations/numpy/README.md
cat 01_foundations/pandas/README.md
cat 03_machine_learning/scikit-learn/preprocessing/README.md
```

---

## Keyboard Shortcuts in Jupyter

| Shortcut | Description |
|----------|-------------|
| `Shift + Enter` | Run cell and move to next |
| `Ctrl + Enter` | Run cell (stay in place) |
| `Alt + Enter` | Run cell and insert new cell |
| `Ctrl + Shift + -` | Split cell at cursor |
| `Esc` then `A` | Insert cell above |
| `Esc` then `B` | Insert cell below |
| `Esc` then `D` + `D` | Delete cell |
| `Ctrl + /` | Toggle comment |
| `Ctrl + Z` | Undo |
| `Ctrl + Y` | Redo |

---

## Structure at a Glance

```
01_foundations/     ← Start here: NumPy, Pandas, data basics
        ├── numpy/
        ├── pandas/
        └── distributed_data/

02_visualization/   ← Plotting & visualization
        ├── matplotlib/
        └── seaborn/

03_machine_learning/  ← Algorithms & ML patterns
        └── scikit-learn/
            ├── preprocessing/
            ├── supervised-learning-algorithms/
            ├── unsupervised-learning-algorithms/
            ├── ensemble-methods/
            ├── model-evaluation-and-selection/
            └── model-pipelines/

04_deep_learning/   ← Neural networks
        ├── keras/
        └── pytorch/

05_sre_applications/  ← Real-world ops use cases
        ├── anomaly_detection/
        ├── log_analysis/
        ├── llm_finetuning/
        ├── mlops_tracking/
        └── model_monitoring/
```

---

## Next Steps

1. **Try a notebook**: Open `01_foundations/numpy/numpy.ipynb` in Jupyter Lab
2. **Run in quick mode**: Set `export NOTEBOOK_MODE=quick` for fast execution
3. **Read CONTRIBUTING.md**: Understand best practices for working with notebooks
4. **Check SETUP.md**: For detailed installation and troubleshooting

## FAQ

**Q: What Python version do I need?**
A: Python 3.10 or higher. Check with `python --version`.

**Q: Can I run this on GPU?**
A: Yes! Install `tensorflow-gpu` or use PyTorch CUDA support. Most notebooks work on CPU.

**Q: How do I contribute?**
A: See `docs/CONTRIBUTING.md` for standards and guidelines.

**Q: Where's the data downloaded?**
A: Check with `python fetch_data.py --status`. Default is `./data/`.

**Q: Can I use these notebooks in production?**
A: The patterns are production-ready, but ensure proper testing and validation for your use case.

---

## Need Help?

- 📖 Check the **topic README.md** files for learning objectives
- 🐛 Look for **GOTCHAS.md** (e.g., in numpy/) for common pitfalls  
- 📝 See **CONTRIBUTING.md** for coding standards
- 💬 Open an issue on GitHub
