## Binary Numbers
- Each digit (bit) is either 1 or 0 (true or false)
- Each bit represents a power of 2, from left to right:

![binary1](https://github.com/vgorbic1/Tutorials/blob/master/Architecture/images/binary.png)


### Binary to Decimal
Weighted positional notation shows how to calculate the decimal value of each binary bit:

*dec = (D<sub>n-1</sub> x 2<sup>n-1</sup>) + (D<sub>n-2</sub> x 2<sup>n-2</sup>) + ... + (D<sub>1</sub> x 2<sup>1</sup>) + (D<sub>0</sub> x 2<sup>0</sup>) where D is a binary digit*

![binary2](https://github.com/vgorbic1/Tutorials/blob/master/Architecture/images/binary2.png)

**Translation Algorithm**
- Repeatedly divide the decimal integer by 2.
- If there is a remainder (the base number is an odd digit) put *1* in the beginning of a line. If there is no remainder (the base number is an even digit) put *0* in the beginning of a line.
- If the result can be further divieded by 2 (till the division by 0, which is impossible) go to the top of the algorithm.

What is the binary representation of decimal 37?
```
37 / 2 = 18 (1), 18 / 2 = 9 (0), 9 / 2 = 4 (1), 4 / 2 = 2 (0), 2 / 2 = 1 (0), 1 / 2 = 0 (1)

37 = 100101
```

## Hexadecimal Integers

![binary2](https://github.com/vgorbic1/Tutorials/blob/master/Architecture/images/binary3.png)


