# BASIC FUNCTION #

### FUNCTION>>>RTN RANDOM ITEM(S) FROM ARRAY #

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

#### ES6 VERSION #

// Arrow function to return a random item from array

	const random_item = items => items[Math.floor(Math.random() * items.length)];

// Declare and initialize an array of items

	const items = ["push-ups", "pull-ups", "squats", "burpies"];


// Output result of random_item function with the array of items

	console.log(random_item(items));


RESOURCE:  https://www.w3resource.com/javascript-exercises/javascript-array-exercise-35.php#:~:text=%2F%2F%20Arrow%20function%20to%20return,the%20array%20of%20items%20console

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


## RANDOM DATA FROM ARRAY #

### Picking random elements from an array in JS #

	const myArray = ['apple', 'banana', 'cherry', 'date', 'elderberry', 'fig', 'grape'];

	const randomElement = myArray[Math.floor(Math.random() * myArray.length)];

	console.log(randomElement)



### Get Multiple Random Elements from Array in JS #

To get multple random elements from an array:

// Use the sort() method to shuffle the array
// Use the slice() method on the shuffled array to get multiple random elements

	function getMultipleRandom(arr, num) {
		const shuffled = [...arr].sort(() => .5 - Math.random());

		return shuffled.slice(0, num);
	}

	const arr = ['apples', 'bananas', 'cantelope', 'dairy']

	console.log(getMultipleRandom(arr, 2)); // ['cantelope', 'bananas']

	console.log(getMultipleRandom(arr, 3)); // ['bananas', 'apples', 'bananas']