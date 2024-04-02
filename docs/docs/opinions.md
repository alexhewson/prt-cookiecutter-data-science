# Opinions

The default project structure reflects certain opinions about how to do collaborative data science work. These opinions grew out of our own experiences with what works and what doesn't. Some of these opinions are about workflows, and others are about tools that can make the process easier. These opinions are discussed below.

## Data analysis is a directed acyclic graph

> Don't _ever_ edit your raw data, especially not manually, and _especially_ not in Excel.

The most important features of a quality data analysis are **correctness** and **reproducibility**—anyone should be able to re-run your analysis using only your code and raw data and produce the same final products. The best way to ensure correctness is to test your analysis code. **The best way to ensure reproducibility is to treat your data analysis pipeline as a directed acyclic graph ([DAG](https://en.wikipedia.org/wiki/Directed_acyclic_graph))**. This means each step of your analysis is a node in a directed graph with no loops. You can run through the graph forwards to recreate any analysis output, or you can trace backwards from an output to examine the combination of code and data that created it.

### Raw data is immutable

That proper data analysis is a DAG means that **raw data must be treated as immutable**—it's okay to read and copy raw data to manipulate it into new outputs, but never okay to change it in place. This informs the design of the default `data/` directory subfolders in which data originates from `raw/`, intermediate analytical outputs get serialized or cached in `interim/`, and final products end up in `processed/` (the number or names of these folders is less important than flow of data between them). 

Some **do**s and **don't**s that follow from treating data analysis as a DAG:

* ✅ **Do** write code that moves the raw data through a pipeline to your final analysis.
* ✅ **Do** serialize or cache the intermediate outputs of long-running steps.
* ✅ **Do** make it possible (and ideally, documented and automated) for anyone to reproduce your final data products with only the code in `{{ cookiecutter.module_name }}` and the data in `data/raw/`.

* ⛔ **Don't** _ever_ edit your raw data, especially not manually, and _especially_ not in Excel. This includes changing file formats or fixing errors that might break a tool that's trying to read your data file.
* ⛔ **Don't** overwrite your raw data with a newly processed or cleaned version.
* ⛔ **Don't** save multiple versions of the raw data. 

### Data should (mostly) not be kept in source control

Another consequence of treating data as immutable is that data doesn't need source control in the same way that code does. Therefore, **by default, the `data/` folder is included in the `.gitignore` file.** If you have a small amount of data that rarely changes, you _may_ want to include the data in the repository. GitHub [currently](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github#file-size-limits) warns you if files are over 50MB and rejects any files over 100MB. 

If you have larger amounts of data, consider storing and syncing with a cloud service like [Amazon S3](https://aws.amazon.com/s3/), [Azure Blob Storage](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-overview), or [Google Cloud Storage](https://cloud.google.com/storage/docs/introduction).

## Notebooks are for exploration and communication, source files are for repetition

> Source code is superior for replicability because it is more portable, can be tested more easily, and is easier to code review.

[Jupyter Notebook](https://jupyter.org/) and other literate programming tools are very effective for exploratory data analysis because they enable rapid iteration and visualization of results. However, these tools can be less effective for reproducing an analysis. Source code is superior for replicability because it is more portable, can be tested more easily, and is easier to code review. 

When we use notebooks in our work, we often subdivide the `notebooks/` folder to keep things organized and legible. For example, `notebooks/exploratory/` contains initial explorations, whereas `notebooks/reports/` is more polished work that can be exported as html to the `reports/` directory. We also recommend that you follow a naming convention that shows the owner and the order the analysis was done in. We use the format `<step>-<ghuser>-<description>.ipynb` (e.g., `0.3-bull-visualize-distributions.ipynb`). Since notebooks are challenging objects for source control (e.g., diffs of the `json` are often not human-readable and merging is near impossible), we recommended not collaborating directly with others on Jupyter notebooks. We also recommend using a tool like [`nbautoexport`](https://github.com/drivendataorg/nbautoexport) to make reviewing changes to notebooks easier. 

### Refactor the good parts into source code 

Don't write code to do the same task in multiple notebooks. If it's a data preprocessing task, put it in the pipeline at `{{ cookiecutter.module_name }}/data/make_dataset.py` and load data from `data/interim/`. If it's useful utility code, refactor it to `{{ cookiecutter.module_name }}`. Classic signs that you are ready to move from a notebook to source code include duplicating old notebooks to start new ones, copy/pasting functions between notebooks, and creating object-oriented classes within notebooks.

We make it easy to refactor notebook code because this template makes your project a Python package by default and installs it locally in the requirements file of your chosen environment manager. This enables you to import your project's source code and use it in notebooks with a cell like the following:

```python
# OPTIONAL: Load the "autoreload" extension so that code can change
%load_ext autoreload

# OPTIONAL: always reload modules so that as you change code in {{ cookiecutter.module_name }}, it gets loaded
%autoreload 2

from {{ cookiecutter.module_name }}.data import make_dataset
```

## Build from the environment up

The first step in reproducing an analysis is always replicating the computational environment it was run in. You need the same tools, the same libraries, and the same versions to make everything play nicely together.

Doing so in Python requires choosing and configuring an environment management tool. The ecosystem for this tooling has evolved a lot in recent years. 

For data science work, we prefer to use the **conda** package manager because it also manages non-Python packages, including system library dependencies that you often run into in data science. Our recommended way to install conda is with [Miniconda](https://docs.anaconda.com/free/miniconda/). 

## Keep secrets and configuration out of version control

You _really_ don't want to leak your Plotly secret key or Microsoft 365 username and password on Github—see the [Twelve Factor App](https://12factor.net/config) principles on this point. Here's one way to do this:

### Store your secrets and config variables in a special file

Create a `.env` file in the project root folder. Thanks to the `.gitignore`, this file should never get committed into the version control repository. Here's an example:

```nohighlight
# example .env file
DATABASE_URL=postgres://username:password@localhost:5432/dbname
AWS_ACCESS_KEY=myaccesskey
AWS_SECRET_ACCESS_KEY=mysecretkey
OTHER_VARIABLE=something
```

### Use a package to load these variables automatically.

If you look at the stub script in `{{ cookiecutter.module_name }}/data/make_dataset.py`, it uses a package called [python-dotenv](https://github.com/theskumar/python-dotenv) to load up all the entries in this file as environment variables so they are accessible with `os.environ.get`. Here's an example snippet adapted from the `python-dotenv` documentation:

```python
# {{ cookiecutter.module_name }}/data/dotenv_example.py
import os
from dotenv import load_dotenv, find_dotenv

# find .env automagically by walking up directories until it's found
dotenv_path = find_dotenv()

# load up the entries as environment variables
load_dotenv(dotenv_path)

database_url = os.environ.get("DATABASE_URL")
other_variable = os.environ.get("OTHER_VARIABLE")
```

## Encourage adaptation from a consistent default

To keep this structure broadly applicable for many different kinds of projects, we think the best approach is to be liberal in changing the folders around for _your_ project, but be conservative in modifying the default cookiecutter structure for _all_ projects.

### Examples of template adaptation and evolution

A project's organizational needs may differ from the start and can change over time. Here are some examples of directions to go in evolving your project structure. 

#### Example 1: Simplifying

Some projects don't require multiple sub-directories to organize their module code. When a few python files can effectively accomplish all that is required, flattening folders into files can make things easier to track and maintain. You can see an example of this in our [cyfi package](https://github.com/drivendataorg/cyfi/tree/main/cyfi). If it's in the template but you don't need it, delete it!

#### Example 2: Expanding

By contrast, we've added more folders to organize module code on more complex projects. A good example of this is our [zamba package](https://github.com/drivendataorg/zamba/tree/master/zamba) for which we've introduced new folders to handle task-specific portions of the codebase.

#### Example 3: Re-organizing

On long-running projects, the `notebooks` folder can get congested. One adaptation we've employed is to add a top-level `research/` folder (and a corresponding `data/research` data folder) that contains sub-folders for individual experiments. These sub-folders can contain their own notebooks, code, and even their own Makefiles that inherit from the parent project `Makefile`.