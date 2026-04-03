This is a pretty simple similarity comparing algorithm that returns a score between `0` and `1`, meaning `0` - completely different,`1` - exact match. *Generally used for comparing names*.

## Steps 
1. Select the **longest and shortest** words 
2. Calc **matching range** (within wat range of indexes should appear matching chars)
3. **Find matches**
4. **Calculate transpositions** (how many char swaps should be done for the words to become identical)
5. **Jaro Score** 
$$
J = \frac{1}{3} \left( \frac{m}{|s_1|} + \frac{m}{|s_2|} + \frac{m - t}{m} \right)
$$

6. **Jaro-Winkler distance**
$$
JW = J + \min\left(0.1,\ \frac{1}{|max|}\right) \times p \times (1 - J)
$$
Where:
- $m$ = number of matching characters
- $t$ = transpositions (halved)
- $|s_1|, |s_2|$ = lengths of the two strings
- $|max|$ = length of the longer string
- $p$ = length of the common prefix
- Winkler bonus only applied when $J \geq \text{threshold}$ (default $0.7$)

