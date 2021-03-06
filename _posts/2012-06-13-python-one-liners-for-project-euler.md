---
layout: post
title: Python one-liners for Project Euler
author: Martin Thoma
date: 2012-06-13 17:00:14.000000000 +02:00
category: Cyberculture
tags: Python, Project Euler
featured_image: 2011/09/Python-Logo.png
---
Today, I've been trying to get used to <a href="../functional-programming-in-python/" title="Functional Programming in Python">Pythons functional programming tools</a> by solving <a href="http://projecteuler.net/about">Project-Euler</a> tasks. To make them more interesting, I've solved them in one line. But I realized, that it is difficult to read online as only about 70 characters get displayed without a scrollbar. So I made multi-line solutions out of them. 

These snippets are also good examples what's possible to do with Python and to show that Python is fast.

<h2>Problem 24</h2>
<blockquote>What is the millionth lexicographic permutation of the digits 0, 1, 2, 3, 4, 5, 6, 7, 8 and 9?</blockquote>
```python
from itertools import permutations, islice
print next(islice(permutations("0123456789"), 999999, 999999 + 1))
```

<h2>Problem 29</h2>
<blockquote>How many distinct terms are in the sequence generated by $a^b$ for $2 \leq a \leq 100$ and $2 \leq b \leq 100$?</blockquote>
```python
d = lambda top: len(set([a**b for a in xrange(2,top+1) 
                                      for b in xrange(2, top+1)]))
```

<h2>Problem 34</h2>
<blockquote>145 is a curious number, as 1! + 4! + 5! = 1 + 24 + 120 = 145.
Find the sum of all numbers which are equal to the sum of the factorial of their digits.
Note: as 1! = 1 and 2! = 2 are not sums they are not included.</blockquote>
```python
from math import factorial
l = lambda n: reduce(lambda x, y: int(x) + factorial(int(y)), 
                     [d for d in "0" + str(n)])
print(reduce(lambda x,y: x+y, 
             filter(lambda x: x == l(x), 
                    xrange(3, 100000))))
```

<h2>Problem 36</h2>
<blockquote>The decimal number, 585 = 10010010012 (binary), is palindromic in both bases.
Find the sum of all numbers, less than one million, which are palindromic in base 10 and base 2.</blockquote>
```python
palindrom = lambda x: str(x) == str(x)[::-1] and 
                              str(bin(x))[2:] == str(bin(x))[2:][::-1]
d = lambda top: reduce(lambda x,y: x+y, 
                       filter(palindrom, xrange(0,top+1)))
```

<h2>Problem 48</h2>
<blockquote>The series, $1^1 + 2^2 + 3^3 + ... + 10^{10} = 10405071317$.

Find the last ten digits of the series, $1^1 + 2^2 + 3^3 + ... + 1000^{1000}$.</blockquote>


```python
d = lambda top: str(reduce(lambda x,y: x+y, 
                            [i**i for i in xrange(1, top+1)]))[-10:]
```

<h2>Problem 52</h2>
<blockquote>Find the smallest positive integer, x, such that 2x, 3x, 4x, 5x, and 6x, contain the same digits in some order.</blockquote>

```python
digits = lambda n, p: set(str(n*p))
d = lambda n: all(digits(n, 1) ==  digits(n, x) for x in range(2, 7))
print(filter(d, xrange(0, 1000000)))
```

<h2>Problem 53</h2>
<blockquote>How many values of $\binom{n}{r}$, for $1 \leq r \leq n \leq 100$, exceed one-million?</blockquote>
```python
from math import factorial as f
print(sum((f(i) / (f(j) * f(i-j))) > 1000000 for i in range(1, 101) 
		for j in range(1, i)))
```

<h2>Problem 56</h2>
<blockquote>Considering natural numbers of the form, $a^b$, finding the maximum digital sum.</blockquote>

```python
print max([sum([int(c) for c in str(a**b)])
				for a in xrange(1,100) 
				for b in xrange(1,100)])
```

<h2>Problem 97</h2>
<blockquote>Find the last ten digits of the non-Mersenne prime: $28433 \cdot 2^{7830457} + 1$.</blockquote>
```python
print (28433*(2**7830457)+1)%(10**10)
```
