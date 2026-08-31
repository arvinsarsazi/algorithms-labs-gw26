# CSCI 3212 Lab 1

## Fibonacci numbers

Source: https://en.wikipedia.org/wiki/Fibonacci_sequence  

The Fibonacci sequence is a sequence of numbers where:  
1. The first and second numbers are both ``1``, that is, ``fibonacci(1) = fibonacci(2) = 1``
2. The numbers that follow are the sum of the previous TWO numbers, so  
``fibonacci(3) = fibonacci(2) + fibonacci(1) = 1 + 1 = 2``  
``fibonacci(4) = fibonacci(3) + fibonacci(2) = 2 + 1 = 3``.

```
TODO: Answer the following questions:
fibonacci(5) = 5
fibonacci(6) = 8
fibonacci(7) = 13
fibonacci(8) = 21
fibonacci(9) = 34
```

## Basic implementation

Let's take a look at an implementation:
```python
def fibonacci(n):
    if n <= 0:
        return 0
    if n == 1:
        return 1
    return fibonacci(n-1) + fibonacci(n-2)
```
You can also find this in ``algorithms-labs-gw26/lab1/fibonacci.py``, and run it: 
```bash
cd algorithms-labs-gw26/lab1
python fibonacci.py
```
The code version also tells you how much time does it take to complete each calculation.
```
TODO:
1. Explain what the code above is doing.
A: It is recursively calling a function to calculate the fibbonaci sequance, with base cases of 1 and 0.
2. What happens if we remove the "if ... return ..." and only keep the last line?
A: There will be overflow, as without base case the algorithm would never end.
3. What is fibonacci(20)? how much time did it take to calculate that?
A: fibonacci(20) = 6765, calculating this took 1.8667 * 10^(-3) seconds.
4. What is fibonacci(30)? how much time did it take to calculate that?
A: fibonacci(30) = 832040, calculating this took 7.4479 * 10^(-2) seconds.
5. How much time did it take you to calculate fibonacci(40)? (this might take a while...)
A: fibonacci(40) = 102334155, calculating this took 6.6714 seconds.
```

## How many function calls?

Modify ``fibonacci_counting.py`` so that it does the same calculation as ``fibonacci.py``, but it also counts how many times the function ``fibonacci(n)`` had to be called. Then answer the following:
```
TODO:
1. How many function calls does fibonacci(1) take? 1
2. How many function calls does fibonacci(5) take? 15
3. How many function calls does fibonacci(10) take? 177
4. Why is it so slow? Where does the complexity come from? The function is called recursively, so we are calling the fibboncai function many times, making it slow.
5. Is this O(n)? is this O(2^n)? Why? It is not O(n), as the recursive calling is definitively not linear and take much longer. We can guess that based on the growth of the above examples, and also logically, for each function call, we are making two more function calls, so at most it is O(2^n). O(2^n) seems reasonable.
6. Is this Ω(n)? Why?
Yes, linear growth is definitively a lower limit for the growth of this recursive fibbonaci function.
```

## Memoization Optimization

Take a look at ``fibonacci_counting.py``, where memoization is used.
```
TODO:
1. How is this one different from the previous one?
Instead of using a recursive algorithm, we are using a cache to store the values we calculate for any number, and then we don't need to call the function again, we can just look at the cache and retrieve the answer for the numbers previously calculated.
2. How much time does it take to calculate fibonacci(30)?
fibonacci(30) = 832040, calculating this took 4.3625e-05 seconds. The function "fibonacci" was called 59 times.
3. Why is it often faster?
It takes many fewer function calls.
4. Also modify this file to count: how many times the function had to be called for fibonacci(30)? 59.
5. Is this O(n)? is this O(2^n)? Why? It is O(n), basically the algorthim is 2n, because for each number we only check fibbonaci of n-1 and n-2 once, so the algorithm is 2n. We can drop the 2 and big O(n) is correct, it is also O(2^n) because that grows much faster and if it is O(n)then it is also O(2^n).
6. Is this Ω(n)? is this Ω(2^n)? Why?
It is Ω(n), but it is not Ω(2^n), because that is not a lower limit.
```

## Extension: Staircase Problem

Implement ``fibonacci_threeway.py``, where:
1. The first, second, and third numbers are ``1``.
2. The numbers afterwards are the sum of the previous **THREE** numbers, instead of two.
3. Your implementation should be optimized, taking less than 1 second to calculate ``fibonacci_threeway(50)``.

## Optional, challenge problems
1. Instead of recursion, implement ``fibonacci(n)`` using iteration instead.
2. ``fibonacci_memoized.py`` fails if you give it a very large input number such as one million - why? Try fixing it.
3. There is an even faster way to calculate fibonacci numbers, in (almost) O(1) time. Read Wikipedia and try to implement it, or if you like a big challenge, implement it without looking it up.