# START YOUR APP IN PRODUCTION

## Heroku # **_ PAID APP _**

heroku.com to sign up

> heroku cli - download & install

## RENDER (Deployment Application)

_\*\*RENDER_ platform is alternative _FREE_ option
Start by pushing your project to GitHub – then connect/deploy to Render. But first CREATE NEW REPOSITORY to deploy as a separate project.

_By creating a new repo, each time you make updates, you avoid project being picked up and automatically redeployed by Render._ This also helps avoid ‘bugs’

    	 - Open GitHub – *CREATE NEW Repository*
    	 - Create a ‘temp’ repo name (i.e.:  temp-jobs-api)
    	 - Public
    	 - Click “Create repository”

This will give you commands to push (or create) new repo from command line

    	i.e.:  get remote add origin git@github.com:gitmissv/temp-jobs-api.git
    	git branch -M main
    	git push -u origin main

Go to desktop file, copy existing repo/file – rename with the temp file (i.e.: temp-jobs-api).

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

Confirm you see all of your files in GitHub before proceeding with Render.

### RENDER

    > ADD:  New > Web Service

Create Name (best usually to go with same naming convention (i.e.: temp-jobs-api)

    	Build and deploy from a Git repository > Connect to the repository

Deploy Web Service in Render:

    	Name (unique name for your web service … can be same as git repo).
    	Root Directory:  <leave blank>
    	Environment:  Node
    	Region:  <your region>
    	Branch:  main
    	Build Command:  npm install
    	Start Command:  node app.js              (or server.js if you named that in your fiels)

Go with FREE tier – then ‘Advanced’ … in order for your project to deploy without fail …

### Advanced

Add **Environment Variable(s)**: Add all variables from your .env file for project

    	JWT_LIFETIME:		<add value>
    	JWT_SECRET:		<add value>
    	MONGO_URI:		<add value>
    	Etc., as applicable

Auto-Deploy: YES (if you want Render to pick up whenever updates are pushed to your repo on GitHub.

Finally: Click **Create Web Service** W-A-I-T … this will take several minutes to complete (3-5 min or so).

Once complete, you should see results showing Build successful … etc. and should see what port server is listening on. This is dependent upon the platform we’re using … which is why in our app.js file we set as process.env.PORT … but we can still use whatever port we prefer during build and test processes … end result is as follows:

    	const port = process.env.PORT || 5050;

#

**CHECK YOUR VERSIONS OF APPS**

from your computer terminal:
node -v _// to check node version_

after devDependencies (within pkg.json) add comma, then:

      "engines": {
         "node": "14.x"         *// USE YOUR node version*
      }

Update your scripts (_nodemon is only for testing & developing_)

      "scripts": {
         "start": "node app.js"
      }

## Add a Procfile to the route of app

      Procfile       // NO .js, or other

      within Procfile - add:

            web: node app.js

Stage your app in GitHub:

      git init          // initialize empty git repo

      git add .         // add everything to staging area (git add 'dot')

      git commit -m "initial commit"      // add your commit message

\*_IF USING HEROKU_

      heroku login         // to initialize, then press any key to open, login

\*_CREATE NEW APPLICATION - HEROKU_

      heroku create [name]       // cannot start with number, unique/unduplicated  (i.e.:  jobs-api-06)

      **if no name is added, Heroku will add name for you**

      Make sure in right repo, then add:
         git remote -v

         *be sure you see the (fetch) & (push) values ...

\*BEFORE PUSHING UP ... UPDATE YOUR .ENV variables

Command line in .env:

      JWT_LIFETIME=30d

Other alternatives:

      heroku config:set JWT_LIFETIME=30d

      git push heroku master   // push to gitHub

In Heroku: Add your .env data as Config Vars:

      JWT_LIFETIME
      MONGO_URI
      JWT_SECRET

Then under "More" menu in upperR -> Restart all dynos

... Once app is up and running, copy URL and test out

---

# Swagger UI

Clone an exisiting Heroku app \*_Avoid keeping apps on your local machine_

> In your terminal > navigate to desktop (or wherever your app resides): cd desktop
> heroku git:clone -a [name of app] _i.e.: jobs-api-06_

      missing node_modules and .env (due to gitignore)

      > create .env in clonned docs; install pkgs:  npm install && npm start

Once app is running on localhost:[port], export requests from Postman:

      look for 'collection', use menu to 'Export'
      >  use 2nd 'recommended' option > Export > add Name & Location

# APIMatic

      sign up for *FREE* account:  apimatic.io

_Import your app_

      > Once downloaded (ignore warnings - *Just be sure NO ERRORS*)

      > then click: Edit API
         Basic Settings > Rename (i.e.:  Jobs API), optional, add image
         **CLICK SAVE** before moving on

         Server Configuration > add URL
         **CLICK SAVE** before moving on

         Authentication >

         Endpoints > Bring in Auth and Login routes
            **Skip Authentication**

            > Others, bring in & rename, but DO NOT SKIP AUTH...
            - should have 2 folders: 1) Auth, and 2) Routes

# Swagger UI Editor

> https://editor.swagger.io/

> https://swagger.io/docs/specification/describing-parameters/

Common Parameters
Common Parameters for All Methods of a Path
Parameters shared by all operations of a path can be defined on the path level instead of the operation level. Path-level parameters are inherited by all operations of that path. A typical use case are the GET/PUT/PATCH/DELETE operations that manipulate a resource accessed via a path parameter.

      /jobs/{id}:
         parameters:
            - in: path
              name: id
              schema:
                 type: string
              required: true
              description: The job ID

\*_Remove hard-coded path data in SwaggerEditor_, then copy/ paste above

For more info: see udemy.com course: nodejs-tutorial-and-projects-course:
*https://www.udemy.com/course/nodejs-tutorial-and-projects-course/learn/lecture/27635626#overview*

> Section 9: Jobs API (esp: 200 - 213)
