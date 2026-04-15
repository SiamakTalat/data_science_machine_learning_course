# Data Science and Machine Learning Course

A structured, hands-on notebook series covering the full Python data science stack — from environment setup to machine learning capstone projects.
It will be updated.

---

## Contents

| Folder | Topics |
|--------|--------|
| [00_setup_and_tools](00_setup_and_tools/) | Course intro, environment setup, reproducible environments, Docker, Jupyter, VS Code, Colab, Kaggle, Hugging Face, GitHub |
| [01_python](01_python/) | Python crash course, generators |
| [02_numpy](02_numpy/) | NumPy fundamentals |
| [03_pandas](03_pandas/) | Pandas fundamentals, SF Salaries exercise, Ecommerce exercise |
| [04_visualization](04_visualization/) | Matplotlib, Seaborn, Pandas built-in plots, Plotly, geographical plotting, choropleth maps |
| [05_capstones](05_capstones/) | 911 Calls capstone, Finance capstone |
| [06_git](06_git/) | Git basics, branching, remotes, advanced Git, cheatsheet |

---

## How to Use

1. Clone the repository
   ```bash
   git clone https://github.com/SiamakTalat/data_science_machine_learning_course.git
   cd python-ds-ml-bootcamp
   ```

2. Set up the environment
   ```bash
   conda env create -f 00_setup_and_tools/environment.yml
   conda activate ds-env
   ```
   Or with pip:
   ```bash
   pip install -r requirements.txt
   ```

3. Launch Jupyter
   ```bash
   jupyter notebook
   ```

4. Open the notebooks in order starting from `00_setup_and_tools/`

---

## Requirements

- Python 3.9+
- Anaconda or Miniconda (recommended) — see [00_02A_Reproducible_Environments](00_setup_and_tools/00_02A_Reproducible_Environments.ipynb)
- Key packages: `pandas`, `numpy`, `matplotlib`, `seaborn`, `plotly`, `scikit-learn`, `jupyter`

---

## Structure Notes

- Each section folder contains the main notebook, exercises, and solutions
- Exercises have empty code cells for practice; solutions are in separate files
- The `06_git/` section is self-referential — it teaches Git while being managed with Git

References:
https://www.udemy.com/course/python-for-data-science-and-machine-learning-bootcamp/?srsltid=AfmBOoqGJEvQ3DKBrsIdsaSC6cm-FG3lyiRCAE-dsW7CBjc9hhusvUBO