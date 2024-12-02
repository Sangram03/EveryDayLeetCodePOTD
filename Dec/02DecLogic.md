# java
```java
class Solution {
    public int isPrefixOfWord(String sentence, String searchWord) {
        String[] arr = sentence.split(" ");               
        int n=arr.length;
        
        for(int i=0; i<n; i++){
            if(arr[i].startsWith(searchWord)){                
                return i+1;
            }
        }

        return -1;
    }
}
```


Let's do a dry run of the `isPrefixOfWord` function from the `Solution` class for an example input.

### Example Input:
- `sentence = "I love programming"`
- `searchWord = "pro"`

### Execution Steps:

1. **Splitting the sentence**:
   - The sentence `"I love programming"` will be split into an array of words: `arr = ["I", "love", "programming"]`.
   - `n = arr.length = 3`.

2. **Loop Iteration**:
   The loop will run from `i = 0` to `i = 2` (since `n = 3`).

   - **Iteration 1 (i = 0)**:
     - `arr[0] = "I"`
     - Check if `"I".startsWith("pro")`: This is **false**, so continue to the next iteration.

   - **Iteration 2 (i = 1)**:
     - `arr[1] = "love"`
     - Check if `"love".startsWith("pro")`: This is **false**, so continue to the next iteration.

   - **Iteration 3 (i = 2)**:
     - `arr[2] = "programming"`
     - Check if `"programming".startsWith("pro")`: This is **true**.
     - Since the condition is true, the function returns `i + 1 = 2 + 1 = 3`.

### Final Output:
- The function returns `3`, which means that `"pro"` is a prefix of the third word `"programming"` in the sentence.

---

### Edge Cases:
- If `sentence = "I am learning"`, and `searchWord = "am"`, it would return `2` because `"am"` is a prefix of the second word `"am"`.
- If `sentence = "Hello world"`, and `searchWord = "world"`, it would return `2` because `"world"` is the second word in the sentence.
- If no word starts with the given prefix, the function will return `-1`.

