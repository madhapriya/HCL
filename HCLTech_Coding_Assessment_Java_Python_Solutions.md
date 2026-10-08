# HCLTech Coding Assessment - Easy Java & Python Solutions

Here is the full solution guide for all 15 HCLTech coding assessment problems.

Each problem includes an easy-to-understand **Java solution** and **Python solution**, along with the approach and time/space complexity.

---

# 1. Longest Substring with At Most K Distinct Characters

Given a string and an integer `K`, find the length of the longest substring containing at most `K` distinct characters.

---

## Java - Sliding Window Approach

This approach uses a sliding window and a `HashMap` to store the frequency of each character.

**Complexity:** Time O(n), Space O(k)

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String s = sc.nextLine();
        int k = sc.nextInt();

        HashMap<Character, Integer> map = new HashMap<>();

        int left = 0;
        int maxLength = 0;

        for (int right = 0; right < s.length(); right++) {
            char ch = s.charAt(right);

            map.put(ch, map.getOrDefault(ch, 0) + 1);

            while (map.size() > k) {
                char leftChar = s.charAt(left);

                map.put(leftChar, map.get(leftChar) - 1);

                if (map.get(leftChar) == 0) {
                    map.remove(leftChar);
                }

                left++;
            }

            maxLength = Math.max(maxLength, right - left + 1);
        }

        System.out.println(maxLength);
    }
}
```

## Python - Sliding Window Approach

This is the same sliding-window logic using a Python dictionary.

**Complexity:** Time O(n), Space O(k)

```python
s = input()
k = int(input())

count = {}

left = 0
max_length = 0

for right in range(len(s)):
    ch = s[right]

    count[ch] = count.get(ch, 0) + 1

    while len(count) > k:
        left_ch = s[left]

        count[left_ch] -= 1

        if count[left_ch] == 0:
            del count[left_ch]

        left += 1

    max_length = max(max_length, right - left + 1)

print(max_length)
```

---

# 2. Minimum Platforms Required

Given arrival and departure times of trains, find the minimum number of platforms required so that no train has to wait.

If an arrival time is equal to a departure time, a separate platform is required.

---

## Java - Sorting and Two Pointers

Sort arrivals and departures separately and process them using two pointers.

**Complexity:** Time O(n log n), Space O(n)

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
        int maxPlatforms = 0;

        while (i < n) {
            if (arrival[i] <= departure[j]) {
                current++;
                maxPlatforms = Math.max(maxPlatforms, current);
                i++;
            } else {
                current--;
                j++;
            }
        }

        System.out.println(maxPlatforms);
    }
}
```

## Python - Sorting and Two Pointers

Sort both arrays and compare the next arrival with the next departure.

**Complexity:** Time O(n log n), Space O(n)

```python
n = int(input())

arrival = list(map(int, input().split()))
departure = list(map(int, input().split()))

arrival.sort()
departure.sort()

i = 0
j = 0

current = 0
max_platforms = 0

while i < n:
    if arrival[i] <= departure[j]:
        current += 1
        max_platforms = max(max_platforms, current)
        i += 1
    else:
        current -= 1
        j += 1

print(max_platforms)
```

---

# 3. Maximum Product Subarray

Given an array containing positive numbers, negative numbers and zeroes, find the contiguous subarray having the maximum product.

---

## Java - Track Maximum and Minimum Product

We maintain both maximum and minimum products because a negative number can turn the minimum product into the maximum.

**Complexity:** Time O(n), Space O(1)

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
        int answer = a[0];

        for (int i = 1; i < n; i++) {

            if (a[i] < 0) {
                int temp = maxProduct;
                maxProduct = minProduct;
                minProduct = temp;
            }

            maxProduct = Math.max(a[i], maxProduct * a[i]);
            minProduct = Math.min(a[i], minProduct * a[i]);

            answer = Math.max(answer, maxProduct);
        }

        System.out.println(answer);
    }
}
```

## Python - Track Maximum and Minimum Product

The Python version follows the same logic.

**Complexity:** Time O(n), Space O(1)

```python
n = int(input())
a = list(map(int, input().split()))

max_product = a[0]
min_product = a[0]
answer = a[0]

for x in a[1:]:

    if x < 0:
        max_product, min_product = min_product, max_product

    max_product = max(x, max_product * x)
    min_product = min(x, min_product * x)

    answer = max(answer, max_product)

print(answer)
```

---

# 4. Trapping Rain Water

Given the heights of buildings, calculate the total amount of water that can be trapped after rainfall.

---

## Java - Two Pointer Approach

Use two pointers from both ends. The side with the smaller height is processed first.

**Complexity:** Time O(n), Space O(1)

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

## Python - Two Pointer Approach

Use `left`, `right`, `left_max` and `right_max` to calculate trapped water.

**Complexity:** Time O(n), Space O(1)

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

# 5. Next Lexicographic Permutation

Given an array, rearrange it into the next greater permutation.

If no greater permutation exists, arrange the array in ascending order.

---

## Java - Swap and Reverse Approach

Find the first decreasing element from the right, swap it with the next larger element, and reverse the remaining suffix.

**Complexity:** Time O(n), Space O(1)

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

## Python - Swap and Reverse Approach

The same three steps are implemented directly in Python.

**Complexity:** Time O(n), Space O(1)

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

# 6. Count Subarrays with Sum Equal to K

Given an array and a target `K`, count the number of contiguous subarrays whose sum is exactly `K`.

---

## Java - Prefix Sum and HashMap

Store the frequency of previous prefix sums in a `HashMap`.

**Complexity:** Time O(n), Space O(n)

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();
        int k = sc.nextInt();

        HashMap<Integer, Integer> map = new HashMap<>();

        map.put(0, 1);

        int prefix = 0;
        int count = 0;

        for (int i = 0; i < n; i++) {

            int x = sc.nextInt();

            prefix += x;

            count += map.getOrDefault(prefix - k, 0);

            map.put(prefix, map.getOrDefault(prefix, 0) + 1);
        }

        System.out.println(count);
    }
}
```

## Python - Prefix Sum and Dictionary

Store prefix sums and their frequencies in a dictionary.

**Complexity:** Time O(n), Space O(n)

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

# 7. Longest Increasing Subsequence

Find the length of the longest strictly increasing subsequence.

---

## Java - Binary Search Approach

Maintain the smallest possible ending value for every subsequence length.

**Complexity:** Time O(n log n), Space O(n)

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

## Python - Binary Search Approach

Python's `bisect_left()` performs the required binary search.

**Complexity:** Time O(n log n), Space O(n)

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

# 8. Minimum Coins to Make an Amount

Given coin denominations with unlimited supply, find the minimum number of coins required to make the given amount.

If the amount cannot be formed, print `-1`.

---

## Java - Dynamic Programming

`dp[i]` stores the minimum number of coins required to make amount `i`.

**Complexity:** Time O(n × amount), Space O(amount)

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

        for (int i = 1; i <= amount; i++) {

            for (int coin : coins) {

                if (coin <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
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

## Python - Dynamic Programming

Build the answer from amount `0` up to the required amount.

**Complexity:** Time O(n × amount), Space O(amount)

```python
n, amount = map(int, input().split())

coins = list(map(int, input().split()))

dp = [amount + 1] * (amount + 1)

dp[0] = 0

for i in range(1, amount + 1):

    for coin in coins:

        if coin <= i:
            dp[i] = min(dp[i], dp[i - coin] + 1)

if dp[amount] == amount + 1:
    print(-1)
else:
    print(dp[amount])
```

---

# 9. Edit Distance

Find the minimum number of operations needed to convert one string into another.

Allowed operations:

- Insert a character
- Delete a character
- Replace a character

---

## Java - Dynamic Programming

Use two rows of DP instead of storing the complete matrix.

**Complexity:** Time O(m × n), Space O(n)

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
                        Math.min(current[j - 1], previous[j - 1])
                    );
                }
            }

            previous = current;
        }

        System.out.println(previous[n]);
    }
}
```

## Python - Dynamic Programming

Use two arrays to store the previous and current DP rows.

**Complexity:** Time O(m × n), Space O(n)

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

# 10. Count Connected Regions - Number of Islands

Given a grid containing `1` for land and `0` for water, count the number of islands.

Only horizontal and vertical connections are considered.

---

## Java - BFS Approach

Whenever an unvisited land cell is found, start BFS and mark the entire island as visited.

**Complexity:** Time O(R × C), Space O(R × C)

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

## Python - BFS Approach

Use a queue to visit every connected land cell.

**Complexity:** Time O(R × C), Space O(R × C)

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

# 11. Minimum Time to Infect All Systems - Rotting Oranges

Every infected system infects its healthy neighbours in one minute.

Find the minimum time required to infect all systems. If some systems can never be infected, print `-1`.

---

## Java - Multi-Source BFS

Add all initially infected cells to the queue. Each BFS level represents one minute.

**Complexity:** Time O(R × C), Space O(R × C)

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
                }

                if (grid[i][j] == 1) {
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

## Python - Multi-Source BFS

Start BFS from every infected cell at the same time.

**Complexity:** Time O(R × C), Space O(R × C)

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

# 12. Build Order of Modules

Given modules and their dependencies, find a valid build order.

If multiple modules are available, choose the smallest module number first.

If a cycle exists, print `-1`.

---

## Java - Topological Sort with PriorityQueue

Use Kahn's algorithm. A `PriorityQueue` always gives the smallest available module.

**Complexity:** Time O((n + m) log n), Space O(n + m)

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

        PriorityQueue<Integer> queue = new PriorityQueue<>();

        for (int i = 0; i < n; i++) {

            if (indegree[i] == 0) {
                queue.add(i);
            }
        }

        ArrayList<Integer> order = new ArrayList<>();

        while (!queue.isEmpty()) {

            int u = queue.poll();

            order.add(u);

            for (int v : graph[u]) {

                indegree[v]--;

                if (indegree[v] == 0) {
                    queue.add(v);
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

## Python - Topological Sort with Min Heap

Python's `heapq` is used as a min-heap.

**Complexity:** Time O((n + m) log n), Space O(n + m)

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

# 13. Sliding Window Maximum

Given an array and a window size `K`, find the maximum value in every window.

---

## Java - Deque Approach

Maintain indices in a decreasing order of their values. The first index always represents the maximum.

**Complexity:** Time O(n), Space O(k)

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

            // Remove elements outside the window
            if (!deque.isEmpty() && deque.peekFirst() <= i - k) {
                deque.pollFirst();
            }

            // Remove smaller elements
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

## Python - Deque Approach

Use a deque of indices. The front of the deque contains the maximum element.

**Complexity:** Time O(n), Space O(k)

```python
from collections import deque

n, k = map(int, input().split())

a = list(map(int, input().split()))

deque = deque()

result = []

for i in range(n):

    # Remove elements outside the window
    if deque and deque[0] <= i - k:
        deque.popleft()

    # Remove smaller elements
    while deque and a[deque[-1]] <= a[i]:
        deque.pop()

    deque.append(i)

    if i >= k - 1:
        result.append(a[deque[0]])

print(*result)
```

---

# 14. Largest Rectangle in a Histogram

Given the heights of histogram bars, find the largest rectangular area.

---

## Java - Monotonic Stack

Use an increasing stack. When a smaller bar appears, calculate the area of the bars that are removed.

**Complexity:** Time O(n), Space O(n)

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

        // Sentinel zero
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

## Python - Monotonic Stack

Add a final `0` height to force all remaining bars to be processed.

**Complexity:** Time O(n), Space O(n)

```python
n = int(input())

h = list(map(int, input().split()))

# Sentinel zero
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

# 15. Network Delay Time

A signal starts from server `S` and travels through directed links.

Find the minimum time required for all servers to receive the signal.

If any server cannot be reached, print `-1`.

---

## Java - Dijkstra's Algorithm

Use a `PriorityQueue` to always process the server with the smallest known distance.

**Complexity:** Time O((n + m) log n), Space O(n + m)

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
            return Integer.compare(this.distance, other.distance);
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

        PriorityQueue<Node> queue = new PriorityQueue<>();

        queue.add(new Node(source, 0));

        while (!queue.isEmpty()) {

            Node current = queue.poll();

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

                    queue.add(new Node(v, distance[v]));
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

## Python - Dijkstra's Algorithm

Use `heapq` as a min-heap to process the server having the smallest distance.

**Complexity:** Time O((n + m) log n), Space O(n + m)

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

            heapq.heappush(heap, (new_distance, v))

answer = max(distance[1:])

if answer == INF:
    print(-1)
else:
    print(answer)
```

---

# Quick Revision - Important Techniques

| Problem | Main Technique |
|---|---|
| Longest Substring with K Distinct | Sliding Window + HashMap |
| Minimum Platforms | Sorting + Two Pointers |
| Maximum Product Subarray | Maximum/Minimum DP |
| Trapping Rain Water | Two Pointers |
| Next Permutation | Swap + Reverse |
| Subarray Sum K | Prefix Sum + HashMap |
| Longest Increasing Subsequence | Binary Search |
| Minimum Coins | Dynamic Programming |
| Edit Distance | Dynamic Programming |
| Number of Islands | BFS |
| Rotting Oranges | Multi-Source BFS |
| Build Order | Topological Sort + Min Heap |
| Sliding Window Maximum | Deque |
| Largest Rectangle | Monotonic Stack |
| Network Delay Time | Dijkstra + Min Heap |
