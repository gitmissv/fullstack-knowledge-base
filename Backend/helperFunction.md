# BASIC FUNCTION #

### FUNCTION>>>RTN RANDOM ARRAY ITEM #

// Function to return a random item from an array

	function random_item(items) {
		// Use Math.random() to generate random number btwn 0 and 1,
		// Multiply it by lenth of array; use Math.floor() to round down to nearest integer

		return items[Math.floor(Math.random() * items.length)]
	}

// Declare and initialize an array of items

	const items = ["push-ups", "pull-ups", "squats", "burpies"];


// Output result of random_item function with the array of items

	console.log(random_item(items));
  

##

// Import exercises …


	function levelOne() {
		return x
	}

	levelOne()

	function levelTwo() {
		return x
	}

	levelTwo()

	function levelThree() {
		return x
	}

	levelThree()

// export {levelOne, levelTwo, levelThree}

  
  

# FIND RANDOM #

  
	function randomNumberBetween(min, max) {
		return Math.floor(Math.random( ) * (max – min + 1) + min)
	}

	function randomSampleExercise( ) {
		return array [randomNumberBetween(0, array.length -1)]
	}

  
  

# PLUCK vs GROUPBY #

  

*Pluck* = pic one specific key from any random object:

	function pluck(array, key) {
		return array.map(element => element[key])
	}

 

*GroupBy*: taking an array & a key and grouping all of the elements in the array by that key (i.e.: all exercises in level 1):

	function groupBy(array, key) {
		return array.reduce((group, element) => {
			const keyValue = element[key]
			return { … group, [keyValue]: […(group[keyValue] ?? []), element]
			}
		{} )
	}

  

## EXAMPLE: #
 
	Const people = [
		{ name: “a”, age: 30 },
		{ name: “b”, age: 31 },
		{ name: “c”, age: 24 },
		{ name: “d”, age: 31 },
		{ name: “e”, age: 26 },
	]

	console.log(“Pluck:\n”, pluck(people, “name”))
	console.log(“Group By:\n”, groupBy(people, “age”))

  

# RESPONSES: #

  

// * IMPORTS

// * METHODS

// SUCCCESS RESPONSE

	function successfulRes({ res, status = 200, data = {} }) {
		return res.status(status).json({
			success: true,
			error: null,
			data,
		});
	}

  

// ERROR RESPONSE

	function unsuccessfulRes({
		res,
		status = 400,
		message = 'Uh oh! Something went wrong.',
		}) {
			return res.status(status).json({
			success: false,
			error: {
				status,
				message,
				},
			data: null,
		});
	}

  

// * EXPORTS

	module.exports = {
		successfulRes,
		unsuccessfulRes,
	};