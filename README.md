# evm-puzzles

### My solutions for EVM Puzzles

### You can Download the Repo from this [link.](https://github.com/fvictorio/evm-puzzles) Follow the instructions and you will be on your way to start hacking 🕵🏻.

### [evm.codes](https://www.evm.codes/) will help you all the way, take look at opcodes you are unaware of it and play around with it in playground.

# Puzzle 1 

```shell
00      34      CALLVALUE
01      56      JUMP
02      FD      REVERT
03      FD      REVERT
04      FD      REVERT
05      FD      REVERT
06      FD      REVERT
07      FD      REVERT
08      5B      JUMPDEST
09      00      STOP

```
1. `CALLVALUE` - is similar to the msg.value take value in wei.
2. `JUMP` - It takes a single argument, which is the destination of the jump. 

<br />

Solution : Puzzle 1
---
If we do not pass the correct `CALLVALUE` then it will revert, let's see our target is to get to the `JUMPDEST` which is instruction 8 and so put the `CALLVALUE` as the 8 you will `JUMP` to the instruction 8.

# Puzzle 2 #

```shell
00      34      CALLVALUE
01      38      CODESIZE
02      03      SUB
03      56      JUMP
04      FD      REVERT
05      FD      REVERT
06      5B      JUMPDEST
07      00      STOP
08      FD      REVERT
09      FD      REVERT
```

1. `CODESIZE` - This opcode measures the size of our code in bytes.
2. `SUB` - takes 2 items from the top of the stack `s[-2]`, `s[-1]` and perform substration `s[-2] - s[-1]`.

Solution : Puzzle 2
---
Let's See First We see the `CALLVALUE` and `CODESIZE` we need to add `CALLVALUE` and `CODESIZE` given which is `a` in hex which is `10` in dec and then sub `CODESIZE - CALLVALUE` our target destination is instruction 6 so we want to make sure our `CODESIZE - CALLVALUE` = 6 then `CALLVALUE` will be 4. 


# Puzzle 3 #

```shell
00      36      CALLDATASIZE
01      56      JUMP
02      FD      REVERT
03      FD      REVERT
04      5B      JUMPDEST
05      00      STOP
```

1. `CALLDATASIZE` - Returns the size of the calldata in bytes.

Solution : Puzzle 3
---
Our target destination is at instruction 4 and we need to pass valid `CALLDATASIZE` so we can pass this test (ex. 0xFFEECC calldata size is 3.) but we need to make jump to the instruction 4 so `CALLDATASIZE` need to be 4 `0xAABBCCDD` will be your solution.

# Puzzle 4 #

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
