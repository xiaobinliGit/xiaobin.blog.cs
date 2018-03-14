---
title: LeetCode
date: 2018-02-16 13:49:14
categories:
  - 技术日志
  - C++
tags:
  -C++
---
### 摘要: leetCode solution
<!--more-->
Solution for leetcode one by one in free time.

## <font color=#0000FF>leetcode 1</font>
```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> result;
        int index_a, index_b;
        //vector<int>::iterator iter;
        for(index_a = 0; index_a < nums.size(); index_a++)
        {
        	for(index_b = index_a+1; index_b < nums.size(); index_b++)
        	{
        		if(nums[index_a]+nums[index_b]==target)
        		{
        			result.push_back(nums[index_a]);
        			result.push_back(nums[index_b]);
        			cout<<"[" <<index_a <<"," << index_b << "]"<<endl;
        			return result;
        		}
        	}
        }
        return result;
    }
};
```

## <font color=#0000FF>leetcode 2</font>
```cpp
class Solution {
public:
    Solution()
    {
        //listhead = listnode;
    }
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    	ListNode* index1 = l1;
    	ListNode* index2 = l2;
        ListNode* head;
    	int index = 0;
        int index_a = 0; 
        int index_b = 0;
    	std::vector<int> v;
    	v.push_back(0);
    	while(index1!=NULL&&index2!=NULL)
    	{
    		if(index1->val+index2->val+v[index] > 9)
    		{
    			v[index]+=(index1->val+index2->val-10);
    			v.push_back(1);
    		}
            else
            {
                v[index]+=(index1->val+index2->val);
                v.push_back(0);
            }
            index++;
            index_a++;
            index_b++;
            index1 = index1->next;
            index2 = index2->next;
    	}
        while(index1!=NULL)
        {
            if(index1->val+v[index] > 9)
            {
                v[index]+=(index1->val-10);
                v.push_back(1);
            }
            else
            {  
                v[index]+=(index1->val);
                v.push_back(0);
            }
            index++;
            index_a++;
            index1 = index1->next;
        }
        while(index2!=NULL)
        {
            if(index2->val+v[index] > 9)
            {
                v[index]+=(index2->val-10);
                v.push_back(1);
            }
            else
            {  
                v[index]+=(index2->val);
                v.push_back(0);
            }
            index++;
            index_b++;
            index2 = index2->next; 
        }
        if(v[index]==0)  //no exceed size
        {
            v.pop_back();
            if(index_a >= index_b)
            {
                head = l1;
                std::vector<int>::iterator iter;
                for(iter = v.begin(); iter!=v.end(); iter++)
                {
                    l1->val = *iter;
                    l1 = l1->next;
                }
                return head;
            }
            else
            {
                head = l2;
                std::vector<int>::iterator iter;
                for(iter = v.begin(); iter!=v.end(); iter++)
                {
                    l2->val = *iter;
                    l2 = l2->next;
                }
                return head;
            }
        }
        else  // add one node in list
        {
            //ListNode* tempnode = (ListNode*)malloc(sizeof(ListNode));
            ListNode* tempnode = new ListNode(0);
            head = tempnode;
            if(index_a >= index_b)
            {
                std::vector<int>::iterator iter;
                tempnode->next = l1;
                l1 = tempnode;
                for(iter = v.begin(); iter!=v.end(); iter++)
                {
                    l1->val = *iter;
                    l1 = l1->next;
                }
                return head;
            }
            else
            {
                std::vector<int>::iterator iter;
                tempnode->next = l2;
                l2 = tempnode;
                for(iter = v.begin(); iter!=v.end(); iter++)
                {
                    l2->val = *iter;
                    l2 = l2->next;
                }
                return head;
            }
        }
    }
private:
    //ListNode* listhead;
};
```

## <font color=#0000FF>leetcode 3</font>
关键点在于确定start的点和end的点，同时要保证hash的字符的值与字符序列号绑定（试了3种思想，最后一种才最终正确）
```cpp
int lengthOfLongestSubstring2(string s) {
    int v[256];
    int i = 0;
    int start = 0, end;
    int len = 0;
    int size = s.size()-1;
    while(size>=0)
    {
        v[s[size]] = size--;
    }
    while(i<s.size())
    {
        if(v[s[i]]!=i) //repeat char
        {
            start = max(start,++v[s[i]]);
        }
        else //not repeat
        {
            //end = i;
        }
        v[s[i]] = i++;
        len = max(len,i-start);
    }
    return len;
}

```

## <font color=#0000FF>leetcode 35</font>
```cpp
int searchInsert(vector<int>& nums, int target) {
        int start = 0;
        int end = nums.size()-1;
        int mid = (start+end)/2;
        if(target>nums[end])
        {
            return end+1;
        }
        if(target<=nums[start]) //remember the '='' for single element
        {
            return start;
        }
        while(start+1<end)
        {
            mid = (start+end)/2;
            if(nums[mid]==target)
            {
                return mid;
            }
            else if(nums[mid]>target)
            {
                end = mid;
            }
            else
            {
                start = mid;
            }
        }
        return start+1;
    }

```

## <font color=#0000FF>leetcode 100</font>
```cpp
bool isSameTree1( TreeNode* p,  TreeNode* q)
{	
	if (p!=NULL&&q!=NULL)
	{
		if(p->val == q->val)
		{
			return (isSameTree1(p->left, q->left)&&isSameTree1(p->right, q->right));
		}
		else
		{
			return false;
		}
	}
	else if(p==NULL&&q==NULL)
	{
		return true;
	}
	else
	{
		return false;
	}
}

```
