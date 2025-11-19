# TCS NQT CODING CHEATSHEET
### Complete Reference Guide with Techniques and Data Structures

> Based on karthikreddy-7/TCS-NQT-CODING-SHEET repository
> Format: **Question** | **Technique/DS** | **Key Review Points**

---

## 📊 PROBLEMS ON ARRAYS (23 Questions)

| # | Question | Technique/Data Structure | Time | Review Points |
|---|----------|-------------------------|------|---------------|
| 1 | Find smallest number in array | **Linear Scan** | O(n) | Track min during single pass, handle empty array |
| 2 | Find largest number in array | **Linear Scan** | O(n) | Track max during single pass, initialize with first element |
| 3 | Second smallest & largest element | **Sorting / Two-pass scan** | O(n log n) / O(n) | Skip duplicates, need at least 2 distinct elements |
| 4 | Reverse a given array | **Two Pointers** | O(n) | Swap elements from both ends, in-place O(1) space |
| 5 | Count frequency of elements | **HashMap** | O(n) | Use HashMap<Integer, Integer> for freq count |
| 6 | Rearrange array increasing-decreasing | **Sorting + Reconstruction** | O(n log n) | Sort, then arrange alternately from middle |
| 7 | Calculate sum of array elements | **Linear Scan** | O(n) | Watch for integer overflow, use long if needed |
| 8 | Rotate array by K elements (Block Swap) | **Reverse Algorithm** | O(n) | Reverse(0,n) → Reverse(0,k) → Reverse(k,n), handle k>n |
| 9 | Average of all elements | **Linear Scan** | O(n) | Sum/length, handle empty array, use double for precision |
| 10 | Find median of array | **Sorting / QuickSelect** | O(n log n) / O(n) | Sort first, middle element(s), even/odd length cases |
| 11 | Remove duplicates from sorted array | **Two Pointers (Write Index)** | O(n) | In-place, maintain write pointer, return new length |
| 12 | Remove duplicates from unsorted array | **HashSet** | O(n) | Use HashSet to track seen elements, O(n) space |
| 13 | Adding element in array | **Array Copy / ArrayList** | O(n) | Arrays are fixed size, use ArrayList for dynamic |
| 14 | Find all repeating elements | **HashMap / Frequency Array** | O(n) | Count freq, filter where count > 1 |
| 15 | Find all non-repeating elements | **HashMap** | O(n) | Count freq, filter where count == 1 |
| 16 | Find all symmetric pairs | **HashMap<Integer, Integer>** | O(n) | Store (a,b), check if (b,a) exists |
| 17 | Maximum product subarray | **DP (Track max & min)** | O(n) | Track maxProd & minProd (negatives flip signs) |
| 18 | Replace element by rank | **Sorting + HashMap** | O(n log n) | Sort unique elements, assign ranks, map back |
| 19 | Sort elements by frequency | **HashMap + Custom Comparator** | O(n log n) | Count freq, sort by frequency then value |
| 20 | Rotation of array (left & right) | **Reverse Algorithm** | O(n) | Left: reverse(0,k) + reverse(k,n) + reverse(0,n) |
| 21 | Finding equilibrium index | **Prefix Sum** | O(n) | leftSum == rightSum, maintain running sums |
| 22 | Check if array is subset | **HashSet** | O(n+m) | Add arr1 to set, check all arr2 elements exist |
| 23 | Circular rotation of array | **Modulo Arithmetic** | O(1) | arr[(i + k) % n] for k rotations |

---

## 🔢 PROBLEMS ON NUMBERS (27 Questions)

| # | Question | Technique/Data Structure | Time | Review Points |
|---|----------|-------------------------|------|---------------|
| 24 | Check palindrome number | **Two Pointers / Reverse** | O(log n) | Reverse and compare, or convert to string |
| 25 | Palindromes in range | **Loop + Palindrome Check** | O(n log m) | Check each number, n=range, m=digits |
| 26 | Check prime number | **Trial Division (√n)** | O(√n) | Check divisibility up to √n, skip even numbers |
| 27 | Primes in range | **Sieve of Eratosthenes** | O(n log log n) | Optimal for range, mark multiples as composite |
| 28 | Armstrong number | **Digit Extraction** | O(log n) | Sum of (digit^numberOfDigits) == number |
| 29 | Perfect number | **Divisor Sum** | O(√n) | Sum of proper divisors == number (6, 28, 496) |
| 30 | Strong number | **Factorial Sum of Digits** | O(d) | Sum of factorial of each digit == number |
| 31 | Automorphic number | **Modulo Check** | O(1) | n² ends with n (5→25, 6→36, 76→5776) |
| 32 | Harshad number | **Digit Sum** | O(log n) | Number divisible by sum of its digits |
| 33 | Abundant number | **Divisor Sum** | O(√n) | Sum of proper divisors > number |
| 34 | Leap year | **Conditional Logic** | O(1) | (year%400==0) or (year%4==0 && year%100!=0) |
| 35 | Reverse digits | **Modulo Arithmetic** | O(log n) | reversed = reversed*10 + n%10, n/=10 |
| 36 | Max & Min digit | **Digit Extraction** | O(log n) | Track max/min while extracting digits |
| 37 | Fibonacci series | **Iterative DP / Space-Optimized** | O(n) | Use two variables (a,b) not array, O(1) space |
| 38 | Factorial | **Iterative Loop** | O(n) | result *= i, watch for overflow (use long) |
| 39 | Power of number | **Binary Exponentiation** | O(log n) | Divide and conquer: x^n = (x^(n/2))² |
| 40 | Factors of number | **Loop to √n** | O(√n) | Print i and n/i, avoid duplicate for perfect squares |
| 41 | Prime factors | **Trial Division** | O(√n) | Divide by prime factors while divisible |
| 42 | GCD of two numbers | **Euclidean Algorithm** | O(log(min(a,b))) | gcd(a,b) = gcd(b, a%b), recursive/iterative |
| 43 | LCM of two numbers | **Formula: (a*b)/gcd(a,b)** | O(log n) | Calculate GCD first, use formula |
| 44 | Sum of digits | **Modulo Loop** | O(log n) | sum += n%10, n /= 10 |
| 45 | Sum in range | **Arithmetic Series** | O(1) | sum = n*(n+1)/2, use formula not loop |
| 46 | Sum of AP series | **Formula** | O(1) | S = (n/2) * (2a + (n-1)d) |
| 47 | Sum of GP series | **Formula** | O(1) | S = a*(r^n - 1)/(r-1) if r≠1 |
| 48 | Replace 0s with 1s | **Digit Manipulation** | O(log n) | Rebuild number, replace 0→1 during extraction |
| 49 | Sum of two primes | **Prime Check + Loop** | O(n√n) | Check if n-i is prime for each prime i |
| 50 | Quadratic equation roots | **Discriminant Formula** | O(1) | D=b²-4ac, roots=(-b±√D)/2a, check D<0 |

---

## 🔄 PROBLEMS ON NUMBER SYSTEM (6 Questions)

| # | Question | Technique/Data Structure | Time | Review Points |
|---|----------|-------------------------|------|---------------|
| 51 | Binary to Decimal | **Positional Value** | O(n) | Sum of (digit * 2^position), position from right |
| 52 | Binary to Octal | **Group by 3 bits** | O(n) | Group from right, convert each group to octal |
| 53 | Decimal to Binary | **Repeated Division by 2** | O(log n) | Divide by 2, collect remainders in reverse |
| 54 | Decimal to Octal | **Repeated Division by 8** | O(log n) | Divide by 8, collect remainders in reverse |
| 55 | Octal to Binary | **Each Octal = 3 Binary** | O(n) | Convert each octal digit to 3-bit binary |
| 56 | Octal to Decimal | **Positional Value** | O(n) | Sum of (digit * 8^position) |

---

## 🔀 PROBLEMS ON SORTING (5 Questions)

| # | Question | Technique/Algorithm | Time | Review Points |
|---|----------|---------------------|------|---------------|
| 57 | Bubble Sort | **Nested Loops** | O(n²) | Compare adjacent, swap if out of order, n passes |
| 58 | Selection Sort | **Find Min + Swap** | O(n²) | Find min in unsorted, swap with first unsorted |
| 59 | Insertion Sort | **Insert in Sorted Portion** | O(n²) | Build sorted array by inserting elements one by one |
| 60 | Quick Sort | **Divide & Conquer (Pivot)** | O(n log n) avg | Choose pivot, partition, recursively sort sub-arrays |
| 61 | Merge Sort | **Divide & Conquer (Merge)** | O(n log n) | Split in half, recursively sort, merge sorted halves |

**Sorting Comparison Table:**
```
Algorithm    | Best    | Average   | Worst   | Space  | Stable | Use Case
-------------|---------|-----------|---------|--------|--------|------------------
Bubble       | O(n)    | O(n²)     | O(n²)   | O(1)   | Yes    | Small/nearly sorted
Selection    | O(n²)   | O(n²)     | O(n²)   | O(1)   | No     | Memory-constrained
Insertion    | O(n)    | O(n²)     | O(n²)   | O(1)   | Yes    | Small/nearly sorted
Quick        | O(nlogn)| O(nlogn)  | O(n²)   | O(logn)| No     | General purpose
Merge        | O(nlogn)| O(nlogn)  | O(nlogn)| O(n)   | Yes    | Linked lists/stable
```

---

## 📝 PROBLEMS ON STRING (20 Questions)

| # | Question | Technique/Data Structure | Time | Review Points |
|---|----------|-------------------------|------|---------------|
| 62 | Check palindrome string | **Two Pointers** | O(n) | Compare from both ends, ignore case/spaces |
| 63 | Count vowels, consonants, spaces | **Linear Scan + Set** | O(n) | Use vowel set for O(1) lookup |
| 64 | Remove vowels | **StringBuilder + Filter** | O(n) | Build new string without vowels |
| 65 | Remove spaces | **replaceAll() / Filter** | O(n) | str.replaceAll("\\s+", "") or filter |
| 66 | Reverse a string | **Two Pointers / StringBuilder** | O(n) | Swap from ends or use reverse() method |
| 67 | Reverse words in string | **Split + Reverse + Join** | O(n) | Split by space, reverse array, join |
| 68 | Character frequency | **HashMap<Character, Integer>** | O(n) | Count occurrences, getOrDefault(char, 0)+1 |
| 69 | Non-repeating characters | **HashMap (Freq Count)** | O(n) | Find chars with frequency == 1 |
| 70 | Check anagram | **Sorting / HashMap** | O(n log n) / O(n) | Sort both or compare char frequencies |
| 71 | Maximum occurring character | **HashMap / Frequency Array** | O(n) | Track max frequency while counting |
| 72 | Remove duplicates | **HashSet / LinkedHashSet** | O(n) | LinkedHashSet preserves order |
| 73 | Print all duplicates | **HashMap (Freq > 1)** | O(n) | Filter characters with count > 1 |
| 74 | Count common subsequence | **Dynamic Programming** | O(n*m) | 2D DP table for subsequence matching |
| 75 | Wildcard pattern matching | **DP / Recursion** | O(n*m) | '?' matches 1 char, '*' matches any sequence |
| 76 | Capitalize first/last of words | **Split + Manipulation** | O(n) | Split, modify first/last char of each word |
| 77 | Find largest word | **Split + Max Length** | O(n) | Split by space, track longest word |
| 78 | Sort characters | **toCharArray() + Sort** | O(n log n) | Convert to char array, sort, rebuild string |
| 79 | Count number of words | **Split by Space / Count Spaces** | O(n) | words = str.trim().split("\\s+").length |
| 80 | Highest repeated letters in sequence | **Run-Length Encoding** | O(n) | Track consecutive char counts |
| 81 | Next lexicographic alphabet | **ASCII Manipulation** | O(n) | (char + 1) with wrap-around for 'z' |

---

## 🚀 ADVANCED PATTERNS & TECHNIQUES

### Common Data Structures Usage:

1. **HashMap / HashSet** (Most Common in TCS NQT)
   - Frequency counting
   - Duplicate detection
   - O(1) lookup operations
   - Example: Character/element frequency, anagrams

2. **Two Pointers**
   - Array reversal
   - Palindrome check
   - In-place modifications
   - Example: Remove duplicates, rotate array

3. **Sliding Window**
   - Substring problems
   - Subarray problems
   - Example: Max sum subarray, longest substring

4. **Dynamic Programming**
   - Optimization problems
   - Subsequence problems
   - Example: Knapsack, longest common subsequence

5. **Divide & Conquer**
   - Sorting algorithms
   - Binary search variations
   - Example: Quick sort, merge sort

6. **Greedy**
   - Optimization problems
   - Activity selection
   - Example: Fractional knapsack

### Space-Time Tradeoffs:

```
Technique          | Time        | Space | When to Use
-------------------|-------------|-------|----------------------------------
HashMap            | O(n)        | O(n)  | Fast lookups, frequency counting
Two Pointers       | O(n)        | O(1)  | In-place operations, palindromes
Sorting First      | O(n log n)  | O(1)  | When order matters, duplicates
Brute Force        | O(n²)       | O(1)  | Small inputs, simple logic
Binary Search      | O(log n)    | O(1)  | Sorted array, find element
```

### Input Handling Patterns (Critical for TCS IDE):

```java
// Pattern 1: Variable length array input
Scanner sc = new Scanner(System.in);
String[] tokens = sc.nextLine().trim().split("\\s+");
int[] arr = Arrays.stream(tokens).mapToInt(Integer::parseInt).toArray();

// Pattern 2: Robust integer parsing
try {
    int n = Integer.parseInt(input);
} catch (NumberFormatException e) {
    // Handle error
}

// Pattern 3: Handle empty/null inputs
if (arr == null || arr.length == 0) return defaultValue;
```

---

## 📊 PROBLEM DIFFICULTY DISTRIBUTION

**By Category:**
- Arrays: 23 problems (30% of total)
- Numbers: 27 problems (35% of total)
- Strings: 20 problems (26% of total)
- Number System: 6 problems (8% of total)
- Sorting: 5 problems (1% of total)

**By Difficulty:**
- Easy (Basic implementation): ~40%
- Medium (Requires optimization): ~45%
- Hard (DP/Advanced DS): ~15%

**By Data Structure:**
- HashMap/HashSet: ~30% of problems
- Two Pointers: ~20% of problems
- Mathematical: ~25% of problems
- DP/Recursion: ~10% of problems
- Other: ~15% of problems

---

## 🎯 PREPARATION STRATEGY

### Week 1-2: Master Fundamentals
✅ All Array problems (1-23)
✅ Basic Number problems (24-40)
✅ String basics (62-69)

### Week 3: Intermediate Topics
✅ Advanced Number problems (41-50)
✅ All Sorting algorithms (57-61)
✅ Advanced String problems (70-81)

### Week 4: Polish & Practice
✅ Number System conversions (51-56)
✅ Solve recent TCS NQT actual questions
✅ Time yourself: 45 min per question

### Day Before Exam:
✅ Review this cheatsheet
✅ Practice input handling edge cases
✅ Revise time complexities

---

## 💡 QUICK TIPS

1. **Time Complexity Goals:**
   - Target O(n) or O(n log n) solutions
   - Avoid O(n²) unless n < 100

2. **Space Optimization:**
   - Use HashMap only when necessary
   - Prefer in-place modifications (two pointers)

3. **Edge Cases to Always Check:**
   - Empty array/string
   - Single element
   - All same elements
   - Negative numbers
   - Very large numbers (overflow)

4. **Common Mistakes:**
   - Integer overflow (use long)
   - Array index out of bounds
   - Null pointer exceptions
   - Not handling k > n in rotation

5. **Interview Favorites:**
   - Palindrome (any form)
   - Prime numbers
   - Array rotation
   - Frequency counting
   - Anagrams

---

## 📚 REFERENCES

- Repository: https://github.com/karthikreddy-7/TCS-NQT-CODING-SHEET
- Total Problems: ~81 problems across 5 categories
- Language: Java (easily adaptable to Python/C++)
- Last Updated: January 2024

---

**⭐ Star this cheatsheet and practice consistently!**

*Good luck with your TCS NQT exam! 🚀*
