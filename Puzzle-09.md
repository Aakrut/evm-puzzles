# Puzzle 9

```shell
00      36        CALLDATASIZE
01      6003      PUSH1 03
03      10        LT
04      6009      PUSH1 09
06      57        JUMPI
07      FD        REVERT
08      FD        REVERT
09      5B        JUMPDEST
0A      34        CALLVALUE
0B      36        CALLDATASIZE
0C      02        MUL
0D      6008      PUSH1 08
0F      14        EQ
10      6014      PUSH1 14
12      57        JUMPI
13      FD        REVERT
14      5B        JUMPDEST
15      00        STOP
```

1. `LT` - Take the top most 2 values from the stack `s[-2]`
and `s[-1]`. if the condition statisfy then 1 otherwise 0.

Solution : Puzzle 9
--- 
Let's see this first 👇
```shell
00      36        CALLDATASIZE
01      6003      PUSH1 03
03      10        LT
04      6009      PUSH1 09
06      57        JUMPI
```

We need to make `CALLDATASIZE` must be greater than 3 and it will check the `LT` condition which is `03 < CALLDATASIZE` which will be 4 means `0xAABBCCDD` and we will get 1 for successfully then after adding `09` to stack and JUMPI condition statisfy and it will `JUMP` to `JUMPDEST` which is instruction `09` and second we need to statisfy this 👇

```shell
0A      34        CALLVALUE
0B      36        CALLDATASIZE
0C      02        MUL
0D      6008      PUSH1 08
0F      14        EQ
10      6014      PUSH1 14
12      57        JUMPI
```
`CALLVALUE` and `CALLDATASIZE` will MUL (multiply) and it will check the if it is 8 if condition statisfy then 1 otherwise 0. and adding 14 to stack and JUMP to JUMPDEST which in this case will be instruction 14, so we `CALLVALUE` will be 2 So it will statisfy the `EQ` which is `CALLDATASIZE * CALLVALUE` (4 * 2) = 8 and it will return 1. 

And Here's the answer to your puzzle `CALLDATA` is `0xAABBCCDD` which means `CALLDATASIZE` is `4` and `CALLVALUE` will be `2`.