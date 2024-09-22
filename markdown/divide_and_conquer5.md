# Divide and Conquer 5: FFT

## FFT: High-Level

1. Goal: Evaluate polynomial A(x) of degree <= n-1 at n points
    * N points: n^th^ roots of unity
        - n = 2^k^
    * Define A~even~(y) and A~odd~(y) of degree <= n/2-1
    * Recursively evaluate A~even~ and A~odd~ at (n^th^ roots)^2^
    * Then, O(n) time to get A(x) at n^th^ roots
        - A(x) = A~even~(x^2^) + xA~odd~(x^2^)
    * T(n) = 2T(n/2) + O(n) = O(nlogn)

## FFT: Pseudocode

1. FFT(a,w):
    * Input: coefficients a = (a~0~,a~1~,...,a~n-1~) for polynomial A(x) where n
    is a power of 2
        - w is a n^th^ root of unity
        - Use w = w~n~ = (1,2pi/n) = e^(2ipi/n)^
    * Output: A(w^0^), A(w), A(w^2^), ..., A(w^n-1^)

## FFT: Core

``` Python
FFT(a,w):
    if n == 1:
        return A(1)
    Let Aeven = (a0,a2,a4,...an-2)
    Let Aodd = (a1, a3, ..., an-1)
    Call FFT(Aeven, w^2): get Aeven(w0), Aeven(w2), ..., Aeven(w^(n-2))
    Call FFT(Aodd, w^2): get Aodd(w0), ..., Aodd(w^(n-2))
    # if w == wn then (wn^j)^2 = (wn/2)^j
    for j = 0 to n/2-1:
        A(wj) = Aeven(w^2j) + w^jAodd(w^2j)
        A(w^(n/2+j)) = A(-w^j) = Aeven(w^2j) - w^j * Aodd(w^2j)
    return [A(w0), A(w1) ..., A(wn-1)]
```

| ![fft](images/lesson7_fft_pseudocode.png) |
|:--:|
| FFT Pseudocode |

## FFT: Concise

1. Part of the appeal of the FFT algorithm is how concise it is

| ![fft](images/lesson7_fft_pseudocode_concise.png) |
|:--:|
| FFT Pseudocode Concise |

## FFT: Running Time

1. T(n) = 2T(n/2) + O(n) = O(nlogn)

## Polynomial Multiplication using FFT

1. Input:
    * Polynomials A(x) and B(x)
        - A(x) = a~0~ + a~1~x + a~2~x^2^ + ... + a~n-1~x^n-1^
        - B(x) = b~0~ + b~1~x + b~2~x^2^ + ... + b~n-1~x^n-1^
2. Output:
    * Want C(x) = A(x)B(x)
        - C(x) = c~0~ + c~1~x + c~2~x^2^ + ... + c~2n-2~x^2n-2^
        - c~k~ = a~0~b~k~ + a~1~b~k-1~ + ... + a~k~b~0~
3. Procedure:
    * (r~0~, r~1~, ..., r~2n-1~) = FFT(a, w~2n~)
    * (s~0~, s~1~, ..., s~2n-1~) = FFT(b, w~2n~)
    * for j=0 -> 2n-1: t[j] = r[j] * s[j]
    * Have C(x) at 2n^th^ roots of unity: Run inverse FFT to get coefficients

## Linear Algebra View

1. For point x~j~: A(x~j~) = a~0~ + a~1~x~j~ + ... + a~n-1~x~j~^n-1^
    * A(x~j~) = (1,x~j~,...,x~j~^n-1^) \* (a~0~,a~1~,...,a~n-1~)

| ![linear](images/lesson7_linear_algebra.png) |
|:--:|
| Linear Algebra View |

## LA View of FFT

| ![linear](images/lesson7_linear_algebra_fft.png) |
|:--:|
| Linear Algebra View of FFT |

## LA for Inverse FFT

| ![linear](images/lesson7_linear_algebra_inverse_fft.png) |
|:--:|
| Linear Algebra View of Inverse FFT |

## Inverse FFT

1. Lemma: M~n~(w~n~)^-1^ = 1/n \* M~n~(w~n~^-1^)
    * What is w~n~^-1^?
        - w~n~ * w~n~^-1^ = 1
        - w~n~ * w~n~^n-1^ = w~n~^n^ = w~n~^0^ = 1
    * M~n~(w~n~)^-1^ = 1/n \* M~n~(w~n~^n-1^)

## Inverse FFT via FFT

1. Lemma: M~n~(w~n~)^-1^ = 1/n \* M~n~(w~n~^-1^) = M~n~(w~n~)^-1^ = 1/n \* M~n~(w~n~^n-1^)
    * na = M~n~(w~n~^n-1^)A = FFT(A,w~n~^n-1^)
    * a = 1/n \* FFT(A, w~n~^n-1^)

## Quiz: Inverses

1. What is (w~n~^2^)-1? For what power k is (w~n~)^k^ \* (w~n~)^2^ = 1?
    * k = n - 2
    * w~n~^2^ \* w~n~^n-2^ = w~n~^n^ = 1

## Quiz: Sum of Roots

1. For even n, 1 + w~n~ + w~n~^2^ + ... + w~n~^n-1^?
    * 0
    * w~n~^j^ = -w~n~^n/2+j^

## Proof of Claim (FFT)

1. Claim: For any n^th^ root of unity w where w != 1:
    * 1 + w + w^2^ + ... + w^n-1^ = 0
2. Proof: For any number z (z-1)(1+z+z^2^+...+z^n-1^)
    * = (z + z^2^ + ... + z^n^) - (1 + z + ... + z^n-1^)
    * = z^n^ - 1
    * Let z = w:
        - z^n^ = 1
        * Because we assume w != 1, z-1 != 0, so the second term must equal 0

## Proof of Lemma

1. Need to show:
    * M~n~(w~n~)^-1^ = 1/n \* M~n~(w~n~^-1^)
    * 1/n \* M~n~(w~n~^-1^)M~n~(w~n~) = I
2. For M~n~(w~n~^-1^)M~n~(w~n~):
    * Show entries (k,k) are n and for k != j (k,j) are 0

## Diagonal Entries

1. For M~n~(w~n~^-1^)M~n~(w~n~): Show entry (k,k) = n

| ![proof](images/lesson7_diagonal_entries.png) |
|:--:|
| Diagonal Entries |

## Off-Diagonal Entries

1. For M~n~(w~n~^-1^)M~n~(w~n~): Show entry (k,j) = 0

| ![proof](images/lesson7_off_diagonal_entries.png) |
|:--:|
| Off-diagonal Entries |

## Back to Polynomial Multiplication

1. Input:
    * Polynomials A(x) and B(x)
        - A(x) = a~0~ + a~1~x + a~2~x^2^ + ... + a~n-1~x^n-1^
        - B(x) = b~0~ + b~1~x + b~2~x^2^ + ... + b~n-1~x^n-1^
2. Output:
    * Want C(x) = A(x)B(x)
        - C(x) = c~0~ + c~1~x + c~2~x^2^ + ... + c~2n-2~x^2n-2^
        - c~k~ = a~0~b~k~ + a~1~b~k-1~ + ... + a~k~b~0~
3. Procedure:
    * (r~0~, r~1~, ..., r~2n-1~) = FFT(a, w~2n~)
    * (s~0~, s~1~, ..., s~2n-1~) = FFT(b, w~2n~)
    * for j=0 -> 2n-1: t[j] = r[j] * s[j]
    * Have C(x) at 2n^th^ roots of unity: Run inverse FFT to get coefficients
        - (c~0~, ..., c~2n-1~) = 1/2n * FFT(t, w~2n~^2n-1^)
