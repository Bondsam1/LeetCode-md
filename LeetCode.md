# LeetCode

**DAY1 2019.5.13 Mon**

## No.1 Add Two Numbers

Question:

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)

Output: 7 -> 0 -> 8

Explanation: 342 + 465 = 807.
```

Code:

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        def form(l: ListNode):
            a = l.val
            #print(a)
            i=10
            while l.next:
                l=l.next
                a+=l.val*i
                #print(a,i)
                i=i*10
            return a
        b = form(l1)+form(l2)
        #print(b)
        aff = []
        aff.append(b%10)
        while b>=10:
            b//=10
            aff.append(b%10)
        #print(aff)
        res=ListNode(aff[0])
        node=res
        for item in aff[1:]:
            node.next = ListNode(item)
            node=node.next
        return res
```
Result:

> Runtime: 84 ms, faster than 75.64% of Python3 online submissions for Add Two Numbers.
Memory Usage: 13.4 MB, less than 5.21% of Python3 online submissions for Add Two Numbers.

Way:

_create a function to transform the link into array, then add the two numbers and transform the result to the link_

Improve:

_maybe it's better not to transform, do the calculation in the form of link_
**DAY1 2019.5.16 Thu**

```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        bool run_loop = true;
        int div_mod = 0; 
        ListNode *curr, *result = new ListNode(0);
        
        curr = result;
        
        while (run_loop) {
            int sum = (l1 ? l1->val : 0) + (l2 ? l2->val : 0);
            div_mod = sum + curr->val >= 10 ? 1 : 0;
            curr->val = (curr->val + sum) % 10;
            if ((l1 && l1->next) || (l2 && l2->next) || div_mod) {
                curr->next = new ListNode(div_mod);
                curr = curr->next;
            }
            else {
                run_loop = false;    
            }
            
            l1 = (l1 && l1->next) ? l1->next : NULL;
            l2 = (l2 && l2->next) ? l2->next : NULL;
        }
        
        return result;
    }
};
```


Sum:

- how to build a LinkNode

	`LinkNode(x)`
	
- take the special case into consideration, in this case [0][0]


## No.2 Two Sum

Question:

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

Code:

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int>a;
        for(int i=0;i<nums.size();i++){
            for(int j=i+1;j<nums.size();j++){
                if(nums[i]+nums[j]==target){
                    a.push_back(i);
                    a.push_back(j);
                }
            }
        }
    return a;
    }
};
```

Result:

> Runtime: 348 ms</br>
Memory Usage: 9.4 MB

Way:

_simply add select one number from the array and add it with the rest_

Improve:

_maybe using the hash table will help_

Sum:

- get familiar with the vector

**DAY1 2019.5.14 Tue**

## No.3 Reverse Integer

Question:

Given a 32-bit signed integer, reverse digits of an integer.

```
Example 1:

Input: 123
Output: 321
Example 2:

Input: -123
Output: -321
Example 3:

Input: 120
Output: 21
```

Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

Code:

```
class Solution {
public:
    int reverse(int x) {
        if (x>=2147483648 || x<-2147483648) {
            return 0;
        }
        else {
            long res = 0;
            while(x){
                long a = x%10;
                x/=10;

                res += a;
                res *=10;
            }
            res/=10;
            if (res>=2147483648 || res<-2147483648) {
                return 0;
            }
            else{
            return res;}
        }
    }
};
```

Result:

> Runtime: 4 ms, faster than 98.32% of C++ online submissions for Reverse Integer.
>  
> Memory Usage: 8.4 MB, less than 96.56% of C++ online submissions for Reverse Integer.

Improve:

_it seems there's no need to improve_

Way:

use a to store the poped number, then add it to the res and *10, repeat

**DAY1 2019.5.15 Wes**

## No.4 Palindrome Number

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

```
Example 1:

Input: 121
Output: true
Example 2:

Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
Example 3:

Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

Code:

```
class Solution:
    def isPalindrome(self, x: int) -> bool:
        y=x
        res=0
        if x<0:
            return False
        else:
            while x:
                k=x%10
                x=x//10
                res+=k
                res*=10
            res//=10
            print(res)
            return res==y
```

Result:

> Runtime: 88 ms, faster than 78.88% of Python3 online submissions for Palindrome Number.
> 
Memory Usage: 13.2 MB, less than 58.90% of Python3 online submissions for Palindrome Number.

Improve:

_somehow it cannot be run in c++, the code could perform better in c++_

Way:

use stack mathematically, if the reversed number is as same as the original one, return true

**2019.5.17 Fri**

## No.5 Roman to Integer

Question:

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.
```
Example 1:

Input: "III"
Output: 3
Example 2:

Input: "IV"
Output: 4
Example 3:

Input: "IX"
Output: 9
Example 4:

Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
Example 5:

Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

Code:

```
class Solution {
public:
    int romanToInt(string s) {
        int res = 0;
        map<char,int> T ={{'I',1},
                          {'V',5},
                          {'X',10},
                          {'L',50},
                          {'C',100},
                          {'D',500},
                          {'M',1000}
                         };
        int sum = T[s.back()];
        for(int i = s.length()-1;i>=0;i--){
            if(T[s[i]]>T[s[i-1]]){
                sum-=T[s[i-1]];
            }
            else{
                sum+=T[s[i-1]];
            }
        }
        return sum;
    }
};
```

Result:

> Runtime: 20 ms, faster than 84.40% of C++ online submissions for Roman to Integer.
Memory Usage: 11.1 MB, less than 63.03% of C++ online submissions for Roman to Integer.

Way:

Using map
If the later character is bigger, minus the former one;
Else add the former one;

**2019.5.19 Sun**

## No.6 Remove All Adjacent Duplicates In String


Question:

Given a string S of lowercase letters, a duplicate removal consists of choosing two adjacent and equal letters, and removing them.

We repeatedly make duplicate removals on S until we no longer can.

Return the final string after all such duplicate removals have been made.  It is guaranteed the answer is unique.

 
```
Example 1:

Input: "abbaca"
Output: "ca"
Explanation: 
For example, in "abbaca" we could remove "bb" since the letters are adjacent and equal, and this is the only possible move.  The result of this move is that the string is "aaca", of which only "aa" is possible, so the final string is "ca".
```

Code:

```
class Solution {
public:
    string removeDuplicates(string S) {
        // detect the adjacent and equal letters
        int i = 0;
        while(i<S.length()){
            int j = 0;
            int k = i;
            while(S[k]==S[k+1]){
                k++;
                j++;
            }
            if(j){
                S.erase(i,2);
                i=0;
                }
            else{i++;}
        }
        return S;
    }
};
```

Way:

use a while to search for the longest duplicated string, then use another to repeat

notice: after one erase, the detector must be initialized

## No.7 Last Stone Weight

Question:

We have a collection of rocks, each rock has a positive integer weight.

Each turn, we choose the two heaviest rocks and smash them together.  Suppose the stones have weights x and y with x <= y.  The result of this smash is:

If x == y, both stones are totally destroyed;
If x != y, the stone of weight x is totally destroyed, and the stone of weight y has new weight y-x.
At the end, there is at most 1 stone left.  Return the weight of this stone (or 0 if there are no stones left.)

 
```
Example 1:

Input: [2,7,4,1,8,1]
Output: 1
Explanation: 
We combine 7 and 8 to get 1 so the array converts to [2,4,1,1,1] then,
we combine 2 and 4 to get 2 so the array converts to [2,1,1,1] then,
we combine 2 and 1 to get 1 so the array converts to [1,1,1] then,
we combine 1 and 1 to get 0 so the array converts to [1] then that's the value of last stone.
```

Code:

```
class Solution:
    def lastStoneWeight(self, stones: List[int]) -> int:
        def QuickSort(myList,start,end):
            if start < end:
                i,j = start,end
                base = myList[i]
                while i < j:
                    while (i < j) and (myList[j] >= base):
                        j = j - 1
                    myList[i] = myList[j]
                    while (i < j) and (myList[i] <= base):
                        i = i + 1
                    myList[j] = myList[i]
                myList[i] = base
                QuickSort(myList, start, i - 1)
                QuickSort(myList, j + 1, end)
            return myList

        QuickSort(stones,0,len(stones)-1)
        
        while len(stones)>1:
            biggest = stones.pop()
            second = stones.pop()
            temp = biggest-second
            stones.append(temp)
            QuickSort(stones,0,len(stones)-1)
        
        return stones[0]
```

Way:

use QuickSort to sort the numbers then pop the last one and the second last one

Improve:

maybe QuickSort is too expensive

**2019.5.20 Mon**

## No.8 Longest Common Prefix

Question:

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string 
"".

```
Example 1:

Input: ["flower","flow","flight"]
Output: "fl"
Example 2:

Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

Code:

```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if(strs.size()==0) return "";
        string first = strs[0];
        int num = 10000;
        for(int i=1;i<strs.size();i++){
            int j = 0;
            while(j<strs[i].size() && strs[i][j]==first[j]){
                j++;
            }
            num = num<j?num:j;
        }
        return num==0?"":first.substr(0,num);
    }
};
```

Result:

> Runtime: 8 ms, faster than 94.02% of C++ online submissions for Longest Common Prefix.
> 
Memory Usage: 8.9 MB, less than 72.29% of C++ online submissions for Longest Common Prefix.

Way:

no special but the usage of substr


**2019.5.21 Tue**

## No.9 Longest Substring Without Repeating Characters

Question:

Given a string, find the length of the longest substring without repeating characters.

```
Example 1:

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

Code:

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        string res="";
        int count = 0;
        for(int i = 0;i<s.size();i++){
            int j = i;
            int temp = 0;
            while(res.find(s[j])==-1 && j<s.size()){
                res.push_back(s[j]);
                j++;
                temp++;
            }
            count=count<temp?temp:count;
            res="";
        }
        return count;
    }
};
```

Result:

> Runtime: 68 ms, faster than 18.54% of C++ online submissions for Longest Substring Without Repeating Characters.
> 
Memory Usage: 9.5 MB, less than 88.37% of C++ online submissions for Longest Substring Without Repeating Characters.

Way:

notice that j<s.size()
string.find returns -1 when no string is found

**2019.5.22 THU**

## No.10 Median of Two Sorted Arrays

Question:

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

You may assume nums1 and nums2 cannot be both empty.

```
Example 1:

nums1 = [1, 3]
nums2 = [2]

The median is 2.0
Example 2:

nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

Code:

```
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        nums1.extend(nums2)
        nums1=sorted(nums1)
        l=len(nums1)
        if l%2==0:
            return (nums1[l//2]+nums1[l//2-1])/2
        else:
            return nums1[l//2]
```

Result:

> Runtime: 64 ms
> 
Memory Usage: 13.3 MB

Way:
Simple


**2019.5.24 Fri**

## No.11 PreorderTraversal

Question:

preorderTraversal

Code:

```
class Solution {
public:
    void preorder(TreeNode* root,vector<int>& res) {
            if(root){
                //cout<<root->val;
                res.push_back(root->val);
                preorder(root->left,res);
                preorder(root->right,res);
            }
        }
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        preorder(root,result);
        return result;
    }
};
```

Result:

> Runtime: 4 ms
> 
Memory Usage: 9.5 MB

Notice:

**when vector is used as a variable in a function, there should be a &**

## No.12 InorderTraversal

Question:

inorderTraversal

Code:

```
class Solution {
public:
    void inorder(TreeNode* root,vector<int> & res){
        if(root){
            inorder(root->left,res);
            res.push_back(root->val);
            inorder(root->right,res);
        }
        
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        inorder(root,res);
        return res;
    }
};
```

Result:

> Runtime: 0 ms
> 
Memory Usage: 9.5 MB

## No.13 PostOrderTraversal

Question:

PostOrderTraversal

Code:

```
class Solution {
public:
    void post(TreeNode* root, vector<int> & res){
        if(root){
            post(root->left,res);
            post(root->right,res);
            res.push_back(root->val);
        }
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> res;
        post(root,res);
        return res;
    }
};
```

Result:

> Runtime: 0 ms
> 
Memory Usage: 9.6 MB


## No.14 LevelOrder

Code:

```
class Solution {
public:
      void help(TreeNode* root, vector<vector<int>> &out, int level) {
        if (!root)
            return;
        if (level==out.size())
            out.push_back(vector<int>());
        help(root->left, out, level+1);
        help(root->right, out, level+1);
        out[level].push_back(root->val);
        
    }
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> out;
        help(root, out, 0);
        return out;

    }
};
```

**2019.5.25 Sat**

## No.15 Maximum Depth of Binary Tree

Code:

```
class Solution {
public:
    int answer;		       // don't forget to initialize answer before call maximum_depth
    void maximum_depth(TreeNode* root, int depth) {
        if (!root) {
            return;
        }
        if (!root->left && !root->right) {
            answer = max(answer, depth);
        }
        maximum_depth(root->left, depth + 1);
        maximum_depth(root->right, depth + 1);
    }
    int maxDepth(TreeNode* root) {
        int depth=1;
        maximum_depth(root,depth);
        return answer;
    }
};
```

Result:

> Runtime: 8 ms
> 
Memory Usage: 19.4 MB

**2019.5.17 Mon**

## No.14 Symmetric Tree

Code:

```
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        queue<TreeNode*> q1, q2;
        q1.push(root->left);
        q2.push(root->right);
        while (!q1.empty() && !q2.empty()) {
            TreeNode *node1 = q1.front(); q1.pop();
            TreeNode *node2 = q2.front(); q2.pop();
            if (!node1 && !node2) continue;
            if((node1 && !node2) || (!node1 && node2)) return false;
            if (node1->val != node2->val) return false;
            q1.push(node1->left);
            q1.push(node1->right);
            q2.push(node2->right);
            q2.push(node2->left);
        }
        return true;
    }
};
```

Code1:

```
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        return isSymmetric(root->left,root->right);
    }
    bool isSymmetric(TreeNode* r1,TreeNode* r2){
        if(!r1&&!r2) return true;
        if(!r1&&r2 ||r1&&!r2 || r1->val!=r2->val){
            return false;
        }
        return isSymmetric(r1->left,r2->right)&&isSymmetric(r1->right,r2->left);
    }
};
```

**2019.5.28 Tue**

## No.15 Merge Two Sorted Lists

Qustion:

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

Code:

```
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(!l1 && !l2)
            return l1;
        vector<int> temp;
        while(l1){
            temp.push_back(l1->val);
            l1=l1->next;
        }
        while(l2){
            temp.push_back(l2->val);
            l2=l2->next;
        }
        sort(temp.begin(),temp.end());
        ListNode* x=new ListNode(temp[0]);
        ListNode* p=x;
        for(int i=1;i<temp.size();i++){
            //cout<<temp[i]<<' ';
            ListNode* node=new ListNode(temp[i]);
            p->next=node;
            p=p->next;
        }
        return x;
    }
};
```

Result:

> Runtime: 8 ms, faster than 95.75% of C++ online submissions for Merge Two Sorted Lists.
> 
Memory Usage: 9.3 MB, less than 53.79% of C++ online submissions for Merge Two Sorted Lists.

**2019.5.29 Wes**

## No.16 Integer to Roman

Question:

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.

```
Example 1:

Input: 3
Output: "III"
Example 2:

Input: 4
Output: "IV"
Example 3:

Input: 9
Output: "IX"
Example 4:

Input: 58
Output: "LVIII"
Explanation: L = 50, V = 5, III = 3.
```

Code:

```
class Solution {
public:
    string intToRoman(int num) {
        int inte[13]={1000,900,500,400,100,90,50,40,10,9,5,4,1};
        string rom[13]={"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
        string res;
        int start=0;
        for(int i=0;i<13;i++){
            if(num<inte[i]&&num>inte[i+1])
                start=i;
        }
        int j=start;
        while(j<13){
            if(inte[j]<=num){
                res+=rom[j];
                num-=inte[j];
                j=start;
            }
            else
                j++;
        }
        return res;
    }
};
```

Result:

> Runtime: 4 ms, faster than 99.20% of C++ online submissions for Integer to Roman.
> 
Memory Usage: 8.4 MB, less than 84.27% of C++ online submissions for Integer to Roman.

**2019.5.31 Fri**

## No.17 Path Sum

Question:

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

Note: A leaf is a node with no children.

Example:

Given the below binary tree and sum = 22,

```
      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
```
return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

Code:

```
class Solution {
public:
    bool check(TreeNode* root,int sum, int temp){
        if(!root){
            return false;
        }
        temp+=root->val;
        if(!root->left&&!root->right&&temp==sum)
            return true;
        return check(root->left,sum,temp)||check(root->right,sum,temp);
    }
    bool hasPathSum(TreeNode* root, int sum) {
        int temp=0;
        return check(root,sum,temp);
    }
};
```

## No.18 3Sum Closest

Question:

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

Example:

Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

Code:

```
int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(),nums.end());
        int result=0;
        int gap=INT_MAX;
        for(int i=0;i<nums.size();i++){
            int left=i+1;
            int right=nums.size()-1;
            int sum=0;
            while(left<right){
                sum=nums[i]+nums[left]+nums[right];
                int gap_now=sum-target;
                if(abs(gap_now)<gap){
                    gap=abs(gap_now);
                    result=sum;
                }
                else if(gap_now==0){
                    return sum;
                }
                if(gap_now>=0){
                    right--;
                }
                else{
                    left++;
                }
            }
        }
        return result;
            
    }
```
   
Result:

> Runtime: 4 ms, faster than 99.82% of C++ online submissions for 3Sum Closest.
> 
Memory Usage: 8.8 MB, less than 59.04% of C++ online submissions for 3Sum Closest.


**2019.6.2 Sunday**

Code:

```
class Solution {
public:
    string gcdOfStrings(string str1, string str2) {
        if(str1==""||str2=="")
            return "";
        int start=0;
        int length=0;
        string shorts;
        string longs;
        if(str1.size()>=str2.size()){
            longs=str1;
            shorts=str2;
        }
        else{
            shorts=str1;
            longs=str2;
        }
        for(int i=0;i<shorts.size();i++){
            for(int j=0;j<longs.size();j++){
                int temp=0;
                int templen=0;
                if(shorts[i]==longs[j]){
                    temp=i;
                    while(shorts[i]==longs[j]&&j<longs.size()&&i<shorts.size()){
                        i++;j++;
                        templen++;
                    }
                    if(templen>length){
                        length=templen;
                        start=temp;
                    }
                }
            }
        }
        return shorts.substr(start,start+length);
    }
};
```
GCD

```
class Solution {
public:
    int gcd(int a,int b)  
    {  
        int t;  
        if(a<b)  
        {  
            t=a;  
            a=b;  
            b=t;  
        }  
        while(t=a%b)  
        {  
            a=b;  
            b=t;  
        }  
        return b;  
    }
    string gcdOfStrings(string str1, string str2) {
        if(str1==""||str2=="")
            return "";
        string shorts;
        string longs;
        if(str1.size()>=str2.size()){
            longs=str1;
            shorts=str2;
        }
        else{
            shorts=str1;
            longs=str2;
        }
        int length=shorts.size();
        int k=0;
        if(longs.substr(0,length)!=shorts)
            return "";
        else{
                k=gcd(shorts.size(),longs.size());
            }
            return shorts.substr(0,k);
        
        
    }
};
```