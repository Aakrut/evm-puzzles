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
