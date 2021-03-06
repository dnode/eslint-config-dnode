[![Dependency Status](https://david-dm.org/dnode/dredis.svg)](https://david-dm.org/dnode/dredis)
[![devDependency Status](https://david-dm.org/dnode/dredis/dev-status.svg)](https://david-dm.org/dnode/dredis#info=devDependencies)

# Installation

`npm i --save dexpress`

Add a `.eslintrc`:
```json
{
  "extends": "dnode"
}
```


# Rules

## class-methods-use-this

A method not using this can be static, yes, but I wouldn't force it. 
There can be reasons a method should be declared used with an instance
(non static) independently if the method really use this or not.


## comma-dangle

Trailing commas always if multiline. Exception for functions because 
node doesn't allow it.


## consistent-return

A function without a `return` returns implicit `undefined`. So if I have 
one case which returns something and other cases which not, I don't 
write a `return;` or `return undefined;`.
 
### bad

Use `return;` or `return undefined;` if nothing should be returned:
```javascript
function example(example) {
  if (example === 'example') {
    return example;
  }
  return;
}
```

### good

Just skip the unneeded returns and rely on the implicit return 
`undefined`:
```javascript
function example(example) {
  if (example === 'example') {
    return example;
  }
}
```


## global-require

I don't like to force the use of `require` in a global way. Sometimes 
its just shorter to use it inside a structure. Like inside an object for 
the `lib.js`.
 
### bad

Define first `const` variables for all `require`:
```javascript
const Example = require('./Example');

module.exports = {
  Example,
};
```

### good

Just use `require` inside the object:
```javascript
module.exports = {
  Example: require('./Example'),
};
```


##  import/newline-after-import

If using require it can be smart to chain and group the require together 
with other sequences.

### bad

Using always new lines to separate require and another sequences:
```javascript
const app = require('express')();

app.listen(process.env.PORT);
```

### good

Group the lines by logically:
```javascript
const app = require('express')();
app.listen(process.env.PORT);
```


## import/no-dynamic-require

Dynamic require can not be analysed by static code analyser. But they
allow a lot of convenient structures.

## bad

Manually require all files statically into an object:
```javascript
const examples = {
  a: require('./a'),
  b: require('./b'),
  c: require('./c'),
};
const example = 'a';
examples[example]();
```

### good

Use dynamic require for a convenient structure:
```javascript
const example = 'a';
require(`./${example}`)();
```


## no-await-in-loop

Sometimes the async operations depending on each other in a loop. So its
a legal use of await in a loop.


## no-console

There isn't something bad in using `console.log` in node. 12factor say
explicit logging should be done by `stdout` which is `console.log`.


## no-lonely-if

Sometimes there is an else with a following if which is not depending to
each other. In this cases its not usefull to transform this into an else
if.


## no-param-reassign

JavaScript doesn't have overloaded functions. So to define functions 
which allows multiple type of parameters I think reassign this parameter
is a short and effective way to handle this.
  
### bad

Define new variables:
```javascript
function example(examples) {
  let checkedExamples = examples;
  if (!Array.isArray(checkedExamples)) {
    checkedExamples = [checkedExamples];
  }
}
```

### good

Just reassign the parameters:
```javascript
function example(examples) {
  if (!Array.isArray(examples)) {
    examples = [examples];
  }
}
```


## no-restricted-syntax

JavaScript allow to iterate over arrays/objects with `for ... in` and
`for ... of`. I want to use these keywords instead of functions like 
`.forEach` because its better readable.
  
### bad

`.forEach` with arrow function:
```javascript
examples.forEach(example => {

});
```

### good

Use the native keywords of JavaScript:
```javascript
for (const example of examples) {
  
}
```


## no-shadow

It can make sense to use the same variables in different layers, 
especially for closures in array functions. But still care about the 
readability.
  
### bad

Numerate or prefix variables:
```javascript
const element = elements.map(element2 => element2.valid)[0];
// or
const element = elements.map(innerElement => innerElement.valid)[0];
```

### good

Use the same variable names if the readability is still given:
```javascript
const element = elements.map(element => element.valid)[0];
```


## no-underscore-dangle

There is not a problem in using underscores in the beginning of a 
variable or function, especially if its not used to hint private or
protected e.g. in translation function '__()'.
