# Guidelines for Junior Bioinformaticians

## Best Practices in Software Engineering & Data Analysis

# 1. Mindset First: Think Like an Engineer, Not Just an Analyst

Bioinformatics is not just about “getting results” — it’s about producing:

-   ✅ Reproducible analyses

-   ✅ Reliable pipelines

-   ✅ Interpretable outputs

-   ✅ Maintainable code

-   ✅ Transparent decisions

If someone cannot rerun your analysis in 6 months, it is not finished.

# 2. Reproducibility Is Non-Negotiable

## 2.1 Version Control (Always Use Git)

-   Every project lives in a Git repository.

-   Commit small, logical changes.

-   Write meaningful commit messages:

    -   ❌ `fix stuff`

    -   ✅ `Fix indexing bug in normalization step`

-   Use branches for:

    -   New features

    -   Major refactoring (restructuring code)

    -   Experimental analyses (exploration)

## 2.2 Environment Management

Never rely on your local setup.

Use:

-   `conda` / `mamba`

-   `venv`

-   `renv` (R)

-   Docker / Singularity for pipelines

Always:

-   Export environment files (`environment.yml`, `requirements.txt`)

-   Pin versions for critical dependencies

## 2.3 Workflow Management

Avoid long ad-hoc scripts.

Use workflow managers:

-   Nextflow

-   Snakemake

-   targets (R)

Benefits:

-   Scalable

-   Traceable

-   HPC/cloud compatible

-   Reproducible by design

-   Parallel execution

------------------------------------------------------------------------

# 3. Code Quality Principles

## 3.1 Write Readable Code

Code is read far more than written.

-   Use meaningful variable names

    -   ❌ `x`, `tmp`, `df2`

    -   ✅ `normalized_counts`, `sample_metadata`

-   Keep functions short and focused.

-   One function → one responsibility.

------------------------------------------------------------------------

## 3.2 Modular Design

Avoid monolithic scripts.

Core Principle

> Separate *what you are thinking* from *what you are delivering*.

Exploration and production serve different purposes and must not live in the same place.

-   Exploration = hypothesis generation, rapid iteration, trial-and-error

-   Production = clean, parameterized, reproducible, documented execution

-   If they are mixed, reproducibility collapses.

------------------------------------------------------------------------

### 3.2.1 Design Code as Layers

Think in layers rather than scripts.

**Layer 1 — Configuration**

-   Parameters

-   File paths

-   Thresholds

-   Model settings

These must never be hard-coded inside analysis scripts.

Use:

-   `config.yaml`

-   `params.json`

------------------------------------------------------------------------

**Layer 2 — Reusable Logic (src/)**

Reusable components go here:

-   Data loading functions

-   Normalization routines

-   QC functions

-   Plotting utilities

-   Statistical wrappers

-   Rules:

    -   No hard-coded file paths

    -   No direct writing to results/

    -   Functions only

------------------------------------------------------------------------

**Layer 3 — Pipeline / Execution**

Workflow manager or driver scripts that:

-   Call reusable modules

-   Pass configuration

-   Control execution order

-   Generate structured outputs

-   This is the "production engine".

------------------------------------------------------------------------

**Layer 4 — Exploration**

Jupyter / RMarkdown notebooks used to:

-   Test ideas

-   Explore distributions

-   Try alternative models

-   Validate assumptions

Notebooks are not the final product.

------------------------------------------------------------------------

### 3.2.2 Recommended Project Folder Structure

Below is a clean, scalable structure aligned with Sections 3.2 and 4.2.

```         
project_name/
│
├── README.md
├── config/
│   └── config.yaml
│
├── data/
│   ├── raw/            # immutable input data
│   ├── external/       # reference files, annotations
│   └── interim/        # temporary processed files
│
├── metadata/
│   └── sample_sheet.csv
│
├── src/                # reusable functions and modules
│   ├── io.py
│   ├── qc.py
│   ├── normalization.py
│   ├── modeling.py
│   └── visualization.py
│
├── workflows/          # pipeline definitions
│   ├── Snakefile
│   └── nextflow.config
│
├── notebooks/
│   ├── 01_exploration_qc.ipynb
│   ├── 02_model_testing.ipynb
│   └── scratch/
│
├── scripts/            # thin execution wrappers
│   └── run_analysis.py
│
├── results/
│   ├── qc/
│   ├── figures/
│   ├── tables/
│   └── reports/
│
├── logs/
│
├── env/
│   ├── environment.yml
│   └── Dockerfile
│
└── tests/
    └── test_normalization.py
```

**Explanation of Key Design Choices**

#### data/raw/

-   Never modified.

-   If altered, re-download.

-   Ensures traceability.

#### notebooks/

-   Exploration only.

-   Can be messy.

-   Never used as the production engine.

-   Once stable → logic migrated to `src/`.

#### src/

This is your intellectual property.

All reusable logic lives here.

Notebooks may import:

```         
from src.normalization import tpm_normalization
```

This prevents duplicated code.

#### scripts/

Thin wrappers like:

```         
python scripts/run_analysis.py --config config/config.yaml
```

No analytical logic here — only orchestration.

#### results/

Structured outputs:

-   QC reports

-   Model outputs

-   Publication-ready figures

-   Final tables\

Never mix temporary and final outputs.

#### tests/

Even minimal testing improves reliability:

-   Does normalization return expected shape?

-   Does model fail gracefully with wrong input?

-   Are missing values handled?

------------------------------------------------------------------------

## 3.3 Documentation

Minimum standard:

-   A clear `README.md`

-   Description of:

    -   Input data

    -   Expected output

    -   How to run the analysis

    -   Dependencies

For production tools:

-   Docstrings

-   Usage examples

-   Parameter explanation

------------------------------------------------------------------------

# 4. Data Analysis Best Practices

## 4.1 Understand the Data Before Modeling

Always check:

-   Missing values

-   Batch effects

-   Outliers

-   Distribution shapes

-   Library size variation (RNAseq)

-   Coverage variation (NGS)

Never apply a method blindly.

------------------------------------------------------------------------

## 4.2 Separate Exploration from Production

Exploratory notebooks:

-   Allowed to be messy.

-   Used to test ideas.

Production analysis:

-   Clean scripts

-   Version controlled

-   Parameterized

-   Re-runnable

------------------------------------------------------------------------

## 4.3 Avoid Hard-Coding

❌ Bad:

```         
if sample == "sample_23":
```

✅ Good:

-   Use configuration files (`.yaml`, `.json`)

-   Define parameters centrally

------------------------------------------------------------------------

# 5. Statistical and Scientific Rigor

-   Validate assumptions of statistical models.

-   Do not report p-values without effect sizes.

-   Correct for multiple testing.

-   Document all filtering and normalization steps.

-   Is there any prior knowledge supporting the results? Is this biologically possible?

------------------------------------------------------------------------

# 6. Logging and Error Handling

For pipelines:

-   Log every major step.

-   Capture software versions.

-   Save intermediate outputs where appropriate.

-   Fail loudly — do not silently continue.

------------------------------------------------------------------------

# 7. Testing and Validation

At minimum:

-   Test scripts on small datasets.

-   Validate results on:

    -   Known controls

    -   Published benchmark datasets

For reusable tools:

-   Unit tests (pytest / testthat)

-   Integration tests for workflows

------------------------------------------------------------------------

# 8. Collaboration Best Practices

## 8.1 With Wet-Lab Scientists

-   Clarify biological question early.

-   Define:

    -   What is the hypothesis?

    -   What is the provided input?

    -   What is the expected output?

    -   What decisions depend on this analysis? (timeline?)

Avoid:

-   “Just analyze everything.”

------------------------------------------------------------------------

## 8.2 Code Review Culture

Encourage:

-   Peer review of code

-   Pull requests

-   Constructive feedback

This improves:

-   Quality

-   Knowledge sharing

-   Team robustness

-   Cross speciality

------------------------------------------------------------------------

# 9. Data Governance & Ethics

Always consider:

-   Patient privacy (patient consent)

-   GDPR compliance

-   De-identification

-   Secure storage, data residency

-   Access control

Never:

-   Share raw patient data casually.

-   Upload sensitive data to uncontrolled platforms.

------------------------------------------------------------------------

# 10. Documentation of Decisions

In addition to code:

Document:

-   Why method X was chosen over Y

-   Parameter choices

-   Filtering thresholds

-   Limitations

-   

Future you (or your successor) will thank you.

------------------------------------------------------------------------

# 11. Common Mistakes to Avoid

-   

-   Copy-paste coding without understanding

-   

-   Not tracking versions

-   

-   Overfitting models

-   

-   Ignoring batch effects

-   

-   Running analyses only once

-   

-   Publishing plots without reproducibility

-   

------------------------------------------------------------------------

# 12. Professional Development

Encourage juniors to:

-   Learn basic software engineering principles

-   Practice clean coding

-   Learn versioning git

-   Learn workflow systems

-   Learn containerization/environment management

-   Study statistics deeply

Bioinformatics is increasingly engineering-driven.

------------------------------------------------------------------------

# 13. Gold Standard Checklist Before Delivering Results

Before sending results to collaborators, ask:

-   Can I rerun this from scratch?

-   Are all parameters documented?

-   Are plots publication-quality?

-   Are assumptions validated?

-   Are versions recorded?

-   Is the biological interpretation cautious and justified?
