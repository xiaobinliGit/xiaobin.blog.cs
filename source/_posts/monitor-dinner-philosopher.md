---
title: 通过管程实现哲学家进餐
date: 2017-11-06 14:00:00
categories:
  - 技术日志
  - Operating System
tags:
  -OS
cover: /images/Ph.JPG
---
### 摘要: 哲学家进餐管程实现（代码+分析）
<!--more-->

最近在一个地方突然看到操作系统里的同步操作和信号量的概念，上学那时候感觉对这块掌握的不是那么扎实，索性就看了一下，在CSDN的一篇博客里找到一个不错的利用管程来实现哲学家进餐问题，贴在这里，顺带整理了一下格式，对singal这块的理解还是有些疑问，需要mark下等最近项目闲下来继续研究：

### 使用管程解决进程同步问题
####  <font color=#330099> 管程解决五个哲学家吃通心面问题</font>
首先，引入枚举类型enum {thinking,hungry,eating} state[5]表示哲学家的状态，哲学家i能建立状态state［i］=eating，仅当他的两个邻座不在吃的时候，即state［(i-1)%5］!=eating及state［(i+1)%5］!=eating；另外还要引入条件变量(信号量)：semaphore self[5]，当哲学家i饥饿但又不能获得两把叉子时，进入其信号量等待队列。
 
<font color=#B0B0B0 style="font-style:italic">说明: 在释放叉子的时候，唤醒左邻居和右邻居。如果以顺时针编号，对于i号哲学家，(i-1)%5是i号哲学家的右邻居，(i+1)%5是i号哲学家的左邻居。每个哲学家在三个状态(thinking,hungry,eating)中变换，其中是hungry是thinking向eating的过渡状态  </font>

####  <font color=#330099> 代码实现</font>
```C++

enum {thinking,hungry,eating} state[5];
semaphore self[5];//Hoare方法数据结构和enter、wait、signal及leave操作
typedef struct InterfaceModule 
{ //InterfaceModule是结构体的名字
	semaphore mutex;             //进程调用管程过程前使用的互斥信号量
	semaphore next;              //发出signal的进程挂起自己的信号量
	int next_count;              //在next上等待的进程数
};

mutex=1;next=0;next_count=0;//初始化语句

void enter(InterfaceModule &IM) 
{
	P(IM.mutex);             //互斥进入管程
}
void leave(InterfaceModule &IM) {
	if(IM.next_count>0)       //判有否发出过signal的进程?
		V(IM.next);          //有就释放一个发出过signal的进程
	else
		V(IM.mutex);         //否则开放管程
}
void wait(semaphore &x_sem,int &x_count,InterfaceModule &IM) 
{
	x_count++;              //等资源进程个数加1，x_count初始化为0
	if(IM.next_count>0)     //判有否发出过signal的进程
		V(IM.next);         //有就释放一个
	else 
		V(IM.mutex);        //否则开放管程
	P(x_sem);               //这里会一直忙等，等资源进程阻塞自己，x_sem初始化为0
	x_count--;              //等资源进程个数减1 
}
void signal(semaphore &x_sem,int &x_count,InterfaceModule &IM) 
{
	if(x_count>0) 
	{           //有等资源进程吗?
		IM.next_count++;       //发出signal进程个数加1
		V(x_sem);              //释放一个等资源的进程
		P(IM.next);            //这里会一直忙等，发出signal进程阻塞自己
		IM.next_count--;       //发出signal进程个数减1
	}
}

 //初始化列表
IM.mutex=1; 
next=0; 
next_count=0; 
self[i]=0; 
self_count=0; 
state[i]=thinking; 
mutex=1;next=0;next_count=0; 


//DP实现
type dining_philosophers=monitor
{
	int self_count[5];
	InterfaceModule IM;
	for (int i=0;i<5;i++)      //初始化，i为进程号
		state[i]=thinking;
	define pickup,putdown;
	use enter,leave,wait,signal；
	void pickup(int i) {        //i=0,1,...,4
		enter(IM);
		state[i]=hungry;
		test(i);
		if(state[i]!=eating)
			wait(self[i],self_count[i],IM);
		leave(IM);
	}
	void putdown(int i) {       //i=0,1,2,..,4
		enter(IM);
		state[i]=thinking;
		test((i-1)%5);
		test((i+1)%5);
		leave(IM);
	}
	void test(int k)  {       //k=0,1,...,4
		if((state[(k-1)%5]!=eating)&&(state[k]==hungry)
			&&(state[(k+1)%5]!=eating)) 
		{
			state[k]=eating;
			signal(self[k],self_count[k],IM);
		}
	}

	任一个哲学家想吃通心面时调用过程pickup，吃完通心面之后调用过程putdown。           
	process philosopher_i( ) {  //i=0,…,4
		while(true) 
		{
			thinking( );
			dining_philosophers.pickup(i);        
			eating( );
			dining_philosophers.putdown(i);
		}
	}
}
```

####  <font color=#330099> 状态转换过程详解决</font>
##### (A) ->
假设一开始3号哲学家，第一个做pickup，他会很顺畅，在pickup中通过enter(IM)进入管程，修改自身状态state[3]=hungry, 接着test(3)中if条件通过，修改自身状态state[3]=eating, 因为这时候没有进程(哲学家)阻塞在self[3]上，即self_count[3]==0，对照signal(self[3], self_count[3], IM)中的PV实现，实际上此时signal什么也不做。然后，判断if (state[3]!=eating)不成立，因此wait操作也不做。再然后，3号哲学家执行leave(IM)退出管程，以便让其他哲学家进入管程。
<font color=#0000FF>分析：实际上这里3号哲学家成功的取到他需要的两个叉子。他通过将自己的状态改为eating，对于i=2号哲学家在取叉子的时需要做test(i)，state[i+1]!=eating不成立；对于i=4号哲学家在取叉子的时需要做test(i)，state[i-1]!=eating不成立；从而封堵其左右哲学家转入eating状态，2、4号哲学家不能成功转入eating状态，将执行wait操作，也即在3号哲学家没有执行putdown中的test((i-1)%5)和test((i+1)%5)之前，左右哲学家不能成功取到叉子。</font>

##### (B) ->
接着，在3号哲学家还没有putdown之前，如果1号哲学家执行pickup，他也会很顺畅，与之前的3号哲学家pickup时的情形类似，在pickup中通过enter(IM)进入管程，修改自身状态state[1]=hungry, 接着test(1)中if条件通过，修改自身状态state[1]=eating, 因为这时候没有进程(哲学家)阻塞在self[1]上，即self_count[1]==0，对照signal(self[1], self_count[1], IM)中的PV实现，实际上此时signal什么也不做。然后，判断if (state[1]!=eating)不成立，因此wait操作也不做。再然后，3号哲学家执行leave(IM)退出管程，以便让其他哲学家进入管程。
<font color=#0000FF>分析：实际上这里1号哲学家成功的取到他需要的两个叉子。他通过将自己的状态改为eating，从而封堵其左右哲学家转入eating状态，0、2号哲学家不能成功转入eating状态，也即在1号哲学家没有执行putdown中的test((i-1)%5)和test((i+1)%5)之前，不能成功取到叉子。</font>

##### (C)->
接着，在1和3号哲学家没有putdown之前，此时，state[1]==eating，state[3]==eating。如果2号哲学家执行pickup，他会很不顺畅，在pickup中通过enter(IM)进入管程，修改自身状态state[2]=hungry，接着test(2)中的if条件state[1]!=eating，state[3]!=eating都不成立，因此2号哲学家没有成功把自身状态修改为eating，也不用做test(2)中signal(self[2], self_count[2], IM)操作，再接着判断if (state[2]!=eating)成立，因此做wait(self[2], self_count[2], IM)操作，对照wait操作的PV实现，此时，self[2].count++表示在self[2]等待的进程数加1，然后判断if (IM.next_count>0)，如果此时1和3号进程都没有执行putdown中的signal操作，那么该条件不成立，然后执行V(IM.mutex)退出管程，接着P(self[2])阻塞自己，等待1和3号哲学家执行putdown中的signal操作唤醒之。

##### (D)->
接着，假设1号哲学家吃完，执行putdown，在putdown中通过enter(IM)进入管程，并修改自身状态state[1]=thinking，然后test((i-1)%5)，即test(0)，其中state[(0-1)%5]即state[4]!=eating成立，state[0]==hungry不成立(表示0号哲学家没有执行pickup)，state[(0+1)%5]即state[1]!=eating成立，即整个if条件不成立，if下的语句不做。然后test((i+1)%5)，即test(2)，其中state[(2-1)%5]即state[1]!=eating成立，state[2]==hungry(表示之前2号哲学家已经执行了pickup，且没有成功取到叉子)，state[(2+1)%5]即state[3]!=eating不成立，即整个if条件还是不成立，然后1号哲学家执行leave(IM)退出管程，以便其他哲学家进入管程。
<font color=#0000FF>分析: 1号哲学在putdown的时候执行test(0)和test(2)，test(0)用意在于唤醒右邻居0号哲学家，但是0号哲学家还没有执行pickup，也就没有把自身状态修改为hungry，1号哲学家的这份好心浪费了；接着test(2)用意在于唤醒左邻居2号哲学家，但是2号哲学家成功取到叉子之前要判断3号是否eating，实际上此时3号依然eating，因此test(2)的用意没有真正成功。看来还真不简单，不要紧，继续往下看。</font>

##### (E)->
当1号哲学家在putdown中退出管程，此时state[1]==thinking，state[2]==hungry，假设此时3号哲学家开始执行putdown，在putdown中通过enter(IM)进入管程，并修改自身状态state[3]=thinking，然后test((i-1)%5)，即test(2)，其中state[(2-1)%5]即state[1]!=eating成立，state[2]==hungry成立(表示之前2号哲学家已经执行了pickup，且没有成功取到叉子)，state[(2+1)%5]即state[3]!=eating成立，即整个if条件成立，看到希望了，接着执行signal(self[2], self_count[2], IM)，因为之前，2号哲学家已经在self[2]上等待许久了，对照signal操作的PV实现，self_count[2]>0，执行IM.next_count++，V(self[2]) (注:终于把2号哲学家等待许久的self[2]释放，唤醒2号哲学家)，P(IM.next)阻塞自己。
<font color=#0000FF>分析：对于2号哲学家被唤醒之后，他将执行其pickup中P(self[2])之后的语句，self_count[2]--，即self_count[2]恢复为0，并最终执行pickup中leave(IM)，在leave(IM)中参考Hoare管程leave操作的PV实现，判断if (IM.next_count)>0成立，则执行V(IM.next) 唤醒3号哲学家之前在P(IM.next)上的等待，并有机会执行后续语句IM.next_count--，即计数恢复为0，最终执行putdown中的leave(IM)退出管程，以便其他进程能够再进入管程，这里可以看出对于Hoare管程的实现，signal操作不必是过程体的最后一个操作。对于3号哲学家通过test(2)完成了唤醒2号哲学家的任务，然而他自己暂时阻塞在IM.next上，暂时不能执行putdown中后续的test((i+1)%5)，即不能执行test(4)。</font>

##### (F) ->
接着，假设在2号哲学家被唤醒取到叉子之后开始吃，3号哲学家执行完putdown中的leave(IM)退出管程，如果1号哲学家想再一次取叉子，此时state[0]==state[3]==thinking，state[2]==eating，1号不如之前顺畅，在pickup中通过enter(IM)进入管程，修改自身状态state[1]=hungry, 接着test(1)中，state[2]!=eating不成立，即if条件不通过，因此1号哲学家没有成功把自身状态修改为eating，也不用做test(1)中signal(self[1], self_count[1], IM)操作，再接着判断if (state[1]!=eating)成立，因此做wait(self[1], self_count[1], IM)操作，对照wait操作的PV实现，此时，self[1].count++表示在self[1]等待的进程数加1，然后判断if (IM.next_count>0)，如果此时2号进程还没有执行putdown中的signal操作，那么该条件不成立，然后执行V(IM.mutex)退出管程，接着P(self[1])阻塞自己，等待2号哲学家执行putdown中的signal操作唤醒之。
<font color=#0000FF>分析: 到此为止，2号哲学家状态为eating正在吃，还没有执行putdown，1号哲学家因为左邻居2号在eating，被阻塞在self[1]上，等待2号执行putdown的时候唤醒之。后续的场景演绎依照上述思路展开，不再赘述。</font>

##### <-END

####  <font color=#330099> 状态转换序列</font>
|调用进程|被调用的操作|信号量状态||
|:--|:--|:--|:--|
|1. |P3|pickup|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking;|
|2. |P3|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking;|
|3. |P3|State[3]=hungry|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]=hungry;|
|4. |P3|test(3)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]=hungry;|
|5. |P3|State[3]=eating|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|6. |P3|Signal(self[3])|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|||//空操作||
|7. |P3|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|8. |P1|pickup|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|9. |P1|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating;|
|10. |P1|State[1]=hungry|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]=hungry;|
|11. |P1|test(1)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]=hungry;|
|12. |P1|State[1]=eating|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|13. |P1|Signal(self[1])|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|||//空操作||
|14. |P3|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|15. |P2|pickup|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|16. |P2|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating;|
|17. |P2|State[2]=hungry|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating; state[2]= hungry;|
|18. |P2|test(2)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[3]= eating; state[1]= eating; state[2]= hungry;|
|19. |P2|wait(self[2])|IM.mutex=1; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= eating; state[2]= hungry;|
|||//||
|20. |P1|putdown|IM.mutex=1; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= eating; state[2]= hungry;|
|21. |P1|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|22. |P1|State[1]=thinking|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|23. |P1|test(0)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|24. |P1|test(2)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|25. |P1|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|26. |P3|putdown|IM.mutex=1; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|27. |P3|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[3]=eating; state[1]= thinking; state[2]= hungry;|
|28. |P3|State[3]=thinking|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[2]= hungry;|
|29. |P3|test(2)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[2]= hungry;|
|||//序30, 31, 34||
|30. |P3|State[2]=eating|IM.mutex=0; next=0; next_count=0; self[i]=0; self[2]=-1 (P2); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[2]= eating;|
|||//P3.test(2)中||
|31. |P3|Signal(self[2])|IM.mutex=0; next=-1 (P3); next_count=1; self[i]=0; self[2]=0 P2 (); self_count[i]=0; self_count[2]=1; state[i]=thinking; state[2]= eating;|
|||//P3.test(2)中||
|32. |P2|Self_count[2]—|IM.mutex=0; next=-1 (P3); next_count=1; self[i]=0; self_count[i]=0; self_count[2]=0; state[i]=thinking; state[2]= eating;|
|||//P2.P(wait)的末尾语句||
|33. |P2|leave(IM)|IM.mutex=0; next=0 P3 (); next_count=1; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|||//P2.pickup中的||
|34. |P3|next_count--|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|||//P3.test(2)中的signal(self[2])的末尾语句||
|35. |P3|test(4)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|36. |P3|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|||//P3.putdwon的末尾语句||
|37. |P1|Pickup|IM.mutex=1; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|38. |P1|Enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; state[i]=thinking; state[2]= eating;|
|39. |P1|State[1]=hungry|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; self_count[2]=0; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|40. |P1|Test(1)|IM.mutex=0; next=0; next_count=0; self[i]=0; self_count[i]=0; self_count[2]=0; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|41. |P1|Wait(self[1])|IM.mutex=1; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|42. |P2|Putdown |IM.mutex=1; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|43. |P2|enter(IM)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= eating;|
|44. |P2|State[2]=thinking|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= thinking;|
|45. |P2|test(1)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=hungry; state[2]= thinking;|
|||//序||
|46. |P2|State[1]=eating|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=-1 (P1); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P2.test(1)中||
|47. |P2|Signal(self[2])|IM.mutex=0; next=-1 (P2); next_count=1; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=1; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P3.test(2)中||
|48. |P1|Self_count[1]—|IM.mutex=0; next=-1 (P2); next_count=1; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P1.P(wait)的末尾语句||
|49. |P1|leave(IM)|IM.mutex=0; next=0 P2 (); next_count=1; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P1.pickup中的||
|50. |P2|next_count--|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|||//P2.test(1)中的signal(self[1])的末尾语句||
|51. |P2|test(3)|IM.mutex=0; next=0; next_count=0; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinking; state[1]=eating; state[2]= thinking;|
|52. |P2|leave(IM)|IM.mutex=1; next=0; next_count=0; self[i]=0; self[1]=0 P1 (); self_count[i]=0; self_count[1]=0; state[i]=thinki|
|||//P2.putdwon的末尾语句||