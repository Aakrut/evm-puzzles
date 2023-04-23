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

# Puzzle 2 

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


# Puzzle 3 

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

# Puzzle 6 

```shell
00      6000      PUSH1 00
02      35        CALLDATALOAD
03      56        JUMP
04      FD        REVERT
05      FD        REVERT
06      FD        REVERT
07      FD        REVERT
08      FD        REVERT
09      FD        REVERT
0A      5B        JUMPDEST
0B      00        STOP
```

1. `CALLDATALOAD` - It is determined which byte of the data in the calldata will be transferred to the stack.

Solution : Puzzle 6
---
 Our target Destination is `0A` in `hex` (`10` in `dec`) so we need calldata that load `A` in `hex` so we can jump to our destination.

First Let's Play with CALLDATALOAD open this [link](https://www.evm.codes/playground?unit=Wei&callData=0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF&codeType=Mnemonic&code=%27%7E1w0yzz%7E2w31y%27%7E%2F%2F+Example+z%5CnyzCALLDATALOADwzPUSH1+%01wyz%7E_&fork=merge)

and if your run the memonics then it will run `PUSH1 0` and load the calldata which is `ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff`
then if you `PUSH1 31` it will request to pull out last 1 byte from the `CALLDATA`.

Back to the Solution, if we want to make jump to `0A` then we need `CALLDATA` that contains only `0A` which is `0x000000000000000000000000000000000000000000000000000000000000000A` answer to your puzzle.

# Puzzle 7 

```shell
00      36        CALLDATASIZE
01      6000      PUSH1 00
03      80        DUP1
04      37        CALLDATACOPY
05      36        CALLDATASIZE
06      6000      PUSH1 00
08      6000      PUSH1 00
0A      F0        CREATE
0B      3B        EXTCODESIZE
0C      6001      PUSH1 01
0E      14        EQ
0F      6013      PUSH1 13
11      57        JUMPI
12      FD        REVERT
13      5B        JUMPDEST
14      00        STOP
```

1. `CALLDATACOPY` - It will Pop top most 3 values from the stack. here are the input.
     - destOffset: The data to be retrieved from calldata will be saved in memory starting from which byte.
     - offset: Starting from which byte in calldata data will be received
     - size: Byte length to copy
2. `CREATE` - It will Create contract. It will Pop top most 3 values from the stack and here are the inputs.
    - value: value in wei to send to the new account.
    - offset: byte offset in the memory in bytes, the initialisation code for the new account.
    - size: byte size to copy (size of the initialisation code).
3. `EXTCODESIZE` - length of the contract bytecode at address, in bytes.

Solution : Puzzle 7
---
First **READ** This ⬇️
> […] The creation code gets executed in a transaction, which returns a copy of the runtime code, which is the actual code of the contract. As we will see, the constructor is part of the creation code, and not part of the runtime code. The contract’s constructor is part of the creation code; it will not be present in the contract’s code once it is deployed.

When the CREATE opcode is executed, only the code returned by the RETURN opcode is the "runtime code" that will be executed when the deployed contract is called in the future. The other section of the bytecode is only utilized once, for the constructor.

So, our calldata can contain as much code as we like, but we must ensure that the returned code (runtime code) contains just one instruction, so EXTCODESIZE returns one (byte).


Let's have a look at how the RETURN opcode works: It selects two values from the stack and uses them as input for:

memory offset from where to begin reading <br /> 
memory size to read and return

So the opcodes
```shell
PUSH1 00 // for STOP
PUSH1 00 // this will use as offset
MSTORE8 // store

PUSH1 01 // how many bytes to be returned
PUSH1 00 // offset
RETURN
```

Here's The answer `600060005360016000F3` to your puzzle.

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

Solution 
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
