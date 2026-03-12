![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# Lab | EDA Toolkit and Summary Pitfalls

## Overview

Descriptive statistics are the first tool you reach for when exploring a new dataset — means, medians, standard deviations, and quartiles give you a quick snapshot of what you're working with. But a snapshot can be misleading. Two datasets can share identical summary statistics yet tell completely different stories once you visualize them. This is the core lesson behind Anscombe's quartet and the Datasaurus Dozen, and it's a trap that catches even experienced analysts.

In this lab you'll build a hands-on workflow for exploratory data analysis (EDA). You'll compute summary statistics with Pandas and NumPy, then immediately pair those numbers with visualizations — histograms, boxplots, and kernel density estimates — to see what the numbers alone might hide. Along the way you'll inject outliers, compare skewed and symmetric distributions, and construct mini-cases where relying on a single summary measure would lead you to the wrong conclusion.

By the end of this lab, you'll have a repeatable EDA checklist and a healthy skepticism toward any analysis that reports numbers without plots.

## Learning Goals

By the end of this lab, you should be able to:

- Compute measures of central tendency (mean, median, mode) and spread (variance, standard deviation, IQR, range) using Pandas and NumPy.
- Create and interpret histograms, boxplots, and KDE plots to assess distribution shape.
- Explain how outliers shift the mean while leaving the median relatively stable.
- Demonstrate that identical summary statistics can arise from fundamentally different distributions.
- Choose appropriate summary statistics based on data shape and the presence of outliers.
- Apply a structured EDA workflow that pairs numerical summaries with visual inspection.

## Setup and Context

You'll work inside a Jupyter Notebook for this lab. All analysis, code, and written interpretations should live in a single notebook so that your reasoning is visible alongside the output.

This lab connects directly to the lesson on descriptive statistics and distribution shapes. You'll use the same Pandas and NumPy methods introduced in class, plus Matplotlib and Seaborn for visualization.

## Requirements

### Fork and clone

1. Fork this repository to your own GitHub account.
2. Clone the fork to your local machine.
3. Navigate into the project directory.

### Python environment

Make sure you have the following packages installed (all are standard in most data-science environments):

```bash
pip install pandas numpy matplotlib seaborn scipy
```

- **Python** ≥ 3.9
- **pandas** — data manipulation and summary statistics
- **numpy** — numerical operations and random data generation
- **matplotlib** — base plotting library
- **seaborn** — statistical visualization layer on top of Matplotlib
- **scipy** — statistical functions (optional, useful for skewness/kurtosis)

## Getting Started

1. Create a new Jupyter Notebook in the repository root called **`m3-01-eda-toolkit-summary-pitfalls.ipynb`**.
2. Start with an import cell:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats

np.random.seed(42)
sns.set_style("whitegrid")
```

3. Work through the tasks in order. Each task builds on the previous one.
4. Include markdown cells between code cells to explain your observations and reasoning.

## Tasks

### Task 1: Build and Summarize Synthetic Datasets

Start by creating three synthetic datasets that represent different distribution shapes. Each dataset should have **500** observations.

1. **Dataset A** — Symmetric: draw from a normal distribution with mean = 50 and standard deviation = 10.
2. **Dataset B** — Right-skewed: draw from an exponential distribution, then shift and scale so the values fall roughly in the 0–100 range.
3. **Dataset C** — Bimodal: combine two normal distributions (e.g., means at 30 and 70) with equal sample sizes.

For each dataset, compute and display in a summary table:
- Mean, median, mode (rounded to 2 decimals)
- Standard deviation, variance, IQR
- Skewness and kurtosis (use `scipy.stats.skew` and `scipy.stats.kurtosis`)

**Guiding question:** Which summary statistics look similar across the three datasets, and which reveal the differences?

### Task 2: Visualize the Distributions

Create a figure with **three rows and three columns** (9 subplots total). Each row represents one dataset (A, B, C). The columns are:

1. **Histogram** with 30 bins and a KDE overlay.
2. **Boxplot** (horizontal orientation).
3. **KDE plot** alone, with vertical lines marking the mean (dashed red) and median (solid blue).

Add clear titles and axis labels to every subplot. Use `plt.tight_layout()` to prevent overlap.

**Guiding question:** For which dataset(s) do the mean and median diverge the most? What visual feature explains the divergence?

### Task 3: The Outlier Stress Test

Take **Dataset A** (the symmetric one) and create a modified copy:

1. Replace the **5 largest values** with extreme outliers: multiply each by 10.
2. Compute the same summary statistics table as Task 1 for both the original and modified versions.
3. Create side-by-side boxplots (original vs. modified) and overlay the mean as a diamond marker on each.

Answer the following in a markdown cell:
- Which statistics changed the most? Which were robust?
- If you were reporting a "typical" value for the modified dataset, would you choose the mean or the median? Why?

## Submission

### What to submit

- `m3-01-eda-toolkit-summary-pitfalls.ipynb` — your completed notebook with all code, outputs, and markdown explanations.

### Definition of done (checklist)

- [ ] All three tasks are completed with code and outputs visible.
- [ ] Each task includes at least one markdown cell explaining observations.
- [ ] Plots are properly labeled with titles, axis labels, and legends where appropriate.
- [ ] The outlier stress test shows clear before/after comparison with interpretation.
- [ ] The notebook runs top-to-bottom without errors (`Kernel → Restart & Run All`).

### How to submit (Git workflow)

```bash
git add .
git commit -m "lab: complete EDA toolkit and summary pitfalls"
git push origin main
```

Then open a **Pull Request** on the original repository with a brief description of your work.
