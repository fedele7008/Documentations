# How to contribute to Github project

There are various ways to contribute to Github projects.

* You may clone the repository, make changes, and push directly to the main branch.

    But if you are working with other people, this is not recommended and should be avoided.

* You may clone the repository, also create a new branch, and make changes in your working branch. Finally, create the pull request of your branch.

    This is a good practice to follow but may have to configure some privilege issue in the Github repo for pushing branches to remote. (Especially if you are contributing to some open source project).

* Finally, we can fork and clone the repository, create new working branch, and create pull request. This is highly recommended practice for collaboration. (In open source project, this is must)

Note that the naming of primary branch may vary depending on the project.
The traditional naming convention was `master` however, people tends to use `main` instead as the "master" resembles the slavery.

Some may use completely different naming conventions like `develop`, `core`, etc.

In this documentation, we are going to learn the third approach using fork.

## Fork

1. Goto Github repository you want to work on and Fork the repo by clicking on the `Fork` button. Now you should have the new forked repository under your account.

    ![git-fork.png](../assets/git/img/git-fork.png)

1. Clone the **forked repository** into your local machine.

    ```git
    git clone ≪Forked Repository≫
    ```

    * You can run `git remote -v` to check remote repositories for current repository.

        The `origin` should be reserved for currently **forked repository**.

1. Setup the upstream for the forked repository.

    ```git
    # git remote add ≪alias≫ ≪Upstream Repository≫
    ```

    * The `≪alias≫` is typically named "upstream". We will use `upstream` as our upstream repository alias in this document.

## Creating a new working branch

1. Goto the root folder where you cloned the **forked repository** in your terminal.

1. Check out to primary branch that you are going to start from.

    ```git
    git checkout ≪Primary Branch≫
    ```

1. Fetch any updates from upstream repository.

    ```git
    git fetch upstream
    ```

1. Rebase primary branch up-to-date.

    ```git
    git rebase upstream/≪Primary Branch≫
    ```

1. Push the up-to-date branch to remote repository.

    ```git
    git push origin ≪Primary Branch≫
    ```

1. Create a new working branch

    ```git
    git checkout -b ≪Working Branch≫
    ```

* You can check the branches on **local machine** using `git branch`
* You can check all branches on both **local** and **remote** machine using `git branch -a`
* If you want to remove some branch from the **local machine**, use `git branch -d ≪Branch Name≫`
* If you want to force-delete some branch from the **local machine**, use `git branch -D ≪Branch Name≫`
* If you want to remove some branch from the **remote repository**, use `git push ≪Remote≫ --delete ≪Branch Name≫`
* If you removed some branch from the **remote repository** and want to update that fact to local machine, use `git fetch --prune`. 

    You still have to run `git branch -D ≪Branch Name≫` to remove the branch completely from the local machine too.

## Submitting code from the working branch

1. After writing code on your working branch, add the files with changes to commit list.

    ```git
    git add ≪File names≫
    ```

    * `*` or `.` for the `≪File names≫` implies all files that has been changed will be added.

        This excludes the files that are enlisted in `.gitignore` file

1. Commit the work

    ```git
    git commit
    ```

    * You will be seeing some file editor after `git commit`, write some commit messages and **save & exit** the file editor to finish the commit. If you **discard changes & quit**, the commit will be discarded.
        * If you use `vim` editor, `:wq` to **save & exit**, or use `:q!` to **discard changes & quit**.

    * You can also use `git commit -m ≪Some commit message≫` to write simple commit message. (Only recommended for small changes)

1. Push all local commits to remote repository

    ```git
    git push origin ≪Working Branch≫
    ```

## Update the codebase while working on the working branch

Sometimes, you may want to update the codebase while working on the working branch.

1. Fetch changes from upstream repository

    ```git
    git fetch upstream
    ```

1. Goto primary branch

    ```git
    git checkout ≪Primary Branch≫
    ```

1. Rebase primary branch up-to-date.

    ```git
    git rebase upstream/≪Primary Branch≫
    ```

1. Push changes to remote repository

    ```git
    git push origin ≪Primary Branch≫
    ```

1. Goto working branch

    ```git
    git checkout ≪Working Branch≫
    ```

1. Rebase working branch up-to-date.

    ```git
    git rebase ≪Primary Branch≫
    ```

1. Pull updates from other contributors push on the working branch

    ```git
    git pull origin ≪Working Branch≫
    ```

1. Push the changes to remote repository

    ```git
    git push origin ≪Working Branch≫
    ```

## Creating Pull Request

1. Goto your forked repository from Github.

1. Select your **working branch** and click on **Contribute** button.

    ![git-pr-1.png](../assets/git/img/git-pr-1.png)

1. Click **Open pull request** button, describe about the issue and leave comments about your pull request.

1. Press **Create pull request** button.

## Synchronizing repository after pull request get merged

After your pull request has been merged, you have to update your forked repository to apply the changes to made.

1. Fetch changes from upstream repository

    ```git
    git fetch upstream
    ```

1. Goto primary branch

    ```git
    git checkout ≪Primary Branch≫
    ```

1. Rebase primary branch up-to-date.

    ```git
    git rebase upstream/≪Primary Branch≫
    ```

1. Push the changes to upstream repository

    ```git
    git push origin ≪Primary Branch≫
    ```

1. Remove local working branch

    ```git
    git branch -D ≪Working Branch≫
    ```

1. Remove the working branch from forked repository

    ```git
    git push origin --delete ≪Working Branch≫
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

1. Update codebase if your master branch is outdated

    ```git
    git fetch upstream
    git checkout master
    git rebase upstream/master
    git push origin master
    ```

1. Create your working branch

    ```git
    git checkout -b some-issue
    ```

1. Update your codebase from upstream (if necessary)

    ```git
    git fetch upstream
    git checkout master
    git rebase upstream/master
    git push origin master
    git checkout some-issue
    git rebase master
    git pull origin some-issue
    git push origin some-issue
    ```

1. Make any changes to working branch and commit

    ```git
    git add *
    git commit -m "≪Some commit message≫"
    git push origin some-issue
    ```

    and create Pull Request if you haven't already.

    Your pull request should be from your **forked some-issue** branch to **upstream master** branch.

1. Repeat from step **5** until your work is done.

    Updating code once a while is recommended.

1. After Your pull request has been approved and merged, delete the working branch and update your forked repository's master branch

    ```git
    git fetch upstream
    git checkout master
    git rebase upstream/master
    git push origin master
    git branch -D some-issue
    git push origin --delete some-issue
    ```

1. Repeat from step 3 if you get assigned to another issue
