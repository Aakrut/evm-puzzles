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