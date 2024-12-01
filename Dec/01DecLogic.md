# java
```java
import java.util.HashSet;

public class Solution {
    public boolean checkIfExist(int[] arr) {
        HashSet<Integer> set = new HashSet<>();
        for (int num : arr) {
            if (set.contains(num * 2) || (num % 2 == 0 && set.contains(num / 2))) {
                return true;
            }
            set.add(num);
        }
        return false;
    }
}
```




Let's perform a dry run of the `checkIfExist` method step by step using an example array. Suppose we use the input:

```java
int[] arr = {10, 2, 5, 3};
```

### Code Explanation:

1. A `HashSet` is used to keep track of visited numbers.
2. For each number `num` in the array:
   - Check if `num * 2` is already in the set.
   - Check if `num / 2` is already in the set (only if `num` is even).
   - If either condition is true, return `true`.
   - Otherwise, add `num` to the set.

---

### Step-by-Step Dry Run:

#### Initial State:
- `set = {}` (empty)

#### Iteration 1:
- `num = 10`
- Conditions:
  - `set.contains(10 * 2) → set.contains(20) → false`
  - `10 % 2 == 0 && set.contains(10 / 2) → set.contains(5) → false`
- Add `10` to the set.
- `set = {10}`

#### Iteration 2:
- `num = 2`
- Conditions:
  - `set.contains(2 * 2) → set.contains(4) → false`
  - `2 % 2 == 0 && set.contains(2 / 2) → set.contains(1) → false`
- Add `2` to the set.
- `set = {10, 2}`

#### Iteration 3:
- `num = 5`
- Conditions:
  - `set.contains(5 * 2) → set.contains(10) → true`
- Return `true`.

---

### Final Result:
- The method returns `true` because `5 * 2 = 10`, and `10` is already in the set.

### Example of False Case:
For an input like `int[] arr = {1, 3, 7, 11};`, no number satisfies the condition. The method would iterate through the array and return `false`.
