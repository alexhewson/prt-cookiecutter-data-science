# Prison Reform Trust Cookiecutter Data Science

_A logical, reasonably standardized, but flexible project structure for doing and sharing data science work—adapted for Prison Reform Trust._


<!-- #### [Project homepage](http://drivendata.github.io/cookiecutter-data-science/) -->


### Requirements to use the cookiecutter template:
-----------
 - Python 3.5+
 - [Cookiecutter Python package](http://cookiecutter.readthedocs.org/en/latest/installation.html) >= 1.4.0: We recommend that this is installed with [Conda Python package management](https://docs.conda.io/projects/conda/en/latest/index.html):

``` bash
$ conda config --add channels conda-forge
$ conda install cookiecutter
```


### To start a new project, run:
------------

    cookiecutter https://github.com/Prison-Reform-Trust/prt-cookiecutter-data-science


<!-- [![asciicast](https://asciinema.org/a/244658.svg)](https://asciinema.org/a/244658) -->

### The resulting directory structure
------------

The directory structure of your new project looks like this: 

```
├── LICENSE
├── Makefile           <- Makefile with commands like `make create_environment`, 
│                         `make update_environment or `make data`.
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for analysis.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default Sphinx project for adding documentation to this project; 
│                         see sphinx-doc.org for details.
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `conda list --export > requirements.txt`
│
├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
└── src                <- Source code for use in this project.
    ├── __init__.py    <- Makes src a Python module
    │
    ├── data           <- Scripts to download or generate data
    │   └── make_dataset.py
    │
    ├── analysis        <- Scripts to process raw data for analysis
    │   └── process_data.py
    │
    └── visualization  <- Scripts to create exploratory and results oriented visualizations
        └── visualize.py
```

## Contributing

This project is currently in development and borrows heavily on the excellent work of DrivenData and their cookiecutter-data-science template. Which we have relied on for a considerable period. The development of this template is also indebted to Easydata and their [excellent cookiecutter template](https://github.com/hackalog/easydata) which inspired the development of the PRT project, and provided a deeper understanding of how to create reproducible environments; datasets and workflows for data analysis.

As such, this project is primarily focused on adapting the project to suit our own organisational needs and isn't actively seeking contributions from outside of the organisation.

If you would like to find out more about the DrivenData cookiecutter-data-science template and how to contribute to their project then [see their docs for guidelines](https://drivendata.github.io/cookiecutter-data-science/#contributing).

<!-- ### Installing development requirements
------------

    pip install -r requirements.txt

### Running the tests
------------

    py.test tests -->
