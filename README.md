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
     



