
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
op: 000000 --> R type instruction
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


