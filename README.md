# consistent-return

A function without a `return` returns implicit `undefined`. So if I have 
one case which returns something and other cases which not, I don't 
write a `return;` or `return undefined;`.
 
## bad

Use `return;` or `return undefined;` if nothing should be returned:
```
function example(example) {
  if (example === 'example') {
    return example;
  }
  return;
}
```

## good

Just skip the unneeded returns and rely on the implicit return 
`undefined`:
```
function example(example) {
  if (example === 'example') {
    return example;
  }
}
```


# global-require

I don't like to force the use of `require` in a global way. Sometimes 
its just shorter to use it inside a structure. Like inside an object for 
the `lib.js`.
 
## bad

Define first `const` variables for all `require`:
```
const Example = require('./Example');

module.exports = {
  Example,
};
```

## good

Just use `require` inside the object:
```
module.exports = {
  Example: require('./Example'),
};
```


# no-await-in-loop

Sometimes the async operations depending on each other in a loop. So its
a legal use of await in a loop.


# no-param-reassign

JavaScript doesn't have overloaded functions. So to define functions 
which allows multiple type of parameters I think reassign this parameter
is a short and effective way to handle this.
  
## bad

Define new variables:
```
function example(examples) {
  let checkedExamples = examples;
  if (!Array.isArray(checkedExamples)) {
    checkedExamples = [checkedExamples];
  }
}
```

## good

Just reassign the parameters:
```
function example(examples) {
  if (!Array.isArray(examples)) {
    examples = [examples];
  }
}
```


# no-restricted-syntax

JavaScript allow to iterate over arrays/objects with `for ... in` and
`for ... of`. I want to use these keywords instead of functions like 
`.forEach` because its better readable.
  
## bad

`.forEach` with arrow function:
```
examples.forEach(example => {

});
```

## good

Use the native keywords of JavaScript:
```
for (const example of examples) {
  
}
```


# no-underscore-dangle

I don't like to use `_` for private/protected, but sometimes its just 
good to avoid name collisions without think about stupid other names. 
