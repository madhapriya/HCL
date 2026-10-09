# LeetCode Coding Questions – Easy & Best Java + Python Solutions

## Selected LeetCode Problems

This set contains the LeetCode questions requested by problem number:

**121, 53, 152, 921, 856, 2078, 3483, 3870, 3871, 1, 191**

For each problem:
- Problem Statement
- Input / Output
- Constraints
- Example
- Easy & Best Approach
- Iteration / Dry Run
- Java Solution
- Python Solution
- Time & Space Complexity

---

# 1. LeetCode 121 – Best Time to Buy and Sell Stock

**Difficulty:** Easy  
**Pattern:** Array / Greedy

## Problem Statement

You are given an array `prices`, where `prices[i]` is the stock price on day `i`.

Choose one day to buy one stock and a later day to sell it so that the profit is maximum.

Return the maximum profit. If no profit is possible, return `0`.

## Input Format

```text
prices = [7,1,5,3,6,4]
```

## Output Format

```text
5
```

## Constraints

- `1 <= prices.length <= 10^5`
- `0 <= prices[i] <= 10^4`

## Example

```text
Input:  [7,1,5,3,6,4]
Output: 5
```

Buy at `1` and sell at `6`.

## Approach

Keep track of:

- `minPrice` = minimum price seen so far
- `maxProfit` = maximum profit found so far

For every price:

```text
profit = currentPrice - minPrice
```

Then update the minimum price.

This avoids checking every possible buy/sell pair.

## Iteration / Dry Run

For `[7,1,5,3,6,4]`:

| Price | Minimum Price | Profit | Maximum Profit |
|---:|---:|---:|---:|
| 7 | 7 | 0 | 0 |
| 1 | 1 | 0 | 0 |
| 5 | 1 | 4 | 4 |
| 3 | 1 | 2 | 4 |
| 6 | 1 | 5 | 5 |
| 4 | 1 | 3 | 5 |

**Answer = 5**

## Java Solution

```java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = prices[0];
        int maxProfit = 0;

        for (int price : prices) {
            minPrice = Math.min(minPrice, price);
            maxProfit = Math.max(maxProfit, price - minPrice);
        }

        return maxProfit;
    }
}
```

## Python Solution

```python
class Solution:
    def maxProfit(self, prices):
        min_price = prices[0]
        max_profit = 0

        for price in prices:
            min_price = min(min_price, price)
            max_profit = max(max_profit, price - min_price)

        return max_profit
```

**Time:** `O(n)`  
**Space:** `O(1)`

---

# 2. LeetCode 53 – Maximum Subarray

**Difficulty:** Medium  
**Pattern:** Kadane's Algorithm / Dynamic Programming

## Problem Statement

Given an integer array `nums`, find the contiguous subarray with the largest sum and return that sum.

The subarray must contain at least one element.

## Input Format

```text
nums = [-2,1,-3,4,-1,2,1,-5,4]
```

## Output Format

```text
6
```

## Constraints

- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

## Example

```text
Input:  [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
```

The best subarray is:

```text
[4,-1,2,1]
```

Sum = `6`.

## Approach – Kadane's Algorithm

At every element, decide:

1. Start a new subarray from this element.
2. Extend the previous subarray.

Formula:

```text
current = max(num, current + num)
answer = max(answer, current)
```

## Iteration / Dry Run

For `[-2,1,-3,4,-1,2,1,-5,4]`:

| Number | Current | Best |
|---:|---:|---:|
| -2 | -2 | -2 |
| 1 | 1 | 1 |
| -3 | -2 | 1 |
| 4 | 4 | 4 |
| -1 | 3 | 4 |
| 2 | 5 | 5 |
| 1 | 6 | 6 |
| -5 | 1 | 6 |
| 4 | 5 | 6 |

**Answer = 6**

## Java Solution

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int current = nums[0];
        int best = nums[0];

        for (int i = 1; i < nums.length; i++) {
            current = Math.max(nums[i], current + nums[i]);
            best = Math.max(best, current);
        }

        return best;
    }
}
```

## Python Solution

```python
class Solution:
    def maxSubArray(self, nums):
        current = nums[0]
        best = nums[0]

        for num in nums[1:]:
            current = max(num, current + num)
            best = max(best, current)

        return best
```

**Time:** `O(n)`  
**Space:** `O(1)`

---

# 3. LeetCode 152 – Maximum Product Subarray

**Difficulty:** Medium  
**Pattern:** Dynamic Programming

## Problem Statement

Given an integer array `nums`, find a contiguous subarray whose product is as large as possible.

Return the maximum product.

## Input Format

```text
nums = [2,3,-2,4]
```

## Output Format

```text
6
```

## Constraints

- `1 <= nums.length <= 2 * 10^4`
- `-10 <= nums[i] <= 10`
- The product fits in a 32-bit signed integer.

## Example

```text
Input:  [2,3,-2,4]
Output: 6
```

The best subarray is `[2,3]`.

## Approach

For sums, Kadane's algorithm keeps one value.

For products, we need **two values**:

- `maxProduct` = maximum product ending here
- `minProduct` = minimum product ending here

Why keep the minimum?

Because multiplying a negative number by the minimum negative product can create a large positive product.

When the current number is negative, swap the maximum and minimum before updating.

## Iteration / Dry Run

For `[2,3,-2,4]`:

| Number | Max Ending Here | Min Ending Here | Answer |
|---:|---:|---:|---:|
| 2 | 2 | 2 | 2 |
| 3 | 6 | 3 | 6 |
| -2 | -2 | -12 | 6 |
| 4 | 4 | -48 | 6 |

**Answer = 6**

## Java Solution

```java
class Solution {
    public int maxProduct(int[] nums) {
        int maxProduct = nums[0];
        int minProduct = nums[0];
        int answer = nums[0];

        for (int i = 1; i < nums.length; i++) {
            int num = nums[i];

            if (num < 0) {
                int temp = maxProduct;
                maxProduct = minProduct;
                minProduct = temp;
            }

            maxProduct = Math.max(num, maxProduct * num);
            minProduct = Math.min(num, minProduct * num);

            answer = Math.max(answer, maxProduct);
        }

        return answer;
    }
}
```

## Python Solution

```python
class Solution:
    def maxProduct(self, nums):
        max_product = nums[0]
        min_product = nums[0]
        answer = nums[0]

        for num in nums[1:]:
            if num < 0:
                max_product, min_product = min_product, max_product

            max_product = max(num, max_product * num)
            min_product = min(num, min_product * num)

            answer = max(answer, max_product)

        return answer
```

**Time:** `O(n)`  
**Space:** `O(1)`

---

# 4. LeetCode 921 – Minimum Add to Make Parentheses Valid

**Difficulty:** Medium  
**Pattern:** Greedy / Parentheses

## Problem Statement

You are given a string containing only `(` and `)`.

In one move, you can insert one parenthesis anywhere.

Return the minimum number of insertions needed to make the string valid.

## Input Format

```text
s = "())"
```

## Output Format

```text
1
```

## Constraints

- `1 <= s.length <= 1000`
- Each character is `(` or `)`.

## Example

```text
Input:  "())"
Output: 1
```

One extra `(` is enough:

```text
(())
```

## Approach

We do not need an actual stack.

Maintain:

- `open` = unmatched `(` count
- `answer` = unmatched `)` that need an opening `(`

For `(`:

```text
open++
```

For `)`:

- If an opening bracket exists, match it: `open--`
- Otherwise, we need to insert `(`: `answer++`

At the end, every remaining `open` needs a `)`.

```text
answer += open
```

## Iteration / Dry Run

For `"()))"`:

| Character | Open | Insertions |
|---|---:|---:|
| `(` | 1 | 0 |
| `)` | 0 | 0 |
| `)` | 0 | 1 |
| `)` | 0 | 2 |

Final answer:

```text
2
```

## Java Solution

```java
class Solution {
    public int minAddToMakeValid(String s) {
        int open = 0;
        int answer = 0;

        for (char c : s.toCharArray()) {
            if (c == '(') {
                open++;
            } else if (open > 0) {
                open--;
            } else {
                answer++;
            }
        }

        return answer + open;
    }
}
```

## Python Solution

```python
class Solution:
    def minAddToMakeValid(self, s):
        open_count = 0
        answer = 0

        for c in s:
            if c == '(':
                open_count += 1
            elif open_count > 0:
                open_count -= 1
            else:
                answer += 1

        return answer + open_count
```

**Time:** `O(n)`  
**Space:** `O(1)`

---

# 5. LeetCode 856 – Score of Parentheses

**Difficulty:** Medium  
**Pattern:** Stack / Depth

## Problem Statement

Given a balanced parentheses string, calculate its score using:

```text
() = 1
AB = A + B
(A) = 2 * A
```

Return the total score.

## Input Format

```text
s = "(())"
```

## Output Format

```text
2
```

## Constraints

- `2 <= s.length <= 50`
- The string contains only `(` and `)`.
- The input is balanced.

## Examples

```text
Input:  "()" 
Output: 1

Input:  "(())"
Output: 2

Input:  "()()"
Output: 2
```

## Approach – Depth Counting

Keep track of the current nesting depth.

Whenever we see a closing `)` immediately after `(`, we found a primitive `()`.

Its contribution is:

```text
2^(depth - 1)
```

Why?

Each surrounding pair doubles the score.

## Iteration / Dry Run

For `"(())"`:

```text
(  -> depth = 1
(  -> depth = 2
)  -> previous was '('
      add 2^(2-1) = 2
)  -> depth = 0
```

Answer:

```text
2
```

For `"()()"`:

```text
() -> 1
() -> 1

Total = 2
```

## Java Solution

```java
class Solution {
    public int scoreOfParentheses(String s) {
        int depth = 0;
        int score = 0;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (c == '(') {
                depth++;
            } else {
                if (s.charAt(i - 1) == '(') {
                    score += 1 << (depth - 1);
                }
                depth--;
            }
        }

        return score;
    }
}
```

## Python Solution

```python
class Solution:
    def scoreOfParentheses(self, s):
        depth = 0
        score = 0

        for i, c in enumerate(s):
            if c == '(':
                depth += 1
            else:
                if s[i - 1] == '(':
                    score += 1 << (depth - 1)
                depth -= 1

        return score
```

**Time:** `O(n)`  
**Space:** `O(1)`

---

# 6. LeetCode 2078 – Two Furthest Houses With Different Colors

**Difficulty:** Easy  
**Pattern:** Greedy / Array

## Problem Statement

You are given an array `colors`, where each element represents the color of a house.

Find the maximum distance between two houses having different colors.

Distance between indices `i` and `j` is:

```text
abs(i - j)
```

## Input Format

```text
colors = [1,1,1,6,1,1,1]
```

## Output Format

```text
3
```

## Constraints

- `2 <= colors.length <= 100`
- `0 <= colors[i] <= 100`
- At least two houses have different colors.

## Example

```text
Input:  [1,1,1,6,1,1,1]
Output: 3
```

House `0` and house `3` have different colors.

Distance:

```text
3 - 0 = 3
```

## Approach

The maximum distance must involve either:

- the first house, or
- the last house.

Check:

```text
distance from first house to every different-color house
distance from last house to every different-color house
```

Keep the maximum.

## Iteration / Dry Run

For:

```text
[1,1,1,6,1,1,1]
```

From first house:

```text
index 3 -> color 6 != 1
distance = 3
```

From last house:

```text
index 3 -> color 6 != 1
distance = 6 - 3 = 3
```

**Answer = 3**

## Java Solution

```java
class Solution {
    public int maxDistance(int[] colors) {
        int n = colors.length;
        int answer = 0;

        for (int i = 0; i < n; i++) {
            if (colors[i] != colors[0]) {
                answer = Math.max(answer, i);
            }

            if (colors[i] != colors[n - 1]) {
                answer = Math.max(answer, n - 1 - i);
            }
        }

        return answer;
    }
}
```

## Python Solution

```python
class Solution:
    def maxDistance(self, colors):
        n = len(colors)
        answer = 0

        for i in range(n):
            if colors[i] != colors[0]:
                answer = max(answer, i)

            if colors[i] != colors[-1]:
                answer = max(answer, n - 1 - i)

        return answer
```

**Time:** `O(n)`  
**Space:** `O(1)`

---

# 7. LeetCode 3483 – Unique 3-Digit Even Numbers

**Difficulty:** Easy  
**Pattern:** Enumeration / Hash Set

## Problem Statement

You are given an array of digits.

Count how many distinct three-digit even numbers can be formed.

Rules:

- Each copy of a digit can be used at most once for a number.
- The first digit cannot be `0`.
- The last digit must be even.

## Input Format

```text
digits = [1,2,3,4]
```

## Output Format

```text
12
```

## Constraints

- `3 <= digits.length <= 10`
- `0 <= digits[i] <= 9`

## Example

```text
Input:  [1,2,3,4]
Output: 12
```

Some valid numbers are:

```text
124, 132, 134, 142,
214, 234,
312, 314, 324, 342,
412, 432
```

## Approach

Since there are at most 10 digits, a simple triple loop is fast enough.

Choose:

```text
i = hundreds digit
j = tens digit
k = units digit
```

Check:

```text
i, j, k are different indices
hundreds digit != 0
units digit is even
```

Insert the resulting number into a `HashSet` so duplicates are counted only once.

## Iteration / Dry Run

For:

```text
digits = [0,2,2]
```

Possible valid numbers include:

```text
202
220
```

Both are distinct, so:

```text
answer = 2
```

The repeated `2` can be used twice because the input contains two copies.

## Java Solution

```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int totalNumbers(int[] digits) {
        Set<Integer> set = new HashSet<>();
        int n = digits.length;

        for (int i = 0; i < n; i++) {
            if (digits[i] == 0) {
                continue;
            }

            for (int j = 0; j < n; j++) {
                if (j == i) {
                    continue;
                }

                for (int k = 0; k < n; k++) {
                    if (k == i || k == j) {
                        continue;
                    }

                    if (digits[k] % 2 == 0) {
                        int number = digits[i] * 100
                                   + digits[j] * 10
                                   + digits[k];

                        set.add(number);
                    }
                }
            }
        }

        return set.size();
    }
}
```

## Python Solution

```python
class Solution:
    def totalNumbers(self, digits):
        numbers = set()
        n = len(digits)

        for i in range(n):
            if digits[i] == 0:
                continue

            for j in range(n):
                if j == i:
                    continue

                for k in range(n):
                    if k == i or k == j:
                        continue

                    if digits[k] % 2 == 0:
                        number = digits[i] * 100 + digits[j] * 10 + digits[k]
                        numbers.add(number)

        return len(numbers)
```

**Time:** `O(n^3)`  
**Space:** `O(n^3)` in the worst case for the set; with `n <= 10`, this is very small.

---

# 8. LeetCode 3870 – Count Commas in Range

**Difficulty:** Easy  
**Pattern:** Math / Counting

## Problem Statement

Given an integer `n`, count the total number of commas used when writing every number from `1` to `n` using standard number formatting.

A comma is placed after every three digits from the right.

Numbers below `1000` have no commas.

## Input Format

```text
n = 1002
```

## Output Format

```text
3
```

## Constraints

- `1 <= n <= 10^5`

## Examples

```text
Input: 1002
Output: 3
```

The numbers:

```text
1,000
1,001
1,002
```

each contain one comma.

Another example:

```text
Input: 998
Output: 0
```

## Approach

Because `n <= 100000`:

- `1` to `999` → 0 commas
- `1000` to `n` → exactly 1 comma

Therefore, if:

```text
n >= 1000
```

the answer is:

```text
n - 1000 + 1
```

which simplifies to:

```text
n - 999
```

Otherwise the answer is `0`.

## Iteration / Dry Run

For `n = 1002`:

```text
1000 -> 1 comma
1001 -> 1 comma
1002 -> 1 comma
```

Total:

```text
3
```

Formula:

```text
1002 - 999 = 3
```

## Java Solution

```java
class Solution {
    public int countCommas(int n) {
        if (n < 1000) {
            return 0;
        }

        return n - 999;
    }
}
```

## Python Solution

```python
class Solution:
    def countCommas(self, n):
        if n < 1000:
            return 0

        return n - 999
```

**Time:** `O(1)`  
**Space:** `O(1)`

---

# 9. LeetCode 3871 – Count Commas in Range II

**Difficulty:** Medium  
**Pattern:** Math / Counting Powers

## Problem Statement

Given an integer `n`, count the total number of commas used when writing all integers from `1` through `n` using standard formatting.

Numbers gain another comma whenever they reach another group of three digits.

## Input Format

```text
n = 1002
```

## Output Format

```text
3
```

## Constraints

- `1 <= n <= 10^15`

## Examples

```text
Input: 1002
Output: 3

Input: 998
Output: 0
```

## Approach

Do not iterate from `1` to `n`, because `n` can be as large as `10^15`.

Think about comma positions:

```text
1000                  -> first comma
1,000,000             -> second comma
1,000,000,000         -> third comma
1,000,000,000,000     -> fourth comma
```

For every threshold `power`:

```text
power = 1000
power = 1000000
power = 1000000000
...
```

Every number from `power` to `n` contributes one comma for that particular comma position.

Therefore:

```text
answer += n - power + 1
```

Then multiply `power` by `1000`.

## Iteration / Dry Run

Take:

```text
n = 1,000,002
```

First comma:

```text
power = 1,000
numbers from 1,000 to 1,000,002
count = 999,003
```

Second comma:

```text
power = 1,000,000
numbers from 1,000,000 to 1,000,002
count = 3
```

Total:

```text
999,003 + 3 = 999,006
```

## Java Solution

Use `long` because `n` can be as large as `10^15`.

```java
class Solution {
    public long countCommas(long n) {
        long answer = 0;

        for (long power = 1000; power <= n; power *= 1000) {
            answer += n - power + 1;
        }

        return answer;
    }
}
```

## Python Solution

```python
class Solution:
    def countCommas(self, n):
        answer = 0
        power = 1000

        while power <= n:
            answer += n - power + 1
            power *= 1000

        return answer
```

**Time:** `O(log n)`  
**Space:** `O(1)`

---

# 10. LeetCode 1 – Two Sum

**Difficulty:** Easy  
**Pattern:** Hash Map

## Problem Statement

Given an integer array `nums` and an integer `target`, find the indices of two different elements whose sum equals `target`.

You may assume exactly one valid answer exists.

The same array element cannot be used twice.

## Input Format

```text
nums = [2,7,11,15]
target = 9
```

## Output Format

```text
[0,1]
```

## Constraints

- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- Exactly one valid answer exists.

## Examples

```text
Input:
nums = [2,7,11,15]
target = 9

Output:
[0,1]
```

Because:

```text
2 + 7 = 9
```

Another example:

```text
nums = [3,2,4]
target = 6

Output = [1,2]
```

## Approach – Hash Map

For every number:

```text
needed = target - current
```

Check whether `needed` was already seen.

If yes, we found the answer.

Otherwise store:

```text
number -> index
```

This reduces the brute-force `O(n²)` solution to `O(n)`.

## Iteration / Dry Run

For:

```text
nums = [2,7,11,15]
target = 9
```

### Step 1

```text
current = 2
needed = 9 - 2 = 7
```

`7` is not in the map.

Store:

```text
2 -> 0
```

### Step 2

```text
current = 7
needed = 9 - 7 = 2
```

`2` is already in the map at index `0`.

Answer:

```text
[0,1]
```

## Java Solution

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {
            int needed = target - nums[i];

            if (map.containsKey(needed)) {
                return new int[]{map.get(needed), i};
            }

            map.put(nums[i], i);
        }

        return new int[0];
    }
}
```

## Python Solution

```python
class Solution:
    def twoSum(self, nums, target):
        seen = {}

        for i, num in enumerate(nums):
            needed = target - num

            if needed in seen:
                return [seen[needed], i]

            seen[num] = i

        return []
```

**Time:** `O(n)` average  
**Space:** `O(n)`

---

# 11. LeetCode 191 – Number of 1 Bits

**Difficulty:** Easy  
**Pattern:** Bit Manipulation

## Problem Statement

Given an unsigned 32-bit integer, return the number of `1` bits in its binary representation.

This is also called the **Hamming weight**.

## Input Format

```text
n = 11
```

Binary representation:

```text
1011
```

## Output Format

```text
3
```

## Constraints

- The input is treated as a 32-bit unsigned integer.
- The number of `1` bits must be counted.

## Example

```text
Input:  11
Binary: 1011
Output: 3
```

There are three `1`s.

## Approach – Brian Kernighan's Algorithm

The important bit trick is:

```text
n & (n - 1)
```

This removes the **rightmost set bit** (`1`) from `n`.

Example:

```text
n     = 1011
n - 1 = 1010

1011
1010
----
1010
```

One `1` has been removed.

So repeatedly perform:

```text
n = n & (n - 1)
```

and count how many times it happens.

## Iteration / Dry Run

For:

```text
n = 11 = 1011
```

### Step 1

```text
1011 -> 1010
count = 1
```

### Step 2

```text
1010 -> 1000
count = 2
```

### Step 3

```text
1000 -> 0000
count = 3
```

Now `n = 0`.

**Answer = 3**

## Java Solution

```java
class Solution {
    public int hammingWeight(int n) {
        int count = 0;

        while (n != 0) {
            n = n & (n - 1);
            count++;
        }

        return count;
    }
}
```

## Python Solution

```python
class Solution:
    def hammingWeight(self, n):
        count = 0

        while n:
            n = n & (n - 1)
            count += 1

        return count
```

**Time:** `O(k)`, where `k` is the number of set bits; at most 32 iterations for a 32-bit value.  
**Space:** `O(1)`

---

# Quick Revision Table

| # | LeetCode | Problem | Difficulty | Main Pattern | Time | Space |
|---:|---:|---|---|---|---|---|
| 1 | 121 | Best Time to Buy and Sell Stock | Easy | Greedy | O(n) | O(1) |
| 2 | 53 | Maximum Subarray | Medium | Kadane / DP | O(n) | O(1) |
| 3 | 152 | Maximum Product Subarray | Medium | DP | O(n) | O(1) |
| 4 | 921 | Minimum Add to Make Parentheses Valid | Medium | Greedy | O(n) | O(1) |
| 5 | 856 | Score of Parentheses | Medium | Depth | O(n) | O(1) |
| 6 | 2078 | Two Furthest Houses With Different Colors | Easy | Greedy | O(n) | O(1) |
| 7 | 3483 | Unique 3-Digit Even Numbers | Easy | Enumeration + Set | O(n³) | O(n³) |
| 8 | 3870 | Count Commas in Range | Easy | Math | O(1) | O(1) |
| 9 | 3871 | Count Commas in Range II | Medium | Math | O(log n) | O(1) |
| 10 | 1 | Two Sum | Easy | Hash Map | O(n) | O(n) |
| 11 | 191 | Number of 1 Bits | Easy | Bit Manipulation | O(k) | O(1) |

---

# Important Coding Patterns for Exams

## 1. Hash Map

Use when you need:

```text
target - current
```

Classic example:

```text
LeetCode 1 – Two Sum
```

---

## 2. Kadane's Algorithm

Use when the question asks for:

```text
Maximum sum of a contiguous subarray
```

Classic:

```text
LeetCode 53
```

Basic formula:

```text
current = max(num, current + num)
```

---

## 3. Maximum Product

For product subarrays, maintain:

```text
maximum product
minimum product
```

because a negative value can turn the minimum into the maximum.

Classic:

```text
LeetCode 152
```

---

## 4. Greedy Minimum Tracking

If you need the best profit from buying before selling:

```text
keep minimum price so far
calculate today's profit
```

Classic:

```text
LeetCode 121
```

---

## 5. Parentheses

For parentheses problems, think about:

```text
open brackets
current depth
matching brackets
```

Examples:

```text
921 – Minimum Add to Make Parentheses Valid
856 – Score of Parentheses
```

---

## 6. Enumeration

When the input is extremely small, brute force can be the best solution.

For example, LeetCode 3483 has at most 10 digits, so trying all triples is completely practical.

---

## 7. Mathematical Thresholds

For number-formatting problems, look for points where the pattern changes.

For comma problems:

```text
1000
1000000
1000000000
1000000000000
...
```

This gives an `O(log n)` solution for LeetCode 3871.

---

## 8. Bit Manipulation

Remember this important trick:

```text
n & (n - 1)
```

It removes the rightmost `1` bit.

Useful for:

```text
LeetCode 191 – Number of 1 Bits
```

---

# Final Exam Strategy

Before coding, identify the pattern:

```text
Two numbers + target
        ↓
Hash Map

Maximum subarray sum
        ↓
Kadane

Maximum product
        ↓
Max + Min

Buy before Sell
        ↓
Minimum so far

Parentheses
        ↓
Open / Depth

Tiny input
        ↓
Brute Force / Enumeration

Huge number with repeated digit groups
        ↓
Math / Powers

Count 1 bits
        ↓
n & (n - 1)
```

These 11 problems cover several very common interview patterns and are good practice for coding assessments.
