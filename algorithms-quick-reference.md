# Data structures and Algorithms

### Arrays:

1. **Two Pointers:**
   - **Problem:** Remove Duplicates from Sorted Array
     ```java
     int removeDuplicates(int[] nums) {
         int i = 0;
         for (int j = 1; j < nums.length; j++) {
             if (nums[i] != nums[j]) {
                 i++;
                 nums[i] = nums[j];
             }
         }
         return i + 1;
     }
     ```

2. **Sliding Window:**
   - **Problem:** Maximum Subarray Sum
     ```java
     int maxSubArray(int[] nums) {
         int maxSum = nums[0], currentSum = nums[0];
         for (int i = 1; i < nums.length; i++) {
             currentSum = Math.max(nums[i], currentSum + nums[i]);
             maxSum = Math.max(maxSum, currentSum);
         }
         return maxSum;
     }
     ```

### Strings:

1. **Reverse String:**
   - **Problem:** Reverse String
     ```java
     void reverseString(char[] s) {
         int i = 0, j = s.length - 1;
         while (i < j) {
             char temp = s[i];
             s[i++] = s[j];
             s[j--] = temp;
         }
     }
     ```

2. **Anagrams:**
   - **Problem:** Valid Anagram
     ```java
     boolean isAnagram(String s, String t) {
         char[] sChars = s.toCharArray();
         char[] tChars = t.toCharArray();
         Arrays.sort(sChars);
         Arrays.sort(tChars);
         return Arrays.equals(sChars, tChars);
     }
     ```

### Linked Lists:

1. **Fast and Slow Pointers:**
   - **Problem:** Detect Cycle in a Linked List
     ```java
     boolean hasCycle(ListNode head) {
         ListNode slow = head, fast = head;
         while (fast != null && fast.next != null) {
             slow = slow.next;
             fast = fast.next.next;
             if (slow == fast) {
                 return true;
             }
         }
         return false;
     }
     ```

2. **Reverse Linked List:**
   - **Problem:** Reverse Linked List
     ```java
     ListNode reverseList(ListNode head) {
         ListNode prev = null, current = head;
         while (current != null) {
             ListNode nextNode = current.next;
             current.next = prev;
             prev = current;
             current = nextNode;
         }
         return prev;
     }
     ```

### Trees:

1. **Depth-First Search (DFS):**
   - **Problem:** Binary Tree Inorder Traversal
     ```java
     List<Integer> inorderTraversal(TreeNode root) {
         List<Integer> result = new ArrayList<>();
         inorderTraversalRecursive(root, result);
         return result;
     }

     void inorderTraversalRecursive(TreeNode node, List<Integer> result) {
         if (node != null) {
             inorderTraversalRecursive(node.left, result);
             result.add(node.val);
             inorderTraversalRecursive(node.right, result);
         }
     }
     ```

2. **Depth-First Search (DFS)):**
   - **Problem:** Find Kth smallest elements from the tree
     ```java
     public Integer kthSmallest(int k) {
        ArrayList<Integer> result = new ArrayList<>();
        
        class Traverse {
            Traverse(Node currentNode) {
                if(currentNode.left != null) {
                    new Traverse(currentNode.left);
                }
                 if (currentNode != null) result.add(currentNode.value);
                
                if (currentNode.right != null) {
                    new Traverse(currentNode.right);
                }
                
            }
        }
        new Traverse(root);
        
        if(k <= 0 || k > result.size()) {
            return null;
        } else {
            return result.get(k-1);
        }
     }
     ```
     
 4. **Breadth-First Search (BFS):**
   - **Problem:** Level Order Traversal
     ```java
     List<List<Integer>> levelOrder(TreeNode root) {
         List<List<Integer>> result = new ArrayList<>();
         if (root == null) return result;
         Queue<TreeNode> queue = new LinkedList<>();
         queue.add(root);
         while (!queue.isEmpty()) {
             int levelSize = queue.size();
             List<Integer> currentLevel = new ArrayList<>();
             for (int i = 0; i < levelSize; i++) {
                 TreeNode node = queue.poll();
                 currentLevel.add(node.val);
                 if (node.left != null) queue.add(node.left);
                 if (node.right != null) queue.add(node.right);
             }
             result.add(currentLevel);
         }
         return result;
     }
     ```

### Sorting and Searching:

1. **Binary Search:**
   - **Problem:** Binary Search
     ```java
     int binarySearch(int[] nums, int target) {
         int left = 0, right = nums.length - 1;
         while (left <= right) {
             int mid = left + (right - left) / 2;
             if (nums[mid] == target) {
                 return mid;
             } else if (nums[mid] < target) {
                 left = mid + 1;
             } else {
                 right = mid - 1;
             }
         }
         return -1;
     }
     ```

2. **Merge Sort:**
   - **Problem:** Merge Sort
     ```java
     void mergeSort(int[] arr, int left, int right) {
         if (left < right) {
             int mid = left + (right - left) / 2;
             mergeSort(arr, left, mid);


             mergeSort(arr, mid + 1, right);
             merge(arr, left, mid, right);
         }
     }

     void merge(int[] arr, int left, int mid, int right) {
         int n1 = mid - left + 1;
         int n2 = right - mid;
         int[] leftArr = new int[n1];
         int[] rightArr = new int[n2];
         System.arraycopy(arr, left, leftArr, 0, n1);
         System.arraycopy(arr, mid + 1, rightArr, 0, n2);
         int i = 0, j = 0, k = left;
         while (i < n1 && j < n2) {
             if (leftArr[i] <= rightArr[j]) {
                 arr[k++] = leftArr[i++];
             } else {
                 arr[k++] = rightArr[j++];
             }
         }
         while (i < n1) {
             arr[k++] = leftArr[i++];
         }
         while (j < n2) {
             arr[k++] = rightArr[j++];
         }
     }
     ```

### Dynamic Programming:

1. **Fibonacci Series:**
   - **Problem:** Fibonacci Number
     ```java
     int fibonacci(int n) {
         if (n <= 1) return n;
         int[] dp = new int[n + 1];
         dp[0] = 0;
         dp[1] = 1;
         for (int i = 2; i <= n; i++) {
             dp[i] = dp[i - 1] + dp[i - 2];
         }
         return dp[n];
     }
     ```

2. **Longest Common Subsequence:**
   - **Problem:** Longest Common Subsequence
     ```java
     int longestCommonSubsequence(String text1, String text2) {
         int m = text1.length(), n = text2.length();
         int[][] dp = new int[m + 1][n + 1];
         for (int i = 1; i <= m; i++) {
             for (int j = 1; j <= n; j++) {
                 if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                     dp[i][j] = dp[i - 1][j - 1] + 1;
                 } else {
                     dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                 }
             }
         }
         return dp[m][n];
     }
     ```

### Graphs:

1. **Depth-First Search (DFS):**
   - **Problem:** Depth-First Search
     ```java
     void dfs(Graph graph, int start, boolean[] visited) {
         visited[start] = true;
         System.out.print(start + " ");
         for (int neighbor : graph.adjList.get(start)) {
             if (!visited[neighbor]) {
                 dfs(graph, neighbor, visited);
             }
         }
     }
     ```

2. **Breadth-First Search (BFS):**
   - **Problem:** Breadth-First Search
     ```java
     void bfs(Graph graph, int start) {
         boolean[] visited = new boolean[graph.vertices];
         Queue<Integer> queue = new LinkedList<>();
         visited[start] = true;
         queue.add(start);
         while (!queue.isEmpty()) {
             int current = queue.poll();
             System.out.print(current + " ");
             for (int neighbor : graph.adjList.get(current)) {
                 if (!visited[neighbor]) {
                     visited[neighbor] = true;
                     queue.add(neighbor);
                 }
             }
         }
     }
     ```

### Miscellaneous:

1. **Hashing:**
   - **Problem:** Two Sum
     ```java
     int[] twoSum(int[] nums, int target) {
         Map<Integer, Integer> map = new HashMap<>();
         for (int i = 0; i < nums.length; i++) {
             int complement = target - nums[i];
             if (map.containsKey(complement)) {
                 return new int[]{map.get(complement), i};
             }
             map.put(nums[i], i);
         }
         throw new IllegalArgumentException("No two sum solution");
     }
     ```

2. **Greedy Algorithms:**
   - **Problem:** Jump Game
     ```java
     boolean canJump(int[] nums) {
         int maxReach = 0;
         for (int i = 0; i < nums.length; i++) {
             if (i > maxReach) {
                 return false;
             }
             maxReach = Math.max(maxReach, i + nums[i]);
         }
         return true;
     }
     ```


### Backtracking:
All backtracking problems are composed by these three steps: choose, explore, unchoose.


1. **Backtracking:**
   - **Problem:** All sub sets
        ```java
        class Solution {
            public List<List<Integer>> subsets(int[] nums) {
            List<List<Integer>> list = new ArrayList<>();
            // If the array is duplicate, sort the array so that we can remove duplicates
            // Arrays.sort(nums)
            // Start with 0 index
            backtrack(0, list, new ArrayList<>(), nums);
            return list;
            }

            // Required Parameters
            // 1. Start
            // 2. Final result
            // 3. Temp result
            // 4. Input array
            public void backtrack(int start, List<List<Integer>> result, List<Integer> temp, int[] nums) {
                result.add(new ArrayList<>(temp));
                for(int i=start; i<nums.length; i++) {
                    temp.add(nums[i]);
                    backtrack(i+1, result, temp, nums);
                    temp.remove(temp.size() - 1);
                }
            }
        }
        ```

