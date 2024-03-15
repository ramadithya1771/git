# Git --> Version Control System, Github --> UI which adds on git.
Repository --> Folder or place we store code
Local Repository --> Sits on our local machine and its our version of the code
Remote Repository --> A place where many developers can access to make a project or personal program and use it as the main code

Usually we do the code on our local machine and then it is pushed to the remote repository 
If others want to have the changes you made on their local machine they pull it from the remote repository to their local machine.

# Git History:

Git has a history of all the changes being made, which is done through "commit".

So commit is like a checkpoint.
We can retrieve the commit incase the code goes wrong in the future.

Lets say that we do some bug fix or some changes to our code in our local machine. To make sure we have some checkpoints at certain times, 
we commit the code on our local machine. Later on, this can be retrieved if anything goes wrong in the future.

When we push this commit to the remote repository, it merges the existing code with the commit.

# Git Branches:

The main branch is called the "master or main"

Assume a timeline, where each * is a commit made and the right most end being the present.
<--------*---------*------------*-----------*-------------*--->
                      <master or main>


<--------*---------*------------*-----------*-------------*--->
                   | <master or main branch>
                    \
                     \ 
                       ------------*------*
                          <new branch>


Branches are made so that the members can work on the project on a new timeline and can merge it with the master
(which has the ideal code that works always).
If you are sure in knowing that your code works and is the right one, you can commit and push directly to the master branch.

The new branch can still get updated from the main branch(master) and can be kept up to date.

In more advanced and long projects, the new branches have their own branches, which works in the same way as the master and the new branch.


# Git commands:

git init -- This is to make sure that the repo on the local machine will be tracked by git and all git commands can be used

* Let say we make repository on our local machine

-- mkdir test_repo

* To make sure git tracks this repo, we will initialize it

-- cd test_repo #Get into the repo first
-- git init #initialize to get the git commands working

* Now, lets say we create a file called "readme.md"

--touch readme.md

* Then lets say there are some contents in this file.

  When we think the changes we made so far in our repo is worthy of a checkpoint which we want to return to in the future,
  we will be commiting this

*---------------------------------------------------------------------------------------------------------------------------------------*

* After this, there is a part called the staging place

* Here we can add or remove specific changes which we want our    commit to have the record of.

* So lets say we add this change,

-- git add readme.md

Since this is the only change we made, we will be commiting it or aka creating a checkpoint.

*---------------------------------------------------------------------------------------------------------------------------------------*

--git commit -m "added readme file" # -m indicates the message for each commit within 50 characters describing the changes made

[main (root-commit) dc12a83] added readme.md
 1 file changed, 1 insertion(+)
 create mode 100644 readme.md


 * Here we get a commit ID and shows how the commit is made on the main branch or the master branch.

*---------------------------------------------------------------------------------------------------------------------------------------*

 * Let say now we make one more change by adding extra content in the readme.md file

 * when we try,

 -- git status

 we get,

 On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   readme.md

* As we can see, the changes we made our waiting to be staged and then commited.
Now to do the same thing again but in a different way,

we can do,

 -- git add . # The . considers all the changes to be commited next
 -- git commit -m "Made Changes"

 Or,

 -- git commit -am "Made Changes" # This does staging and commiting simultaneously


 * The output for both these would be,

 [main 24df03a] Made changes
 1 file changed, 3 insertions(+), 1 deletion(-)

 *---------------------------------------------------------------------------------------------------------------------------------------*

 * Now when we dont want to do any more commits on the main branch, and instead want to work on a new branch to use them for the main later on, we create a new branch and this is done by,

 -- git checkout -b new # -b creates a new branch and checkout switches you to the progress of that new branch, here "new" is the name
                          of the branch.
* Now we have all the information similar to that of the main branch, but from here on, we will be commiting and doing all the changes in the new branch.

 *---------------------------------------------------------------------------------------------------------------------------------------*

* Lets say we edit the content of readme.md in this branch,
Now we will stage this and then commit,

-- git add .
--git commit -m "first commit on new branch" 

* When we try switching back to the main branch by,

-- git checkout main # Switches the branch to main

* The changes we made in the new branch wont affect the main, So we get the same contents which existed from the last time we left.

 *---------------------------------------------------------------------------------------------------------------------------------------*

* Lets say we create a new file in the main branch,

-- touch test.py # Creates an empty .py file

* Lets say it has some contents in it.

* Lets stage it and commit,

-- git commit -am "added test.py"

* Now when we switch back to the new branch,
 
 -- git checkout new

We can see it hasnt been affected.

 *---------------------------------------------------------------------------------------------------------------------------------------*

* If we want the new branch to get updated by the changes made on the main branch, we will merge it,
(Note: Before merging, make sure you are currently in the branch which you want it to be updated)

-- git merge main

* This now updated the new branch with all the changes that took place in the main.
(Note : The extra content added in the new branch will remain as it was but the other changes will be updated)

* If you want to update main with the contents of the new branch, then we checkout to main and then merge the new branch.

 *---------------------------------------------------------------------------------------------------------------------------------------*

# Remote Repositories

We are going to go on a platform called "Github" to create a remote repository.

A remote repository is basically people being able to see your codes and content and it is not confined within your local machine. This is also tracked by git and all commands can be applied.

* First, we create a new repo in Github.

* We take the ssh key and copy it

* Use the terminal and do the following command,

-- git remote add origin git@github.com:ramadithya1771/test.git 

* This is called a remote, which sets the remote repo's URL to the name "origin", so now we will be able to push our content from the local machine onto our remote repo.

 *---------------------------------------------------------------------------------------------------------------------------------------*

Now we do the command to push files from our local machine to the remote repo

-- git push -u origin main
 
 * This command pushes the content from your local repo to origin(remote repo URL) and on the main branch of the remote repo.
 (Note: Make sure you are in the correct branch before pushing to remote repo, i.e. Your local repo should be on main to push it correctly to main on the remote repo. This is not compulsory, but to have the same data on both ends, it should be aligned with each other)

 *---------------------------------------------------------------------------------------------------------------------------------------*

* Let say there are changes made in the remote repo that is the one on Github.

* Lets say we also make changes on our local repo on our local machine.

* When we try pushing our changes to the remote repo, we will get a conflict, which should be manually resolved.

To github.com:ramadithya1771/test.git
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'github.com:ramadithya1771/test.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.


* This is done by doing,
 
 -- git pull origin main

* After this, go into the file and manually correct them to what both the remote and local repo has to be.

* In the end, it can be pushed back to the remote repo with no conflicts.

-- git push 

* You dont need to do git push origin main everytime, git knows it is in origin so just git push will do fine 

# Pushing into a new branch on the remote repo

We do,

-- git push origin new

