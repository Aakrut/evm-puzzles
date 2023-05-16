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