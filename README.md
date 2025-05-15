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
### 2697. Lexicographically Smallest Palindrome
[Leetcode link](https://leetcode.com/problems/lexicographically-smallest-palindrome/description/)
<br>
You are given a string s consisting of lowercase English letters, and you are allowed to perform operations on it. In one operation, you can replace a character in s with another lowercase English letter.
Your task is to make s a palindrome with the minimum number of operations possible. If there are multiple palindromes that can be made using the minimum number of operations, make the lexicographically smallest one.
A string a is lexicographically smaller than a string b (of the same length) if in the first position where a and b differ, string a has a letter that appears earlier in the alphabet than the corresponding letter in b.
Return the resulting palindrome string.

Example 1:
Input: s = "egcfe"
Output: "efcfe"
Explanation: The minimum number of operations to make "egcfe" a palindrome is 1, and the lexicographically smallest palindrome string we can get by modifying one character is "efcfe", by changing 'g'.

Example 2:
Input: s = "abcd"
Output: "abba"
Explanation: The minimum number of operations to make "abcd" a palindrome is 2, and the lexicographically smallest palindrome string we can get by modifying two characters is "abba".

Example 3:
Input: s = "seven"
Output: "neven"
Explanation: The minimum number of operations to make "seven" a palindrome is 1, and the lexicographically smallest palindrome string we can get by modifying one character is "neven". 

Constraints:
1 <= s.length <= 1000
s consists of only lowercase English letters.

```java
class Solution {
    public String makeSmallestPalindrome(String s) {
        StringBuilder str = new StringBuilder();
        for(int i=0;i<s.length();i++)
        {
            if(s.charAt(i)==s.charAt(s.length()-i-1)) str.append(s.charAt(i));
            else
            {
                if(s.charAt(i)<s.charAt(s.length()-i-1)) str.append(s.charAt(i));
                else str.append(s.charAt(s.length()-i-1));
            }
        }
        return str.toString();

    }
}
```
- Check if the two character that is first and last is equal or not if it is equal then we append the character.
- Otherwise we check the minimum one then we append the minimum one to the stringbuilder.
- Finally we return the stringbuilder as a string using the toString() method.
### 1827. Minimum Operations to Make the Array Increasing
[Leetcode link](https://leetcode.com/problems/minimum-operations-to-make-the-array-increasing/)
<br>
You are given an integer array nums (0-indexed). In one operation, you can choose an element of the array and increment it by 1.
For example, if nums = [1,2,3], you can choose to increment nums[1] to make nums = [1,3,3].
Return the minimum number of operations needed to make nums strictly increasing.
An array nums is strictly increasing if nums[i] < nums[i+1] for all 0 <= i < nums.length - 1. An array of length 1 is trivially strictly increasing.

Example 1:
Input: nums = [1,1,1]
Output: 3
Explanation: You can do the following operations:
1) Increment nums[2], so nums becomes [1,1,2].
2) Increment nums[1], so nums becomes [1,2,2].
3) Increment nums[2], so nums becomes [1,2,3].

Example 2:
Input: nums = [1,5,2,4,1]
Output: 14

Example 3:
Input: nums = [8]
Output: 0

Constraints:
1 <= nums.length <= 5000
1 <= nums[i] <= 104

```java
class Solution {
    public int minOperations(int[] nums) {
        int sum = 0;
        for(int i=0;i<nums.length-1;i++)
        {
            if(nums[i]>=nums[i+1]) 
            {
                sum+=(nums[i]-nums[i+1])+1;
                nums[i+1]=nums[i]+1;
            }
        }
        return sum;
    }
}
```
- in this code we create array that must be in strictly increasing sequence.
- So what we do is whenever the first element is greater than or equal to the second element then we find the difference between the two elements and add 1 to the sum
- And also change the second element value by first (element+1)
### 561. Array Partition
[Leetcode link](https://leetcode.com/problems/array-partition/)
<br>
Given an integer array nums of 2n integers, group these integers into n pairs (a1, b1), (a2, b2), ..., (an, bn) such that the sum of min(ai, bi) for all i is maximized. Return the maximized sum.

Example 1:
Input: nums = [1,4,3,2]
Output: 4
Explanation: All possible pairings (ignoring the ordering of elements) are:
1. (1, 4), (2, 3) -> min(1, 4) + min(2, 3) = 1 + 2 = 3
2. (1, 3), (2, 4) -> min(1, 3) + min(2, 4) = 1 + 2 = 3
3. (1, 2), (3, 4) -> min(1, 2) + min(3, 4) = 1 + 3 = 4
So the maximum possible sum is 4.

Example 2:
Input: nums = [6,2,6,5,1,2]
Output: 9
Explanation: The optimal pairing is (2, 1), (2, 5), (6, 6). min(2, 1) + min(2, 5) + min(6, 6) = 1 + 2 + 6 = 9.

Constraints:
1 <= n <= 104
nums.length == 2 * n
-104 <= nums[i] <= 104

```java
class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int sum=0;
        for(int i=0;i<nums.length-1;i+=2)
        {
            sum+=Math.min(nums[i],nums[i+1]);
        }
        return sum;
    }
}
```
- In this code we form a pair.
- we add the minimum of the each pair to the sum and return the sum as a answer.
- So how we must maximaize the sum.
- What we can do is first we sort the array then only we get the maximum sum
- because we get the minimum to the next immediate number.
### 1974. Minimum Time to Type Word Using Special Typewriter
[Leetcode link](https://leetcode.com/problems/minimum-time-to-type-word-using-special-typewriter/)
<br>
There is a special typewriter with lowercase English letters 'a' to 'z' arranged in a circle with a pointer. A character can only be typed if the pointer is pointing to that character. The pointer is initially pointing to the character 'a'.
![](https://assets.leetcode.com/uploads/2021/07/31/chart.jpg)
<br>
Each second, you may perform one of the following operations:
Move the pointer one character counterclockwise or clockwise.
Type the character the pointer is currently on.
Given a string word, return the minimum number of seconds to type out the characters in word.
 
Example 1:
Input: word = "abc"
Output: 5
Explanation: 
The characters are printed as follows:
- Type the character 'a' in 1 second since the pointer is initially on 'a'.
- Move the pointer clockwise to 'b' in 1 second.
- Type the character 'b' in 1 second.
- Move the pointer clockwise to 'c' in 1 second.
- Type the character 'c' in 1 second.

Example 2:
Input: word = "bza"
Output: 7
Explanation:
The characters are printed as follows:
- Move the pointer clockwise to 'b' in 1 second.
- Type the character 'b' in 1 second.
- Move the pointer counterclockwise to 'z' in 2 seconds.
- Type the character 'z' in 1 second.
- Move the pointer clockwise to 'a' in 1 second.
- Type the character 'a' in 1 second.
  
Example 3:
Input: word = "zjpc"
Output: 34
Explanation:
The characters are printed as follows:
- Move the pointer counterclockwise to 'z' in 1 second.
- Type the character 'z' in 1 second.
- Move the pointer clockwise to 'j' in 10 seconds.
- Type the character 'j' in 1 second.
- Move the pointer clockwise to 'p' in 6 seconds.
- Type the character 'p' in 1 second.
- Move the pointer counterclockwise to 'c' in 13 seconds.
- Type the character 'c' in 1 second.

Constraints:
1 <= word.length <= 100
word consists of lowercase English letters.

```java
class Solution {
    public int minTimeToType(String word) {
        int ans = word.length();
        if(word.charAt(0)<='m') ans+=Math.abs('a'-word.charAt(0));
        else ans+=26-Math.abs('a'-word.charAt(0));
        for(int i=0;i<word.length()-1;i++)
        {
            if(Math.abs(word.charAt(i)-word.charAt(i+1))>13)
            {
                System.out.println(26-Math.abs(word.charAt(i)-word.charAt(i+1)));
                ans+=26-Math.abs(word.charAt(i)-word.charAt(i+1));
            }
            else 
            {
                System.out.println(Math.abs(word.charAt(i)-word.charAt(i+1)));
                ans+=Math.abs(word.charAt(i)-word.charAt(i+1));
            }
        }
        return ans;
    }
}
```
- in this code we give a minimum time to type the string
- in the ans first i declare the length of the string because 1 second will take for ftype the word we must type the each letter in the string so each will take one second.
- then initially the pointer will point the letter 'a' so first we move the pointer to the first letter of the word so if the first letter is less than the 'm' we add the abs of the 'a' and the first word.
- Other wise we subract the abs value to the 26
- because it will rotate in counter clock wise.
- in the innerside of the loop the abs of the adjacent letters is greater than the value of 13 we will subract the abs value from 26
- Other wise we straigtly add the abs vlaue to the ans.
**NOTE : The noted abs value in the above describtion is abs(adjacent element letters)**
### 409. Longest Palindrome
[Leetcode link](https://leetcode.com/problems/longest-palindrome/?envType=problem-list-v2&envId=greedy&status=TO_DO&difficulty=EASY)
<br>
Given a string s which consists of lowercase or uppercase letters, return the length of the longest 
palindrome that can be built with those letters. Letters are case sensitive, for example, "Aa" is not considered a palindrome.
Example 1:
Input: s = "abccccdd"
Output: 7
Explanation: One longest palindrome that can be built is "dccaccd", whose length is 7.
Example 2:
Input: s = "a"
Output: 1
Explanation: The longest palindrome that can be built is "a", whose length is 1.
Constraints:
1 <= s.length <= 2000
s consists of lowercase and/or uppercase English letters only.
```java
class Solution {
    public int longestPalindrome(String s) {
        int[] arr = new int[58];
        int l = s.length(),f=0;
        for(int i=0;i<s.length();i++) arr[s.charAt(i)-'A']++;
        for(int i=0;i<58;i++){
            if(arr[i]%2!=0){
                if(f==0) f=1;
                else l--;
            }
        }
        return l;
    }
}
```
### 56. Merge Intervals
[Leetcode link](https://leetcode.com/problems/non-overlapping-intervals/)
<br>
Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.

 

Example 1:

Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
Example 2:

Input: intervals = [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
 

Constraints:

1 <= intervals.length <= 104
intervals[i].length == 2
0 <= starti <= endi <= 104

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        int c = 0;
        List<List<Integer>> list = new ArrayList<>();
        for(int row[]:intervals)
        {
            List<Integer> innerlist = new ArrayList<>();
            for(int x:row)
            {
                innerlist.add(x);
            }
            list.add(innerlist);
        }
        list.sort((a, b) -> {
            if (!a.get(1).equals(b.get(1))) return Integer.compare(a.get(1), b.get(1));
            else return Integer.compare(a.get(0), b.get(0)); 
        });
        int end = list.get(0).get(1);
        for(int i=1;i<list.size();i++)
        {
            if(list.get(i).get(0)<end) c++;
            else end = list.get(i).get(1);
        }
        return c;
    }
}
```
- Tor reduce the overlaping interval and minimize this count first we sort the interval depends on the end time.
- Then if the next interval's start value is less than the end value then that should must removed so remove that other wise change the end value by the current intervals end value.
> [REference](https://www.youtube.com/watch?v=HDHQ8lAWakY)
### 2429. Minimize XOR
[Leetcode link](https://leetcode.com/problems/minimize-xor/?envType=daily-question&envId=2025-01-15)
<br>
Given two positive integers num1 and num2, find the positive integer x such that:

x has the same number of set bits as num2, and
The value x XOR num1 is minimal.
Note that XOR is the bitwise XOR operation.

Return the integer x. The test cases are generated such that x is uniquely determined.

The number of set bits of an integer is the number of 1's in its binary representation.

 

Example 1:

Input: num1 = 3, num2 = 5
Output: 3
Explanation:
The binary representations of num1 and num2 are 0011 and 0101, respectively.
The integer 3 has the same number of set bits as num2, and the value 3 XOR 3 = 0 is minimal.
Example 2:

Input: num1 = 1, num2 = 12
Output: 3
Explanation:
The binary representations of num1 and num2 are 0001 and 1100, respectively.
The integer 3 has the same number of set bits as num2, and the value 3 XOR 1 = 2 is minimal.
 

Constraints:

1 <= num1, num2 <= 109

```java
class Solution {
    public int minimizeXor(int num1, int num2) {
        int count = 0;
        while(num2>0){
            num2 = (num2 & (num2-1));
            count++;
        }
        int res=0;
        for(int i=31;i>=0 && count>0;i--){
            if((num1 & (1<<i)) != 0){
                count--;
                res += (1<<i);
            }
        }
        for(int i=0;i<32 && count>0;i++){
            if((num1 & (1<<i)) == 0)
            {
                count--;
                res += (1<<i);
            } 
        }
        return res;
    }
}
```
- First to find the number of set bits in num2 with the optimal way.
- Then from the right to left that is in num1 setbits then we set that bit in the res also and the remaining set bit will set from the right to left for the purpose of reduce the value.
> [Reference](https://www.youtube.com/watch?v=zSuIRdCuRmw)

### 2900. Longest Unequal Adjacent Groups Subsequence I
[Leetcode link](https://leetcode.com/problems/longest-unequal-adjacent-groups-subsequence-i/?envType=daily-question&envId=2025-05-15)
<br>
You are given a string array words and a binary array groups both of length n.

A subsequence of words is alternating if for any two consecutive strings in the sequence, their corresponding elements at the same indices in groups are different (that is, there cannot be consecutive 0 or 1).

Your task is to select the longest alternating subsequence from words.

Return the selected subsequence. If there are multiple answers, return any of them.

Note: The elements in words are distinct.

 

Example 1:

Input: words = ["e","a","b"], groups = [0,0,1]

Output: ["e","b"]

Explanation: A subsequence that can be selected is ["e","b"] because groups[0] != groups[2]. Another subsequence that can be selected is ["a","b"] because groups[1] != groups[2]. It can be demonstrated that the length of the longest subsequence of indices that satisfies the condition is 2.

Example 2:

Input: words = ["a","b","c","d"], groups = [1,0,1,1]

Output: ["a","b","c"]

Explanation: A subsequence that can be selected is ["a","b","c"] because groups[0] != groups[1] and groups[1] != groups[2]. Another subsequence that can be selected is ["a","b","d"] because groups[0] != groups[1] and groups[1] != groups[3]. It can be shown that the length of the longest subsequence of indices that satisfies the condition is 3.

 

Constraints:

1 <= n == words.length == groups.length <= 100
1 <= words[i].length <= 10
groups[i] is either 0 or 1.
words consists of distinct strings.
words[i] consists of lowercase English letters.
```java
class Solution {
    public List<String> getLongestSubsequence(String[] words, int[] groups) {
        int max = 0;
        List<String> ans = new ArrayList<>();
        for(int i=0;i<groups.length;i++)
        {
            List<String> temp = new ArrayList<>();
            temp.add(words[i]);
            int prev = groups[i];
            for(int j=i+1;j<groups.length;j++)
            {
                if(prev != groups[j])
                {
                    temp.add(words[j]);
                    prev = groups[j];
                }
            }
            if(ans.size()<temp.size())
            {
                ans.clear();
                ans = new ArrayList<>(temp);
            }
        }
        return ans;
    }
}
```
