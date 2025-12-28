## 并发进程的特点
	- 互斥关系
	- 同步关系
	- 前序关系
- ## 进程之间的低级通信
	- ### 临界区
		- 准则：
			- 互斥使用
			  logseq.order-list-type:: number
			- 让权等待
			  logseq.order-list-type:: number
			- 有空让进
			  logseq.order-list-type:: number
			- 有限等待
			  logseq.order-list-type:: number
	- ### 临界资源
		- 一次仅允许一个进程使用的系统中的共享
	- ### 信号量
		- P操作
			- 当一个进程执行 $P(s)$ 时，它在说：“**我想要一份资源。**”
			- ```
			  wait(s) {
			  	s.value--;
			      if(s.value < 0) { add this process to s.list; block();}
			  }
			  ```
		- V操作
			- ```
			  signal(s) {
			  	s.value++;
			      if(s.value<=0) {remove; wakeup();}
			  }
			  ```
	- [[PV问题]]
	-
- ## 进程的高级通信
- ## 死锁