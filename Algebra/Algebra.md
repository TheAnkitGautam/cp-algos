#  1.Binary Exponentiation

### Naive Approach
Raising a to the power of n is expressed naively as multiplication by **a** done n−1 times: **a<sup>n</sup> = a.a …a** However, this approach is not practical for large **a or n**.<br>
Clearly, This is an **O(n)** approach.
<br>
<br>
## Algorithm

The idea of binary exponentiation is, that we split the work using the binary representation of the exponent.

Let's suppose, we need to find 7<sup>5</sup><br>
Let **a** = 7 and **n** = 5 <br>
Now, Let's write **n** in base 2 (or Binary representation), <br>
=> **n** = 101 <br>
**=> 7<sup>5</sup> = 7<sup>101</sup> = 7<sup>1.2<sup>2</sup></sup> . 7<sup>0.2<sup>1</sup></sup> . 7<sup>1.2<sup>0</sup></sup> = 7<sup>4</sup> . 7<sup>1</sup>**<br>

As it can be seen easily from the above example, we only need find the powers **a<sup>1</sup>, a<sup>2</sup>, a<sup>4</sup> ... a<sup>[log n]</sup> (7<sup>4</sup> and 7<sup>1</sup> in the above example)**. 
Luckily this is very easy, since each element in the above sequence is just the square of the previous element.<br>
=> 7<sup>1</sup> = 7<br>
=> 7<sup>2</sup> = (7<sup>1</sup>)<sup>2</sup> = 49<br>
=> 7<sup>4</sup> = (7<sup>2</sup>)<sup>2</sup> = 2401<br>
Now, we only need to multipy the terms whose corresponding bit is set (or bit is 1 ) in the binay representation of **n** <br>
=> To find 7<sup>5</sup>, we need to multiply only two terms i.e. 7<sup>4</sup> and 7<sup>1</sup> <br>
=> So, the final result will be 7<sup>5</sup> = 7<sup>4</sup> . 7<sup>1</sup> = 2401 . 7 = 16807
<br>

## Implementation

``` cpp
long long binExpo(long long a, long long n) 
{
    long long res = 1;
    while (n > 0) 
    {
        if (n & 1)
            res = res * a;
        a = a * a;
        n >>= 1;
    }
    return res;
}    
```

### Time Complexity
The number **n** will always have **[log**<sub>**2**</sub> **n] + 1** digits in its binary representation.
Therefore, we always need to perform only **O(log n)** operations.
