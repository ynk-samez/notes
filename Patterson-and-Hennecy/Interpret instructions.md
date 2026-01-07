
>[!Prelininaries] 
>|register name|index
|--|--|
>|s0~s7|16~23|
>|t0~t7|8~t15|
>

## Excercises
- Machine code
```shell
00af8020 hex
```
- decimal code
```shell
0 0 10 15 8 0 2 0
```
- binary code
 ``` shell
[0000] [0000] [1010] [1111] [1000] [0000] [0010] [0000]
#reformat
[000000] [00101] [01111] [10000] [00000] [100000]
  ```
- interpreting
```shell
op: 000000 --> "R type instruction"
rs: 00011  --> 00101--> 2^2+2^0 = 5 --> a1
rt: 01111 --> 2^3+2^2+2^1+2^0 --> 8+4+2+1 = 15--> t7
rd: 10000 --> 2^4 --> 16 -> s0 
shamt: 00000 --> 0
funct: 100000 --> add
```
- reordering
```MIPS
add $s0,$a1,$t7 
```

>[! Question]
>The initial state is PC=00000100hex, and the contents of register number _n_ are _2n_ (Example: Register number of register $t1 is 9, so the content of register $t1 is "18"). The content of memory address _m_ is _m+1_.
>Answer the values of the signal lines of the CPU when the following instructions are being executed.  
>When ClockCycle is set to 1, the sub instruction is assumed to be executed. 
>```MIPS
>sub $s4, $s7, $s2  
>add $s2, $s4, $t3  
>addi $t2, $t2, 4hex  
>lw $t3, 12($t2)  
>slt $t6, $s6, $t3  
>bne $t6, $zero, 1hex  
>j 108hex  
>sw $t3, 12($t2)
>```
- When the clock cycle is 4:
	- analyse
		- sub
		- s4 register(rd) : 15+4=20 -> [10100]
		- s7 register(rs):  16+7=23 -> [10111]
		- s2 register(rt): 16+2=18 -> [10001]
			- field representation in binary goes to be
				- 000000 10111 10001 10100 00000(shamt) 100010(funct)
			- signal paths
				- [000000]: goes to be input to the control unit
				- [10111]: read register 1
				- [10001]: read register 2
				- [10100]:destination / goes to instruction

