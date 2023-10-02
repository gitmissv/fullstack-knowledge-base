# Cloning FULL Repository from GitHub

*git clone* is how you get a local copy of existing repository to work on ... when you do NOT already have a copy on your computer.

1. Open your repository in GitHub
2. Click <> Code to get your link

> copy the HTTPS link

3. Open Git Bash terminal

> Navigate to the appropriate directory you want your cloned files
Run git clone [*https link from repository*]


> i.e.  git clone https://github.com/gitmissv/fullstack-knowledge-base.git

**NOTE**  Copy/Paste functions:  
> To copy in Git Bash: hold Shif and use the left/right arrows to select text area, then press 'Enter' to copy.

> To paste in Git Bash: use (Shift + Insert)


4. Press **Enter** to create your local clone

***When finished working - be sure to upload updates (commit) back to GitHub.**



# Pulling changes from a remote repository

*git pull* is a shortcut for both git fetch and git merge and is how you **UPDATE** your local copy with new commits from the remote repository on GitHub.

> i.e.:  git pull REMOTE-NAME BRANCH NAME
*grabs online updates and merges them with local work*

**Make sure local work is committed before running the *pull* command**

> **ISSUES**:  quit the merge by running *git merge --abort* to take branch back where it was before you pulled.



# Fetching Changes from Remote Repository

Use *git fetch* to retrieve updates (by others or you working on different computers). 

> Fetching will grab all new work and tags without merging the changes into your own branch.

If you already have a local respository with a remote URL for project, you can grab all of the new info using *git fetch* * *remotename* * in terminal

> i.e.:  git fetch REMOTE-NAME


# Merging changes into your local **branch**

Merging combines your local changes w/ changes made by others.

> git merge REMOTE-NAME/BRANCH-NAME
merges updates made online with your **local** work.



See also GitHub docs about Managing Remote repositories:  https://docs.github.com/en/get-started/getting-started-with-git/managing-remote-repositories