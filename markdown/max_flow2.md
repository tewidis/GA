# Max Flow 2

## Max-Flow Min-Cut Lecture Outline

1. Max-flow = Min st-cut theorem
    * Image segmentation
2. Correctness of Ford-Fulkerson algorithm

## Recap: Ford-Fulkerson

1. Input: Flow network: Directed G=(V,E) with s,t in V and capacities c~e~ > 0
2. Output: flow f\* of maximum size
    * Size(f) = f^out^(s) = f^in^(t)
3. When does Ford-Fulkerson stop?
    * No augmenting path in residual G^f\*^
4. Lemma: For a flow f\* if no augmenting path in G^f\*^ then f|8 is a max-flow

## Quiz: Verifying Max-Flow

1. Given a flow network and a flow f
    * What is the time to check whether or not f is a max flow?
        - O(n + m)
    * Build residual graph in O(n + m) time, then check for a path from s to t
    in this residual graph
        - Simply run DFS s to check whether t is reachable from s
        - If there is no path, then f is a max-flow
        - If there is a path, then there's an augmenting path and we can increase
        the flow

## Min-Cut Problem

1. Cut is a partition of V = L U R
    * st-cut is a cut where s is in L and t is in R
    * Capacity of a cut is sum of capacities of all edges from L to R

| ![cut](images/lesson12_st_cut.png) |
|:--:|
| st-cut |

## Problem Formulation

1. Minimum st-cut problem:
    * Input: Flow network
    * Output: st-cut (L,R) with minimum capacity
2. Max-flow min-cut theorem: Size of max flow is equal to size of min cut

| ![cut](images/lesson12_min_cut.png) |
|:--:|
| Minimum cut |

## Max-Flow = Min st-Cut

1. Theorem: Size of max-flow = Minimum capacity of a st-cut
    * Creating a minimum cut doesn't necessarily require an s and t like a
    max-flow does
2. Proof:
    * First, max-flow <= min st-cut. Then, max-flow >= min st-cutj
        - Proving both proves equality
    * We'll show: For any flow f and any st-cut (L,R)
        - size(f) <= capacity(L,R)
        - max size(f) <= min capacity(L,R)

## Max-Flow Min st-Cut

1. We'll show: For any flow f and any st-cut (L,R)
    * size(f) <= capacity(L,R)
2. Claim: size(f) = f^out^(L) - f^in^(L)

## Proof of Claim (Max-Flow Min-Cut)

1. Claim: size(f) = f^out^(L) - f^in^(L)
2. Proof:

| ![proof](images/lesson12_proof.png) |
|:--:|
| Proof |

## Finishing Off

1. Claim: size(f) = f^out^(L) - f^in^(L)
2. Want: size(f) <= capacity(L,R)
    * size(f) = f^out^(L) - f^in^(L) <= f^out^(L) <= cap(L,R)
3. Max-flow <= min st-cut capacity

## Reverse Inequality

1. Now we'll show:
    * max size(f) >= min capacity(L,R)
2. Take flow f\* from Ford-Fulkerson algorithm
    * f\* has no st-path in residual G^f\*^
    * We'll construct (L,R) where:
        - max size(f) >= size(f\*) = capacity(L,R)

## Proof of Claim (Max-Flow Min-Cut 2)

1. Take flow f\* with no st-path in residual G^f\*^
    * Let L = vertices reachable from s in G^f\*^
        - Know t is not in L
        - Let R = V - L

## Properties of Cut

1. Flow f\* with no st-path in G^f\*^
    * Capacities of edges aren't important, only which edges are present
    * L = vertices reachable from s in G^f\*^
    * For vw in E, v in L and w in R, f~vw~ = c~vw~
        - This means the total flow out of l f^\*out^(L) = capacity(L,R)
    * For zy in E, z in R and y in L, f\*~zy~ = 0
        - This means for the total flow into l f^\*in^(L) = 0
    * size(f\*) = capacity(L,R)

## Completing the Proof

1. Now we'll show: max size(f) >= min capacity(L,R)
    * Take flow f\* from Ford-Fulkerson algorithm
        - f\* has no st-path in residual G^f\*^
        - We'll construct (L,R) where:
            + size(f\*) = capacity(L,R)
2. Proves that Ford-Fulkerson stops when there is no augmenting path and
outputs the maximum flow
    * Shows we can construct a min st-cut
        - If we take a max flow f\* and set L to be those vertices reachable
        from s in the residual network, then that st-cut has capacity equal
        to the size of the flow
            + Must be a minimum st-cut (optimal)
    * Can both verify a max-flow and create a minimum st-cut
