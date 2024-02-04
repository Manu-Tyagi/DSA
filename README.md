# DSA


1. [Print All Subsequence of a String](#print-all-subsequence-of-a-string)


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


