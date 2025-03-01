# Max Flow 4

## Max-Flow Min-Cut Algorithms

1. Ford-Fulkerson
    * Find augmenting paths using DFS or BFS
    * O(mC) time where C = size of max flow
        - Assumes integer capacities
2. Edmonds-Karp
    * Find augmenting paths using BFS
    * O(m^2^n) time
        - No assumptions on capacities

## Ford-Fulkerson Algorithm

1. Input: Flow network G=(V,E) with positive integer capacities c~e~
    * Set f~e~=0 for all e in E
    * Build residual network G^f^
    * Check for st-path P in G^f^ using BFS or DFS
    * If no such path, return(f)
    * Let c(P) = min capacity along P in G^f^
    * Augment f by c(P) units along P
    * Go to step 2

## Edmonds-Karp Algorithm

1. Input: Flow network G=(V,E) with positive capacities c~e~
    * Set f~e~=0 for all e in E
    * Build residual network G^f^
    * Check for st-path P in G^f^ using BFS
    * If no such path, return(f)
    * Let c(P) = min capacity along P in G^f^
    * Augment f by c(P) units along P
    * Go to step 2

## Proof Outline

1. Running time: O(m^2^n)
    * Number of rounds <= mn
2. In every round, residual graph changes (>= 1 edge deleted)
3. Key lemma: For every edge e, e is deleted and reinserted later <= n/2 times
    * Since m edges are in the graph, <= mn/2 total rounds

## BFS Properties

1. Lemma: For every edge e, e is deleted and reinserted later <= n/2 times
2. BFS
    * Input: directed G=(V,E), no edge weights, s in V
    * Output: For all v in V, dist(v) = min number of edges s -> v

## BFS Example

1. Run BFS on the following example
    * level(v) = dist(v) = min number of edges s -> v
    * P = s -> a -> d -> t
        - Levels: s = 0, a = 1, d = 2, t = 3

| ![bfs](images/lesson13_bfs.png) |
|:--:|
| BFS Example |

## BFS Properties - Part 2

1. How does level(z) change as G^f^ changes?
    * Claim: For every z in V, level(z) does not decrease

## Add/Delete Edges

1. How does G^f^ change in a round?
    * For vw in E
        - Add vw if flow was full and then reduced
            + This means wv is in P
        - Remove vw if flow is now full
            + This means vw is in P
        - Add wv if flow was empty
            + This means vw is in P
        - Remove wv if flow was positive and now empty
            + This means wv is in P

## Conclusion

1. If add yz to G^f^ then zy is in P
2. If remove yz to G^f^ then yz is in P

## Proof of Claim (Edmonds-Karp Algorithm)

1. Claim: For every vertex z in V, level(z) does not decrease
    * Might decrease if we add edge yz
        - Suppose level(z) = i
        - Add yz to G^f^, so zy in P
        - Because P is a BFS path, level(y) = level(z) + 1
            + This means level(y) = i + 1
            + Level does not decrease

## Delete/Add Effect

1. Say level(v) = i
    * Suppose we delete vw from G^f^ so vw is on the augmented path P
        - level(w) = level(v) + 1 >= i + 1
    * Later add vw in G^f^ so wv in P
        - level(v) = level(w) + 1 >= i + 2
    * So level(v) increases by >= 2

## Finishing Off

1. If we delete vw from G^f^ and later add vw, then level(v) increases by >= 2
2. Minimum level = 0, Maximum level = n
    * delete + add vw <= n/2 times meaning <= nm rounds
