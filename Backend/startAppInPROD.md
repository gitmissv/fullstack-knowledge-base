# START YOUR APP IN PRODUCTION #

## Heroku # *** PAID APP ***

   heroku.com to sign up

   > heroku cli - download & install


***RENDER* platform is alternative *FREE* option


**CHECK YOUR VERSIONS OF APPS**

from your computer terminal:
      node -v   *// to check node version*
      
after devDependencies (within pkg.json) add comma, then:
      
      "engines": {
         "node": "14.x"         *// USE YOUR node version*
      }

Update your scripts (*nodemon is only for testing & developing*)

      "scripts": {
         "start": "node app.js"
      }

## Add a Procfile to the route of app #

      Procfile       // NO .js, or other

      within Procfile - add:

            web: node app.js


   Stage your app in GitHub:

      git init          // initialize empty git repo

      git add .         // add everything to staging area (git add 'dot')

      git commit -m "initial commit"      // add your commit message


**IF USING HEROKU*

      heroku login         // to initialize, then press any key to open, login

**CREATE NEW APPLICATION - HEROKU*

      heroku create [name]       // cannot start with number, unique/unduplicated  (i.e.:  jobs-api-06)

      **if no name is added, Heroku will add name for you**

      Make sure in right repo, then add:
         git remote -v

         *be sure you see the (fetch) & (push) values ...

*BEFORE PUSHING UP ... UPDATE YOUR .ENV variables

Command line in .env:

      JWT_LIFETIME=30d

Other alternatives:

      heroku config:set JWT_LIFETIME=30d

      git push heroku master   // push to gitHub

In Heroku:  Add your .env data as Config Vars:

      JWT_LIFETIME
      MONGO_URI
      JWT_SECRET

   Then under "More" menu in upperR -> Restart all dynos

   ... Once app is up and running, copy URL and test out

-----------------------------------------------

# Swagger UI #

Clone an exisiting Heroku app  **Avoid keeping apps on your local machine*
>  In your terminal > navigate to desktop (or wherever your app resides): cd desktop
>  heroku git:clone -a [name of app]       *i.e.: jobs-api-06*

      missing node_modules and .env (due to gitignore)

      > create .env in clonned docs; install pkgs:  npm install && npm start


Once app is running on localhost:[port], export requests from Postman:

      look for 'collection', use menu to 'Export'
      >  use 2nd 'recommended' option > Export > add Name & Location


# APIMatic #

      sign up for *FREE* account:  apimatic.io 

*Import your app*

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


# Swagger UI Editor #

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

**Remove hard-coded path data in SwaggerEditor*, then copy/ paste above

For more info:  see udemy.com course: nodejs-tutorial-and-projects-course:
*https://www.udemy.com/course/nodejs-tutorial-and-projects-course/learn/lecture/27635626#overview*

   >  Section 9: Jobs API (esp:  200 - 213)