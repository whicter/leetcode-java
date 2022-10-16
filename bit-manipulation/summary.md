## Basic Operators
| Symbol  | Operator           | Description                                 |
| ------- | ------------------ | -------------------------------------       |
|  &      | AND                |  = 1 only if both are 1s                    |
| \|      | OR                 |  = 0 only if both are 0s                    | 
|  ^      | XOR (Exclusive or) |  = 1 if same digits, = 0 if different       |
|  ~      | NOT                |  0 -> 1 or 1 -> 0                           |
|  <<     | Left Shift         |  高位丢弃, 低位补0, 每左移一位相当于乘一次2       |
|  >>     | Right Shift        |  低位丢弃, 高位补0, 符号位不变(two's compliment 每右移一位相当于除一次2|

## Basic Example From [WikiPedia](https://en.wikipedia.org/wiki/Bitwise_operation#Arithmetic_shift)


#### NOT 
```
NOT 0111  (decimal 7)
  = 1000  (decimal 8)```  

```
NOT 10101011
  = 01010100
```  
If two's complement arithmetic is used, then NOT x = -x − 1.


#### AND 
```    
    0101 (decimal 5)
AND 0011 (decimal 3)
  = 0001 (decimal 1)
``` 
 
it becomes easy to check the parity of a binary number by checking the value of the lowest valued bit. Using the example above:

```
    0110 (decimal 6)
AND 0001 (decimal 1)
  = 0000 (decimal 0)
```  

#### OR
```
   0101 (decimal 5)
OR 0011 (decimal 3)
 = 0111 (decimal 7)
```

#### XOR
```
    0101 (decimal 5)
XOR 0011 (decimal 3)
  = 0110 (decimal 6)
```

#### Arithmetic shift

In an arithmetic shift, the bits that are shifted out of either end are discarded. In a left arithmetic shift, zeros are shifted in on the right; in a right arithmetic shift, the sign bit (the MSB in two's complement) is shifted in on the left, thus preserving the sign of the operand.

```
   00010111 (decimal +23) LEFT-SHIFT
=  00101110 (decimal +46)
```

```
   10010111 (decimal −105) RIGHT-SHIFT
=  11001011 (decimal −53)
```

```
   00010111 (decimal +23) LEFT-SHIFT-BY-TWO
=  01011100 (decimal +92)
```
A left arithmetic shift by n is equivalent to multiplying by 2n (provided the value does not overflow), while a right arithmetic shift by n of a two's complement value is equivalent to dividing by 2n and rounding toward negative infinity. If the binary number is treated as ones' complement, then the same right-shift operation results in division by 2n and rounding toward zero.
Logical shift[edit]
Main article: Logical shift

#### Logical shift
In a logical shift, zeros are shifted in to replace the discarded bits. Therefore, the logical and arithmetic left-shifts are exactly the same.

However, as the logical right-shift **_inserts value 0 bits into the most significant bit_**, instead of copying the sign bit, it is ideal for unsigned binary numbers, while the arithmetic right-shift is ideal for signed two's complement binary numbers.

## Applications

#### Basic Facts
      x ^ 0s = x      x & 0s = 0    x | 0s = x
      x ^ 1s = ~x     x & 1s = x    x | 1s = 1s
      x ^ x  = 0      x & x = x     x | x  = x

#### Get Bit
``` java
boolean getBit(int i, int num){
        return ( (num & (1 << i)) != 0 );
}
```

#### Set Bit

``` java

int setBit(int i, int num){
        return num | (1 << i);
}
```

#### Clear Bit
   - Position i
    
      ``` java
         
      int clearBit(int num, int i) {
         int mask = ~(1 << i);
         return num & mask;
      }
      ``` 
      
   - Left most -> i
      ``` java
      
      int clearBitMSBthroughI(int num, int i){
         int mask = (1<< i) -1;
         return num & mask;
      }
      ```

   - Position i -> 0
      ``` java
         
      int clearBitsIThrough0(int i, int num) {
             int mask = ~( (1 << (i+1) )  -1 );
             return num & mask;
      }
      ```
   
#### 去掉数字n中最右一位1
``` java

int clearOne(int num) {
    num = (num & (num - 1));
    return num;
}
```

#### Swap
``` java
   a ^= b;  
   b ^= a;  
   a ^= b;  
```

- a ^= b: a = a ' = (a ^ b)
- b ^= a: b' = b ^ a' = b ^ (a ^ b) = b ^ b ^ a = a
- a ^= b: a = a' ^ b' = (a ^ b) ^ a = a

## Reference
[bit manipulation的总结](https://segmentfault.com/a/1190000004157808)






 
