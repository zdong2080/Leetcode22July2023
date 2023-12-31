# Leetcode 148. Sort List

## 题目描述
<div class="px-5 pt-4"><div class="flex"></div><div class="_1l1MA" data-track-load="description_content"><p>Given the <code>head</code> of a linked list, return <em>the list after sorting it in <strong>ascending order</strong></em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg" style="width: 450px; height: 194px;">
<pre><strong>Input:</strong> head = [4,2,1,3]
<strong>Output:</strong> [1,2,3,4]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg" style="width: 550px; height: 184px;">
<pre><strong>Input:</strong> head = [-1,5,3,4,0]
<strong>Output:</strong> [-1,0,3,4,5]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> head = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is in the range <code>[0, 5 * 10<sup>4</sup>]</code>.</li>
	<li><code>-10<sup>5</sup> &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Can you sort the linked list in <code>O(n logn)</code> time and <code>O(1)</code> memory (i.e. constant space)?</p>
</div></div>

## 测试用例
* 无效输入测试用例（输入数组为空；长度为n的数组中包含 0 到 n-1之外的数字）

## 代码
## 解法1 93% 99%
```c++ 
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode*merge(ListNode*f,ListNode*s){
        
        ListNode*head;
        ListNode*h1=f;
        ListNode*h2=s;
        
        if(h1->val<=h2->val){
            head=h1;
            h1=h1->next;
        }
        else{
            head=h2;
            h2=h2->next;
        }
        ListNode*h=head;
        
        while(h1!=NULL && h2!=NULL){
            if(h1->val<=h2->val){
                h->next=h1;
                h=h1;
                h1=h1->next;
            }
            else{
                h->next=h2;
                h=h2;
                h2=h2->next;
            }
        }
        
        if(h1!=NULL){
            h->next=h1;
        }
        if(h2!=NULL){
            h->next=h2;
        }
        return head;
    }
    ListNode* merge_sort(ListNode* head){
        
        if(head==NULL || head->next==NULL){
            return head;
        }
        
        ListNode*slow=head;
        ListNode*fast=head->next;

        while(fast!=NULL && fast->next!=NULL){
            slow=slow->next;
            fast=fast->next->next;
        }

        ListNode*second=slow->next;
        slow->next=NULL;
        
        ListNode*firsthalf=merge_sort(head);
        ListNode*sechalf=merge_sort(second);
        
        return merge(firsthalf,sechalf);
    }
    ListNode* sortList(ListNode* head) {
        return merge_sort(head);
    }
};
```
