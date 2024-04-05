# Starting a new project
So you've already [set up your prtdata development environment](setting-up-a-development-environment.md) and now you're ready to get coding!

## Create your project/repo
The best time to use the prt cookiecutter template is right at the start, when you first create your project/repo. We will assume that you are starting your project from scratch.

!!! warning
    We recommend using prtdata to create every project you work with so that there is at least a 1:1 ratio between your conda environments and your projects. There are many issues with having more than one repo using the same conda environment, so whatever you do **please don't use a monolithic environment to rule them all**. For more on this idea see Tip #2 of [this talk on building reproducible workflows](https://youtu.be/cCzkL9DhWEE?t=365). 

### Create a project using a PRT cookiecutter template

1. Open a terminal window
1. Activate the `prtdata` environment you created earlier: `conda activate prtdata`
1. Navigate to the location that you'd like your project to located (without creating the project directory, that happens automagically in the next step). For example, if you want my project to be located in `/home/<my-repo-name>` navigate to `/home` in this step.
1. Create your project. Run `cookiecutter https://github.com/Prison-Reform-Trust/prt-cookiecutter-data-science` and fill in the prompts. Note that the repo name that you enter will be the name of the directory that your project lives in.

We've now created a project filled with the PRT cookiecutter template files in `<my-repo-name>`. 

### Initialize the project as a GitHub repo
As we have [previously explained](setting-up-a-development-environment.md#git-and-github) we'd like to use git to keep track of changes that are made to our project. Now is the best time to initialize the git repo and create the GitHub connection.

1. Load VS Code and open your project folder
2. Click the 'Source Control' tab (:octicons-git-branch-24:) on the left hand side vertical bar of icons (it looks like three circle joined with lines)
3. You should see two options - to Initialize Repository or Publish to GitHub.
4. Initialize Repository - this will create the necessary Git repository metadata files and show your workspace files as untracked changes ready to be staged. 
5. Publish to GitHub - this will directly publish your workspace folder to a GitHub repository, allowing you to choose between private and public repositories. You will probably be prompted to authenticate your GitHub account at this stage.

!!! tip
    This is just a starting point for using Git and GitHub, there is lots more to explore. We strongly recommend visiting the [GitHub and Visual Studio Code getting started tutorials](https://vscode.github.com/) to get the most out of this powerful integration.


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

So you've now created your PRT cookiecutter project and initialised it as a GitHub repo. The next step is to build your development environment. 

1. Open a terminal window in VS Code (Terminal > New Terminal)
2. Check that the terminal prompt is showing your project's directory 
```bash
<my-repo-name> $ 
```
3. Activate `prtdata`
```bash
conda activate prtdata
(prtdata)<my-repo-name> $ 
```
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
Whilst the vast majority of your development will take place using VS Code, if this is bothering you, then run the following command and a shortened version will be set:

```bash
conda config --set env_prompt '({name})'
(envs) $
```
Let the coding begin!

## Exploring the default environment
The prt template project `<my-repo-name>` is populated with recommended default settings. Defaults that we've developed over time that work as a nice base for most folks who are creating a data science related project. It's a great place to start, and until you're familiar with how and why these defaults work in most cases, we don't recommend messing with them.

### Using your conda environment in a Jupyter notebook
1. In VS Code press ++cmd+shift+p++
2. Type 'Jupyter' in the menu and select 'Create: New Jupyter notebook'
3. Save the new notebook as `prtdata-test.ipynb` in the 'notebooks' folder of your project
4. Select the `envs` environment from within the notebook: Click **Select Kernel > Python Environments > envs (Python 3.XX) `<my-repo-name>`**`/envs/bin/python`. 
5. Check that it's finding the right environment by entering  `conda list` in a cell and running the cell. The output should include this at the top:
```bash
# packages in environment at <path-to-environment>: 

...
```
    where the `<path-to-environment>` ends in `<my-repo-name>/envs`. 

### Exploring what makes up your environment
To see what's in your Conda environment, open up the `environment.yml` file. In it is a list of the packages that are installed in your project's virtual Conda environment.

You might notice that the output that was returned when you ran `conda list` in your Jupyter Notebook was quite a bit longer than the number of packages listed in the `environment.yml`. That's because there were other dependencies that had to be installed to make the packages in `environment.yml` run.

**[Need to include a reference to lockfiles here once implemented]**

We like to think of these two files are representing two different perspectives:

* **`environment.yml`**: The packages that you **want**. This file is manually maintained.
* **`environment.<your-architecture>.lock.yml`**: The packages that you **need** (to run what you want). This file is autogenerated and updated.