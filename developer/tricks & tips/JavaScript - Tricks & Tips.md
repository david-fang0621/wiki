### Ternary Operator

```jsx
function getResult(score) {
  return score > 5 ? "Yes" : "No";
}
```

### Nullish coalescing operator

```jsx
function printMessage(text) {
  const message = text ?? "NA"; // if undefined or null, then 'NA'
  console.log(message);
}
// Tips - default parametter is only for undefined
// Logical OR oprator `||` if undefined, null, NAN, 0, -0, '', false, then 'NA'
```

### Object Destructuring

```jsx
const { name, email, phone } = contact;
```

### Spread syntax

```jsx
const item = { type: "shoes", size: "M" };
const detail = { price: 20, gender: "M" };

// Old method 1
const newObj = new Object();
newObj["type"] = item.type;

// Old method 2
const newObj = {
  type: item.type,
  size: item.size,
  price: detail.price,
};

// Old method 3
const newObj = Object.assign(item, detail);

// Spread syntax (Object)
const newObj = { ...item, ...detail };

// Spread syntax (Array)
const fruits1 = ["apple", "bear", "orange"];
fruits1 = [...fruits1, "strawberry"]; // fruits.push('strawberry');
fruits1 = ["strawberry", ...fruits1]; // fruits.unshift('strawberry')
const fruits2 = ["berry", "cherry", "cdf"];
const combined = [...fruits1, ...fruits2]; // fruits1.contact(fruits2)
```

### Optional Chaining

```jsx
function displayJobTitle(person) {
  if (person.job?.title) {
    // person.job && person.job.title
    console.log(person.job.title);
  }
}
```

### Template Literals

```jsx
const message = `Hello ${name}, Your current score is: ${score}`;
```

### Looping

```jsx
const items = [1, 2, 3, 4, 5, 6];
// Requirements - sum(even(items) * 4)
// Old method
const evens = items.filter((num) => num % 2 === 0);
const multiple = evens.map((num) => num * 4);
const sume = multiple.reduce((a, b) => a + b, 0);
// Chaining
const reulst = items
  .filter((num) => num % 2 === 0)
  .map((num) => num * 4)
  .reduce((a, b) => a + b, 0);
```

### Async / Await

```jsx
// Old method
function displayUser() {
  fetchUser().then((user) => {
    fetchProfile(user).then((profile) => {
      updateUI(user, profile);
    });
  });
}
// Async / Await
async function displayuser() {
  const user = await fetchUser();
  const profile = await fetchProfile(user);
  updateUI(user, profile);
}
```

### Remove Duplicates

```jsx
const array = ["a", "b", "c", "a", "d"];
console.log([...new Set(array)]);
```

### Coding Rule

```
DRY - Don't Repeat Yourself
KISS - Keep It Simple, Stupid
YAGNI - You Aren't Gonna Need It
```
