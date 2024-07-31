# Problems and Solutions


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