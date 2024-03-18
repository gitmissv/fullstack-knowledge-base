FullStack NodeJS and Angular NOTES

Project:

https://github.com/josephwwilliams/postly

Add.env File:

    MONGODB_URL=mongodb+srv://mongotutorial:<password>@cluster0.5wdxkym.mongodb.net/postly?retryWrites=true&w=majority&appName=Cluster0

        *postly is name of project

    JWT_SECRET=

In your terminal - type in 'node', then type in crypto.randomBytes…

        node           <enter>

        … then …

        crypto.randomBytes(32).toString('hex')

OR

        $ node
        > require('crypto').randomBytes(32).toString('hex')

        It will look something like this…

        $ node
        Welcome to Node.js v20.10.0.
        Type ".help" for more information.
        > require('crypto').randomBytes(32).toString('hex')
        ‘string is returned’

_This creates a 32 character random string you can paste into your JWT_SECRET_

#

**NOTE** – if errors when running npm install … check versions under your package.json file. If some are v16 and others are v17 … you can upgrade all … OR … find a version of the lower for the ‘higher’ ones, then update pkg.json.

    THEN … delete package.lock file and xxx … then run npm install again.

    i.e.:  ngx-cookie-service is running on v17 whereas all other @angular on v16

        "dependencies": {
            "@angular/animations": "^16.2.0",
            "@angular/common": "^16.2.0",
            "@angular/compiler": "^16.2.0",
            "@angular/core": "^16.2.0",
            "@angular/forms": "^16.2.0",
            "@angular/platform-browser": "^16.2.0",
            "@angular/platform-browser-dynamic": "^16.2.0",
            "@angular/router": "^16.2.0",
            "ngx-cookie-service": "^17.0.1",
            "rxjs": "~7.8.0",
            "tslib": "^2.3.0",
            "zone.js": "~0.13.0"
        },
        "devDependencies": {
            "@angular-devkit/build-angular": "^16.2.10",
            "@angular/cli": "^16.2.10",
            "@angular/compiler-cli": "^16.2.0",
            "@types/jasmine": "~4.3.0",
            "autoprefixer": "^10.4.16",
            "jasmine-core": "~4.6.0",
            "karma": "~6.4.0",
            "karma-chrome-launcher": "~3.2.0",
            "karma-coverage": "~2.2.0",
            "karma-jasmine": "~5.1.0",
            "karma-jasmine-html-reporter": "~2.1.0",
            "postcss": "^8.4.32",
            "tailwindcss": "^3.4.0",
            "typescript": "~5.1.3"
        }

**Find a version of **ngx-cookie-service\*\* that is compatible with Angular 16.

- everything is version 16 except that package

- need to find a 16 one and change it in the package.json,

       delete package.lock,
       clear npm cache, and
       run npm i again

# Check to see if everything is running

## FrontEnd

    	Run:   ng serve

## Server / Backend

    	Run:   npm run start

**check your work on localhost**
