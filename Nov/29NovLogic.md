# java
```java
class Solution {
    public int minimumTime(int[][] grid) {
        int m=grid.length;
        int n=grid[0].length;
        PriorityQueue<int[]> pq=new PriorityQueue<>((a,b)->a[2]-b[2]);  // Array: row, col, value
        boolean[][] visited=new boolean[m][n];
        

        if (grid[0][1] > 1 && grid[1][0] > 1){           
            return -1;
        }

        int[][] moves={ {0,-1},{0,1},{-1,0},{1,0}};

        pq.add(new int[]{0,0,0});
        while(!pq.isEmpty()){
            int[] arr=pq.poll();
            int row=arr[0];
            int col=arr[1];
            int time=arr[2];
            
            if(row==m-1 && col==n-1){
                return time;
            } 

            if(visited[row][col]) continue;
            visited[row][col]=true;


            for(int[] move:moves){
                int nrow=row+move[0];
                int ncol=col+move[1];

                if(nrow>=0 && nrow<m && ncol>=0 && ncol<n && !visited[nrow][ncol]){
                    int newtime=0; 
                    
                    // if(time+1>=grid[nrow][ncol]) newtime=time+1;
                    // else if((grid[nrow][ncol]-time)%2==0) newtime=grid[nrow][ncol]+1; //even
                    // else newtime=grid[nrow][ncol]; //odd

                    int diff=grid[nrow][ncol]-time;                    
                    if(diff<=1) newtime=time+1;                
                    else newtime=time+1+(diff/2)*2;

                    pq.add(new int[]{nrow,ncol,newtime});
                    
                }
            }


        }

        return -1;
    }
}
```


Let's perform a dry run for the given implementation of the `minimumTime` function with a test case to understand how the logic flows step by step.

---

### Test Case:
```java
grid = [
    [0, 1, 3],
    [1, 2, 4],
    [2, 3, 5]
];
```

---

### Explanation of the Code:
- **Priority Queue (`pq`)**:
  - Stores `[row, col, time]` tuples.
  - It processes the smallest `time` first (Dijkstra-like approach).
  
- **Visited Matrix**:
  - Tracks visited cells to avoid re-processing.

- **Moves**:
  - Defines possible directions: left, right, up, down.

- **Key Logic**:
  - Calculate the earliest possible `newtime` to move to the next cell based on the grid value and the current `time`.

---

### Dry Run:

#### Initial Setup:
- Dimensions: `m = 3`, `n = 3`.
- `pq = [[0, 0, 0]]` (starting point with time 0).
- `visited = [[false, false, false], [false, false, false], [false, false, false]]`.

---

#### Iteration 1:
- **Pop**: `[0, 0, 0]` from `pq`.
- **Check**: Not at the bottom-right yet.
- **Mark Visited**: `visited[0][0] = true`.
- **Neighbors**:
  - **Right (0, 1)**:
    - `grid[0][1] = 1`.
    - `time = 0`, `diff = 1 - 0 = 1`.
    - `newtime = 1`.
    - Add `[0, 1, 1]` to `pq`.
  - **Down (1, 0)**:
    - `grid[1][0] = 1`.
    - `time = 0`, `diff = 1 - 0 = 1`.
    - `newtime = 1`.
    - Add `[1, 0, 1]` to `pq`.

- **`pq`**: `[[0, 1, 1], [1, 0, 1]]`.

---

#### Iteration 2:
- **Pop**: `[0, 1, 1]` from `pq`.
- **Check**: Not at the bottom-right yet.
- **Mark Visited**: `visited[0][1] = true`.
- **Neighbors**:
  - **Right (0, 2)**:
    - `grid[0][2] = 3`.
    - `time = 1`, `diff = 3 - 1 = 2`.
    - `newtime = 3`.
    - Add `[0, 2, 3]` to `pq`.
  - **Down (1, 1)**:
    - `grid[1][1] = 2`.
    - `time = 1`, `diff = 2 - 1 = 1`.
    - `newtime = 2`.
    - Add `[1, 1, 2]` to `pq`.

- **`pq`**: `[[1, 0, 1], [1, 1, 2], [0, 2, 3]]`.

---

#### Iteration 3:
- **Pop**: `[1, 0, 1]` from `pq`.
- **Mark Visited**: `visited[1][0] = true`.
- **Neighbors**:
  - **Down (2, 0)**:
    - `grid[2][0] = 2`.
    - `time = 1`, `diff = 2 - 1 = 1`.
    - `newtime = 2`.
    - Add `[2, 0, 2]` to `pq`.

- **`pq`**: `[[1, 1, 2], [0, 2, 3], [2, 0, 2]]`.

---

#### Iteration 4:
- **Pop**: `[1, 1, 2]` from `pq`.
- **Mark Visited**: `visited[1][1] = true`.
- **Neighbors**:
  - **Right (1, 2)**:
    - `grid[1][2] = 4`.
    - `time = 2`, `diff = 4 - 2 = 2`.
    - `newtime = 4`.
    - Add `[1, 2, 4]` to `pq`.
  - **Down (2, 1)**:
    - `grid[2][1] = 3`.
    - `time = 2`, `diff = 3 - 2 = 1`.
    - `newtime = 3`.
    - Add `[2, 1, 3]` to `pq`.

- **`pq`**: `[[2, 0, 2], [0, 2, 3], [2, 1, 3], [1, 2, 4]]`.

---

#### Iteration 5:
- **Pop**: `[2, 0, 2]` from `pq`.
- **Mark Visited**: `visited[2][0] = true`.
- **Neighbors**:
  - **Right (2, 1)**:
    - `grid[2][1] = 3`.
    - Already in `pq`.

- **`pq`**: `[[0, 2, 3], [2, 1, 3], [1, 2, 4]]`.

---

#### Iteration 6:
- **Pop**: `[0, 2, 3]` from `pq`.
- **Mark Visited**: `visited[0][2] = true`.

- **`pq`**: `[[2, 1, 3], [1, 2, 4]]`.

---

#### Final Iterations:
- The process continues similarly until the destination is reached. For `(2, 2)`:
  - Calculated time will be 5.

---

### Final Output:
```java
System.out.println(solution.minimumTime(grid)); // Output: 5
```