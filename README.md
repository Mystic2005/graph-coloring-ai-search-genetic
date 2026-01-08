# Graph Coloring Practical Assignment
Author: Bostangiu Luca-Nicolae

## A* result analysis

I implemented A* algorithm using the state representation, expansion, cost and heuristic functions. I ran three heuristic variants, represented below. For each heuristic I ran A* on all problems:
### 1. h = 0
- Admissible trivial heuristic, but uninformed, so it is really slow but it returns the most optimal cost.
  | Problem | Algorithm | Time | Benefit |
|----------|-----------|--------|-----------|
| P0       |  A*       | 0.000041s     | 5         |
| P1       |  A*      | 0.000087s     | 5         |
| P2       |  A*       | 0.0016s    | 5         |
| P3       |  A*       | 0.45s     | 5         |
| P4       |  A*      | 208.60s     | 5         |
### 2. h = len(state["colors"]) - state["nextnode"]) (estimates the number of remaining nodes)
- Very fast and cheap heuristic ( O(1) ), the fastest out of these 3, but unadmissible and not so well informed, getting bad quality results in the more complicated datasets.
  | Problem | Algorithm | Time | Benefit |
|----------|-----------|--------|-----------|
| P0       |  A*       | 0.000024s     | 5         |
| P1       |  A*      | 0.0023s     | 5         |
| P2       |  A*       | 0.00036s    | 5         |
| P3       |  A*       | 0.00029s     | 6         |
| P4       |  A*      | 0.0010s     | 7         |
### 3. h = active heuristic which verifies for each remaining uncolored node if it s necessary a new color (u can see the code in the heuristic function above)
- More costy, but really well informed, I found this unadmissible heuristic the best as it keeps a balance between speed and the quality of the solution, getting the same results as the admissible one but much much faster. (I explained about admissibility in the active function if u scroll up again)
  | Problem | Algorithm | Time | Benefit |
|----------|-----------|--------|-----------|
| P0       |  A*       | 0.000048s     | 5         |
| P1       |  A*      | 0.00044s     | 5         |
| P2       |  A*       | 0.0014s    | 5         |
| P3       |  A*       | 0.0052s     | 5         |
| P4       |  A*      | 0.16s     | 5         |
### Conclusion
- So, using the first heuristic as reference of corectitude, I concluded the third heuristic, and the one that is implemented in the active heuristic function is the best, getting the correct results the fastest.

## Genetic Algorithm Analysis

I implemented the algorithm with the chromosome representation, fitness, roulette selection, one‑point crossover and uniform mutation.
I tested several parameter configs, modifying: population size, mutation rate and elitism. 

For each configuration, I ran the algorithm three times in order to account for the stochastic nature of genetic algorithms and reported both execution time and solution benefit (number of colors used).

### Config 1

- Config: pop_size=50, offspring_size=50, p_cross=0.9, p_mut= 1/len(problem) ,max_gen=100, elite_n=2

| Problem | Algorithm     | Time (s) | Benefit |
| ------- | ------------- | -------- | ------- |
| Run 0   |               |          |         |
| P0      | GA (Config 1) | 0.024    | 5       |
| P1      | GA (Config 1) | 0.030    | 5       |
| P2      | GA (Config 1) | 0.072    | 5       |
| P3      | GA (Config 1) | 0.068    | 6       |
| P4      | GA (Config 1) | 0.092    | 8       |
| Run 1   |               |          |         |
| P0      | GA (Config 1) | 0.021    | 5       |
| P1      | GA (Config 1) | 0.027    | 5       |
| P2      | GA (Config 1) | 0.043    | 6       |
| P3      | GA (Config 1) | 0.061    | 7       |
| P4      | GA (Config 1) | 0.108    | 9       |
| Run 2   |               |          |         |
| P0      | GA (Config 1) | 0.034    | 5       |
| P1      | GA (Config 1) | 0.048    | 5       |
| P2      | GA (Config 1) | 0.047    | 5       |
| P3      | GA (Config 1) | 0.069    | 7       |
| P4      | GA (Config 1) | 0.106    | 8       |


#### Averages

- This config prioritizes speed over exploration. With a smaller pop_size=50 and minimal elitism (2 individuals), it runs very fast on all problems. It performs the best on smaller problems (P0,P1,P2), consistently finding 5-color solutions. However, on more complex graphs (P3,P4), the limited diversity becomes a constraint: P3 often requires 6–7 colors, while P4 occasionally reaches 9 colors.

| Problem | Algorithm     | Time (s) | Benefit |
| ------- | ------------- | -------- | ------- |
| P0      | GA (Config 1) | 0.026    | 5.00    |
| P1      | GA (Config 1) | 0.035    | 5.00    |
| P2      | GA (Config 1) | 0.054    | 5.33    |
| P3      | GA (Config 1) | 0.066    | 6.67    |
| P4      | GA (Config 1) | 0.102    | 8.33    |




### Config 2

- Config: pop_size=100, offspring_size=100, p_cross=0.9, p_mut=2/len(problem), max_gen=100, elite_n=5

| Problem | Algorithm     | Time (s) | Benefit |
| ------- | ------------- | -------- | ------- |
| Run 0   |               |          |         |
| P0      | GA (Config 2) | 0.069    | 5       |
| P1      | GA (Config 2) | 0.087    | 5       |
| P2      | GA (Config 2) | 0.081    | 5       |
| P3      | GA (Config 2) | 0.170    | 6       |
| P4      | GA (Config 2) | 0.222    | 7       |
| Run 1   |               |          |         |
| P0      | GA (Config 2) | 0.060    | 5       |
| P1      | GA (Config 2) | 0.094    | 5       |
| P2      | GA (Config 2) | 0.140    | 5       |
| P3      | GA (Config 2) | 0.166    | 6       |
| P4      | GA (Config 2) | 0.261    | 8       |
| Run 2   |               |          |         |
| P0      | GA (Config 2) | 0.065    | 5       |
| P1      | GA (Config 2) | 0.083    | 5       |
| P2      | GA (Config 2) | 0.115    | 5       |
| P3      | GA (Config 2) | 0.132    | 6       |
| P4      | GA (Config 2) | 0.249    | 7       |


#### Averages

- This config increases mutation pressure while keeping a moderate population size. The higher mutation rate improves exploration stability but does not significantly improve solution quality for smaller problems. P0–P2 consistently find 5 colors (which is the optimal path), while P3 stabilizes at 6 colors. On the hardest problem (P4), results vary between 7 and 8 colors, indicating improved exploration compared to Config 1 but still some variability.

| Problem | Algorithm     | Time (s) | Benefit |
| ------- | ------------- | -------- | ------- |
| P0      | GA (Config 2) | 0.065    | 5.00    |
| P1      | GA (Config 2) | 0.088    | 5.00    |
| P2      | GA (Config 2) | 0.112    | 5.00    |
| P3      | GA (Config 2) | 0.156    | 6.00    |
| P4      | GA (Config 2) | 0.244    | 7.33    |







### Config 3

- Config: pop_size=200, offspring_size=200, p_cross=0.9, p_mut=2/len(problem), max_gen=150, elite_n=5

| Problem | Algorithm     | Time (s) | Benefit |
| ------- | ------------- | -------- | ------- |
| Run 0   |               |          |         |
| P0      | GA (Config 3) | 0.263    | 5       |
| P1      | GA (Config 3) | 0.290    | 5       |
| P2      | GA (Config 3) | 0.355    | 5       |
| P3      | GA (Config 3) | 0.500    | 5       |
| P4      | GA (Config 3) | 0.743    | 7       |
| Run 1   |               |          |         |
| P0      | GA (Config 3) | 0.275    | 5       |
| P1      | GA (Config 3) | 0.325    | 5       |
| P2      | GA (Config 3) | 0.366    | 5       |
| P3      | GA (Config 3) | 0.555    | 6       |
| P4      | GA (Config 3) | 0.782    | 7       |
| Run 2   |               |          |         |
| P0      | GA (Config 3) | 0.226    | 5       |
| P1      | GA (Config 3) | 0.309    | 5       |
| P2      | GA (Config 3) | 0.357    | 5       |
| P3      | GA (Config 3) | 0.564    | 6       |
| P4      | GA (Config 3) | 0.745    | 7       |


#### Averages

- This config prioritizes exploration and solution stability over execution speed. With a large population size (pop_size=200), extended evolution (max_gen=150), and strong elitism (5 individuals), it significantly increases computational cost. For simpler problems (P0, P1, P2), the algorithm consistently finds the optimal 5-color solutions. On more complex problems (P3, P4), the larger population helps stabilize results: P3 mostly converges to 5–6 colors, while P4 consistently finds 7-color solutions.

| Problem | Algorithm     | Time (s) | Benefit |
| ------- | ------------- | -------- | ------- |
| P0      | GA (Config 3) | 0.255    | 5.00    |
| P1      | GA (Config 3) | 0.308    | 5.00    |
| P2      | GA (Config 3) | 0.359    | 5.00    |
| P3      | GA (Config 3) | 0.540    | 5.67    |
| P4      | GA (Config 3) | 0.757    | 7.00    |

- Overall, this configuration achieves the most stable benefits across runs, but at the cost of substantially longer execution times (though less than a second even for the hardest problem).
