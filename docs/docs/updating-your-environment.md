# Updating your development environment

We've already created a development environment and now you realise that there's a package that you need or forgot to install—let's customize it.

## Always use the `environment.yml`!
!!! warning
    When adding packages to your python environment, **do not use `pip install` or `conda install` directly**. Always edit `environment.yml` and run `conda env update` instead. This will go a long way to avoiding the dreaded dependency hell.

Your `environment.yml` file will look something like this:
```yaml
channels:
  - defaults
  - conda-forge
dependencies:
  - notebook
  - cookiecutter
  - black
  - jupyterlab
  - lxml
  - matplotlib
  - odfpy
  - poppler
  - python-dotenv
  - seaborn
  - plotly
  - nbqa
  - pandas
  - python-kaleido
  - chart-studio
  - ipywidgets
  - plotly::plotly-geo
...
```
To add any package available from conda, add it to the end of the list and save.

Once you've made your edits, run `conda env update` in the terminal and voila, you're updated.

## Checking your updates back into the project repo
To share your updated environment, check in your `environment.yml` file so others can use it. We'll follow the [EasyData git workflow](https://github.com/hackalog/easydata/blob/master/%7B%7B%20cookiecutter.repo_name%20%7D%7D/reference/easydata/git-workflow.md)

1. Checkout a new branch: `git checkout -b update-environment`
1. Stage the changes: `git add -p environment.yml` and include the desired changes, discarding the rest
1. Commit the changes: `git commit -m "update the environment file"
1. Push to your origin: `git push origin update-environment`
1. [Create a pull request (PR) to the main branch](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)
1. Merge this PR: If you look at the PR, the only changes should be to the `environment.yml` file. If all looks well, merge this PR.
1. Incorporate changes back into your local setup: 
```bash
git checkout main
git fetch origin
git merge origin/main
```
The local `main` branch will now have the updated `environment.yml`. While it seems a bit roundabout here, we recommend always using GitHub PRs to keep track of changes. This allows for the adoption of a [multi-user workflow using an `upstream`](https://github.com/hackalog/easydata/wiki/GitHub-%28GitLab%29-Workflow-Cheat-Sheet) seamlessly. 