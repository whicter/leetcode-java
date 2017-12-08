## Basic Operators
| Operator| Name               | Description                                 |
| ------- | ------------------ | -------------------------------------       |
|  &      | AND                |  = 1 only if both are 1s                    |
| \|      | OR                 |  = 0 only if both are 0s                    | 
|  ^      | XOR (Exclusive or) |  = 1 if same digits, = 0 if different       |
|  ~      | NOT                |  0 -> 1 or 1 -> 0                           |
|  <<     | Left Shift         |  高位丢弃, 低位补0                            |
|  >>     | Right Shift        |  低位丢弃, 高位补0, 符号位不变(two's compliment |

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





 
