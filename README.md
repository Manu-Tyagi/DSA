# DSA

Hello this is the collection of my all studied topics on DSA, code snippets mostly will be in Javascript

- [DSA](#dsa)
  - [Print All Subsequence of a String](#print-all-subsequence-of-a-string)
  - [Reverse the Array](#reverse-the-array)
  - [Permutations of a given string](#permutations-of-a-given-string)
  - [Split the binary string into substrings](#split-the-binary-string-into-substrings)
  - [Next Permutation of a string](#next-permutation-of-a-string)
  - [Parenthesis Checker](#parenthesis-checker)
  - [Word Break](#word-break)
  - [Convert Sentence into mobile numeric keypad sequence](#convert-sentence-into-mobile-numeric-keypad-sequence)
  - [Count the Reversals](#count-the-reversals)
  - [Find maximum and minimum element in array](#find-maximum-and-minimum-element-in-array)
  - [Find kth smallest element in array](#find-kth-smallest-element-in-array)
  - [Count of number of given string in 2D character array](#count-of-number-of-given-string-in-2d-character-array)
  - [Sort without using sorting Algorithm](#sort-without-using-sorting-algorithm)
  - [Search a word in 2D grid of characters](#search-a-word-in-2d-grid-of-characters)
  - [Boyer Moore Algorithm](#boyer-moore-algorithm)


## Print All Subsequence of a String
	
* We resolve this question using Reccursion
* We have one termination condition 
* We have two loops inside one reccursion where we include current character or not
* When reccursion ends we print current character
* ![source image](https://shorturl.at/esxI5)

```javascript
    function subSeq(str, current = '', index = 0) {
    if (index === str.length) {
        console.log(current);
        return;
    }
    subSeq(str, current + str[index], index + 1);
    subSeq(str, current, index + 1);
    }

    let inputString = "abc";
    subSeq(inputString);
```

## Reverse the Array

* Find start and end index of array
* Swap a[start] with a[end]
* start++ & end –

```javascript
let a=[1,2,3,4,5,6]
let s = 0;
let e = a.length-1;
console.log('arr',a);
while(s<e){
    let t = a[s];
    a[s]=a[e];
    a[e]=t;
    s++;
    e--;
}
console.log('rev arr',a);
```

## Permutations of a given string

* Take current string as empty and remaining string
* Pick one string in current and and remove that from remaining and start again permutation
* repeate above step for all strings (inital combo will be (a,bc)(b,ac)(c,ab))
* ![source image](https://shorturl.at/FGVW7)

```javascript
const result = [];

function permute(current, remaining) {
    if (remaining.length === 0) {
        result.push(current);
        return;
    }
    for (let i = 0; i < remaining.length; i++) {
        const nextCurrent = current + remaining[i];
        const nextRemaining = remaining.slice(0, i) + remaining.slice(i + 1);
        // if i = 1, nextCurrent = ac , nextRemaining = b for first iteration
        permute(nextCurrent, nextRemaining);
    }
}

permute('', "abc");
console.log(result);
```

## Split the binary string into substrings

* Take two counter as c1 and c2, 
* Increase them respectively on occurence of '0' and '1'
* When c1 == c2, string found slice from orignal string and return it
* Time complexity O(n)

```javascript
function splitBinaryString(s) {
  let c0 = 0;
  let c1 = 0;
  let substrings = [];

  for (let i = 0; i < s.length; i++) {
    if (s[i] === '0') {
      c0++;
    } else {
      c1++;
    }

    if (c0 === c1) {
      substrings.push(s.substring(0, i + 1));
      s = s.slice(i + 1);
      c0 = 0;
      c1 = 0;
      i = -1;
    }
  }

  return substrings;
}

// Example usage:
let binaryString = "1100011100111001100011";
let result = splitBinaryString(binaryString);
console.log(result);
```

## Next Permutation of a string

* Find the rightmost element smaller than the element to its right
* Find the rightmost element greater than the element at index i
* Swap the elements at indices i and j
* Reverse the subarray to the right of index i

```javascript
function nextPermutation(arr) {
    const n = arr.length;

    // Step 1: Find the rightmost element smaller than the element to its right
    let i = n - 2;
    while (i >= 0 && arr[i] >= arr[i + 1]) {
        i--;
    }

    // Step 2: Find the rightmost element greater than the element at index i
    if (i >= 0) {
        let j = n - 1;
        while (arr[j] <= arr[i]) {
            j--;
        }

        // Step 3: Swap the elements at indices i and j
        [arr[i], arr[j]] = [arr[j], arr[i]];
    }

    // Step 4: Reverse the subarray to the right of index i
    let start = i + 1;
    let end = n - 1;
    while (start < end) {
        [arr[start], arr[end]] = [arr[end], arr[start]];
        start++;
        end--;
    }
}

// Example usage:
let arr = [1, 2, 3];
nextPermutation(arr);
console.log(arr);  // Output: [1, 3, 2]

arr = [3, 2, 1];
nextPermutation(arr);
console.log(arr);  // Output: [1, 2, 3]

arr = [1, 1, 5];
nextPermutation(arr);
console.log(arr);  // Output: [1, 5, 1]

```

## Parenthesis Checker

* Make two array, one of openChars, and another for closeChars
* If character belongs to openChars, push in stack
* If character belongs to closeChars, pop element and check it must belong to corresponding openChars
* If true then continue if false then break and return false

```javascript
function isBalanced(exp) {
    const stack = [];
    const openChars = ['{', '(', '['];
    const closeChars = ['}', ')', ']'];

    for (let i = 0; i < exp.length; i++) {
        const char = exp[i];
        if (openChars.includes(char)) {
            stack.push(char);
        } else if (closeChars.includes(char)) {
            const correspondingOpenChar = openChars[closeChars.indexOf(char)];
            if (stack.length === 0 || stack.pop() !== correspondingOpenChar) {
                return false;
            }
        }
    }

    return stack.length === 0;
}

// Drive code
const exp1 = "[()]{}{[()()]()}";
const exp2 = "[(])";

if (isBalanced(exp1)) {
    console.log("balanced");
} else {
    console.log("not balanced");
}

if (isBalanced(exp2)) {
    console.log("balanced");
} else {
    console.log("not balanced");
}

```

## Word Break

* Create DP array fill values with false and first value must be true
* For each character create substring and check if it is in dictionary or not
* If it is in dictionary mark that index as true in DP array
* next time create substring from that index and go further
* If last index of DP array is true then return true else false

```javascript
function wordBreak(A, B) {
    const n = A.length;
    const dp = new Array(n + 1).fill(false);
    dp[0] = true;

    for (let i = 1; i <= n; i++) {
        for (let j = 0; j < i; j++) {
            if (dp[j] && B.includes(A.substring(j, i))) {
                dp[i] = true;
                break;
            }
        }
    }

    return dp[n] ? 1 : 0;
}

// Example usage:
const A = "leetcode";
const B = ["leet", "code"];

console.log(wordBreak(A, B)); // Output: 1 (A can be segmented into "leet code")
```

## Convert Sentence into mobile numeric keypad sequence

* Create an array to store all combination for each characters
* If input character is blank ' ' choose 0 from sequence
* If input character is alphabet then find corresponding number from charCodeAt method and use that number as index

```javascript
let str = ["2", "22", "222",
       "3", "33", "333",
       "4", "44", "444",
       "5", "55", "555",
       "6", "66", "666",
       "7", "77", "777", "7777",
       "8", "88", "888",
       "9", "99", "999", "9999", "0" ]
     
let input = "GEEKS FOR GEEKS";

console.log('print sequence',printSeq(str,input))
function printSeq(arr,input){
    let output="";
    for(let i=0;i<input.length;i++){
        if(input[i] == ' '){
            output += arr[26]
        }
        else{
            let p = input[i].charCodeAt(0) - 'A'.charCodeAt(0);
            output += arr[p]
        }
    }
    return output;
}
```
## Count the Reversals

*  If string length is odd, string cannot be balanced
*  If char is '{' push in stack
*  If char is '}' and stack length is 0 then reversal is required and push '{'
*  If char is '}' and stack length is not 0 then pop from stack

```javascript
function minReversals(S) {
    if (S.length % 2 !== 0) {
        return -1; // If the length of the string is odd, it can't be balanced
    }

    let stack = [];
    let reversals = 0;

    for (let i = 0; i < S.length; i++) {
        if (S[i] === '{') {
            stack.push('{');
        } else if (S[i] === '}') {
            if (stack.length === 0) {
                // If the stack is empty, it means we need to reverse the current '}'
                reversals++;
                stack.push('{'); // Push '{' onto the stack to balance
            } else {
                stack.pop(); // Pop matching '{'
            }
        }
    }

    // At this point, the stack contains unbalanced '{' brackets
    // For each pair of unbalanced brackets, we need 1 reversal
    // If there are odd number of unbalanced brackets, we need 2 reversals for each pair
    reversals += Math.ceil(stack.length / 2);

    return reversals;
}

// Example usage:
console.log(minReversals("}}{{")); // Output: 2
console.log(minReversals("{{{{")); // Output: 2
console.log(minReversals("}{{{{{{{{{{{{{{{{{{{{")); // Output: 10
console.log(minReversals("}{{{{{{{{{{{{{{{{{{{{{{")); // Output: 11
console.log(minReversals("{{{{{{{{{{{{{{{{{{{{{{")); // Output: 0

```

## Find maximum and minimum element in array

* Take first two element as minimum and maximum
* Take next pair and compare them with existing one
* In n/2 loop you will get minimum and maximum

```javascript
let arr = [10,23,31,45,1,4,6,90]
let minmax=findMinMax(arr);
console.log('min->',minmax[0],'max->',minmax[1]);

function findMinMax(a){
let mx = 0;
let mn =0;
let n= a.length;
let i =0;
if(n%2 == 0){
    mn = Math.min(a[0],a[1]);
    mx = Math.max(a[0],a[1]);
    i=2;
}
else{
    mx = a[0];
    mn = a[0];
    i=1;
}

while(i<n-1){
    if(a[i]>a[i+1]){
        mx=Math.max(mx,a[i]);
        mn=Math.min(mn,a[i+1]);
    }
    else{
        mx=Math.max(mx,a[i+1]);
        mn=Math.min(mn,a[i]);
    }
    i=i+2;
}
return [mn,mx];
}
```

## Find kth smallest element in array

* Sort the array
* Return k-1 element

```javascript
class Solution {
    kthSmallest(arr,l,r,k){
        return arr.sort((a,b)=>(a-b))[k-1];
    }
}
```

## Count of number of given string in 2D character array

* iterate through each element to check first character of string
* if first character found, check subsequent characters in the row
* if subsequent characters found, increase counter, finally return counter

```javascript
function countStringOccurrences(matrix, targetString) {
    let count = 0;

    // Iterate through each row
    for (let i = 0; i < matrix.length; i++) {
        // Iterate through each element in the row
        for (let j = 0; j < matrix[i].length; j++) {
            // If the current element matches the target string
            // increase the count
            if (matrix[i][j] === targetString[0]) {
                let k = 1;
                let x = i, y = j;
                let found = true;
                while (k < targetString.length) {
                    if (++y >= matrix[i].length || matrix[x][y] !== targetString[k]) {
                        found = false;
                        break;
                    }
                    k++;
                }
                if (found) count++;
            }
        }
    }

    return count;
}

// Example usage:
const matrix = [
    ['a', 'b', 'c', 'd'],
    ['e', 'f', 'a', 'b'],
    ['a', 'b', 'c', 'd']
];

const targetString = 'ab';
console.log(countStringOccurrences(matrix, targetString)); // Output: 4

```

## Sort without using sorting Algorithm

* Traverse through array
* Create an object container 0,1,2
* Increase counter of each field when number occurs while traversing
* Loop through ek field in object and assign its key to new array

```javascript
sort(arr, N)
{
    // your code here
    let a =[];
    let obj={
    0:0,
    1:0,
    2:0
    };
    arr.map((a)=>{
        obj[a]++;
    });
    Object.keys(obj).forEach((key)=>{
        for(let i=0;i<obj[key];i++)
            a.push(parseInt(key));
    });
    return a;
}
```

## Search a word in 2D grid of characters

* Perform depth first search
* If word.length == index that we are searching return true
* If row or column < 0 or row or coloumn expand out of grid or grid[row][col] != word[index] return false
* else perform DFS again for [r+1][c], [r-1][c], [r][c+1], [r][c-1]
* if character visited mark it with #
* [solution explaination](#https://www.youtube.com/watch?v=4QjCc7HeR8s&ab_channel=CuriousChahar)

```javascript
function searchWord(grid, word) {
    const numRows = grid.length;
    const numCols = grid[0].length;
    
    function dfs(row, col, index) {
        // Base case: If all characters in the word are found
        if (index === word.length) {
            return true;
        }
        
        // Boundary conditions and character matching
        // if row or column becomes negative
        // if row or column comes out of range
        if (
            row < 0 || 
            col < 0 || 
            row >= numRows || 
            col >= numCols || 
            grid[row][col] !== word[index]
        ) {
            return false;
        }
        
        // Mark the current cell as visited
        const temp = grid[row][col];
        // Marked as visited
        grid[row][col] = '#'; 
        
        // Explore neighboring cells in all direction
        const found = dfs(row + 1, col, index + 1) ||
                     dfs(row - 1, col, index + 1) ||
                     dfs(row, col + 1, index + 1) ||
                     dfs(row, col - 1, index + 1);
        
        // Restore the character before backtracking
        grid[row][col] = temp;
        
        return found;
    }
    
    // Iterate through each cell in the grid
    for (let i = 0; i < numRows; i++) {
        for (let j = 0; j < numCols; j++) {
            // if first letter found and dfs return true
            if (grid[i][j] === word[0] && dfs(i, j, 0)) {
                return true;
            }
        }
    }
    
    return false; // Word not found
}

// Example usage:
const grid = [
    ['A', 'B', 'C', 'E'],
    ['S', 'F', 'C', 'S'],
    ['A', 'D', 'E', 'E']
];

console.log(searchWord(grid, 'ABCCED')); // Output: true
console.log(searchWord(grid, 'SEE'));    // Output: true
console.log(searchWord(grid, 'ABCB'));   // Output: false

```

## Boyer Moore Algorithm

* Make bad match table
  * max(1,length-index-1)
* compare pattern from behind
* if character found move index to left
* else skip characters acording to badtable

```javascript
function boyerMooreHorspool(text, pattern) {
    const textLength = text.length;
    const patternLength = pattern.length;

    // Function to preprocess the pattern and create the bad character skip table
    function preprocessPattern(pattern) {
        const skipTable = {};

        // Filling the table with the rightmost occurrence index of each character in the pattern
        for (let i = 0; i < patternLength - 1; i++) {
            skipTable[pattern[i]] = patternLength - i - 1;
        }

        return skipTable;
    }

    // Preprocessing the pattern
    const skipTable = preprocessPattern(pattern);

    // Function to perform the search
    function search() {
        let i = patternLength - 1; // Start comparing from the end of the pattern
        while (i < textLength) {
            let j = patternLength - 1;
            let k = i;

            // Matching characters from right to left in the pattern and text
            while (j >= 0 && pattern[j] === text[k]) {
                j--;
                k--;
            }

            // If a match is found, return the index where the pattern starts
            if (j === -1) {
                return k + 1;
            } else {
                // Calculate the shift based on the bad character rule
                const badCharacter = text[i];
                const shift = skipTable[badCharacter] || patternLength;
                i += shift;
            }
        }
        return -1; // Pattern not found
    }

    return search();
}

// Example usage:
const text = "ABAAABCD";
const pattern = "ABC";

console.log(boyerMooreHorspool(text, pattern)); // Output: 4 (pattern found at index 4)

```