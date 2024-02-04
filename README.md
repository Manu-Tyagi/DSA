# DSA

Hello this is the collection of my all studied topics on DSA, code snippets mostly will be in Javascript

* [Print All Subsequence of a String](#print-all-subsequence-of-a-string)
* [Reverse the Array](#reverse-the-array)
* [Permutations of a given string](#permutations-of-a-given-string)


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

