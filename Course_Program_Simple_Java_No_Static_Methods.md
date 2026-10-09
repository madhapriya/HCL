# Course Program – Simple Java Solution (No Separate Static Methods)

## Problem Summary

Create a `Course` class with private attributes `courseId`, `courseName`, `courseAdmin`, `quiz`, and `handson`. Add a parameterized constructor, getters, and setters.

Read four courses, an admin name, and a handson threshold. Then:
1. Print the integer average quiz score for courses managed by the given admin.
2. Print the names of courses whose `handson` value is below the threshold, sorted in ascending order.

As requested, both operations are written directly inside `main()`—there are **no separate static methods**.

> The original statement asks for static methods. This version keeps the same logic inside `main()` to match your request for a simpler solution.

## Simple Java Code

```java
import java.util.*;

class Course {
    private int courseId;
    private String courseName;
    private String courseAdmin;
    private int quiz;
    private int handson;

    Course(int courseId, String courseName, String courseAdmin, int quiz, int handson) {
        this.courseId = courseId;
        this.courseName = courseName;
        this.courseAdmin = courseAdmin;
        this.quiz = quiz;
        this.handson = handson;
    }

    public int getCourseId() {
        return courseId;
    }

    public void setCourseId(int courseId) {
        this.courseId = courseId;
    }

    public String getCourseName() {
        return courseName;
    }

    public void setCourseName(String courseName) {
        this.courseName = courseName;
    }

    public String getCourseAdmin() {
        return courseAdmin;
    }

    public void setCourseAdmin(String courseAdmin) {
        this.courseAdmin = courseAdmin;
    }

    public int getQuiz() {
        return quiz;
    }

    public void setQuiz(int quiz) {
        this.quiz = quiz;
    }

    public int getHandson() {
        return handson;
    }

    public void setHandson(int handson) {
        this.handson = handson;
    }
}

public class courseProgram {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Course[] courses = new Course[4];

        // Read the 4 course records
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

        // 1. Find average quiz score for the given admin
        int sum = 0;
        int count = 0;

        for (int i = 0; i < courses.length; i++) {
            if (courses[i].getCourseAdmin().equalsIgnoreCase(searchAdmin)) {
                sum += courses[i].getQuiz();
                count++;
            }
        }

        if (count > 0) {
            System.out.println(sum / count);
        } else {
            System.out.println("No Course found");
        }

        // 2. Collect courses with handson less than threshold
        Course[] result = new Course[4];
        int size = 0;

        for (int i = 0; i < courses.length; i++) {
            if (courses[i].getHandson() < threshold) {
                result[size] = courses[i];
                size++;
            }
        }

        // Sort matching courses by handson in ascending order
        for (int i = 0; i < size - 1; i++) {
            for (int j = i + 1; j < size; j++) {
                if (result[i].getHandson() > result[j].getHandson()) {
                    Course temp = result[i];
                    result[i] = result[j];
                    result[j] = temp;
                }
            }
        }

        // Print course names, or the required message
        if (size > 0) {
            for (int i = 0; i < size; i++) {
                System.out.println(result[i].getCourseName());
            }
        } else {
            System.out.println("No Course found with mentioned attribute.");
        }

        sc.close();
    }
}
```

## Dry Run – Input 1

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

### Part 1: Average quiz score for `Nisha`

Matching courses: `kubernetes` (40) and `Apache Spark` (30).

```text
sum = 40 + 30 = 70
count = 2
average = 70 / 2 = 35
```

### Part 2: Courses with `handson < 17`

After sorting by handson:

1. kubernetes – 10
2. Apache Spark – 12
3. cassandra – 15

### Output 1

```text
35
kubernetes
Apache Spark
cassandra
```

## Dry Run – Input 2

The admin is `Shubhamk`, which does not match any course admin. Also, no course has a `handson` value below `5`.

### Output 2

```text
No Course found
No Course found with mentioned attribute.
```

## Important Notes

- `equalsIgnoreCase()` compares admin names without case sensitivity.
- `sum / count` performs integer division.
- The condition is strictly `handson < threshold`, not `<=`.
- Sorting is applied only to matching courses.
- If the assessment explicitly requires the two named static methods, use the method-based version. This file follows your request for simple logic inside `main()`.
