# How to contribute to Github project

You may make changes in main branch and push right away but this is not recommended and should be avoided when you are working with other people.

You may also create a new branch in the repo and make changes there and create the pull request of that branch. This is a good practice to do but may have to configure some privilege issue in the Github repo for pushing branches to remote.

Finally, we can fork the repository, and create pull request of changes made in that forked repository. This is highly recommended practice for collaboration.

Note that we are using `main` branch as primary branch. Some may use `master`, `develop`, etc. instead.

## Fork

1. Goto Github repository you want to work on and Fork the repo by clicking on the `Fork` button. Now you should have the new forked repository under your account.
1. Clone the **forked repository** into your local machine.

    ```git
    # Clone the forked repository into your local machine
    git clone ≪Forked Repository≫
    ```

    * You can run `git remote -v` to check remote repositories for current repository. The `origin` should be reserved for currently **forked repository**.
1. Setup the upstream for the forked repository.

    ```git
    # register upstream repository
    # git remote add ≪alias≫ ≪Upstream Repository≫
    git remote add upstream ≪Upstream Repository≫
    ```

    * The `≪alias≫` is typically named "upstream".

## Creating a new working branch

1. Before creating a new working branch in the forked repository, you should update the **main** branch up to date. You can do this by running the following:

    ```git
    # Move to main branch
    git checkout main

    # Fetch changes from upstream
    git fetch upstream

    # Pull updates from upstream repository
    # git pull --rebase ≪Upstream remote≫ main
    git pull --rebase upstream main

    # Push the changes from upstream repository to our forked repository
    # git push ≪Forked remote≫ main
    git push origin main
    ```

1. Then, you may create a new working branch

    ```git
    # Create a new working branch and checkout to it
    git checkout -b ≪Name of the Working Branch≫
    ```

    * You can check the branches on **local machine** using `git branch`
    * You can check all branches on both **local** and **remote** machine using `git branch -a`
    * If you want to remove some branch from the **local machine**, use `git branch -d ≪Branch name≫`
    * If you want to force-delete some branch from the **local machine**, use `git branch -D ≪Branch name≫`
    * If you want to remove some branch from the **remote repository**, use `git push ≪Remote≫ --delete ≪Branch name≫`
    * If you removed some branch from the **remote repository** and want to update that fact to local machine, use `git fetch --prune`. You still have to run `git branch -D ≪Branch name≫` to remove the branch completely from the local machine too.

## Submitting code from the working branch

1. After writing code from the working branch, add the files with changes

    ```git
    # Add changed files to git watch list
    # git add ≪File names≫
    git add *
    ```

    * `*` implies all files that has been changed, this excludes the files that are enlisted in `.gitignore` file

1. Commit the work

    ```git
    # Commit changes
    git commit
    ```

    * You will be seeing some file editor after `git commit`, write some commit messages and "save & exit" the file editor to finish the commit. If you "discard changes & quit", the commit will be discarded.
        * If you use `vim` editor, `:wq` to "save & exit", or use `:q!` to "discard changes & quit".
    * You can also use `git commit -m ≪Commit message≫` to write simple commit message. (Only recommended for small changes)

1. Push all local commits to remote repository

    ```git
    # Push to remote repository
    # git push ≪Forked Repository≫ ≪Name of Working Branch≫
    git push origin ≪Name of Working Branch≫
    ```

## Update the codebase while working on the working branch

Sometimes, you may want to update the codebase while working on the working branch, then you can do the following steps

```git
# Move to working branch
git checkout ≪Name of Working Branch≫

# Fetch changes from upstream
git fetch upstream

# Pull updates from upstream repository
# git pull --rebase ≪Upstream remote≫ main
git pull --rebase upstream main

# Push the changes from upstream repository to our forked repository
# git push ≪Forked remote≫ ≪Name of Working Branch≫
git push origin ≪Name of Working Branch≫
```

## Creating Pull Request

Goto the forked repository and select your working branch and press `Open pull request` button you may see from `Contribute` dropdown.

Ensure that your **Working branch of Forked Repository** is getting merged into **Primary branch of Upstream Repository**.

Use appropriate title for the pull request, describe about the issue and leave the log of what this pull request is about.

Then press `Create pull request` button.

## Synchronizing repository after pull request get merged

After your pull request has been merged, you have to update your forked repository to apply the changes to made.

```git
# Move to main branch
git checkout main

# Fetch changes from upstream
git fetch upstream

# Pull updates from upstream repository
# git pull --rebase ≪Upstream remote≫ main
git pull --rebase upstream main

# Push the changes from upstream repository to our forked repository
# git push ≪Forked remote≫ main
git push origin main

# Remove local working branch
git branch -D ≪Name of Working Branch≫
```

Then you may delete working branch from Github website fetch with prune option to update your local repository too.

```git
# fetch the fact that you deleted the working branch
git fetch --prune
```

Or if you want to delete the working branch in remote repository from local, run the following command

```git
# remove the working branch from forked repository
git push origin --delete ≪Name of Working Branch≫
```

## Example

Here is an example of work flow that you will be using.

Assume that your upstream repository use **master** branch as primary branch (as well as your forked repository) and you will be working on a branch named **some-issue**.

1. Fork the repository

    ```git
    git clone ≪Forked Repository≫
    ```

1. Setup the upstream for the forked repository.

    ```git
    git remote add upstream ≪Upstream Repository≫
    ```

1. Create your working branch

    ```git
    git checkout -b some-issue
    ```

1. Update your codebase from upstream

    ```git
    git checkout some-issue
    git fetch upstream
    git pull --rebase upstream master
    # Fix any conflicts
    git push origin some-issue
    ```

1. Make any changes to working branch and commit

    ```git
    git add *
    git commit -m "Some commit message"
    git push origin some-issue
    ```

    and create Pull Request if you haven't already, from your **forked some-issue** branch to **upstream master** branch.

1. Repeat from step 4 if you had not updated your codebase **today**.

    If you already have updated your codebase, repeat from 5 until you are completely ready.

1. After Your pull request has been approved and merged, delete the working branch and update your forked repository's master branch

    ```git
    git checkout master
    git fetch upstream
    git pull --rebase upstream master
    git push origin master
    git branch -D some-issue
    git push origin --delete some-issue
    ```

1. Repeat from step 3 if you get assigned to another issue
