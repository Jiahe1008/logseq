## 数据寻址方式
	- CPU操作数寻址
		- 立即寻址方式
		- 寄存器寻址方式
	- 存储器操作数寻址
		- 直接寻址方式
		- 寄存器间接寻址方式
		- 寄存器相对寻址方式
		- 基址变址寻址方式
		- 相对基址变址寻址方式
- ## 数据运算指令
	- **数据传送指令**
		- 通用数据传送指令
			- `MOV`
				- 立即数->通用寄存器
				- 通用寄存器->通用寄存器
				- 立即数->内存
				- 内存->通用寄存器
				- 段寄存器->内存
				- 通用寄存器->段寄存器
			- `MOVSX`
			- `MOVZX`
			- 堆栈操作指令`PUSH`,`POP`
			- `XCHG`
		- 输入/输出指令
			- `IN`
			- `OUT`
		- 地址传送指令
			- `LEA`
		- 标志传送指令
			- `PUSHF`
			- `POPF`
			- `PUSHFD`
			- `POPFD`
	- **算术运算指令**
		- 类型转换指令
			- 字节扩展成字指令`CBW`
			- 扩展成双字`CWD`
			- 双字扩展到四字`CDQ`
			- AX扩展到EAX`CWDE`
			-
		- 二进制加法指令
			- 加法指令`ADD`
			- 带进位加法指令`ADC`
			- 加1指令`INC`
			- 互换并加法指令`XADD`
		- 二进制减法指令
			- 减法指令`SUB`
			- 带借位减法指令`SBB`
			- 减1指令`DEC`
			- 比较指令`CMP`
			- 求补指令`NEG`
			- ```
			  LEA		DI, SUM
			  ADD 	DI, 2
			  MOV		BX, 2
			  MOV		AL,FIRST[BX]
			  ADD		AL, SECOND+2
			  MOV		[DI], AL
			  DEC		DI
			  DEC		BX
			  MOV		AL, SECOND+1
			  MOV		[DI], AL
			  DEC		DI
			  DEC		BX
			  MOV		AL, FIRST[BX]
			  ADC		AL, SEDOND
			  MOV		[DI], AL
			  ```
		- 二进制乘法指令
			- 无符号数乘法`MUL`
			- 带符号数乘法`IMUL`
		- 二进制除法指令
			- 无符号数除法`DIV`
			- 带符号数除法`IDIV`
	- **位运算指令**
		- 逻辑运算指令
			- `NOT`
			- `AND`
			- `TEST`
			- `OR`
			- `XOR`
		- 位测试指令
			- `BT`
			- `BTS`
			- `BTR`
			- `BTC`
		- 基本移位指令
			- `SHL`
			- `SAL`
			- `SHR`
			- `SAR`
		- 循环移位指令
			- `ROL`
			- `ROR`
			- `RCL`
			- `RCR`
- ## 程序控制指令
	- 转移指令的寻址方式
		- 段内直接寻址方式
		- 段内间接寻址方式
		- 段间直接寻址方式
		- 段间间接寻址方式
	- 转移指令
		- 无条件转移指令
		- 条件转移指令
			- 条件码：
			  id:: 6951197e-97cc-4841-a721-6d1ce3b3bb86
				- ZF (Zero Flag) —— 零标志位
				- SF (Sign Flag) —— 符号标志位
				- OF (Overflow Flag) —— 溢出标志位（针对有符号数）
				  CF (Carry Flag) —— 进位标志位（针对无符号数）
				- PF 奇偶标志位 （奇校验标志位）
			- |指令名|判断条件|功能|
			  |JC|有进位转移||
			  |JNC|无进位转移||
			  |JO|溢出转移||
			  |JNO|无溢出||
			  |JP/JPE|偶||
			  |JNP/JPO|奇数||
			  |JS|负数||
			  |JNS|非负数||
			  |JZ/JE|结果为0，相等|ZF=1|
			  |JNZ/JNE|不为0，不相等|ZF=0|
			  |JG/JNLE|大于（有符号）||
			  |JNG/JLE|小于等于（有符号）||
			  |JL/JNGE|小于（有符号）||
			  |JNL|大于等于（有符号）||
			  |JA|高于（无符号）||
			  |JNA|不高于（无符号）||
			  |JB|低于（无符号）||
			  |JNB|不低于（无符号）||
		- 测试CX/ECX值为0的转移指令
	- 循环指令
		- 循环指令
		- 相等循环指令
		- 不等循环指令
	- 子程序调用与返回指令
		- 子程序调用指令
		- 子程序返回指令
	- 中断调用与返回指令
		- 中断向量
		- 中断类型号
		- 中断返回指令
- ## 处理机控制指令
	- 标志操作指令
		- |指令|功能|影响标志|
		  |CLC(clear Carry)|||
		  |STC(set carry)|||
		  |CMC(complement carry)|||
		  |CLD(clear direction)|||
		  |STD(set direction)|||
		  |CLI(clear interrupt)|||
		  ||||
		  ||||
	- 常用处理机控制指令
- ## 块操作指令
	- 块操作指令格式
	- 块操作指令示例