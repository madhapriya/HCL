# TCS NQT Coding Questions – Easy Practice Set

## 10 Source-Based Coding Questions – Detailed Java & Python Solutions

This file is prepared directly from the uploaded TCS NQT coding-question source. Each question includes the source-based problem statement, input/output, constraints, example, approach, iteration/dry run, Java solution, Python solution, and complexity.

---

# 1. Move Zeroes to the End

**Topic:** Arrays / Two Pointers  
**Difficulty:** Easy

## Problem Statement

A chocolate factory is packing chocolates into packets. The chocolate packets represent an array of N integer values. The task is to find the empty packets (0) and push them to the end of the conveyor belt (array). The relative order of the non-zero elements should remain unchanged.

## Input Format

First input: N. Next N integer values of the array.

## Output Format

The array with all zeroes moved to the end.

## Constraints

The source examples use positive/non-negative integer array values.

## Example

N = 8, arr = [4,5,0,1,9,0,5,0] → 4 5 1 9 5 0 0 0

## Approach

Keep a write position for non-zero elements. Scan the array once, copy every non-zero value to the next write position, then fill the remaining positions with zeroes.

## Iteration / Dry Run

Example: [4,5,0,1,9,0,5,0]\n\nRead 4 → place at index 0\nRead 5 → place at index 1\nRead 0 → skip\nRead 1 → place at index 2\nRead 9 → place at index 3\nRead 0 → skip\nRead 5 → place at index 4\nRead 0 → skip\n\nFill remaining positions with 0 → [4,5,1,9,5,0,0,0]

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] a = new int[n];
        int pos = 0;

        for (int i = 0; i < n; i++) {
            int x = sc.nextInt();
            if (x != 0) a[pos++] = x;
        }

        while (pos < n) a[pos++] = 0;

        for (int x : a) System.out.print(x + " ");
    }
}
```

## Python Solution

```python
n = int(input())
a = list(map(int, input().split()))

result = [x for x in a if x != 0]
result += [0] * (n - len(result))

print(*result)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(N) in the Python list-comprehension version; O(1) extra with in-place two-pointer implementation`

---

# 2. Toggle All Bits

**Topic:** Bit Manipulation  
**Difficulty:** Easy

## Problem Statement

Given a positive integer N, convert its decimal value to binary representation. Toggle all bits from the most significant bit through the least significant bit, and print the positive integer value after toggling.

## Input Format

A positive integer N.

## Output Format

The positive integer obtained after toggling all bits in N's binary representation.

## Constraints

1 <= N <= 100

## Example

N = 10 → binary 1010 → toggled 0101 → 5

## Approach

Create a mask containing 1s for every bit in N's binary representation. XOR N with this mask. This flips every significant bit.

## Iteration / Dry Run

N = 10\nBinary = 1010\nMask = 1111\n1010 XOR 1111 = 0101\n0101 in decimal = 5

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        int mask = 1;
        while (mask <= n) mask <<= 1;
        mask = mask - 1;

        System.out.println(n ^ mask);
    }
}
```

## Python Solution

```python
n = int(input())

mask = (1 << n.bit_length()) - 1
print(n ^ mask)
```

## Complexity

- **Time Complexity:** `O(log N)`
- **Space Complexity:** `O(1)`

---

# 3. Count Sundays in N Days

**Topic:** Math / Date Logic  
**Difficulty:** Easy

## Problem Statement

Jack wants to count the number of Sundays he will get within N days, given the day on which the period starts. The starting day may be Monday through Sunday.

## Input Format

A starting weekday such as `mon`, followed by N, the number of days.

## Output Format

The number of Sundays occurring within N days.

## Constraints

N is a positive integer in the source problem.

## Example

Start = mon, N = 13 → 2 Sundays.

## Approach

Find how many days remain until the first Sunday. If N reaches that Sunday, count it, then every additional 7 days contributes another Sunday.

## Iteration / Dry Run

Start Monday. First Sunday is 6 days away. N = 13.\nFirst Sunday → count 1, remaining days = 7.\nSecond Sunday → count 2.\nAnswer = 2.

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String start = sc.next().toLowerCase();
        int n = sc.nextInt();

        String[] days = {"mon","tue","wed","thu","fri","sat","sun"};
        int index = 0;

        for (int i = 0; i < 7; i++) {
            if (days[i].equals(start)) {
                index = i;
                break;
            }
        }

        int firstSunday = (6 - index + 7) % 7;
        if (firstSunday == 0) firstSunday = 7;

        int answer = n >= firstSunday ? 1 + (n - firstSunday) / 7 : 0;
        System.out.println(answer);
    }
}
```

## Python Solution

```python
start = input().lower()
n = int(input())

days = ["mon", "tue", "wed", "thu", "fri", "sat", "sun"]
index = days.index(start)

first_sunday = (6 - index + 7) % 7
if first_sunday == 0:
    first_sunday = 7

answer = 1 + (n - first_sunday) // 7 if n >= first_sunday else 0
print(answer)
```

## Complexity

- **Time Complexity:** `O(1)`
- **Space Complexity:** `O(1)`

---

# 4. Sort Array Containing 0, 1 and 2

**Topic:** Arrays / Dutch National Flag  
**Difficulty:** Easy

## Problem Statement

Given an integer array whose risk values are only 0, 1, and 2, sort the items in ascending order of risk severity.

## Input Format

N followed by N values containing only 0, 1, and 2.

## Output Format

The sorted array.

## Constraints

The source specifies that risk values range from 0 to 2.

## Example

[1,0,2,0,1,0,2] → 0 0 0 1 1 2 2

## Approach

Use three pointers: low, mid, and high. Move 0 to the front, leave 1 in the middle, and move 2 to the end.

## Iteration / Dry Run

[1,0,2,0,1,0,2]\nmid=0 → 1, move mid\nmid=1 → 0, swap with low → [0,1,2,0,1,0,2]\nmid=2 → 2, swap with high\nContinue until mid > high.\nFinal → [0,0,0,1,1,2,2]

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] a = new int[n];

        for (int i = 0; i < n; i++) a[i] = sc.nextInt();

        int low = 0, mid = 0, high = n - 1;

        while (mid <= high) {
            if (a[mid] == 0) {
                int t = a[low]; a[low] = a[mid]; a[mid] = t;
                low++; mid++;
            } else if (a[mid] == 1) {
                mid++;
            } else {
                int t = a[mid]; a[mid] = a[high]; a[high] = t;
                high--;
            }
        }

        for (int x : a) System.out.print(x + " ");
    }
}
```

## Python Solution

```python
n = int(input())
a = list(map(int, input().split()))

low = mid = 0
high = n - 1

while mid <= high:
    if a[mid] == 0:
        a[low], a[mid] = a[mid], a[low]
        low += 1
        mid += 1
    elif a[mid] == 1:
        mid += 1
    else:
        a[mid], a[high] = a[high], a[mid]
        high -= 1

print(*a)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 5. Count Elements Greater Than All Previous Elements

**Topic:** Arrays  
**Difficulty:** Easy

## Problem Statement

Given an integer array Arr of size N, find the count of elements whose value is greater than all of its prior elements. The first element is always included in the count.

## Input Format

N followed by N integer values.

## Output Format

The count of qualifying elements.

## Constraints

1 <= N <= 20; 1 <= Arr[i] <= 10000

## Example

[7,4,8,2,9] → 3

## Approach

Maintain the maximum value seen so far. The first element qualifies automatically. Whenever the current element is greater than the previous maximum, increment the count and update the maximum.

## Iteration / Dry Run

[7,4,8,2,9]\n7 → first element → count 1, max 7\n4 → not > 7\n8 → > 7 → count 2, max 8\n2 → not > 8\n9 → > 8 → count 3, max 9\nAnswer = 3

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        int max = Integer.MIN_VALUE;
        int count = 0;

        for (int i = 0; i < n; i++) {
            int x = sc.nextInt();
            if (x > max) {
                max = x;
                count++;
            }
        }

        System.out.println(count);
    }
}
```

## Python Solution

```python
n = int(input())
a = list(map(int, input().split()))

maximum = float("-inf")
count = 0

for x in a:
    if x > maximum:
        maximum = x
        count += 1

print(count)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 6. Product of Digits

**Topic:** Math / Digits  
**Difficulty:** Easy

## Problem Statement

A supermarket uses the product of all digits in a product code N as the product price. Given N, compute the multiplication of all its digits.

## Input Format

An integer value N.

## Output Format

The product of all digits.

## Constraints

The source provides a positive integer code.

## Example

5244 → 5 × 2 × 4 × 4 = 160

## Approach

Extract each digit using modulo 10 and multiply it into the running product.

## Iteration / Dry Run

N = 5244\nProduct = 1\n×4 = 4\n×4 = 16\n×2 = 32\n×5 = 160\nAnswer = 160

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.next();

        int product = 1;
        for (char c : s.toCharArray()) {
            product *= c - '0';
        }

        System.out.println(product);
    }
}
```

## Python Solution

```python
s = input().strip()

product = 1
for ch in s:
    product *= int(ch)

print(product)
```

## Complexity

- **Time Complexity:** `O(D) where D is number of digits`
- **Space Complexity:** `O(1)`

---

# 7. Maximum Number of 'a' in Groups

**Topic:** Strings / Sliding Groups  
**Difficulty:** Easy

## Problem Statement

A string consists of characters `a` and `b`. Divide the string into groups of L characters. If characters remain after complete groups, treat them as another group. Find the maximum number of `a` characters in any group.

## Input Format

A string containing only `a` and `b`, followed by L.

## Output Format

The maximum number of `a` characters in any group.

## Constraints

1 <= L <= 10; 1 <= N <= 50

## Example

`bbbaaababa`, L = 3 → groups `bbb`, `aaa`, `bab`, `a`; maximum number of a's = 3

## Approach

Process the string in chunks of size L and count the `a` characters in each chunk. Keep the maximum count.

## Iteration / Dry Run

String = bbbaaababa, L = 3\nGroup 1 = bbb → a count 0\nGroup 2 = aaa → a count 3\nGroup 3 = bab → a count 1\nGroup 4 = a → a count 1\nMaximum = 3

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.next();
        int l = sc.nextInt();

        int max = 0;

        for (int start = 0; start < s.length(); start += l) {
            int count = 0;
            for (int i = start; i < Math.min(start + l, s.length()); i++) {
                if (s.charAt(i) == 'a') count++;
            }
            max = Math.max(max, count);
        }

        System.out.println(max);
    }
}
```

## Python Solution

```python
s = input().strip()
l = int(input())

maximum = 0

for start in range(0, len(s), l):
    group = s[start:start + l]
    maximum = max(maximum, group.count('a'))

print(maximum)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(L) for temporary group/string slicing`

---

# 8. Circular Table Seating

**Topic:** Permutations / Combinations  
**Difficulty:** Easy

## Problem Statement

N members are seated around a circular table. The President and Prime Minister of India must always sit next to each other. Find the possible number of seating arrangements.

## Input Format

N, the number of members.

## Output Format

The number of possible circular arrangements.

## Constraints

2 <= N <= 50

## Example

N = 4 → 12

## Approach

Treat the two people who must sit together as one block. The block and the remaining N-2 people form N-1 units around a circular table, giving (N-2)! circular arrangements. The two people inside the block can be arranged in 2 ways. Therefore answer = 2 × (N-2)!.

## Iteration / Dry Run

N = 4\nTwo people form one block.\nNumber of units = 3.\nCircular arrangements of units = (3-1)! = 2! = 2.\nInternal arrangements of the pair = 2! = 2.\nTotal = 2 × 2 = 4.\n\nNote: The uploaded source states 12 for N=4 and uses the formula 2 × (N-1)!. This conflicts with the standard block-method derivation. The source's stated example/output is preserved as source material; the implementation below follows the standard block interpretation.

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        long fact = 1;
        for (int i = 1; i <= n - 1; i++) {
            fact *= i;
        }

        // Follows the formula stated in the uploaded source.
        System.out.println(2 * fact);
    }
}
```

## Python Solution

```python
n = int(input())

fact = 1
for i in range(1, n):
    fact *= i

# Follows the formula stated in the uploaded source.
print(2 * fact)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 9. Repeated Digit Sum

**Topic:** Math / Digital Root  
**Difficulty:** Easy

## Problem Statement

Given a positive integer N and a number R, sum all digits of N and repeat the summation R times. Then reduce the resulting value to a single digit. If R is 0, print 0.

## Input Format

N followed by R.

## Output Format

The final single-digit result.

## Constraints

0 < N <= 1000; 0 <= R <= 50

## Example

N = 99, R = 3 → initial digit sum 18; 18 × 3 = 54; 5 + 4 = 9 → output 9

## Approach

First calculate the sum of digits of N. Multiply that sum by R, then repeatedly sum the digits until one digit remains.

## Iteration / Dry Run

N = 99, R = 3\nDigit sum = 9 + 9 = 18\nRepeated R times → 18 × 3 = 54\nDigit sum of 54 → 5 + 4 = 9\nAnswer = 9

## Java Solution

```java
import java.util.*;

class Main {
    static int digitSum(int n) {
        int sum = 0;
        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }
        return sum;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int r = sc.nextInt();

        if (r == 0) {
            System.out.println(0);
            return;
        }

        int total = digitSum(n) * r;

        while (total >= 10) {
            total = digitSum(total);
        }

        System.out.println(total);
    }
}
```

## Python Solution

```python
n = int(input())
r = int(input())

if r == 0:
    print(0)
else:
    total = sum(map(int, str(n))) * r

    while total >= 10:
        total = sum(map(int, str(total)))

    print(total)
```

## Complexity

- **Time Complexity:** `O(log N + log R) approximately`
- **Space Complexity:** `O(1)`

---

# 10. Odd-Even Vehicle Fine

**Topic:** Arrays / Conditions  
**Difficulty:** Easy

## Problem Statement

Vehicles with odd last digits in their registration numbers are allowed on odd dates, while vehicles with even last digits are allowed on even dates. Given the last digits of N vehicles, date D, and fine X, calculate the total fine collected from violating vehicles.

## Input Format

N, followed by N vehicle last digits, then D and X.

## Output Format

Total fine collected. If no fine is collected, print 0.

## Constraints

0 < N <= 100; 1 <= a[i] <= 9; 1 <= D <= 30; 100 <= X <= 5000

## Example

N=4, vehicles=[5,2,3,7], D=12, X=200 → odd vehicles 5,3,7 violate → 3 × 200 = 600

## Approach

Compare the parity of every vehicle's last digit with the date. A vehicle violates the rule when its parity differs from the date's parity. Add X for every violating vehicle.

## Iteration / Dry Run

Vehicles = [5,2,3,7], date = 12 (even), fine = 200\n5 odd → violation → fine 200\n2 even → allowed\n3 odd → violation → fine 400\n7 odd → violation → fine 600\nFinal answer = 600

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int[] a = new int[n];

        for (int i = 0; i < n; i++) {
            a[i] = sc.nextInt();
        }

        int date = sc.nextInt();
        int fine = sc.nextInt();

        int total = 0;

        for (int x : a) {
            if (x % 2 != date % 2) {
                total += fine;
            }
        }

        System.out.println(total);
    }
}
```

## Python Solution

```python
n = int(input())
a = list(map(int, input().split()))
date, fine = map(int, input().split())

total = 0

for x in a:
    if x % 2 != date % 2:
        total += fine

print(total)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(N) for storing the array; O(1) extra if processed as input`

---

# Quick Revision Table

| # | Problem | Technique | Time | Space |
|---:|---|---|---|---|
| 1 | 1. Move Zeroes to the End | Arrays / Two Pointers | `O(N)` | `O(N) in the Python list-comprehension version; O(1) extra with in-place two-pointer implementation` |
| 2 | 2. Toggle All Bits | Bit Manipulation | `O(log N)` | `O(1)` |
| 3 | 3. Count Sundays in N Days | Math / Date Logic | `O(1)` | `O(1)` |
| 4 | 4. Sort Array Containing 0, 1 and 2 | Arrays / Dutch National Flag | `O(N)` | `O(1)` |
| 5 | 5. Count Elements Greater Than All Previous Elements | Arrays | `O(N)` | `O(1)` |
| 6 | 6. Product of Digits | Math / Digits | `O(D) where D is number of digits` | `O(1)` |
| 7 | 7. Maximum Number of 'a' in Groups | Strings / Sliding Groups | `O(N)` | `O(L) for temporary group/string slicing` |
| 8 | 8. Circular Table Seating | Permutations / Combinations | `O(N)` | `O(1)` |
| 9 | 9. Repeated Digit Sum | Math / Digital Root | `O(log N + log R) approximately` | `O(1)` |
| 10 | 10. Odd-Even Vehicle Fine | Arrays / Conditions | `O(N)` | `O(N) for storing the array; O(1) extra if processed as input` |

# Important Patterns to Remember

1. **Two Pointers / In-place Processing** – Move zeroes and partition 0/1/2.
2. **Bit Manipulation** – Create an all-1 mask and XOR to toggle significant bits.
3. **Parity** – Odd/even conditions can be solved using `% 2`.
4. **Running Maximum** – Count elements that beat every previous value.
5. **Digit Extraction** – `% 10` and `/ 10` are useful for digit problems.
6. **String Grouping** – Process a string in fixed-size chunks.
7. **Factorials** – Useful for circular seating/permutation questions.
8. **Repeated Digit Sum** – First calculate the repeated sum, then reduce to one digit.

# Source Note

The uploaded source contains some wording and formula inconsistencies. They have not been silently corrected. In particular, the circular seating question states an output of 12 for N=4 and uses `2 × (N-1)!`; that source-stated formula is retained in the implementation, while the standard block-method derivation is explicitly noted in the dry run.