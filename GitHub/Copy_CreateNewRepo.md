# CREATE NEW REPOSITORY and/or COPY as a separate project.

    	 - Open GitHub – *CREATE NEW Repository*
    	 - Create a repo name (i.e.:  blogPostStarter)
    	 - Public / Private  <your choice>
    	 - Click “Create repository”

This will give you commands to push (or create) new repo from command line

    	i.e.:  get remote add origin git@github.com:gitmissv/blogPostStarter.git
    	git branch -M main
    	git push -u origin main

Go to desktop file, copy existing repo/file – rename with the new file (i.e.: blogPostStarter).

\*_Be sure to copy so that you create ‘new’ that has not been pushed to GitHub._

Move file to desktop, then open VSCode and copy new file into VSC, then _REMOVE_ existing GitHub repo

    	rm -rf .git

Once removed, set up github repo (git init), add all of the files (git add .), then make first commit (git commit -m “first commit”) :

    	git init

    	git add .

    	git commit -m “first commit”

Once above is completed, copy/paste lines of code from GitHub command for new repo \*_(… or push an existing repo from the command line)_:

    	get remote add origin git@github.com:gitmissv/temp-jobs-api.git
    	git branch -M main
    	git push -u origin main

Confirm you see all of your files in GitHub before proceeding.
