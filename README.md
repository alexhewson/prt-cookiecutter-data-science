# Prison Reform Trust Cookiecutter Data Science

_A logical, reasonably standardized, but flexible project structure for doing and sharing data science work—adapted for Prison Reform Trust._

## Getting started

### Setting up a development environment

Before starting your project, your computer needs to be able to interpret all of this code. We have created a separate section which sets out a step-by-step guide to help make this process as straightforward as possible, with information that we have found helpful along the way.

!!! tip
    If you've never created a Python environment before, or you need a refresher on how we approach this seemingly straightforward task, then this section should be your starting point.

[Setting up a development environment](setting-up-a-development-environment.md)

### Requirements to use the cookiecutter template
-----------
 - Python 3.5+
 - [Cookiecutter Python package](http://cookiecutter.readthedocs.org/en/latest/installation.html) >= 1.4.0: We recommend that this is installed with [Conda's Miniconda Python package management](https://docs.anaconda.com/free/miniconda/):

### Starting a new project

Starting a new project is as easy as running this command at the command line. No need to create a directory first, the cookiecutter will do it for you.

```nohighlight
cookiecutter https://github.com/Prison-Reform-Trust/prt-cookiecutter-data-science
```

### Example

Now that you've got your project, you're ready to go! You should do the following:

 - **Check out the [directory structure](#directory-structure)** below so you know what's in the project and how to use it.
 - **Read the [opinions](docs/docs/opinions.md)** that are baked into the project so you understand best practices and the philosophy behind the project structure.
 <!-- - **Read the [using the template](using-the-template.md) guide** to understand how to get started on a project that uses the template. -->


## Directory structure

```nohighlight
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
├── src                <- Source code for use in this project.
│   ├── __init__.py    <- Makes src a Python module
│   │
│   ├── analysis       <- Scripts to process raw data for analysis
│   │   └── process_data.py
│   │
│   ├── data           <- Scripts to download or generate data
│   │   └── make_dataset.py
│   │
│   └── visualization  <- Scripts to create exploratory and results oriented visualizations
│       └── visualize.py
│
└── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


## Contributing

This project is currently in development and borrows heavily on the excellent work of DrivenData and their cookiecutter-data-science template (CCDS). Which we have relied on for a considerable period. The development of this template is also indebted to EasyData and their [excellent cookiecutter template](https://github.com/hackalog/easydata) which inspired the development of the PRT project, and provided a deeper understanding of how to create reproducible environments; datasets and workflows for data analysis.

As such, this project is primarily focused on adapting the project to suit our own organisational needs and isn't actively seeking contributions from outside of the organisation.

If you would like to find out more about the DrivenData cookiecutter-data-science template and how to contribute to their project then [see their docs for guidelines](https://drivendata.github.io/cookiecutter-data-science/#contributing).


## Links to related projects and references

Here are some projects and blog posts that have provided a huge amount of information and guidance to inform this cookiecutter template and which you may find useful.

 - [Cookiecutter Data Science (CCDS)](https://drivendata.github.io/cookiecutter-data-science/) - The original template on which this is based.
 - [EasyData](https://github.com/hackalog/easydata/wiki) - A revised implementation of the CCDS template and which triggered the development of this project.
 - [Coding for Economists](https://aeturrell.github.io/coding-for-economists) - An excellent blog by [Arthur Turrell](https://aeturrell.com/) covering a wide range of topics, from getting your development environment started to suggested workflows; data transformation; designing reproducible analysis and much, much more.
 - [Government Analysis Function guidance aka The Duck Book](https://best-practice-and-impact.github.io/qa-of-code-guidance/intro.html) - Another great guidance doc to draw from, which govers guiding principles; modular coding; documentation; version control and loads more.

Finally, a huge thanks to the [Cookiecutter](https://cookiecutter.readthedocs.org/en/latest/) project ([github](https://github.com/audreyr/cookiecutter)), which is helping us all spend less time thinking about and writing boilerplate and more time getting things done.
