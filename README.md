# Greedy_Algorithm
### 455. Assign Cookies
[LeetCode link](https://leetcode.com/problems/assign-cookies/description/)
<br>
Assume you are an awesome parent and want to give your children some cookies. But, you should give each child at most one cookie.
Each child i has a greed factor g[i], which is the minimum size of a cookie that the child will be content with; and each cookie j has a size s[j]. If s[j] >= g[i], we can assign the cookie j to the child i, and the child i will be content. Your goal is to maximize the number of your content children and output the maximum number.

Example 1:
Input: g = [1,2,3], s = [1,1]
Output: 1
Explanation: You have 3 children and 2 cookies. The greed factors of 3 children are 1, 2, 3. 
And even though you have 2 cookies, since their size is both 1, you could only make the child whose greed factor is 1 content.
You need to output 1.

Example 2:
Input: g = [1,2], s = [1,2,3]
Output: 2
Explanation: You have 2 children and 3 cookies. The greed factors of 2 children are 1, 2. 
You have 3 cookies and their sizes are big enough to gratify all of the children, 
You need to output 2.
 
Constraints:
1 <= g.length <= 3 * 104
0 <= s.length <= 3 * 104
1 <= g[i], s[j] <= 231 - 1

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(s);
        Arrays.sort(g);
        int child_count=0;
        int index=0;
        for(int i=0;i<g.length;i++)
        {
            for(int j=index;j<s.length;j++)
            {
                if(g[i]<=s[j])
                {
                    child_count++;
                    index=j+1;
                    break;
                }
            }
        }
        return child_count;
    }
}
```
- g is the childrens greed value.
- s is the cookies values
- so say for example g=[1 5 3 3 4] s=[4 2 1 2 1 3]
- first we sort both array
- g=[1 3 3 4 5] s=[1 1 2 2 3 4]
- then we iterate each childrens greedy and check wheather we satisfy the children or not 1<=1 so count=1.
- 3<=3 so count=2.
- 4<=4 so count=3
- We did not satisfy the second 3 and 5 so count = 3.
> [Reference](https://www.youtube.com/watch?v=DIX2p7vb9co&list=PLgUwDviBIf0rF1w2Koyh78zafB0cz7tea&index=1)
### 860. Lemonade Change
[Leetcode Link](https://leetcode.com/problems/lemonade-change/description/)
<br>
At a lemonade stand, each lemonade costs $5. Customers are standing in a queue to buy from you and order one at a time (in the order specified by bills). Each customer will only buy one lemonade and pay with either a $5, $10, or $20 bill. You must provide the correct change to each customer so that the net transaction is that the customer pays $5.
Note that you do not have any change in hand at first.
Given an integer array bills where bills[i] is the bill the ith customer pays, return true if you can provide every customer with the correct change, or false otherwise.

Example 1:
Input: bills = [5,5,5,10,20]
Output: true
Explanation: 
From the first 3 customers, we collect three $5 bills in order. From the fourth customer, we collect a $10 bill and give back a $5. From the fifth customer, we give a $10 bill and a $5 bill.
Since all customers got correct change, we output true.

Example 2:
Input: bills = [5,5,10,10,20]
Output: false
Explanation: 
From the first two customers in order, we collect two $5 bills.
For the next two customers in order, we collect a $10 bill and give back a $5 bill.
For the last customer, we can not give the change of $15 back because we only have two $10 bills.
Since not every customer received the correct change, the answer is false.
 
Constraints:
1 <= bills.length <= 105
bills[i] is either 5, 10, or 20.

```java
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int count1=0,count2=0;
        for(int i=0;i<bills.length;i++){
            if(bills[i]==5) count1++;
            else if(bills[i]==10){
                if(count1>0){
                    count2++;
                    count1--;
                }
                else return false;
            }
            else{
                if(count2>0 && count1>0){
                    count2--;
                    count1--;
                }
                else if(count1>2) count1=count1-3;
                else return false;
            }
        }
        return true;
    }
}
```
- count1 will count the 5 and count2 will count the 10 iterate through all the elements in bills array we check if bills[i] is 5 then we didnot return any amount so we simply increase the count1.
- if bills[i] is 10 then we return 5 to the customer (10-5=5) so we check if (count1 will greater than zero if it is then increase count2 by one and decrease count1 by one) else ( return false) because we did not return the amount.
- if bills[i] is 20 then we return 15 to the customer (20-5 = 15) so check count1 and count2 is greater than zero if both are greater than zero then we decrease the counts by one
- other wise we check count1 will greater that 2 so we give three five ruppes
- both case are not satisfy then we return false. 
> [Reference](https://www.youtube.com/watch?v=n_tmibEhO6Q&list=PLgUwDviBIf0rF1w2Koyh78zafB0cz7tea&index=2)

### Shortest Job first
[GeeksforGeeks link](https://www.geeksforgeeks.org/problems/shortest-job-first/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=shortest-job-first)
<br>
Geek is a software engineer. He is assigned with the task of calculating average waiting time of all the processes by following shortest job first policy.
The shortest job first (SJF) or shortest job next, is a scheduling policy that selects the waiting process with the smallest execution time to execute next.
Given an array of integers bt of size n. Array bt denotes the burst time of each process. Calculate the average waiting time of all the processes and return the nearest integer which is smaller or equal to the output.
Note: Consider all process are available at time 0.

Example 1:

Input:
n = 5
bt = [4,3,7,1,2]
Output: 4
Explanation: After sorting burst times by shortest job policy, calculated average waiting time is 4.

Example 2:
Input:
n = 4
arr = [1,2,3,4]
Output: 2
Explanation: After sorting burst times by shortest job policy, calculated average waiting time is 2.
Your Task:
You don't need to read input or print anything. Your task is to complete the function solve() which takes bt[] as input parameter and returns the average waiting time of all the processes.

Expected Time Complexity: O(nlog(n))
Expected Auxiliary Space: O(1)

Constraints:
1 <= n <= 105
1 <= arr[i] <= 105

```java
class Solution {
    static int solve(int bt[] ) {
    // code here
    int t=0,w=0;
    Arrays.sort(bt);
    for(int i=0;i<bt.length;i++)
    {
        w=w+t;
        t=t+bt[i];
    }
    return w/bt.length;
  }
}
```
> [Reference](https://www.youtube.com/watch?v=3-QbX1iDbXs&list=PLgUwDviBIf0rF1w2Koyh78zafB0cz7tea&index=3)
### 55. Jump Game
[lrrtcode link](https://leetcode.com/problems/jump-game/description/)
<br>
You are given an integer array nums. You are initially positioned at the array's first index, and each element in the array represents your maximum jump length at that position.
Return true if you can reach the last index, or false otherwise.

Example 1:
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.

Example 2:
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.

```java
class Solution {
    public boolean canJump(int[] nums) {
        int max_index=0;
        for(int i=0;i<nums.length;i++)
        {
            if(i>max_index) return false;
            max_index=Math.max(max_index,i+nums[i]);
        }
        return true;
    }
}
```
- in this code we return true if we cross the array otherwise return false
- initially maxindex is 0
- iterate througth the elements in the array find the maximum index jump
- if the iteration is greater than the maxindex then we return false because i cross the one element but we did not reach means we did not jump the element.
> [Refrence](https://youtu.be/tZAa_jJ3SwQ?si=voKd7n9VTLDRRNzJ)
### 2037. Minimum Number of Moves to Seat Everyone
[Leetcode link](https://leetcode.com/problems/minimum-number-of-moves-to-seat-everyone/)
<br>
There are n availabe seats and n students standing in a room. You are given an array seats of length n, where seats[i] is the position of the ith seat. You are also given the array students of length n, where students[j] is the position of the jth student.
You may perform the following move any number of times:
Increase or decrease the position of the ith student by 1 (i.e., moving the ith student from position x to x + 1 or x - 1)
Return the minimum number of moves required to move each student to a seat such that no two students are in the same seat.
Note that there may be multiple seats or students in the same position at the beginning.

Example 1:
Input: seats = [3,1,5], students = [2,7,4]
Output: 4
Explanation: The students are moved as follows:
- The first student is moved from from position 2 to position 1 using 1 move.
- The second student is moved from from position 7 to position 5 using 2 moves.
- The third student is moved from from position 4 to position 3 using 1 move.
In total, 1 + 2 + 1 = 4 moves were used.

Example 2:
Input: seats = [4,1,5,9], students = [1,3,2,6]
Output: 7
Explanation: The students are moved as follows:
- The first student is not moved.
- The second student is moved from from position 3 to position 4 using 1 move.
- The third student is moved from from position 2 to position 5 using 3 moves.
- The fourth student is moved from from position 6 to position 9 using 3 moves.
In total, 0 + 1 + 3 + 3 = 7 moves were used.

```java
class Solution {
    public int minMovesToSeat(int[] seats, int[] students) {
        Arrays.sort(seats);
        Arrays.sort(students);
        int sum=0;
        for(int i=0;i<students.length;i++){
            sum=sum+Math.abs(seats[i]-students[i]);
        }
        return sum;
    }
}
```
- In this code we return the minimum no of position that the students move to sit the seat.
- so seats array is position of seats and the students array is the position of the students position.
- So we sort both array. Then the first seat is for the first student so we find the difference of the each pair we get the minimum position 
> [Reference](https://www.youtube.com/watch?v=wS7Ag33hf8E)
### Fractional Knapsack
[Geeksfrgeeks link]()
<br>
Given weights and values of n items, we need to put these items in a knapsack of capacity w to get the maximum total value in the knapsack. Return a double value representing the maximum value in knapsack.
Note: Unlike 0/1 knapsack, you are allowed to break the item here. The details of structure/class is defined in the comments above the given function.

Examples :
Input: n = 3, w = 50, value[] = [60,100,120], weight[] = [10,20,30]
Output: 240.000000
Explanation: Take the item with value 60 and weight 10, value 100 and weight 20 and split the third item with value 120 and weight 30, to fit it into weight 20. so it becomes (120/30)*20=80, so the total value becomes 60+100+80.0=240.0 Thus, total maximum value of item we can have is 240.00 from the given capacity of sack. 
Input: n = 2, w = 50, value[] = [60,100], weight[] = [10,20]
Output: 160.000000
Explanation: Take both the items completely, without breaking. Total maximum value of item we can have is 160.00 from the given capacity of sack.

```java
class Solution {
    double fractionalKnapsack(int w, Item arr[], int n) {
        // Create an array of indices sorted by value-to-weight ratio in descending order
        Integer[] indices = new Integer[n];
        for (int i = 0; i < n; i++) {
            indices[i] = i;
        }
        Arrays.sort(indices, new Comparator<Integer>() {
            public int compare(Integer i1, Integer i2) {
                double r1 = (double) arr[i1].value / arr[i1].weight;
                double r2 = (double) arr[i2].value / arr[i2].weight;
                return Double.compare(r2, r1); // Sort in descending order
            }
        });
        
        double totalValue = 0.0;
        int currentWeight = 0;
        
        for (int i = 0; i < n; i++) {
            int idx = indices[i];
            if (currentWeight + arr[idx].weight <= w) {
                currentWeight += arr[idx].weight;
                totalValue += arr[idx].value;
            } else {
                int remain = w - currentWeight;
                totalValue += arr[idx].value * ((double) remain / arr[idx].weight);
                break;
            }
        }
        
        return totalValue;
    }
}
```
- In this code first sort the arr Items by one value That is per weight calucalation.
- After sort the arr items iterate over the loop check if current+arr[idx] weight is lesser than the maximum weight.
- else we find remain
- add the remain weight value to the tatal value.
> [Reference](https://www.youtube.com/watch?v=1ibsQrnuEEg)
### 678. Valid Parenthesis String
[Leetcode link](https://leetcode.com/problems/valid-parenthesis-string/description/)
<br>
Given a string s containing only three types of characters: '(', ')' and '*', return true if s is valid.
The following rules define a valid string:
Any left parenthesis '(' must have a corresponding right parenthesis ')'.
Any right parenthesis ')' must have a corresponding left parenthesis '('.
Left parenthesis '(' must go before the corresponding right parenthesis ')'.
'*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string "".

Example 1:
Input: s = "()"
Output: true

Example 2:
Input: s = "(*)"
Output: true

Example 3:
Input: s = "(*))"
Output: true
#### Recursive Solution
```java
class Solution {
    public boolean checkValidString(String s) {
        int c=0;
        int star=0;
        for(int i=0;i<s.length();i++) if(s.charAt(i)=='*') star++;
        if(star>=s.length()) 
        {
            if(star%2==0) return true;
            else return false;
        }
        boolean t=check(s,0,0);
        return t;
        //open +1 close -1.
    }
    public boolean check(String s,int index,int count)
    {
        if(count<0) return false;
        if(index>=s.length()) return true && (count==0);
        if(s.charAt(index)=='(') return check(s,index+1,count+1);
        else if(s.charAt(index)==')') return check(s,index+1,count-1);
        else return check(s,index+1,count+1) || check(s,index+1,count-1) || check(s,index+1,count);
    }
}
```
#### Greedy Solution
```java
class Solution {
    public boolean checkValidString(String s) {
        int leftmin=0;
        int leftmax=0;
        for(int i=0;i<s.length();i++){
            if(s.charAt(i)=='('){
                leftmin++;
                leftmax++;
            }
            else if(s.charAt(i)==')'){
                leftmin--;
                leftmax--;
            }
            else{
                leftmin--;
                leftmax++;
            }
            if(leftmax<0) return false;
            if(leftmin<0) leftmin=0;
        }
        return leftmin==0;
        
    }
}
```
> [Refernce](https://www.youtube.com/watch?v=QhPdNS143Qg&t=587s)
### 1221. Split a String in Balanced Strings
[Leetcode Link](https://leetcode.com/problems/split-a-string-in-balanced-strings/)
<br>
Balanced strings are those that have an equal quantity of 'L' and 'R' characters. Given a balanced string s, split it into some number of substrings such that: Each substring is balanced.
Return the maximum number of balanced strings you can obtain.

Example 1:
Input: s = "RLRRLLRLRL"
Output: 4
Explanation: s can be split into "RL", "RRLL", "RL", "RL", each substring contains same number of 'L' and 'R'.

Example 2:
Input: s = "RLRRRLLRLL"
Output: 2
Explanation: s can be split into "RL", "RRRLLRLL", each substring contains same number of 'L' and 'R'.
Note that s cannot be split into "RL", "RR", "RL", "LR", "LL", because the 2nd and 5th substrings are not balanced.

Example 3:
Input: s = "LLLLRRRR"
Output: 1
Explanation: s can be split into "LLLLRRRR".

```java
class Solution {
    public int balancedStringSplit(String s) {
        int ans=0;
        int current_count=0;
        for(int i=0;i<s.length();i++){
            if(current_count==0) ans++;
            if(s.charAt(i)=='R') current_count++;
            else current_count--;
        }
        return ans;
        
    }
}
```
- In this code we return the maximum satisfying string.
- Maximum meaning (equal no of R and L )
- So if R then increase the current count and L decrease the current count.
- Whenever it reaches to zero then that is consider to be a satisfying string so increase the ans then return the ans.
### 2160. Minimum Sum of Four Digit Number After Splitting Digits
[leetcode link](https://leetcode.com/problems/minimum-sum-of-four-digit-number-after-splitting-digits/)
<br>
You are given a positive integer num consisting of exactly four digits. Split num into two new integers new1 and new2 by using the digits found in num. Leading zeros are allowed in new1 and new2, and all the digits found in num must be used.
For example, given num = 2932, you have the following digits: two 2's, one 9 and one 3. Some of the possible pairs [new1, new2] are [22, 93], [23, 92], [223, 9] and [2, 329].
Return the minimum possible sum of new1 and new2.

Example 1:
Input: num = 2932
Output: 52
Explanation: Some possible pairs [new1, new2] are [29, 23], [223, 9], etc.
The minimum sum can be obtained by the pair [29, 23]: 29 + 23 = 52.

Example 2:
Input: num = 4009
Output: 13
Explanation: Some possible pairs [new1, new2] are [0, 49], [490, 0], etc. 
The minimum sum can be obtained by the pair [4, 9]: 4 + 9 = 13.

```java
class Solution {
    public int minimumSum(int num) {
        int[] digit = new int[10];
        while(num>0)
        {
            digit[num%10]++;
            num/=10;
        }
        int h1=0,h2=0;
        int f=1;
        for(int i=0;i<10;i++){
            while(digit[i]>0){
                if(f==1){
                    h1=(h1*10)+i;   
                    f=0;
                }
                else{
                    h2=(h2*10)+i;
                    f=1;
                }
                digit[i]--;
            }
        }
        return h1+h2;
    }
}
```
- We can use the two smallest digits out of the four as the digits found in the tens place respectively.
- Similarly, we use the final 2 larger digits as the digits found in the ones place.
- So from the first first smaller digit in h1 and second smaller digit in h2 simultaneously changing.
- After completing the loop we return the sum of the h1 and h2.
### 2864. Maximum Odd Binary Number
[Leetcode link](https://leetcode.com/problems/maximum-odd-binary-number/description/)
<br>
You are given a binary string s that contains at least one '1'.You have to rearrange the bits in such a way that the resulting binary number is the maximum odd binary number that can be created from this combination.Return a string representing the maximum odd binary number that can be created from the given combination.Note that the resulting string can have leading zeros.

Example 1:
Input: s = "010"
Output: "001"
Explanation: Because there is just one '1', it must be in the last position. So the answer is "001"

Example 2:
Input: s = "0101"
Output: "1001"
Explanation: One of the '1's must be in the last position. The maximum number that can be made with the remaining digits is "100". So the answer is "1001".

```java
class Solution {
    public String maximumOddBinaryNumber(String s) {
        int one=0;
        StringBuilder str = new StringBuilder();
        for(int i=0;i<s.length();i++){
            if(s.charAt(i)=='1') one++;
        }
        for(int i=0;i<s.length()-1;i++){
            if(one>1) {
                str.append('1');
                one--;
            }
            else str.append('0');
        }
        str.append('1');
        return str.toString();
    }
}
```
- The binary representation of an odd number contains '1' in the least significant place.
- From the above hint we easily find that if we return the odd integer then the last digit is must be a one
- If we return the maximum odd integer then the remaining ones are in the front of the string
- In that information we count the one from the given string and store in variable one then (one-1) ones are in the front of the string the remaining place are zeros except the final place
- And return the string.
### 1323. Maximum 69 Number
[Leetcode link](https://leetcode.com/problems/maximum-69-number/)
<br>
You are given a positive integer num consisting only of digits 6 and 9.Return the maximum number you can get by changing at most one digit (6 becomes 9, and 9 becomes 6).

Example 1:
Input: num = 9669
Output: 9969
Explanation: 
Changing the first digit results in 6669.
Changing the second digit results in 9969.
Changing the third digit results in 9699.
Changing the fourth digit results in 9666.
The maximum number is 9969.

Example 2:
Input: num = 9996
Output: 9999
Explanation: Changing the last digit 6 to 9 results in the maximum number.

Example 3:
Input: num = 9999
Output: 9999
Explanation: It is better not to apply any change.

Constraints:
1 <= num <= 104
num consists of only 6 and 9 digits.

```java
class Solution {
    public int maximum69Number (int num) {
        String s1 = Integer.toString(num);
        int change = 0;
        StringBuilder s2 = new StringBuilder(); 
        for(int i=0;i<s1.length();i++)
        {
            if(s1.charAt(i)=='6' && change==0)
            {
                s2.append('9');
                change=1;
            } 
            else s2.append(s1.charAt(i));
        }
        return Integer.parseInt(s2.toString());  
    }
}
```
- In this code we change any one digit then it will be the maximum.
- Only 6 and 9 in the num
- first we convert the num to string
- Then create a empty stringbuilder.
- Iterate the string when we find the first 6 that time we appdend the 9 otherwise we append the same char in string (s1).
- It will occur only one time so i use change variable to track it.
- After finish the loop convert string builder to string using toString
- And convert the string to Integer using Integer.parseInt().
### 135. Candy
[Leetcode link](https://leetcode.com/problems/candy/)
<br>
There are n children standing in a line. Each child is assigned a rating value given in the integer array ratings.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy. Children with a higher rating get more candies than their neighbors. Return the minimum number of candies you need to have to distribute the candies to the children.

Example 1:

Input: ratings = [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.

Example 2:
Input: ratings = [1,2,2]
Output: 4
Explanation: You can allocate to the first, second and third child with 1, 2, 1 candies respectively.
The third child gets 1 candy because it satisfies the above two conditions.

```java
class Solution {
    public int candy(int[] ratings) {
        int[] l = new int[ratings.length];
        int[] r = new int[ratings.length];
        Arrays.fill(l,1);
        Arrays.fill(r,1);
        for(int i=1;i<ratings.length;i++)
        {
            if(ratings[i]<ratings[i-1]) 
            {
                if(l[i-1]<=l[i]) l[i-1]=l[i]+1;
            }
            else if(ratings[i]>ratings[i-1]) 
            {
                if(l[i]<=l[i-1]) l[i]=l[i-1]+1;
            }
        }
        for(int i=ratings.length-1;i>0;i--)
        {
            if(ratings[i]<ratings[i-1]) 
            {
                if(r[i-1]<=r[i]) r[i-1]=r[i]+1;
            }
            else if(ratings[i]>ratings[i-1]) 
            {
                if(r[i]<=r[i-1]) r[i]=r[i-1]+1;
            }
        }
        int sum=0;
        for(int i=0;i<l.length;i++)
        {
            sum=sum+Math.max(l[i],r[i]);
        }
        return sum;
    }
}
```
- In this program we return the minimum no of candies.
- So right to left and left to right we assign the candies
- find the maximum of these two arrays we find the sum and return it
- Why we iterate both right to left and left to right.
- ex see the note.
> [Reference](https://www.youtube.com/watch?v=h6_lIwZYHQw)
### 3016. Minimum Number of Pushes to Type Word II
[Leetcode link](https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii/description/?envType=daily-question&envId=2024-08-06)
<br>
You are given a string word containing lowercase English letters.
Telephone keypads have keys mapped with distinct collections of lowercase English letters, which can be used to form words by pushing them. For example, the key 2 is mapped with ["a","b","c"], we need to push the key one time to type "a", two times to type "b", and three times to type "c" .
It is allowed to remap the keys numbered 2 to 9 to distinct collections of letters. The keys can be remapped to any amount of letters, but each letter must be mapped to exactly one key. You need to find the minimum number of times the keys will be pushed to type the string word.
Return the minimum number of pushes needed to type word after remapping the keys.
An example mapping of letters to keys on a telephone keypad is given below. Note that 1, *, #, and 0 do not map to any letters.

Input: word = "abcde"
Output: 5
Explanation: The remapped keypad given in the image provides the minimum cost.
"a" -> one push on key 2
"b" -> one push on key 3
"c" -> one push on key 4
"d" -> one push on key 5
"e" -> one push on key 6
Total cost is 1 + 1 + 1 + 1 + 1 = 5.
It can be shown that no other mapping can provide a lower cost.
Example 2:
Input: word = "aabbccddeeffgghhiiiiii"
Output: 24
Explanation: The remapped keypad given in the image provides the minimum cost.
"a" -> one push on key 2
"b" -> one push on key 3
"c" -> one push on key 4
"d" -> one push on key 5
"e" -> one push on key 6
"f" -> one push on key 7
"g" -> one push on key 8
"h" -> two pushes on key 9
"i" -> one push on key 9
Total cost is 1 * 2 + 1 * 2 + 1 * 2 + 1 * 2 + 1 * 2 + 1 * 2 + 1 * 2 + 2 * 2 + 6 * 1 = 24.
It can be shown that no other mapping can provide a lower cost.
Example 3:
Input: word = "xyzxyzxyzxyz"
Output: 12
Explanation: The remapped keypad given in the image provides the minimum cost.
"x" -> one push on key 2
"y" -> one push on key 3
"z" -> one push on key 4
Total cost is 1 * 4 + 1 * 4 + 1 * 4 = 12
It can be shown that no other mapping can provide a lower cost.
Note that the key 9 is not mapped to any letter: it is not necessary to map letters to every key, but to map all the letters.

```java
class Solution {
    public int minimumPushes(String word) {
        int[] a1 = new int[26];
        for(int i=0;i<word.length();i++) a1[word.charAt(i)-'a']++;
        ArrayList<Integer> a2 = new ArrayList<>();
        for(int i=0;i<26;i++) if(a1[i]>0) a2.add(a1[i]);
        Collections.sort(a2);
        Collections.reverse(a2);
        for(int i=0;i<a2.size();i++) System.out.print(a2.get(i));
        int sum = 0;
        for(int i=0;i<a2.size();i++) sum = sum+(i/8+1)*a2.get(i);
        return sum;
    }
}
```
- In this code we totally have 8 buttons first. So the maximum number of frequency letter should be in the first then only we reduce our pushes.
- So what we do is find the each letter frequency. Then sort them in desending order because higher frequency element go to second then our pushes must be doubled.
- Our aim is to minimize the pushes. So after sort the frequency in descending order then first eight letters we pust one time so (i/8+1) = 1 * frequency of letter.
- the next eight buttons we push two times so (i/8) = 1 + 1 = 2 * frequency of the letter.
- The next eight buttons we push three times so (i/8)+1 = 3 * frequency of the letter.
- the next three buttons we push four times so (i/8)+1 = 4 * frequency of the letter.
- finaaly we add all the pushes and return it.
> [Refernce](https://www.youtube.com/watch?v=gvaYi6X6SQw&t=184s)


 

 
 
     



