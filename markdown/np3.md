# NP3: Graph Problems

## Graph Problems Lecture Outline I

1. 3SAT is NP-complete
2. Upcoming:
    * Independent Sets
    * Clique
    * Vertex Cover

## Independent Set

1. For undirected G=(V,E), a subset S in V is an independent set if no edges are
contained in S
    * For all x,y in S, (x,y) is not in E

| ![is](images/np3_independent_set.png) |
|:--:|
| Independent Set |

## Quiz: Max Independent Set

1. The max indepdendent set problem is known to be in NP
    * False; for a given problem to be in NP, a given solution must be verifiable
    in polynomial time. Max IS is not verifiable in polynomial-time.

## Search Version

1. Input: Undirected G=(V,E) and goal g
2. Output: Independent set S with size |S| >= g if one exists and NO otherwise
3. Theorem: The independent set problem is NP-complete

## Proof Outline

1. The independent set problem is NP-complete
    * Need to show independent set is in NP
        - Given input G and goal g and solution S
        - In O(n^2^) time can check all pairs x,y in S: verify (x,y) not in E
        - In O(n) time check |S| >= g
    * Show 3SAT can be reduced to independent set
        - 3SAT is simpler than SAT

## 3SAT IS

1. Consider 3SAT input f with variables x~1~, ..., x~n~ and clauses C~1~, .., C~n~
    * Each clause has size |C~i~| <= 3
2. We'll define a graph G and set g = m (number of clauses)
    * Idea: For each clause C~i~, create |C~i~| vertices

## Clause Edges

1. Clause C = (x~1~ v !x~3~ v x~2~)
    * Add edges between all variables in the clause
2. Indepdendent set S has <= 1 vertex per clause
3. Since g = m, solution has = 1 vertex per clause

| ![clause](images/np3_clauses.png) |
|:--:|
| Clause Edges |

## Variable Edges

1. For each x~i~: Add edges between all x~i~ and all !x~i~

| ![variable](images/np3_variables.png) |
|:--:|
| Variable Edges |

## Example

1. Variables x, y, w, x
    * f = (!x v y v !z) ^ (x v !y v w) ^ (!x v !w) ^ (!y v z v w)

| ![example](images/np3_is_example.png) |
|:--:|
| Example |

## Graph Problems Correctness

1. f has a satisfying assignment if and only if G has an independent set of
size >= g
    * Consider a satisfying assignment for f
        - For each clause C, take 1 of the satisfied literals
            + Add corresponding vertex to S
            + |S| = m = g
        - S has =1 vertex per clause and not both x~i~ and !x~i~ because it
        corresponds to a satisfying assignment (can't have both)
            + No clause edges and no variable edges

## Reverse Implication

1. f has a satisfying assignment if and only if G has an independent set of
size >= g
    * Take independent set S of size >= g has =1 vertex per clause
        - Set corresponding literal to True => every clause is satisfied
            + No contradictory literals since edges x~i~ <-> !x~i~, so valid
            assignment

## NP-hard

1. Max Independent Set Problem
    * IS (search) is in NP-complete
    * Max-IS
        - IS (size at least g) -> Max-IS (max)
            + Straightforward to reduce the search version to the optimization
            version
        - Max-IS is at least as hard as every problem in NP
    * Theorem: Max-Indepdendent Set problem is NP-hard

## Clique

1. Clique = Fully connected subgraph
    * For G=(V,E), subset S is a clique if for all x,y in S, (x,y) is in E
2. Want to find large cliques

| ![clique](images/np3_clique.png) |
|:--:|
| Clique |

## Clique: Search Version

1. Input: G=(V,E) and goal g
2. Output: S in V where S is a clique of size |S| >= g if one exists, NO otherwise
3. Theorem: Clique problem is NP-complete

## Clique: Proof Outline

1. Clique is in NP
    * Given input (G,g) and S
        - For all x,y in S, check that (x,y) in E in O(n^2^)
        - Check that |S| >= g in O(n)
    * Show that clique is at least as hard as every problem in NP-complete
        - Reduce IS to clique

## IS Clique Idea

1. Key idea: Clique is opposite of Independent Set
    * Clique is fully connectd (all edges within S)
    * Independent set has no edges within S
2. For G=(V,E), let !G = (V,!E) where:
    * !E = {(x,y): (x,y) not in E}
        - (x,y) in !E <=> (x,y) not in E
3. Observation:
    * S is a clique in !G <=> S is an independent set in G

## IS Clique

1. Independent Set -> Clique:
    * Given input G=(V,E) and goal g for IS problem, let !G and g be input to
    the clique problem
    * If we get solution S for clique, then return S for IS problem
    * If we get NO, then return NO

## Vertex Cover

1. For G=(V,E), a subset of vertices S is a vertex cover if S "covers every edge"
    * For every (x,y) in E, either x is in S and/or y is in S

| ![vertex](images/np3_vertex_cover.png) |
|:--:|
| Vertex Cover |

## VC: Search Version

1. Input: G=(V,E) and budget b (trying to find minimum vertex cover)
2. Output: Vertex cover S of size |S| <= b if one exists and NO otherwise
3. Theorem: Vertex cover problem is NP-complete

## VC: Proof Outline

1. VC is in NP
    * Given input (G,b) and proposed solution S
        - For every (x,y) in E, >= 1 of x or y are in S in O(n+m) time
        - Check that |S| <= in O(n) time
    * Reduce IS to VC

## VC: Reduction Idea

1. Claim: S is a vertex cover <=> !S is an independent set

## Forward Implication

1. Take vertex cover S
    * For edge (x,y) in E: >= 1 of x or y are in S
        - Therefore, <= 1 of x or y in !S
        - Therefore, no edge contained in !S, so !S is an independent set

## Reverse Implication

1. Take independent set !S
    * For every (x,y) in E, <= 1 of x or y in !S
        - Therefore, >- 1 of x or y in S
        - Therefore, S covers every edge

## IS VC

1. For input G=(V,E) and g for independent set
    * Let b = n - g
    * Run vertex cover on G, b
2. G has a vertex cover of size <= n - g <=> G has an independent set of size >= g

## IS VC Correctness

1. (G,g) for IS -> (G,b) for VC
2. Given solution S for VC return !S as solution to IS problem
3. If NO solution for VC, return NO for IS problem

## Practice Problems

1. DPV 8.4: NP-completeness error
2. DPV 8.10: Proof by generalization
3. DPV 8.14: Clique + IS
4. 8.19: Kite
