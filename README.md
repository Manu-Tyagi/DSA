# DSA

Hello this is the collection of my all studied topics on DSA, code snippets mostly will be in Javascript

* [Print All Subsequence of a String](#print-all-subsequence-of-a-string)
* [Reverse the Array](#reverse-the-array)
* [Permutations of a given string](#permutations-of-a-given-string)
* [Split the binary string into substrings with equal number of 0s and 1s](#split-the-binary-string-into-substrings)
* [Next Permutation of a string](#next-permutation-of-a-string)
* [Parenthesis Checker](#parenthesis-checker)
* [Word Break](#word-break)
* [Convert Sentence into mobile numeric keypad sequence](#convert-sentence-into-mobile-numeric-keypad-sequence)
* [Count the Reversals](#count-the-reversals)


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