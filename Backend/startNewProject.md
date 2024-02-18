**Building REST API with Node.js, Express, & MongoDB**

**New Application**:

    Initialize & Install pkg.json:  **npm init -y**

    Initiate GitHub repository:  **git init**

    Install Dependencies:  **npm i express mongoose dotevn**
    	> Express creates web application using express than stsandard js; provides tools to make js easier
    	> Mongoose allows to interact with MongoDB
    	> Dotenv:  allows to pull in environment variables from a .env file

    Install DevDependencies: npm i --save-dev nodemon
    	// --save-dev is same as -D
    	> Nodemon:  allows to refresh server every time you make changes w/o having to restart server (manually) and is typically only used during development/testing stages

    AS NEEDED ... Install:
    	npm i express-fileupload
    		// w/Yarn:  yarn add express-fileupload
    	> allows your app to upload files, photos, etc.

    	Security Packages:
    		npm i helmet      			// middleware pkg protects agains vulnerabilities
    		npm i xss-clean   			// Cross-Site Scripting
    		npm i express-rate-limit	// middleware pkg used to limit repeated requests to APIs & endpoints


    Package.json:
    	> REMOVE test script and create own (like Start, Dev, devStart, or other) to allow to start server
    	> i.e.:  “devStart”: “nodemon server.js”  || or ||  “nodemon app.js”

    Create Files:
    	> server.js ||  **app.js** _// app.js or server.js serve same purpose_
    	> .gitignore       // add .env and /node_modules_
    	> .env

    Create Folder(s):
    	 > routes  (_contains the path for all processes/functions_)
    		> [name].routes.js      // within routes folder

    	> controllers  (contains the processes/functions)
    		> [name].controller.js

    	> lib
    		> constants.lib.js
    		> mongoose.lib.js

    	>models
    		> [name].models.js

    	>middleware            // could also add files w/i lib folder
    		> not-found.middleware.js
    		> asyncWraper.middleware.js

**Review of Concepts – videos to watch:**

- [Build A REST API With Node.js, Express, & MongoDB - Quick](https://www.youtube.com/watch?v=fgTGADljAeg&pp=ygUSbW9uZ29kYiBhbmQgbm9kZWpz)
- [Node.js Crash Course Tutorial #9 - MongoDB](https://www.youtube.com/watch?v=bxsemcrY4gQ)
- [How to create MongoDB Schemas and Data Models | Node.js Tutorials for Beginners](https://www.youtube.com/watch?v=jZ-dzj6ut54)

_\*\*May want to watch the first video multiple times and work through it at your own pace._

#

**app.js file:**

    // IMPORTS_
    require(‘dotenv’).config( )

    const express = require(‘express’)
    const app = express( )

    const connectToDB = require(‘./middleware/mongoose’)  // could also be located in a db file

    // MIDDLEWARE_
    app.use(express.json( ))  		// parse json data_

    const subscribersRouter = require(‘./routes/subscribers’)
    app.use(‘/subscribers’, subscribersRouter)

    // ROUTES_
    app.use(‘/api/v1/…’, …);

    // LISTEN & DB_
    async function startBackend( ) {
    	try {
    		// Connect to DB_
    		await connectToDB(process.env.MONGODB_URL);

    		app.listen(PORT, ( ) => console.log(‘Server is listening at: ${SERVER_URL}’)

    	})  catch (err) {
    			Console.log(‘ERROR’, err)
    		}
    	};

    startBackend( )

#

**router:subscribers.js file:**

    const express = require(‘express’)
    const router = express.Router( )

    const { getAllProducts, … } = require(‘./…/controllers/…);

    // Getting ALL (get)_
    router.get(‘/’, (req, res) => {
    })

    // Getting One (get)_
    router.get(‘/:id’, (req, res) => {
    })

    // Creating One (post)_
    router.post(‘/’, (req, res) => {
    })

    // Updating One (patch or put)_
    	_*Patch:  updates only the data the user sends/passes_
    	_*Put:  updates all data all at once (not just information that is passed)_
    router.patch(‘/:id’, (req, res) => {
    })

    // Deleting One (delete)_
    router.delete(‘/:id’, (req, res) => {
    })

    module.exports = router

#

**Middleware:mongoose.js file:**

    const mongoose = require('mongoose'); _// import mongoose_

    const connectToDB = (url) => {
    	const dbConnection = mongoose.connect(url); _// connect to database_
    	if (dbConnection) {
    		console.log('Connected to database successfully!'); _// log success message_
    	}
    	return dbConnection; _// return database connection_
    };

    module.exports = connectToDB; _// export connectToDB method_

#

**.env:**

    MONGO_URL=mongodb+srv…..

#

**models: model.js file:**

    const mongoose = require(‘mongoose’);

    const taskSchema = new mongoose.Schema({
    	name: {
    		type: String,
    		required: [true, ‘Must provide a name’],
    		trim: true,
    		maxlength: [25, ‘Name cannot exceed 20 characters’],
    	},
    	Price: {
    		Type: Number,
    		Required: [true, ‘Product price must be provided’],},
    	completed: {
    		type:  Boolean,
    		default: false,},
    });

    Module.exports = mongoose.model(‘Task’, taskSchema);

#

**asyncWrapper (middleware):**

    const asyncWrapper = (callback) => {
    	return async (req, res, next) => {
    	try {
    		await callback(req, res, next);
    	}  catch (err) {
    		Next(err);
    		}
    	};
    };

    Module.exports = asyncWrapper;

#

**controllers:**

    const asyncWrapper = require(‘./…../async-wrapper/…);

    const getAllProducts = asyncWrapper(async (req, res) => {
    	res.status(200).json({ msg: ‘All Products!’ });
    });

    module.exports = {
    	getAllProducts,
    	…
    };

#

**PORT VARIABLE**: _When ready to deploy app_

const port = process.env.PORT || 3000

**Query Strings:**

Sort vs Select: _Sort_ will sort by [name, object, etc] whereas _Select_ will call back only the fields chosen.

#

**OperatorMap:**

    if (numericFilters) {
    	const operatorMap = {
    		'>':'$gt', _// greater than_
    		'>=':'$gte', _// greater than or equals_
    		'=':'$eq', _// equals_
    		'<':'$lt', _// less than_
    		'<=':'$lte', _// less than or equals_
    	}

    const regEx = /\b(<|>|>=|=|<|<=)\b/g;
    	let filters = numericFilters.replace(
    		regEx,
    		(match) => `-${operatorMap[match]}-`
    	);

    const options = ["price", "rating"];
    	filters = filters.split(",").forEach((item) => {
    	const [field, operator, value] = item.split("-");
    	if (options.includes(field)) {
    		queryObject[field] = { [operator]: Number(value) };
    	}
    });
    	console.log(numericFilters);
    }

#
