# Starting a new project
So you've already [set up your prtdata development environment](setting-up-a-development-environment.md) and now you're ready to get coding!

## Create your project/repo
The best time to use the prt cookiecutter template is right at the start, when you first create your project/repo. We will assume that you are starting your project from scratch.

!!! warning
    We recommend using prtdata to create every project you work with so that there is at least a 1:1 ratio between your conda environments and your projects. There are many issues with having more than one repo using the same conda environment, so whatever you do **please don't use a monolithic environment to rule them all**. For more on this idea see Tip #2 of [this talk on building reproducible workflows](https://youtu.be/cCzkL9DhWEE?t=365). 

### Create a project using a PRT cookiecutter template

1. Open a terminal window
1. Activate the `prtdata` environment you created earlier: `conda activate prtdata`
1. Navigate to the location that you'd like your project to located (without creating the project directory, that happens automagically in the next step). For example, if I want my project to be located in `/home/<my-repo-name>` I would navigate to `/home` in this step.
1. Create your project. Run `cookiecutter https://github.com/Prison-Reform-Trust/prt-cookiecutter-data-science` and fill in the prompts. Note that the repo name that you enter will be the name of the directory that your project lives in.

We've now created a project filled with the PRT cookiecutter template files in `<my-repo-name>`. 

### Initialize the project as a GitHub repo



### Building your project environment

As we have already set out above, there is a very strong case against having a single monolithic development environment from which you build all of your projects. Whilst no package manager (read Conda) is perfect, there are features that you can make use of to try and avoid what's known as [dependency hell](https://en.wikipedia.org/wiki/Dependency_hell).

#### environment.yml

One such way that Conda attempts to mitigate against the dreaded:
```bash
> Solving environment: failed 
```
is through the use of `environment.yml` files. These are a simple text file which contains a list of the names of the packages that you want to include in your development environment (dependencies), and may also include the chosen name of that environment and the channels to use to download the dependencies/packages. 

We're not going to get into much more detail on `environment.yml` files, but there's a short primer in [Conda's docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#create-env-file-manually) if you want to find out more..

#### How to build your environment

!!! warning
    If you have not already completed the preceding steps then return to [Create your project/repo](#create-your-projectrepo) and follow the steps back to here.

1. Open a terminal window
2. Navigate to your project's directory
3. Activate `prtdata` 
4. Build your project environment by entering the following command:

```bash
conda env create --prefix ./envs -f environment.yml
```

This command reads the `environment.yml` file within your project directory and builds a new development environment called `./envs` within that directory. As Conda sets out in their docs:

!!! quote "[Specifying a location for an environment](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#specifying-a-location-for-an-environment)"
    Specifying a path to a subdirectory of your project directory when creating an environment has the following benefits:

    * It makes it easy to tell if your project uses an isolated environment by including the environment as a subdirectory.
    * It makes your project more self-contained as everything, including the required software, is contained in a single project directory.

Once all of the packages have been downloaded and your environment has been created it's time to activate your environment. 

```bash
conda activate ./envs
```
By doing this you avoid the cognitive load of having to think of a new name for your development environment every time you start a new project. As long as you navigate to your project folder and activate `./envs` you know you'll be working in that project's dedicated environment.

One small downside is that the full filepath to the environment might take up a lot of visible space in your terminal prompt. For example:

```bash
(/Users/USER_NAME/research/data-science/PROJECT_NAME/envs) $
```
If this is bothering you, then run the following command and a shortened version can be set:

```bash
conda config --set env_prompt '({name})'
```
Let the coding begin!