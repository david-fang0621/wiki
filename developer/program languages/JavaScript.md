# Array Methods

```jsx
[4, 5, 6, 7]
  .at(1) // 5
  [(4, 5, 6, 7)].push(8) // [4,5,6,7,8]
  [(4, 5, 6, 7)].pop() // [4,5,6]
  [(4, 5, 6, 7)].fill(1) // [1,1,1,1]
  [(4, 5, 6, 7)].join(" ") // 4 5 6 7 (string)
  [(4, 5, 6, 7)].shift() // [5,6,7]
  [(4, 5, 6, 7)].reverse() // [7,6,5,4]
  [(4, 5, 6, 7)].unshift(3) // [3,4,5,6,7]
  [(4, 5, 6, 7)].includes(6) // true
  [(4, 5, 6, 7)].map((item) => 2 * item) // [8,10,12,14]
  [(4, 5, 6, 7)].filter((item) => item > 5) // [6,7]
  [(4, 5, 6, 7)].find((item) => item > 5) // 6 (first match)
  [(4, 5, 6, 7)].every((item) => item > 0) // true
  [(4, 5, 6, 7)].findIndex((item) => item == 5) // 1
  [(4, 5, 6, 7)].reduce((prev, curr) => prev + curr, 0) // 22
  [(4, 5, 6, 7)].some((item) => item > 5); // true
```

# JavaScript Snippets

```jsx
// Get current date and time
const now = new Date();

// Check if a variable is an array:
Array.isArray(variable);

// Merge two arrays:
const newArray = array1.concat(array2);

// Remove duplicates from an array:
const uniqueArray = [...new Set(array)];

// Sort an array in ascending order:
array.sort((a, b) => a - b);

// Reverse an array:
array.reverse();

// Convert string to number:
const number = parseInt(string);

// Generate a random number between two values:
const randomNumber = Math.floor(Math.random() * (max - min + 1)) + min;

// Check if a string contains a substring:
string.includes(substring);

// Get the length of an object:
Object.keys(object).length;

// Convert object to array:
const array = Object.entries(object);

// Check if an object is empty:
Object.keys(object).length === 0;

// Get current URL:
const url = window.location.href;

// Redirect to a new URL:
window.location.replace(url);

// Copy text to clipboard:
navigator.clipboard.writeText(text);
```
