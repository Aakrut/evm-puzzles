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