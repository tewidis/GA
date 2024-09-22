# Divide and Conquer 4: FFT

## Polynomial Multiplication

1. Multiplying polynomials using Fast Fourier Transform
    * Polynomials A(x) and B(x)
        - A(x) = a~0~ + a~1~x + a~2~x^2^ + ... + a~n-1~x^n-1^
        - B(x) = b~0~ + b~1~x + b~2~x^2^ + ... + b~n-1~x^n-1^
    * Want C(x) = A(x)B(x)
        - C(x) = c~0~ + c~1~x + c~2~x^2^ + ... + c~2n-2~x^2n-2^
        - c~k~ = a~0~b~k~ + a~1~b~k-1~ + ... + a~k~b~0~
    * Given a = (a~0~, a~1~, ..., a~n--1~) and b = (b~0~, b~1~, ..., B~n--1~)
        - Compute c = a \* b = (c~0~, c~1~, ..., c~n--1~)
        - Convolution of a and b

## Quiz: PM Example

1. A(x) = 1 + 2x + 3x^2^
    * a = (1, 2, 3)
2. B(x) = 2 - x + 4x^2^
    * b = (2, -1, 4)
3. c = a \* b = (2,3,8,5,12)

## PM: General Problem

1. Given a = (a~0~, a~1~, ..., a~n--1~) and b = (b~0~, b~1~, ..., B~n--1~)
    * Compute c = a \* b = (c~0~, c~1~, ..., c~n--1~)
    * Convolution of a and b
2. Naive solution: O(k) time for c~k~ => O(n^2^) total time
    * FFT: O(nlogn)

## Convolution Applications

1. Filtering: data y = (y~1~, ..., y~n~)
    * Applications: Reducing noise, adding effects
    * Mean filtering: Replace value with moving mean of surrounding values
    * Gaussian filtering: Replace value with Gaussian weighting of surrounding
    values
    * Gaussian blur: 2-dim Gaussian filter

## Polynomials Basics

1. Polynomial A(x) = a~0~ + a~1~x + a~2~x^2^ + ... + a~n-1~x^n-1^
    * Two natural representations for A(x):
        - Coefficients a = (a~0~, a~1~, ..., a~n-1~)
        - Values: A(x~1~), A(x~2~), ..., A(x~n~)
    * Lemma: Polynomial of degree n-1 is uniquely determined by its values at
    any n distinct points
    * FFT converts from coefficients to values and values to coefficients
        - For particular x~1~, ..., x~n~

## PM: Values

1. Key idea: Multiplying polynomials is easy in values representation
    * Given A(x~1~), ..., A(x~2n~) and B(x~1~), ..., B(x~2n~)
    * for i = 1 -> 2n C(x~i~) = A(x~i~)B(x~i~)
        - O(1) time for each
        - O(n) total time

## FFT: Opposites

1. Given a = (a~0~, a~1~, ..., a~n-1~) for polynomial A(x) = a~0~ + a~1~x + 
a~2~x^2^ + ... + a~n-1~x^n-1^
    * Want to compute A(x~1~), A(x~2~), A(x~2n~) for 2n points x~1~,...,x~2n~
    that we choose
2. Key: Suppose x~1~, ..., x~n~ are opposite of x~n+1~, ..., x~2n~
    * So: x~n+1~ = -x~1~, x~n+2~ = -x~2~
        - Plus/minus property

## FFT: Splitting A(x)

1. Plus/minus property: x~1~, ..., x~n~ are opposite of x~n+1~, ..., x~2n~
    * Look at A(x~i~) and A(x~n+i~) = A(-x~i~)
        - Even terms a~2k~x^2k^ - same
        - Odd terms a~2k+1~x^2k+1^ - opposite
    * Let a~even~ = (a~0~, a~2~, a~4~, ..., a~n-2~)
    * Let a~odd~ = (a~1~, a~3~, a~5~, ..., a~n-1~)

## FFT: Even and Odd

1. Given a = (a~0~, a~1~, ..., a~n-1~) for polynomial A(x) = a~0~ + a~1~x + 
a~2~x^2^ + ... + a~n-1~x^n-1^
    * Let a~even~ = (a~0~, a~2~, a~4~, ..., a~n-2~)
    * Let a~odd~ = (a~1~, a~3~, a~5~, ..., a~n-1~)
2. A~even~(y) = a~0~ + a~2~y + a~4~y^2^ + ... + a~n-2~y^(n-2)/2^
3. A~odd~(y) = a~1~ + a~3~y + a~5~y^2^ + ... + a~n-1~y^(n-2)/2^
4. A~even~ and A~odd~ are degree n/2 - 1
5. Note: A(x) = A~even~(x^2^) + xA~odd~(x^2^)

## FFT: Recursion

1. A(x) = A~even~(x^2^) + xA~odd~(x^2^)
    * Plus/minus property: x~1~, ..., x~n~ are opposite of x~n+1~, ..., x~2n~
    * A(x~i~) = A~even~(x~i~^2^) + x~i~A~odd~(x~i~^2^)
    * A(x~n+i~) = A(-x~i~) = A~even~(x~i~^2^) - x~i~A~odd~(x~i~^2^)
2. Given A~even~(y~1~) ..., A~even~(y~n~) and A~odd~(y~1~), ..., A~odd~(y~n~)
    * for y~1~ = x~1~^2^, ..., y~n~=x~n~^2^
    * Takes O(n) time to get A(x~1~), ..., A(x~2n~)

## FFT: Summary

1. To get A(x) of degree <= n-1 at 2n points x~1~, ..., x~2n~
    * Define A~even~(y) and A~odd~(y) of degree <= n/2 - 1
    * Recursively evaluate at n points
        - y~1~ = x~1~^2^ = x~n+1~^2^
        - y~2~ = x~2~^2^ = x~n+2~^2^
        - y~n~ = x~n~^2^ = x~2n~^2^
    * In O(n) time, get A(x) at x~1~, ..., x~2n~
2. T(n) = 2T(n/2) + O(n)
    * Evaluates to O(nlogn)

## FFT: Recursive Problem

1. Choose: x~n+1~ = -x~1~, x~n+2~ = -x~2~, x~2n~ = -x~n~
    * Next level: y~1~ = x~1~^2^, ..., y~n~ = x~n~^2^
        - y~1~ = -y~n/2+1~ <=> x~1~^2^ = -x~n/2+1~^2^
    * For real numbers, the square of a number is always positive, so
    x~1~^2^ = -x~n/2+1~^2^ will never be true
        - Need to use complex numbers

## Review: Complex Numbers

1. z = a + b~i~
    * z = (a,b)
    * Alternatively, z = (r,theta) in polar coordinates
    * (a,b) = (rcos(theta),rsin(theta))
    * Euler's formula: r(cos(theta) + isin(theta)) = re^itheta^

| ![complex](images/lesson6_complex_plane.png) |
|:--:|
| Complex Numbers |

## Multiplying in Polar

1. Polar is convenient for multiplication
    * z~1~z~2~ = (r~1~r~2~,theta~1~ + theta~2~)

| ![complex](images/lesson6_complex_number_multiplication.png) |
|:--:|
| Complex Number Multiplication |

## Complex Roots

1. n^th^ complex roots of unity
    * What number raised to the nth power equals 1?
        - n = 2: 1, -1
        - n = 4: 1, -1, i, -i
    * z where z^n^ = 1

## Roots: Graphical View

1. z where z^n^ = 1 = (1,2pij) for integer j
    * z = (r,theta)

| ![roots](images/lesson6_nth_roots.png) |
|:--:|
| nth Roots |

## Roots: Notation

1. (1,2pin/j) for j = 0, 1, ..., n-1
    * theta = 2pi/n
    * Let w~n~ = (1, 2pi/n) = e^2ipi/n^
2. n^th^ roots of unity:
    * w~n~^0^, w~n~^1^, ..., w~n~^n-1^
    * w~n~^j^ = e^2ipij/n^

## Roots: Examples

1. n = 2: 1, -1
2. n = 4: 1, i, -1, -i
3. (n^th^ roots)^2^ = n/2 roots
    * w~16~^2^ = w~8~
    * Plus/minus property
        - w~n~^j^ = -w~n~^j+n/2^

## Complex Roots Practice

1. Consider the n^th^ roots of unity for n = 16
    * What is w~16~ in polar coordinates?
    * (1, pi/8)
2. Consider w~16~. For what power k is (w~16~)^k^ = -1?
    * k = 8
    * -1 = (1,pi) and if z = (r,theta) then zk = (rk,kthetha)
3. Consider w~16~. For what power k is (w~16~)^k^ = -w~16~?
    * k = 9
4. Consider w~16~. For what power k is (w~16~)^-1^ = -w~16~^k^?
    * k = 15
5. Consider w~16~. For what power k is (w~16~)^k^ = -w~8~^2^?
    * k = 4

## Key Property: Opposites

1. Properties of n^th^ roots of unity:
    * For even n: Satisfy plus/minus property
        - First n/2 are opposite of last n/2
            + w~n~^0^ = -w~n~^n/2^
            + w~n~^1^ = -w~n~^n/2+1^
            + w~n~^n/2-1^ = -w~n~^n-1^

## Key Property: Squares

1. Properties of n^th^ roots of unity:
    * For n = 2^k^:
        - (n^th^ roots)^2^ = n/2 roots

| ![roots](images/lesson6_nth_roots_squared.png) |
|:--:|
| nth Roots Squared |

