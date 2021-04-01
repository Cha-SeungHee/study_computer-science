``` py
class Solution:
    def reverseBits(self, n: int) -> int:
        reverse_bits = 0
        for i in range(32):
            reverse_bits = (reverse_bits << 1) + (n & 1)
            n >>= 1
        
        return reverse_bits
```
