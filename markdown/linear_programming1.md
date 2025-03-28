# Linear Programming

## Linear Programming

1. Linear programming handles any problem that can be formulated as an
optimization over a set of variables where the goal (objective function) and
constraints can all be expressed as linear functions of the variables
    * Applications to optimization research
2. Outline
    * Introduction
        - Examples
        - General Formulation
        - Simplex
    * Duality
    * Max-SAT approximation

## Linear Programming Lecture Outline

1. Examples
    * Max-flow
    * Simple production
2. Standard form
3. LP duality

## Max-Flow as LP

1. Input: Directed G=(V,E) with capacities c~e~ > 0 for all edges
2. LP: m variables: f~e~ for every edge in E
    * Objective function: Max sum over flow out of a vertex
    * Subject to:
        - For every edge: 0 <= f~e~ <= c~e~
        - For every vertex: sum of flow in equals sum of flow out

## Simple 2D Example

1. Basic production:
    * Company makes A and B
    * How many of each to maximize profit?
    * Each unit of A profits $1 and B profits $6
    * Demand: <= 300 units of A and <= 200 units of B
    * Supply: <= 700 hours, A takes 1 hour and B takes 3 hours

## 2D LP Formulation

1. Variables
    * Let x~1~ = # of units of A to produce per day
    * Let x~2~ = # of units of B to produce per day
2. Objective function
    * max(x~1~ + 6x~2~)
3. Constraints
    * 0 <= x~1~ <= 300
    * 0 <= x~2~ <= 200
    * x~1~ + 3x~2~ <= 700

## 2D LP Recap

1. Formulation 
    * max(x~1~ + 6x~2~) such that
        - x~1~ <= 300
        - x~2~ <= 200
        - x~1~ >= 0
        - x~2~ >= 0
        - x~1~ + 3x~2~ <= 700

## 2D Geometric View

| ![2d](images/lp1_2d_geometric.png) 
|:--:|
| 2D Geometric View |

## Optimum

1. Goal: Maximize x~1~ + 6x~2~ = c
    * Solution:
        - x~1~ = 100
        - x~2~ = 200
        - c = 1300

## Key Issues

1. Optimum may be non-integer
    * What do we do if we require an integer solution? Can round
2. LP is in P
3. Integer linear programming (ILP) is NP-complete
4. Vertex = corner
5. Feasible region is convex
    * Any two points within the feasible region can be connected by a line
    totally contained within the set
    * Therefore, optimal point lies at a vertex
6. Simplex algorithm
    * Local greed approach
    * Start at a vertex and look at its neighboring vertices
    * Continue until we find a vertex that is better than all its neighbors

## 3D Example

1. Products A, B, C
    * Profit: $1 for A, $6 for B, $10 for C
    * Demand: <= 300 for A, <= 200 for B, unlimited for C
    * Supply: <= 1000 total, A takes 1, B takes 3, C takes 2
    * Packaging: <= 500 total, A takes 0, B takes 1, C takes 3

## 3D LP Formulation

1. Objective: max(x~1~ + 6x~2~ + 10x~3~)
2. Constraints
    * Demand: 0 <= x~1~ <= 300
    * Demand: 0 <= x~2~ <= 200
    * Supply: x~1~ + 3x~2~ + 2x~3~ <= 1000
    * Packaging: x~2~ + 3x~3~ <= 500
    * x~1~, x~2~, x~3~ >= 0

| ![3d](images/lp1_3d_geometric.png) 
|:--:|
| 3D Geometric View |

## 3D Geometric View

1. Standard form
    * n variables x~1~, ..., x~n~
    * Objective function:
        - max(c~1~x~1~ + ... + c~n~x~n~)
    * Constraints:
        - a~11~x~1~ + a~12~x1 + ... + a~1n~x~n~ <= b~1~
        - a~m1~x~1~ + a~m2~x1 + ... + a~mn~x~n~ <= b~m~
        - x~1~, ..., x~n~ >= 0

## Standard Form

| ![linalg](images/lp1_linear_algebra.png) 
|:--:|
| Linear Algebra |

## Converting to Standard Form

1. To convert from minimum to maximum, multiply by -1
    * min(c^T^x) <=> max(-c^T^x)
    * a~1~x~1~ + ... + a~n~x~n~ >= b <=> -a~1~x~1~ - ... - a~n~x~n~ <= -b
    * a~1~x~1~ + ... + a~n~x~n~ = b <=> a~1~x~1~ + ... + a~n~x~n~ <= b, >= b
2. Strict inequalities (\<, \>) are not allowed in linear programming
3. Unconstrained variable x (can be positive or negative)
    * Add x^+^ and x^-^ where x^+^ >= 0, x^-^ >= 0
    * x = x^+^ - x^-^

## General Geometric View

1. n variables -> n dimensions
    * n + m constraints
    * Feasible region = Intersection of n+m halfspaces = convex polyhedron

## Vertices

1. Vertex of convex polyhedron:
    * Points satisfying n constraints with equality
    * Points satisfying m constraints with <=
    * nm neighbors per vertex

## LP Algorithms

1. Polynomial-time algorithms:
    * Ellipsoid algorithms
    * Interior point methods
2. Simplex algorithm:
    * Worst-case exponential time
    * Widely used on HUGE LPs; guaranteed to give an optimal answer

## Simplex Algorithm

1. Simplex algorithm:
    * Start at x = 0
    * Look for neighboring vertex with higher objective value
        - Then, move there and repeat
    * If there are multiple vertices with higher objective value, can use
    various heuristics
        - Pick one at random, pick largest
        - Because the feasible region is convex, the surface can not decrease
        and then increase again
    * Else, output(x)

## Simplex Example

1. Start at (0,0,0): profit = 0
2. Move to (300,0,0): profit = 300
3. Move to (300,200,0): profit = 1500
4. Move to (300,200,50): profit = 2000
4. Move to (200,200,100): profit = 2400

| ![3d](images/lp1_3d_geometric.png) 
|:--:|
| 3D Geometric View |
