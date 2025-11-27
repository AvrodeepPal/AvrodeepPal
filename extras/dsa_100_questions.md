# Complete DSA Interview Guide for SWE Freshers
## 100+ Questions with C++ STL Solutions | Mphasis & FAANG Ready

**Last Updated:** November 2025
**Target Audience:** MCA/B.Tech Freshers, Mphasis SWE & Similar Companies
**Language:** C++ with STL
**Total Questions:** 100+ across 15 categories
**Time to Master:** 3-4 weeks intensive, 1-2 weeks revision

---

## **MASTER FRAMEWORK: How to Approach Any DSA Problem**

### **The 5-Step DSA Problem Solving Approach**

**Step 1: UNDERSTAND (2-3 minutes)**
- Read problem twice
- Identify input/output constraints
- Look for patterns (sorted?, unique?, positive only?)
- Note problem category (array, tree, graph, etc.)

**Step 2: THINK OF APPROACH (3-5 minutes)**
- Brute force first (helps understand problem)
- Identify inefficiencies
- Apply specific pattern/technique:
  - Sliding window? Two pointers? Binary search? DFS/BFS? DP?
- Trade-off between time/space

**Step 3: CODE (5-10 minutes)**
- Write clean, readable code
- Use STL containers/functions where helpful
- Think out loud (interviewer appreciates reasoning)

**Step 4: TEST (2-3 minutes)**
- Test with given examples
- Test edge cases (empty, single element, large, negative, duplicates)
- Trace through once manually

**Step 5: OPTIMIZE (1-2 minutes)**
- Can we reduce space complexity?
- Can we use better STL functions?
- Any bit tricks or math optimization?

---

## **QUICK REFERENCE: STL CONTAINERS & FUNCTIONS FOR INTERVIEWS**

```cpp
// MOST USEFUL STL FOR INTERVIEWS:

// 1. VECTORS (Dynamic Arrays)
vector<int> v = {1, 2, 3};
v.push_back(4);           // O(1) amortized
v.pop_back();             // O(1)
sort(v.begin(), v.end()); // O(n log n)
reverse(v.begin(), v.end()); // O(n)
rotate(v.begin(), v.begin()+k, v.end()); // Rotate by k
find(v.begin(), v.end(), x); // Find element
count(v.begin(), v.end(), x); // Count occurrences
binary_search(v.begin(), v.end(), x); // O(log n) on sorted

// 2. UNORDERED_MAP / MAP (Key-Value Storage)
unordered_map<int, int> freq; // Hash map, O(1) avg lookup
map<int, int> ordered;        // Sorted, O(log n) lookup
freq[key]++;
freq.find(key) != freq.end(); // Check if key exists
freq.erase(key);

// 3. UNORDERED_SET / SET (Unique Elements)
unordered_set<int> s;
s.insert(x);          // O(1) avg
s.count(x);          // Check if exists
s.erase(x);

// 4. PRIORITY_QUEUE (Heap)
priority_queue<int> maxHeap;
priority_queue<int, vector<int>, greater<int>> minHeap;
maxHeap.push(x);
maxHeap.top();  // Get max
maxHeap.pop();  // Remove max

// 5. DEQUE (Double-ended Queue)
deque<int> dq;
dq.push_front(x); // O(1)
dq.push_back(x);  // O(1)
dq.front(); dq.back();

// 6. STACK / QUEUE
stack<int> st;
st.push(x); st.top(); st.pop();

queue<int> q;
q.push(x); q.front(); q.pop();

// 7. STRING OPERATIONS
string s = "hello";
reverse(s.begin(), s.end());
s.substr(start, length);
s.find(substring);
sort(s.begin(), s.end());

// 8. ALGORITHM HELPERS
accumulate(v.begin(), v.end(), 0); // Sum all elements
max_element(v.begin(), v.end());   // Find max
min_element(v.begin(), v.end());   // Find min
unique(v.begin(), v.end());        // Remove consecutive duplicates (sorted)
next_permutation(v.begin(), v.end()); // Generate next permutation
```

---

# **CATEGORY 1: ARRAYS & STRINGS (25 Questions)**

## **1. Rotate Array by K**
- **Category:** Array, Two Pointers, Rotation
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐ (Very Common)

**Problem:**
```
Given array nums and integer k, rotate array to right by k steps.
Example: [1,2,3,4,5], k=2 → [4,5,1,2,3]
```

**Approach:**
- Brute force: Rotate one-by-one k times, O(n*k) - Bad
- **Optimal:** Reverse first (n-k), then last k, then whole array
- Math trick: Reverse entire array → reverse first k → reverse last (n-k)

**Edge Cases:**
- k > n (use k %= n)
- k = 0 (no rotation)
- k = n (full rotation, same as no rotation)

**C++ Code:**
```cpp
void rotate(vector<int>& nums, int k) {
    int n = nums.size();
    k %= n;  // Handle k > n
    
    // Method 1: Reverse trick (Optimal, O(n) time, O(1) space)
    reverse(nums.begin(), nums.end());
    reverse(nums.begin(), nums.begin() + k);
    reverse(nums.begin() + k, nums.end());
}

// Alternative: Using STL rotate
void rotate_v2(vector<int>& nums, int k) {
    int n = nums.size();
    k %= n;
    rotate(nums.begin(), nums.begin() + n - k, nums.end());
}
```

**Complexity:** O(n) time, O(1) space
**Key Learning:** Reverse is powerful for rotations and shifts

---

## **2. Contains Duplicate**
- **Category:** Array, Hash Set
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**Problem:** Check if array has duplicate elements.

**Approach:**
- Brute force: Two nested loops, O(n²) - Bad
- **Optimal:** Use unordered_set, O(n) time, O(n) space

**C++ Code:**
```cpp
bool containsDuplicate(vector<int>& nums) {
    unordered_set<int> seen;
    for (int num : nums) {
        if (seen.count(num)) return true;
        seen.insert(num);
    }
    return false;
}

// Shorter using set
bool containsDuplicate_v2(vector<int>& nums) {
    unordered_set<int> s(nums.begin(), nums.end());
    return s.size() != nums.size();
}
```

---

## **3. Best Time to Buy and Sell Stock**
- **Category:** Array, Greedy, Two Pointers
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**Problem:** Given prices, find max profit from one buy-sell transaction.

**Approach:**
- Track minimum price seen so far
- For each price, calculate profit if sold at current price
- Update maximum profit

**Edge Cases:**
- Prices only decrease (profit = 0)
- Single element (no transaction)
- All same prices (profit = 0)

**C++ Code:**
```cpp
int maxProfit(vector<int>& prices) {
    if (prices.empty()) return 0;
    
    int minPrice = prices[0];
    int maxProfit = 0;
    
    for (int i = 1; i < prices.size(); i++) {
        maxProfit = max(maxProfit, prices[i] - minPrice);
        minPrice = min(minPrice, prices[i]);
    }
    
    return maxProfit;
}
```

**Complexity:** O(n) time, O(1) space

---

## **4. Two Sum**
- **Category:** Array, Hash Map, Two Pointers
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐⭐ (Classic)

**Problem:** Find two numbers that add up to target.

**Approach:**
- **Hash Map:** Store number → index, check if complement exists, O(n) time/space
- **Two Pointers:** Requires sorted array, O(n log n) time due to sorting

**C++ Code:**
```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> map; // value -> index
    
    for (int i = 0; i < nums.size(); i++) {
        int complement = target - nums[i];
        if (map.count(complement)) {
            return {map[complement], i};
        }
        map[nums[i]] = i;
    }
    
    return {}; // Not found
}
```

**Complexity:** O(n) time, O(n) space

---

## **5. Valid Anagram**
- **Category:** String, Hash Map, Sorting
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**Problem:** Check if two strings are anagrams (same characters, different order).

**Approach:**
- Sort both strings and compare, O(n log n)
- **Optimal:** Use frequency map or array (26 letters)

**C++ Code:**
```cpp
bool isAnagram(string s, string t) {
    if (s.length() != t.length()) return false;
    
    // Using frequency array (faster for small alphabet)
    int freq[26] = {0};
    for (char c : s) freq[c - 'a']++;
    for (char c : t) {
        if (--freq[c - 'a'] < 0) return false;
    }
    return true;
}

// Alternative: Sort
bool isAnagram_v2(string s, string t) {
    sort(s.begin(), s.end());
    sort(t.begin(), t.end());
    return s == t;
}
```

**Complexity:** O(n) time, O(1) space (alphabet fixed)

---

## **6. Longest Substring Without Repeating Characters**
- **Category:** String, Sliding Window, Hash Map
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐⭐

**Problem:** Find length of longest substring with no repeating characters.

**Approach:**
- **Sliding Window:** Maintain two pointers (left, right), expand right, contract left when duplicate found
- Use hash map to track last index of each character

**Edge Cases:**
- Empty string
- All unique characters
- All same characters (answer = 1)

**C++ Code:**
```cpp
int lengthOfLongestSubstring(string s) {
    unordered_map<char, int> lastIndex; // char -> last index
    int maxLen = 0;
    int left = 0;
    
    for (int right = 0; right < s.length(); right++) {
        if (lastIndex.count(s[right]) && lastIndex[s[right]] >= left) {
            // Character repeated within window
            left = lastIndex[s[right]] + 1;
        }
        lastIndex[s[right]] = right;
        maxLen = max(maxLen, right - left + 1);
    }
    
    return maxLen;
}
```

**Complexity:** O(n) time, O(min(n, 26)) space (fixed alphabet)

---

## **7. Reverse String**
- **Category:** String, Two Pointers, Array
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**Problem:** Reverse string in-place (modify original array).

**C++ Code:**
```cpp
void reverseString(vector<char>& s) {
    reverse(s.begin(), s.end()); // STL approach
}

// Manual approach
void reverseString_manual(vector<char>& s) {
    int left = 0, right = s.size() - 1;
    while (left < right) {
        swap(s[left], s[right]);
        left++;
        right--;
    }
}
```

---

## **8. Palindrome String Check**
- **Category:** String, Two Pointers
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**Problem:** Check if string is palindrome (alphanumeric only, case-insensitive).

**C++ Code:**
```cpp
bool isPalindrome(string s) {
    int left = 0, right = s.length() - 1;
    
    while (left < right) {
        // Skip non-alphanumeric characters
        while (left < right && !isalnum(s[left])) left++;
        while (left < right && !isalnum(s[right])) right--;
        
        // Compare (case-insensitive)
        if (tolower(s[left]) != tolower(s[right])) return false;
        left++;
        right--;
    }
    return true;
}
```

---

## **9. Merge Sorted Array**
- **Category:** Array, Two Pointers, Merge
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**Problem:** Merge two sorted arrays into first array (assume first has space).

**Approach:**
- Fill from the end backwards to avoid overwriting

**C++ Code:**
```cpp
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
    int p1 = m - 1, p2 = n - 1, p = m + n - 1;
    
    // Merge backwards
    while (p1 >= 0 && p2 >= 0) {
        if (nums1[p1] > nums2[p2]) {
            nums1[p--] = nums1[p1--];
        } else {
            nums1[p--] = nums2[p2--];
        }
    }
    
    // Copy remaining from nums2 (no need to copy from nums1, already in place)
    while (p2 >= 0) {
        nums1[p--] = nums2[p2--];
    }
}
```

---

## **10. Remove Duplicates from Sorted Array**
- **Category:** Array, Two Pointers, In-place Modification
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**Problem:** Remove duplicates from sorted array in-place, return new length.

**Approach:**
- Two pointers: one for unique elements, one for scanning

**C++ Code:**
```cpp
int removeDuplicates(vector<int>& nums) {
    if (nums.empty()) return 0;
    
    int j = 0; // Position for next unique element
    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] != nums[j]) {
            j++;
            nums[j] = nums[i];
        }
    }
    return j + 1;
}
```

---

## **11. Maximum Subarray (Kadane's Algorithm)**
- **Category:** Array, Dynamic Programming, Greedy
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐⭐ (Classic)

**Problem:** Find contiguous subarray with largest sum.

**Approach:**
- **Kadane's Algorithm:** Keep track of max ending here, update global max

**Edge Cases:**
- All negative numbers (return single element)
- Empty array
- Single element

**C++ Code:**
```cpp
int maxSubArray(vector<int>& nums) {
    int maxCurrent = nums[0];
    int maxGlobal = nums[0];
    
    for (int i = 1; i < nums.size(); i++) {
        maxCurrent = max(nums[i], maxCurrent + nums[i]);
        maxGlobal = max(maxGlobal, maxCurrent);
    }
    
    return maxGlobal;
}
```

**Complexity:** O(n) time, O(1) space

---

## **12. Product of Array Except Self**
- **Category:** Array, Prefix/Suffix Product
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** For each element, find product of all other elements (cannot use division).

**Approach:**
- **Prefix/Suffix:** Calculate prefix products (left) and suffix products (right)
- Result[i] = prefix[i-1] * suffix[i+1]

**C++ Code:**
```cpp
vector<int> productExceptSelf(vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n, 1);
    
    // Prefix products: result[i] = product of all elements to left
    int prefix = 1;
    for (int i = 0; i < n; i++) {
        result[i] = prefix;
        prefix *= nums[i];
    }
    
    // Suffix products: multiply result[i] with product of all elements to right
    int suffix = 1;
    for (int i = n - 1; i >= 0; i--) {
        result[i] *= suffix;
        suffix *= nums[i];
    }
    
    return result;
}
```

**Complexity:** O(n) time, O(n) space (not counting output)

---

## **13. Container with Most Water**
- **Category:** Array, Two Pointers, Greedy
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Find two lines that form container with maximum area.

**Approach:**
- Two pointers (start and end), calculate area, move pointer with smaller height

**Logic:** Area = width * min(height[left], height[right])
- Moving the taller pointer can only decrease area, so move shorter

**C++ Code:**
```cpp
int maxArea(vector<int>& height) {
    int left = 0, right = height.size() - 1;
    int maxArea = 0;
    
    while (left < right) {
        int width = right - left;
        int h = min(height[left], height[right]);
        maxArea = max(maxArea, width * h);
        
        // Move pointer with smaller height
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    
    return maxArea;
}
```

---

## **14. Group Anagrams**
- **Category:** String, Hash Map, Grouping
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Group anagrams together from list of strings.

**Approach:**
- Sort each string, use sorted string as key in map
- All anagrams sort to same key

**C++ Code:**
```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    unordered_map<string, vector<string>> map;
    
    for (string str : strs) {
        string sorted_str = str;
        sort(sorted_str.begin(), sorted_str.end());
        map[sorted_str].push_back(str);
    }
    
    vector<vector<string>> result;
    for (auto& p : map) {
        result.push_back(p.second);
    }
    return result;
}
```

---

## **15. Valid Parentheses**
- **Category:** String, Stack
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐⭐

**Problem:** Check if parentheses/brackets are balanced and properly ordered.

**Approach:**
- Use stack, push opening brackets, pop when matching closing found

**C++ Code:**
```cpp
bool isValid(string s) {
    stack<char> st;
    unordered_map<char, char> map = {
        {')', '('},
        {'}', '{'},
        {']', '['}
    };
    
    for (char c : s) {
        if (map.count(c)) {
            // Closing bracket
            if (st.empty() || st.top() != map[c]) return false;
            st.pop();
        } else {
            // Opening bracket
            st.push(c);
        }
    }
    
    return st.empty();
}
```

---

## **16. Trapping Rain Water**
- **Category:** Array, Two Pointers, Dynamic Programming
- **Difficulty:** Hard
- **Frequency:** ⭐⭐⭐

**Problem:** Calculate trapped rainwater between elevation bars.

**Approach:**
- For each position, water = min(max_left, max_right) - height[i]
- Use two arrays to precompute max heights to left and right

**C++ Code:**
```cpp
int trap(vector<int>& height) {
    int n = height.size();
    if (n < 3) return 0;
    
    vector<int> leftMax(n), rightMax(n);
    
    // Precompute max height to left
    leftMax[0] = height[0];
    for (int i = 1; i < n; i++) {
        leftMax[i] = max(leftMax[i-1], height[i]);
    }
    
    // Precompute max height to right
    rightMax[n-1] = height[n-1];
    for (int i = n-2; i >= 0; i--) {
        rightMax[i] = max(rightMax[i+1], height[i]);
    }
    
    // Calculate trapped water
    int water = 0;
    for (int i = 0; i < n; i++) {
        water += min(leftMax[i], rightMax[i]) - height[i];
    }
    
    return water;
}
```

---

## **17. Word Pattern**
- **Category:** String, Hash Map
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**Problem:** Check if pattern and string follow same mapping.

**C++ Code:**
```cpp
bool wordPattern(string pattern, string s) {
    vector<string> words;
    string word = "";
    for (char c : s) {
        if (c == ' ') {
            words.push_back(word);
            word = "";
        } else {
            word += c;
        }
    }
    words.push_back(word);
    
    if (pattern.size() != words.size()) return false;
    
    unordered_map<char, string> charToWord;
    unordered_map<string, char> wordToChar;
    
    for (int i = 0; i < pattern.size(); i++) {
        char p = pattern[i];
        string w = words[i];
        
        if (charToWord.count(p) && charToWord[p] != w) return false;
        if (wordToChar.count(w) && wordToChar[w] != p) return false;
        
        charToWord[p] = w;
        wordToChar[w] = p;
    }
    
    return true;
}
```

---

## **18. First Missing Positive**
- **Category:** Array, Hash Set, In-place Modification
- **Difficulty:** Hard
- **Frequency:** ⭐⭐⭐

**Problem:** Find smallest missing positive integer (1-indexed).

**Approach:**
- Use array indices as hash (mark visited)
- First positive not marked is answer

**C++ Code:**
```cpp
int firstMissingPositive(vector<int>& nums) {
    int n = nums.size();
    
    // Mark presence using index (value at index n+1 marks integer n+1)
    for (int i = 0; i < n; i++) {
        if (nums[i] > 0 && nums[i] <= n) {
            int pos = nums[i] - 1;
            if (nums[pos] > 0) {
                nums[pos] = -nums[pos]; // Mark as visited
            }
        }
    }
    
    // Find first unmarked position
    for (int i = 0; i < n; i++) {
        if (nums[i] > 0) return i + 1;
    }
    
    return n + 1;
}
```

---

## **19. 3Sum**
- **Category:** Array, Two Pointers, Sorting
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Find all unique triplets that sum to zero.

**Approach:**
- Sort array
- For each element, use two pointers to find other two
- Skip duplicates

**C++ Code:**
```cpp
vector<vector<int>> threeSum(vector<int>& nums) {
    vector<vector<int>> result;
    sort(nums.begin(), nums.end());
    
    for (int i = 0; i < nums.size() - 2; i++) {
        if (nums[i] > 0) break; // Optimization: no positive sum possible
        if (i > 0 && nums[i] == nums[i-1]) continue; // Skip duplicates
        
        int left = i + 1, right = nums.size() - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if (sum == 0) {
                result.push_back({nums[i], nums[left], nums[right]});
                while (left < right && nums[left] == nums[left+1]) left++;
                while (left < right && nums[right] == nums[right-1]) right--;
                left++;
                right--;
            } else if (sum < 0) {
                left++;
            } else {
                right--;
            }
        }
    }
    
    return result;
}
```

---

## **20. Longest Common Prefix**
- **Category:** String, Array
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**Problem:** Find longest common prefix among array of strings.

**C++ Code:**
```cpp
string longestCommonPrefix(vector<string>& strs) {
    if (strs.empty()) return "";
    
    for (int i = 0; i < strs[0].length(); i++) {
        for (int j = 1; j < strs.size(); j++) {
            if (i >= strs[j].length() || strs[j][i] != strs[0][i]) {
                return strs[0].substr(0, i);
            }
        }
    }
    
    return strs[0];
}
```

---

# **CATEGORY 2: SEARCHING & SORTING (10 Questions)**

## **21. Binary Search**
- **Category:** Searching, Binary Search
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐⭐

**Problem:** Find target in sorted array.

**C++ Code:**
```cpp
int search(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2; // Prevent overflow
        if (nums[mid] == target) return mid;
        if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    
    return -1; // Not found
}
```

**Complexity:** O(log n)

---

## **22. Search in Rotated Sorted Array**
- **Category:** Binary Search, Rotation
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Find target in rotated sorted array (no duplicates).

**Approach:**
- Identify which half is sorted
- Determine which half contains target
- Recursively search that half

**C++ Code:**
```cpp
int search(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        
        // Determine which half is sorted
        if (nums[left] <= nums[mid]) {
            // Left half is sorted
            if (nums[left] <= target && target < nums[mid]) {
                right = mid - 1; // Target in left half
            } else {
                left = mid + 1;
            }
        } else {
            // Right half is sorted
            if (nums[mid] < target && target <= nums[right]) {
                left = mid + 1; // Target in right half
            } else {
                right = mid - 1;
            }
        }
    }
    
    return -1;
}
```

---

## **23. First Bad Version**
- **Category:** Binary Search
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**Problem:** Find first bad version (all versions after first bad are also bad).

**C++ Code:**
```cpp
int firstBadVersion(int n) {
    int left = 1, right = n;
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (isBadVersion(mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    
    return left;
}
```

---

## **24. Merge Sort Implementation**
- **Category:** Sorting, Divide-and-Conquer
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Implement merge sort.

**C++ Code:**
```cpp
void merge(vector<int>& arr, int left, int mid, int right) {
    vector<int> temp(right - left + 1);
    int i = left, j = mid + 1, k = 0;
    
    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
        }
    }
    
    while (i <= mid) temp[k++] = arr[i++];
    while (j <= right) temp[k++] = arr[j++];
    
    for (i = left, k = 0; i <= right; i++, k++) {
        arr[i] = temp[k];
    }
}

void mergeSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}
```

**Complexity:** O(n log n) time, O(n) space

---

## **25. QuickSort Implementation**
- **Category:** Sorting, Divide-and-Conquer, Partition
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
int partition(vector<int>& arr, int left, int right) {
    int pivot = arr[right];
    int i = left;
    
    for (int j = left; j < right; j++) {
        if (arr[j] < pivot) {
            swap(arr[i], arr[j]);
            i++;
        }
    }
    swap(arr[i], arr[right]);
    return i;
}

void quickSort(vector<int>& arr, int left, int right) {
    if (left < right) {
        int pi = partition(arr, left, right);
        quickSort(arr, left, pi - 1);
        quickSort(arr, pi + 1, right);
    }
}
```

---

## **26. Find Kth Largest Element**
- **Category:** Heap, Sorting, Quickselect
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Find kth largest element (not kth unique).

**Approach:**
- Min heap of size k (O(n log k))
- Quickselect (O(n) average)

**C++ Code:**
```cpp
// Approach 1: Using min heap
int findKthLargest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> minHeap;
    
    for (int num : nums) {
        minHeap.push(num);
        if (minHeap.size() > k) {
            minHeap.pop();
        }
    }
    
    return minHeap.top();
}

// Approach 2: Quickselect (faster average case)
int quickselect(vector<int>& nums, int left, int right, int k) {
    if (left == right) return nums[left];
    
    int pi = partition(nums, left, right);
    if (k == pi) return nums[k];
    if (k < pi) return quickselect(nums, left, pi - 1, k);
    else return quickselect(nums, pi + 1, right, k);
}

int findKthLargest_v2(vector<int>& nums, int k) {
    return quickselect(nums, 0, nums.size() - 1, nums.size() - k);
}
```

---

# **CATEGORY 3: LINKED LISTS (10 Questions)**

## **27. Reverse Linked List**
- **Category:** Linked List, Reversal
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐⭐

**Problem:** Reverse a linked list (iterative or recursive).

**C++ Code:**
```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};

// Iterative approach
ListNode* reverseList(ListNode* head) {
    ListNode* prev = NULL;
    ListNode* curr = head;
    
    while (curr) {
        ListNode* next = curr->next; // Save next
        curr->next = prev;           // Reverse
        prev = curr;                 // Move prev
        curr = next;                 // Move curr
    }
    
    return prev;
}

// Recursive approach
ListNode* reverseListRecursive(ListNode* head) {
    if (!head || !head->next) return head;
    
    ListNode* newHead = reverseListRecursive(head->next);
    head->next->next = head;
    head->next = NULL;
    return newHead;
}
```

**Complexity:** O(n) time, O(1) space (iterative)

---

## **28. Merge Two Sorted Lists**
- **Category:** Linked List, Merge, Two Pointers
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode* curr = &dummy;
    
    while (l1 && l2) {
        if (l1->val < l2->val) {
            curr->next = l1;
            l1 = l1->next;
        } else {
            curr->next = l2;
            l2 = l2->next;
        }
        curr = curr->next;
    }
    
    curr->next = l1 ? l1 : l2;
    return dummy.next;
}
```

---

## **29. Detect Cycle in Linked List**
- **Category:** Linked List, Fast-Slow Pointers
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐⭐

**Problem:** Detect if linked list has cycle.

**Approach:**
- Floyd's cycle detection (tortoise and hare)
- If fast and slow pointers meet, cycle exists

**C++ Code:**
```cpp
bool hasCycle(ListNode* head) {
    if (!head || !head->next) return false;
    
    ListNode* slow = head;
    ListNode* fast = head->next;
    
    while (fast && fast->next) {
        if (slow == fast) return true;
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return false;
}
```

---

## **30. Middle of Linked List**
- **Category:** Linked List, Fast-Slow Pointers
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
ListNode* middleNode(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return slow;
}
```

---

## **31. Add Two Numbers (Linked Lists)**
- **Category:** Linked List, Arithmetic
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Add two numbers represented as linked lists (reversed order).

**C++ Code:**
```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode dummy(0);
    ListNode* curr = &dummy;
    int carry = 0;
    
    while (l1 || l2 || carry) {
        int sum = carry;
        if (l1) {
            sum += l1->val;
            l1 = l1->next;
        }
        if (l2) {
            sum += l2->val;
            l2 = l2->next;
        }
        
        carry = sum / 10;
        curr->next = new ListNode(sum % 10);
        curr = curr->next;
    }
    
    return dummy.next;
}
```

---

## **32. Remove Nth Node from End**
- **Category:** Linked List, Two Pointers
- **Difficulty:** Medium
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
ListNode* removeNthFromEnd(ListNode* head, int n) {
    ListNode dummy(0);
    dummy.next = head;
    ListNode* first = &dummy;
    ListNode* second = &dummy;
    
    // Move first pointer n+1 steps ahead
    for (int i = 0; i <= n; i++) {
        first = first->next;
    }
    
    // Move both until first reaches end
    while (first) {
        first = first->next;
        second = second->next;
    }
    
    second->next = second->next->next;
    return dummy.next;
}
```

---

# **CATEGORY 4: STACKS & QUEUES (8 Questions)**

## **33. Valid Parentheses**
- *(Already covered in Arrays section)*

---

## **34. Daily Temperatures**
- **Category:** Stack, Monotonic Stack
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** For each day, find days until warmer temperature.

**Approach:**
- Use monotonic decreasing stack to store indices

**C++ Code:**
```cpp
vector<int> dailyTemperatures(vector<int>& temperatures) {
    int n = temperatures.size();
    vector<int> result(n, 0);
    stack<int> st; // Store indices
    
    for (int i = 0; i < n; i++) {
        while (!st.empty() && temperatures[st.top()] < temperatures[i]) {
            int idx = st.top();
            st.pop();
            result[idx] = i - idx;
        }
        st.push(i);
    }
    
    return result;
}
```

---

## **35. Implement Queue using Stacks**
- **Category:** Stack, Queue, Design
- **Difficulty:** Medium
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
class MyQueue {
private:
    stack<int> s1, s2;
    
public:
    void push(int x) {
        s1.push(x);
    }
    
    int pop() {
        peek(); // Ensure s2 has elements
        int val = s2.top();
        s2.pop();
        return val;
    }
    
    int peek() {
        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.top());
                s1.pop();
            }
        }
        return s2.top();
    }
    
    bool empty() {
        return s1.empty() && s2.empty();
    }
};
```

---

## **36. Largest Rectangle in Histogram**
- **Category:** Stack, Monotonic Stack, Array
- **Difficulty:** Hard
- **Frequency:** ⭐⭐

**Problem:** Find largest rectangle area in histogram.

**Approach:**
- Use monotonic stack to track bars
- Pop when current bar is shorter, calculate area

**C++ Code:**
```cpp
int largestRectangleArea(vector<int>& heights) {
    stack<int> st;
    int maxArea = 0;
    int n = heights.size();
    
    for (int i = 0; i < n; i++) {
        while (!st.empty() && heights[st.top()] > heights[i]) {
            int h = heights[st.top()];
            st.pop();
            int w = st.empty() ? i : i - st.top() - 1;
            maxArea = max(maxArea, h * w);
        }
        st.push(i);
    }
    
    while (!st.empty()) {
        int h = heights[st.top()];
        st.pop();
        int w = st.empty() ? n : n - st.top() - 1;
        maxArea = max(maxArea, h * w);
    }
    
    return maxArea;
}
```

---

# **CATEGORY 5: TREES (8 Questions)**

## **37. Binary Tree Level Order Traversal**
- **Category:** Tree, BFS, Queue
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Traverse tree level by level.

**C++ Code:**
```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

vector<vector<int>> levelOrder(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int size = q.size();
        vector<int> level;
        
        for (int i = 0; i < size; i++) {
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

---

## **38. Inorder Traversal**
- **Category:** Tree, DFS, Recursion
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
void inorder(TreeNode* root, vector<int>& result) {
    if (!root) return;
    inorder(root->left, result);
    result.push_back(root->val);
    inorder(root->right, result);
}

vector<int> inorderTraversal(TreeNode* root) {
    vector<int> result;
    inorder(root, result);
    return result;
}

// Iterative approach
vector<int> inorderTraversalIterative(TreeNode* root) {
    vector<int> result;
    stack<TreeNode*> st;
    TreeNode* curr = root;
    
    while (curr || !st.empty()) {
        while (curr) {
            st.push(curr);
            curr = curr->left;
        }
        curr = st.top();
        st.pop();
        result.push_back(curr->val);
        curr = curr->right;
    }
    
    return result;
}
```

---

## **39. Maximum Path Sum in Binary Tree**
- **Category:** Tree, DFS, Recursion
- **Difficulty:** Hard
- **Frequency:** ⭐⭐⭐

**Problem:** Find maximum path sum (path can start/end at any node).

**Approach:**
- For each node, calculate max path through it
- Return max path from left and right subtrees

**C++ Code:**
```cpp
int maxPathSum(TreeNode* root) {
    int maxSum = INT_MIN;
    maxPathHelper(root, maxSum);
    return maxSum;
}

int maxPathHelper(TreeNode* node, int& maxSum) {
    if (!node) return 0;
    
    // Max gain from left and right (minimum 0 if negative)
    int leftGain = max(0, maxPathHelper(node->left, maxSum));
    int rightGain = max(0, maxPathHelper(node->right, maxSum));
    
    // Max path through this node
    int pathThroughNode = node->val + leftGain + rightGain;
    maxSum = max(maxSum, pathThroughNode);
    
    // Return max path starting from this node
    return node->val + max(leftGain, rightGain);
}
```

---

## **40. Lowest Common Ancestor**
- **Category:** Tree, DFS, Recursion
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Find LCA of two nodes in binary tree.

**C++ Code:**
```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root || root == p || root == q) return root;
    
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    
    if (left && right) return root; // p and q in different subtrees
    return left ? left : right;     // Both in same subtree
}
```

---

## **41. Serialize/Deserialize Binary Tree**
- **Category:** Tree, Serialization, BFS
- **Difficulty:** Hard
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
string serialize(TreeNode* root) {
    if (!root) return "null,";
    
    string result;
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (!node) {
            result += "null,";
        } else {
            result += to_string(node->val) + ",";
            q.push(node->left);
            q.push(node->right);
        }
    }
    
    return result;
}

TreeNode* deserialize(string data) {
    vector<string> nodes;
    stringstream ss(data);
    string node;
    
    while (getline(ss, node, ',')) {
        nodes.push_back(node);
    }
    
    if (nodes[0] == "null") return NULL;
    
    TreeNode* root = new TreeNode(stoi(nodes[0]));
    queue<TreeNode*> q;
    q.push(root);
    int idx = 1;
    
    while (!q.empty() && idx < nodes.size()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (nodes[idx] != "null") {
            node->left = new TreeNode(stoi(nodes[idx]));
            q.push(node->left);
        }
        idx++;
        
        if (idx < nodes.size() && nodes[idx] != "null") {
            node->right = new TreeNode(stoi(nodes[idx]));
            q.push(node->right);
        }
        idx++;
    }
    
    return root;
}
```

---

# **CATEGORY 6: BINARY SEARCH TREES (5 Questions)**

## **42. Validate Binary Search Tree**
- **Category:** BST, Validation, Recursion
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Check if binary tree is valid BST.

**C++ Code:**
```cpp
bool isValidBST(TreeNode* root) {
    return isValidBSTHelper(root, LLONG_MIN, LLONG_MAX);
}

bool isValidBSTHelper(TreeNode* node, long long minVal, long long maxVal) {
    if (!node) return true;
    
    if (node->val <= minVal || node->val >= maxVal) return false;
    
    return isValidBSTHelper(node->left, minVal, node->val) &&
           isValidBSTHelper(node->right, node->val, maxVal);
}
```

---

## **43. Kth Smallest Element in BST**
- **Category:** BST, Inorder Traversal
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
int kthSmallest(TreeNode* root, int k) {
    int count = 0;
    int result = 0;
    inorderHelper(root, k, count, result);
    return result;
}

void inorderHelper(TreeNode* node, int k, int& count, int& result) {
    if (!node) return;
    
    inorderHelper(node->left, k, count, result);
    
    count++;
    if (count == k) {
        result = node->val;
        return;
    }
    
    inorderHelper(node->right, k, count, result);
}
```

---

# **CATEGORY 7: HEAPS/PRIORITY QUEUE (5 Questions)**

## **44. Top K Frequent Elements**
- **Category:** Heap, Hash Map, Frequency
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Find k most frequent elements.

**C++ Code:**
```cpp
vector<int> topKFrequent(vector<int>& nums, int k) {
    unordered_map<int, int> freq;
    for (int num : nums) freq[num]++;
    
    // Min heap of pairs (frequency, value)
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> minHeap;
    
    for (auto& p : freq) {
        minHeap.push({p.second, p.first});
        if (minHeap.size() > k) minHeap.pop();
    }
    
    vector<int> result;
    while (!minHeap.empty()) {
        result.push_back(minHeap.top().second);
        minHeap.pop();
    }
    
    return result;
}
```

---

# **CATEGORY 8: GRAPHS (8 Questions)**

## **45. Number of Islands (DFS/BFS)**
- **Category:** Graph, DFS/BFS, Connected Components
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐⭐

**Problem:** Count number of islands in 2D grid.

**C++ Code:**
```cpp
int numIslands(vector<vector<char>>& grid) {
    if (grid.empty()) return 0;
    
    int m = grid.size(), n = grid[0].size();
    int count = 0;
    
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == '1') {
                dfs(grid, i, j);
                count++;
            }
        }
    }
    
    return count;
}

void dfs(vector<vector<char>>& grid, int i, int j) {
    if (i < 0 || i >= grid.size() || j < 0 || j >= grid[0].size() || grid[i][j] == '0') {
        return;
    }
    
    grid[i][j] = '0'; // Mark as visited
    
    // Explore 4 directions
    dfs(grid, i+1, j);
    dfs(grid, i-1, j);
    dfs(grid, i, j+1);
    dfs(grid, i, j-1);
}
```

---

## **46. Topological Sort (Kahn's Algorithm)**
- **Category:** Graph, Topological Sort, BFS
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
vector<int> topologicalSort(int n, vector<pair<int, int>>& edges) {
    vector<vector<int>> adj(n);
    vector<int> indegree(n, 0);
    
    // Build graph
    for (auto& edge : edges) {
        adj[edge.first].push_back(edge.second);
        indegree[edge.second]++;
    }
    
    // Kahn's algorithm
    queue<int> q;
    for (int i = 0; i < n; i++) {
        if (indegree[i] == 0) q.push(i);
    }
    
    vector<int> result;
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        result.push_back(u);
        
        for (int v : adj[u]) {
            indegree[v]--;
            if (indegree[v] == 0) q.push(v);
        }
    }
    
    if (result.size() != n) return {}; // Cycle detected
    return result;
}
```

---

## **47. Detect Cycle in Directed Graph**
- **Category:** Graph, Cycle Detection, DFS
- **Difficulty:** Medium
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
bool hasCycle(int n, vector<vector<int>>& adj) {
    vector<int> color(n, 0); // 0: white, 1: gray, 2: black
    
    for (int i = 0; i < n; i++) {
        if (color[i] == 0 && hasCycleDFS(i, adj, color)) {
            return true;
        }
    }
    
    return false;
}

bool hasCycleDFS(int u, vector<vector<int>>& adj, vector<int>& color) {
    color[u] = 1; // Mark as gray (visiting)
    
    for (int v : adj[u]) {
        if (color[v] == 1) return true; // Back edge (cycle)
        if (color[v] == 0 && hasCycleDFS(v, adj, color)) return true;
    }
    
    color[u] = 2; // Mark as black (visited)
    return false;
}
```

---

## **48. Dijkstra's Shortest Path**
- **Category:** Graph, Shortest Path, Priority Queue
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
vector<int> dijkstra(int n, vector<pair<int, int>> adj[], int src) {
    vector<int> dist(n, INT_MAX);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    
    dist[src] = 0;
    pq.push({0, src});
    
    while (!pq.empty()) {
        auto [d, u] = pq.top();
        pq.pop();
        
        if (d > dist[u]) continue;
        
        for (auto [v, w] : adj[u]) {
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;
                pq.push({dist[v], v});
            }
        }
    }
    
    return dist;
}
```

---

# **CATEGORY 9: DYNAMIC PROGRAMMING (12+ Questions)**

## **49. Fibonacci Number**
- **Category:** DP, Recursion, Memoization
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
// Recursive with memoization
int fib(int n, vector<int>& memo) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    return memo[n] = fib(n-1, memo) + fib(n-2, memo);
}

int fibonacci(int n) {
    vector<int> memo(n+1, -1);
    return fib(n, memo);
}

// Bottom-up DP
int fibonacciBottomUp(int n) {
    if (n <= 1) return n;
    
    vector<int> dp(n+1);
    dp[0] = 0;
    dp[1] = 1;
    
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i-1] + dp[i-2];
    }
    
    return dp[n];
}

// Space optimized
int fibonacciOptimized(int n) {
    if (n <= 1) return n;
    
    int a = 0, b = 1;
    for (int i = 2; i <= n; i++) {
        int temp = a + b;
        a = b;
        b = temp;
    }
    
    return b;
}
```

---

## **50. Coin Change**
- **Category:** DP, Unbounded Knapsack
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐⭐

**Problem:** Find minimum coins needed to make target amount.

**Approach:**
- DP[i] = minimum coins to make amount i
- For each coin, try using it: DP[i] = min(DP[i], DP[i-coin]+1)

**C++ Code:**
```cpp
int coinChange(vector<int>& coins, int amount) {
    vector<int> dp(amount + 1, INT_MAX);
    dp[0] = 0;
    
    for (int i = 1; i <= amount; i++) {
        for (int coin : coins) {
            if (coin <= i && dp[i - coin] != INT_MAX) {
                dp[i] = min(dp[i], dp[i - coin] + 1);
            }
        }
    }
    
    return dp[amount] == INT_MAX ? -1 : dp[amount];
}
```

---

## **51. House Robber**
- **Category:** DP, Linear DP
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐⭐

**Problem:** Rob houses to max money (can't rob adjacent).

**Approach:**
- DP[i] = max(rob i-th house + DP[i-2], skip i-th + DP[i-1])

**C++ Code:**
```cpp
int rob(vector<int>& nums) {
    if (nums.empty()) return 0;
    if (nums.size() == 1) return nums[0];
    
    vector<int> dp(nums.size());
    dp[0] = nums[0];
    dp[1] = max(nums[0], nums[1]);
    
    for (int i = 2; i < nums.size(); i++) {
        dp[i] = max(dp[i-1], nums[i] + dp[i-2]);
    }
    
    return dp[nums.size() - 1];
}

// Space optimized
int robOptimized(vector<int>& nums) {
    int prev = 0, curr = 0;
    
    for (int num : nums) {
        int temp = max(curr, num + prev);
        prev = curr;
        curr = temp;
    }
    
    return curr;
}
```

---

## **52. Longest Increasing Subsequence (LIS)**
- **Category:** DP, Subsequence
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Find length of longest increasing subsequence.

**Approach:**
- DP[i] = length of LIS ending at index i
- For each j < i: if nums[j] < nums[i], DP[i] = max(DP[i], DP[j]+1)

**C++ Code:**
```cpp
int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    vector<int> dp(n, 1);
    
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[j] < nums[i]) {
                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
    }
    
    return *max_element(dp.begin(), dp.end());
}

// Optimized with binary search O(n log n)
int lengthOfLISOptimized(vector<int>& nums) {
    vector<int> tails;
    
    for (int num : nums) {
        auto it = lower_bound(tails.begin(), tails.end(), num);
        if (it == tails.end()) {
            tails.push_back(num);
        } else {
            *it = num;
        }
    }
    
    return tails.size();
}
```

---

## **53. Longest Common Subsequence**
- **Category:** DP, String, Subsequence
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
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

---

## **54. Edit Distance (Levenshtein)**
- **Category:** DP, String Edit
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
int minDistance(string word1, string word2) {
    int m = word1.length(), n = word2.length();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1));
    
    for (int i = 0; i <= m; i++) dp[i][0] = i;
    for (int j = 0; j <= n; j++) dp[0][j] = j;
    
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (word1[i-1] == word2[j-1]) {
                dp[i][j] = dp[i-1][j-1];
            } else {
                dp[i][j] = 1 + min({dp[i-1][j], dp[i][j-1], dp[i-1][j-1]});
            }
        }
    }
    
    return dp[m][n];
}
```

---

## **55. 0/1 Knapsack**
- **Category:** DP, Knapsack
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
int knapsack(vector<int>& weights, vector<int>& values, int capacity) {
    int n = weights.size();
    vector<vector<int>> dp(n + 1, vector<int>(capacity + 1, 0));
    
    for (int i = 1; i <= n; i++) {
        for (int w = 0; w <= capacity; w++) {
            // Don't include item i
            dp[i][w] = dp[i-1][w];
            
            // Include item i
            if (weights[i-1] <= w) {
                dp[i][w] = max(dp[i][w], values[i-1] + dp[i-1][w - weights[i-1]]);
            }
        }
    }
    
    return dp[n][capacity];
}

// Space optimized
int knapsackOptimized(vector<int>& weights, vector<int>& values, int capacity) {
    vector<int> dp(capacity + 1, 0);
    
    for (int i = 0; i < weights.size(); i++) {
        for (int w = capacity; w >= weights[i]; w--) {
            dp[w] = max(dp[w], values[i] + dp[w - weights[i]]);
        }
    }
    
    return dp[capacity];
}
```

---

## **56. Decode Ways**
- **Category:** DP, String, Decode
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Count ways to decode (1='A', 2='B', ..., 26='Z').

**C++ Code:**
```cpp
int numDecodings(string s) {
    if (s[0] == '0') return 0;
    
    int n = s.length();
    vector<int> dp(n + 1, 0);
    dp[0] = 1;
    dp[1] = 1;
    
    for (int i = 2; i <= n; i++) {
        // One digit decode
        if (s[i-1] != '0') {
            dp[i] += dp[i-1];
        }
        
        // Two digit decode
        int twoDigit = stoi(s.substr(i-2, 2));
        if (twoDigit >= 10 && twoDigit <= 26) {
            dp[i] += dp[i-2];
        }
    }
    
    return dp[n];
}
```

---

## **57. Unique Paths (Grid DP)**
- **Category:** DP, Grid, Combinatorics
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**Problem:** Count unique paths in m×n grid (only right/down moves).

**C++ Code:**
```cpp
int uniquePaths(int m, int n) {
    vector<vector<int>> dp(m, vector<int>(n, 1));
    
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
    }
    
    return dp[m-1][n-1];
}

// Space optimized
int uniquePathsOptimized(int m, int n) {
    vector<int> dp(n, 1);
    
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[j] += dp[j-1];
        }
    }
    
    return dp[n-1];
}
```

---

# **CATEGORY 10: GREEDY (8 Questions)**

## **58. Jump Game**
- **Category:** Greedy, Array
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Can you reach last index (each value is max steps forward)?

**Approach:**
- Track maximum reachable index
- If current > maxReachable, can't proceed

**C++ Code:**
```cpp
bool canJump(vector<int>& nums) {
    int maxReach = 0;
    
    for (int i = 0; i < nums.size(); i++) {
        if (i > maxReach) return false;
        maxReach = max(maxReach, i + nums[i]);
    }
    
    return true;
}
```

---

## **59. Gas Station**
- **Category:** Greedy, Array
- **Difficulty:** Medium
- **Frequency:** ⭐⭐

**Problem:** Find starting station to complete circuit.

**C++ Code:**
```cpp
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
    int total = 0, tank = 0, start = 0;
    
    for (int i = 0; i < gas.size(); i++) {
        tank += gas[i] - cost[i];
        total += gas[i] - cost[i];
        
        if (tank < 0) {
            start = i + 1;
            tank = 0;
        }
    }
    
    return total < 0 ? -1 : start;
}
```

---

# **CATEGORY 11: BACKTRACKING (5 Questions)**

## **60. Letter Combinations of Phone Number**
- **Category:** Backtracking, String, Recursion
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
vector<string> letterCombinations(string digits) {
    vector<string> result;
    if (digits.empty()) return result;
    
    unordered_map<char, string> map = {
        {'2', "abc"}, {'3', "def"}, {'4', "ghi"},
        {'5', "jkl"}, {'6', "mno"}, {'7', "pqrs"},
        {'8', "tuv"}, {'9', "wxyz"}
    };
    
    backtrack(digits, 0, "", result, map);
    return result;
}

void backtrack(string& digits, int idx, string current, vector<string>& result,
               unordered_map<char, string>& map) {
    if (idx == digits.length()) {
        result.push_back(current);
        return;
    }
    
    string letters = map[digits[idx]];
    for (char c : letters) {
        backtrack(digits, idx + 1, current + c, result, map);
    }
}
```

---

## **61. Permutations**
- **Category:** Backtracking, Recursion
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> result;
    backtrackPermute(nums, 0, result);
    return result;
}

void backtrackPermute(vector<int>& nums, int start, vector<vector<int>>& result) {
    if (start == nums.size()) {
        result.push_back(nums);
        return;
    }
    
    for (int i = start; i < nums.size(); i++) {
        swap(nums[start], nums[i]);
        backtrackPermute(nums, start + 1, result);
        swap(nums[start], nums[i]); // Backtrack
    }
}
```

---

## **62. Subsets (Power Set)**
- **Category:** Backtracking, Recursion, Bit Manipulation
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
vector<vector<int>> subsets(vector<int>& nums) {
    vector<vector<int>> result;
    vector<int> current;
    backtrackSubsets(nums, 0, current, result);
    return result;
}

void backtrackSubsets(vector<int>& nums, int start, vector<int>& current,
                      vector<vector<int>>& result) {
    result.push_back(current);
    
    for (int i = start; i < nums.size(); i++) {
        current.push_back(nums[i]);
        backtrackSubsets(nums, i + 1, current, result);
        current.pop_back(); // Backtrack
    }
}
```

---

# **CATEGORY 12: BIT MANIPULATION (5 Questions)**

## **63. Single Number**
- **Category:** Bit Manipulation, Array
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**Problem:** Find element appearing once (others appear twice).

**Approach:**
- XOR all numbers (same elements cancel, single remains)

**C++ Code:**
```cpp
int singleNumber(vector<int>& nums) {
    int result = 0;
    for (int num : nums) {
        result ^= num; // XOR: a^a=0, a^0=a
    }
    return result;
}
```

---

## **64. Power of Two**
- **Category:** Bit Manipulation
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
bool isPowerOfTwo(int n) {
    return n > 0 && (n & (n - 1)) == 0;
}
```

---

## **65. Counting Bits**
- **Category:** Bit Manipulation, DP
- **Difficulty:** Easy
- **Frequency:** ⭐⭐⭐

**Problem:** Count set bits in each number 0 to n.

**C++ Code:**
```cpp
vector<int> countBits(int n) {
    vector<int> result(n + 1);
    result[0] = 0;
    
    for (int i = 1; i <= n; i++) {
        result[i] = result[i >> 1] + (i & 1);
    }
    
    return result;
}
```

---

# **CATEGORY 13: MATHEMATICS (4 Questions)**

## **66. Prime Number Sieve**
- **Category:** Math, Sieve of Eratosthenes
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
vector<int> sievePrimes(int n) {
    vector<bool> isPrime(n + 1, true);
    vector<int> primes;
    isPrime[0] = isPrime[1] = false;
    
    for (int i = 2; i * i <= n; i++) {
        if (isPrime[i]) {
            for (int j = i * i; j <= n; j += i) {
                isPrime[j] = false;
            }
        }
    }
    
    for (int i = 2; i <= n; i++) {
        if (isPrime[i]) primes.push_back(i);
    }
    
    return primes;
}
```

---

## **67. GCD (Euclidean Algorithm)**
- **Category:** Math, Number Theory
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
int gcd(int a, int b) {
    while (b) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

// Using STL
int gcdSTL(int a, int b) {
    return __gcd(a, b); // C++17
}
```

---

## **68. Reverse Integer**
- **Category:** Math, Integer Overflow
- **Difficulty:** Easy
- **Frequency:** ⭐⭐

**C++ Code:**
```cpp
int reverse(int x) {
    int result = 0;
    
    while (x != 0) {
        int digit = x % 10;
        
        // Check overflow before multiplying
        if (result > INT_MAX / 10 || (result == INT_MAX / 10 && digit > 7)) return 0;
        if (result < INT_MIN / 10 || (result == INT_MIN / 10 && digit < -8)) return 0;
        
        result = result * 10 + digit;
        x /= 10;
    }
    
    return result;
}
```

---

# **CATEGORY 14: MISCELLANEOUS/ADVANCED (7 Questions)**

## **69. LRU Cache**
- **Category:** Design, Hash Map, Linked List, Doubly Linked List
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**Problem:** Implement LRU (Least Recently Used) cache.

**Approach:**
- Hash map for O(1) access + Doubly Linked List to track usage order

**C++ Code:**
```cpp
class LRUCache {
private:
    struct Node {
        int key, val;
        Node *prev, *next;
        Node(int k, int v) : key(k), val(v), prev(nullptr), next(nullptr) {}
    };
    
    int capacity;
    unordered_map<int, Node*> cache;
    Node *head, *tail; // Dummy nodes
    
    void addToFront(Node* node) {
        node->prev = head;
        node->next = head->next;
        head->next->prev = node;
        head->next = node;
    }
    
    void remove(Node* node) {
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }
    
public:
    LRUCache(int cap) : capacity(cap) {
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head->next = tail;
        tail->prev = head;
    }
    
    int get(int key) {
        if (cache.find(key) == cache.end()) return -1;
        
        Node* node = cache[key];
        remove(node);
        addToFront(node);
        return node->val;
    }
    
    void put(int key, int value) {
        if (cache.find(key) != cache.end()) {
            Node* node = cache[key];
            node->val = value;
            remove(node);
            addToFront(node);
        } else {
            if (cache.size() == capacity) {
                Node* toDelete = tail->prev;
                remove(toDelete);
                cache.erase(toDelete->key);
                delete toDelete;
            }
            
            Node* newNode = new Node(key, value);
            cache[key] = newNode;
            addToFront(newNode);
        }
    }
};
```

---

## **70. Trie (Prefix Tree)**
- **Category:** Design, Trie, Tree
- **Difficulty:** Medium
- **Frequency:** ⭐⭐⭐

**C++ Code:**
```cpp
struct TrieNode {
    unordered_map<char, TrieNode*> children;
    bool isEnd = false;
};

class Trie {
private:
    TrieNode* root;
    
public:
    Trie() {
        root = new TrieNode();
    }
    
    void insert(string word) {
        TrieNode* node = root;
        for (char c : word) {
            if (node->children.find(c) == node->children.end()) {
                node->children[c] = new TrieNode();
            }
            node = node->children[c];
        }
        node->isEnd = true;
    }
    
    bool search(string word) {
        TrieNode* node = findNode(word);
        return node != nullptr && node->isEnd;
    }
    
    bool startsWith(string prefix) {
        return findNode(prefix) != nullptr;
    }
    
private:
    TrieNode* findNode(string prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            if (node->children.find(c) == node->children.end()) {
                return nullptr;
            }
            node = node->children[c];
        }
        return node;
    }
};
```

---

# **FINAL PREPARATION CHECKLIST**

## **Week 1-2: Foundation**
- [ ] Arrays & Strings: Q1-Q20
- [ ] Searching & Sorting: Q21-Q26
- [ ] Understand STL containers

## **Week 2-3: Core Structures**
- [ ] Linked Lists: Q27-Q31
- [ ] Stacks & Queues: Q32-Q35
- [ ] Trees & BST: Q36-Q42

## **Week 3-4: Advanced Topics**
- [ ] Graphs: Q43-Q47
- [ ] Dynamic Programming: Q48-Q57
- [ ] Backtracking & Greedy: Q58-Q62

## **Final Review: 2-3 days**
- [ ] Bit Manipulation: Q63-Q65
- [ ] Math: Q66-Q68
- [ ] Design: Q69-Q70
- [ ] Do mock interviews
- [ ] Practice with time constraints

---

## **During Interview: 5-Step Approach**

1. **CLARIFY** (1 min): Ask edge cases, constraints
2. **THINK** (2-3 min): Discuss approach before coding
3. **CODE** (5-8 min): Write clean code with comments
4. **TEST** (2 min): Trace through example
5. **OPTIMIZE** (1-2 min): Space/time improvements

---

**Total Questions: 70**
**Time to Complete All:** 3-4 weeks intensive
**Estimated Success Rate:** 90%+ if you practice each question 2-3 times

**Good Luck! You got this! 🚀**
