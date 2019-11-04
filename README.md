template
==============================

This template repository contains standardized folder structures and best practices for reproducibility. It is designed to be used as a template when creating a new repository.

The template pre-populates the following important items:

*  MIT License
*  Requirements.txt and setup.py for environment set-up
*  Tox.ini for automated unit tests -- which will be run for each commit by GitHub actions
*  Makefile
*  Folders to remind users to keep data, documentation, references, notebooks, and source files separate.
*  GitHub workflows to build and push Docker images, and to test the Python package installation for CI/CD
*  Automated actions to create a pull request fixing PEP8 Issues

Note:

*  As an Enterprise organization, WRI receives 50,000 free minutes of CI/CD time per month. The CI/CD for this template takes about 6/minutes of time per push.

Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── docs               <- A default Sphinx project; see sphinx-doc.org for details
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    ├──tests               <- Test scripts
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.testrun.org



Pre-commit hooks
------------

[Pre-commit hooks](https://pre-commit.com/) run basic code checks before every commit to identify simple issues before pushing code to Github.
Hooks included in this templace are

Code linting and formatting
- black 
- flake8
- mypy
- trailing-whitespace

Secret and password detection
- detect-aws-credentials
- detect-private-key
- detect-secrets

Once installed, pre-commit will execute automatically every time you run `git commit`. 
It will prevent you from committing your changes if any of the checks fail.

### Installation

Step 0: Create your git repo
```bash
git init
```

Step 1: Install Pre-commit
```bash
pip install pre-commit
```

Step 2a (optional):
```bash
pip install detect-secrets
```

Step 2b (optional): Create a base line

```bash
detect-secrets scan > .secrets.baseline
```

Step 3: Edit your .pre-commit-config.yaml. 
```.yaml
exclude: '^$'
fail_fast: false
repos:
-   repo: https://github.com/ambv/black
    rev: stable
    hooks:
    - id: black
      language_version: python3.6
-   repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v1.2.3
    hooks:
    - id: detect-aws-credentials
    - id: detect-private-key
    - id: trailing-whitespace
    - id: flake8
      args: ['--ignore=E203, E266, E501, W503, F403, F401']
-   repo: https://github.com/pre-commit/mirrors-mypy
    rev: v0.650
    hooks:
    -   id: mypy
-   repo: https://github.com/Yelp/detect-secrets
    rev: v0.13.0
    hooks:
    -   id: detect-secrets
        args: ['--baseline', '.secrets.baseline']
        exclude: .*/tests/.*
```

Step 4: Add pre-commit hooks to your repo
```bash
pre-commit install

```

Step 5: Run against all files at least once
```bash
pre-commit run --all

```


--------
<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>
