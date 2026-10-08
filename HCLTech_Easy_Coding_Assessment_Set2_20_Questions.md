# HCLTech Coding Assessment – Easy Level Set 2

## 20 Easy Coding Questions – Java & Python

This set is designed for **beginner-friendly HCLTech coding practice**. Each problem includes the full problem statement, input/output details, constraints, example, approach, iteration/dry run, Java solution, Python solution, and complexity analysis.

---

# 1. Find the Largest Element in an Array

**Topic:** Arrays  
**Difficulty:** Easy

## Problem Statement

Given an array of integers, find and print the largest element in the array.

## Input Format

An integer array.

## Output Format

The largest element.

## Constraints

1 <= N <= 10^5; -10^9 <= A[i] <= 10^9.

## Example

[10, 5, 20, 8, 15] → 20

## Approach

Start with the first element as the maximum. Scan the remaining elements and update the maximum whenever a larger value is found.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: [10, 5, 20, 8, 15]

| Step | Current Element | Maximum |
|---|---:|---:|
| Start | 10 | 10 |
| 1 | 5 | 10 |
| 2 | 20 | 20 |
| 3 | 8 | 20 |
| 4 | 15 | 20 |

Final answer = 20

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        int[] a = {10, 5, 20, 8, 15};
        int max = a[0];

        for (int i = 1; i < a.length; i++) {
            if (a[i] > max) max = a[i];
        }

        System.out.println(max);
    }
}
```

## Python Solution

```python
a = [10, 5, 20, 8, 15]
maximum = a[0]

for x in a[1:]:
    if x > maximum:
        maximum = x

print(maximum)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 2. Find the Smallest Element in an Array

**Topic:** Arrays  
**Difficulty:** Easy

## Problem Statement

Given an array of integers, find and print the smallest element.

## Input Format

An integer array.

## Output Format

The smallest element.

## Constraints

1 <= N <= 10^5.

## Example

[7, 3, 9, 2, 6] → 2

## Approach

Initialize the minimum with the first element and scan the array, updating it whenever a smaller value is found.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: [7, 3, 9, 2, 6]

| Element | Minimum |
|---:|---:|
| 7 | 7 |
| 3 | 3 |
| 9 | 3 |
| 2 | 2 |
| 6 | 2 |

Final answer = 2

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int[] a = {7, 3, 9, 2, 6};
        int min = a[0];

        for (int i = 1; i < a.length; i++) {
            if (a[i] < min) min = a[i];
        }

        System.out.println(min);
    }
}
```

## Python Solution

```python
a = [7, 3, 9, 2, 6]
minimum = a[0]

for x in a[1:]:
    if x < minimum:
        minimum = x

print(minimum)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 3. Sum of Array Elements

**Topic:** Arrays  
**Difficulty:** Easy

## Problem Statement

Given an array of integers, calculate the sum of all elements.

## Input Format

An integer array.

## Output Format

The sum of all elements.

## Constraints

1 <= N <= 10^5.

## Example

[1, 2, 3, 4, 5] → 15

## Approach

Initialize sum as 0 and add every array element to it.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: [1, 2, 3, 4, 5]

sum = 0
→ 0 + 1 = 1
→ 1 + 2 = 3
→ 3 + 3 = 6
→ 6 + 4 = 10
→ 10 + 5 = 15

Final answer = 15

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 5};
        int sum = 0;

        for (int x : a) {
            sum += x;
        }

        System.out.println(sum);
    }
}
```

## Python Solution

```python
a = [1, 2, 3, 4, 5]
total = 0

for x in a:
    total += x

print(total)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 4. Count Even and Odd Numbers

**Topic:** Arrays  
**Difficulty:** Easy

## Problem Statement

Given an array of integers, count how many elements are even and how many are odd.

## Input Format

An integer array.

## Output Format

Two counts: even and odd.

## Constraints

1 <= N <= 10^5.

## Example

[1, 2, 3, 4, 6] → Even = 3, Odd = 2

## Approach

For each number, check `number % 2`. If it is 0, increment the even count; otherwise increment the odd count.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: [1, 2, 3, 4, 6]

| Number | Type | Even | Odd |
|---:|---|---:|---:|
| 1 | Odd | 0 | 1 |
| 2 | Even | 1 | 1 |
| 3 | Odd | 1 | 2 |
| 4 | Even | 2 | 2 |
| 6 | Even | 3 | 2 |

Final answer: Even = 3, Odd = 2

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 6};
        int even = 0, odd = 0;

        for (int x : a) {
            if (x % 2 == 0) even++;
            else odd++;
        }

        System.out.println("Even = " + even);
        System.out.println("Odd = " + odd);
    }
}
```

## Python Solution

```python
a = [1, 2, 3, 4, 6]
even = 0
odd = 0

for x in a:
    if x % 2 == 0:
        even += 1
    else:
        odd += 1

print("Even =", even)
print("Odd =", odd)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 5. Reverse an Array

**Topic:** Arrays  
**Difficulty:** Easy

## Problem Statement

Given an array, print its elements in reverse order.

## Input Format

An integer array.

## Output Format

The reversed array.

## Constraints

1 <= N <= 10^5.

## Example

[1, 2, 3, 4, 5] → [5, 4, 3, 2, 1]

## Approach

Use two pointers: one at the beginning and one at the end. Swap the elements and move both pointers toward the center.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: [1, 2, 3, 4, 5]

| Left | Right | Array after swap |
|---:|---:|---|
| 0 | 4 | [5,2,3,4,1] |
| 1 | 3 | [5,4,3,2,1] |
| 2 | 2 | Stop |

Final array = [5,4,3,2,1]

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        int[] a = {1, 2, 3, 4, 5};
        int left = 0, right = a.length - 1;

        while (left < right) {
            int temp = a[left];
            a[left] = a[right];
            a[right] = temp;
            left++;
            right--;
        }

        System.out.println(Arrays.toString(a));
    }
}
```

## Python Solution

```python
a = [1, 2, 3, 4, 5]
left, right = 0, len(a) - 1

while left < right:
    a[left], a[right] = a[right], a[left]
    left += 1
    right -= 1

print(a)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 6. Check if a Number is Prime

**Topic:** Number Theory  
**Difficulty:** Easy

## Problem Statement

Given an integer N, determine whether it is a prime number.

## Input Format

An integer N.

## Output Format

Print `Prime` or `Not Prime`.

## Constraints

2 <= N <= 10^9.

## Example

17 → Prime; 18 → Not Prime

## Approach

A prime number has exactly two factors. Check divisibility from 2 up to the square root of N. If any number divides N, it is not prime.

**Complexity:**
- Time: `O(√N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: N = 17

Check:
2 → 17 % 2 ≠ 0
3 → 17 % 3 ≠ 0
4 → 17 % 4 ≠ 0

Since no divisor is found up to √17, 17 is prime.

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int n = 17;
        boolean prime = n >= 2;

        for (int i = 2; i * i <= n && prime; i++) {
            if (n % i == 0) prime = false;
        }

        System.out.println(prime ? "Prime" : "Not Prime");
    }
}
```

## Python Solution

```python
n = 17
prime = n >= 2

i = 2
while i * i <= n:
    if n % i == 0:
        prime = False
        break
    i += 1

print("Prime" if prime else "Not Prime")
```

## Complexity

- **Time Complexity:** `O(√N)`
- **Space Complexity:** `O(1)`

---

# 7. Reverse a Number

**Topic:** Math  
**Difficulty:** Easy

## Problem Statement

Given an integer, reverse its digits and print the reversed number.

## Input Format

An integer N.

## Output Format

The reversed integer.

## Constraints

0 <= N <= 10^9.

## Example

12340 → 4321

## Approach

Repeatedly take the last digit using `% 10`, add it to the reversed number, and remove the last digit using integer division by 10.

**Complexity:**
- Time: `O(D) where D is number of digits`
- Space: `O(1)`

## Iteration / Dry Run

Example: N = 123

| N | Digit | Reverse |
|---:|---:|---:|
| 123 | 3 | 3 |
| 12 | 2 | 32 |
| 1 | 1 | 321 |
| 0 | - | 321 |

Final answer = 321

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int n = 123;
        int reverse = 0;

        while (n > 0) {
            int digit = n % 10;
            reverse = reverse * 10 + digit;
            n /= 10;
        }

        System.out.println(reverse);
    }
}
```

## Python Solution

```python
n = 123
reverse = 0

while n > 0:
    digit = n % 10
    reverse = reverse * 10 + digit
    n //= 10

print(reverse)
```

## Complexity

- **Time Complexity:** `O(D) where D is number of digits`
- **Space Complexity:** `O(1)`

---

# 8. Check Palindrome Number

**Topic:** Math  
**Difficulty:** Easy

## Problem Statement

Given an integer, determine whether it reads the same forward and backward.

## Input Format

An integer N.

## Output Format

Print `Palindrome` or `Not Palindrome`.

## Constraints

0 <= N <= 10^9.

## Example

121 → Palindrome; 123 → Not Palindrome

## Approach

Store the original number, reverse the number, and compare the reversed number with the original.

**Complexity:**
- Time: `O(D)`
- Space: `O(1)`

## Iteration / Dry Run

Example: N = 121

Reverse:
1 → 1
12 → 12
121 → 121

Original = 121
Reverse = 121

Therefore, it is a palindrome.

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int n = 121;
        int original = n;
        int reverse = 0;

        while (n > 0) {
            reverse = reverse * 10 + n % 10;
            n /= 10;
        }

        System.out.println(original == reverse ? "Palindrome" : "Not Palindrome");
    }
}
```

## Python Solution

```python
n = 121
original = n
reverse = 0

while n > 0:
    reverse = reverse * 10 + n % 10
    n //= 10

print("Palindrome" if original == reverse else "Not Palindrome")
```

## Complexity

- **Time Complexity:** `O(D)`
- **Space Complexity:** `O(1)`

---

# 9. Factorial of a Number

**Topic:** Math  
**Difficulty:** Easy

## Problem Statement

Given a non-negative integer N, calculate N!.

## Input Format

An integer N.

## Output Format

The factorial of N.

## Constraints

0 <= N <= 12.

## Example

5 → 120

## Approach

Start with result = 1 and multiply it by every integer from 1 to N.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: 5!

result = 1
→ 1 × 1 = 1
→ 1 × 2 = 2
→ 2 × 3 = 6
→ 6 × 4 = 24
→ 24 × 5 = 120

Final answer = 120

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int n = 5;
        long fact = 1;

        for (int i = 1; i <= n; i++) {
            fact *= i;
        }

        System.out.println(fact);
    }
}
```

## Python Solution

```python
n = 5
fact = 1

for i in range(1, n + 1):
    fact *= i

print(fact)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 10. Fibonacci Number

**Topic:** Recursion / Iteration  
**Difficulty:** Easy

## Problem Statement

Given N, print the Nth Fibonacci number. Use the sequence 0, 1, 1, 2, 3, 5, ...

## Input Format

An integer N.

## Output Format

The Nth Fibonacci number.

## Constraints

0 <= N <= 30.

## Example

6 → 8

## Approach

Use two variables to store the previous two Fibonacci numbers. Repeatedly calculate the next value.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: N = 6

Fibonacci sequence:
0, 1, 1, 2, 3, 5, 8

So F(6) = 8.

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int n = 6;
        int a = 0, b = 1;

        for (int i = 0; i < n; i++) {
            int next = a + b;
            a = b;
            b = next;
        }

        System.out.println(a);
    }
}
```

## Python Solution

```python
n = 6
a, b = 0, 1

for _ in range(n):
    a, b = b, a + b

print(a)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 11. Count Digits in a Number

**Topic:** Math  
**Difficulty:** Easy

## Problem Statement

Given an integer N, count how many digits it contains.

## Input Format

An integer N.

## Output Format

Number of digits.

## Constraints

0 <= N <= 10^18.

## Example

12345 → 5

## Approach

Repeatedly divide the number by 10 until it becomes 0. Count how many divisions are performed. Handle 0 as one digit.

**Complexity:**
- Time: `O(D)`
- Space: `O(1)`

## Iteration / Dry Run

Example: 12345

12345 → 1234 → 123 → 12 → 1 → 0

Number of divisions = 5

Final answer = 5

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        long n = 12345;
        int count = 0;

        if (n == 0) count = 1;
        while (n > 0) {
            count++;
            n /= 10;
        }

        System.out.println(count);
    }
}
```

## Python Solution

```python
n = 12345
count = 1 if n == 0 else 0

while n > 0:
    count += 1
    n //= 10

print(count)
```

## Complexity

- **Time Complexity:** `O(D)`
- **Space Complexity:** `O(1)`

---

# 12. Sum of Digits

**Topic:** Math  
**Difficulty:** Easy

## Problem Statement

Given an integer N, calculate the sum of all its digits.

## Input Format

An integer N.

## Output Format

Sum of digits.

## Constraints

0 <= N <= 10^18.

## Example

1234 → 10

## Approach

Extract the last digit using `% 10`, add it to the sum, and remove it using `/ 10`.

**Complexity:**
- Time: `O(D)`
- Space: `O(1)`

## Iteration / Dry Run

Example: 1234

4 → sum = 4
3 → sum = 7
2 → sum = 9
1 → sum = 10

Final answer = 10

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        long n = 1234;
        long sum = 0;

        while (n > 0) {
            sum += n % 10;
            n /= 10;
        }

        System.out.println(sum);
    }
}
```

## Python Solution

```python
n = 1234
total = 0

while n > 0:
    total += n % 10
    n //= 10

print(total)
```

## Complexity

- **Time Complexity:** `O(D)`
- **Space Complexity:** `O(1)`

---

# 13. Check Anagram Strings

**Topic:** Strings  
**Difficulty:** Easy

## Problem Statement

Given two strings, determine whether they contain the same characters with the same frequencies.

## Input Format

Two strings.

## Output Format

Print `Anagram` or `Not Anagram`.

## Constraints

1 <= length <= 10^5.

## Example

listen, silent → Anagram

## Approach

If the strings have different lengths, they cannot be anagrams. Otherwise, count the frequency of each character in both strings and compare.

**Complexity:**
- Time: `O(N log N)`
- Space: `O(N)`

## Iteration / Dry Run

Example: `listen` and `silent`

Both contain:
l:1, i:1, s:1, t:1, e:1, n:1

All frequencies match.

Final answer = Anagram

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        String s1 = "listen";
        String s2 = "silent";

        char[] a = s1.toCharArray();
        char[] b = s2.toCharArray();

        Arrays.sort(a);
        Arrays.sort(b);

        System.out.println(Arrays.equals(a, b) ? "Anagram" : "Not Anagram");
    }
}
```

## Python Solution

```python
s1 = "listen"
s2 = "silent"

print("Anagram" if sorted(s1) == sorted(s2) else "Not Anagram")
```

## Complexity

- **Time Complexity:** `O(N log N)`
- **Space Complexity:** `O(N)`

---

# 14. Count Vowels in a String

**Topic:** Strings  
**Difficulty:** Easy

## Problem Statement

Given a string, count the number of vowels (a, e, i, o, u) in it.

## Input Format

A string.

## Output Format

The number of vowels.

## Constraints

1 <= length <= 10^5.

## Example

hello world → 3

## Approach

Traverse each character and check whether it belongs to the set of vowels.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: `hello world`

h → no
e → vowel (1)
l → no
l → no
o → vowel (2)
space → no
w → no
o → vowel (3)

Final answer = 3

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        String s = "hello world";
        int count = 0;

        for (char c : s.toLowerCase().toCharArray()) {
            if ("aeiou".indexOf(c) != -1) {
                count++;
            }
        }

        System.out.println(count);
    }
}
```

## Python Solution

```python
s = "hello world"
count = 0

for ch in s.lower():
    if ch in "aeiou":
        count += 1

print(count)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 15. Reverse a String

**Topic:** Strings  
**Difficulty:** Easy

## Problem Statement

Given a string, print the string in reverse order.

## Input Format

A string.

## Output Format

The reversed string.

## Constraints

1 <= length <= 10^5.

## Example

hello → olleh

## Approach

Use two pointers or traverse the string from the last character to the first.

**Complexity:**
- Time: `O(N)`
- Space: `O(N)`

## Iteration / Dry Run

Example: `hello`

Read from right to left:
o → ol
l → oll
l → oll e? 
Correct sequence: o, l, l, e, h

Final answer = `olleh`

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        String s = "hello";
        StringBuilder result = new StringBuilder();

        for (int i = s.length() - 1; i >= 0; i--) {
            result.append(s.charAt(i));
        }

        System.out.println(result);
    }
}
```

## Python Solution

```python
s = "hello"
print(s[::-1])
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(N)`

---

# 16. Find the Frequency of a Character

**Topic:** Strings / Hashing  
**Difficulty:** Easy

## Problem Statement

Given a string and a character, count how many times the character occurs in the string.

## Input Format

A string and a target character.

## Output Format

The frequency of the target character.

## Constraints

1 <= length <= 10^5.

## Example

banana, a → 3

## Approach

Traverse the string and increment a counter whenever the current character equals the target character.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: `banana`, target = `a`

b → no
a → count = 1
n → no
a → count = 2
n → no
a → count = 3

Final answer = 3

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        String s = "banana";
        char target = 'a';
        int count = 0;

        for (char c : s.toCharArray()) {
            if (c == target) count++;
        }

        System.out.println(count);
    }
}
```

## Python Solution

```python
s = "banana"
target = "a"
count = 0

for ch in s:
    if ch == target:
        count += 1

print(count)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 17. Remove Duplicates from a Sorted Array

**Topic:** Arrays  
**Difficulty:** Easy

## Problem Statement

Given a sorted array, remove duplicate values so that each value appears only once.

## Input Format

A sorted integer array.

## Output Format

The unique elements.

## Constraints

1 <= N <= 10^5.

## Example

[1, 1, 2, 2, 3, 4, 4] → [1, 2, 3, 4]

## Approach

Use a write pointer. Whenever a new value different from the previous unique value is found, place it at the next write position.

**Complexity:**
- Time: `O(N)`
- Space: `O(1) extra for Java two-pointer approach`

## Iteration / Dry Run

Example: [1,1,2,2,3]

Start: [1]
Second 1 → duplicate, skip
2 → write → [1,2]
Second 2 → skip
3 → write → [1,2,3]

Final unique array = [1,2,3]

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        int[] a = {1, 1, 2, 2, 3, 4, 4};
        int k = 1;

        for (int i = 1; i < a.length; i++) {
            if (a[i] != a[k - 1]) {
                a[k] = a[i];
                k++;
            }
        }

        System.out.println(Arrays.toString(Arrays.copyOf(a, k)));
    }
}
```

## Python Solution

```python
a = [1, 1, 2, 2, 3, 4, 4]
unique = []

for x in a:
    if not unique or unique[-1] != x:
        unique.append(x)

print(unique)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1) extra for Java two-pointer approach`

---

# 18. Find the Second Largest Element

**Topic:** Arrays  
**Difficulty:** Easy

## Problem Statement

Given an array of integers, find the second largest distinct element.

## Input Format

An integer array.

## Output Format

The second largest distinct element.

## Constraints

2 <= N <= 10^5; a second distinct value exists.

## Example

[10, 5, 20, 8, 20] → 10

## Approach

Maintain the largest and second-largest distinct values while scanning the array once.

**Complexity:**
- Time: `O(N)`
- Space: `O(1)`

## Iteration / Dry Run

Example: [10, 5, 20, 8, 20]

10 → largest=10
5 → second=5
20 → largest=20, second=10
8 → no change
20 → duplicate of largest, ignore

Final answer = 10

## Java Solution

```java
class Main {
    public static void main(String[] args) {
        int[] a = {10, 5, 20, 8, 20};
        int largest = Integer.MIN_VALUE;
        int second = Integer.MIN_VALUE;

        for (int x : a) {
            if (x > largest) {
                second = largest;
                largest = x;
            } else if (x > second && x != largest) {
                second = x;
            }
        }

        System.out.println(second);
    }
}
```

## Python Solution

```python
a = [10, 5, 20, 8, 20]
largest = float("-inf")
second = float("-inf")

for x in a:
    if x > largest:
        second = largest
        largest = x
    elif largest > x > second:
        second = x

print(second)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1)`

---

# 19. Two Sum

**Topic:** Arrays / Hashing  
**Difficulty:** Easy

## Problem Statement

Given an array and a target value, find two elements whose sum equals the target. Return their indices.

## Input Format

An integer array and target.

## Output Format

Indices of two elements whose sum is the target.

## Constraints

2 <= N <= 10^5.

## Example

[2,7,11,15], target=9 → [0,1]

## Approach

Store previously seen values in a hash map. For each value x, check whether target - x has already been seen.

**Complexity:**
- Time: `O(N)`
- Space: `O(N)`

## Iteration / Dry Run

Example: [2,7,11,15], target = 9

x = 2 → need 7 → not found → store 2
x = 7 → need 2 → found at index 0

Answer = [0,1]

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        int[] a = {2, 7, 11, 15};
        int target = 9;
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < a.length; i++) {
            int need = target - a[i];

            if (map.containsKey(need)) {
                System.out.println(map.get(need) + " " + i);
                return;
            }

            map.put(a[i], i);
        }
    }
}
```

## Python Solution

```python
a = [2, 7, 11, 15]
target = 9
seen = {}

for i, x in enumerate(a):
    need = target - x

    if need in seen:
        print(seen[need], i)
        break

    seen[x] = i
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(N)`

---

# 20. Move All Zeroes to the End

**Topic:** Arrays / Two Pointers  
**Difficulty:** Easy

## Problem Statement

Given an array, move all zeroes to the end while keeping the relative order of non-zero elements unchanged.

## Input Format

An integer array.

## Output Format

The modified array.

## Constraints

1 <= N <= 10^5.

## Example

[0,1,0,3,12] → [1,3,12,0,0]

## Approach

Keep a position for the next non-zero element. First place all non-zero values at the front, then fill the remaining positions with zeroes.

**Complexity:**
- Time: `O(N)`
- Space: `O(1) extra`

## Iteration / Dry Run

Example: [0,1,0,3,12]

Read 0 → skip
Read 1 → place at position 0 → [1,...]
Read 0 → skip
Read 3 → place at position 1 → [1,3,...]
Read 12 → place at position 2 → [1,3,12,...]

Fill remaining positions with 0:
[1,3,12,0,0]

## Java Solution

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        int[] a = {0, 1, 0, 3, 12};
        int pos = 0;

        for (int x : a) {
            if (x != 0) {
                a[pos++] = x;
            }
        }

        while (pos < a.length) {
            a[pos++] = 0;
        }

        System.out.println(Arrays.toString(a));
    }
}
```

## Python Solution

```python
a = [0, 1, 0, 3, 12]
pos = 0

for x in a:
    if x != 0:
        a[pos] = x
        pos += 1

while pos < len(a):
    a[pos] = 0
    pos += 1

print(a)
```

## Complexity

- **Time Complexity:** `O(N)`
- **Space Complexity:** `O(1) extra`

---

# Quick Revision Table

| # | Problem | Main Technique | Time | Space |
|---:|---|---|---|---|
| 1 | 1. Find the Largest Element in an Array | Arrays | `O(N)` | `O(1)` |
| 2 | 2. Find the Smallest Element in an Array | Arrays | `O(N)` | `O(1)` |
| 3 | 3. Sum of Array Elements | Arrays | `O(N)` | `O(1)` |
| 4 | 4. Count Even and Odd Numbers | Arrays | `O(N)` | `O(1)` |
| 5 | 5. Reverse an Array | Arrays | `O(N)` | `O(1)` |
| 6 | 6. Check if a Number is Prime | Number Theory | `O(√N)` | `O(1)` |
| 7 | 7. Reverse a Number | Math | `O(D) where D is number of digits` | `O(1)` |
| 8 | 8. Check Palindrome Number | Math | `O(D)` | `O(1)` |
| 9 | 9. Factorial of a Number | Math | `O(N)` | `O(1)` |
| 10 | 10. Fibonacci Number | Recursion / Iteration | `O(N)` | `O(1)` |
| 11 | 11. Count Digits in a Number | Math | `O(D)` | `O(1)` |
| 12 | 12. Sum of Digits | Math | `O(D)` | `O(1)` |
| 13 | 13. Check Anagram Strings | Strings | `O(N log N)` | `O(N)` |
| 14 | 14. Count Vowels in a String | Strings | `O(N)` | `O(1)` |
| 15 | 15. Reverse a String | Strings | `O(N)` | `O(N)` |
| 16 | 16. Find the Frequency of a Character | Strings / Hashing | `O(N)` | `O(1)` |
| 17 | 17. Remove Duplicates from a Sorted Array | Arrays | `O(N)` | `O(1) extra for Java two-pointer approach` |
| 18 | 18. Find the Second Largest Element | Arrays | `O(N)` | `O(1)` |
| 19 | 19. Two Sum | Arrays / Hashing | `O(N)` | `O(N)` |
| 20 | 20. Move All Zeroes to the End | Arrays / Two Pointers | `O(N)` | `O(1) extra` |

# Important Easy-Level Patterns

1. **Array Traversal** – largest, smallest, sum, counting.
2. **Two Pointers** – reversing arrays and moving zeroes.
3. **Basic Mathematics** – prime, factorial, Fibonacci, digits.
4. **String Traversal** – reverse, vowels, character frequency.
5. **Hashing** – anagrams and Two Sum.
6. **In-place Array Processing** – remove duplicates and move zeroes.
7. **Single-Pass Optimization** – second largest and other O(N) problems.

# Exam Tip

For easy coding questions, first identify the pattern, write the simplest correct solution, then check edge cases such as an empty/one-element array, zero, duplicates, and negative values where applicable.