# Object destructuring

> Syntax for split assignment, added in ECMAScript 2015. Only certain properties of an object can be referenced in a single variable.

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
    };
const {a, b} = obj;

console.log(a); //=> 1
console.log(b); //=> 2
````

Normally, the name of the variable should match the name of the object property, but you can also give it an alias by doing the following.

### give it an alias
a the value of the property to the variable newA
b Assign the value of the property to the variable newB

```js
const obj = {
    a: 1,
    b: 2,
    c: 3
    };
const {a: newA, b: newB} = obj;
// const {a, b} = obj; can be abbreviated as

console.log(newA); //=> 1
console.log(newB); //=> 2
```

### Specifying default values
You can specify a default value when assigning a split.
If the object you are splitting does not have any properties (undefined), the default value will be used.
```js
const obj = {
    a: 1,
    b: 2,
    c: 3
    };
const {a: newA, x: newX=999} = obj;

console.log(newA); //=> 1
console.log(newX); //=> 999
```

## Example usage.

## Shortcuts for constant fields
Referencing a property provided by a class, without the class name prefix

PI constants (pi) can be referred to by the short name PI.
```js
const {PI} = Math;
console.log(PI * 2); //=> 6.283185307179586
```

### object-split assignment in a for loop
```js
const books = [
  {title: 'Title1', author: 'Author1'},
  {title: 'Title2', author: 'Author2'},
  {title: 'Title3', author: 'Author3'},
];

for (const {title, author} of books) {
  console.log(`${title}, ${author}`);
}
```

### Extracting properties from complex objects
Extracting necessary properties from complex objects into individual variables

JSON data retrieved from Web APIs, etc., contains a lot of unneeded data, so extracting only the necessary properties with split assignments will simplify the subsequent code.
```js
// Data with complex structure (e.g., data retrieved via REST API)
const user = {
  id: 1,
  userName: 'Maku',
  avatar: { id: 1, userName: 'Maku', avatar: {
    id: 'avatar123',
    url: 'http://example.com/sample.png',
  },
};

// Extract only the properties we need into individual variables
const {
  userName,
  avatar: {
    id: avatarId
  }
} = user;

console.log(`${userName}, ${avatarId}`); //=> Maku, avatar123
```

### Refer to exported properties separately.


***

[Get only specific properties of an object into a single variable by split assignment (Object destructuring)](https://maku77.github.io/js/syntax/object-destructuring.html) Translated with www.DeepL.com/Translator (free version)