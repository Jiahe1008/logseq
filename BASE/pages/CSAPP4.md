-
- Y86-64指令
	- ||||
	  |halt|00||
	  |nop|10||
	  |rrmovq|20||
	  |irmovq|30||
	  |rmmovq|40||
	  |addq|60||
	  |subq|61||
	  |andq|62||
	  |xorq|63||
	  |jmp|70||
	  |jle|71||
	  |jl|72||
	  |je|73||
	  |jne|74||
	  |jge|75||
	  |jg|76||
	  |cmovle|21||
	  |cmovl|22||
	  |cmove|23||
	  |cmovne|24||
	  |cmovge|25||
	  |cmovg|26||
	  |call|80||
	  |ret|90||
	  |pushq|A0||
	  |popq|B0||
- 寄存器对应编码
	- |||||
	  |0|`rax`|8|`r8`|
	  |1|`rcx`|9|`r9`|
	  |2|`rdx`|A|`r10`|
	  |3|`rbx`|B|`r11`|
	  |4|`rsp`|C|`r12`|
	  |5|`rbp`|D|`r13`|
	  |6|`rsi`|E|`r14`|
	  |7|`rdi`|F|无寄存器|
- ## Y86-64顺序实现
	- 将处理组织成阶段
		- 取指
		- 译码
		- 执行
		- 访存
		- 写回
		- 更新PC
	- SEQ硬件结构
	- ### Y86-64流水线实现
		- 数据冒险
		- 在标准的 5 级流水线（**Fetch, Decode, Execute, Memory, WriteBack**）
- ## 练习题
	- 4-1
		- ```
		  .pos 0x100
		  	irmovq $15, %rbx           30F3 0F00 0000 0000 0000
		      rrmovq %rbx, %rcx          2031
		  loop:                          # 共有12个字节，所以loop起始地址0x010C
		  	rmmovq %rcx, -3(%rbx)      4013 FDFF FFFF FFFF FFFF
		      addq   %rbx, %rcx  		   6031
		      jmp    loop                70 0C01 0000 0000 0000
		  ```
	- 4-2
	- 4-3
		- 去掉与%r8有关指令。将`addq %r8, %rdi` 变成`iaddq $8, %rdi`,`subq %r9, %rsi`变成`iaddq $-1, %rdi`
	- 4-4
		- ```
		  long rsum(long *start, long count)
		  {
		  	if (count <= 0)
		      	return 0;
		      return *start + rsum(start+1, count-1);
		  }
		  ```
		- 用Y86-84编写，先用x86-84编译：
			- 编译指令 `gcc example.c -o example`
		- 直接用Y86-84编写
	- 4-5
		- ```
		  sum_abs:
		      irmovq $8, %r8        # Constant 8
		      irmovq $1, %r9        # Constant 1
		      xorq %rax, %rax       # sum = 0
		      andq %rsi, %rsi       # Set CC
		      jmp test              # Goto test
		  loop:
		      mrmovq (%rdi), %r10   # Get val
		      andq %r10, %r10       # Check sign of val
		      jl is_neg             # If val < 0, goto is_neg
		      addq %r10, %rax       # sum += val
		      jmp update            # Skip negative handling
		  is_neg:
		      subq %r10, %rax       # sum -= val (Smart, huh?)
		  update:
		      addq %r8, %rdi        # start++
		      subq %r9, %rsi        # count--
		  test:
		      jne loop              # Stop when 0
		      ret
		  ```
	- 4-6
	- 4-7
		- ```
		  pushtest:
		  	movq	%rsp, %rax
		      pushq	%rsp
		      popq	%rdx
		      subq	%rdx, %rax
		      ret
		  ```
		- `pushtest`总是返回0. 这意味着压入栈的是`rsp`的原始值。
	- 4-8
	- 4-9
		- `xor`的HCL表达式
		- `bool xor = (a && !b) || (!a && b)`
		- 和`eq`的关系是：`xor = !eq`
	- 4-10
	- 4-11
		- `A <= B && A <= C : A;`
		- `B <= C           : B;`
		- `1                : C;`
	- 4-12
	- 4-13
		- |阶段|通用|具体|
		  |--|--|--|
		  ||`irmovq V, rB`|`irmovq $128, %rsp`|
		  |取指|`icode:ifun <- M1[PC]`[:br]`rA:rB <- M1[PC+1]`[:br]`valC <- M8[PC+2]`[:br]`valP <- PC+10`|`icode:ifun <- M1[0x016] = 3:0`[:br]`rA:rB <- M1[0x017] = F:4`|
		  |译码|||
		  |执行|`valE <- 0 + valC`||
		  |访存|||
		  |写回|`R[rB] <- valE`||
		  |更新PC|`PC <- valP`||
	- 4-14
	- 4-15
	- 4-16
	- 4-17
	- 4-18