# Linear Programming

## LP Duality

1. Motivating Example
2. General Form
3. Weak duality theorem
4. Strong duality theorem

## Example

1. Objective:
    * max(x~1~ + 6x~2~ + 10x~3~)
2. Constraints
    * 0 <= x~1~ <= 300
    * 0 <= x~2~ <= 200
    * x~1~ + 3x~2~ + 2x~3~ <= 1000
    * x~2~ + 3x~3~ <= 500
    * x~1~, x~2~, x~3~ >= 0
3. Ran simplex
    * Optimal at (200,200,100)
    * Profit = 2400
    * Given a solution, can we verify that it is optimal?
        - Take linear combinations of constraints to find an upper bound

## Upper Bound

1. Let y = (y~1~, y~2~, y~3~, y~4~) = (0, 1/3, 1, 8/3)
    * y~1~ * C~1~ + y~2~ * C~2~ + y~3~ ^ C~3~ + y~4~ * C~4~
        - C~1~, C~2~, C~3~, C~4~ are constraints
2. Plug in the constraints
    * x~1~y~1~ + x~2~y~2~ + x~1~y~3~ + 3x~2~y~3~ + 2x~3~y~3~ + 3x~3~y~4~ <= 300y~1~ + 200y~2~ + 1000y~3~ + 500y~4~
3. Simplify
    * x~1~(y~1~ + y~3~) + x~2~(y~2~ + 3y~3~ + y~4~) + x~3~(2y~3~ + 3y~4~) <= 300y~1~ + 200y~2~ + 1000y~3~ + 500y~4~
4. Plug in values of y
    * x~1~ + 6x~2~ + 10x~3~ <= 2400
5. The LP is upper bounded by 2400 based on the constraints
    * We have a point that meets the upper bound, so it is optimal

## Dual LP

1. How do we find y? What do we require from y?
    * Coefficient for x~1~ must be at least the coefficient in the objective
    function
        - y~1~ + y~3~ >= 1
        - y~2~ + 3y~3~ + y~4~ >= 6
        - 2y~3~ + 3y~4~ >= 10
    * Any y meeting these three constraints yields an upper bound on the objective
    function
        - Therefore, we want to minimize the right hand side to get the smallest
        possible upper bound
    * min(300y~1~ + 200y~2~ + 1000y~3~ + 500y~4~)
2. Number of variables in the original LP defines the number of constraints in
the dual LP
3. Number of constraints in the dual LP defines the number of constraints in
the original LP

## Dual LP Example

1. Primal LP
    * Objective:
        - max(x~1~ + 6x~2~ + 10x~3~)
    * Constraints
        - 0 <= x~1~ <= 300
        - 0 <= x~2~ <= 200
        - x~1~ + 3x~2~ + 2x~3~ <= 1000
        - x~2~ + 3x~3~ <= 500
        - x~1~, x~2~, x~3~ >= 0
2. Dual LP
    * Objective:
        - min(300y~1~ + 200y~2~ + 1000y~3~ + 500y~4~)
    * Constraints
        - y~1~ + y~3~ >= 1
        - y~2~ + 3y~3~ + y~4~ >= 6
        - 2y~3~ + 3y~4~ >= 10
        - y~1~, y~2~, y~3~ >= 0

## General Form

1. Primal LP
    * max(c^T^x) subject to Ax <= b, x >= 0
        - n variables
        - m constraints
2. Dual LP
    * min(b^T^y) subject to A^T^y >= c, y >= 0
        - m variables
        - n constraints
    * This assumes that the primal LP is in canonical form

## Dual of Dual

1. Primal LP
    * max(c^T^x) subject to Ax <= b, x >= 0
2. Dual LP
    * min(b^T^y) subject to A^T^y >= c, y >= 0
3. Convert dual to canonical form
    * max(-b^T^y) subject to -A^T^y <= -c, y >= 0
4. Take the dual of the dual
    * min(-c^T^z) subject to -Az >= -b, z >= 0
5. Convert to canonical form
    * max(c^T^z) subject to -Az <= -b, z >= 0
6. The dual of the dual is the primal

## Quiz: Dual LP

1. Objective:
    * max(5x~1~ - 7x~2~ + 2x~3~)
2. Constraints:
    * x~1~ + x~2~ - 4x~3~ <= 1
    * 2x~1~ - x~2~ >= 3
    * x~1~, x~2~, x~3~ >= 0
3. How many variables in the dual LP?
    * 2 (one for each constraint)
4. How many constrains in the dual LP? (not counting non-negative constraint)
    * 3 (one for each variable)

## Quiz: Dual LP Constraints

1. Write the dual LP
    * Objective:
        - min(y~1~ - 3y~2~)
    * Constraints:
        - y~1~ - 2y~2~ >= 5
        - y~1~ + y~2~ >= -7
        - -4y~1~ >= 2
2. Need to put the primal LP in standard form
    * 2x~1~ - x~2~ >= 3 becomes -2x~1~ + x~2~ <= -3

## Weak Duality

1. Theorem: Feasible x for primal LP, feasible y for dual LP
    * x^T^x <= b^T^y
    * Primal LP objective function <= dual LP objective function

## Matching Values

1. Corollary: If we find feasible x for primal LP and feasible y for dual LP
where c^T^x = b^T^y then x and y are optimal

## Unbounded LP

1. Corollary: If primal LP is unbounded then dual LP is infeasible
    * Dual must be greater than infinity, not possible
2. Corollary: If dual LP is unbounded, then primal LP is infeasible

## Check Unbounded

1. Check if a primal LP is feasible by adding another variable z and checking if
the solution is non-negative
2. We can check if the dual LP is feasible using the same technique as this
implies that the primal is either unbounded or infeasible
    * If primal is feasible and dual is infeasible, then primal is unbounded

## Weak Duality - Part 2

1. If the primal and dual LP are both bounded and feasible, then there exists an
x and y that are optimal

## Strong Duality

1. Theorem: Primal LP is feasible and bounded iff dual LP is feasible and bounded
2. Primal has optimal x\* iff dual has optimal y\*
    * c^T^x\* b^T^y\*
3. For max-flow problem:
    * Primal is size of max flow
    * Dual is capacity of min st-cut
    * We can prove these are equal using the strong duality theorem
