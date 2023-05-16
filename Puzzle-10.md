# Puzzle 10

```shell
00      38          CODESIZE
01      34          CALLVALUE
02      90          SWAP1
03      11          GT
04      6008        PUSH1 08
06      57          JUMPI
07      FD          REVERT
08      5B          JUMPDEST
09      36          CALLDATASIZE
0A      610003      PUSH2 0003
0D      90          SWAP1
0E      06          MOD
0F      15          ISZERO
10      34          CALLVALUE
11      600A        PUSH1 0A
13      01          ADD
14      57          JUMPI
15      FD          REVERT
16      FD          REVERT
17      FD          REVERT
18      FD          REVERT
19      5B          JUMPDEST
1A      00          STOP
```

1. `SWAP1` - Takes the top most 2 values from the stack s[-2] and s[-1] and swap and it becomes like this s[-2] , s[-1] -> s[-1], s[-2].

2. `MOD` - Modulo remainder operation.

3. `ISZERO` - Take the top most 1 value from the stack s[-1] if it is 0 and then return 1 otherwise 0.

4. `ADD` - Takes the top most 2 values from the stack s[-2] and s[-1] and perform addition and add value to the stack.

Solution : Puzzle 10
---
First Take Look at this 

```shell
00      38          CODESIZE
01      34          CALLVALUE
02      90          SWAP1
03      11          GT
04      6008        PUSH1 08
06      57          JUMPI
07      FD          REVERT
08      5B          JUMPDEST
```

First we add `CODESIZE` to stack and after `CALLVALUE` and we will swap this two. then it checks the `CODESIZE > CALLVALUE` then it will return 1 `CALLVALUE` will be `19` then it passes the condition and `JUMPI` to the `JUMPDEST`.

now let's Look after this remaining

```shell
09      36          CALLDATASIZE
0A      610003      PUSH2 0003
0D      90          SWAP1
0E      06          MOD
0F      15          ISZERO
10      34          CALLVALUE
11      600A        PUSH1 0A
13      01          ADD
14      57          JUMPI
15      FD          REVERT
16      FD          REVERT
17      FD          REVERT
18      FD          REVERT
19      5B          JUMPDEST
1A      00          STOP
```

`CALLDATASIZE` pushed to stack and after `0003` to stack and `CALLVALUE` and `0003` it will swap and checks `MOD` condition if we need to pass this test then we need 3 because `MOD` opeartion will give remainder which is 0 the condition statisfy. and it will check if `ISZERO` top most value is `0` then it will become `1`. our target destination instruction `19` and adding 9 as wei value will revert the excution so what went wrong? if we see this in hex  `CALLVALUE` and `0A` (`10` in dec) perform `ADD` and perform our `CALLVALUE` is `15` (dec) in `0F` so we need to add Both of them `0A + 0F = 19`. then we will get to `JUMPDEST` which is instruction `19` so the callvalue must be `15`.

Here's the answer to your puzzle `CALLDATA` needs to be `0xAABBCC` so `CALLDATASIZE` becomes the `3` and `CALLVALUE` `15`.