# Starting a new project
So you've already [set up your prtdata development environment](setting-up-a-development-environment.md) and now you're ready to get coding!

## Create your project/repo
The best time to use the prt cookiecutter template is right at the start, when you first create your project/repo. We will assume that you are starting your project from scratch.

!!! warning
    We recommend using prtdata to create every project you work with so that there is at least a 1:1 ratio between your conda environments and your projects. There are many issues with having more than one repo using the same conda environment, so whatever you do **please don't use a monolithic environment to rule them all**. For more on this idea see Tip #2 of [this talk on building reproducible workflows](https://youtu.be/cCzkL9DhWEE?t=365). 

### Create a project using a PRT cookiecutter template

1. Open a terminal window
1. Activate the `prtdata` environment created above: `conda activate prtdata`
1. Navigate to the location that you'd like your project to located (without creating the project directory, that happens automagically in the next step). For example, if I want my project to be located in `/home/<my-repo-name>` I would navigate to `/home` in this step.
1. Create your project. Run `cookiecutter https://github.com/Prison-Reform-Trust/prt-cookiecutter-data-science` and fill in the prompts. Note that the repo name that you enter will be the name of the directory that your project lives in.

We've now created a project filled with the PRT cookiecutter template files in `<my-repo-name>`. 

### Initialize the project as a GitHub repo