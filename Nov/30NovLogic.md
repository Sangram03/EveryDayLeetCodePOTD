# java
```java
class Solution {
    List<Integer> circuit;
    public int[][] validArrangement(int[][] pairs) {
        Map<Integer, List<Integer>> graph=new HashMap();
        Map<Integer, Integer> node=new HashMap();

        for(int[] pair:pairs){
            if(!graph.containsKey(pair[0])){
                graph.put(pair[0], new ArrayList());
            }
            graph.get(pair[0]).add(pair[1]);    //Preparing graph
            node.put(pair[0], node.getOrDefault(pair[0],0)-1); //Outgoing
            node.put(pair[1], node.getOrDefault(pair[1],0)+1); //Incoming
        }


        //selecting the starting node
        int startNode=pairs[0][0];
        for(Map.Entry<Integer, Integer> enty:node.entrySet()){
            if(enty.getValue()==-1){
                startNode=enty.getKey();
                break;
            }
        }

        circuit=new ArrayList();
        dfs(graph, startNode);
        Collections.reverse(circuit);
        
       
        int[][] result=new int[pairs.length][2];
        for(int i=1; i<circuit.size(); i++){
            result[i-1][0]=circuit.get(i-1);
            result[i-1][1]=circuit.get(i);
        }

        return result;
    }

    void dfs(Map<Integer, List<Integer>> graph, int u){
        while(graph.containsKey(u) && !graph.get(u).isEmpty()){
            int v=graph.get(u).remove(0);
            dfs(graph, v);
        }
        circuit.add(u);
    }


}
```




The code provided is a solution to the problem of finding a valid arrangement of pairs in the form of a directed Eulerian path in a graph. Let me guide you through the details and steps:

### Overview
The goal is to reorder the pairs into a valid sequence such that:
1. Every pair connects directly to the next.
2. All pairs are used exactly once.

This can be solved by identifying and constructing an **Eulerian path** in the directed graph formed by the pairs.

---

### Code Explanation
1. **Graph Construction**:
   - A directed graph is represented using a `Map<Integer, List<Integer>>`, where keys are nodes and values are lists of their neighbors.
   - A `Map<Integer, Integer>` keeps track of in-degree and out-degree for each node to help identify the starting node.

   ```java
   for (int[] pair : pairs) {
       if (!graph.containsKey(pair[0])) {
           graph.put(pair[0], new ArrayList());
       }
       graph.get(pair[0]).add(pair[1]);  // Adding edges to the graph
       node.put(pair[0], node.getOrDefault(pair[0], 0) - 1); // Outgoing
       node.put(pair[1], node.getOrDefault(pair[1], 0) + 1); // Incoming
   }
   ```

2. **Identify Start Node**:
   - If a node has `-1` in the `node` map, it becomes the starting node.
   - If no node has `-1`, the first node of the first pair is chosen as the default.

   ```java
   int startNode = pairs[0][0];
   for (Map.Entry<Integer, Integer> entry : node.entrySet()) {
       if (entry.getValue() == -1) {
           startNode = entry.getKey();
           break;
       }
   }
   ```

3. **Depth-First Search (DFS)**:
   - Perform DFS to build the Eulerian path by recursively visiting and removing edges until all are used.
   - The path is stored in reverse order, which is corrected by reversing the list later.

   ```java
   void dfs(Map<Integer, List<Integer>> graph, int u) {
       while (graph.containsKey(u) && !graph.get(u).isEmpty()) {
           int v = graph.get(u).remove(0); // Remove edge
           dfs(graph, v);                 // Continue DFS
       }
       circuit.add(u); // Add to the Eulerian circuit
   }
   ```

4. **Generate Result**:
   - Construct the result matrix from the computed Eulerian path (`circuit`).

   ```java
   Collections.reverse(circuit);
   int[][] result = new int[pairs.length][2];
   for (int i = 1; i < circuit.size(); i++) {
       result[i - 1][0] = circuit.get(i - 1);
       result[i - 1][1] = circuit.get(i);
   }
   ```

---

### Running the Code
To execute this code in a Java environment, you can include it in a class and use appropriate test cases to verify its correctness.

#### Example Input:
```java
int[][] pairs = {{1, 2}, {2, 3}, {3, 1}};
```

#### Expected Output:
```java
[[1, 2], [2, 3], [3, 1]]
```

---

Let me know if you'd like further clarification or additional examples!