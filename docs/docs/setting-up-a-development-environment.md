# Setting up a development environment

This tutorial outlines how you can get up and running managing your Python development environments.

## Installation

We recommend that that you install and configure the following to get started:

* Miniconda
* Git/GitHub
* Visual Studio Code

Once you have set up your development environment you can move on to [Starting a new project](starting-a-new-project.md).

## Miniconda
This is a setup step that you only need to do once per machine. After this is done, you shouldn't need to do this step again. Occasionally it may be necessary to update your requirements.

### Installing Miniconda

1. [Install Miniconda](https://docs.anaconda.com/free/miniconda/miniconda-install/): if you don't already have Miniconda, you'll need to install it following the instructions for your platform (MacOS/Windows/Linux)
2. Open a terminal window
3. To verify that conda is installed, in your terminal window, run:
```bash
conda --version
```
    Conda responds with the version number that you have installed, such as `conda 24.1.2`.

    If you get an error message, check the [Anaconda website](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-conda.html) for advice on suggestions on how to resolve.

### Configuring Miniconda

Set your channel priority to strict by entering in the terminal:
```bash
conda config --set channel_priority strict
```
Then prevent the base Conda environment from automatically activating when you open a terminal window:
```bash
conda config --set auto_activate_base false
```

### Creating a base prtdata environment

!!! note
    This section is intended to provide a simple step-by-step guide to creating your development environment. If you want to find out more about managing Conda environments, visit the [Conda docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html).

Create your base prtdata environment with the following requirements:
```bash
conda create -n prtdata python=3 cookiecutter make
```
You've now created a new conda environment named `prtdata` that you'll use to create all PRT cookiecutter projects. Once this environment has been created, you won't need to create it again.

You can now activate your new environment using the following command:
```bash
conda activate prtdata
```
By default, the active environment---the one you are currently using---is shown in parentheses ( ) or brackets [ ] at the beginning of your command prompt:
```bash
(prtdata) $
```
To deactivate your environment enter:
```bash
conda deactivate prtdata
```

## Git and GitHub

Building projects is one of the core parts of being a developer. And Git and GitHub are essential tools you'll use when building projects with others.

Having a way to document or track your code helps to make your work organised, and lets you keep track of the changes you've made at different stages. This is what [Git](https://git-scm.com/) lets you do.

But what if you're working with other developers or if you work in different locations with different computers, such as at work or at home? This is where [GitHub](https://github.com/) comes in.

GitHub provides you with a place to host your code. This makes controlling each version of your project easier and faster, and enables developers to collaborate.

**When you're using GitHub, you're working with Git beneath the hood.**

### Installing Git
Git generally comes pre-installed on MacOS and Linux-based systems, but you can always check if you have Git installed in your machine by typing `git version` in your terminal.

Similar to when you checked your Conda installation above, you should receive a response, such as `git version 2.28.0`. If you don't have Git installed in your computer, you won't get a version.

1. [Install Git](https://git-scm.com/download): if you don't already have Git, you'll need to install it following the instructions for your platform (MacOS/Windows/Linux)
2. Open terminal and type `git version` to verify that Git was successfully installed.

### Configuring Git
1. Set your Git username
```bash
git config --global user.name "Mona Lisa"
```
2. Set your Git email address
```bash
git config --global user.email "YOUR_EMAIL"
```
3. Confirm that you have set these correctly in Git:
```bash
git config --global user.name
> Mona Lisa
git config --global user.email
> YOUR_EMAIL
```

### GitHub

1. [Create a GitHub account](https://github.com/) and follow the prompts.
2. [Verify your email address](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/verifying-your-email-address). You should receive an email to the address you signed up with at GitHub.
3. Check your GitHub account is working by logging on and taking a look around.

!!! tip
    Git and GitHub can seem a bit intimidating at first, but remember it's just a way of tracking changes and providing effective version control. Check out [XXXXXX] for a separate guide on our preferred GitHub workflow, as well as the extensive docs from both [Git](https://git-scm.com/doc) and [GitHub](https://docs.github.com/en).

## Visual Studio Code
[Visual Studio Code](https://code.visualstudio.com/) aka VS Code is a free and open source integrated development environment (IDE) from Microsoft that is available on all major operating systems.

Just like Python itself, VS Code can be extended with packages, and it is those packages, called extensions in this case, that make it so useful. As well as Python, VS Code supports a ton of other languages.

There are other IDEs available, but VS Code brings a lot of features together in one app, including Jupyter Notebooks, Git version control, code linting, debugging, and much more. Use it, then try [Spyder](https://www.spyder-ide.org/), you'll thank us later.

### Installing VS Code
No need to dwell on this one. Go to the [VS Code website](https://code.visualstudio.com/) and follow the instructions.

### Extensions in VS Code
Once you have VS Code installed and opened, navigate to the ‘extensions’ tab on the left hand side vertical bar of icons (it’s the one that looks like 4 boxes). You’ll need to install the Python extension, which you can search for by using the text box within VS Code’s extensions panel.

There are some other extensions it’s useful to have and install (if they aren’t already):

| Extension | Function |
|---|---|
| Jupyter | Adds Jupyter notebook support |
| Pylance | Adds Python IntelliSense type checking |
| indent-rainbow | Makes code indentation easier to read |
| GitHub Repositories | Remotely browse and edit any GitHub repository |
| Path Intellisense | Adds filename autocompletion |
| Black Formatter | Adds formatting support for Python files using the [ Black ]( https://black.readthedocs.io/en/stable/index.html ) formatter. |
| Rainbow CSV | Rainbow CSV - Highlights columns in comma (.csv) files and more |
| YAML | Adds comprehensive YAML Language support (useful for environment.yml files) |
| vscode-icons | Adds icons to VS code file explorer, making it easier to find the file you want |
| Shebang Snippets | Insert "shebang" lines automatically |

### Hello world!

Whilst a full tutorial on how to use VS Code is outside of the scope of this guide, VS Code's [Getting Started tutorial](https://code.visualstudio.com/docs/python/python-tutorial) is a good place to learn more.

!!! warning
    As you have already installed Miniconda, you can ignore the first steps on installing a Python interpreter. There's also no need to create a virtual environment, as you've already created your `prtdata` conda environment. Open the Command Palette (⇧⌘P), start typing the **Python: Select Interpreter** command and select the `(prtdata)` environment from the list.

## You're ready

If you've made it this far then congratulations! You are now ready to start your journey as a developer and move on to the next stage — [Starting a new project](starting-a-new-project.md)