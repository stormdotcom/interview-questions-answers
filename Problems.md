# Problems and Solutions

## **How can you copy an object by value, not by reference, in JavaScript?**

To copy an object by value in JavaScript, you can use methods like:
- **Shallow Copy:**
  - `Object.assign({}, originalObject)` 
  - `{...originalObject}`
- **Deep Copy:**
  - `JSON.parse(JSON.stringify(originalObject))`
  - Libraries like Lodash with `_.cloneDeep(originalObject)`

Shallow copies only copy the top-level properties, while deep copies clone the entire object, including nested properties.

## **What is the `this` keyword in an arrow function in JavaScript?**

In arrow functions, the `this` keyword does not refer to the function itself as it does in regular functions. Instead, it inherits `this` from the surrounding lexical scope, maintaining the context from where the arrow function is defined. This means that `this` in an arrow function is consistent with the `this` of the outer function or context.

## **Which Git command enables you to pick up commits from a branch within a repository and apply them to another branch?**

The `git cherry-pick` command enables you to pick specific commits from one branch and apply them to another branch. This command is useful for integrating particular changes without merging entire branch histories.

## **What are Git hooks?**

Git hooks are scripts that Git executes before or after events such as committing changes, merging branches, pushing commits, and more. These hooks are customizable and can automate tasks, enforce policies, and integrate with external systems. Examples include pre-commit hooks for linting code or post-commit hooks for deploying changes.

## **How can you return the names of people who are reported to (excluding null values), the number of members that report to them, and the average age of those members as an integer, ordered by names alphabetically?**

To achieve this, you can use the following SQL query:
```sql
SELECT ReportsTo AS Name,
       COUNT(*) AS NumberOfMembers,
       FLOOR(AVG(Age)) AS AverageAge
FROM Employees
WHERE ReportsTo IS NOT NULL
GROUP BY ReportsTo
ORDER BY ReportsTo;
```
This query selects the `ReportsTo` column, counts the number of members reporting to each person, calculates the average age (rounded down to the nearest integer), excludes null values, and orders the results alphabetically by `ReportsTo`.

## **How can you find the first word with the greatest number of repeated letters in a string in JavaScript?**

To find the first word with the greatest number of repeated letters in a string, follow these steps:
1. Split the string into words.
2. Define a function to count repeated letters in each word.
3. Iterate through the words to determine which word has the highest count of repeated letters.
4. Return the first word that meets this criterion.

Example code:
```javascript
function getFirstWordWithGreatestRepeats(str) {
  function countRepeatedLetters(word) {
    const counts = {};
    let maxCount = 0;
    for (const char of word) {
      counts[char] = (counts[char] || 0) + 1;
      if (counts[char] > maxCount) {
        maxCount = counts[char];
      }
    }
    return maxCount;
  }

  const words = str.split(' ');
  let maxRepeats = 0;
  let resultWord = '';

  for (const word of words) {
    const repeats = countRepeatedLetters(word);
    if (repeats > maxRepeats) {
      maxRepeats = repeats;
      resultWord = word;
    }
  }

  return resultWord;
}
```
This function splits the string into words, counts the repeated letters in each word, and returns the first word with the greatest number of repeated letters.

```