## 1. Two Pointers

**When to use:** Sorted arrays, palindromes, pair finding 
**Rationale:** Reduces O(n²) brute force to O(n)

```cpp
// Classic example: Two Sum in sorted array
vector<int> twoSum(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) return {left, right};
        else if (sum < target) left++;
        else right--;
    }
    return {};
}
```

---

## 2. Sliding Window

**When to use:** Subarray/substring problems with constraints 
**Rationale:** Maintains a "window" of valid elements, avoiding nested loops

```cpp
// Longest substring without repeating characters
int lengthOfLongestSubstring(string s) {
    unordered_set<char> window;
    int left = 0, maxLen = 0;
    
    for (int right = 0; right < s.length(); right++) {
        while (window.count(s[right])) {
            window.erase(s[left++]);
        }
        window.insert(s[right]);
        maxLen = max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

**Tip:** Think "expand right, contract left when invalid"

---

## 3. Fast & Slow Pointers

**When to use:** Cycle detection, finding middle elements 
**Rationale:** Nice way to detect patterns in sequences

```cpp
// Detect cycle in linked list
bool hasCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;
    }
    return false;
}
```

**Tip:** Also called "tortoise and hare" 

---

## 4. Binary Search

**When to use:** Sorted data, "search space" problems 
**Rationale:** O(log n) beats O(n) every time

```cpp
// Template for most binary search problems
int binarySearch(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

**Tip:** Watch out for integer overflow - use `left + (right - left) / 2`

---

## 5. Tree Traversal (DFS/BFS)

**When to use:** Any tree/graph problem 
**Rationale:** Systematic way to visit all nodes

```cpp
// Inorder traversal (recursive)
void inorder(TreeNode* root, vector<int>& result) {
    if (!root) return;
    inorder(root->left, result);
    result.push_back(root->val);
    inorder(root->right, result);
}

// Level order traversal (BFS)
vector<vector<int>> levelOrder(TreeNode* root) {
    if (!root) return {};
    
    vector<vector<int>> result;
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int levelSize = q.size();
        vector<int> level;
        
        for (int i = 0; i < levelSize; i++) {
            TreeNode* node = q.front();
            q.pop();
            level.push_back(node->val);
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        result.push_back(level);
    }
    return result;
}
```

**Tip:** DFS for depth/path problems, BFS for level/shortest path

---

## 6. Dynamic Programming

**When to use:** Optimisation problems with overlapping subproblems 
**Rationale:** Trade space for time by storing solutions

```cpp
// 1D DP: Climbing stairs
int climbStairs(int n) {
    if (n <= 2) return n;
    
    int prev2 = 1, prev1 = 2, current;
    for (int i = 3; i <= n; i++) {
        current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
    }
    return current;
}

// 2D DP: Longest common subsequence
int longestCommonSubsequence(string text1, string text2) {
    int m = text1.length(), n = text2.length();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
    
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1[i-1] == text2[j-1]) {
                dp[i][j] = dp[i-1][j-1] + 1;
            } else {
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }
    return dp[m][n];
}
```

**Tip:** Start with recursive solution, then add memoisation, then convert to bottom-up

---

## 7. Backtracking

**When to use:** Generate all possibilities, constraint satisfaction 
**Rationale:** Systematically explore solution space with pruning

```cpp
// Generate all permutations
void backtrack(vector<int>& nums, vector<int>& current, 
               vector<bool>& used, vector<vector<int>>& result) {
    if (current.size() == nums.size()) {
        result.push_back(current);
        return;
    }
    
    for (int i = 0; i < nums.size(); i++) {
        if (used[i]) continue;
        
        current.push_back(nums[i]);
        used[i] = true;
        backtrack(nums, current, used, result);
        current.pop_back();  // backtrack
        used[i] = false;     // backtrack
    }
}
```

**Tip:** Always remember to "undo" changes when backtracking

---
## Common Gotchas

- **Off-by-one errors** - Draw examples with small inputs
- **Integer overflow** - Use `long long` when in doubt
- **Edge cases** - Empty inputs, single elements, very large inputs
- [[Algorithmic Complexity]] - Always analyse and optimise if needed