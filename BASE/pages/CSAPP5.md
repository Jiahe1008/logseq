### 优化编译器
- ### 程序性能表示
- ### 消除循环
- ### 减少过程调用
	- ```
	  void combine3(vec_ptr v, data_t *dest) {
	  	long i;
	      long length = vec_length(v);
	      data_t *data = get_vec_start(v);
	      
	      *dest = IDENT;
	      for( i = 0; i< length; i++) {
	      	*dest = *dest OP data[i];
	      }
	  }
	  ```
	- ```
	  // Inner loop of combine3. data_t = double, OP = *
	  // dest in %rbx, data+i in %rdx, data+length in %rax
	  .L17:
	  	vmovsb		(%rbx), %xmm0
	      vmulsd		(%rdx),	%xmm0, %xmm0
	      vmovsd		%xmm0, (%rbx)
	      addq 		$8, %rdx
	      cmpq		%rax, %rdx
	      jne			.L17
	  ```
- ### 消除内存引用
- ### 现代处理器
	- 整体操作
		- 指令控制单元ICU和执行单元EU
		-
- ### 循环展开
- ### 并行性
	- 多个累计变量
	- 重新结合变换
- ### 限制因素
- ### 内存性能
- 逻辑地址物理地址转换