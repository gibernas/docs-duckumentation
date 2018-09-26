# (Experts) Compiling all books {#duckumentation-installing-docs-system status=ready}

This section describes how to compile all the books at the same time.

## Setup

### Fork the `duckuments` repo

In the following, we are going to assume that the documentation system is installed in `~/duckuments`. However, it can be installed anywhere.  You will need to add your public key to github following [these instructions](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/).

Fork the `duckietown/duckuments` repository in the `~/duckuments` directory:

```
$ git clone --depth 10 git@github.com:duckietown/duckuments ~/duckuments
$ cd ~/duckuments
$ git submodule init --recursive
$ git submodule update --recursive
```

The command `--depth 10` tells it we do not care about the whole history.

### Setup the virtual environment

```
$ cd ~/duckuments
$ virtualenv --system-site-packages deploy
$ git clone git@github.com:AndreaCensi/mcdp.git
```


## Compiling the documentation   {#compiling-master}

### Compiling all the books

To compile everything from scratch, run:

```
$ make realclean all -j
```

To see the results, open the file

```
~/duckuments/duckuments-dist/index.html
```

If you want to do incremental compilation, you can omit the `clean` and just use:

```
$ make all -j
```

### Compiling a single book

After you have compiled all the books,  you can use one of the following commands to re-compile one single book:

```
$ make book-duckumentation
$ make book-the_duckietown_project
$ make book-opmanual_duckiebot
$ make book-opmanual_duckietown
$ make book-software_reference
$ make book-software_devel
$ make book-software_architecture
$ make book-class_fall2017
$ make book-class_fall2017_projects
$ make book-learning_materials
$ make book-exercises
$ make book-drafts
$ make book-guide_for_instructors
$ make book-deprecated
$ make book-preliminaries
```

The compilation is always incremental, but sometimes you might need to do a reset using:

```
$ make realclean
```

## Editing the books

The books sources are in `docs/docs-![book]`.

Each of those are a submodule.

To edit, do the following.

Fork the `docs-![book]` repository that you wish to edit.

For example, for `docs-exercises`, it looks like this:

    $ cd ~/duckuments/docs/docs-exercises
    $ hub fork
    Updating ![username]
    From ssh://github.com/duckietown/docs-exercises
     * [new branch]      master     -> ![username]/master
    new remote: ![username]

The command has forked the repository.

It also created a new Git remote called `![username]`:

    $ git remote -v
    ![username] git@github.com:![username]/docs-exercises.git (fetch)
    ![username] git@github.com:![username]/docs-exercises.git (push)
    origin  git@github.com:duckietown/docs-exercises.git (fetch)
    origin  git@github.com:duckietown/docs-exercises.git (push)

Tell Git that you want to push to your fork:

    $ git branch --set-upstream-to ![username]/master

Now, when you push you will push to your fork:

    $ git push

To create a pull request, use:

    $ hub pull-request
    https://github.com/duckietown/docs-exercises/pull/![id]

Visit the URL to check your pull request.


## Editing the book collection

Once you have changed your changes to the books, you need to do a pull-request for the `duckuments` repo.


### Forking

As before, make sure you are on your fork:

    $ cd ~/duckuments/
    $ hub fork
    Updating ![username]
    From ssh://github.com/duckietown/duckuments
     * [new branch]      master     -> ![username]/master
    new remote: ![username]
    $ git branch --set-upstream-to ![username]/master


### Updating

For this you need to be able to know how to use submodules.

If you go to `~/duckuments`, the status will appear like this:

    $ git status
    On branch master
    Your branch is up-to-date with 'origin/master'.

    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)
      (commit or discard the untracked or modified content in submodules)

        modified:   docs/docs-exercises (new commits)

This means that you have changes in the submodules that you need to commit.

Just like with files, you can use `git commit` to do so:

    $ git commit -a -m "Update of repository"
    $ git push

Now create the pull request using:

    $ hub pull-request
