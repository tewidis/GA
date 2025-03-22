# NP4: Knapsack

## Knapsack Lecture Outline

1. NP-completeness:
    * All of NP -> SAT -> 3SAT -> IS
        - 3SAT -> Subset-Sum -> Knapsack
        - IS -> Clique, Vertex Cover
2. DP solution to knapsack is O(nB), not polynomial

## Subset Sum

1. Input: Positive integers a~1~, ..., a~n~ and t
2. Output: Subset S of {1, ..., n} where:
    * sum(a~i~) = t
    * Return NO if no such subset exists
3. Dynamic programming: Give an O(nT) algorithm

## Subset Sum in P?

1. Claim: Subset-sum is known to be in P
    * False; subset-sum is not known to be polynomial in the input size

## Subset-Sum NP-complete

1. Theorem: Subset-sum problem is NP-complete
    * Subset-sum is in NP
        - Given inputs a~1~, ..., a~n~, t and S, check that sum(a~i~) = t, which
        takes O(nlogt)
    * Reduce 3SAT to subset-sum

## 3SAT Subset-Sum: Input

1. Input to subset-sum: 2n + 2m + 1 numbers
    * v~1~, v~1~', ..., v~n~, v~n~' and t
    * All are <= n + m digits long and base 10
        - t is on the order of 10^n+m^

## 3SAT Subset-Sum: Variables

1. v~i~ corresponds to x~i~: v~i~ in S <=> x~i~ = T
2. v~i~' corresponds to !x~i~: v~i~' in S <=> x~i~ = F
    * Need to ensure exactly one of v~i~ or v~i~' is in S
    * In i^th^ digit of v~i~, v~i~' and t put a 1
        - All other numbers put a 0

## 3SAT Subset-Sum: Example

| ![example](images/np4_example1.png) |
|:--:|
| Example |

## 3SAT Subset-Sum: Clauses

1. Digit n+j corresponds to clause C~j~
    * If x~i~ in C~j~, put a 1 in digit n+j for v~i~
    * If !x~i~ in C~j~, put a 1 in digit n+j for v~i~'
2. Use S buffer numbers to get to the desired sum for some digit

| ![example](images/np4_example2.png) |
|:--:|
| Example |

## 3SAT Subset-Sum: Buffers

1. Digit n+j corresponds to clause C~j~
    * If x~i~ in C~j~, put a 1 in digit n+j for v~i~
    * If !x~i~ in C~j~, put a 1 in digit n+j for v~i~'
2. Put a 3 in digit n+j of t
    * Use S~j~, S~j~' as buffers:
        - Put a 1 in digit n+j of S~j~ and S~j~'
    * Put a 0 in digit n+j of other numbers

## 3SAT Subset-Sum: Correctness

1. Subset-sum has a solution <=> 3SAT f is satisfiable
    * Take solution S to subset sum
        - For digit i where 1 <= i <= n:
            + To get a 1 in digit i, include v~i~ or v~i~' (not both)
            + If v~i~ in S the x~i~ = T
            + If v~i~' in S then x~i~ = F
        - This provides an assignment

## Proof: Satisfying Assignment

1. Prove the assignment is satisfying
    * For digit n+j  where 1 <= j <= m to get a sum of 3 in digit n+j:
        - Need to include >= 1 literal of C~j~ and use S~j~, S~j~'
    * Therefore, C~j~ is satisfied

## Reverse Implication

1. Subset-sum has a solution <=> 3SAT f is satisfiable
    * Take satisfying assignment for f
        - If x~i~ = T: Add v~i~ to S
        - If x~i~ = F: Add v~i~' to S
            + i^th^ digit of t is correct
        - For clause C~j~: >= 1 literal in C~j~ is satisfied
        - To get a sum of 3 in digit n+j, use S~j~, S~j~'

## Knapsack is NP-complete

1. HW: Prove that knapsack (search) problem is NP-complete
    * Knapsack in NP
    * Known NP-complete problem -> knapsack
        - Use subset-sum
