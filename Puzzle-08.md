# Puzzle 8

```shell
00      36        CALLDATASIZE
01      6000      PUSH1 00
03      80        DUP1
04      37        CALLDATACOPY
05      36        CALLDATASIZE
06      6000      PUSH1 00
08      6000      PUSH1 00
0A      F0        CREATE
0B      6000      PUSH1 00
0D      80        DUP1
0E      80        DUP1
0F      80        DUP1
10      80        DUP1
11      94        SWAP5
12      5A        GAS
13      F1        CALL
14      6000      PUSH1 00
16      14        EQ
17      601B      PUSH1 1B
19      57        JUMPI
1A      FD        REVERT
1B      5B        JUMPDEST
1C      00        STOP
```

1. `SWAP5` - Exchange 1st and 6th stack items.
2. `GAS` - Get the amount of available gas, including the corresponding reduction for the cost of this instruction.
3. `CALL` - Message-call into an accoun, It takes 7 input arguments 👇🏻
    - gas: amount of gas to send to the sub context to execute. The gas that is not used by the sub context is returned to this one.
    - address: the account which context to execute.
    - value: value in wei to send to the account.
    - argsOffset: byte offset in the memory in bytes, the calldata of the sub context.
    - argsSize: byte size to copy (size of the calldata).
    - retOffset: byte offset in the memory in bytes, where to store the return data of the sub context.
    - retSize: byte size to copy (size of the return data).
If call made successful then it will return 1 otherwise 0.

Solution : Puzzle 8
---
Same as Last But Some Twist, The Solution we need to pass `REVERT` so we can jump to 1A to 1B so  the we make calldata like this. So `EQ` condition statisfy `FD` Opcode(`REVERT`) + 1. and we will get `1B`. 

```shell
PUSH1 FD // REVERT
PUSH1 00 // this will be use as offset
MSTORE8 //  store 1 byte

PUSH1 01 // how many bytes to be returned
PUSH1 00 // offset
RETURN
```

Here's the answer`60FD60005360016000F3` to your puzzle.