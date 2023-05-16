# Puzzle 5 

```shell
00      34          CALLVALUE
01      80          DUP1
02      02          MUL
03      610100      PUSH2 0100
06      14          EQ
07      600C        PUSH1 0C
09      57          JUMPI
0A      FD          REVERT
0B      FD          REVERT
0C      5B          JUMPDEST
0D      00          STOP
0E      FD          REVERT
0F      FD          REVERT
```

1. `DUP1` - Duplicate 1st stack item.
2. `MUL` - Take Two top most items from the stack and multiply.
3. `PUSH2` - Place 2 byte item on stack.
4. `EQ` - Returns 1 if the last value on the stack is equal to the previous value, 0 otherwise.
5. `PUSH1` - Place 1 byte item on stack.
6. `JUMPI` - JUMPI is a conditional jump that takes top 2 elements from the stack i.e. destination and condition.

Solution : Puzzle 5
---
First what we need is `CALLVALUE` that will duplicate and multiply with it (eg. `CALLVALUE` = 16 in `dec` but in `hex` 10 and `DUP1` 16 and we take both value from the stack and multiply becomes `100`) then add back to stack and `PUSH2` will add `0100` (in hex) and `EQ` checks if both the top most items are the same or not if yes then return 1 other wise 0. JUMPI same as JUMP but second position must not be 0 otherwise there will be no jump. Therefor `CALLVALUE` will be 16 answer to your puzzle.