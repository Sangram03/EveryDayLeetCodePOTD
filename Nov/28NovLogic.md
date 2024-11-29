# java
```java
class Solution {
    public int minimumObstacles(int[][] grid) {

        int m = grid.length, n = grid[0].length;
        int[][] distance = new int[m][n];
        for (int[] row : distance)
            Arrays.fill(row, Integer.MAX_VALUE);
        Deque<int[]> dq = new ArrayDeque<>();

        distance[0][0] = 0;
        dq.offerFirst(new int[] { 0, 0 });
        int[][] directions = { { 0, 1 }, { 1, 0 }, { 0, -1 }, { -1, 0 } };

        while (!dq.isEmpty()) {
            int[] cell = dq.pollFirst();
            int x = cell[0], y = cell[1];
            for (int[] dir : directions) {
                int nx = x + dir[0], ny = y + dir[1];
                if (nx >= 0 && nx < m && ny >= 0 && ny < n) {
                    int newDist = distance[x][y] + grid[nx][ny];
                    if (newDist < distance[nx][ny]) {
                        distance[nx][ny] = newDist;
                        if (grid[nx][ny] == 0) {
                            dq.offerFirst(new int[] { nx, ny });
                        } else {
                            dq.offerLast(new int[] { nx, ny });
                        }
                    }
                }
            }
        }
        return distance[m - 1][n - 1];

    }
}
```


Let’s perform a **dry run** of the `minimumObstacles` method step by step with a sample test case to understand the execution flow.

---

### Test Case:
```java
grid = [
    [0, 1, 1],
    [0, 1, 0],
    [0, 0, 0]
];
```

### Explanation of the Code:
1. **Goal**: Find the minimum number of obstacles to remove to reach the bottom-right corner from the top-left corner.
2. **Distance Array**: Tracks the minimum number of obstacles removed to reach each cell.
3. **Deque (dq)**: A double-ended queue for BFS with 0-cost cells prioritized (processed first).
4. **Directions**: Four possible directions (right, down, left, up).

---

### Initial Setup:
- Dimensions: `m = 3`, `n = 3`.
- `distance`:
  ```
  [0, ∞, ∞]
  [∞, ∞, ∞]
  [∞, ∞, ∞]
  ```
- `dq`: `[[0, 0]]`.

---

### Dry Run:

#### **Iteration 1**:
- **Pop**: `[0, 0]` from `dq`.
- **Neighbors**:
  1. **Right (0, 1)**:
     - `grid[0][1] = 1`.
     - `newDist = distance[0][0] + grid[0][1] = 0 + 1 = 1`.
     - Update: `distance[0][1] = 1`.
     - Add to `dq`: `[[0, 1]]` (end of deque, obstacle cell).
  2. **Down (1, 0)**:
     - `grid[1][0] = 0`.
     - `newDist = distance[0][0] + grid[1][0] = 0 + 0 = 0`.
     - Update: `distance[1][0] = 0`.
     - Add to `dq`: `[[1, 0], [0, 1]]` (front of deque, 0-cost cell).

- **`distance`**:
  ```
  [0, 1, ∞]
  [0, ∞, ∞]
  [∞, ∞, ∞]
  ```
- **`dq`**: `[[1, 0], [0, 1]]`.

---

#### **Iteration 2**:
- **Pop**: `[1, 0]` from `dq`.
- **Neighbors**:
  1. **Right (1, 1)**:
     - `grid[1][1] = 1`.
     - `newDist = distance[1][0] + grid[1][1] = 0 + 1 = 1`.
     - Update: `distance[1][1] = 1`.
     - Add to `dq`: `[[0, 1], [1, 1]]`.
  2. **Down (2, 0)**:
     - `grid[2][0] = 0`.
     - `newDist = distance[1][0] + grid[2][0] = 0 + 0 = 0`.
     - Update: `distance[2][0] = 0`.
     - Add to `dq`: `[[2, 0], [0, 1], [1, 1]]`.

- **`distance`**:
  ```
  [0, 1, ∞]
  [0, 1, ∞]
  [0, ∞, ∞]
  ```
- **`dq`**: `[[2, 0], [0, 1], [1, 1]]`.

---

#### **Iteration 3**:
- **Pop**: `[2, 0]` from `dq`.
- **Neighbors**:
  1. **Right (2, 1)**:
     - `grid[2][1] = 0`.
     - `newDist = distance[2][0] + grid[2][1] = 0 + 0 = 0`.
     - Update: `distance[2][1] = 0`.
     - Add to `dq`: `[[2, 1], [0, 1], [1, 1]]`.

- **`distance`**:
  ```
  [0, 1, ∞]
  [0, 1, ∞]
  [0, 0, ∞]
  ```
- **`dq`**: `[[2, 1], [0, 1], [1, 1]]`.

---

#### **Iteration 4**:
- **Pop**: `[2, 1]` from `dq`.
- **Neighbors**:
  1. **Right (2, 2)**:
     - `grid[2][2] = 0`.
     - `newDist = distance[2][1] + grid[2][2] = 0 + 0 = 0`.
     - Update: `distance[2][2] = 0`.
     - Add to `dq`: `[[2, 2], [0, 1], [1, 1]]`.

- **`distance`**:
  ```
  [0, 1, ∞]
  [0, 1, ∞]
  [0, 0, 0]
  ```
- **`dq`**: `[[2, 2], [0, 1], [1, 1]]`.

---

#### **Iteration 5**:
- **Pop**: `[2, 2]` from `dq`.
- **Check**: Reached the bottom-right corner.

---

### Final Result:
- Minimum number of obstacles to remove: `distance[2][2] = 0`.

---

### Output:
```java
System.out.println(solution.minimumObstacles(grid)); // Output: 0
```