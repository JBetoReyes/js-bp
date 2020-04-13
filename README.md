## References

1. Use ```const``` for all of your references; avoid using var.

* This ensures that you can't reassign your references
```javascript
//bad
var a = 1;

// good
const b = 1;
```

2. If you must reassign references, use ```let``` instead of ```var````
```javascript
// bad
var count = 1;
if (true) {
    count +=1;
}

// good, use the let
let count = 1;
if (true) {
    count+= 1;
}

// const and let only exist in the blocks they are defined in.
{
  let a = 1;
  const b = 1;
}
console.log(a); // ReferenceError
console.log(b); // ReferenceError
```

## Objects

3. Use property value shorthand.

* It's shorter and descriptive

```javascript
const lukeSkywalker = 'Luke Skywalker';

// bad
const obj = {
  lukeSkywalker: lukeSkywalker,
};

// good
const obj = {
  lukeSkywalker,
};
```

4. Only quote properties that are invalid identifiers.

* It improves syntax highlighting, and is also more easily optimzed by many JS engines.

```javascript
// bad
const bad = {
  'foo': 3,
  'bar': 4,
  'data-blah': 5,
};

// good
const good = {
  foo: 3,
  bar: 4,
  'data-blah': 5,
};
```

5. Prefer the object spread operator over ``Object.assign```to shallow-copy objects. Use the object rest operator to get a new object with certain properties ommited.

```javascript
// very bad
const original = { a: 1, b: 2 };
const copy = Object.assign(original, { c: 3 }); // this mutates `original` ಠ_ಠ
delete copy.a; // so does this

// bad
const original = { a: 1, b: 2 };
const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

// good
const original = { a: 1, b: 2 };
const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
```

## Arrays

6. Use array spreads ```...```to copy arrays.

```javascript
// bad
const len = items.length;
const itemsCopy = [];
let i;

for (i = 0; i < len; i += 1) {
  itemsCopy[i] = items[i];
}

// good
const itemsCopy = [...items];
```

7. It's ok to omit the return if the function body consists of a single statement.

```javascript
// good
[1, 2, 3].map((x) => {
  return x + 1;
});

// good
[1, 2, 3].map((x) => x + 1);
```

## Destructuring

8. Use object destructuring when accessing and using multiple properties of an object.

```javascript
// bad
function getFullName(user) {
  const firstName = user.firstName;
  const lastName = user.lastName;

  return `${firstName} ${lastName}`;
}

// good
function getFullName(user) {
  const { firstName, lastName } = user;
  return `${firstName} ${lastName}`;
}

// best
function getFullName({ firstName, lastName }) {
  return `${firstName} ${lastName}`;
}
```

9. Use array destructuring.

```javascript
const arr = [1, 2, 3, 4];

// bad
const first = arr[0];
const second = arr[1];

// good
const [first, second] = arr;
```

## Functions

10. Use default parameter syntax rather than mutating function arguments

```javascript
// really bad
function handleThings(opts) {
  // No! We shouldn’t mutate function arguments.
  // Double bad: if opts is falsy it'll be set to an object which may
  // be what you want but it can introduce subtle bugs.
  opts = opts || {};
  // ...
}

// still bad
function handleThings(opts) {
  if (opts === void 0) {
    opts = {};
  }
  // ...
}

// good
function handleThings(opts = {}) {
  // ...
}
```

11. Never reassign paramaters.

* Reassigning parameters can lead to unexpected behavior, especially when accessing the ```arguments``` object. it can also cause optimization issues, especially in V8.

```javascript
// bad
function f1(a) {
  a = 1;
  // ...
}

function f2(a) {
  if (!a) { a = 1; }
  // ...
}

// good
function f3(a) {
  const b = a || 1;
  // ...
}

function f4(a = 1) {
  // ...
}
```