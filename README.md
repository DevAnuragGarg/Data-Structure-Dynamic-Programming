# Data-Structure-Dynamic-Programming

Dynamic Programming is a method for solving a complex problem by breaking it down into a collection of simpler subproblems, solving each of those subproblems just once, and storing their solutions using a memory-based data structure (array, map,etc). So the next time the same subproblem occurs, instead of recomputing its solution, one simply looks up the previously computed solution, thereby saving computation time. This technique of storing solutions to subproblems instead of recomputing them is called memoization. The problem should be able to be divided into smaller overlapping sub-problems.

======
Top to Down: The "top down" approach takes a high level definition of the problem and subdivides it into subproblems, which you then do recursively until you're down to pieces that are obvious and easy to code. This is often associated with the "functional decomposition" style of programming, but needn't be.

Bottom to Up: In "bottom up" programming, you identify lower-level tools that you can compose to become a bigger program.

In reality, almost all programming is done with a combination of approaches. In OOPs, you commonly subdivide the problem by identifying domain objects (which is a top down step), and refining those, then recombining those into the final program — a bottom up step.

======
Overlapping Problems: When the data has to be calculated again due to recursion.. Just like Fibonacci series, then we can store the values that can be repeated again in the temporary array. OR we can use the memoization matrix

======
Cutting a rod problem to get maximum profit. Cut the rod of length 5 in such a way to get maximum profit
Length Profit
  1		 2
  2		 5
  3		 7
  4		 8
We create an array having rows for the lengths available and columns for the length provided. Profit = max(profit by including new piece, profit by not including new piece)

======
Staircase problem: At most m steps are allowed to climb one at a time. How many steps are needed to climb n number of steps. Calculate one by 1. Assume m to be 2. Calculating the steps to climb below stairs:
Ground 0 -> (1) = 1
Step 1 -> (1) = 1 
Step 2 -> (1,1) (2) = 2
Step 3 -> (1,1,1) (2,1) (1,2) = 3 .....
Similarly for others, basically n step number is dependent upon n-1 and n-2 as m is 2. If we look broadly the result shows a particular sequence that is Fibonacci series.

======
Minimum jump to reach end: Maximum jump can be equal to the value present at the index from where the jump has to be taken. It can be equal or less to the value present at that index. We maintain the two arrays i.e. Minimum jumps array(minimum jumps required to reach that index) and jump path array(maintaining the last index from where we have reached that index)
Main Array 		   = 2,1,3,2,3,4,5,1,2,8
Minimum Jump Array = 0,1,1,2,2,2,3,3,3,3
Jump Path Array    = -,0,0,2,2,2,4,4,5,5
Keep checking whether you are in range or not. Have two variables i and j. J will start from 0 for every increment of i. Whether the i placed index is in range from j by checking the value at index j. Time complexity for this is n2

=======
Weighted Job Scheduling: Need to find the job sequence for maximum profit. Each job has the start time, end time and profit value.
Job 1:  {1, 2, 50} 
Job 2:  {3, 5, 20}
Job 3:  {6, 19, 100}
Job 4:  {2, 100, 200}
Sort the jobs in increasing order of end time. Then create a array having the default values of profits set. Now have two variables i and j. i will start from 1 and for each value of i, j will start from 0 to i-1. We will check if it is in range or not. It is in range. Then sum the basic profit and put into the array, otherwise leave. You will get the maximum value at the end.
https://www.youtube.com/watch?v=cr6Ip0J9izc

=======
Convert a string into another string with minimum number of operations.
Make a two dimensional array having the width height as per the input string and expected string. Diagonal is replace, left to right is insert, top to bottom is remove. Now put the value which is minimum of the three (left, top, diagonal) + 1. If the value matches then just copy the same value on the diagonal element. The final value which will be at the last is the final answer.
https://www.youtube.com/watch?v=b6AGUjqIPsA

=======
Longest common subsequence: All the characters which are matching in the same order is the common subsequence. There can be more than 1 subsequence but we have to find the longest subsequence. LCS for input Sequences “ABCDGH” and “AEDFHR” is “ADH” of length 3. LCS for input Sequences “AGGTAB” and “GXTXAYB” is “GTAB” of length 4.

Let the input sequences be X[0..m-1] and Y[0..n-1] of lengths m and n respectively. And let L(X[0..m-1], Y[0..n-1]) be the length of LCS of the two sequences X and Y. Following is the recursive definition of L(X[0..m-1], Y[0..n-1]). If last characters of both sequences match (or X[m-1] == Y[n-1]) then L(X[0..m-1], Y[0..n-1]) = 1 + L(X[0..m-2], Y[0..n-2]). If last characters of both sequences do not match (or X[m-1] != Y[n-1]) then L(X[0..m-1], Y[0..n-1]) = MAX ( L(X[0..m-2], Y[0..n-1]), L(X[0..m-1], Y[0..n-2]) )
                         lcs("AXYT", "AYZX")
                       /                 \
         lcs("AXY", "AYZX")            lcs("AXYT", "AYZ")
         /                                        \              
lcs("AX", "AYZX") lcs("AXY", "AYZ")   lcs("AXY", "AYZ") lcs("AXYT", "AY")
In the above partial recursion tree, lcs(“AXY”, “AYZ”) is being solved twice

Create a 2D matrix. having one column and row extra and make all the elements as 0. Now start matching the row and column. If the row and column value is same then increment the box value by 1 + value from the diagonal box. If the value is not equal then the select the value which is maximum from the left box and top box. The last number in the row and column will represent the longest common subsequence length.

if(input1[i] == input2[j]){
	T[i][j] = T[i-1][j-1] + 1
}else{
	T[i][j]= max(T[i-1][j]), T[i][j-1])
}
https://www.youtube.com/watch?v=NnD96abizww

=======
Longest common substring: All the characters which are matching is the common substring.
Input : X = “abcdxyz”, y = “xyzabcd”
Output : 4
The longest common substring is “abcd” and is of length 4.

If last characters match, then we reduce both lengths by 1, LCSuff(X, Y, m, n) = LCSuff(X, Y, m-1, n-1) + 1 if X[m-1] = Y[n-1]. If last characters do not match, then result is 0, i.e., LCSuff(X, Y, m, n) = 0 if (X[m-1] != Y[n-1])
The maximum length Longest Common Suffix is the longest common substring. LCSubStr(X, Y, m, n) = Max(LCSuff(X, Y, i, j)) where 1 <= i <= m and 1 <= j <= n

It is little different but nearly same in finding the substring in place of subsequence. Create a 2D matrix. having one column and row extra and make all the elements as 0. Now start matching the row and column. If the row and column value is same then increment the box value by 1 + value from the diagonal box. If the value is not equal then make it 0. After completion find the largest number in the matrix.
https://www.youtube.com/watch?v=BysNXJHzCEs

=======
Longest increasing subsequence
arr 		        = 0 4 12 2 10 6 9 13 3 11 7 15
length		      = 1 2  3 2  3 3 4  5 3  5 4  6
sub sequence    = - 0  1 0  3 3 5  6 3  6 8  9
We initially fill the all the length elements as 1 as each individually can act as increasing subsequence. We will use two variables i and j. For every increment in i, j will start from 0th index. Now, for every i we check the j if it is more than j then value at i is incremented by value at j + 1, and value in sub sequence array for i index is j. Get the maximum value in the list and that is the length of the longest increasing subsequence.

=======
KMP(Knuth-Morris-Pratt) String search algorithm: By default if we use the basic search and find in the main string it will compare the whole string starting from each char. This will lead to time complexity of O(n*m). But we can achieve the searching in the time complexity of O(m+n) using KMP algorithm.
Sample input string: abcxabcdabxabcdabcdabcy
Pattern to search: abcdabcy . The main aim is to while matching the pattern if not found we should not go back and start searching there. So, we find if there is suffix in search pattern which is also the prefix till what we have searched. Now generating the array having the suffix prefix till that string.
a c b a c d a b c y
0 0 0 1 2 0 1 0 0 0

a b c d a b c a
0 0 0 0 1 2 3 1
j i
a a b a a b a a a
0 1 0 1 2 3 4 5 2
Comparing the char at i and j. If there is a match we have to set the value at i = j + 1 and increment both i and j and compared again. If there is a mismatch then go to previous char in the array, take the value of that array, and set j to arr[value] and compare again. If not matched repeat the same process until reached the 0th index. This array will help in finding the next comparison positions. The indexes in the array will help to start comparing from which index. You can jump that much indexes.
https://www.youtube.com/watch?v=GTJr8OvyEVQ

=======
Z algorithm finding a substring in a string or pattern matching: Let length of text be n and of pattern be m, then total time taken is O(m + n) with linear space complexity. Now we can see that both time and space complexity is same as KMP algorithm but this algorithm is Simpler to understand.
What is Z Array: For a string str[0..n-1], Z array is of same length as string. An element Z[i] of Z array stores length of the longest substring starting from str[i] which is also a prefix of str[0..n-1]. The first entry of Z array is meaning less as complete string is always prefix of itself.
Text             a   a   b   c   a   a   b   x   a   a   a   z
Z values         X   1   0   0   3   1   0   0   2   2   1   0 
Text             a   b   a   b   a   b   a   b
Z values         X   0   6   0   4   0   2   0
How is Z array helpful in Searching Pattern in Linear time: The idea is to concatenate pattern and text, and create a string “P$T” where P is pattern, $ is a special character should not be present in pattern and text, and T is text. Build the Z array for concatenated string. In Z array, if Z value at any point is equal to pattern length, then pattern is present at that point.
Pattern P = "aab",  Text T = "baabaa", The concatenated string is = "aab$baabaa"
Z array for above concatenated string is {x, 1, 0, 0, 0, 3, 1, 0, 2, 1}. Since length of pattern is 3, the value 3 in Z array indicates presence of pattern. 

Calculating Z index in O(n) time:
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18
a a b x a a b x c a a  b  x  a  a  b  x  a  y
X 1 0 0 4 1 0 0 0 8
First start matching the till the index 4. After index 4 we can directly copy the values from index 1 to 3. We would have checked if any value is exceeding the right bound or not. It will come later. Now start comparing. For index 8 value is 0. next, for index 9 value is 8. So, my idea is not to do any comparison for the characters from index 10 to 16 and directly use the values that are already calculated.
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18
a a b x a a b x c a a  b  x  a  a  b  x  a  y
X 1 0 0 4 1 0 0 0 8 1  0  0  5 
Now copying the values, but while copying the value to index 13 if we check 13 + 4 is exceeding the right bound i.e. 16, we will have to do further comparisons. For that I need to shift my left bound from 10 to 13. As we know that from a index 13 the value is 4 which already matched from 0 to 3, now further comparing we got to know the z value as 5. Again we transfer the values from index 1 to 4 to 14 to 17. But while copying the value at 4 we check the right bound which is just 1 less than the right bound. So now comparing index 18 with 1 which makes z value at 17 as 1. And then at index 18 z value is 0.
private int[] calculateZ(char input[]) {
    int Z[] = new int[input.length];
    int left = 0;
    int right = 0;
    for(int k = 1; k < input.length; k++) {
        if(k > right) {
            left = right = k;
            while(right < input.length && input[right] == input[right - left]) {
                right++;
            }
            Z[k] = right - left;
            right--;
        } else {
            //we are operating inside box
            int k1 = k - left;
            //if value does not stretches till right bound then just copy it.
            if(Z[k1] < right - k + 1) {
                Z[k] = Z[k1];
            } else { //otherwise try to see if there are more matches.
                left = k;
                while(right < input.length && input[right] == input[right - left]) {
                    right++;
                }
                Z[k] = right - left;
                right--;
            }
        }
    }
    return Z;
}
https://www.youtube.com/watch?v=CpZh4eF8QBw

=====
Rabin-Karp substring search algorithm: Find the hash value of the searched string and keep checking in the original string a substring by calculating hash of the substrings. The best way to generate hash value for all the substring is rolling hash function. String abeda. Let there be a prime number 101. and values of the string chars is ASCII values. hash of abe = 97 + 98*3^1 + 101*3^2. hash of bed = 98 + 101*3^1 + 101*3^2. The second has can be calculated easily using the first one. 
https://www.youtube.com/watch?v=H4VrKHVG5qI

======
Coin change problem. Using the different denominations, get the maximum number of ways in which a particular value can be created.
Created 2D array. One is having the denominations, and other having the values. One extra row and column too for 0.
Now how to find the maximum ways:
1) Exclude the new denominations
2) Include the new denominations
3) Add the both number of ways (1 and 2)
If row value is more than column value, just copy the value from above cell
	0	1	2	3	4	5
0|	1	0	0	0	0	0
1|	1	1	1	1	1	1
2|	1	1	2	2	3	3
3|	1	1	2	3	4	5
4|	1	1	2	3	5	6
5|	1	1	2	3	5	7
https://www.youtube.com/watch?v=PafJOaMzstY

======
Kadane's Algorithm: Largest Sum Contiguous Sub array
4, -3, -2, 2, 3, 1, -2, -3, 4, 2, -6, -3, -1, 3, 1, 2
Whenever you encounter value less then 0 while summing up the items, start from next item with 0 as starting sum. Also save the maximum value in separate variable.

=======
Subset Sum Problems: Available Set: {1,2,7,5}, Sum should be 8, find the values which can be picked to form the sum
The isSubsetSum problem can be divided into two subproblems
1) Include the last element, recur for n = n-1, sum = sum – set[n-1]
2) Exclude the last element, recur for n = n-1. This shows we can find the divide into sub problems.
Sorted the available sets and make a matrix having top to bottom as set values and left to right as sum values.
values\SUM. You need to check if the the value can be achieved using the previous value or it can be achieved using old value. isPoosible = (check old value) OR (check new value)
	0	1	2	3	4	5	6	7	8
0	1	0	0	0	0	0	0	0	0
1	1	1	0	0	0	0	0	0	0
2	1	1	1	1	0	0	0	0	0
5	1	1	1	1	0	1	1	1	1
7	1	1	1	1	0	1	1	1	1

======
Creating Zig Zag Array: Given an array of DISTINCT elements, rearrange the elements of array in zig-zag fashion in O(n) time. The converted array should be in form a < b > c < d > e < f. 
Input:  arr[] = {4, 3, 7, 8, 6, 2, 1}
Output: arr[] = {3, 7, 4, 8, 2, 6, 1}
Create a boolean variable. We will check the condition if the next element is less than the current value, if yes we mark the flag true. And the next element should be more than current value. If it is not more then we swap the values. And then compare again (not from starting). O(1) space complexity and O(n) time complexity

======
Magic Square Construction: Addition of every row,column and both the diagonals is a constant. Constant value can be found using formula n(n2 +1)/2 where n is the dimension of the matrix. The box will be filled from 1 to n2.
2 7 6
9 5 1
4 3 8 
1) 1 is stored at position (n/2, n-1). 
2) Keep changing the position from (i,j) -> (i-1, j+1)
3) If i = -1 -> i = n-1
4) If j = n -> j = 0
5) If (-1, n) is reached then change it to (0, n-2)
Consider i moving in anticlockwise direction and j moving in clockwise direction. and the circle has 0-n values. When i, j reached at the end or -1, then again initialized.

======
Total number of ways to reach a particular cell in a matrix: Create the array of same size. Then check in how many ways you can reach any cell in first column or first row. For the cell 1,1 you can reach from top or left. Add the values from top and left
1 1 1 1
1 2 3 4
1 3 6 10
1 4 10 20

======
Hamming distance: between the two strings of equal length is the number of positions at which the corresponding symbols are different. XOR each element with corresponding element at same position. If you don't get 0 then it is not matching and increment the counter of distance. Application: Error detection and correction in network.
int x = n1 ^ n2; 
int setBits = 0; 
while (x > 0){ 
    setBits += x & 1; 
    x >>= 1; 
} 
return setBits;

======
Huffman Coding: also called as Huffman Encoding is a famous greedy algorithm that is used for the lossless compression of data. It uses variable length encoding where variable length codes are assigned to all the characters depending on how frequently they occur in the given text. For representing a and b you need only 1 bit i.e. 0 and 1. If there is 3rd letter than 2nd bit is required. Text: abbcdbcccdccaecfeccc. We need 3 bits to store 8 values mentioned below
Letter  Frequency  Probability Bits/Letter
	a		    2			        .1		3*2=6
	b		    3			        .15		3*3=9
	c		    10		        .5		3*10=30
	d		    2			        .1		3*2=6
	e		    2			        .1		3*2=6
	f		    1			        .05		3*1=3
			   20					          Total 60 bits are required.
Here the letters can be represented using the 3 bits.
Now arrange the letters as per the probability: f a d e b c. Make f and a as leafs of a tree whose node is sum of the probability of both. then join that node with other node d and make a new parent node with sum of these two node and keep doing this. Now assign the left node as 0 and right node as 1 of each node. Keep doing this. Now f which is at bottom will be represented using 0 and 1 is 00000(5 bits used). Similarly calculate for other, you will get to know number of bits used. Answer comes out to be 45 bits. We can save 15 bits. 
https://www.youtube.com/watch?v=fFO3R7-sBfA

======
Get minimum from stack in O(n): We will have another supporting stack. When we keep putting the value in main stack, we put the that value if value is less than any value in supporting stack. like first value put in the main stack is 40, then 40 is added also in the supporting stack. When popped if the value popped from main stack is same as supporting stack then pop from supporting stack too.
 
======
0/1 Knapsack problem: 0/1 means it will pick or will not. There are some weights given and corresponding values for it. We have to find the maximum value with minimum weights sum up to given weight. 
We can solve this solution by breaking up the problem. Consider all subsets of items, there can be two cases for every item: (1) the item is included in the optimal subset, (2) not included in the optimal set. Maximum value obtained by n-1 items and W weight (excluding nth item). 2) Value of nth item plus maximum value obtained by n-1 items and W minus weight of the nth item.
Sort item with weights. Make a memorization matrix having column side the weights/values and row side the sum of the weights 0, 1, 2, 4
					Sum of weight ->      0	1	2	3	4	5	6	7	8
				                      1	0	1	1	1	1	1	1	1	1
          value/weight	      2	0	1	4	5	5	5	5	5	5
	                       			3	0	1	4	5	5	8	9	9	9
				                      4	0	1	4	5	5	8	9 10 10
So to have the sum using 1,2,3,4 weights the maximum value we get is 10.
 
======
Longest Palindrome subsequence: Given a string, find the longest substring which is palindrome. For example, if the given string is “forgeeksskeegfor”, the output should be “geeksskeeg”.

Generic Solution:
// Every single character is a palindrome of length 1
L(i, i) = 1 for all indexes i in given sequence
// IF first and last characters are not same
If (X[i] != X[j])  L(i, j) =  max{L(i + 1, j),L(i, j - 1)} 
// If there are only 2 characters and both are same
Else if (j == i + 1) L(i, j) = 2  
// If there are more than two characters, and first and last 
// characters are same
Else L(i, j) =  L(i + 1, j - 1) + 2

// Using dynamic programming: As their are number of subproblems that are overlapping
			   L(0, 5)
             /        \ 
            /          \  
        L(1,5)          L(0,4)
       /    \            /    \
      /      \          /      \
  L(2,5)    L(1,4)  L(1,4)  L(0,3)
In the above partial recursion tree, L(1, 4) is being solved twice. If we draw the complete recursion tree, then we can see that there are many subproblems which are solved again and again. Create a 2 dimensional matrix. FIrst take l=0, means taking 1 char at a time. They will be always the palindrome of length 1. Now l=2. as a !=g the max palindrome in ag will be 1. Keep doing for l=2 for all values then do for l=3. agb as a!= b we can divide into max(ag, gb) = 1. Lets take bdb. here b==b, so we can write 2+ max(d) = 3. Now take l=4.
	a  g  b  d  b  a  
a   1  1  1  1  3  5
g      1  1  1  3  3
b         1  1  3  3
d            1  1  1
b               1  1
a                  1
Now how to get the subsequence by using the matrix. Here 5(0,5) is highest add that aa. Now in between 5 has come from diagonal 3. That 3 has come from (2,4) so add that abba. Now check diagonal 1. It has come from nowhere so add (3,3) abdba.
Note: It is like we are going from bottom to up. Starting from l=0 bottom to l=size up.
if(input[i] == input[j]){
	T[i][j] = T[i+1][j-1] +2
}else{
	T[i][j] = max(T[i+1][j],T[i][j-1])
}

========
Longest palindrome substring: We can you the above method to get the longest palindrome substring. In place of writing the values we write the boolean values that if the string is palindrome or not. Just we need to check the outer two chars and rest will be provided by the matrix. For ex. take l=1, every char will be palindrome of itself. Fill all the a[0][0] like as T. Now, l=2, ag, as a!=g not a palindrome. So put false. All values are false in this example. Now, l=3, agb, check a!=b so not a palindrome. Take bdb. As b==b check a[3][3] in array, if it a palindrome. If yes put T. Now l=4, agbd a!=d so not a palindrome. All the values are false in this example. l=5, agbdb, a!=b no need to check internally so not a palindrome. Now the values which are T in the matrix are the palindrome. Fetch and check the length. The value having the maximum length is the answer.
	a  g  b  d  b  a  
a   T  F  F  F  F  F
g      T  F  F  F  F
b         T  F  T  F
d            T  F  F
b               T  F
a                  T
https://www.youtube.com/watch?v=Fi5INvcmDos

========
Longest palindrome substring (Manacher's algorithm): The whole concept is related to mirroring. We use here the # and and we then try to find the number of items present in the palindrome. In this the value under first # is 0, as there is no palindrome. Moving to A. Now expanding to left and right of A gives us the value as 1 because there is one character on either side of A which when combined with A will gives us palindrome i.e. #A#. So we store 1 in the array. As we have found the palindrome we will update our mirror line and make it point to A. We also set L and R marker to 1 and 3 where the palindrome starts and where it ends respectively.
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
$ # A # B # A # B # A  #  B  #  A  #  @
0 0 1 
  L M R
Then we move to i to next char i.e. #. We realize that char[i] and R are same. Basically, char[i] does not lie within the boundary of R. So, mirroring property does not work here. So we expand and get as 0 as A != B. Then we move to char[i] = B. As it is outside the scope of mirror property we expand and get as 3 #a#b#a#. There are 3 char which are on either side of b. We then check if palindrome centered at i is beyond the previous R. It is, so we move the center M to i and accordingly R moves ahead.
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
$ # A # B # A # B # A  #  B  #  A  #  @
0 0 1 0 3
  L     M     R
Now move i to position 5, the mirror for it lies at position 3 as i lies within the boundary of R. So we can definitely copy the value from position 3 to 5 and then we try to expand. As B != A. We check if i is beyond R. It is not. So no need to shift the center. So center remains at B. Moving i = 6 and i lies within the boundary of R, we can directly copy the mirror length from position 2 i.e. 1. We know know that the palindrome centered at i is having at least 1 char on either side. So, now we have to expand. We compare directly B at position 4 and 8 and continue doing it. And we check if palindrome centered at i=6 moves beyond the boundary R. It does. So we have to move the center from position 4 to position 6 and R to position 11.
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
$ # A # B # A # B # A  #  B  #  A  #  @
0 0 1 0 3 0 5
  L         M          R
Now we move i to position 7. As i is withing the boundary of R. We can directly copy mirror value from position 5 i.e. 0 and then try to expand where A!=B. So we move the i to 8. As it lies within the boundary we directly copy the mirror value from position 4 i.e. 3. Then we expand and it covers the whole array except at the ends. Now we check does it expands beyond the boundary of M. Yes, it does. So we shift the center to B at 8 and set the R to the last. 
0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
$ # A # B # A # B # A  #  B  #  A  #  @ == T
0 0 1 0 3 0 5 0 7 0 5  0  3  0  1  0  0 == P
  L             M                     R
Keep doing this...

// initializing temp array
int[] P = new int[T.length];

// making C as center and R as Right boundary
int C = 1, R = 0;

// Looping till end of the array
for(int i=1; i< T.length-1; i++){

	// getting the mirror
	int mirr = 2*C - i; [This is because we have added # in between]

	// check if current index is inside the boundary of R
	if(i < R){
		// If yes than copy the minimum value either from R-i or from the mirror value
		P[i] = Math.min(R-i, P[mirror]);
	}

	// expanding and checking the opposite values
	// if same then increment the temp array value
	while(T[i + (1 + P[i])] == T[i - (1 + P[i])]){
		P[i]++;
	}

	// change the center and the R boundary if the new palindrome is out of R boundary
	if(i + P[i] > R){
		C = i;
		R = i + P[i];
	}
}
https://www.youtube.com/watch?v=nbTSfrEfo6M

======
Matrix multiplication: There are two ways of calculating matrix multiplication for below example 
[2,3] [3,6] [6,4] [4,5]
  0     1     2     3
1) (01)(23) = 2*3*6 + 6*4*5 + 2*6*5 = 36 + 120 + 60 = 216
2) ((01)2)3 = 2*3*6 + 2*6*4 + 2*4*5 = 36 + 48 + 40 = 124
for (0...3) = Min(0(123),(01)(23),(012)3) = Min(2*3*5 + 132, 2*6*5 + 36, 84 + 2*4*5) = Min(162, 216, 124) = 124
	0	1	2	3
0	0	36	84  124
1		0	72	132
2			0	120
3				0
https://www.youtube.com/watch?v=vgLJZMUfnsU

======
Box stacking: You are given a set of n types of rectangular 3-D boxes, where the i^th box has height h(i), width w(i) and depth d(i) (all real numbers). You want to create a stack of boxes which is as tall as possible, but you can only stack a box on top of another box if the dimensions of the 2-D base of the lower box are each strictly larger than those of the 2-D base of the higher box(both length and width). Of course, you can rotate a box so that any side functions as its base. It is also allowable to use multiple instances of the same type of box.
Let there be 2 boxes of l w h : 1 2 4, 3 2 5. We write down the rotations of the boxes having length > width. And calculate the area. sort them according to area. Why we are sorting as per area as if the box having high area is put above the box having less area then it will go out of that box.
4 2 1   5 3 2 
4 1 2		5 2 3 
2 1 4		4 2 1
5 3 2		3 2 5
3 2 5		4 1 2
5 2 3		2 1 4
Now use the technique used in finding longest increasing subsequence. Create two arrays and one for finding the maximum height and another to save indexes of which boxes to use. save heights of the possibilities in those array.
2 3 1 5 2 4
0 0 0 0 0 0
Now check if the ith box size can be put onto the jth. if yes include the height and update the array index. Keep doing this and keep updating the index array.
https://www.youtube.com/watch?v=9mod_xRB-O0

======
Word problem: Given an input string and a dictionary of words, find out if the input string can be segmented into a space-separated sequence of dictionary words. {i, like, sam, sung, samsung, mobile, ice, cream, icecream, man, go, mango}. Input: ilike. Output: yes
Create a matrix of size n x n where n is length of input string. First check char by char if that char is present in the dictionary. Then take 2 char at a time and check if they are present in the dictionary. Break that work into 2 char, and check separately if that single char is present in the dictionary. Keep updating the array. Keep on doing for 3, 4 char at a time. Value at the top right in the array will be the answer.
https://www.youtube.com/watch?v=WepWFGxiwRs

======
Find the longest path in a matrix with given constraints: Given a n*n matrix where all numbers are distinct, find the maximum length path (starting from any cell) such that all cells along the path are in increasing order with a difference of 1. We can move in 4 directions from a given cell (i, j), i.e., we can move to (i+1, j) or (i, j+1) or (i-1, j) or (i, j-1) with the condition that the adjacent cells have a difference of 1.
Use dynamic programming: since all numbers are unique and in range from 1 to n*n, there is at most one possible direction from any cell
// Function that returns length of the longest path beginning with mat[i][j] This function mainly uses lookup table dp[n][n] 
static int findLongestFromACell(int i, int j, int mat[][], int dp[][]) { 
    // Base case 
    if (i<0 || i>=n || j<0 || j>=n) 
        return 0; 
    // If this subproblem is already solved 
    if (dp[i][j] != -1) 
        return dp[i][j]; 
    // Since all numbers are unique and in range from 1 to n*n, 
    // there is atmost one possible direction from any cell
    // if right one is in sequence 
    if (j<n-1 && ((mat[i][j] +1) == mat[i][j+1])) 
        return dp[i][j] = 1 + findLongestFromACell(i,j+1,mat,dp); 
    // if left one is in sequence 
    if (j>0 && (mat[i][j] +1 == mat[i][j-1])) 
        return dp[i][j] = 1 + findLongestFromACell(i,j-1,mat,dp); 
    // if top one is in sequence 
    if (i>0 && (mat[i][j] +1 == mat[i-1][j])) 
        return dp[i][j] = 1 + findLongestFromACell(i-1,j,mat,dp); 
    // if bottom one is in sequence 
    if (i<n-1 && (mat[i][j] +1 == mat[i+1][j])) 
        return dp[i][j] = 1 + findLongestFromACell(i+1,j,mat,dp);
    // If none of the adjacent fours is one greater 
    return dp[i][j] = 1; 
} 
// Function that returns length of the longest path beginning with any cell 
static int finLongestOverAll(int mat[][]) { 
    // Initialize result 
    int result = 1;   
    // Create a lookup table and fill all entries in it as -1 
    int[][] dp = new int[n][n]; 
    for(int i=0;i<n;i++) 
        for(int j=0;j<n;j++) 
            dp[i][j] = -1; 
    // Compute longest path beginning from all cells 
    for (int i=0; i<n; i++) { 
        for (int j=0; j<n; j++) { 
            if (dp[i][j] == -1) 
                findLongestFromACell(i, j, mat, dp); 
            //  Update result if needed 
            result = Math.max(result, dp[i][j]); 
        } 
    } 
    return result; 
} 

======
Egg dropping puzzle: Suppose that we wish to know which stories in a 36-story building are safe to drop eggs from, and which will cause the eggs to break on landing. We make a few assumptions: An egg that survives a fall can be used again. A broken egg must be discarded. The effect of a fall is the same for all eggs. If an egg breaks when dropped, then it would break if dropped from a higher floor. If an egg survives a fall then it would survive a shorter fall. It is not ruled out that the first-floor windows break eggs, nor is it ruled out that the 36th-floor do not cause an egg to break. If i have 10 floors and 1 egg, for the worst case scenario, it will take 10 attempts to find out from which floor it is gonna break. We have to find minimum number of attempts to find from which floor egg will break. 
There are two cases: If egg breaks from the floor then we have to work with the floors below that floor and with remaining eggs(n-1). But if it doesn't break then we have to work with floors above that floor with same number of eggs. So, for any floor the minimum number of attempts to find is = k ==> Number of floors, n ==> Number of Eggs
eggDrop(n, k) ==> Minimum number of trials needed to find the critical floor in worst case.
eggDrop(n, k) = 1 + min{max(eggDrop(n - 1, x - 1), eggDrop(n, k - x)): x in {1, 2, ..., k}}.
Since we need to minimize the number of trials in worst case, we take the maximum of two cases. Sample input is 2 eggs and six floors. Create a 2D array having floors in row and column as eggs. If there is only 1 egg then to find the number of attempts at floor would be same as number of floors in worst case scenario. For eggs 2 at number 1 floor equation becomes = 1 + max(arr[2][0] = 0 , arr[0][2] = 0). For number 2 floor we have two options: 1st, egg is dropped from 1st floor and take permutations(egg break and not break), 2nd, egg is dropped from 2nd floor egg break or not. Whichever has the minimum value will be taken into account. Similarly for 3rd need to find for all the 3 floors.
	1	2		3			4			5		       6
1	1	2		3			4			5		 	   6 	
2	1 (2,2)  (3,2,3)	(3,3,3,4)  (4,3,3,4,5)	  (4,4,3,4,5,6)
https://www.youtube.com/watch?v=3hcaVyX00_4
https://www.geeksforgeeks.org/egg-dropping-puzzle-dp-11/

======
Given a big file containing billions of numbers. How can you find the 10 maximum numbers from that file? Always remember that when need to find n elements, best data structure to use is priority queue. Make batches of 1000, Use the heapSort to get top 10 from each batch and then heapify them again.

======
Merge k sorted lists with total n elements
- take one list, merge with second, then merge result with third... O(nk) Space: O(1)
- take pairs of the lists and merge them, in 1st go you will get k/2 lists, then k/4....Time Complexity: O(nlogn) Space: O(n)
- Use heapify. Take the first element from every list and get minimum. Then remove min from heap. Take next value from the same list from which min is extracted. O(nLogk) Space: O(k)

======
Generate all the strings of length n drawn from 0 to k-1. 
It can be done easily using recursively
void nString(int length, String x){
	if(length<1){
		print(x);
	}else{
		for(int i=0; i< k; i++){
			nString(length-1, x + i);
		}
	}
}

======
N people decided to elect a leader by arranging themselves in a circle and eliminating every mth person around the circle, closing ranks as each person drops out. Find which person will be the last one remaining one(with rank 1)
Use a circular linked list and after moving m times remove.

======
Hanoi Puzzle: Tower of Hanoi is a mathematical puzzle where we have three rods and n disks. The objective of the puzzle is to move the entire stack to another rod, obeying the following simple rules:
1) Only one disk can be moved at a time.
2) Each move consists of taking the upper disk from one of the stacks and placing it on top of another stack i.e. a disk can only be moved if it is the uppermost disk on a stack.
3) No disk may be placed on top of a smaller disk.
- Here we have to divide the problem into, if there is only one item transfer from source to destination directly. Transfer n-1 items from source to auxiliary rod and then transfer those auxiliary rod to destination.
Algorithm:
tower(n, s, a , d){
    if(n==1){
      print(S->D)
      return
    }
    tower(n-1, s, d, a)
    print(S->A)
    tower(n-1, a, d, s)
    return
}

======
If N students in a class play a game against each other where each student plays against all other students in the class, find the total number of matches to be conducted. Also, if the class leader has to arrange the students in a line where each student would have lost the match with the student in front of him (Remember: student may or may not have won the match with the student front of front of him). Design a suitable data structure for maintaining such an order.
- It will be nC2. We will arrange the students in the required manner using a Binary Search tree. Take any student as the root node. Now, for every student who has lost to the student in the tree we create a left child and place him there. Insert all the students following the standard BST insertion. The inorder traversal of the tree will give us the required order of the students.

======
Optimal Strategy for a Game: We play a game against an opponent by alternating turns. In each turn, a player selects either the first or last coin from the row, removes it from the row permanently, and receives the value of the coin. Determine the maximum possible amount of money we can definitely win if we move first.
Ex. 1. 5, 3, 7, 10 :The user collects maximum value as 15(10 + 5). 2. 8, 15, 3, 7 : The user collects maximum value as 22(7 + 15)

There are two choices:
1) The user chooses the ith coin with value Vi: The opponent either chooses (i+1)th coin or jth coin. The opponent intends to choose the coin which leaves the user with minimum value. The user can collect the value Vi + min(F(i+2, j), F(i+1, j-1))
2) The user chooses the jth coin with value Vj: The opponent either chooses ith coin or (j-1)th coin. The opponent intends to choose the coin which leaves the user with minimum value. i.e. The user can collect the value Vj + min(F(i+1, j-1), F(i, j-2) )
So, we can write: F(i, j) represents the maximum value the user can collect from i'th coin to j'th coin.
F(i, j)  = Max(Vi + min(F(i+2, j), F(i+1, j-1) ), Vj + min(F(i+1, j-1), F(i, j-2) ))
https://www.geeksforgeeks.org/optimal-strategy-for-a-game-dp-31/

Another way is create a memoization matrix of size n*n. Now we have to break it like in arr[i][i] means if i have a array of only 1 item then the first player will have that value and other will have 0. Similarly for other spaces. 
Input array: 3,9,1,2. Here at position (1,1) is (3,0) meaning first player will have value 3 then 2nd will have 0.
		1		2		3		4
1	  (3,0)	  (9,3)	  (4,9)	 (11,4)
2			  (9,0)   (9,1)	 (10,2)	  
3					  (1,0)	  (2,1)
4							  (2,0)
After checking the positions where i==j. We now take the array from 1 to 2 meaning i=1 and j=2. We need to find and compare the values if user1 takes the 3 and when takes 9. If user takes 3 it means for i=2,j=2 user needs to take the minimum value, so it would be 0, so 3 + 0 = 3. If user takes 9 it means for i=1,j=1 user needs to take minimum that would be 0, so 9 + 0 =9. Out of 3 and 9, 9 is max so we write for i=1,j=2 as (9,3)
Formula is T[i][j].first = max(T[i+1][j].second + Value[i], T[i+1][j].second + Value[j])
https://www.youtube.com/watch?v=WxpIHvsu1RI

======
Dice problem: Given n dice each with m faces, numbered from 1 to m, find the number of ways to get sum X. X is the summation of values on each face when all the dice are thrown.
The function can be represented as:
Sum(m, n, X) = Finding Sum (X - 1) from (n - 1) dice plus 1 from nth dice
               + Finding Sum (X - 2) from (n - 1) dice plus 2 from nth dice
               + Finding Sum (X - 3) from (n - 1) dice plus 3 from nth dice
                  ...................................................
                  ...................................................
                  ...................................................
               + Finding Sum (X - m) from (n - 1) dice plus m from nth dice
It becomes the dynamic programming problem as some of the subset overlap. It can be solved using the 2 dimensional array the rows having the number of dice used and columns having the sum which can be achieved in number of ways.
https://www.geeksforgeeks.org/dice-throw-dp-30/

======
URBANCLAP
100 people stand in a circle in order 1 to 100. No. 1 has a sword. He kills the next person (i.e. No. 2) and gives the sword to the next living person (i.e. No. 3). All people do the same until only 1 survives. Which number survives to the end?
- Examine what happens when the number of 'players' is a 2n number, as in 2, 4, 8, 16 etc. You will notice that in this case the person who starts, player 1, is also the last person to survive. The significance of the powers of 2 is that these can halve without a remainder. Hence if the number of players is a power of 2 the survivor will be the person who starts the game.
Now consider: when we have a game with something other than a power of 2 players as we kill people, the number of players will necessarily reduce to be a power of two. At that point the survivor will be the person holding the sword. Effectively the first player in a game with 2n players.
In our example starting with 100 players - we need to kill 36 of them to get down to a power of 2 (64). Since we kill every other person starting at player 2 the last person we need to die is player 72, they will be killed by player 71 and the first person in the effective power of 2 game, who will win is player 73.

======
Integer partition problem / coin change problem: Given a value N, if we want to make change for N cents, and we have infinite supply of each of S = { S1, S2, .. , Sm} valued coins, how many ways can we make the change? The order of coins doesn’t matter. For example, for N = 4 and S = {1,2,3}, there are four solutions: {1,1,1,1},{1,1,2},{2,2},{1,3}. So output should be 4. For N = 10 and S = {2, 5, 3, 6}, there are five solutions: {2,2,2,2,2}, {2,2,3,3}, {2,2,6}, {2,3,5} and {5,5}. So the output should be 5.
Make a memoization matrix having vertical side as the coins available and horizontal as total sum you want starting from 0. Now each item will be called as number of ways of making total sum 5 while including and excluding the current coin. If we include current coin, subtract the value from the total sum and check the corresponding part of the memoization matrix. If exclude then take the value above that. 
https://www.youtube.com/watch?v=PafJOaMzstY&t=898s

======
Similar question as above, we need to find the minimum number of coins that can be used to achieve the desired sum. In this memoization matrize we need to take the value which is minimum of(including the current denomination coin, excluding the current denomination coin)
https://www.youtube.com/watch?v=Y0ZqKpToTic

======
Sieve of Eratosthenes: The sieve of Eratosthenes is one of the most efficient ways to find all primes smaller than n when n is smaller than 10 million or so. We take an array of size n. Starting from value 2. we calculate the square of the number and then start marking the multiple of that value from that number as 0. We do this till we get the number whose square is greater than n. Numbers left are the prime numbers.
https://www.youtube.com/watch?v=I6HrVRGGYNI

======
