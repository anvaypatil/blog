---
layout: post
title: "Bloom Filter (Python)"
date: 2020-07-20 13:01:20 +0300
description: Bloom Filter in Python . # Add post description (optional)
img:  python.png # Add image post (optional)
categories: python-language
icon: blogging.png
---

### Code
**Test Code**
```python
n = 2_00_00_000 # number of items to add
p = 0.000001 # false positive probability
bloomf = BloomFilter(n, p)

for item in ['abound', 'abounds', 'abundance', 'abundant']:
    bloomf.add(item)

print(bloomf.check('abound')) # False
print(bloomf.check('abounds')) # True

```

**Implementation**
```python
from bitarray import bitarray
import mmh3
import math

class BloomFilter:
    def __init__(self, items_count: int, fp_prob: float) -> None:
        """
        :param items_count: int
            Number of items expected to be stored in bloom filter
        :param fp_prob: float
            False Positive probability in decimal
        """
        # False possible probability in decimal
        self.fp_prob = fp_prob
        # Size of bit array to use
        self.size = self.get_size(items_count, fp_prob)
        # number of hash functions to use
        self.hash_count = self.get_hash_count(self.size, items_count)
        # Bit array of given size
        self.bit_array = bitarray(self.size)
        self.bit_array.setall(0)

    def add(self, item):
        """
        Add an item in the filter
        :param item:
        :return:
        """
        for i in range(self.hash_count):
            digest = mmh3.hash(item, i) % self.size
            self.bit_array[digest] = True

    def check(self, item):
        """
        Check for existence of an item in filter
        :param item:
        :return:
        """
        for i in range(self.hash_count):
            digest = mmh3.hash(item, i) % self.size
            if not self.bit_array[digest]:
                return False
        return True

    @classmethod
    def get_size(cls, n: int, p: float):
        """
        Return the size of bit array(m) to used using
        following formula
        m = -(n * lg(p)) / (lg(2)^2)
        :param n : int
            number of items expected to be stored in filter
        :param p : float
            False Positive probability in decimal
        """
        m = - (n * math.log(p)) / (math.log(2) ** 2)
        return int(m)

    @classmethod
    def get_hash_count(cls, m: int, n: int):
        """
        Return the hash function(k) to be used using
        following formula
        k = (m/n) * lg(2)
        :param m:int
            size of bit array
        :param n:int
            number of items expected to be stored in filter
        :return: int
        """
        k = (m / n) * math.log(2)
        return int(k)

```