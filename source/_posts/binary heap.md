---
title: 二叉堆时间复杂度证明
date: 2017-10-27 22:03:24
categories:
  - 技术日志
  - 算法
tags:
  -二叉堆
---
### 摘要: 二叉堆的时间复杂度为O(n)
<!--more-->
最近在看些基础算法，从http://zh.visualgo.net/zh 上看到关于二叉堆的创建方式2，其实从代码实现上表面用了O(nlog(n))，但是实际算下来只有O(n)的时间复杂度，对其证明不是很明白，遂百度之，记录如下：

1　具有n个元素的平衡二叉树，树高为log(n)，我们设这个变量为h。
2　最下层非叶节点的元素，因为这时候只需要和叶子节点做交换，所以做一次线性运算便可以确定大根，而这一层具有2^(h-1)个元素，O(1)=1，那么h-1层的元素所需时间为2^(h-1)×1。
3　由于是bottom-top建立堆，因此在调整上层元素的时候，并不需要同下层所有元素做比较，只需要同其中之一分支作比较，而作比较次数则是树的高度减去当前节点的高度。因此，第y层元素的计算量为2^(y)×(h-y)。
4　又以上通项公式可得知，构造树高为h的二叉堆的精确时间复杂度为：
<b><font color=#A52A2A><1> </font></b> S = 2^(h-1)×(h-(h-1)) + 2^(h-2)×(h-(h-2)) + …… +1×(h-1)    

通过观察第四步得出的公式可知，该求和公式为等差数列和等比数列的乘积，因此用错位想减发求解，给公式左右两侧同时乘以2，可知：
 <b><font color=#A52A2A><2> </font></b> 2S = 2^h×1 + 2^(h-1)×2 + …… +2×(h-1)     

用<2>减去<1>可知： 
<b><font color=#A52A2A><3> </font></b> S =2^h×1 - h +1        

将h = log(n) 带入<3>，得出如下结论：

S = n -log(n) +1 = O(n)

结论：构造二叉堆的时间复杂度为线性得证

附最大二叉树构造代码：

{% codeblock lang:cpp %}
include "Binary_Heap.hpp"

void BinaryHeap::createMaxBinaryHeap(int index)
{
	int leftindex = (index<<1)+1;
	int rightindex = (index<<1)+2;
	int maxindex = index;
	if(leftindex < array_size && array_bh[leftindex] > array_bh[maxindex])
	{
		maxindex = leftindex;
	}
	if(rightindex < array_size && array_bh[rightindex] > array_bh[maxindex])
	{
		maxindex = rightindex;
	}
	if(maxindex!=index)
	{
		bhswap(&array_bh[maxindex], &array_bh[index]);
		createMaxBinaryHeap(maxindex);
	}
}

void BinaryHeap::genMaxHeap()
{
	int begin;
	for(begin = (array_size-1)>>1; begin>=0; begin--)
	{
		createMaxBinaryHeap(begin);
	}
}

void BinaryHeap::genHeap()
{
	int begin;
	for(begin = array_size-1; begin>=0; begin--)
	{
		array_bh.push_back(randomGenerator(103));
	}
}

void BinaryHeap::getBinaryHeap()
{
	int begin;
	for(begin = 0; begin<array_size; begin++)
	{
		cout<<array_bh[begin]<<"\t";
	}
	cout<<endl;
}
{% endcodeblock %}

