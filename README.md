# Ra+

*Dynamically determine EVM exploits*

## Requirements
- Python3 (confirmed 3.6)
- Python modules
    - z3-solver
    - pysha3 (used for convenience to represent sha3 output)
- Graphviz (required to draw the execution path)


## Usage

1. Install required dependencies 

2. Run the application

```bash
python3 ra.py
```

3. Give some EVM bytecode to standard input.

```
606060405260043610610041576000357c0100000000000000000000000000000000000000000000000000000000900463ffffffff1680633ccfd60b14610046575b600080fd5b341561005157600080fd5b61005961005b565b005b3373ffffffffffffffffffffffffffffffffffffffff166000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205460405180602001905060006040518083038185875af192505050156101155760008060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020819055505b5600a165627a7a72305820e598d1a576b5047521cba20260ee9579fee29311bfbb5623191a49ca74a1e4380029
```

4. If the given code has re-entrancy, RA will generate the combination of functions which may cause re-entrancy as `tuple` of function IDs. For example:
 
`('0x3ccfd60b', '0x3ccfd60b', True, 6.267011556017678)`

In this case, `'0x3ccfd60b'` is function ID of the first called function, and `'0x3ccfd60b'` is function ID of the second called (called by malicious contract) function.

## Limitations
- RA cannnot create new contract whose code will be determine dynamically (such part will be symbol variable). This is due to the data type which represents smart contracts. Ra just uses a string as EVM bytecode. Thus, if it is replaced with python list, or temporally fixes such dynamic code, you can analyse such contracts.

- Some EVM opcodes are not implemented in RA's VM. (on roadmap).

## License
This program is released under the MIT license. Author: [wanidon](https://github.com/wanidon)
