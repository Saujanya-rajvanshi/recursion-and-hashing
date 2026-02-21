# recursion-and-hashing

# Recursion and Hashing 
- [Recursion](#RECURSION)
- [Hashing](#HASHING)

# RECURSION

## INDEX 
- [basic](#basic)
- [relevant questions](#important-questions)
- [striver questions](#striver-questions)


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

## 🔄 Types of recursion

1. **Direct recursion**
   Function calls itself directly
2. **Indirect recursion**
   Function A → Function B → Function A
3. **Tail recursion**
   Recursive call is the **last statement**
4. **Non-tail recursion**
   Work remains after recursive call

---

### important questions



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

# HASHING 

**Hashing = storing and searching data in constant time using a key.**

It uses a **hash function** to convert a key into an index of an array.

```
index = hash(key)
```

Example:

```
key = 27
hash(key) = 27 % 10 = 7
store at index 7
```


hashing can be done for 10^7 in globally and 10^6 in main 



### code for number hashing 
```cpp
#include <bits/stdc++.h>
using namespace std;
int hash[10000000] = {0};       //<----- either this ,here it can take 1e7

int main() {
    int n;
    cin >> n; 

    int arr[n];
    for(int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    // frequency array (assuming values 0–12)
    int hash[13] = {0};       //<----- or this , in here it can take 1e6

    // precompute frequency
    for(int i = 0; i < n; i++) {
        hash[arr[i]]++;
    }

    // one query input
    int x;
    cin >> x;

    // output frequency of x
    cout << hash[x];

    return 0;
}
```

### code for character hashing
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s;
    cin >> s;

    // precompute
    int hash[256] = {0};

    for(int i = 0; i < s.size(); i++) {
        hash[s[i]]++;
    }

    int q;
    cin >> q;

    while(q--) {
        char c;
        cin >> c;

        // fetch frequency of character c
        cout << hash[c] << endl;
    }

    return 0;
}
```
### as array hashing has a limit of 10^7 so for above we use stl 

### using map 
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {

    int n;
    cin >> n;

    int arr[n];
    for(int i = 0; i < n; i++) {
        cin >> arr[i];
    }

    // Pre-compute using map
    map<int, int> mpp;

    for(int i = 0; i < n; i++) {
        mpp[arr[i]]++;
    }

    // Print frequency of all elements
    cout << "Element -> Frequency" << endl;
    for(auto it : mpp) {
        cout << it.first << " -> " << it.second << endl;
    }

    int q;
    cin >> q;

    while(q--) {
        int number;
        cin >> number;

        // Fetch frequency
        cout << mpp[number] << endl;
    }

    return 0;
}
```


## how does a map data structure is created 
1. division method
2. folding method
3. mid square method
<br>
in hashing atmost 10 elements are allowed <br>
These methods are used in **hashing** (especially in hash tables like `unordered_map`, not ordered `map`).
<br>
TC = O(1) -> average case
TC = O(n) -> worst case , n = number of elements in map

### 1. Division Method

#### Formula:

```
hash(key) = key % table_size
```

#### Idea:

Take remainder after dividing by table size.

#### Example:

```
key = 47
table_size = 10
47 % 10 = 7
→ store at index 7
```

* Simple and fast
* Choose table_size as prime for better distribution

### 2. Folding Method

#### Idea:

Split key into parts, add them together.

#### Example:

```
key = 12345
Split: 12 + 34 + 5
= 51
```

Then:

```
51 % table_size
```

* Good for large keys
* Used when key has many digits

### 3. Mid-Square Method

#### Idea:

1. Square the key
2. Take middle digits

#### Example:

```
key = 44
44² = 1936
Middle digits = 93
```

Then:

```
93 % table_size
```











### Components

1. **Hash function**

   * Converts key → array index
   * Should be fast and distribute keys evenly

2. **Hash table**

   * Array where values are stored using hashed index

### Basic Operations

* Insert → O(1)
* Search → O(1)
* Delete → O(1)

(average case)

### Collision

When two keys get the same index.

Example:

```
27 % 10 = 7
37 % 10 = 7   ← collision
```

### Collision Handling Methods

1. **Separate Chaining**

   * Each index stores a list (vector/linked list)
   * Multiple values stored at same index

```
table[7] → [27, 37, 47]
```

2. **Open Addressing**

   * Find another empty index

Types:

* Linear Probing: `(h + i) % size`
* Quadratic Probing: `(h + i²) % size`
* Double Hashing: use second hash function

### Load Factor

```
load factor = number of elements / table size
```

Higher load factor → more collisions → slower

### Rehashing

When table becomes too full:

* Create bigger table
* Reinsert all elements with new hash

### Good Hash Function Properties

* Deterministic (same input → same output)
* Uniform distribution
* Fast to compute
* Minimizes collisions

### Applications of Hashing

* Searching in O(1)
* Counting frequency of elements
* Finding duplicates
* Two Sum problem
* Caching
* Password storage (with secure hashes)
* Dictionaries / Maps / Sets

### Hashing in C++ STL

1. **unordered_map** (key → value)

```cpp
unordered_map<int,int> mp;
mp[5] = 10;        // insert
cout << mp[5];     // access
```

2. **unordered_set** (only keys)

```cpp
unordered_set<int> st;
st.insert(5);
if(st.find(5) != st.end()) cout << "Found";
```

Average Time Complexity:

* Insert/Search/Delete → **O(1)**
  Worst case (many collisions) → **O(n)**

### When to use Hashing

* When order does not matter
* When fast lookup is needed
* When working with large data

### Limitations

* No ordering of elements
* Extra memory for hash table
* Worst case can be slow if many collisions

**In short:**
Hashing = fast lookup by converting keys into array positions using a hash function.
