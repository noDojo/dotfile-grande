# **Git Cheatsheet**

**Add an existing project to an new repository:**

1. Create a new repository in GitHub by clicking the `+` symbol in the top right corner and selecting `New Repository`.

2. Name the repository and initialize it without a README or .gitignore file by clicking the `Create repository` button.

3. In the Finder, locate the existing project's `.git` directory and open the file named `config`. The `url` value under `[remote "origin"]` needs to match the `url` of the new repository you've just created.

4. This can be achieved by running the following commands:

```
$ git remote set-url origin {new-repos-ssh}
$ git pull --rebase
```

5. Now set the master branch of the existing project to match the master branch of the new repository and push the project to its new repository:

```
$ git branch --set-upstream-to=origin/master master
$ git pull --rebase
$ git push
```