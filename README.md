<h1>DSA</h1>
<br>
<br>
<table>
	<tr>
		<th>S.No</th>
		<th>Topics</th>
	</tr>
	<tr>
		<td>
			1
		</td>
		<td>
			<a href="#topic-1">Print All Subsequence of a String</a>
		</td>
	</tr>
</table>
<br>
<br>
<div id="topic-1">
	<h2>
		Print All Subsequence of a String
	</h2>
	<br>
	<pre>
        We resolve this question using Reccursion
        We have one termination condition 
        We have two loops inside one reccursion where we include current character or not
        When reccursion ends we print current character
    </pre>
    <code>
        function subSeq(str, current = '', index = 0) {
        if (index === str.length) {
            console.log(current);
            return;
        }

        // Include the current character in the subsequence
        subSeq(str, current + str[index], index + 1);

        // Exclude the current character from the subsequence
        subSeq(str, current, index + 1);
        }

        // Example usage
        let inputString = "abc";
        subSeq(inputString);
    </code>
</div>