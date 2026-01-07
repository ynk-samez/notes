
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
				- [10100]:destination / goes to be input to the instruction
	- analyze:
		- lw
		- I type
		- t3 register(rd) : 8+3=11 -> [01011]
		- t2 register(rs): 8+2=10 -> [01010]
		- 12($t2): 12(8+2)=12(10)
			- op: 100011
			- rd: 01011
			- rs($t2): 01010
			- shamt: 12
				- [0000 0000 0000 1010]
		- representation
			- 100011 01010 01011 /0000 0000 0011 0000
		- addi $t2, $t2, 4hex
			- t2 (rs): 
			- t2(rd): 8+2 = 10 -> 01010
			- op : [001000]
			- 001000 01010 01010  [0000 0000 0000 0000](shamt)


add $s3, $s5, $t0  
sub $s5, $s3, $s6  
sll $s5, $s5, 2ten  
lw $s3, 120ten($s5)  
slt $t7, $s3, $s5  
addi $s5, $s3, 3ten  
beq $t7, $zero, -3ten  
and $t2, $s3, $s2

sub $s5, $s3, $s6  
- sub
	- R type
	- s5(rd): 16+5=21
	- s3(rs):16+3=19
	- s6(rt):16+6=22
- Binary representation
	- 000000 10011 10110 10101 00000 100010(funct)
- [15-0]
-  1111 1111 1111 1111 + 10101 00000 100010
- F F F F A 8 2 2
- 11111111111111111010100000100010<<2
- 11111111111111101010000010001000<<2
- FFFEA088
	- sll $s5, $s5, 2ten  
		-  R type
		- (rd) s5 ->16+5=21 
		- (rs) x
		- shamt 00010
		- funct 000 000
		- 000000  00000  10101  10101 00010 000000
		- 000000  00000  10101  1010 1000 1000 0000
	- extended
		- 1111 1111 1111 1111 1010　1101　0100　0100　00000
		- F F F F a  8 8 0
		-  11111111111111111010100010000000
		-  1111 1111 1111 1111 1010 1000 1000 0000
		- F F F F a 8 8 0
		- 11111111111111101010001000000000
![[Pasted image 20260107215949.png]]



- addi $t8, $s2, 20
- t8 = 8+8=16
- s2= 16+2=18
- op: 001000
- rs: 16 
- rt: 18
- 001000 10000 10010 0000 0000 0001 0100

- 0000 0000 0000 0000 0000 0000 0001 0100
- 00 0000 0000 0000 0000 0000 0001 010000

- lw s4, 34ten($t9)
- s4=16+4=20
- t9=8+9=17
- 100011 10001 10100  0000 0000 0010 0010
-  00000000000000000000000000100010
- 