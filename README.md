# leetcode-top_100
## 1. 两数之和
### 问题：给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。
### 代码：
class Solution(object):

    def twoSum(self, nums, target):
        hashmap = {} 
        for index, num in enumerate(nums):         
            another_num = target - num                    
            if another_num in hashmap:                    
                return [hashmap[another_num], index]                           
            hashmap[num] = index        
        return None

## 2.两数相加
### 问题：给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。您可以假设除了数字 0 之外，这两个数都不会以 0 开头。
### 代码：
class Solution(object):

    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        s1=''
        s2=''
        while l1:
            s1+=str(l1.val)
            l1=l1.next
        while l2:
            s2+=str(l2.val)
            l2=l2.next
        s1=s1[::-1]
        s2=s2[::-1]
        return [int(i) for i in str(int(s1)+int(s2))[::-1]]

## 3.无重复字符的最长子串
### 问题：给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度 链接：https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/
### 思路：采用hashmap存储上一个字符出现的位置，若下一次出现这个字符，将下一次出现字符所在的位置和上一次所在的位置取差值+1，比较每次长度
### 代码：
class Solution(object):

    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        res = 0
        if s is None or len(s) == 0:
            return res
        d = {}
        tmp = 0
        start = 0
        for i in range(len(s)):
            if s[i] in d and d[s[i]] >= start:
                start = d[s[i]] + 1
            tmp = i - start + 1
            d[s[i]] = i
            res = max(res, tmp)
        return res
        
## 4. 寻找两个有序数组的中位数
### 问题：给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。你可以假设 nums1 和 nums2 不会同时为空。
### 思路：将两个数组合并，计算中位数
### 代码：

class Solution(object):

    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        
        nums1.extend(nums2)
        res = nums1
        if not res: 
            return None
        res.sort()
        l = len(res)
        if l % 2:
            return res[l/2] / 1.0 
        else : 
            return (res[l/2] + res[(l/2)-1]) / 2.0
            
## 5. 最长回文子串
### 问题：给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。
### 思路：暴力破解，时间复杂度有点高，
### 代码：
class Solution:

    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        if not s:
            return ""
        if len(s)==1:
            return s
        l=[]
        len1=len(s)
        for index,i in enumerate(s):
            for index_1,j in enumerate(s[:index:-1]):
                s1=s[index:len1-index_1]
                if s1==s1[::-1]:
                    l.append(s1)
                    break
        d={}
        if not l:
            return s[-1]
        for i in l:
            d[i]=len(i)
        return max(d, key=d.get)
        
## 11. 盛最多水的容器
### 问题：给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。说明：你不能倾斜容器，且 n 的值至少为 2  链接：https://leetcode-cn.com/problems/container-with-most-water/
### 思路：动态规划，先比较最左边和最右边的高度，计算面积，如果左边的比右边的小，左边和右边无论如何哪一个组合都没有它们两组合面积大，左边向右移动1格，右边同理，获得最大
### 代码：

class Solution(object):

    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        left = 0
        right = len(height) - 1
        max_res = 0
        while left<right:
            w=right-left
            if height[left]<height[right]:
                h=height[left]
                left+=1
            else:
                h=height[right]
                right-=1
            if max_res<w*h:
                max_res=w*h
        return max_res
        
##17. 电话号码的字母组合
### 问题：给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。 链接：https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/
### 思路：递归，写一个函数处理两个串之间的组合，组合之后在和后面来的字符串用同样的方法两两组合
### 代码：

class Solution(object):

    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        hashmap={
            '1':'','2':'abc','3':'def','4':'ghi','5':'jkl','6':'mno','7':'pqrs','8':'tuv','9':'wxyz'
                }
        if not digits:
            return []
        l=[i for i in hashmap[digits[0]]]
        for i in digits[1:]:
            x=hashmap[i]
            l=self.convert(l,x)
        return l
    def convert(self,str1,str2):
        res=[]
        for i in range(len(str1)):
            for j in range(len(str2)):
                           res.append(str1[i]+str2[j])
        return res
                         

## 19. 删除链表的倒数第N个节点
### 问题：给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。 链接：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/
### 思路：获得一个快链表和一个慢链表，当快链表走n步后，慢链表开始走，当快链表到达终点时，慢链表到达-n的地方
### 代码：

class Solution(object):

    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        result = ListNode(0)
        result.next = head
        first = result
        second = result
        index = 0
        while True:
            if first.next == None:
                second.next = second.next.next
                break
            first = first.next
            index += 1
            if index > n:
                second = second.next
        return result.next

## 20. 有效的括号
### 问题：给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

    有效字符串需满足：
    左括号必须用相同类型的右括号闭合。
    左括号必须以正确的顺序闭合。
    注意空字符串可被认为是有效字符串。
    链接：https://leetcode-cn.com/problems/valid-parentheses/submissions/
### 思路：将这些字符串以键值对的形式存入字典，通过栈实现
### 代码：

class Solution(object):

    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        d = {'}': '{', ']': '[', ')': '('}
        stack = [' ']
        for item in s:
            key = d.get(item, '')
            if stack[-1] == key:
                stack.pop()
            elif key:
                return False
            else:
                stack.append(item)
        return len(stack) == 1

## 21. 合并两个有序链表
### 问题：将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
    示例：
    输入：1->2->4, 1->3->4
    输出：1->1->2->3->4->4
### 思路：新建一个链表，比较两个链表，轮询，将小的存入新的链表
### 代码：
class Solution(object):

    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        head=ListNode(0)
        dummp=head
        while l1 and l2:
            if l1.val>l2.val:
                head.next=l2
                l2=l2.next
            else:
                head.next=l1
                l1=l1.next
            head=head.next
        if l1:
            head.next=l1
        if l2:
            head.next=l2
        return dummp.next
        
## 
