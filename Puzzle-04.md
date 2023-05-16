# Puzzle 4 

```shell
00      34      CALLVALUE
01      38      CODESIZE
02      18      XOR
03      56      JUMP
04      FD      REVERT
05      FD      REVERT
06      FD      REVERT
07      FD      REVERT
08      FD      REVERT
09      FD      REVERT
0A      5B      JUMPDEST
0B      00      STOP
```

1. `XOR` - takes to values from the top of the stack `s[1]` and `s[0]` and perform bit operation.

Solution : Puzzle 4
--- 
You need to know binary bit opeation so you can solve this challenge. First we have need add to `CALLVALUE` and our `CODESIZE` is `c` in (hex which is `12` in dec) and our jump destination is `0a` (binary) `10` (hex) so we  do is convert the `12` which is `1100` in binary and `10` in binary `1010`. and we make xor opeartion `1100 ^ 1010` we will get `0110` which is `6` in dec.`CALLVALUE` will be 6 answer to your puzzle.