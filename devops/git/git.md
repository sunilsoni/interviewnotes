Git
====================

> Git is an open source distributed version control system and source code management (SCM) system with an insistence to control small and large projects with speed and efficiency.


advantages of git
------
- Data repetition and data replication is possible
- It is a much applicable service
- For one depository you can have only one directory of Git
- The network performance and disk application are excellent
- It is effortless to collaborate on any project
- You can work on any plan within the Git


git push
--------
`git push` updates remote refs along with related objects


git pull vs git fetch
--------
`git pull` command pulls innovation or commits from a specific branch from your central repository and updates your object branch in your local repository.

`git fetch` is also used for the same objective, but it works in a slightly different method. When you behave a git fetch, it pulls all new commits from the desired branch and saves it in a new branch in your local repository. If you need to reflect these changes in your target branch, git fetch should be followed with a git merge. Your target branch will only be restored after combining the target branch and fetched branch. To make it simple for you, remember the equation below:

> git pull = git fetch + git merge

conflict
--------
A 'conflict' appears when the commit that has to be combined has some change in one place, and the current act also has a change at the same place. Git will not be easy to predict which change should take precedence.

resolve a conflict
----------
If you need to resolve a conflict in Git, edit the list for fixing the different changes, and then you can run "git add" to add the resolved directory, and after that, you can run the 'git commit' for committing the repaired merge.

git clone
--------
The git clone command generates a copy of a current Git repository. To get the copy of a central repository, 'cloning' is the simplest way used by programmers.

git pull origin
--------
pull is a get and a consolidation. 'git pull origin master' brings submits from the master branch of the source remote (into the local origin/master branch), and then it combines origin/master into the branch you currently have looked out.

git commit a
--------
Git commits "records changes to the storehouse" while git push " updates remote refs along with contained objects" So the first one is used in a network with your local repository, while the latter one is used to communicate with a remote repository.



For more information:

1. [GIT Interview Questions](https://www.javatpoint.com/git-interview-questions)


