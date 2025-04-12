# **Java Revision Guide for LeetCode DSA Problems**

---

## **1. Core Java Syntax**  
### **1.1 Data Types**  
- **Primitives**: `int`, `long`, `double`, `float`, `char`, `boolean`  
- **Objects**: `String`  
- **Type Conversions**:  
  ```java
  String s = "123";  
  int x = Integer.parseInt(s);    // String → int  
  String s2 = String.valueOf(x);  // int → String  
  char c = 'a';  
  int ascii = (int) c;            // char → ASCII  
  ```

### **1.2 Control Structures**  
- **Conditionals**:  
  ```java
  if (a > b) { ... }  
  else if (a < b) { ... }  
  else { ... }  
  switch (var) { case 1: ... break; }  
  ```  
- **Loops**:  
  ```java
  for (int i = 0; i < n; i++) { ... }  
  while (condition) { ... }  
  do { ... } while (condition);  
  ```

### **1.3 Arrays & Strings**  
- **1D/2D Arrays**:  
  ```java
  int[] arr = {1, 2, 3};  
  int[][] matrix = new int[3][4];  
  ```  
- **String Operations**:  
  ```java
  String s = "leetcode";  
  char[] chars = s.toCharArray();  
  int len = s.length();  
  int index = s.indexOf('e');  
  boolean equal = s.equals("test");  
  ```

### **1.4 Math Utilities**  
```java
Math.max(a, b);  
Math.min(a, b);  
Math.abs(x);  
Math.pow(2, 3); // 8.0  
Math.sqrt(16);   // 4.0  
Math.log(10);  
```

---

## **2. Data Structures & Collections**  
### **2.1 Arrays Utility**  
```java
Arrays.sort(arr);  
int pos = Arrays.binarySearch(arr, key);  
boolean equal = Arrays.equals(arr1, arr2);  
```

### **2.2 List**  
- **ArrayList**:  
  ```java
  List<Integer> list = new ArrayList<>();  
  list.add(5);  
  list.get(0);  
  list.remove(0);  
  ```  
- **LinkedList (Deque)**:  
  ```java
  Deque<Integer> dq = new LinkedList<>();  
  dq.addFirst(1);  
  dq.addLast(2);  
  dq.removeFirst();  
  ```

### **2.3 Set & Map**  
- **HashSet**:  
  ```java
  Set<Integer> set = new HashSet<>();  
  set.add(10);  
  set.contains(10);  
  ```  
- **HashMap**:  
  ```java
  Map<Integer, String> map = new HashMap<>();  
  map.put(1, "one");  
  map.get(1);  
  map.containsKey(1);  
  ```

### **2.4 Queue & Stack**  
- **Queue**:  
  ```java
  Queue<Integer> q = new LinkedList<>();  
  q.offer(5);  
  q.poll();  
  ```  
- **Stack**:  
  ```java
  Stack<Integer> stack = new Stack<>();  
  stack.push(10);  
  stack.pop();  
  ```

### **2.5 PriorityQueue (Heap)**  
```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();  
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());  
```

---

## **3. Object-Oriented Concepts**  
### **3.1 Custom Classes**  
- **TreeNode Class**:  
  ```java
  class TreeNode {  
      int val;  
      TreeNode left, right;  
      TreeNode(int x) { val = x; }  
  }  
  ```  
- **Pair Class**:  
  ```java
  class Pair {  
      int x, y;  
      Pair(int x, int y) { this.x = x; this.y = y; }  
  }  
  ```

---

## **4. Algorithmic Patterns**  
### **4.1 Two Pointers**  
```java
int left = 0, right = nums.length - 1;  
while (left < right) {  
    int sum = nums[left] + nums[right];  
    if (sum == target) return true;  
    else if (sum < target) left++;  
    else right--;  
}  
```

### **4.2 Sliding Window**  
```java
int left = 0, sum = 0;  
for (int right = 0; right < nums.length; right++) {  
    sum += nums[right];  
    while (sum > target) {  
        sum -= nums[left];  
        left++;  
    }  
}  
```

### **4.3 Backtracking**  
```java
void backtrack(List<List<Integer>> result, List<Integer> temp, int[] nums, boolean[] used) {  
    if (temp.size() == nums.length) {  
        result.add(new ArrayList<>(temp));  
        return;  
    }  
    for (int i = 0; i < nums.length; i++) {  
        if (used[i]) continue;  
        used[i] = true;  
        temp.add(nums[i]);  
        backtrack(result, temp, nums, used);  
        used[i] = false;  
        temp.remove(temp.size() - 1);  
    }  
}  
```

### **4.4 Sorting**  
```java
// Sort 2D array by first column  
Arrays.sort(arr, (a, b) -> a[0] - b[0]);  
```

---

## **5. Tree & Graph Algorithms**  
### **5.1 Tree Traversal**  
- **BFS (Level Order)**:  
  ```java
  Queue<TreeNode> q = new LinkedList<>();  
  q.offer(root);  
  while (!q.isEmpty()) {  
      int size = q.size();  
      for (int i = 0; i < size; i++) {  
          TreeNode node = q.poll();  
          if (node.left != null) q.offer(node.left);  
          if (node.right != null) q.offer(node.right);  
      }  
  }  
  ```  
- **DFS**:  
  ```java
  void dfs(TreeNode root) {  
      if (root == null) return;  
      dfs(root.left);  
      dfs(root.right);  
  }  
  ```

### **5.2 Graph Representation & Traversal**  
- **Adjacency List**:  
  ```java
  List<List<Integer>> graph = new ArrayList<>();  
  for (int i = 0; i < n; i++) graph.add(new ArrayList<>());  
  graph.get(u).add(v);  
  ```  
- **DFS on Graph**:  
  ```java
  void dfs(List<List<Integer>> graph, boolean[] visited, int node) {  
      visited[node] = true;  
      for (int neighbor : graph.get(node)) {  
          if (!visited[neighbor]) dfs(graph, visited, neighbor);  
      }  
  }  
  ```

---

## **6. Dynamic Programming**  
### **6.1 Top-Down (Memoization)**  
```java
int[] memo = new int[n + 1];  
int dp(int i) {  
    if (i == 0) return 1;  
    if (memo[i] != -1) return memo[i];  
    return memo[i] = dp(i - 1) + dp(i - 2);  
}  
```

### **6.2 Bottom-Up (Tabulation)**  
```java
int[] dp = new int[n + 1];  
dp[0] = 1;  
dp[1] = 1;  
for (int i = 2; i <= n; i++) {  
    dp[i] = dp[i - 1] + dp[i - 2];  
}  
```

---

## **7. Bit Manipulation**  
```java
int x = 5; // 101  
x & 1;     // Check even/odd  
x | (1 << 2); // Set 3rd bit  
Integer.bitCount(x); // Count set bits  
```

---

## **8. Essential Libraries**  
```java
import java.util.*; // Covers List, Map, Set, Queue, Stack  
import java.math.*; // For BigInteger, BigDecimal  
```

---

**Key Tips for LeetCode**:  
1. **Optimize Lookups**: Use `HashSet`/`HashMap` for O(1) operations.  
2. **Edge Cases**: Test for empty input, duplicates, and integer overflow.  
3. **Space-Time Tradeoff**: Prefer memoization in DP over brute force.  

**Patterns to Master**:  
- Two Pointers  
- Sliding Window  
- Fast & Slow Pointers  
- Union-Find  
- Trie  

--- 

This consolidated guide covers **100% of Java syntax, APIs, and DSA patterns** needed for Medium/Hard LeetCode problems. Save it as a cheat sheet! 🔥
