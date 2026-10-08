# HCLTech Coding Assessment - Detailed Java & Python Solutions

This document contains detailed solutions for all 15 problems from the HCLTech Coding Assessment Practice Set.

For every problem, the following format is used:

- Problem Statement
- Input Format
- Output Format
- Constraints
- Examples
- Explanation
- Approach
- Java Solution
- Python Solution
- Time and Space Complexity

The solutions are written in an easy, exam-friendly style while following the required constraints.

---

# Problem 1: Longest Substring with At Most K Distinct Characters

**Topic:** Strings, Sliding Window  
**Difficulty:** Medium

## Problem Statement

A log-analysis service receives a stream of event codes, each represented by a lowercase letter. The analytics team wants to find the longest continuous segment of the stream that contains at most `K` distinct event codes.

Given the string `S` and the integer `K`, print the length of the longest substring of `S` that contains at most `K` distinct characters.

## Input Format

- The first line contains the string `S`.
- The second line contains the integer `K`.

## Output Format

Print a single integer representing the length of the longest valid substring.

## Constraints

- `1 ≤ |S| ≤ 10^5`
- `S` consists of lowercase English letters.
- `0 ≤ K ≤ 26`

## Example 1

### Input

```text
eceba
2
```

### Output

```text
3
```

### Explanation

The substring `ece` contains only 2 distinct characters: `e` and `c`.

Its length is `3`, which is the maximum possible.

## Example 2

### Input

```text
aabbcc
1
```

### Output

```text
2
```

### Explanation

The valid substrings are `aa`, `bb`, and `cc`.

Each contains only one distinct character, so the answer is `2`.

---

## Approach

Use the **Sliding Window** technique.

1. Keep two pointers, `left` and `right`.
2. Expand the window using `right`.
3. Store the frequency of each character in a HashMap/dictionary.
4. If the number of distinct characters becomes greater than `K`, move `left` forward.
5. Keep track of the maximum window length.

**Time Complexity:** O(n)  
**Space Complexity:** O(k), at most 26 characters

## Iteration / Dry Run

For the input `eceba`, `K = 2`:

| Right | Character | Window | Distinct | Best |
|---:|:---:|:---|---:|---:|
| 0 | e | `e` | 1 | 1 |
| 1 | c | `ec` | 2 | 2 |
| 2 | e | `ece` | 2 | 3 |
| 3 | b | `eceb` → remove `e` → `ceb` | 2 | 3 |
| 4 | a | `ceba` → remove `c` → `eba` | 3 → 2 | 3 |

**Final Answer:** `3`

The longest valid substring is `ece`.

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String s = sc.nextLine();
        int k = sc.nextInt();

        HashMap<Character, Integer> count = new HashMap<>();

        int left = 0;
        int best = 0;

        for (int right = 0; right < s.length(); right++) {

            char ch = s.charAt(right);

            count.put(ch, count.getOrDefault(ch, 0) + 1);

            while (count.size() > k) {

                char leftChar = s.charAt(left);

                count.put(leftChar, count.get(leftChar) - 1);

                if (count.get(leftChar) == 0) {
                    count.remove(leftChar);
                }

                left++;
            }

            best = Math.max(best, right - left + 1);
        }

        System.out.println(best);
    }
}
```

## Python Solution

```python
s = input()
k = int(input())

count = {}

left = 0
best = 0

for right in range(len(s)):

    ch = s[right]

    count[ch] = count.get(ch, 0) + 1

    while len(count) > k:

        left_ch = s[left]

        count[left_ch] -= 1

        if count[left_ch] == 0:
            del count[left_ch]

        left += 1

    best = max(best, right - left + 1)

print(best)
```

---

# Problem 2: Minimum Platforms Required

**Topic:** Greedy, Sorting, Two Pointers  
**Difficulty:** Medium

## Problem Statement

A railway station receives `N` trains in a day. The arrival and departure time of every train is given in 24-hour `HHMM` format.

A platform is occupied from the arrival time up to and including the departure time of a train.

Therefore, a train arriving at the exact minute another train departs needs a separate platform.

Find the minimum number of platforms required so that no train has to wait.

## Input Format

- The first line contains `N`.
- The second line contains `N` integers representing arrival times.
- The third line contains `N` integers representing departure times.
- The `i-th` departure belongs to the `i-th` arrival.

## Output Format

Print the minimum number of platforms required.

## Constraints

- `1 ≤ N ≤ 10^5`
- `0000 ≤ time ≤ 2359`
- `arrival[i] ≤ departure[i]`

## Example 1

### Input

```text
6
900 940 950 1100 1500 1800
910 1200 1120 1130 1900 2000
```

### Output

```text
3
```

### Explanation

Between `1100` and `1120`, the trains arriving at `940`, `950`, and `1100` are all at the station.

Therefore, 3 platforms are required.

## Example 2

### Input

```text
3
900 1000 1100
950 1050 1150
```

### Output

```text
1
```

### Explanation

No two trains overlap, so only one platform is required.

---

## Approach

Sort the arrival times and departure times separately.

Use two pointers:

- If the next train arrives before or exactly when the next train departs, another platform is required.
- Otherwise, a train has departed and a platform becomes free.

The maximum number of simultaneously occupied platforms is the answer.

**Time Complexity:** O(n log n)  
**Space Complexity:** O(n)

## Iteration / Dry Run

For the input:

`Arrival = [900, 940, 950, 1100, 1500, 1800]`

`Departure = [910, 1120, 1130, 1200, 1900, 2000]`

After sorting, compare the next arrival with the next departure.

| Step | Arrival | Departure | Action | Platforms | Maximum |
|---:|---:|---:|:---|---:|---:|
| 1 | 900 | 910 | Arrival | 1 | 1 |
| 2 | 940 | 910 | Departure | 0 | 1 |
| 3 | 940 | 1120 | Arrival | 1 | 1 |
| 4 | 950 | 1120 | Arrival | 2 | 2 |
| 5 | 1100 | 1120 | Arrival | 3 | 3 |
| 6 | 1500 | 1120 | Departure | 2 | 3 |
| 7 | 1500 | 1130 | Departure | 1 | 3 |
| 8 | 1500 | 1200 | Departure | 0 | 3 |
| 9 | 1500 | 1900 | Arrival | 1 | 3 |
| 10 | 1800 | 1900 | Arrival | 2 | 3 |

**Final Answer:** `3`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] arrival = new int[n];
        int[] departure = new int[n];

        for (int i = 0; i < n; i++) {
            arrival[i] = sc.nextInt();
        }

        for (int i = 0; i < n; i++) {
            departure[i] = sc.nextInt();
        }

        Arrays.sort(arrival);
        Arrays.sort(departure);

        int i = 0;
        int j = 0;

        int current = 0;
        int best = 0;

        while (i < n) {

            if (arrival[i] <= departure[j]) {
                current++;
                best = Math.max(best, current);
                i++;
            } else {
                current--;
                j++;
            }
        }

        System.out.println(best);
    }
}
```

## Python Solution

```python
n = int(input())

arrival = list(map(int, input().split()))
departure = list(map(int, input().split()))

arrival.sort()
departure.sort()

i = 0
j = 0

current = 0
best = 0

while i < n:

    if arrival[i] <= departure[j]:
        current += 1
        best = max(best, current)
        i += 1
    else:
        current -= 1
        j += 1

print(best)
```

---

# Problem 3: Maximum Product Subarray

**Topic:** Arrays, Dynamic Programming  
**Difficulty:** Medium

## Problem Statement

Given an array of `N` integers that may contain positive numbers, negative numbers and zeros, find the contiguous subarray containing at least one element that has the largest product.

Print that product.

## Input Format

- The first line contains `N`.
- The second line contains `N` space-separated integers.

## Output Format

Print the maximum product of any contiguous subarray.

## Constraints

- `1 ≤ N ≤ 10^5`
- `-10 ≤ A[i] ≤ 10`

## Example 1

### Input

```text
4
2 3 -2 4
```

### Output

```text
6
```

### Explanation

The subarray `[2, 3]` has product:

`2 × 3 = 6`

So the answer is `6`.

## Example 2

### Input

```text
3
-2 3 -4
```

### Output

```text
24
```

### Explanation

The whole array has product:

`(-2) × 3 × (-4) = 24`

## Example 3

### Input

```text
3
-2 0 -1
```

### Output

```text
0
```

### Explanation

The best possible subarray is `[0]`, whose product is `0`.

---

## Approach

A negative number can change the smallest product into the largest product.

Therefore, maintain:

- `maxProduct` = maximum product ending at the current position
- `minProduct` = minimum product ending at the current position

When the current number is negative, swap these two values.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

## Iteration / Dry Run

For the input:

`[2, 3, -2, 4]`

Track the maximum and minimum product ending at each position.

| Element | Max Product | Min Product | Best |
|---:|---:|---:|---:|
| 2 | 2 | 2 | 2 |
| 3 | 6 | 3 | 6 |
| -2 | -6 | -12 | 6 |
| 4 | 4 | -48 | 6 |

**Final Answer:** `6`

The subarray `[2, 3]` gives the maximum product.

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] a = new int[n];

        for (int i = 0; i < n; i++) {
            a[i] = sc.nextInt();
        }

        int maxProduct = a[0];
        int minProduct = a[0];
        int best = a[0];

        for (int i = 1; i < n; i++) {

            if (a[i] < 0) {
                int temp = maxProduct;
                maxProduct = minProduct;
                minProduct = temp;
            }

            maxProduct = Math.max(a[i], maxProduct * a[i]);
            minProduct = Math.min(a[i], minProduct * a[i]);

            best = Math.max(best, maxProduct);
        }

        System.out.println(best);
    }
}
```

## Python Solution

```python
n = int(input())
a = list(map(int, input().split()))

max_product = a[0]
min_product = a[0]
best = a[0]

for x in a[1:]:

    if x < 0:
        max_product, min_product = min_product, max_product

    max_product = max(x, max_product * x)
    min_product = min(x, min_product * x)

    best = max(best, max_product)

print(best)
```

---

# Problem 4: Trapping Rain Water

**Topic:** Arrays, Two Pointers  
**Difficulty:** Hard

## Problem Statement

`N` buildings stand in a row, and the `i-th` building has height `H[i]` with unit width.

After heavy rain, water is trapped in the gaps between the buildings.

Compute the total units of water that can be trapped.

## Input Format

- The first line contains `N`.
- The second line contains `N` non-negative integers representing the heights.

## Output Format

Print the total units of trapped water.

## Constraints

- `1 ≤ N ≤ 10^5`
- `0 ≤ H[i] ≤ 10^5`

## Example 1

### Input

```text
12
0 1 0 2 1 0 1 3 2 1 2 1
```

### Output

```text
6
```

### Explanation

Water collects in the dips between the taller buildings.

The total trapped water is `6`.

## Example 2

### Input

```text
6
4 2 0 3 2 5
```

### Output

```text
9
```

### Explanation

The water trapped above each bar is:

`0 + 2 + 4 + 1 + 2 + 0 = 9`

---

## Approach

Use two pointers, `left` and `right`.

The amount of water above a building is limited by the smaller of the tallest buildings on its left and right.

Therefore:

1. If `H[left] < H[right]`, process the left side.
2. Otherwise, process the right side.
3. Maintain `leftMax` and `rightMax`.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

## Iteration / Dry Run

For the input:

`[0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`

The two pointers move inward while maintaining the highest wall seen on each side.

| Step | Left | Right | Left Max | Right Max | Water Added | Total |
|---:|---:|---:|---:|---:|---:|---:|
| 1 | 0 | 11 | 0 | 1 | 0 | 0 |
| 2 | 1 | 11 | 1 | 1 | 0 | 0 |
| 3 | 2 | 11 | 1 | 1 | 1 | 1 |
| 4 | 3 | 11 | 2 | 1 | 0 | 1 |
| 5 | 3 | 10 | 2 | 2 | 1 | 2 |
| 6 | 3 | 9 | 2 | 2 | 1 | 3 |
| 7 | 3 | 8 | 2 | 2 | 0 | 3 |
| 8 | 4 | 8 | 2 | 2 | 1 | 4 |
| 9 | 5 | 8 | 2 | 2 | 2 | 6 |

The remaining movements add no more water.

**Final Answer:** `6`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] h = new int[n];

        for (int i = 0; i < n; i++) {
            h[i] = sc.nextInt();
        }

        int left = 0;
        int right = n - 1;

        int leftMax = 0;
        int rightMax = 0;

        int water = 0;

        while (left < right) {

            if (h[left] < h[right]) {

                leftMax = Math.max(leftMax, h[left]);

                water += leftMax - h[left];

                left++;

            } else {

                rightMax = Math.max(rightMax, h[right]);

                water += rightMax - h[right];

                right--;
            }
        }

        System.out.println(water);
    }
}
```

## Python Solution

```python
n = int(input())
h = list(map(int, input().split()))

left = 0
right = n - 1

left_max = 0
right_max = 0

water = 0

while left < right:

    if h[left] < h[right]:

        left_max = max(left_max, h[left])

        water += left_max - h[left]

        left += 1

    else:

        right_max = max(right_max, h[right])

        water += right_max - h[right]

        right -= 1

print(water)
```

---

# Problem 5: Next Lexicographic Permutation

**Topic:** Arrays, Permutations  
**Difficulty:** Medium

## Problem Statement

Given an arrangement of `N` integers, rearrange it into the next lexicographically greater permutation.

If no greater permutation exists, meaning the array is in descending order, rearrange it into the lowest possible order, which is ascending order.

The rearrangement must be done in place using only constant extra memory.

## Input Format

- The first line contains `N`.
- The second line contains `N` space-separated integers.

## Output Format

Print the next permutation as space-separated integers.

## Constraints

- `1 ≤ N ≤ 10^5`
- `0 ≤ A[i] ≤ 100`

## Example 1

### Input

```text
3
1 2 3
```

### Output

```text
1 3 2
```

### Explanation

The next arrangement after `1 2 3` is `1 3 2`.

## Example 2

### Input

```text
3
3 2 1
```

### Output

```text
1 2 3
```

### Explanation

`3 2 1` is already the largest possible arrangement, so the answer wraps around to the smallest arrangement.

## Example 3

### Input

```text
3
1 1 5
```

### Output

```text
1 5 1
```

### Explanation

Duplicates are allowed. The next lexicographically greater arrangement is `1 5 1`.

---

## Approach

There are three main steps:

1. Find the rightmost index `i` such that `A[i] < A[i + 1]`.
2. Find the rightmost element greater than `A[i]` and swap them.
3. Reverse the suffix after index `i`.

If no such `i` exists, the array is in descending order, so simply reverse the complete array.

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

## Iteration / Dry Run

For the input:

`[1, 2, 3]`

### Step 1: Find the pivot

Start from the right:

- `2 < 3`, so pivot = index `1`
- Pivot value = `2`

### Step 2: Find the next larger value

From the right, `3 > 2`.

Swap `2` and `3`:

`[1, 3, 2]`

### Step 3: Reverse the suffix

The suffix contains only `2`, so no change is needed.

**Final Answer:** `1 3 2`

## Java Solution

```java
import java.util.*;

public class Main {

    static void reverse(int[] a, int left, int right) {

        while (left < right) {

            int temp = a[left];
            a[left] = a[right];
            a[right] = temp;

            left++;
            right--;
        }
    }

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] a = new int[n];

        for (int i = 0; i < n; i++) {
            a[i] = sc.nextInt();
        }

        int i = n - 2;

        while (i >= 0 && a[i] >= a[i + 1]) {
            i--;
        }

        if (i >= 0) {

            int j = n - 1;

            while (a[j] <= a[i]) {
                j--;
            }

            int temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }

        reverse(a, i + 1, n - 1);

        for (int x : a) {
            System.out.print(x + " ");
        }
    }
}
```

## Python Solution

```python
n = int(input())
a = list(map(int, input().split()))

i = n - 2

while i >= 0 and a[i] >= a[i + 1]:
    i -= 1

if i >= 0:

    j = n - 1

    while a[j] <= a[i]:
        j -= 1

    a[i], a[j] = a[j], a[i]

a[i + 1:] = reversed(a[i + 1:])

print(*a)
```

---

# Problem 6: Count Subarrays with Sum Equal to K

**Topic:** Hashing, Prefix Sum  
**Difficulty:** Medium

## Problem Statement

A finance module records daily net transactions, each of which can be positive or negative.

Given `N` transaction values and a target `K`, count how many contiguous subarrays have a sum exactly equal to `K`.

## Input Format

- The first line contains two integers `N` and `K`.
- The second line contains `N` space-separated integers.

## Output Format

Print the number of subarrays whose sum equals `K`.

## Constraints

- `1 ≤ N ≤ 2 × 10^5`
- `-1000 ≤ A[i] ≤ 1000`
- `-10^7 ≤ K ≤ 10^7`

## Example 1

### Input

```text
3 2
1 1 1
```

### Output

```text
2
```

### Explanation

The valid subarrays are:

- `[1, 1]` at positions `(1, 2)`
- `[1, 1]` at positions `(2, 3)`

Therefore, the answer is `2`.

## Example 2

### Input

```text
8 7
3 4 7 2 -3 1 4 2
```

### Output

```text
4
```

### Explanation

The valid subarrays are:

- `[3, 4]`
- `[7]`
- `[7, 2, -3, 1]`
- `[1, 4, 2]`

Therefore, the answer is `4`.

---

## Approach

Use **prefix sum + HashMap**.

Suppose the current prefix sum is `P`.

We need an earlier prefix sum equal to:

`P - K`

If such a prefix exists, the elements between that prefix and the current position have sum `K`.

Store the frequency of every prefix sum.

A sliding window cannot be reliably used because the array may contain negative values.

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

## Iteration / Dry Run

For the input:

`A = [1, 1, 1]`, `K = 2`

Initially:

`seen = {0: 1}`

| Step | Value | Prefix Sum | Prefix - K | Matching Prefixes | Count |
|---:|---:|---:|---:|---:|---:|
| 1 | 1 | 1 | -1 | 0 | 0 |
| 2 | 1 | 2 | 0 | 1 | 1 |
| 3 | 1 | 3 | 1 | 1 | 2 |

The two valid subarrays are:

- `[1, 1]` at positions 1–2
- `[1, 1]` at positions 2–3

**Final Answer:** `2`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int k = sc.nextInt();

        HashMap<Integer, Integer> seen = new HashMap<>();

        seen.put(0, 1);

        int prefix = 0;
        int count = 0;

        for (int i = 0; i < n; i++) {

            int x = sc.nextInt();

            prefix += x;

            count += seen.getOrDefault(prefix - k, 0);

            seen.put(prefix, seen.getOrDefault(prefix, 0) + 1);
        }

        System.out.println(count);
    }
}
```

## Python Solution

```python
n, k = map(int, input().split())

a = list(map(int, input().split()))

seen = {0: 1}

prefix = 0
count = 0

for x in a:

    prefix += x

    count += seen.get(prefix - k, 0)

    seen[prefix] = seen.get(prefix, 0) + 1

print(count)
```

---

# Problem 7: Longest Increasing Subsequence

**Topic:** Dynamic Programming, Binary Search  
**Difficulty:** Hard

## Problem Statement

Given an array of `N` integers, find the length of the longest strictly increasing subsequence.

A subsequence is formed by deleting zero or more elements without changing the order of the remaining elements.

The expected solution runs in `O(N log N)`.

## Input Format

- The first line contains `N`.
- The second line contains `N` space-separated integers.

## Output Format

Print the length of the longest strictly increasing subsequence.

## Constraints

- `1 ≤ N ≤ 10^5`
- `-10^9 ≤ A[i] ≤ 10^9`

## Example 1

### Input

```text
8
10 9 2 5 3 7 101 18
```

### Output

```text
4
```

### Explanation

One longest increasing subsequence is:

`2, 3, 7, 101`

Its length is `4`.

## Example 2

### Input

```text
6
0 1 0 3 2 3
```

### Output

```text
4
```

### Explanation

One longest increasing subsequence is:

`0, 1, 2, 3`

---

## Approach

Use the **patience sorting** technique.

Maintain an array called `tails`.

`tails[i]` represents the smallest possible ending value of an increasing subsequence of length `i + 1`.

For every element:

1. Use binary search to find its position.
2. Replace the value at that position.
3. If the value is larger than all existing values, add it to the end.

The length of `tails` is the answer.

**Time Complexity:** O(n log n)  
**Space Complexity:** O(n)

## Iteration / Dry Run

For the input:

`[10, 9, 2, 5, 3, 7, 101, 18]`

Maintain the `tails` array.

| Element | Position Found | tails |
|---:|---:|:---|
| 10 | 0 | `[10]` |
| 9 | 0 | `[9]` |
| 2 | 0 | `[2]` |
| 5 | 1 | `[2, 5]` |
| 3 | 1 | `[2, 3]` |
| 7 | 2 | `[2, 3, 7]` |
| 101 | 3 | `[2, 3, 7, 101]` |
| 18 | 3 | `[2, 3, 7, 18]` |

The length of `tails` is `4`.

**Final Answer:** `4`

One LIS is `2, 3, 7, 101`.

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] tails = new int[n];

        int size = 0;

        for (int i = 0; i < n; i++) {

            int x = sc.nextInt();

            int left = 0;
            int right = size;

            while (left < right) {

                int mid = (left + right) / 2;

                if (tails[mid] < x) {
                    left = mid + 1;
                } else {
                    right = mid;
                }
            }

            tails[left] = x;

            if (left == size) {
                size++;
            }
        }

        System.out.println(size);
    }
}
```

## Python Solution

```python
from bisect import bisect_left

n = int(input())

a = list(map(int, input().split()))

tails = []

for x in a:

    position = bisect_left(tails, x)

    if position == len(tails):
        tails.append(x)
    else:
        tails[position] = x

print(len(tails))
```

---

# Problem 8: Minimum Coins to Make an Amount

**Topic:** Dynamic Programming  
**Difficulty:** Medium

## Problem Statement

A vending system has coin denominations `C[1..N]`, with an unlimited supply of each.

Find the minimum number of coins needed to make exactly the amount `A`.

If the amount cannot be formed, print `-1`.

## Input Format

- The first line contains `N` and `A`.
- The second line contains `N` distinct coin denominations.

## Output Format

Print the minimum number of coins, or `-1` if the amount cannot be formed.

## Constraints

- `1 ≤ N ≤ 100`
- `1 ≤ C[i] ≤ 10^4`
- `0 ≤ A ≤ 10^4`

## Example 1

### Input

```text
3 11
1 2 5
```

### Output

```text
3
```

### Explanation

`11 = 5 + 5 + 1`

Therefore, 3 coins are needed.

## Example 2

### Input

```text
1 3
2
```

### Output

```text
-1
```

### Explanation

Only coins of value `2` are available, so an odd amount such as `3` cannot be formed.

---

## Approach

Use bottom-up Dynamic Programming.

Let:

`dp[x] = minimum number of coins needed to make amount x`

Start with:

`dp[0] = 0`

For every amount from `1` to `A`, try every available coin.

Greedy does not always work for arbitrary denominations.

**Time Complexity:** O(N × A)  
**Space Complexity:** O(A)

## Iteration / Dry Run

For the input:

`Coins = [1, 2, 5]`, `Amount = 11`

Start with:

`dp[0] = 0`

Then calculate the minimum coins for every amount.

| Amount | Best Combination | Minimum Coins |
|---:|:---|---:|
| 1 | `1` | 1 |
| 2 | `2` | 1 |
| 3 | `1 + 2` | 2 |
| 4 | `2 + 2` | 2 |
| 5 | `5` | 1 |
| 6 | `5 + 1` | 2 |
| 7 | `5 + 2` | 2 |
| 8 | `5 + 2 + 1` | 3 |
| 9 | `5 + 2 + 2` | 3 |
| 10 | `5 + 5` | 2 |
| 11 | `5 + 5 + 1` | 3 |

**Final Answer:** `3`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int amount = sc.nextInt();

        int[] coins = new int[n];

        for (int i = 0; i < n; i++) {
            coins[i] = sc.nextInt();
        }

        int[] dp = new int[amount + 1];

        Arrays.fill(dp, amount + 1);

        dp[0] = 0;

        for (int value = 1; value <= amount; value++) {

            for (int coin : coins) {

                if (coin <= value) {
                    dp[value] = Math.min(
                        dp[value],
                        dp[value - coin] + 1
                    );
                }
            }
        }

        if (dp[amount] == amount + 1) {
            System.out.println(-1);
        } else {
            System.out.println(dp[amount]);
        }
    }
}
```

## Python Solution

```python
n, amount = map(int, input().split())

coins = list(map(int, input().split()))

dp = [amount + 1] * (amount + 1)

dp[0] = 0

for value in range(1, amount + 1):

    for coin in coins:

        if coin <= value:
            dp[value] = min(
                dp[value],
                dp[value - coin] + 1
            )

if dp[amount] == amount + 1:
    print(-1)
else:
    print(dp[amount])
```

---

# Problem 9: Edit Distance

**Topic:** Dynamic Programming, Strings  
**Difficulty:** Hard

## Problem Statement

A spell-correction engine measures how close two words are.

Given strings `S1` and `S2`, find the minimum number of operations needed to convert `S1` into `S2`.

The allowed operations are:

- Insert a character
- Delete a character
- Replace a character

## Input Format

- The first line contains `S1`.
- The second line contains `S2`.

## Output Format

Print the minimum number of operations.

## Constraints

- `1 ≤ |S1|, |S2| ≤ 2000`
- Both strings contain lowercase letters.

## Example 1

### Input

```text
horse
ros
```

### Output

```text
3
```

### Explanation

One possible sequence is:

`horse → rorse → rose → ros`

Three operations are required.

## Example 2

### Input

```text
intention
execution
```

### Output

```text
5
```

### Explanation

The minimum number of operations required is `5`.

---

## Approach

Use the classic **Levenshtein Distance** Dynamic Programming technique.

`dp[i][j]` represents the minimum cost of converting the first `i` characters of `S1` into the first `j` characters of `S2`.

To save memory, only two rows are maintained.

If the current characters are equal, no new operation is required.

Otherwise, choose the minimum of:

- Delete
- Insert
- Replace

and add `1`.

**Time Complexity:** O(m × n)  
**Space Complexity:** O(n)

## Iteration / Dry Run

For the input:

`S1 = "horse"`

`S2 = "ros"`

The DP process compares prefixes of the two strings.

Important transformations include:

1. `horse` → `rorse` : replace `h`
2. `rorse` → `rose` : delete `r`
3. `rose` → `ros` : delete `e`

Therefore:

**Final Answer:** `3`

The DP table ultimately gives `3` as the minimum number of operations.

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        String s1 = sc.nextLine();
        String s2 = sc.nextLine();

        int m = s1.length();
        int n = s2.length();

        int[] previous = new int[n + 1];

        for (int j = 0; j <= n; j++) {
            previous[j] = j;
        }

        for (int i = 1; i <= m; i++) {

            int[] current = new int[n + 1];

            current[0] = i;

            for (int j = 1; j <= n; j++) {

                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {

                    current[j] = previous[j - 1];

                } else {

                    current[j] = 1 + Math.min(
                        previous[j],
                        Math.min(
                            current[j - 1],
                            previous[j - 1]
                        )
                    );
                }
            }

            previous = current;
        }

        System.out.println(previous[n]);
    }
}
```

## Python Solution

```python
s1 = input()
s2 = input()

m = len(s1)
n = len(s2)

previous = list(range(n + 1))

for i in range(1, m + 1):

    current = [i] + [0] * n

    for j in range(1, n + 1):

        if s1[i - 1] == s2[j - 1]:

            current[j] = previous[j - 1]

        else:

            current[j] = 1 + min(
                previous[j],
                current[j - 1],
                previous[j - 1]
            )

    previous = current

print(previous[n])
```

---

# Problem 10: Count Connected Regions - Number of Islands

**Topic:** Graphs, BFS/DFS, Matrix  
**Difficulty:** Medium

## Problem Statement

A satellite image is given as an `R × C` grid where:

- `1` represents land
- `0` represents water

An island is a group of land cells connected horizontally or vertically.

Diagonal connections are not considered.

Count the number of islands.

## Input Format

- The first line contains `R` and `C`.
- Each of the next `R` lines contains `C` space-separated values, either `0` or `1`.

## Output Format

Print the number of islands.

## Constraints

- `1 ≤ R, C ≤ 1000`

## Example 1

### Input

```text
4 5
1 1 0 0 0
1 1 0 0 0
0 0 1 0 0
0 0 0 1 1
```

### Output

```text
3
```

### Explanation

There are three islands:

1. The top-left `2 × 2` block.
2. The single centre cell.
3. The bottom-right pair.

## Example 2

### Input

```text
3 3
1 0 1
0 1 0
1 0 1
```

### Output

```text
5
```

### Explanation

Diagonal cells are not connected, so every land cell forms its own island.

---

## Approach

Scan every cell.

Whenever an unvisited land cell is found:

1. Increase the island count.
2. Start BFS from that cell.
3. Visit all horizontally and vertically connected land cells.
4. Mark them as visited.

An iterative BFS avoids recursion-depth problems.

**Time Complexity:** O(R × C)  
**Space Complexity:** O(R × C)

## Iteration / Dry Run

For the grid:

```text
1 1 0 0 0
1 1 0 0 0
0 0 1 0 0
0 0 0 1 1
```

Scan the grid from top-left.

| Step | Cell Found | Action | Island Count |
|---:|:---:|:---|---:|
| 1 | `(0,0)` | Start BFS and visit top-left block | 1 |
| 2 | `(2,2)` | Start BFS for centre cell | 2 |
| 3 | `(3,3)` | Start BFS and visit `(3,4)` | 3 |

All connected cells are marked as visited during BFS.

**Final Answer:** `3`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int r = sc.nextInt();
        int c = sc.nextInt();

        int[][] grid = new int[r][c];

        for (int i = 0; i < r; i++) {

            for (int j = 0; j < c; j++) {
                grid[i][j] = sc.nextInt();
            }
        }

        int islands = 0;

        int[] dx = {1, -1, 0, 0};
        int[] dy = {0, 0, 1, -1};

        for (int i = 0; i < r; i++) {

            for (int j = 0; j < c; j++) {

                if (grid[i][j] == 1) {

                    islands++;

                    Queue<int[]> queue = new LinkedList<>();

                    queue.add(new int[]{i, j});

                    grid[i][j] = 0;

                    while (!queue.isEmpty()) {

                        int[] cell = queue.poll();

                        int x = cell[0];
                        int y = cell[1];

                        for (int d = 0; d < 4; d++) {

                            int nx = x + dx[d];
                            int ny = y + dy[d];

                            if (nx >= 0 && nx < r &&
                                ny >= 0 && ny < c &&
                                grid[nx][ny] == 1) {

                                grid[nx][ny] = 0;

                                queue.add(new int[]{nx, ny});
                            }
                        }
                    }
                }
            }
        }

        System.out.println(islands);
    }
}
```

## Python Solution

```python
from collections import deque

r, c = map(int, input().split())

grid = []

for _ in range(r):
    grid.append(list(map(int, input().split())))

islands = 0

directions = [
    (1, 0),
    (-1, 0),
    (0, 1),
    (0, -1)
]

for i in range(r):

    for j in range(c):

        if grid[i][j] == 1:

            islands += 1

            queue = deque([(i, j)])

            grid[i][j] = 0

            while queue:

                x, y = queue.popleft()

                for dx, dy in directions:

                    nx = x + dx
                    ny = y + dy

                    if (0 <= nx < r and
                        0 <= ny < c and
                        grid[nx][ny] == 1):

                        grid[nx][ny] = 0

                        queue.append((nx, ny))

print(islands)
```

---

# Problem 11: Minimum Time to Infect All Systems - Rotting Oranges

**Topic:** Graphs, Multi-source BFS  
**Difficulty:** Hard

## Problem Statement

A server farm is laid out as an `R × C` grid.

Each cell contains:

- `0` = empty slot
- `1` = healthy server
- `2` = infected server

Every minute, each infected server infects its healthy neighbours above, below, left and right.

Find the minimum number of minutes until no healthy server remains.

If some healthy server can never be infected, print `-1`.

## Input Format

- The first line contains `R` and `C`.
- Each of the next `R` lines contains `C` space-separated values: `0`, `1`, or `2`.

## Output Format

Print the minimum number of minutes, or `-1`.

## Constraints

- `1 ≤ R, C ≤ 500`

## Example 1

### Input

```text
3 3
2 1 1
1 1 0
0 1 1
```

### Output

```text
4
```

### Explanation

The infection reaches the bottom-right server at minute `4`.

## Example 2

### Input

```text
3 3
2 1 1
0 1 1
1 0 1
```

### Output

```text
-1
```

### Explanation

The server at the bottom-left is isolated and can never be infected.

---

## Approach

Use **Multi-source BFS**.

Instead of starting BFS from one infected server, put every initially infected server into the queue at time `0`.

Each newly infected server is reached one minute later.

At the end:

- If all healthy servers are infected, print the maximum time.
- Otherwise, print `-1`.

**Time Complexity:** O(R × C)  
**Space Complexity:** O(R × C)

## Iteration / Dry Run

For the grid:

```text
2 1 1
1 1 0
0 1 1
```

The initially infected cell is `(0,0)`.

| Minute | Newly Infected Cells |
|---:|:---|
| 0 | `(0,0)` |
| 1 | `(0,1)`, `(1,0)` |
| 2 | `(0,2)`, `(1,1)` |
| 3 | `(2,1)` |
| 4 | `(2,2)` |

At minute `4`, there are no healthy servers left.

**Final Answer:** `4`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int r = sc.nextInt();
        int c = sc.nextInt();

        int[][] grid = new int[r][c];

        Queue<int[]> queue = new LinkedList<>();

        int healthy = 0;

        for (int i = 0; i < r; i++) {

            for (int j = 0; j < c; j++) {

                grid[i][j] = sc.nextInt();

                if (grid[i][j] == 2) {
                    queue.add(new int[]{i, j, 0});
                } else if (grid[i][j] == 1) {
                    healthy++;
                }
            }
        }

        int minutes = 0;

        int[] dx = {1, -1, 0, 0};
        int[] dy = {0, 0, 1, -1};

        while (!queue.isEmpty()) {

            int[] cell = queue.poll();

            int x = cell[0];
            int y = cell[1];
            int time = cell[2];

            minutes = Math.max(minutes, time);

            for (int d = 0; d < 4; d++) {

                int nx = x + dx[d];
                int ny = y + dy[d];

                if (nx >= 0 && nx < r &&
                    ny >= 0 && ny < c &&
                    grid[nx][ny] == 1) {

                    grid[nx][ny] = 2;

                    healthy--;

                    queue.add(new int[]{nx, ny, time + 1});
                }
            }
        }

        if (healthy == 0) {
            System.out.println(minutes);
        } else {
            System.out.println(-1);
        }
    }
}
```

## Python Solution

```python
from collections import deque

r, c = map(int, input().split())

grid = []

queue = deque()

healthy = 0

for i in range(r):

    row = list(map(int, input().split()))

    grid.append(row)

    for j in range(c):

        if row[j] == 2:
            queue.append((i, j, 0))

        elif row[j] == 1:
            healthy += 1

minutes = 0

directions = [
    (1, 0),
    (-1, 0),
    (0, 1),
    (0, -1)
]

while queue:

    x, y, time = queue.popleft()

    minutes = max(minutes, time)

    for dx, dy in directions:

        nx = x + dx
        ny = y + dy

        if (0 <= nx < r and
            0 <= ny < c and
            grid[nx][ny] == 1):

            grid[nx][ny] = 2

            healthy -= 1

            queue.append((nx, ny, time + 1))

if healthy == 0:
    print(minutes)
else:
    print(-1)
```

---

# Problem 12: Build Order of Modules

**Topic:** Graphs, Topological Sort, Heap  
**Difficulty:** Hard

## Problem Statement

A software project has `N` modules numbered from `0` to `N - 1` and `M` dependency rules.

A rule `U V` means module `U` must be built before module `V`.

Print a valid build order.

If several orders are valid, print the lexicographically smallest one.

If a circular dependency makes building impossible, print `-1`.

## Input Format

- The first line contains `N` and `M`.
- Each of the next `M` lines contains two integers `U` and `V`.

## Output Format

Print the build order as space-separated module numbers, or `-1`.

## Constraints

- `1 ≤ N ≤ 10^5`
- `0 ≤ M ≤ 2 × 10^5`

## Example 1

### Input

```text
6 6
5 2
5 0
4 0
4 1
2 3
3 1
```

### Output

```text
4 5 0 2 3 1
```

### Explanation

Modules `4` and `5` have no prerequisites.

The smaller ready module is selected first.

The process continues until all modules are built.

## Example 2

### Input

```text
3 3
0 1
1 2
2 0
```

### Output

```text
-1
```

### Explanation

The dependency graph contains a cycle:

`0 → 1 → 2 → 0`

Therefore, no valid build order exists.

---

## Approach

Use **Kahn's Topological Sort Algorithm**.

1. Calculate the indegree of every module.
2. Put all modules with indegree `0` into a min-heap.
3. Remove the smallest available module.
4. Reduce the indegree of its neighbours.
5. Add a neighbour to the heap when its indegree becomes `0`.
6. If fewer than `N` modules are processed, a cycle exists.

The min-heap ensures the lexicographically smallest valid order.

**Time Complexity:** O((N + M) log N)  
**Space Complexity:** O(N + M)

## Iteration / Dry Run

For the input:

```text
6 6
5 2
5 0
4 0
4 1
2 3
3 1
```

Initial indegrees:

- `0 → 2`
- `1 → 2`
- `2 → 1`
- `3 → 1`
- `4 → 0`
- `5 → 0`

The initial ready modules are `4` and `5`.

Because we use a min-heap, choose the smaller module first.

| Step | Selected Module | Newly Ready Module(s) | Order |
|---:|---:|:---|:---|
| 1 | 4 | — | `4` |
| 2 | 5 | `0`, `2` | `4 5` |
| 3 | 0 | — | `4 5 0` |
| 4 | 2 | `3` | `4 5 0 2` |
| 5 | 3 | `1` | `4 5 0 2 3` |
| 6 | 1 | — | `4 5 0 2 3 1` |

**Final Answer:** `4 5 0 2 3 1`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int m = sc.nextInt();

        ArrayList<Integer>[] graph = new ArrayList[n];

        for (int i = 0; i < n; i++) {
            graph[i] = new ArrayList<>();
        }

        int[] indegree = new int[n];

        for (int i = 0; i < m; i++) {

            int u = sc.nextInt();
            int v = sc.nextInt();

            graph[u].add(v);

            indegree[v]++;
        }

        PriorityQueue<Integer> heap = new PriorityQueue<>();

        for (int i = 0; i < n; i++) {

            if (indegree[i] == 0) {
                heap.add(i);
            }
        }

        ArrayList<Integer> order = new ArrayList<>();

        while (!heap.isEmpty()) {

            int u = heap.poll();

            order.add(u);

            for (int v : graph[u]) {

                indegree[v]--;

                if (indegree[v] == 0) {
                    heap.add(v);
                }
            }
        }

        if (order.size() != n) {

            System.out.println(-1);

        } else {

            for (int x : order) {
                System.out.print(x + " ");
            }
        }
    }
}
```

## Python Solution

```python
import heapq

n, m = map(int, input().split())

graph = [[] for _ in range(n)]

indegree = [0] * n

for _ in range(m):

    u, v = map(int, input().split())

    graph[u].append(v)

    indegree[v] += 1

heap = []

for i in range(n):

    if indegree[i] == 0:
        heapq.heappush(heap, i)

order = []

while heap:

    u = heapq.heappop(heap)

    order.append(u)

    for v in graph[u]:

        indegree[v] -= 1

        if indegree[v] == 0:
            heapq.heappush(heap, v)

if len(order) != n:
    print(-1)
else:
    print(*order)
```

---

# Problem 13: Sliding Window Maximum

**Topic:** Deque, Sliding Window  
**Difficulty:** Hard

## Problem Statement

A monitoring dashboard shows the peak CPU load over every window of `K` consecutive readings.

Given `N` readings and the window size `K`, print the maximum of each window from left to right.

The expected solution runs in `O(N)`.

## Input Format

- The first line contains `N` and `K`.
- The second line contains `N` space-separated integers.

## Output Format

Print `N - K + 1` space-separated integers representing the maximum of every window.

## Constraints

- `1 ≤ K ≤ N ≤ 10^5`
- `-10^4 ≤ A[i] ≤ 10^4`

## Example 1

### Input

```text
8 3
1 3 -1 -3 5 3 6 7
```

### Output

```text
3 3 5 5 6 7
```

### Explanation

The windows include:

`[1, 3, -1] → 3`

`[3, -1, -3] → 3`

`[-1, -3, 5] → 5`

and so on.

## Example 2

### Input

```text
1 1
5
```

### Output

```text
5
```

### Explanation

There is only one window, containing one element.

---

## Approach

Use a **monotonic deque** containing indices.

The values corresponding to these indices are kept in decreasing order.

For every new element:

1. Remove indices that have moved outside the window.
2. Remove smaller elements from the back.
3. Add the current index.
4. The front of the deque is the maximum.

Each index is added and removed at most once.

**Time Complexity:** O(n)  
**Space Complexity:** O(k)

## Iteration / Dry Run

For the input:

`A = [1, 3, -1, -3, 5, 3, 6, 7]`

`K = 3`

The windows and their maximum values are:

| Window | Maximum |
|:---|---:|
| `[1, 3, -1]` | 3 |
| `[3, -1, -3]` | 3 |
| `[-1, -3, 5]` | 5 |
| `[-3, 5, 3]` | 5 |
| `[5, 3, 6]` | 6 |
| `[3, 6, 7]` | 7 |

**Final Answer:** `3 3 5 5 6 7`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int k = sc.nextInt();

        int[] a = new int[n];

        for (int i = 0; i < n; i++) {
            a[i] = sc.nextInt();
        }

        Deque<Integer> deque = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {

            if (!deque.isEmpty() &&
                deque.peekFirst() <= i - k) {

                deque.pollFirst();
            }

            while (!deque.isEmpty() &&
                   a[deque.peekLast()] <= a[i]) {

                deque.pollLast();
            }

            deque.addLast(i);

            if (i >= k - 1) {
                System.out.print(a[deque.peekFirst()] + " ");
            }
        }
    }
}
```

## Python Solution

```python
from collections import deque

n, k = map(int, input().split())

a = list(map(int, input().split()))

deque = deque()

result = []

for i in range(n):

    if deque and deque[0] <= i - k:
        deque.popleft()

    while deque and a[deque[-1]] <= a[i]:
        deque.pop()

    deque.append(i)

    if i >= k - 1:
        result.append(a[deque[0]])

print(*result)
```

---

# Problem 14: Largest Rectangle in a Histogram

**Topic:** Stack, Arrays  
**Difficulty:** Hard

## Problem Statement

Given the heights of `N` bars in a histogram, where every bar has width `1`, find the area of the largest rectangle that fits completely inside the histogram.

## Input Format

- The first line contains `N`.
- The second line contains `N` non-negative integers representing the bar heights.

## Output Format

Print the area of the largest rectangle.

## Constraints

- `1 ≤ N ≤ 10^5`
- `0 ≤ H[i] ≤ 10^4`

## Example 1

### Input

```text
6
2 1 5 6 2 3
```

### Output

```text
10
```

### Explanation

The bars with heights `5` and `6` form a rectangle with:

- Height = `5`
- Width = `2`

Area:

`5 × 2 = 10`

## Example 2

### Input

```text
2
2 4
```

### Output

```text
4
```

### Explanation

The single bar of height `4` gives area `4`.

---

## Approach

Use a **monotonic increasing stack**.

The stack stores indices of bars in increasing order of height.

When a shorter bar arrives:

1. Pop taller bars.
2. The current index becomes their right boundary.
3. The new stack top gives their left boundary.
4. Calculate the rectangle area.
5. Continue until the stack is valid again.

A final height of `0` is added to process all remaining bars.

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

## Iteration / Dry Run

For the input:

`[2, 1, 5, 6, 2, 3]`

The important stack operations are:

| Current Bar | Stack Action | Rectangle Considered | Best Area |
|---:|:---|:---|---:|
| 2 | Push | — | 0 |
| 1 | Pop `2` | `2 × 1 = 2` | 2 |
| 5 | Push | — | 2 |
| 6 | Push | — | 2 |
| 2 | Pop `6` | `6 × 1 = 6` | 6 |
| 2 | Pop `5` | `5 × 2 = 10` | 10 |
| 3 | Push | — | 10 |
| 0 | Pop remaining bars | Remaining rectangles | 10 |

The largest rectangle is formed by bars `5` and `6`.

**Final Answer:** `10`

## Java Solution

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] h = new int[n + 1];

        for (int i = 0; i < n; i++) {
            h[i] = sc.nextInt();
        }

        h[n] = 0;

        Stack<Integer> stack = new Stack<>();

        int best = 0;

        for (int i = 0; i <= n; i++) {

            while (!stack.isEmpty() &&
                   h[stack.peek()] >= h[i]) {

                int height = h[stack.pop()];

                int left;

                if (stack.isEmpty()) {
                    left = 0;
                } else {
                    left = stack.peek() + 1;
                }

                int width = i - left;

                best = Math.max(best, height * width);
            }

            stack.push(i);
        }

        System.out.println(best);
    }
}
```

## Python Solution

```python
n = int(input())

h = list(map(int, input().split()))

h.append(0)

stack = []

best = 0

for i in range(len(h)):

    while stack and h[stack[-1]] >= h[i]:

        height = h[stack.pop()]

        if stack:
            left = stack[-1] + 1
        else:
            left = 0

        width = i - left

        best = max(best, height * width)

    stack.append(i)

print(best)
```

---

# Problem 15: Network Delay Time

**Topic:** Graphs, Dijkstra's Algorithm  
**Difficulty:** Hard

## Problem Statement

A data centre has `N` servers labelled `1` to `N`, connected by `M` directed links.

Each link `U V W` means a signal travels from server `U` to server `V` in `W` milliseconds.

A signal is sent from server `S`.

Find the minimum time needed for all servers to receive the signal.

If any server cannot be reached, print `-1`.

## Input Format

- The first line contains `N`, `M`, and `S`.
- Each of the next `M` lines contains `U`, `V`, and `W`.

## Output Format

Print the minimum time for all servers to receive the signal, or `-1`.

## Constraints

- `1 ≤ N ≤ 10^5`
- `1 ≤ M ≤ 2 × 10^5`
- `0 ≤ W ≤ 10^4`

## Example 1

### Input

```text
4 3 2
2 1 1
2 3 1
3 4 1
```

### Output

```text
2
```

### Explanation

Server `4` is reached last through:

`2 → 3 → 4`

The total time is:

`1 + 1 = 2`

## Example 2

### Input

```text
2 1 2
1 2 1
```

### Output

```text
-1
```

### Explanation

There is no path from server `2` to server `1`.

Therefore, server `1` cannot receive the signal.

---

## Approach

Use **Dijkstra's Algorithm** because all link weights are non-negative.

1. Set the distance of the source server to `0`.
2. Put the source in a min-heap.
3. Always process the server with the smallest known distance.
4. Relax all outgoing edges.
5. Continue until the heap is empty.
6. The answer is the largest shortest distance.
7. If any server remains unreachable, print `-1`.

**Time Complexity:** O((N + M) log N)  
**Space Complexity:** O(N + M)

## Iteration / Dry Run

For the input:

```text
4 3 2
2 1 1
2 3 1
3 4 1
```

Source server = `2`

Initial distances:

```text
Server 1 = ∞
Server 2 = 0
Server 3 = ∞
Server 4 = ∞
```

| Step | Server Processed | Updated Distances |
|---:|---:|:---|
| 1 | 2 | `1 = 1`, `3 = 1` |
| 2 | 1 | No update |
| 3 | 3 | `4 = 2` |
| 4 | 4 | No update |

Final shortest distances:

```text
Server 1 = 1
Server 2 = 0
Server 3 = 1
Server 4 = 2
```

The signal reaches server `4` last at time `2`.

**Final Answer:** `2`

## Java Solution

```java
import java.util.*;

public class Main {

    static class Edge {
        int to;
        int weight;

        Edge(int to, int weight) {
            this.to = to;
            this.weight = weight;
        }
    }

    static class Node implements Comparable<Node> {

        int vertex;
        int distance;

        Node(int vertex, int distance) {
            this.vertex = vertex;
            this.distance = distance;
        }

        public int compareTo(Node other) {
            return Integer.compare(
                this.distance,
                other.distance
            );
        }
    }

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int m = sc.nextInt();
        int source = sc.nextInt();

        ArrayList<Edge>[] graph = new ArrayList[n + 1];

        for (int i = 1; i <= n; i++) {
            graph[i] = new ArrayList<>();
        }

        for (int i = 0; i < m; i++) {

            int u = sc.nextInt();
            int v = sc.nextInt();
            int w = sc.nextInt();

            graph[u].add(new Edge(v, w));
        }

        int INF = Integer.MAX_VALUE;

        int[] distance = new int[n + 1];

        Arrays.fill(distance, INF);

        distance[source] = 0;

        PriorityQueue<Node> heap = new PriorityQueue<>();

        heap.add(new Node(source, 0));

        while (!heap.isEmpty()) {

            Node current = heap.poll();

            int u = current.vertex;
            int d = current.distance;

            if (d > distance[u]) {
                continue;
            }

            for (Edge edge : graph[u]) {

                int v = edge.to;
                int w = edge.weight;

                if (d + w < distance[v]) {

                    distance[v] = d + w;

                    heap.add(new Node(v, distance[v]));
                }
            }
        }

        int answer = 0;

        for (int i = 1; i <= n; i++) {

            if (distance[i] == INF) {
                System.out.println(-1);
                return;
            }

            answer = Math.max(answer, distance[i]);
        }

        System.out.println(answer);
    }
}
```

## Python Solution

```python
import heapq

n, m, source = map(int, input().split())

graph = [[] for _ in range(n + 1)]

for _ in range(m):

    u, v, w = map(int, input().split())

    graph[u].append((v, w))

INF = float('inf')

distance = [INF] * (n + 1)

distance[source] = 0

heap = [(0, source)]

while heap:

    d, u = heapq.heappop(heap)

    if d > distance[u]:
        continue

    for v, w in graph[u]:

        new_distance = d + w

        if new_distance < distance[v]:

            distance[v] = new_distance

            heapq.heappush(
                heap,
                (new_distance, v)
            )

answer = max(distance[1:])

if answer == INF:
    print(-1)
else:
    print(answer)
```

---

# Quick Revision - Problem and Technique

| No. | Problem | Main Technique | Time Complexity | Space Complexity |
|---|---|---|---|---|
| 1 | Longest Substring with K Distinct | Sliding Window + HashMap | O(n) | O(k) |
| 2 | Minimum Platforms | Sorting + Two Pointers | O(n log n) | O(n) |
| 3 | Maximum Product Subarray | Dynamic Programming | O(n) | O(1) |
| 4 | Trapping Rain Water | Two Pointers | O(n) | O(1) |
| 5 | Next Lexicographic Permutation | Swap + Reverse | O(n) | O(1) |
| 6 | Count Subarrays with Sum K | Prefix Sum + HashMap | O(n) | O(n) |
| 7 | Longest Increasing Subsequence | Binary Search | O(n log n) | O(n) |
| 8 | Minimum Coins | Dynamic Programming | O(n × A) | O(A) |
| 9 | Edit Distance | Dynamic Programming | O(m × n) | O(n) |
| 10 | Number of Islands | BFS | O(R × C) | O(R × C) |
| 11 | Rotting Oranges | Multi-source BFS | O(R × C) | O(R × C) |
| 12 | Build Order | Topological Sort + Min Heap | O((N + M) log N) | O(N + M) |
| 13 | Sliding Window Maximum | Deque | O(n) | O(k) |
| 14 | Largest Rectangle | Monotonic Stack | O(n) | O(n) |
| 15 | Network Delay Time | Dijkstra + Min Heap | O((N + M) log N) | O(N + M) |

---

# Important Coding Patterns to Remember

### Sliding Window

Used in:

- Longest Substring
- Sliding Window Maximum

### Two Pointers

Used in:

- Minimum Platforms
- Trapping Rain Water
- Next Permutation

### HashMap / Prefix Sum

Used in:

- Longest Substring
- Count Subarrays with Sum K

### Dynamic Programming

Used in:

- Maximum Product Subarray
- Minimum Coins
- Edit Distance

### BFS

Used in:

- Number of Islands
- Rotting Oranges

### Heap / Priority Queue

Used in:

- Build Order
- Network Delay Time

### Stack

Used in:

- Largest Rectangle in Histogram

### Binary Search

Used in:

- Longest Increasing Subsequence
