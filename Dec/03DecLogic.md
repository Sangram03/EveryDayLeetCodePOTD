# java
```java
class Solution {
    public String addSpaces(String s, int[] spaces) {
        StringBuilder sb=new StringBuilder();

        sb.append(s.substring(0,spaces[0]));
        int i=1;
        for(; i<spaces.length; i++){
            sb.append(" ");
            sb.append(s.substring(spaces[i-1],spaces[i]));            
        }
        sb.append(" ");
        sb.append(s.substring(spaces[i-1])); 

        return sb.toString();
    }
}
```


### Dry Run of the Code

#### Problem Statement:
The method `addSpaces` takes a string `s` and an array of integers `spaces`. It inserts a space character into the string `s` at the specified indices in the `spaces` array.

---

#### Input:
```java
s = "leetcode"
spaces = [2, 5]
```

---

#### Step-by-Step Execution:

1. **Initialization**:
   - `sb = new StringBuilder()` (an empty string builder).
   - `spaces = [2, 5]`.

2. **Add the First Substring (Before the First Space)**:
   - `sb.append(s.substring(0, spaces[0]))`:
     - `spaces[0] = 2`, so `s.substring(0, 2) = "le"`.
     - `sb = "le"`.

3. **Iterate Over the `spaces` Array**:
   - **First Iteration (`i = 1`)**:
     - `sb.append(" ")`: Adds a space, so `sb = "le "`.
     - `sb.append(s.substring(spaces[i-1], spaces[i]))`:
       - `spaces[i-1] = 2`, `spaces[i] = 5`, so `s.substring(2, 5) = "etc"`.
       - `sb = "le etc"`.

4. **After the Loop**:
   - Add the final space and the last part of the string:
     - `sb.append(" ")`: Adds a space, so `sb = "le etc "`.
     - `sb.append(s.substring(spaces[i-1]))`:
       - `spaces[i-1] = 5`, so `s.substring(5) = "ode"`.
       - `sb = "le etc ode"`.

5. **Return the Result**:
   - Return `sb.toString()`, which is `"le etc ode"`.

---

#### Output:
```java
"le etc ode"
```

---

### Explanation:
- The input string `s = "leetcode"` is modified by inserting spaces at the indices specified in `spaces = [2, 5]`.
- The resulting string is `"le etc ode"`.