# econ5200-lab03-eda-diagnostics

## Pipeline Health Check — EDA, Corruption & Distribution Shift

### Objective
This project develops and validates a systematic exploratory data analysis (EDA) workflow for detecting data-quality issues and distributional drift in a real-world country-level panel dataset, establishing reusable diagnostics for production data pipelines.

### Methodology
- Conducted manual EDA on a country panel dataset to identify data-quality issues without relying on automated profiling tools
- Detected and resolved 6 planted data-quality issues, including:
  - Negative GDP values
  - Life expectancy recorded in months instead of years
  - Duplicate records
  - Mixed percentage units (e.g., 0–1 scale vs. 0–100 scale)
  - A GDP unit mismatch (e.g., millions vs. billions)
- Quantified distribution shift between training and inference datasets using the Population Stability Index (PSI), computing a GDP PSI of 2.4589 on a dataset with a deliberate 1.3x scaling shift introduced in the inference set
- Benchmarked manual EDA findings against `ydata-profiling` output, documenting specific issues the automated tool missed and why manual inspection remained necessary
- Authored `eda_utils.py`, a reusable module containing:
  - Impossible-value detection functions
  - PSI calculation functions
  - Summary statistics utilities
- Built an interactive dashboard for ongoing pipeline health monitoring

### Key Findings
- Manual EDA surfaced data-quality issues that automated profiling tools either flagged ambiguously or missed entirely, underscoring the continued need for domain-aware manual review alongside automated tooling
- A GDP PSI of **2.4589** confirms a significant distribution shift between training and inference — consistent with a deliberate 1.3x scaling introduced in the inference set, well above the 0.25 threshold that would typically trigger model retraining or feature revalidation
- The resulting `eda_utils.py` module and dashboard provide a repeatable framework for catching similar data-quality and drift issues in future pipeline runs
