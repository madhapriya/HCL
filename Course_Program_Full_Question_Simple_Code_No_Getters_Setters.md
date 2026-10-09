# Course Program – Full Question and Simple Java Solution

## Full Problem Statement

Create a class named `Course` with the following private attributes:

- `courseId` – `int`
- `courseName` – `String`
- `courseAdmin` – `String`
- `quiz` – `int`
- `handson` – `int`

Create a parameterized constructor to initialize all five attributes.

Create another class named `courseProgram` with the `main()` method.

Read details of **4 Course objects** from standard input. For each course, read the course ID, course name, course admin, quiz score, and hands-on value. Then read a course-admin name and an integer hands-on threshold.

Perform the following operations:

### 1. Find Average Quiz Score by Admin

Find the average quiz score of all courses whose `courseAdmin` matches the given admin name. The comparison should be case-insensitive.

- Return/print the integer average if at least one matching course is found.
- If no course matches the given admin, print:

```text
No Course found
```

### 2. Sort Courses by Hands-On Value

Find all courses whose `handson` value is **strictly less than** the given threshold. Sort those courses in ascending order of `handson`.

- Print the name of each matching course in sorted order.
- If no course matches, print:

```text
No Course found with mentioned attribute.
```

### Important Requirement for This Version

The original question asks for two separate static methods, but this simplified version performs both operations directly inside `main()`, as requested. The `Course` class uses private attributes and a parameterized constructor. **Getters and setters are omitted**; the fields are accessed directly by `courseProgram` through the nested-class arrangement below.

## Input Format

For each of the 4 courses, provide these values in order, each on its own line:

1. Course ID (`int`)
2. Course name (`String`)
3. Course admin (`String`)
4. Quiz score (`int`)
5. Hands-on value (`int`)

After all 4 courses, provide:

6. Admin name to search (`String`)
7. Hands-on threshold (`int`)

## Output Format

- First line: the integer average quiz score for the selected admin, or `No Course found`.
- Following lines: names of courses with hands-on values below the threshold, sorted in ascending order, or `No Course found with mentioned attribute.` if none match.

## Constraints

- Exactly 4 course records are read by the program.
- Course IDs, quiz scores, and hands-on values are integers.
- The admin-name comparison is case-insensitive.
- A course qualifies for the second operation only when `handson < threshold`.
- The average is printed as an integer using integer division.

## Sample Input 1

```text
111
kubernetes
Nisha
40
10
321
cassandra
Roshini
30
15
457
Apache Spark
Nisha
30
12
987
site core
Tirth
50
20
Nisha
17
```

## Sample Output 1

```text
35
kubernetes
Apache Spark
cassandra
```

## Explanation 1

**Operation 1: Average quiz score for `Nisha`**

Two courses are managed by Nisha:

| Course | Quiz score |
|---|---:|
| kubernetes | 40 |
| Apache Spark | 30 |

```text
sum = 40 + 30 = 70
count = 2
average = sum / count = 70 / 2 = 35
```

So the first output line is `35`.

**Operation 2: Sort courses with `handson < 17`**

The qualifying courses are:

| Course | Hands-on |
|---|---:|
| kubernetes | 10 |
| cassandra | 15 |
| Apache Spark | 12 |

Sort by hands-on value in ascending order:

1. kubernetes – 10
2. Apache Spark – 12
3. cassandra – 15

So the remaining output lines are the three course names in that order.

---

## Sample Input 2

```text
111
kubernetes
Nisha
40
10
321
cassandra
Roshini
30
15
457
Apache Spark
Nisha
30
12
987
site core
Tirth
50
20
Shubhamk
5
```

## Sample Output 2

```text
No Course found
No Course found with mentioned attribute.
```

## Explanation 2

- No course has `courseAdmin` equal to `Shubhamk`, so print `No Course found`.
- No course has a `handson` value below `5`, so print `No Course found with mentioned attribute.`

---

# Simple Java Solution

This version has **no separate static methods and no getters/setters**. To keep the attributes private while allowing direct access, `Course` is declared as a nested class inside `courseProgram`.

```java
import java.util.*;

public class courseProgram {

    static class Course {
        private int courseId;
        private String courseName;
        private String courseAdmin;
        private int quiz;
        private int handson;

        Course(int courseId, String courseName, String courseAdmin,
               int quiz, int handson) {
            this.courseId = courseId;
            this.courseName = courseName;
            this.courseAdmin = courseAdmin;
            this.quiz = quiz;
            this.handson = handson;
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Course[] courses = new Course[4];

        // Read 4 courses
        for (int i = 0; i < 4; i++) {
            int id = sc.nextInt();
            sc.nextLine();

            String name = sc.nextLine();
            String admin = sc.nextLine();

            int quiz = sc.nextInt();
            int handson = sc.nextInt();
            sc.nextLine();

            courses[i] = new Course(id, name, admin, quiz, handson);
        }

        String searchAdmin = sc.nextLine();
        int threshold = sc.nextInt();

        // 1. Calculate the average quiz score for the given admin
        int sum = 0;
        int count = 0;

        for (int i = 0; i < 4; i++) {
            if (courses[i].courseAdmin.equalsIgnoreCase(searchAdmin)) {
                sum += courses[i].quiz;
                count++;
            }
        }

        if (count > 0) {
            System.out.println(sum / count);
        } else {
            System.out.println("No Course found");
        }

        // 2. Store courses whose hands-on value is below the threshold
        Course[] result = new Course[4];
        int size = 0;

        for (int i = 0; i < 4; i++) {
            if (courses[i].handson < threshold) {
                result[size] = courses[i];
                size++;
            }
        }

        // Sort the matching courses by hands-on value
        for (int i = 0; i < size - 1; i++) {
            for (int j = i + 1; j < size; j++) {
                if (result[i].handson > result[j].handson) {
                    Course temp = result[i];
                    result[i] = result[j];
                    result[j] = temp;
                }
            }
        }

        // Print the sorted course names
        if (size > 0) {
            for (int i = 0; i < size; i++) {
                System.out.println(result[i].courseName);
            }
        } else {
            System.out.println("No Course found with mentioned attribute.");
        }

        sc.close();
    }
}
```

## Code Explanation

### 1. Read the courses

`Course[] courses = new Course[4]` creates an array to store four course objects. The loop reads each course's details and creates an object using the constructor.

### 2. Calculate the average

- `sum` stores the quiz scores of matching courses.
- `count` stores how many courses match the admin.
- `equalsIgnoreCase()` compares admin names without considering uppercase/lowercase.
- If `count` is greater than zero, print `sum / count`; otherwise, print `No Course found`.

### 3. Select courses by hands-on value

The condition is:

```java
courses[i].handson < threshold
```

Only courses with a hands-on value strictly below the threshold are copied into the `result` array.

### 4. Sort the selected courses

The nested loops compare the hands-on values of each pair. If the earlier value is larger, swap the two course objects.

### 5. Print the result

Print each selected course's name after sorting. If no courses qualify, print the required message.

## Complexity

Let `n` be the number of courses.

- Average calculation: `O(n)`
- Filtering: `O(n)`
- Sorting: `O(n²)` in this simple implementation
- Extra space: `O(n)`

Here `n = 4`, as specified by the question.

## Important Exam Notes

- Keep the comparison as `equalsIgnoreCase()` if admin matching should ignore letter case.
- Use `< threshold`, not `<= threshold`.
- Sort only the filtered courses.
- The average uses integer division.
- If the platform requires a top-level `Course` class, Java's `private` fields cannot be accessed directly by another top-level class without getters/setters. In that case, either use getters/setters or change the field access level. This version uses a nested `Course` class so the fields can remain private and no getters/setters are needed.
