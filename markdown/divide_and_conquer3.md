# Divide and Conquer: Solving Recurrences

## Solving Recurrences

1. Divide and conquer examples:
    * MergeSort
        - T(n) = 2T(n/2) + O(n) = O(nlog(n))
    * Integer Multiplication
        - T(n) = 4T(n/2) + O(n) = O(n^2^)
    * Improved Integer Multiplication
        - T(n) = 3T(n/2) + O(n) = O(n^log~2~3^)
    * Median
        - T(n) = T(3n/4) + O(n) = O(n)

## Example 1

1. T(n) = 4T(n/2) + O(n)
    * For some constant c > 0, T(n) = 4T(n/2) + cn, T(1) <= c
        - T(n) <= cn + 4T(n/2)
        - T(n) <= cn + 4[4T(n/4) + cn/2]
        - T(n) <= cn(1 + 4/2) + 4^2^T(n/4)
        - T(n) <= cn(1 + 4/2) + 4^2^[4T(n/8) + cn/4]
        - T(n) <= cn(1 + 4/2 + (4/2)^2^) + 4^3^T(n/2^3^)

## Expanding Out

1. T(n) <= cn(1 + 4/2 + (4/2)^2^) + 4^3^T(n/2^3^)
    * T(n) <= cn(1 + (4/2) + (4/2)^2^ + ... + (4/2)^i-1^) + 4^i^T(n/2^i^)
        - let i = log~2~n then n/2^i^ = 1
    * T(n) <= cn(1 + (4/2) + (4/2)^2^ + ... + (4/2)^log~2~n-1^) + 4^log~2~n^T(1)
        - cn = O(n)
        - ((4/2)^log~2~n^) = O(n^2^/n) = O(n)
        - 4^log~2~n^ = O(n^2^)
    * Total is O(n^2^)

## Geometric Series

| ![geometric](images/lesson5_geometric_series.png) |
|:--:|
| Geometric Series |

## Manipulating Polynomials

1. 4^log~2~n^ = n^2^
2. 3^log~2~n^ = n^c^
    * 3 = 2^log~2~3^
    * 3^log~2~n^ = (2^log~2~3^)^log~2~n^ = 2^log~2~3\*log~2~n^
    * 2^log~2~3\*log~2~n^ = (2^log~2~n^)^log~2~3^ = n^log~2~3^
    * c = log~2~3

## Example 2

1. T(n) = 3T(n/2) + O(n)
    * T(n) <= cn + 3T(n/2)
    * T(n) <= cn(1 + (3/2) + (3/2)^2^ + ... + (3/2)^i-1^) + 3^i^T(n/2^i^)
        - let i = log~2~n
    * T(n) <= cn(1 + (3/2) + (3/2)^2^ + ... + (3/2)^log~2~n-1^) + 3^log~2~n^T(1)
        - cn = O(n)
        - (1 + (3/2) + (3/2)^2^ + ... + (3/2)^log~2~n-1^) = O((3/2)^log~2~n^) = O(3^log~2~n^)
        - 3^log~2~n^T(1) = O(3^log~2~n^)
    * Total is O(n^log~2~3^)

## General Recurrence

1. Constants a > 0, b > 1
    * T(n) = aT(n/b) + O(n)
    * T(n) = cn(1 + (a/b) + (a/b)^2^ + ... + (a/b)^log~b~n-1^) + a^log~b~n^T(1)
        - If a > b: O(n^log~b~a^)
        - If a = b: O(nlog(n))
        - If a < b: O(n)
    * This is how the Master Theorem is derived
