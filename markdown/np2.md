# NP 2: 3SAT

## NP-Completeness

1. Prove 3SAT is NP-complete
    * Cook-Levin Theorem (1971): SAT is NP-complete
    * Karp (1972): 21 other problems are NP-complete

## 3SAT

1. 3SAT
    * Input: Boolean formula f in CNF with n variables and m clauses where each
    clause has <= 3 literals
    * Output: Satisfying assignment if one exists and NO otherwise

## Proof Outline

1. We'll show 3SAT is NP-complete
    * Need to show:
        - 3SAT is in NP
        - SAT -> 3SAT
            + Thus, for all A in NP, A -> 3SAT

## 3SAT in NP

1. Given 3SAT input f and T/F assignment for x~1~, ..., x~n~
    * For each clause C in f:
        - In O(1) time can check that at least one literal in C is satisfied
        - O(m) total time

## SAT -> 3SAT

1. Take input f for SAT
    * Need to create f' for 3SAT
        - f' has a satisfying assignment iff f has a satisfying assignment
        - f' has no satisfying assignment iff f has no satisfying assignment
    * Transform satisfying output o' for f' -> o for f
        - o' satisfies f' <=> o satisfies f

| ![sat](images/np2_sat.png) |
|:--:|
| SAT -> 3SAT |

## Example

1. f = (x~3~) ^ (!x~2~ v x~3~ v !x~1~ v !x~4~) ^ (x~2~ v x~1~)
    * Input f' for 3SAT:
        - Keep C~1~ and C~3~ the same
        - For C~2~: Create a new variable y
            + C~2~' = (!x~2~ v x~3~ v y) ^ (!y v !x~1~ v !x~4~)
    * Claim: C~2~ is satisfiable iff C~2~' is satisfiable

## Claim: Forward

1. Proof of Claim:
    * C~2~ = (!x~2~ v x~3~ v !x~1~ v !x~4~)
    * C~2~' = (!x~2~ v x~3~ v y) ^ (!y v !x~1~ v !x~4~)
    * Take satisfying assignment for C~2~
        - if x~2~ = F or x~3~ = T: then set y = F
        - if x~1~ = F or x~4~ = F: then set y = T
    * In any case, C~2~' is satisfied

## Claim: Reverse

1. Proof of Claim:
    * C~2~ = (!x~2~ v x~3~ v !x~1~ v !x~4~)
    * C~2~' = (!x~2~ v x~3~ v y) ^ (!y v !x~1~ v !x~4~)
    * Take satisfying assignment for C~2~'
        - if y = T: then x~1~ = F or x~4~ = F
        - if y = F: then x~2~ = F or x~3~ = T
    * In any case, C~2~ is satisfied

## Quiz: 5-SAT 3-SAT

1. C = (!x~2~ v x~3~ v !x~1~ v !x~4~ v x~5~)
    * Create two new variables y and z
    * Define C' where each clause is of size <= 3
    * C is satisfiable <=> C' is satisfiable
2. C' = (!x~2~ v x~3~ v y) ^ (!y v !x~1~ v z) ^ (!z v !x~4~ v x~5~)
    * C -> C': x~1~ = F, y = T, z = F
    * C' -> C: 
        - if y = F then x~2~ or x~3~ are satisfied
        - if z = T then x~4~ or x~5~ are satisfied
        - y = T and z = F then x~1~ is satisfied
3. For a clause of size k, we will create k-3 new variables and k-2 clauses

## Big Clauses

1. C = (a~1~ v a~2~ v ... a~k~) where a~1~ a~2~, ..., a~k~ are literals
    * Create k-3 new variables y~1~, y~2~, ..., y~k-3~
    * Replace C by k-2 clauses
    * C' = (a~1~ v a~2~ v y~1~) ^ ... ^ (!y~k-4~ v a~k-2~ v y~k-3~) ^ (!y~k-3~ v a~k-1~ v a~k~)
2. C is satisfiable <=> C' is satisfiable

## General Claim: Forward

1. Take assignment to a~1~, ..., a~k~ satisfying C
    * Let a~i~ be min i where a~i~ is satisfied
    * Since a~i~ = T -> (i-1)^st^ clause of C' is satisfied
        - Set y~1~ = y~2~ = ... = y~i-2~ = T to satisfy 1^st^ (i-2)
        - Set y~i-1~ = y~i~ = ... = y~k-2~ = F to satisfy rest

## General Claim: Reverse

1. Take assignment to a~1~, ..., a~k~ and y~1~, ..., y~k-3~ satisfying C'
    * Need >= 1 is T
    * Suppose a~1~, ..., a~k~ = F
        - From clause 1 -> y~1~ = T
        - From clause 2 -> y~2~ = T
        - From clause k-3 -> y~k-3~ = T
            + This means the final clause is not satisfied, so our assumption
            that all of our literals are set to false is incorrect

## SAT 3SAT

1. Consider f for SAT
    * Create input f' for 3SAT:
        - For each clause C in f:
            + if |C| <= 3 then add C to f'
            + if |C| > 3 then create k-3 new variables and add C' as defined before
    * f is satisfiable <=> f' is satisfiable

## 3SAT Correctness

1. Given assignment to x~1~, ..., x~n~ satisfying f
    * for clause C in f
        - There is an assignment to k-3 new variables so that C' is satisfied
2. Given satisfying assignment for f'
    * for C' in f >= 1 literal in C is satisfied
3. f is satisfiable <=> f' is satisfiable

## Satisfying Assignment

1. Consider f for SAT
2. Create input f' for 3SAT:
    * For each clause C in f:
        - if |C| <= 3 then add C to f'
        - if |C| > 3 then
            + create k-3 new variables and add C' as defined before
3. f is satisfiable <=> f' is satisfiable
4. Satisfying assignment o' for f' -> ignore new variables to get o
5. Runtime
    * f has n variables, m clauses
    * f' has O(nm) variables and O(nm) clauses
        - Polynomial

## Practice Problems

1. DPV 8.3: Stingy SAT
2. DPV 8.8: Exact 4-SAT
