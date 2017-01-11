# Useful code in JavaScript


## Table of content
<a name="table-of-content"></a>
<!-- MarkdownTOC autolink=true autoanchor=true bracket=round depth=0 -->

- [Introduction](#introduction)
- [More serious introduction](#more-serious-introduction)
- [Variables](#variables)
	- [Use meaningful and pronounceable variable names](#use-meaningful-and-pronounceable-variable-names)
	- [Use ES6 constants when variable values do not change](#use-es6-constants-when-variable-values-do-not-change)
	- [Use the same vocabulary for the same type of variable](#use-the-same-vocabulary-for-the-same-type-of-variable)
	- [Use names instead of magic values](#use-names-instead-of-magic-values)
	- [Use explanatory variables](#use-explanatory-variables)
	- [Avoid Mental Mapping](#avoid-mental-mapping)
	- [Don't add unneeded context](#dont-add-unneeded-context)
	- [Simple conditional, guard clause and short-circuiting are cleaner than conditionals](#simple-conditional-guard-clause-and-short-circuiting-are-cleaner-than-conditionals)
- [Functions](#functions)
	- [Function arguments \(2 or less ideally\)](#function-arguments-2-or-less-ideally)
	- [Functions should only be one level of abstraction](#functions-should-only-be-one-level-of-abstraction)
	- [Remove duplicate code](#remove-duplicate-code)
	- [Set default objects with Object.assign](#set-default-objects-with-objectassign)
	- [Don't use flags as function parameters](#dont-use-flags-as-function-parameters)
	- [Avoid Side Effects](#avoid-side-effects)
	- [Don't write to global functions](#dont-write-to-global-functions)
	- [Favor functional programming over imperative programming](#favor-functional-programming-over-imperative-programming)
	- [Encapsulate conditionals](#encapsulate-conditionals)
	- [Avoid negative conditionals](#avoid-negative-conditionals)
	- [Avoid conditionals](#avoid-conditionals)
	- [Prefer composition over inheritance](#prefer-composition-over-inheritance)
	- [Avoid type-checking \(part 1\)](#avoid-type-checking-part-1)
	- [Don't over-optimize](#dont-over-optimize)
	- [Remove dead code](#remove-dead-code)
- [Objects and Data structures](#objects-and-data-structures)
	- [Use getters and setters](#use-getters-and-setters)
- [Classes](#classes)
	- [Single Responsibility Principle \(SRP\)](#single-responsibility-principle-srp)
	- [Open/Closed Principle \(OCP\)](#openclosed-principle-ocp)
	- [Liskov Substitution Principle \(LSP\)](#liskov-substitution-principle-lsp)
	- [Interface Segregation Principle \(ISP\)](#interface-segregation-principle-isp)
	- [Dependency Inversion Principle \(DIP\)](#dependency-inversion-principle-dip)
	- [Prefer ES6 classes over ES5 plain functions](#prefer-es6-classes-over-es5-plain-functions)
	- [Prefer composition over inheritance](#prefer-composition-over-inheritance-1)
- [Testing](#testing)
	- [Single concept per test](#single-concept-per-test)
- [Concurrency](#concurrency)
	- [Use Promises, not callbacks](#use-promises-not-callbacks)
	- [Async/Await are even cleaner than Promises](#asyncawait-are-even-cleaner-than-promises)
- [Error handling](#error-handling)
- [Formatting](#formatting)
	- [Use consistent capitalization](#use-consistent-capitalization)
	- [Function callers and callees should be close](#function-callers-and-callees-should-be-close)
- [Comments](#comments)
	- [Only comment things that have business logic complexity.](#only-comment-things-that-have-business-logic-complexity)
	- [Don't leave commented out code in your codebase](#dont-leave-commented-out-code-in-your-codebase)
	- [Don't have journal comments](#dont-have-journal-comments)
	- [Avoid positional markers](#avoid-positional-markers)

<!-- /MarkdownTOC -->

<a name="introduction"></a>
## Introduction

Programming have a lot to do with language and abstraction and not only algorithms and technologies. It requires to step back often to see the big pictures and rethink on the complete system and not only about the part that we are currently doing.

Paradoxically, programmers, we  are one of the most lazy guys of the world, we often make the mistake of thinking that is better to have a "beautiful" code than a useful one. Or that is better to ignore corner cases for maintaining the simplicity of the system, all for not taking the time for apply this refactor pattern of what we always speak.

But don't worry! There is a solution for that! And is very simply to apply. Lets do it on the Russian style. Every time you are lazy one big Russian guy will comes and slaps you in the face. And remember, is Russian, it will hurt.

<a name="more-serious-introduction"></a>
## More serious introduction

With Russian guy or not, when a code grows becomes impossible to maintain it in the head. Having ad-hoc conventions not defined is something only feasible when doing scripting and not when programming seriously. I read that a good metric for knowing if a code is goo is the WTFs/minute. Lets assume that our code don't have any WTF and is clean and easy to read, still we can do a lot of mistakes that are going to betray us when try to make the code grow.

With this guide I explain some points that I think people usually do incorrectly in big projects. Mainly because they don't realize the responsibility of writing code that will work with thousands of lines of code more and therefore they apply some scripting tactics. Obviously this is my experience and I don't think is perfect or close to it, but it can helps to people that is not used to make projects of more than some thousands of lines of code. All points are explained and have the why, that means, I explain every point. Therefore it should be easy to know is that applies to your project or not.

Anyway, if you don't agree with me, let me know in a pull request, explaining why you think that you have a better answer.

My base for this rules is [this repository](https://github.com/ryanmcdermott/clean-code-javascript), it has some rules that I think are wrong and not suitable for big projects.

*Note: In this document I define scripting as a style that is more suitable for smalls projects, with a lot of ad-hoc conventions meanwhile I define programming as the style and group of tactics that give the code the possibility to grow and to make architecture changes.*

<a name="variables"></a>
## Variables

<a name="use-meaningful-and-pronounceable-variable-names"></a>
### Use meaningful and pronounceable variable names

I don't think that can have discussion, but still I think it should have some clarifications.

First, if the variable name can be pronounced, better. Let's use the language memory. I mean, we are training that during all our life, why not to use it?

**Bad:**
```javascript
let ids = arr.map(e => e.getId());
```

**Good**:
```javascript
let userIds = users.map(user => user.getId());
```
**[⬆ back to top](#table-of-contents)**

<a name="use-es6-constants-when-variable-values-do-not-change"></a>
### Use ES6 constants when variable values do not change
In the bad example, the variable can be changed. When you declare a constant, the variable should stay the same throughout the program.

**Bad:**
```javascript
var FIRST_US_PRESIDENT = "George Washington";
```

**Good**:
```javascript
const FIRST_US_PRESIDENT = "George Washington";
```
**[⬆ back to top](#table-of-contents)**

<a name="use-the-same-vocabulary-for-the-same-type-of-variable"></a>
### Use the same vocabulary for the same type of variable

It will help you to not question if the correct function is getUser or getClient. I saw databases where the name if the ID of the same logic item (a location) is different in every table. You don't want to work with that database.

**Bad:**
```javascript
getUserInfo();
getClientData();
getCustomerRecord();
```

**Good**:
```javascript
getUser();
```
**[⬆ back to top](#table-of-contents)**

<a name="use-names-instead-of-magic-values"></a>
### Use names instead of magic values
We will read more code than we will ever write. It's important that the code we do write is readable and searchable. By *not* naming variables that end up being meaningful for understanding our program, we hurt our readers. Make your names searchable.

**Bad:**
```javascript
// What the heck is 31536000000?
setInterval(() => runCronJob(), 31536000000);
```

**Good**:
```javascript
// Declare them as capitalized `const` globals.
const YEAR_MILISECONDS = 31536000000;

setInterval(() => runCronJob(), YEAR_MILISECONDS);

```

You can be tented to not do it in some case like this:

**Bad:**
```javascript
socket.timeout = 20000;
```

But still is good to have it in a variable. It makes the file more configurable(without reading all the code) and makes the value reusable.

**Good**:
```javascript
const CLIENT_DISCONNECT_TIMEOUT = HEARTBEAT_TIME * 3;
...
socket.timeout = CLIENT_DISCONNECT_TIMEOUT;
```

**[⬆ back to top](#table-of-contents)**

<a name="use-explanatory-variables"></a>
### Use explanatory variables

When we create long statements with several operations in it becomes difficult to follow what is happening there without stop to it. Only putting some variables in the middle can provide us the contextual information to not need to decipher what is happening.

**Bad:**
```javascript
const cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;
saveCityState(cityStateRegex.match(cityStateRegex)[1], cityStateRegex.match(cityStateRegex)[2]);
```

**Good**:
```javascript
const cityStateRegex = /^(.+)[,\\s]+(.+?)\s*(\d{5})?$/;

const match = cityStateRegex.match(cityStateRegex);
const city = match[1];
const state = match[2];

saveCityState(city, state);
```
**[⬆ back to top](#table-of-contents)**

<a name="avoid-mental-mapping"></a>
### Avoid Mental Mapping
This is basically the same as the [first point](#use-meaningful-and-pronounceable-variable-names)

**Bad:**
```javascript
var locations = ['Austin', 'New York', 'San Francisco'];

locations.forEach((l) => {
	doStuff();
	doSomeOtherStuff();

	...

	// Wait, what is `l` for again?
	dispatch(l);
});
```

**Good**:
```javascript
var locations = ['Austin', 'New York', 'San Francisco'];

locations.forEach((location) => {
	doStuff();
	doSomeOtherStuff();
	...

	dispatch(location);
});
```
**[⬆ back to top](#table-of-contents)**

<a name="dont-add-unneeded-context"></a>
### Don't add unneeded context
If your class/object name tells you something, don't repeat that in your variable name.

**Bad:**
```javascript
var Car = {
	carMake: 'Honda',
	carModel: 'Accord',
	carColor: 'Blue'
};

function paintCar(car) {
	car.carColor = 'Red';
}
```

**Good**:
```javascript
var Car = {
	make: 'Honda',
	model: 'Accord',
	color: 'Blue'
};

function paintCar(car) {
	car.color = 'Red';
}
```

The same is applied to Classes and methods.

**Bad:**
```javascript
class Car {
	starCar() { ... };
	stopCar() { ... };
}

const car = new Car();

car.starCar();
car.stopCar();
```

**Good:**
```javascript
class Car {
	star() { ... };
	stop() { ... };
}

const car = new Car();

car.star();
car.stop();
```

**[⬆ back to top](#table-of-contents)**

<a name="simple-conditional-guard-clause-and-short-circuiting-are-cleaner-than-conditionals"></a>
### Simple conditional, guard clause and short-circuiting are cleaner than conditionals

`if else if else else` is hard to read and understand, better use other tactics that avoid this complexity.

- short-circuiting allows to have in one line the variable and the default value. **But! If you are going to use it, maybe is better to use [ES6 default values](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)**.
- simple conditional makes cleaner the code and is read like a correction over the normal behavior instead of a complex logic. And makes explicit what is a normal behavior and and what not.
- guard clause simplifies the logic when we want to execute the default behavior only in some cases.

**Bad:**
```javascript
function createMicrobrewery(name) {
	var breweryName;
	if (name) {
		breweryName = name;
	} else {
		breweryName = 'Hipster Brew Co.';
	}

	...
}
```

**Good (short-circuiting)**:
```javascript
function createMicrobrewery(name) {
	var breweryName = name || 'Hipster Brew Co.'

	...
}
```

**Good (default values better than short-circuiting)**:
```javascript
function createMicrobrewery(name = 'Hipster Brew Co.') {
	var breweryName = name;
	...
}
```

**Good (simple conditional)**:
```javascript
function createMicrobrewery(name) {
	var breweryName = name;

	if(!name)
		breweryName = 'Hipster Brew Co.';

	...
}
```

**Good (guard clause)**:
```javascript
function createMicrobrewery(name) {
	if(!name) return;

	var breweryName = name;
	...
}
```

You can find other example of guard clause from Martin Fowler [here](https://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html).

**[⬆ back to top](#table-of-contents)**

<a name="function-arguments-2-or-less-ideally"></a>

<a name="functions"></a>
## Functions
<a name="function-arguments-2-or-less-ideally"></a>
### Function arguments (2 or less ideally)

Having a function with many arguments is a smell that indicated that maybe you need some refactoring for avoiding all this arguments. Moreover makes harder to test (more combinations for input) and to work with optional parameters. Some patterns that you can apply in order of preference are:

- **Simply split the function in several function**: If your function have to many arguments maybe that means that you can split its logic in several functions.
- **Builder pattern**: Can help you when you need to pass a lot of optional arguments for constructing something (in the constructor or similar entity)
- **Define a model or data class**: That will group your data in a object. Having it defined as a Class will make the convention explicit and easy to read in the future.

Thing that you must **NOT** do:

- Making the function to receive only one argument expecting to be an object without any type and assuming some properties inside of that object (understanding "any type" as not model or data class forcing the developer to create a ad-hod object for passing several parameters to the function). This will force the developer to read the code of the function for knowing what your function requires. This is simple not acceptable and will bring you a lot of pain and a not very friendly big [Russian guy](#introduction). If you do that I hope you love the smell of napal in the morning when you have 20 calls to this function from several parts of the code base giving totally different objects as argument.

**Bad (builder pattern):**
```javascript
function createMenu(title, body, buttonText, cancellable) {
	...
}

//Without watching the function definition, what is every parameter?
const menu = createMenu('Foo', 'body', 'Baz', true);
```

**Good (builder pattern):**:

All parameters can be optional. That allows you to receive several parameters and at the same time protects you from misusing the function by other developers.

```javascript
const menu = MenuBuilder
.title('Foo')
.body('body')
.buttonText('Baz')
.cancellable(true);

```

**Bad (function split):**
```javascript
showMenu(menu, POSITION_X, POSITION_Y, PARENT, IS_DRAGABLE);
```


**Good (function split):**:

I show this with functions for simplicity, but is the same with classes methods. Split the method in several methods.

```javascript
setDragable(menu);
setPosition(menu, POSITION_X, POSITION_Y);
setDragable(menu, IS_DRAGABLE);
setParent(menu, PARENT);
showMenu(menu);

```

**Bad (define class object):**
```javascript
function createMenu(title, body, buttonText, cancellable) {
	...
}

//Without watching the function definition, what is every parameter?
const menu = createMenu('Foo', 'body', 'Baz', true);
```

**Good (define class object):**
I applied the builder for making the menuConfig object. And I added a JSDocs comment for declaring in the function what type I'm expecting.

```javascript
/*
@param menuConfig MenuConfig
*/
function createMenu(menuConfig) {
	...
}

const menuConfig = MenuConfig()
.title('Foo')
.body('body')
.buttonText('Baz')
.cancellable(true);

createMenu(menuConfig);
```

**[⬆ back to top](#table-of-contents)**

<a name="functions-should-only-be-one-level-of-abstraction"></a>
### Functions should only be one level of abstraction
When you have more than one level of abstraction your function is usually doing too much. Splitting up functions leads to reusability and easier testing.

I really advice to step back and do some little refactors regularly for extracting logic from functions. I tried to modify a function of 200 lines and 13 indentation levels and I needed to expend 2 days first refactoring it (and no, is not fun).

**Bad:**
```javascript
function create() {
	const stars = [];

	for (let i = 0; i < STARS_QUANTITY; i++){
		const star = new Star();

		const x = Math.random() * this.width;
		const y = Math.random() * this.eight;

		const position = new Position(x, y);

		const name = Math.random().toString(36).substring(7);

		star.setPosition(position);
		star.setName(name);
		
		stars.push(star);
	}
}
```

**Good**:
```javascript
	function randomName() {
		return Math.random().toString(36).substring(7);
	}

	function randomPosition() {
		const x = Math.random() * this.width;
		const y = Math.random() * this.eight;
		return new Position(x, y);
	}

	function createStar() {
		const star = new Star();

		const position = this.randomPosition();
		const name = this.randomName();

		star.setPosition(position);
		star.setName(name);

		return star;
	}

	function create() {
		const stars = [];

		for (let i = 0; i < STARS_QUANTITY; i++){
			let star = this.createStar();
			
			stars.push(star);
		}

		return stars;
	}
```
**[⬆ back to top](#table-of-contents)**

<a name="remove-duplicate-code"></a>
### Remove duplicate code
Never ever, ever, under any circumstance, have duplicate code. It ends with several parts of the code with different versions of the same logic that is altered by different developers that forget to update the other duplicates. And that, my friend, is not something that you want. Extract the common logic in a function that other functions can use.

**Bad:**
```javascript
function showDeveloperList(developers) {
	developers.forEach(developer => {
		var expectedSalary = developer.calculateExpectedSalary();
		var experience = developer.getExperience();
		var githubLink = developer.getGithubLink();

		const worker = new WorkerFactory();
		worker.setExpectedSalary(expectedSalary);
		worker.setExperience(experience);
		worker.setGithubLink(githubLink);

		render(worker);
	});
}

function showManagerList(managers) {
	managers.forEach(manager => {
		var expectedSalary = manager.calculateExpectedSalary();
		var experience = manager.getExperience();
		var portfolio = manager.getMBAProjects();

		const worker = new WorkerFactory();
		worker.setExpectedSalary(expectedSalary)
		worker.setExperience(experience)
		worker.setPortfolio(portfolio);

		render(worker);
	});
}
```

**Good**:
```javascript
getWorker(type){
	const expectedSalary = manager.calculateExpectedSalary();
	const experience = manager.getExperience();

	const worker = new WorkerFactory();
	worker.setExpectedSalary(expectedSalary);
	worker.setExperience(experience);

	if(type === WORKER_TYPE_DEVELOPER){
		let githubLink = developer.getGithubLink();
		worker.setGithubLink(githubLink);
	}

	if(type === WORKER_TYPE_MANAGER){
		let portfolio = manager.getMBAProjects();
		worker.setPortfolio(portfolio);
	}
	
	return worker;
}

function showDeveloperList(developers) {
	developers.forEach(developer => {
		const worker = getWorker(WORKER_TYPE_DEVELOPER);
		render(worker.getRaw());
	});
}

function showDeveloperList(developers) {
	developers.forEach(developer => {
		const worker = getWorker(WORKER_TYPE_MANAGER);
		render(worker.getRaw());
	});
}
```
**[⬆ back to top](#table-of-contents)**

<a name="set-default-objects-with-objectassign"></a>
### Set default objects with Object.assign

It create a new Object with the attributes of the first one and overwrite them with the attributes of the second one. [Read about it](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign).

**Bad:**
```javascript
function createMenu(config) {
	config.title = config.title || DEFAULT_CONFIG.title;
	config.body = config.body || DEFAULT_CONFIG.body;
	config.buttonText = config.buttonText || DEFAULT_CONFIG.buttonText;
	config.cancellable = config.cancellable === DEFAULT_CONFIG.cancellable ? config.cancellable : !defaultConfig.cancellable;
}

//Lets assume that this is loaded from a JSON file. Because as we already saw, ad-hod objects are bad.
const menuConfig = {
	title: null,
	body: 'Bar',
	buttonText: null,
	cancellable: true
}

createMenu(menuConfig);
```

**Good**:
```javascript
function createMenu(config) {
	config = Object.assign(DEFAULT_CONFIG, config);
}

//Lets assume that this is loaded from a JSON file. Because as we already saw, ad-hod objects are bad.
const menuConfig = {
	title: 'Order',
	// User did not include 'body' key
	buttonText: 'Send',
	cancellable: true
}

createMenu(menuConfig);
```
**[⬆ back to top](#table-of-contents)**

<a name="dont-use-flags-as-function-parameters"></a>
### Don't use flags as function parameters
Flags tell your user that this function does more than one thing. Functions should do one thing. Split out your functions if they are following different code paths based on a boolean. Moreover, remember to extract the common logic between both function for not ending having code duplication.

**Bad:**
```javascript
function createFile(name, temp) {
	if (temp) {
		fs.create('./temp/' + name);
	} else {
		fs.create(name);
	}
}
```

**Good**:
```javascript
function createTempFile(name) {
	fs.create('./temp/' + name);
}

function createFile(name) {
	fs.create(name);
}
```
**[⬆ back to top](#table-of-contents)**

<a name="avoid-side-effects"></a>
### Avoid Side Effects
A function produces a side effect if it does anything other than take a value in and return another value or values. A side effect could be writing to a file, modifying some global variable, or accidentally wiring all your money to a Russian guy.

Now, you do need to have side effects in a program in some occasions. Like the previous example, you might need to write to a file. What you want to do is to centralize where you are doing this. Don't have several functions and classes that write to a particular file. Have one service that does it. One and only one.

The main point is to avoid common pitfalls like sharing state between objects without any structure, using mutable data types that can be written to by anything, and not centralizing where your side effects occur. This is very related with [no code duplication](remove-duplicate-code).

**Bad:**
```javascript
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
var name = 'Ryan McDermott';

function splitIntoFirstAndLastName() {
	name = name.split(' ');
}

splitIntoFirstAndLastName();

console.log(name); // ['Ryan', 'McDermott'];
```

**Good**:
```javascript
function splitIntoFirstAndLastName(name) {
	return name.split(' ');
}

var name = 'Ryan McDermott'
var newName = splitIntoFirstAndLastName(name);

console.log(name); // 'Ryan McDermott';
console.log(newName); // ['Ryan', 'McDermott'];
```
**[⬆ back to top](#table-of-contents)**

<a name="dont-write-to-global-functions"></a>
### Don't write to global functions
Polluting globals is a bad practice in JavaScript because you could clash with another library and the user of your API would be none-the-wiser until they get an exception in production. Let's think about an example: what if you wanted to extend JavaScript's native Array method to have a `diff` method that could show the difference between two arrays? You could write your new function to the `Array.prototype`, but it could clash with another library that tried to do the same thing. What if that other library was just using `diff` to find the difference between the first and last elements of an array? This is why it would be much better to just use ES6 classes and simply extend the `Array` global.

**Bad:**
```javascript
Array.prototype.diff = function(comparisonArray) {
	var values = [];
	var hash = {};

	for (var i of comparisonArray) {
		hash[i] = true;
	}

	for (var i of this) {
		if (!hash[i]) {
			values.push(i);
		}
	}

	return values;
}
```

**Good:**
```javascript
class SuperArray extends Array {
	constructor(...args) {
		super(...args);
	}

	diff(comparisonArray) {
		var values = [];
		var hash = {};

		for (var i of comparisonArray) {
			hash[i] = true;
		}

		for (var i of this) {
			if (!hash[i]) {
				values.push(i);
			}
		}

		return values;
	}
}
```
**[⬆ back to top](#table-of-contents)**

<a name="favor-functional-programming-over-imperative-programming"></a>
### Favor functional programming over imperative programming
Functional programming is a complex topic, but the little ads that JavaScript includes of it will help you to have better code. Keep in mind that it requires a little change on the thinking way. Doing it "a la functional" will help you to automatically apply some rules in this document ([Like no side effects](avoid-side-effects)).

**Bad:**
```javascript
const programmerOutput = [
	{
		name: 'Uncle Bobby',
		linesOfCode: 500
	}, {
		name: 'Suzie Q',
		linesOfCode: 1500
	},
	//etc
];

var totalOutput = 0;

for (var i = 0; i < programmerOutput.length; i++) {
	totalOutput += programmerOutput[i].linesOfCode;
}
```

**Good**:
```javascript
const programmerOutput = [
	{
		name: 'Uncle Bobby',
		linesOfCode: 500
	}, {
		name: 'Suzie Q',
		linesOfCode: 1500
	},
	//etc
];

var totalOutput = programmerOutput
.map((programmer) => programmer.linesOfCode)
.reduce((acc, linesOfCode) => acc + linesOfCode, 0);
```
**[⬆ back to top](#table-of-contents)**

<a name="encapsulate-conditionals"></a>
### Encapsulate conditionals

**Bad:**
```javascript
if (fsm.state === 'fetching' && isEmpty(listNode)) {
	/// ...
}
```

**Good (if the conditional is used only in the function)**:
```javascript
const shouldShowSpinner = fsm.state === 'fetching' && isEmpty(listNode);
if (shouldShowSpinner) {
	/// ...
}
```

**Good (if the same conditional is shared between functions)**:
Remember, [no code duplication](remove-duplicate-code).

```javascript
function shouldShowSpinner(fsm, listNode) {
  return fsm.state === 'fetching' && isEmpty(listNode);
}

if (shouldShowSpinner(fsmInstance, listNodeInstance)) {

}
```
**[⬆ back to top](#table-of-contents)**

<a name="avoid-negative-conditionals"></a>
### Avoid negative conditionals

**Bad:**
```javascript
function isDOMNodePresent(node) {
	// ...
}

if (!isDOMNodePresent(node)) {
	// ...
}
```

**Good**:
```javascript
function isDOMNodeMissing(node) {
	// ...
}

if (isDOMNodeMissing(node)) {
	// ...
}
```
**[⬆ back to top](#table-of-contents)**

<a name="avoid-conditionals"></a>
### Avoid conditionals
This seems like an impossible task. Upon first hearing this, most people say, "how am I supposed to do anything without an `if` statement?" The answer is that you can use composition to achieve the same task in many cases. The second question is usually, "well that's great but why would I want to do that?" The answer is a previous clean code concept we learned: a function should only do one thing. When you have classes and functions that have `if` statements, you are telling your user that your function does more than one thing. Remember,
just do one thing.

**Bad:**
```javascript
class Airplane {
	//...
	getCruisingAltitude() {
		switch (this.type) {
			case AIRPLANE_TYPE.['777']:
				return getMaxAltitude() - getPassengerCount();

			case AIRPLANE_TYPE.AIR_FORCE_ONE:
				return getMaxAltitude();

			case AIRPLANE_TYPE.CESSNA:
				return getMaxAltitude() - getFuelExpenditure();
		}
	}
}
```

**Good**:
```javascript
class Airplane {
	constructor(altitudeCalculator){
		//altitudeCalculator is give to the Airplane in the construction phase. That means that you need a AitplaneFactory for selecting the correct altitudeCalculator. See next section.
		this.altitudeCalculator = altitudeCalculator;
	}

	getCruisingAltitude() {
		this.altitudeCalculator.get();
	}
}
```
**[⬆ back to top](#table-of-contents)**


<a name="prefer-composition-over-inheritance"></a>
### Prefer composition over inheritance

Inheritance and composition are totally different direction when building the logic. In inheritance is the children who say what logic is going to maintain and to overwrite from the "logic pool" that is the father. In composition is the father that receive some worker children(yeah, I know), that he don't know who they are, and he command them to do the "main logic". The childrens will take care of the details. 

That means that is you want to update some minor logic, just exchange the children for others (Yeah, it sounds horrible). Very good for testing with mock-ups. For example, in conjunction with a Dependency Injector and following the inverse dependency principle from SOLID allows to have change my amqplib dependency by a simple mock, removing RabbitMQ as a external dependency.

**Bad**:
```javascript
class Airplane {
  //...
}

class Boeing777 extends Airplane {
  //...
  getCruisingAltitude() {
	return getMaxAltitude() - getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  //...
  getCruisingAltitude() {
	return getMaxAltitude();
  }
}

class Cessna extends Airplane {
  //...
  getCruisingAltitude() {
	return getMaxAltitude() - getFuelExpenditure();
  }
}
```

**Good**:
```javascript
//a function, a require, a list, etc. Just the association with type and the logic.
AltitudeCalculators = loadAltitudeCalculators();

class AirplaneFactory() {
	static create(type) {
		if(!AltitudeCalculators[type])
			throw new Error('No airplane of type ' + type);
		
		altitudeCalculator = AltitudeCalculators[type];

		return new Airplane(type, altitudeCalculator);
	}
}

class Airplane {
	constructor(type, altitudeCalculator){
		//altitudeCalculator is give to the Airplane in the construction phase. That means that you need a AitplaneFactory for selecting the correct altitudeCalculator
		this.altitudeCalculator = altitudeCalculator;
	}
	getCruisingAltitude() {
		this.altitudeCalculator.get();
	}
}

const airplane = AirplaneFactory.create(AIRPLANE_TYPE.CESSNA);
```

<a name="avoid-type-checking-part-1"></a>
### Avoid type-checking (part 1)
JavaScript is untyped, which means your functions can take any type of argument. Sometimes you are bitten by this freedom and it becomes tempting to do type-checking in your functions. There are many ways to avoid having to do this. The first thing to consider is consistent APIs.

**Bad:**
```javascript
function travelToTexas(vehicle) {
	const location = new Location(TEXAS_LOCATION);

	if (vehicle instanceof Bicycle)
		vehicle.peddle(this.currentLocation, location);
	else if (vehicle instanceof Car)
		vehicle.drive(this.currentLocation, location);
}
```

**Good**:
```javascript
function travelToTexas(vehicle) {
	const location = new Location('texas');

	vehicle.move(this.currentLocation, location);
}
```

**NOTE**: If you are working with basic primitive values like strings, integers, and arrays, and you can't get over the multi-type functions, you can try TypeScript. It is an excellent alternative to normal JavaScript, as it provides you with static typing on top of standard JavaScript syntax. 

If not, keep your JavaScript, clean, write good tests, and have good code reviews. Provably there you will find the way to have function that only need to accept one type.

**[⬆ back to top](#table-of-contents)**

<a name="dont-over-optimize"></a>
### Don't over-optimize
Modern browsers do a lot of optimization under-the-hood at runtime. A lot of times, if you are optimizing then you are just wasting your time. Trust only the profiling tools after the implementation. Only then you will know where to use your time better.

**Bad:**
```javascript

// On old browsers, each iteration would be costly because `len` would be
// recomputed. In modern browsers, this is optimized.
for (var i = 0, len = list.length; i < len; i++) {
  // ...
}
```

**Good**:
```javascript
for (var i = 0; i < list.length; i++) {
  // ...
}
```
**[⬆ back to top](#table-of-contents)**

<a name="remove-dead-code"></a>
### Remove dead code
Dead code is 99% as bad as duplicate code. There's no reason to keep it in your codebase. If it's not being called, get rid of it! It will still be safe in your version history if you still need it. Because you always use a version control system, right?

Sorry, not examples this time. Just delete code that is not used. 
**[⬆ back to top](#table-of-contents)**
<a name="objects-and-data-structures"></a>
## Objects and Data structures

<a name="use-getters-and-setters"></a>
### Use getters and setters
JavaScript doesn't have interfaces or types so it is very hard to enforce this pattern, because we don't have keywords like `public` and `private`. As it is, using getters and setters to access data on objects is far better than simply looking for a property on an object. "Why?" you might ask. Well, here's an unorganized list of reasons why:

1. When you want to do more beyond getting an object property, you don't have to look up and change every accessor in your codebase.
2. Makes adding validation simple when doing a `set`.
3. Encapsulates the internal representation.
4. Easy to add logging and error handling when getting and setting.
6. You can lazy load your object's properties, let's say getting it from a server.


**Bad:**
```javascript
class BankAccount {
  constructor() {
	   this.balance = 1000;
  }
}

let bankAccount = new BankAccount();

// Buy shoes...
bankAccount.balance = bankAccount.balance - 100;
```

**Good**:
```javascript
class BankAccount {
  constructor() {
	   this.balance = 1000;
  }

  // It doesn't have to be prefixed with `get` or `set` to be a getter/setter
  withdraw(amount) {
  	if (verifyAmountCanBeDeducted(amount)) {
  	  this.balance -= amount;
  	}
  }
}

let bankAccount = new BankAccount();

// Buy shoes...
bankAccount.withdraw(100);
```
**[⬆ back to top](#table-of-contents)**

<a name="classes"></a>
## Classes

<a name="single-responsibility-principle-srp"></a>
### Single Responsibility Principle (SRP)
As stated in Clean Code, "There should never be more than one reason for a class to change". It's tempting to jam-pack a class with a lot of functionality, like when you can only take one suitcase on your flight. The issue with this is that your class won't be conceptually cohesive and it will give it many reasons to change. Minimizing the amount of times you need to change a class is important. It's important because if too much functionality is in one class and you modify a piece of it, it can be difficult to understand how that will affect other dependent modules in your codebase.

**Bad:**
```javascript
class UserSettings {
	constructor(user) {
		this.user = user;
	}

	changeSettings(settings) {
		if (this.verifyCredentials(user)) {
		// ...
		}
	}

	verifyCredentials(user) {
		// ...
	}
}
```

**Good**:
```javascript
class UserAuth {
	constructor(user) {
		this.user = user;
	}

	verifyCredentials() {
		// ...
	}
}


class UserSettings {
	//userAuth is an instance of UserAuth.
	constructor(user, userAuth) {
		this.user = user;
		this.auth = userAuth;
	}

	changeSettings(settings) {
		if (this.auth.verifyCredentials()) {
		// ...
		}
	}
}
```
**[⬆ back to top](#table-of-contents)**

<a name="openclosed-principle-ocp"></a>
### Open/Closed Principle (OCP)
As stated by Bertrand Meyer, "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification." What does that mean though? This principle basically states that you should allow users to extend the functionality of your module without having to open up the `.js` source code file and manually manipulate it. Moreover, pattern like command pattern can help you to have systems that are extensible.

**Bad:**
```javascript
class AjaxRequester {
	constructor() {
		// What if we wanted another HTTP Method, like DELETE? We would have to
		// open this file up and modify this and put it in manually.
		this.HTTP_METHODS = ['POST', 'PUT', 'GET'];
	}

	get(url) {

	}

}
```

**Good**:
```javascript
class AjaxRequester {
	constructor() {
		this.HTTP_METHODS = ['POST', 'PUT', 'GET'];
	}

	get(url) {
		// ...
	}

	addHTTPMethod(method) {
		this.HTTP_METHODS.push(method);
	}
}
```
**[⬆ back to top](#table-of-contents)**

<a name="liskov-substitution-principle-lsp"></a>
### Liskov Substitution Principle (LSP)
This is a scary term for a very simple concept. It's formally defined as "If S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e., objects of type S may substitute objects of type T) without altering any of the desirable properties of that program (correctness, task performed, etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class, then the base class and child class can be used interchangeably without getting incorrect results. This might still be confusing, so let's take a look at the classic Square-Rectangle example. Mathematically, a square is a rectangle, but if you model it using the "is-a" relationship via inheritance, you quickly get into trouble.

**Bad:**
```javascript
class Rectangle {
	constructor() {
		this.width = 0;
		this.height = 0;
	}

	setColor(color) {

	}

	render(area) {

	}

	setWidth(width) {
		this.width = width;
	}

	setHeight(height) {
		this.height = height;
	}

	getArea() {
		return this.width * this.height;
	}
}

class Square extends Rectangle {
	constructor() {
		super();
	}

	setWidth(width) {
		this.width = width;
		this.height = width;
	}

	setHeight(height) {
		this.width = height;
		this.height = height;
	}
}

function renderLargeRectangles(rectangles) {
	rectangles.forEach((rectangle) => {
		rectangle.setWidth(4);
		rectangle.setHeight(5);
		let area = rectangle.getArea(); // BAD: Will return 25 for Square. Should be 20.
		rectangle.render(area);
	})
}

let rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles(rectangles);
```

**Good**:
```javascript
class Shape {
	constructor() {}

	setColor(color) {

	}

	render(area) {

	}
}

class Rectangle extends Shape {
	constructor() {
		super();
		this.width = 0;
		this.height = 0;
	}

	setWidth(width) {
		this.width = width;
	}

	setHeight(height) {
		this.height = height;
	}

	getArea() {
		return this.width * this.height;
	}
}

class Square extends Shape {
	constructor() {
		super();
		this.length = 0;
	}

	setLength(length) {
		this.length = length;
	}

	getArea() {
		return this.length * this.length;
	}
}
/** This is a very very short and simple command pattern. Well, at least the most basic idea of a command pattern. See the note after the code.*/
function renderLargeShapes(shapes) {
	shapes.forEach((shape) => {
		const commands = getShapeCommands(shape);
		executeShapeCommands(commands, shape);
	})
}

getShapeCommands(shape){
	return shapesCommands.filter(command => command.test(shape));
}

executeShapeCommands(commands, shape){
	commands.forEach(command => command.exec(shape));
}

const shapesCommands = [
	{
		test: shape => shape instanceof Square,
		exec: shape => {
			shape.setLength(5);
		}
	},
	{
		test: shape => shape instanceof Square,
		exec: shape => {
			shape.setWidth(4);
			shape.setHeight(5);
		}
	}
];
/** End of the command pattern*/

let shapes = [new Rectangle(), new Rectangle(), new Square()];
renderLargeShapes(shapes);
```
**NOTE**: I implemented a super simple command pattern for this example. Usually this should be a Class and have a method "register" for adding new commands ([Open/Close principle](openclosed-principle-ocp)).

**[⬆ back to top](#table-of-contents)**

<a name="interface-segregation-principle-isp"></a>
### Interface Segregation Principle (ISP)
JavaScript doesn't have interfaces so this principle doesn't apply as strictly as others. However, it's important and relevant even with JavaScript's lack of type system.

ISP states that "Clients should not be forced to depend upon interfaces that they do not use." Interfaces are implemented as contracts in JavaScript with Builder patterns, models, and other tactics because of duck typing.

A good example to look at that demonstrates this principle in JavaScript is for classes that require large settings objects. Not requiring clients to setup huge amounts of options is beneficial, because most of the time they won't need all of the settings. Making them optional helps prevent having a "fat interface".

**Bad:**
```javascript
class DOMTraverser {
	constructor(rootNode, animationModule) {
		this.rootNode = rootNode;
		this.animationModule = animationModule;
	}

	traverse() {

	}
}

const rootNode = document.getElementsByTagName('body');
const animationModule = function() {}; // Most of the time, we won't need to animate when traversing.

const $ = new DOMTraverser(rootNode, animationModule);

```

**Good**:

In this example we use the short-circuiting way for having a optional parameter. We can use a simple conditional, a Builder pattern, create a method called "setAnimationModule" or something like a callback "onTraverse" that set a callback that executes the module.

```javascript
const DEFAULT_ANIMATION_MODULE = function () {};

class DOMTraverser {
	constructor(rootNode, animationModule) {
		this.rootNode = rootNode;
		this.animationModule = animationModule || DEFAULT_ANIMATION_MODULE;
	}

	traverse() {
		
	}
}

const rootNode = document.getElementsByTagName('body');

const $ = new DOMTraverser(rootNode, animationModule);
```
**[⬆ back to top](#table-of-contents)**

<a name="dependency-inversion-principle-dip"></a>
### Dependency Inversion Principle (DIP)
This principle states two essential things:

1. High-level modules should not depend on low-level modules. Both should depend on abstractions.
2. Abstractions should not depend upon details. Details should depend on abstractions.

This can be hard to understand at first, but if you've worked with Angular.js, you've seen an implementation of this principle in the form of Dependency Injection (DI). While they are not identical concepts, DIP keeps high-level modules from knowing the details of its low-level modules and setting them up. It can accomplish this through DI. A huge benefit of this is that it reduces the coupling between modules. Coupling is a very bad development pattern because it makes your code hard to refactor/update/extend.

As stated previously, JavaScript doesn't have interfaces so the abstractions that are depended upon are implicit contracts. That is to say, the methods and properties that an object/class exposes to another object/class. In the example below, the implicit contract is that any Request module for an `InventoryTracker` will have a `requestItems` method.

**Bad:**
```javascript
class InventoryTracker {
	constructor(items) {
		this.items = items;

		// BAD: We have created a dependency on a specific request implementation.
		// We should just have requestItems depend on a request method: `request`
		this.requester = new InventoryRequester();
	}

	//Returns a promise because the InventoryRequester is a http that is async.
	requestItems() {
		const pendingItems = this.items.map(item => this.requester.request(item));
		return Promise.all(pendingItems);
	}
}

class InventoryRequester {
	constructor() {
		this.REQ_METHODS = ['HTTP'];
	}

	request(item) {
		// ...
	}
}

let inventoryTracker = new InventoryTracker(['apples', 'bananas']);
inventoryTracker.requestItems();
```

**Good**:
```javascript
class InventoryTracker {
	constructor(items, requester) {
		this.items = items;
		this.requester = requester;
	}

	requestItems() {
		const pendingItems = this.items.map(item => this.requester.request(item));
		return Promise.all(pendingItems);
	}
}

class InventoryRequesterV1 {
	constructor() {
		this.REQ_METHODS = ['HTTP'];
	}

	request(item) {

	}
}

class InventoryRequesterV2 {
	constructor() {
		this.REQ_METHODS = ['WS'];
	}

	request(item) {

	}
}

// By constructing our dependencies externally and injecting them, we can easily
// substitute our request module for a fancy new one that uses WebSockets
let inventoryTracker = new InventoryTracker(['apples', 'bananas'], new InventoryRequesterV2());
inventoryTracker.requestItems();
```
**[⬆ back to top](#table-of-contents)**

<a name="prefer-es6-classes-over-es5-plain-functions"></a>
### Prefer ES6 classes over ES5 plain functions
It's very difficult to get readable class inheritance, construction, and method definitions for classical ES5 classes. If you need inheritance (and be aware that provably not), then prefer classes. However, prefer small functions over classes until you find yourself needing larger and more complex objects.

**Bad:**
```javascript
var Animal = function(age) {
	if (!(this instanceof Animal)) {
		throw new Error("Instantiate Animal with `new`");
	}

	this.age = age;
};

Animal.prototype.move = function() {};

var Mammal = function(age, furColor) {
	if (!(this instanceof Mammal)) {
		throw new Error("Instantiate Mammal with `new`");
	}

	Animal.call(this, age);
	this.furColor = furColor;
};

Mammal.prototype = Object.create(Animal.prototype);
Mammal.prototype.constructor = Mammal;
Mammal.prototype.liveBirth = function() {};

var Human = function(age, furColor, languageSpoken) {
	if (!(this instanceof Human)) {
		throw new Error("Instantiate Human with `new`");
	}

	Mammal.call(this, age, furColor);
	this.languageSpoken = languageSpoken;
};

Human.prototype = Object.create(Mammal.prototype);
Human.prototype.constructor = Human;
Human.prototype.speak = function() {};
```

**Good:**
```javascript
class Animal {
	constructor(age) {
		this.age = age;
	}

	move() {}
}

class Mammal extends Animal {
	constructor(age, furColor) {
		super(age);
		this.furColor = furColor;
	}

	liveBirth() {}
}

class Human extends Mammal {
	constructor(age, furColor, languageSpoken) {
		super(age, furColor);
		this.languageSpoken = languageSpoken;
	}

	speak() {}
}
```
**[⬆ back to top](#table-of-contents)**

<a name="prefer-composition-over-inheritance-1"></a>
### Prefer composition over inheritance
As stated famously in [*Design Patterns*](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four, you should prefer composition over inheritance where you can. There are lots of good reasons to use inheritance and lots of good reasons to use composition. The main point for this maxim is that if your mind instinctively goes for inheritance, try to think if composition could model your problem better. In most of the cases it can.

You might be wondering then, "when should I use inheritance?" It depends on your problem at hand.

It depends of the way to structure your application. One error is to think that Inheritance is about code reuse, when is about extensibility and identification. If you want to share code between classes, composition is your tool. If you want to update only one detail of an existent class in a way that you are sure it never will be affected by the base class modifications (that means, is 100% compatible with the contract of this class), then inheritance is your way. But, be aware, mostly sure you will be programming something that requires composition and not inheritance. That's why the principle "[composition over inheritance](https://www.thoughtworks.com/insights/blog/composition-vs-inheritance-how-choose)"

Dogmas are bad, but using tools in wrong ways in a project that is going to wrong can make disasters.

**Bad:**
```javascript
class Employee {
	constructor(name, email) {
		this.name = name;
		this.email = email;
	}
}

// Bad because Employees "have" tax data. EmployeeTaxData is not a type of Employee
class EmployeeTaxData extends Employee {
	constructor(ssn, salary) {
		super();
		this.ssn = ssn;
		this.salary = salary;
	}
}
```

**Good**:
```javascript
class EmployeeTaxData {
	constructor(ssn, salary) {
		this.ssn = ssn;
		this.salary = salary;
	}
}

class Employee {
	constructor(name, email) {
		this.name = name;
		this.email = email;

	}

	setTaxData(ssn, salary) {
		this.taxData = new EmployeeTaxData(ssn, salary);
	}
}
```
**[⬆ back to top](#table-of-contents)**

<a name="testing"></a>
## Testing

Testing is more important than shipping. If you have no tests or an inadequate amount, then every time you ship code you won't be sure that you didn't break anything. Deciding on what constitutes an adequate amount is up to your team, but having 100% coverage (all statements and branches) is how you achieve very high confidence and developer peace of mind. This means that in addition to having a great testing framework, you also need to use a [good coverage tool](http://gotwarlost.github.io/istanbul/).

There's no excuse to not write tests. There's [plenty of good JS test frameworks](http://jstherightway.org/#testing-tools), so find one that your team prefers. When you find one that works for your team, then aim to always write tests for every new feature/module you introduce. If your preferred method is Test Driven Development (TDD), that is great, but the main point is to just make sure you are reaching your coverage goals before launching any feature, or refactoring an existing one.

You will find that in the test face you discover a lot of bugs and that making test will made you think how to destroy your program, and believe me, that will save you. But more important, with tests you don't need to check if your code breaks something, test tell you and you can refactor without any problem.

<a name="single-concept-per-test"></a>
### Single concept per test

Having an UNI-TEST™ will make difficult to know where the problem was. Split the test in several concepts / rules in a way that when something fail, only knowing the test you will be able to go to fix the code.  

**Bad:**
```javascript
const assert = require('assert');

describe('MakeMomentJSGreatAgain', function() {
	it('handles date boundaries', function() {
		let date;

		date = new MakeMomentJSGreatAgain('1/1/2015');
		date.addDays(30);
		date.shouldEqual('1/31/2015');

		date = new MakeMomentJSGreatAgain('2/1/2016');
		date.addDays(28);
		assert.equal('02/29/2016', date);

		date = new MakeMomentJSGreatAgain('2/1/2015');
		date.addDays(28);
		assert.equal('03/01/2015', date);
	});
});
```

**Good**:
```javascript
const assert = require('assert');

describe('MakeMomentJSGreatAgain', function() {
	it('handles 30-day months', function() {
		const date = new MakeMomentJSGreatAgain('1/1/2015');
		date.addDays(30);
		date.shouldEqual('1/31/2015');
	});

	it('handles leap year', function() {
		const date = new MakeMomentJSGreatAgain('2/1/2016');
		date.addDays(28);
		assert.equal('02/29/2016', date);
	});

	it('handles non-leap year', function() {
		const date = new MakeMomentJSGreatAgain('2/1/2015');
		date.addDays(28);
		assert.equal('03/01/2015', date);
	});
});
```
**[⬆ back to top](#table-of-contents)**

<a name="concurrency"></a>
## Concurrency

<a name="use-promises-not-callbacks"></a>
### Use Promises, not callbacks
Callbacks aren't clean, and they cause excessive amounts of nesting. With ES2015/ES6, Promises are a built-in global type. Use them!

**Bad:**
```javascript
require('request').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', (requestErr, response) => {
	if (requestErr) {
		console.error(requestErr);
	} else {
		require('fs').writeFile('article.html', response.body, (writeErr) => {
			if (writeErr) {
				console.error(writeErr);
			} else {
				console.log('File written');
			}
		})
	}
})

```

**Good**:
```javascript
require('request-promise').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
.then(response => require('fs-promise').writeFile('article.html', response))
.then(() => console.log('File written'))
.catch(err => console.error(err))

```
**[⬆ back to top](#table-of-contents)**

<a name="asyncawait-are-even-cleaner-than-promises"></a>
### Async/Await are even cleaner than Promises
Promises are a very clean alternative to callbacks, but ES2017/ES8 brings async and await which offer an even cleaner solution. All you need is a function that is prefixed in an `async` keyword, and then you can write your logic imperatively without a `then` chain of functions. Use this if you can take advantage of ES2017/ES8 features today! [But! If you don't have fully knowledge of the Promises, stay away from them, because the `async` feature is more complex and have more implications that seems](https://medium.com/@bluepnume/learn-about-promises-before-you-start-using-async-await-eb148164a9c8#.967cvgari).

**Bad:**
```javascript
require('request-promise').get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin')
.then(function(response) {
	return require('fs-promise').writeFile('article.html', response);
})
.then(function() {
	console.log('File written');
})
.catch(function(err) {
	console.error(err);
})
```

**Good**:
```javascript
async function getCleanCodeArticle() {
	try {
		const request = await require('request-promise')
		const response = await request.get('https://en.wikipedia.org/wiki/Robert_Cecil_Martin');
		const fileHandle = await require('fs-promise');

		await fileHandle.writeFile('article.html', response);
		console.log('File written');
	} catch(err) {
		console.error(err);
	}
}
```
**[⬆ back to top](#table-of-contents)**

<a name="error-handling"></a>
## Error handling

Thrown errors are a good thing! They mean the runtime has successfully
identified when something in your program has gone wrong and it's letting
you know by stopping function execution on the current stack, killing the
process (in Node), and notifying you in the console with a stack trace.

Every error well launched & handled with a good message means less hours of debugging (yes, in plural). Using the errors correctly means to have different layers, someone that handle this error, good logging system (the terminal is ok, depending of the size of the project), good system for identify them, and the most important:

**IF YOUR CODE USES PROMISES/AWAIT USE THE FUCKING .CATCH/TRY-CATCH AND WHEN YOU USE THEM, DONT JUST USE EMPTY FUNCTION, LOOG THE ERROR**. Loosing an error or having a silent one can be a bill that is not payed, a developer that will expend hours debugging trying to understand why a silent error happens or a boos that will get on nerves and yielding you because no one is able to explain wtf if happening. 


**Bad:**
```javascript
try {
	functionThatMightThrow();
} catch (error) {
	console.log(error);
}
```

**Good:**
```javascript
try {
	functionThatMightThrow();
} catch (error) {
	// One option (more noisy than console.log):
	console.error(error);
	// Another option:
	notifyUserOfError(error);
	// Another option:
	reportErrorToService(error);
	// OR do all three!
}
```

**Good:**
```javascript
getdata()
.then(data => {
	functionThatMightThrow(data);
})
.catch(error => {
	// One option (more noisy than console.log):
	console.error(error);
	// Another option:
	notifyUserOfError(error);
	// Another option:
	reportErrorToService(error);
	// OR do all three!
});
```

<a name="formatting"></a>
## Formatting

Formatting is subjective. Like many rules herein, there is no hard and fast rule that you must follow. The main point is DO NOT ARGUE over formatting. There are tons of tools to automate this. Use one! It's a waste of time and money for engineers to argue over formatting.

For things that don't fall under the purview of automatic formatting (indentation, tabs vs. spaces, double vs. single quotes, etc.) look here for some guidance.

<a name="use-consistent-capitalization"></a>
### Use consistent capitalization
JavaScript is untyped, so capitalization tells you a lot about your variables, functions, etc. These rules are subjective, so your team can choose whatever they want. The point is, no matter what you all choose, just be consistent.

**Bad:**
```javascript
const DAYS_IN_WEEK = 7;
const daysInMonth = 30;

const songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const Artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restore_database() {}

class animal {}
class Alpaca {}
```

**Good**:
```javascript
const DAYS_IN_WEEK = 7;
const DAYS_IN_MONTH = 30;

const songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restoreDatabase() {}

class Animal {}
class Alpaca {}
```
**[⬆ back to top](#table-of-contents)**


<a name="function-callers-and-callees-should-be-close"></a>
### Function callers and callees should be close
If a function calls another, keep those functions vertically close in the source file. Ideally, keep the caller right above the callee. We tend to read code from top-to-bottom, like a newspaper. Because of this, make your code read that way.

**Bad:**
```javascript
class PerformanceReview {
	constructor(employee) {
		this.employee = employee;
	}

	lookupPeers() {
		return db.lookup(this.employee, 'peers');
	}

	lookupMananger() {
		return db.lookup(this.employee, 'manager');
	}

	getPeerReviews() {
		const peers = this.lookupPeers();
		// ...
	}

	perfReview() {
		this.getPeerReviews();
		this.getManagerReview();
		this.getSelfReview();
	}

	getManagerReview() {
		const manager = this.lookupManager();
	}

	getSelfReview() {
	    // ...
	}
}

const review = new PerformanceReview(user);
review.perfReview();
```

**Good**:
```javascript
class PerformanceReview {
	constructor(employee) {
		this.employee = employee;
	}

	perfReview() {
		this.getPeerReviews();
		this.getManagerReview();
		this.getSelfReview();
	}

	getPeerReviews() {
		const peers = this.lookupPeers();
	// ...
	}

	lookupPeers() {
		return db.lookup(this.employee, 'peers');
	}

	getManagerReview() {
		const manager = this.lookupManager();
	}

	lookupMananger() {
		return db.lookup(this.employee, 'manager');
	}

	getSelfReview() {
		// ...
	}
}

const review = new PerformanceReview(employee);
review.perfReview();
```

**[⬆ back to top](#table-of-contents)**

<a name="comments"></a>
## Comments

<a name="only-comment-things-that-have-business-logic-complexity"></a>
### Only comment things that have business logic complexity.
Comments are an apology, not a requirement. Good code *mostly* documents itself.

**Bad:**
```javascript
function hashIt(data) {
	// The hash
	let hash = 0;

	// Length of string
	const length = data.length;

	// Loop through every character in data
	for (let i = 0; i < length; i++) {
		// Get character code.
		const char = data.charCodeAt(i);
		// Make the hash
		hash = ((hash << 5) - hash) + char;
		// Convert to 32-bit integer
		hash &= hash;
	}
}
```

**Good**:
```javascript

function hashIt(data) {
	let hash = 0;
	const length = data.length;

	for (let i = 0; i < length; i++) {
		const char = data.charCodeAt(i);
		hash = ((hash << 5) - hash) + char;

		// Convert to 32-bit integer
		hash &= hash;
	}
}

```
**[⬆ back to top](#table-of-contents)**

<a name="dont-leave-commented-out-code-in-your-codebase"></a>
### Don't leave commented out code in your codebase
Version control exists for a reason. Leave old code in your history.

**Bad:**
```javascript
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

**Good**:
```javascript
doStuff();
```
**[⬆ back to top](#table-of-contents)**

<a name="dont-have-journal-comments"></a>
### Don't have journal comments
Remember, use version control! There's no need for dead code, commented code,
and especially journal comments. Use `git log` to get history!

**Bad:**
```javascript
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
function combine(a, b) {
	return a + b;
}
```

**Good**:
```javascript
function combine(a, b) {
	return a + b;
}
```
**[⬆ back to top](#table-of-contents)**

<a name="avoid-positional-markers"></a>
### Avoid positional markers
They usually just add noise. Let the functions and variable names along with the
proper indentation and formatting give the visual structure to your code.

**Bad:**
```javascript
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
$scope.model = {
	menu: 'foo',
	nav: 'bar'
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
const actions = function() {
  // ...
}
```

**Good**:
```javascript
$scope.model = {
	menu: 'foo',
	nav: 'bar'
};

const actions = function() {
  // ...
}
```
**[⬆ back to top](#table-of-contents)**
