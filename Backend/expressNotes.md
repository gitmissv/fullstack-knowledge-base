**<H1>Express Notes</h1>**

	**Yarn vs Node Pkg Mgr (npm) **
	First INSTALL yarn using NPM (npm i yarn – g) <if global>
	
	Run    Yarn add -D nodemon
	•	Creates yarn.lock (same as pkg.json)
	•	Yarn installs dependency pkgs in parallel, whereas NPM installs them sequentially – yarn outperforms when installing bigger files.
	•	Yarn is better in terms of speed and performance.
	•	Yarn is more secure but uses more disk space.

   # Create New Project: _ Open in VSCode_
## Add Folders/Files
	backend
		> app.js

	frontend
		> index.html
		> etc.

	public

	run_ **npm init -y**

	Install Packages
		**Express:** npm i express
		**Nodemon** (as devDep):  npm i nodemon -D
		_Add/Update Scripts in pkg.json_

**Create Basic Server EXAMPLE (backend-Express):**
		
In app.js file:
	
	const app = express();

	// CONSTANTS
	const PORT = 5xxx;
	const HOME_PATH = path.resolve(__dirname, ‘../frontend/index.html’);  _// example – use corr [filePathName]_
	const NOT_FOUND_PATH = path.resolve(__dirname, ‘../frontend/404.html’);  _// example – use corr [filePathName]_
	const PUBLIC_PATH = path.resolve(__dirname, ‘../public’)  _// example – use corr [filePathName]_
	const APP_SECRET = ‘ABCDEFG’;  _// example, will actually hide in ‘cookies’/other for security_

	// MIDDLEWARE
	app.use(express.static(PUBLIC_PATH));

	// ROUTES
	app.get(‘/’, (req, res) => {
		res.sendFile(HOME_PATH);
	});
	app.get(‘/api/students’, (req, res) => {
		const secretParam = req.query.secret;
		if (secretParam !== APP_SECRET) {
			res.status(401).json({message: ‘Unauthorized’ });
		}
		res.status(200).json({ students });
	});
	app.all(‘*’, (req, res) => {
		res.status(404).sendFile(NOT_FOUND_PATH);
	});

	// LISTEN SERVER
	App.listen(PORT, () => {
		Console.log(`Server listening on [http://localhost:${PORT}`](http://localhost:$%7bPORT%7d%60));
	});

**Express BASICS**: [https://expressjs.com/](https://expressjs.com/)

	npm i express  _// to install dif’t version, add ‘@[version]; i.e.: npm i express@4.17.1_

	const  express  =  require('express');
	const  app  =  express()

	_Above can also be written as one line:_
		_Const app = require(‘express’)( );_

**Express Methods:**

	app.get  what user is trying to do/requesting
	app.post  what server is sending back to user
	app.put
	app.delete
	app.all  works w/ all methods (typically used for a 404 page, etc.)
	app.use  responsible for middleware
	app.listen  listening on port xxxx

_Basic Example:_

	const  express  =  require('express');
	const  app  =  express()

	app.get('/', (req, res) => {
		res.status(200).send('Home Page')
	})

	app.get('/about', (req, res) => {
		res.status(200).send('About Page')
	})

	app.all('*', (req, res) => {
		res.status(404).send(`<h1>Resource not found</h1>`)
	})

	app.listen(5050, () => {
		console.log('server is listening on port 5050')
	})

**Static Assets:** To gain all files under [folder], create a static asset

App.use(express.static(‘./[filePath]’)

**Express.js (API vs SSR):**

	API – JSON	 |  SSR – TEMPLATE

	Send Data 	 |  Send Template

	Res.json( )  |  res.render( )


##

**JSON Basics**
**Json Response**:  see [https://expressjs.com/en/4x/api.html#res.json](https://expressjs.com/en/4x/api.html#res.json)

Sends a JSON response.  This method sends a response that is the parameter converted to a JSON string using JSON.strigify()

	const express = require('express');
	const app = express();

	app.get('/', (req, res) => {

	res.json([{name: ‘mike’}, {name: ‘austin’}])
	})

	app.listen(5050, () => {
		console.log('Server is listening on port 5050...')
	})  const  express  =  require('express');

	const  app  =  express();
	const {products} =  require('./data')

	app.get('/', (req, res) => {
		res.json(products)
	})

	app.listen(5050, () => {

	console.log('Server is listening on port 5050...')
	})

**ROUTE Parameters:  use colon to identify specific data (i.e.:  api/products/:productID = get by prodID)**

	app.get('/api/products/:productID', (req, res) => {
		// console.log(req)
		// console.log(req.params)
	const {productID} =  req.params;

	const  singleProduct  =  products.find((product) =>  product.id  ===  Number(productID))
	if(!singleProduct) {
		return  res.status(404).send(`<h1>ERROR: Product does not exist!</h1>`)
	}
	return  res.json(singleProduct)
	})

**Query String:**

>Example API: [https://hn.algolia.com/api](https://hn.algolia.com/api) (search: _hacker news algolia api_)
>
>TAGS:  tags can be used based on your API data.  And (&) is default; Or uses parenthesis ()
>>i.e.:  query?search=a&limit=2

**Basic Express Server** _EXAMPLE_:

	const  express  =  require('express');
	const  app  =  express();

	const  PORT  =  5050;

	// ! request => middleware => response

	app.listen(PORT, () => {
		console.log(`Server is listening on port http://localhost:${PORT}`)
	})

**Middleware**:

>Middleware functions have access to the request object (req), the response object (res), and the next middleware function in the code (next).  It can execure any code, terminate the request-response cycle, make needed changes in req and res objects and detect errors.

	// ! request => middleware => response
	// Method, url, date

	const  logger  = (req, res, next) => {
		const  method  =  req.method
		const  url  =  req.url
		const  date  =  new  Date().getFullYear()
		console.log(method,url,date)
		next()
	}

app.get('/', logger, (req, res) => {

res.send('Home')

})

	app.get('/about', logger, (req, res) => {
	res.send('About')
	})

Middleware(cont):

	1. **Use vs Route**:
		a. Use (single) = use in specific get request (app.get) either individual or array []
		b. <![endif]>Route (multiple) = use as a function at top to trigger all requests

	2. **Options** – our own / express / third party
		a. Own = can always set up your own middleware, function or single
		b. Express = app.use() method is _expecting_ a middleware (i.e.: static – app.use().static(‘./[filePath]’]
		c. Third Party = i.e.: morgan npm [https://www.npmjs.com/package/morgan](https://www.npmjs.com/package/morgan); install pkg (npm I morgan)

**HTTP Methods**(cont):

	GET (default)  =  Read Data  _get all orders_
	
	POST  =  Insert Data  _place an order (send data)_
	
	GET  = Single Data  _get single order (path params – separate w/ ‘:’)_

	PUT  =  Update Data  _update specific order (params + send data – separate w/ ‘:’)_

	DELETE  =  Delete Data  _delete order (path params)_

****NOTE** Path can be the SAME (i.e. (‘/api/people/:id’…)) but each method makes path a different request**

**GET :**

	// HTTP Get Method
	app.get('/api/people', (req, res) => {
	res.status(200).json({success:true, data:people})
	})

**POST:**

	// ! HTTP Post Method
	app.post('/login', (req, res) => {
	const {name} =  req.body;
	if(name) {
	return  res.status(200).send(`Welcome ${name}`)
	}
	res.status(401).send(`<h1>Please provie your name</h1>`)
	})

**Postman**: [https://www.postman.com/](https://www.postman.com/)
>Used to run backend programming without need for frontend data.



**Put Method:** Updating data (update specifics [params + send data])

	****NOTE** Path can be the SAME (i.e. (‘/api/people/:id’…)) but each method makes path a different request**
>Set up route parameter with : separator (i.e.: [www.store.com/api/orders/:id](http://www.store.com/api/orders/:id))
>
>Look for specific params AND update

	app.put('/api/people/:id', (req, res) => {
		const {id} = req.params
		const {name} = req.body

		const person = people.find((person)=> person.id === Number(id))

		if(!person) {
			return res.status(404).json({success: false, msg: `no person with id ${id}`})
		}

		const newPeople = people.map((person)=>{  		// update new_
			if(person.id === Number(id)){
				person.name = name
		}
			return person
		})
			res.status(200).json({success: true, data: newPeople})  	// update new_
		})

  
**Delete Method:**  Deleting data

	app.delete('/api/people/:id', (req, res) => {

	const person = people.find((person) => person.id === Number(req.params.id))
		if (!person) {
			return res.status(404).json({success: false, msg: `no person with id ${req.params.id}`})
	}

	// filter out array

	const newPeople = people.filter((person)=> person.id !== Number(req.params.id))
	return res.status(200).json({success: true, data: newPeople})
	})

**EXPRESS Router**

Create **router** folder (router) in program, then set up data:

>Create file:  people.js_

	const express = require('express');
	const router = express.Router();

	let {people} = require('../data')

	router.get('/', (req, res) => {
		res.status(200).json({success: true, data: people})
	})

	router.post('/', (req, res) => {
		const {name} = req.body
		if(!name) {
			return res.status(400).json({success: false, msg: 'Please provide your Name'})
		}
		res.status(201).json({success: true, person:name})
	})

	router.post('/postman', (req, res) => {
		const {name} = req.body
		if (!name) {
			return res.status(400).json({success: false, msg: 'Please provide your Name'})
		}
		res.status(201).json({success: true, data: [...people, name]})
	})

	router.put('/:id', (req, res) => {
		const {id} = req.params
		const {name} = req.body

	const person = people.find((person)=> person.id === Number(id))
		if(!person) {
			return res.status(404).json({success: false, msg: `no person with id ${id}`})
		}

	const newPeople = people.map((person)=>{
		if(person.id === Number(id)){
			person.name = name
		}
		return person
	})
		res.status(200).json({success: true, data: newPeople})
	})

	router.delete('/:id', (req, res) => {
		const person = people.find((person) => person.id === Number(req.params.id))
		if (!person) {
			return res.status(404).json({success: false, msg: `no person with id ${req.params.id}`})
		}

		// filter out array
		const newPeople = people.filter((person)=> person.id !== Number(req.params.id))
		return res.status(200).json({success: true, data: newPeople})
	})

	module.exports = router

_Create file:  auth.js_

	const express = require('express');
	const router = express.Router();

	router.post('/', (req, res) => {
		const {name} = req.body;
		if(name) {
			return res.status(200).send(`Welcome ${name}`)
	}
		res.status(401).send(`<h1>Please provie your name</h1>`)
	})

	module.exports = router_

_then in app.js:_

	const express = require('express');
	const app = express();

	const people = require('./routes/people')
	const auth = require('./routes/auth')
	const PORT = 5050;

	// ! Middleware Data

	// static assets
	app.use(express.static('./methods-public'))

	// parse form data
	app.use(express.urlencoded({extended: false}))

	// parse json
	app.use(express.json())

	app.use('/api/people', people)
	app.use('/login', auth)

	app.listen(PORT, () => {
		console.log(`Server is listening on port http://localhost:${PORT}`)
	})

_Express Router_ – **Controllers**:

	let {people} = require('../data')
	const getPeople = (req, res) => {
		res.status(200).json({success: true, data: people})
	}

	const createPerson = (req, res) => {
		const { name } = req.body
		if (!name) {
			return res.status(400).json({success:false, msg: 'Please provide name'})
		}
		res.status(201).send({success: true, person: name})
	}

	const createPersonPostman = (req, res) => {
		const { name } = req.body
		if(!name) {
			return res.status(400).json({success:false, msg: 'Please provide name'})
		}
		res.status(201).send({success:true, data: [...people, name]})
	}

	const updatePerson = (req, res) => {
		(req, res) => {
			const {id} = req.params
			const {name} = req.body

	const person = people.find((person)=> person.id === Number(id))

		if(!person) {
			return res.status(404).json({success: false, msg: `no person with id ${id}`})
	}

	const newPeople = people.map((person)=>{
		if(person.id === Number(id)){
			person.name = name
	}

	return person
	})
	res.status(200).json({success: true, data: newPeople})
	}
	}

	const deletePerson = (req, res) => {
		const person = people.find((person) => person.id === Number(req.params.id))
		if (!person) {
			return res.status(404).json({success: false, msg: `no person with id ${req.params.id}`})
		}

	// filter out array
	const newPeople = people.filter((person)=> person.id !== Number(req.params.id))
		return res.status(200).json({success: true, data: newPeople})
	}

	module.exports = {
		getPeople,
		createPerson,
		createPersonPostman,
		updatePerson,
		deletePerson,
	}

const express = require('express');

const router = express.Router();

const {

getPeople,

createPerson,

createPersonPostman,

updatePerson,

deletePerson,

} = require('../controllers/people')

// router.get('/',getPeople)

// router.post('/',createPerson)

// router.post('/postman',createPersonPostman)

// router.put('/:id',updatePerson)

// router.delete('/:id',deletePerson)

router.route('/').get(getPeople).post(createPerson);

router.route('/postman').post(createPersonPostman);

router.route('/:id').put(updatePerson).delete(deletePerson)

module.exports = router

**Database Relationships:**

**1:1 Relationship (One-to-One)**

In a one-to-one relationship, an entity in one table is linked to at most one entity in another table.

	**User and User Profile**: In a user management system, each user has exactly one profile, and each profile is associated with exactly one user.
		-Users might contain login information, and UserProfiles might contain personal details like address and phone number.

	**Person and Passport**: Each person can have at most one passport, and each passport is issued to at most one person.
		-Persons might contain personal information, while Passports contain passport-specific data like passport number and issue date.

	**CEO and Company**: In a corporate database, each company has at most one CEO, and each CEO is head of at most one company (assuming they don’t lead multiple companies).

_*Note on this last one… this is highly relevant to your application… it may make sense to NOT have a 1:1 relationship for CEO and Company. Database modeling is sometimes subjective!

**1:M Relationship (One-to-Many)**

In a one-to-many relationship, an entity in one table can be linked to multiple entities in another table.

	**Author and Books**: An author can write multiple books, but each book is written by one specific author.
		-Authors contains author details, while Books contains details about the books.

	**Teacher and Students**: A teacher can have multiple students in a class, but each student is assigned to one teacher (in the context of a specific class).

	**Parent and Children**: A parent can have multiple children, but each child has one set of parents

**M:N Relationship (Many-to-Many)**

	In a many-to-many relationship, entities in one table can be linked to multiple entities in another table and vice versa. These are typically implemented using a junction table.

	**Students and Courses**: Students can enroll in multiple courses, and each course can have multiple students.
		**Tables**: Students, Courses, and a junction table like StudentCourses.

	**Doctors and Patients**: Doctors can have multiple patients, and patients can see multiple doctors.
		**Tables**: Doctors, Patients, and a junction table like DoctorPatient._

	**Authors and Research Papers**: Authors can co-write multiple research papers, and each paper can have multiple authors.
		**Tables**: Authors, ResearchPapers, and a junction table like AuthorPapers._

##

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

-   [Build A REST API With Node.js, Express, & MongoDB - Quick](https://www.youtube.com/watch?v=fgTGADljAeg&pp=ygUSbW9uZ29kYiBhbmQgbm9kZWpz)
-   [Node.js Crash Course Tutorial #9 - MongoDB](https://www.youtube.com/watch?v=bxsemcrY4gQ)
-   [How to create MongoDB Schemas and Data Models | Node.js Tutorials for Beginners](https://www.youtube.com/watch?v=jZ-dzj6ut54)

_**May want to watch the first video multiple times and work through it at your own pace._

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
**All Schema Types**

>_required_: boolean or function, if true adds a [required validator](https://mongoosejs.com/docs/validation.html#built-in-validators) for this property
>
>_default_: Any or function, sets a default value for the path. If the value is a function, the return value of the function is used as the default.
>
>_select_: boolean, specifies default [projections](https://www.mongodb.com/docs/manual/tutorial/project-fields-from-query-results/) for queries
>
>_validate_: function, adds a [validator function](https://mongoosejs.com/docs/validation.html#built-in-validators) for this property
>
>_get_: function, defines a custom getter for this property using Object.defineProperty().
>
>_set_: function, defines a custom setter for this property using Object.defineProperty().
>
>_alias_: string, mongoose >= 4.10.0 only. Defines a virtual with the given name that gets/sets this path.
>
>_immutable_: boolean, defines path as immutable. Mongoose prevents you from changing immutable paths unless the parent document has isNew: true.
>
>_transform_: function, Mongoose calls this function when you call Document#toJSON() function, including when you JSON.stringify() a document.

**String**

>_lowercase_: boolean, whether to always call .toLowerCase() on the value
>
>_uppercase_: boolean, whether to always call .toUpperCase() on the value
>
>_trim_: boolean, whether to always call .trim() on the value
>
>_match_: RegExp, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value matches the given regular expression
>
>_enum_: Array, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is in the given array.
>
>_minLength_: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value length is not less than the given number
>
>_maxLength_: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value length is not greater than the given number
>
>_populate_: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)

**Number**

>_min_: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is greater than or equal to the given minimum.
>
>_max_: Number, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is less than or equal to the given maximum.
>
>_enum_: Array, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is strictly equal to one of the values in the given array.
>
>_populate_: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)

**Date**

>_min_: Date, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is greater than or equal to the given minimum.
>
>_max_: Date, creates a [validator](https://mongoosejs.com/docs/validation.html) that checks if the value is less than or equal to the given maximum.
>
>_expires_: Number or String, creates a TTL index with the value expressed in seconds.

**ObjectId**

>_populate_: Object, sets default [populate options](https://mongoosejs.com/docs/populate.html#query-conditions)
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