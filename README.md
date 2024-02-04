# DSA

Hello this is the collection of my all studied topics on DSA, code snippets mostly will be in Javascript

1. [Print All Subsequence of a String](#print-all-subsequence-of-a-string)
1. [Reverse the Array](#reverse-the-array)


## Print All Subsequence of a String
	
We resolve this question using Reccursion
We have one termination condition 
We have two loops inside one reccursion where we include current character or not
When reccursion ends we print current character


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

Find start and end index of array
Swap a[start] with a[end]
start++ & end –

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

