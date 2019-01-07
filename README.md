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
