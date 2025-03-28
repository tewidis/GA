# Linear Programming

## LP Geometry

1. Consider a linear program in standard form
    * n variables
    * m constraints
    * Feasible region = convex set
        - Simplex algorithm walks on vertices

## LP Optimum

1. Optimum of LP is achieved at a vertex of the feasible region except if:
    * Infeasible: Feasible region is empty
        - Objective:
            + max(5x-7y)
        - Constraints:
            + x + y <= 1
            + 3x + 2y >= 6
            + x, y >= 0
    * Unbounded

## Infeasible Example

1. Feasible region is empty
    * This is regardless of the objective function

| ![infeasible](images/lp2_infeasible.png) |
|:--:|
| Infeasible Region |

## Unbounded Example

1. Unbounded: Optimal is arbitrarily large
    * Objective:
        - max(x+y)
    * Constraints:
        - x - y <= 1
        - x + 5y >= 3
        - x,y >= 0

| ![unbounded](images/lp2_unbounded.png) |
|:--:|
| Unbounded Region |

## Unbounded to Bounded

1. Whether an LP is bounded or unbounded depends on the objective function and
constraints
    * Objective:
        - max(2x-3y)
    * Constraints:
        - x - y <= 1
        - x + 5y >= 3
        - x,y >= 0
2. Whether an LP is feasible or infeasible depends on the constraints

## LP Optimum - Part 2

1. To determine if a feasible LP is bounded, we must consider the dual of the LP

## Infeasible?

1. Is there any x satisfying?
    * Make a new variable z
        - z can be positive or negative, while x must be greater than zero
    * Add the new variable z to the constraints
        - This allows us to make the constraint trivially satisfiable
    * Run the LP and maximize z
        - If there's a solution where z is greater than 0, the LP is feasible
        - This provides a feasible point for the LP if it is feasible
            + Starting point for simplex algorithm
    * Objective:
        - max(z)
    * Constraint:
        - Ax + z <= b
        - x >= 0
