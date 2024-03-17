**BACKEND | NodeJS Notes**

**Globals:**

	__dirname  path to current directory

	__filename  file name

	require  function to use modules (CommonJS)

	module  info about current module (file)

	process  info about environment where the program is being executed

Examples:

	console.log(__dirname)

	setInterval(( ) => {

	console.log(‘hello world’)

	}, 1000)

_// Control + C will stop process from running_

**Modules:**

	> CommonJS – every file in Node is a module (by default)
	> Modules are Encapsulated Code (only sharing minimum)
	> Create a [name].js for one module (i.e.: names) and another [name].js file for second module (i.e.: code data/utilities)

_EXAMPLES:_

>In Module 1:_

	const mike = ‘Mike’

	const austin = ‘Austin’

	module.exports = { mike, austin }  _// to share data (or extract) with another module/file_

>In Module 2:_

	const sayHi = (name) => {

	console.log(`Hello there, ${name}`)

	}

	module.exports = sayHi  _// to share data (extract) to another module/file_

>In app.js use ‘require’:_

	const names = require(‘./[path]’)

	const sayHi = require(‘./[path]’)

	sayHi(‘Verona’)

	sayHi(names.mike)

	sayHi(names.austin)

**Modules (cont):**

Built-in Modules:
>OS  Operating System Module
>PATH
>FS  File System Module
>HTTP

Sync vs Async:
>Sync:  Synchronous programming executes tasks sequentially and is dependent on the previous task running/completing.
>>Single-thread so only one operation/program can run at a time.
>
>Async:  Asynchronous programming allows tasks to run concurrently (not dependent upon other tasks).
>>Multi-thread so operations can run in parallel.

HTTP Module:
>Req (request) = represents incoming request (from web browser)
>Res (response) = represents what we’re sending back

_EXAMPLE-1:_

	const http = require(‘http’);

	const server = http.createServer((req, res) => {

	_console.log(req)  // typically will not want to do this as it will return LARGE FILE;_

	res.write(‘Welcome to our home page’)

	res.end( )

	})

	Server.listen(5000) _// can be 5555 or other; but typical ‘test’ ports are in the 5000 range._

_EXAMPLE-2:_

	const http = require(‘http’);
	const server = http.createServer((req, res) => {
		console.log(req)  // typically will not want to do this as it will return LARGE FILE;_
		if(req.url === ‘/’) {
			res.end(‘Welcome to our home page’)
			return
		}

		(req.url === ‘/about’) {
			Res.end(‘Here is our short history’)
			return
		}

		res.end( ‘[use h1 here]Oops![end /h1 here]
			[use p here] We can’t seem to find the page you are looking for[end /p here]
			[use a href=”/” here]back home[end /a here])
		})

	// could use (refactor) to: if / else if / else with no return after_

	Server.listen(5000)

**NPM**:  **Node Package Manager** ([https://www.npmjs.com/](https://www.npmjs.com/))

>Calls a reusable code (package) – contains js code; sometimes referred to as module, package, dependencies
>
>There is no quality control on npm registry (anyone can do anything) – up to you to ‘sniff out’ what’s good vs what’s not!
>
>Go to npmjs.com to search for packages (i.e.:  bootstrap, etc.)

npm – global command, comes with node

npm –version  _// run in terminal to check version you’re running_

	local dependency – use it only in _a_ particular project
		npm i [pkgName]

	global dependency – use it in any project
		npm i -g [pkgName]

**_Async/Await Example:_**

	Const { readFile, writeFile } = require(‘fs’).promises

	Const start = async ( ) => {

	Try {
		const first = await readFile(‘./[fileName]’, ‘utf8’)
		const second = await readFile(‘./[fileName]’, ‘utf8’)
		await writeFile(‘/[newFileName’, `THIS IS AWESOME : ${first} ; ${second}`,
		{ flag: ‘a’ }
	)

	Console.log(first, second)
	} catch (error) { ….

**Events**:

_Event-Driven Programming_ – flow of the program is determined on the events; listen for specific events then provide results

Events Emitter (code example)  (**on** <listen for event> and **emit** <emit an event>)

	Const EventEmitter = require(‘events’);

	Const customEmitter = new EventEmitter( )

	customEmitter.**on**(‘response’, () => {    // on pass in string and call-back
		console.log(‘data received ‘)  // can have as many ‘on’ listeners as you want (order matters)
	})

	customEmitter.**emit**(‘response’)   // emit pass in same string listening for (from ‘on’)

	   // only need **one** emit (unless there are ‘on’ written AFTER emit)_

_EXAMPLE-2_ Events Emitter_:_

	const http = require(‘http’);

	const server = http.createServer( )  // using Event Emitter API

	server.on(‘request’, (req, res) => {  // emits request event (subscribe, listen, respond)

	res.end(‘Welcome’)
	})

	Server.listen(5000)

**Streams:**

>Writeable
>Readable
>Duplex
>Transform

Read Stream: _// allows large data files to run in ‘chunks’ (like mass emails) in order to successfully run without err_

**Create big file**

	Const { writeFileSync } = require(‘fs’)

	For (let i = 0; i < 10000; i++) {

	writeFileSync(‘./content/big.txt’, `Hello World ${i}\n`, { flag: ‘a’ })

	}

	**Run … node [fileName] **

*THEN …*

	Const { createReadStream } = require(‘fs’);

	Const stream = createReadStream(‘./content/big.txt’, {  // name of file just written above
			highWaterMark: 90000, encoding: ‘utf8’, );

_// default ‘buffer’ file is 64kb (per ‘chunk’)_

_// last ‘buffer’ file shows remainder of data (< 64kb)_

_// highWaterMark – allows you to control the size (added above in readStream file)_

_// const stream = createReadStream(‘./[filename]’, { highWaterMark: 90000, encoding: ‘utf8’ })_

	stream.**on**(‘data’, (result) => {
		Console.log(result)
	})

stream.on(‘error’, (err) => console.log(err))

_ReadStream Example#2_

// ? NOTE:  fileStream allows to pipe (i.e.: if you can ReadStream; you can add .pipe to push from readStream into writeStream) … in short, you take your readStream and pipe into a writeStream

**Create big file**

	Const { writeFileSync } = require(‘fs’)
	For (let i = 0; i < 100000; i++) {
		writeFileSync(‘./content/big.txt’, `Hello World ${i}\n`, { flag: ‘a’ })
	}

	**Run … node [fileName] **

*THEN …*

	Const http = require(‘http’);
	Const fs = require(‘fs’);

	http.createServer(function (req, res) {
		const fileStream = fs.createReadStream(‘./[filePath]’, ‘utf8’);
		fileStream.on(‘open’, () => {      // readStream
		fileStream.pipe(res)               // writeStream (via .pipe method)
	})

	fileStream.on(‘error, (err) => {
		res.end(err)
		})
	})

	.listen(5000)
#
Packages & package.json

Install package.json:  run:  **npm init -y** _// used to install/store dependencies, run scripts, and identify endpoints_

_Change values in pkg.json:_

Name:

Version:  **start with “0.0.1”**

Description:

Main:

Scripts:  {  _// add your own scripts here (can be scripts from devDep for testing)_

_“start”: “node app.js”,_

_“dev”: “nodemon app.js”  // nodemon will watch your app & update as you update code_

},  _// could do same from “start”:”nodemon app.js” **  Ctrl + C  to end **_

Etc…

Install packages:  run:  **npm i [pkg]** _// adds dependencies – i.e.:  lodash(testing only); **bootstrap**; **etc.**_

Install devDep:  run:  **npm i nodemon -D** _// “-D” adds as dev-dependency in pkg.json file (i.e.: not PROD)_

**_// ? Dependencies = pkgs req by your app in prod | devDependencies = pkgs only needed for local dev & testing_**

Share code on Github _***Be sure to add a  **.ignore** file***  < add files/folders you want to ignore within .ignore >_