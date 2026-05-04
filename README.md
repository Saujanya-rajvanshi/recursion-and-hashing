# Recursion and Hashing 
- [Recursion](#RECURSION)
- [Hashing](#HASHING)

# RECURSION

## INDEX 
- [basic](#basic)
- [relevant questions](#important-questions)
- [types](#types)
- [striver questions](#striver-questions)
- [Types of Overflow](#Types-of-Overflow)
- [leetcode](#leetcode)

##### basic
## Definition

**Recursion** is a technique where a function **calls itself** to solve a problem by breaking it into **smaller subproblems** until a **base case** is reached.


## 🧩 Key components
1. **Base case** → stops recursion
2. **Recursive case** → function calls itself
3. **Smaller input** → moves toward base case

* Without a base case → **infinite recursion** 


## 🔧 General form
```cpp
return_type function(parameters) {
    if (base_condition)
        return value;
    return function(smaller_input);
}
```

##### types
## 🔄 Types of recursion

1. **Direct recursion**
   Function calls itself directly
2. **Indirect recursion**
   Function A → Function B → Function A
3. **Tail recursion**
   Recursive call is the **last statement**
4. **Non-tail recursion**
   Work remains after recursive call


### 1. Direct Recursion

```cpp
void print(int n) {
    if(n == 0) return;
    cout << n << " ";
    print(n - 1);
}
```

#### Call:

```cpp
print(3);
```

#### Output:

```
3 2 1
```

Function directly calls itself

### 2. Indirect Recursion

```cpp
void funB(int n);

void funA(int n) {
    if(n <= 0) return;
    cout << n << " ";
    funB(n - 1);
}

void funB(int n) {
    if(n <= 0) return;
    cout << n << " ";
    funA(n - 1);
}
```

#### Call:

```cpp
funA(3);
```

#### Output:

```
3 2 1
```

A → B → A → B …

### 3. Tail Recursion

```cpp
void print(int n) {
    if(n == 0) return;
    cout << n << " ";
    print(n - 1);
}
```

#### Call:

```cpp
print(3);
```

#### Output:

```
3 2 1
```

Work happens **before recursive call** <br>
Nothing after call

### 4. Non-Tail Recursion

```cpp
void print(int n) {
    if(n == 0) return;
    print(n - 1);
    cout << n << " ";
}
```

#### Call:

```cpp
print(3);
```

#### Output:

```
1 2 3
```

Work happens **after recursive call** <br>

| Type     | Output Pattern      |
| -------- | ------------------- |
| Tail     | 3 2 1 (top → down)  |
| Non-tail | 1 2 3 (bottom → up) |




---


## Types of Overflow 

### 1️. Integer Overflow

👉 Value exceeds range of `int`

```cpp
int x = 1e9;
int y = 1e9;
int z = x * y;   // ❌ overflow
```

✅ Fix:

```cpp
long long z = 1LL * x * y;
```

### 2️. Signed Overflow

👉 Goes beyond `INT_MAX` or below `INT_MIN`

```cpp
int x = INT_MAX;
x = x + 1;   // ❌ overflow
```

✅ Fix:

* Use `long long`
* Check before operation

### 3️. Unsigned Overflow

👉 Wraps around (no error)

```cpp
unsigned int x = 0;
x = x - 1;   // → very large number
```

✅ Fix:

* Avoid unsigned unless needed

### 4️. Floating Overflow

👉 Value too large for float/double

```cpp
double x = 1e308 * 1e10;  // ❌ inf
```

✅ Fix:

* Use `long double`
* Scale values

### 5️. Stack Overflow

👉 Too much recursion

```cpp
void f() { f(); }  // ❌ infinite recursion
```

✅ Fix:

* Add base case
* Use iteration

### Common DSA Fixes

#### Multiplication

```cpp
long long mid = low + (high - low) / 2;  // safe
```

#### Division Trick

```cpp
if(a > b / c) → safer than a * c > b
```

### Use Long Long Everywhere

👉 Especially:

* Binary search
* Prefix sum
* Math problems




---


### striver questions 
- [print endless number one](#print-endless--number-one)
- [print number upto some point](print-number-upto-some-point)
- [print name times](#print-name-times)
- [sum of first n numbers](#sum-of-first-n-numbers)
- [reverse an array](#reverse-an-array)
- [check palindrom](#check-palindrom)
- [fibonaci series](#fibonaci-series)



###### print endless number one
```cpp
#include<bits/stdc++.h>
using namespace std;

void print() {
cout << 1 << endl;
print();
}

int main() {
#ifndef ONLINE_JUDGE
freopen("input.txt", "r", stdin);
freopen("output.txt", "w", stdout);
#endif

print();

return 0;
}
```
###### print number upto some point
```cpp
#include<bits/stdc++.h>
using namespace std;
int cnt = 0;
void print() {
if(cnt == 3) return;
cout << cnt << endl;
cnt++;
print();
}


int main() {
#ifndef ONLINE_JUDGE
freopen("input.txt", "r", stdin);
freopen("output.txt", "w", stdout);
#endif

print();

return 0;
}
```
###### print name times 
```cpp
#include <bits/stdc++.h>
using namespace std;

void f(int i, int n) {
    if (i > n)   // base condition
        return;

    cout << "Saujanya" << endl;   // print your name
    f(i + 1, n);                  // recursive call
}

int main() {
    int n;
    cin >> n;

    f(1, n);
    return 0;
}
```

###### sum of first n numbers
```cpp
\\paramaterised way
#include <bits/stdc++.h>
using namespace std;

void f(int i, int sum) {
    if (i < 1) {           // base condition
        cout << sum;      // print final sum
        return;
    }

    f(i - 1, sum + i);     // recursive call
}

int main() {
    int n;
    cin >> n;              // example: n = 3

    f(n, 0);               // start with sum = 0
    return 0;
}
```
```cpp
\\functional way
#include <bits/stdc++.h>
using namespace std;

int f(int n) {
    if (n == 0)           // base condition
        return 0;

    return n + f(n - 1);  // functional recursion
}

int main() {
    int n;
    cin >> n;             // example: 3

    cout << f(n);
    return 0;
}
```

###### reverse an array
```cpp
#include <bits/stdc++.h>
using namespace std;

void f(int l, int r, vector<int> &a) {
    if (l >= r)      // base condition
        return;

    swap(a[l], a[r]);    // swap left and right

    f(l + 1, r - 1, a);  // recursive call
}

int main() {
    int n;
    cin >> n;

    vector<int> a(n);
    for (int i = 0; i < n; i++)
        cin >> a[i];

    f(0, n - 1, a);      // call function to reverse

    for (int i = 0; i < n; i++)
        cout << a[i] << " ";

    return 0;
}
```
###### check palindrom
```cpp
#include <bits/stdc++.h>
using namespace std;

bool f(int i, string &s) {
    int n = s.size();

    if (i >= n / 2)      // base condition
        return true;

    if (s[i] != s[n - i - 1])
        return false;

    return f(i + 1, s);  // recursive call
}

int main() {
    string s;
    cin >> s;

    if (f(0, s))
        cout << "Palindrome";
    else
        cout << "Not Palindrome";

    return 0;
}
```
###### fibonaci series
```cpp
#include <bits/stdc++.h>
using namespace std;

int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}

int main() {
    int n;
    cin >> n;   // number of terms

    for (int i = 0; i < n; i++)
        cout << fib(i) << " ";

    return 0;
}
```


## leetcode 

### 0. RECURSION BASICS

- [509. Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)
- [70. Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)
- [50. Pow(x, n)](https://leetcode.com/problems/powx-n/)

## 🧠 pattern

```text
base case
recursive call
call stack understanding
```

### 1. RECURSION ON ARRAYS / STRINGS

* [344. Reverse String](https://leetcode.com/problems/reverse-string/description/)
* [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)
* [1910. Remove All Occurrences of a Substring](https://leetcode.com/problems/remove-all-occurrences-of-a-substring/)

## 🧠 Pattern

```text
process one element → recurse re
```

## 2. BACKTRACKING (MOST IMPORTANT)

👉 This is **core recursion skill**

## 🧠 Pattern

```text
choose → explore → unchoose
```




## ✅ Subtopic A: Subsets

* [78. Subsets](https://leetcode.com/problems/subsets/)
* [90. Subsets II](https://leetcode.com/problems/subsets-ii/)

---

## ✅ Subtopic B: Combinations

* [39. Combinations]
* [40. Combination Sum]
* [Combination Sum II]

---

## ✅ Subtopic C: Permutations

* Permutations
* Permutations II

---

## ✅ Subtopic D: Strings

* Letter Combinations of a Phone Number
* Generate Parentheses

---

# 🔹 3. RECURSION WITH CONDITIONS (PRUNING)

## 🧠 Pattern

```text
stop early if invalid
```

## ✅ Questions

* Palindrome Partitioning
* Restore IP Addresses

---

# 🔹 4. GRID / MATRIX RECURSION

## 🧠 Pattern

```text
move in directions (DFS)
```

## ✅ Questions

* Flood Fill
* Number of Islands
* Word Search

---

# 🔹 5. TREE RECURSION (VERY IMPORTANT)

## 🧠 Pattern

```text
solve left + solve right
```

## ✅ Questions

* Maximum Depth of Binary Tree
* Same Tree
* Path Sum

---

# 🔹 6. HARDER BACKTRACKING (ADVANCED)

## 🧠 Pattern

```text
multiple constraints + pruning
```

## ✅ Questions

* N-Queens
* Sudoku Solver

---

# 🔥 MASTER PATTERN SUMMARY

| Pattern         | Core Idea             |
| --------------- | --------------------- |
| Basic recursion | function calls itself |
| Subsets         | include / exclude     |
| Permutations    | fix position          |
| Combinations    | choose elements       |
| Backtracking    | undo choices          |
| DFS             | explore directions    |
| Tree recursion  | left + right          |

---

# 🔥 MUST KNOW TEMPLATES

---

## 1. Subset Template

```cpp
void solve(int i, vector<int>& nums, vector<int>& temp) {
    if(i == nums.size()) {
        ans.push_back(temp);
        return;
    }

    // include
    temp.push_back(nums[i]);
    solve(i+1, nums, temp);

    // exclude
    temp.pop_back();
    solve(i+1, nums, temp);
}
```

---

## 2. Backtracking Template

```cpp
void solve(...) {
    if(base case) {
        ans.push_back(...);
        return;
    }

    for(choice) {
        make choice;
        solve(...);
        undo choice;
    }
}
```

---

# 🔥 How many questions you REALLY need?

👉 If you do:

```text
15–20 questions (properly)
```

👉 You can solve:

```text
90% recursion problems
```

---

# 🎯 Final Strategy

1. Start with subsets → easiest
2. Then permutations
3. Then combinations
4. Then backtracking problems
5. Then trees

---

# 🚀 Important Advice

👉 Don’t just solve — **understand pattern**

Ask:

```text
Is it include/exclude?
Is it permutation?
Is it DFS?
```

---

# 💬 Question for you

👉 Do you want me to:

1. Teach you **recursion from zero (step-by-step)**
2. Or start directly with **Subsets (first important pattern)**

Just tell me 👍



































# HASHING 

**Hashing = storing and retrieving data using key–value pairs in constant time (O(1))**

* Key → unique identifier
* Value → data stored

Example:

```id="d1"
{2 → 4, 1 → 3}
```

(2 appears 4 times, 1 appears 3 times) <br><br>


#### Why Hashing?

To **avoid nested loops**

* Without hashing: O(n²) 100s 
* With hashing: O(n)

Core idea:
**Trade space for time**

#### Hash Table Concept

Internally:

```id="d4"
Key → Hash Function → Index → Store Value
```

Example:

```id="d5"
2 → hash → index 5
1 → hash → index 3
```
```cpp
#include<bits/stdc++.h>
using namespace std;

int main() {
    int n;
    cin >> n;
    int arr[n];
    for(int i = 0;i<n; i++) {
        cin >> arr[i];
    }

    // precompute
    int hash[13] = {0};
    for(int i = 0;i<n; i++) {
        hash [arr[i]] += 1;
    }

    int q;
    cin >> q;
    while(q--) {
        int number;
        cin >> number;
        // fetch
        cout << hash [number] << endl;
   }

return 0;
```
## Data Structures Used

### (a) unordered_map (MOST IMPORTANT)

```cpp id="d6"
unordered_map<int, int> mpp;
```

* only individual data type can be key
* O(1) average
* Not sorted

### (b) map

```cpp id="d7"
map<int, int> mpp;
```

* any data type can be key
* O(log n)
* Sorted

### (c) unordered_set

```cpp id="d8"
unordered_set<int> st;
```

* Stores only keys
* No duplicates

### (d) set

```cpp id="d9"
set<int> st;
```

* Sorted + unique

## Basic Operations

### Insert / Update

```cpp id="d10"
mpp[x] = 1;
mpp[x]++;
```

### Access

```cpp id="d11"
mpp[x]
```

### Check existence

```cpp id="d12"
if(mpp.find(x) != mpp.end())
```

### Delete

```cpp id="d13"
mpp.erase(x);
```

## Traversal

```cpp id="d14"
for(auto it : mpp){
    cout << it.first << " " << it.second;
}
```

* `it.first` → key
* `it.second` → value

## Types of Hashing Patterns

### Frequency Counting

Most common

```cpp id="d15"
unordered_map<int,int> mpp;

for(int i = 0; i < n; i++){
    mpp[arr[i]]++;
}
```

Used in:

* Majority element
* Count elements
* Anagrams

### Existence Checking

```cpp id="d16"
if(mpp.find(x) != mpp.end())
```

Used in:

* Duplicate detection
* Lookup problems

### Pair / Target Problems

```cpp id="d17"
if(mpp.find(target - x) != mpp.end())
```

Used in:

* Two Sum
* Pair sum

### Prefix Sum + Hashing 

```cpp id="d18"
sum += arr[i];

if(mpp.find(sum - k) != mpp.end()){
    // subarray exists
}
```

Used in:

* Subarray sum = K
* Longest subarray

### Set-based Hashing

```cpp id="d19"
unordered_set<int> st;
```

Used in:

* Unique elements
* Longest consecutive sequence

## Important Behavior

### Auto Initialization

```cpp id="d20"
mpp[x]++;
```

Means:

```id="d21"
if x not present → value = 0
then increment → becomes 1
```

### Difference: find vs []

```cpp id="d22"
mpp[x]        // inserts if not present
mpp.find(x)   // does NOT insert
```

## 9. map vs unordered_map

| Feature | map      | unordered_map |
| ------- | -------- | ------------- |
| Time    | O(log n) | O(1)          |
| Order   | Sorted   | Not sorted    |
| Use     | Rare     | Most used     |

## Time Complexity

| Operation | Complexity |
| --------- | ---------- |
| Insert    | O(1)       |
| Access    | O(1)       |
| Find      | O(1)       |
| Traverse  | O(n)       |

## Advantages

* Fast lookup
* Reduces time complexity
* Simple implementation

## Disadvantages

* Extra space
* Collisions possible
* unordered_map worst case O(n)

## Common Mistakes

* Using `map` instead of `unordered_map`
* Using `[]` when you should use `find()`
* Wrong order in Two Sum
* Forgetting edge cases

## Standard Templates (MUST REMEMBER)

### Frequency

```cpp id="d23"
unordered_map<int,int> mpp;

for(int i = 0; i < n; i++){
    mpp[arr[i]]++;
}
```

### Two Sum

```cpp id="d24"
unordered_map<int,int> mpp;

for(int i = 0; i < n; i++){
    int rem = target - arr[i];

    if(mpp.find(rem) != mpp.end()){
        return {mpp[rem], i};
    }

    mpp[arr[i]] = i;
}
```

### Prefix Sum

```cpp id="d25"
unordered_map<int,int> mpp;
mpp[0] = 1;

int sum = 0;

for(int i = 0; i < n; i++){
    sum += arr[i];

    if(mpp.find(sum - k) != mpp.end()){
        count += mpp[sum - k];
    }

    mpp[sum]++;
}
```





## 1. IF you need **frequency / counting**

Use **Frequency Pattern**

### Use:

```cpp
unordered_map<int,int> mpp;
mpp[x]++;
```

### Applies when:

* Count elements
* Most frequent / majority
* Duplicates

## 2. IF you need **check element exists or not**

Use **Lookup / Set Pattern**

### Use:

```cpp
unordered_set<int> st;
```

or

```cpp
if(mpp.find(x) != mpp.end())
```

### Applies when:

* Duplicate check
* Unique elements
* Fast search

## 3. IF you need **pair with target (sum/diff)**

Use **Pair / Target Pattern**

### Use:

```cpp
if(mpp.find(target - x) != mpp.end())
```

### Applies when:

* Two Sum
* Pair sum = K
* Pair difference

## 4. IF you see **subarray + sum = K**

Use **Prefix Sum + Hashing**

### Use:

```cpp
sum += arr[i];

if(mpp.find(sum - k) != mpp.end())
```

### Applies when:

* Subarray sum = K
* Count subarrays
* Longest subarray

## 5. IF you need **only unique elements**

Use **Set Pattern**

### Use:

```cpp
unordered_set<int> st;
```

### Applies when:

* Remove duplicates
* Distinct elements
* Sequence problems

## 6. IF you need **index (position)**

Use **Index Mapping Pattern**

### Use:

```cpp
mpp[x] = i;
```

### Applies when:

* Return indices
* First/last occurrence
* Two Sum (optimal)

## SUPER SHORT MEMORY 

```text
frequency → mpp[x]++
exists → set / find
pair → target - x
subarray → prefix sum
unique → set
index → mpp[x] = i
```


