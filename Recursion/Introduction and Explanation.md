**Recursion** is a programming technique where a function calls itself to solve smaller instances of the same problem. This process continues until the problem becomes simple enough to solve directly, referred to as the **base case**

---
Reference : 
https://www.geeksforgeeks.org/introduction-to-recursion-2/?ref=lbp
https://www.youtube.com/watch?v=M2uO2nMT0Bk&t=2736s
https://www.youtube.com/playlist?list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9
https://www.scaler.in/recursion-tree-method/

---
![[FactorialRecursionImage.png]]
### **How Recursion Works**

1. ***Base Case:***  
    The condition where the function stops calling itself is known as the **base case**. Without this, 
    recursion would go on indefinitely, leading to a [stack overflow](https://stackoverflow.com/questions/26158/how-does-a-stack-overflow-occur-and-how-do-you-prevent-it).

2. ***Recursive Case:***  
    The condition where the function calls itself with modified input to reduce the problem size, aiming to reach the base case.
    
3. ***[Call Stack](https://launchschool.com/books/advanced_dsa/read/exploring_call_stack):***  
    Each recursive call is pushed onto a **call stack**, which stores the function’s parameters, local variables, and return addresses. When the base case is reached, the stack unwinds, resolving the computations step by step.
    

---

### **Execution Flow of Recursion**

1. **Recursive Call:**
    - The function calls itself repeatedly, breaking the problem into smaller subproblems.
2. **Base Case Reached:**
    - Once the simplest version of the problem (base case) is reached, the recursion stops.
3. **Stack Unwinding:**
    - Results are returned to previous function calls, step by step, until the final result is computed.

---

### **1. Factorial Calculation**

#### ***Concept**:*

The **factorial** of a non-negative integer `n` is the product of all positive integers less than or equal to `n`. The factorial is commonly denoted as `n!`, and it is defined recursively as:

- `n! = n * (n - 1) * (n - 2) * ... * 1`
- **Base Case**: `0! = 1`

In recursion, we solve a problem by breaking it down into smaller subproblems. The **factorial** function calls itself with decreasing values of `n` until it reaches the base case, where `n == 0`.

#### ***Recursive Approach**:*

1. **Base Case**: If `n == 0`, return 1 (since `0! = 1`).
2. **Recursive Case**: Otherwise, return `n * factorial(n - 1)`.

#### ***Pseudocode**:*

```
Function factorial(n):
    If n == 0:
        Return 1
    Else:
        Return n * factorial(n - 1)
```

#### ***Execution Flow (Example: `factorial(3)`)**:*

- `factorial(3) = 3 * factorial(2)`
- `factorial(2) = 2 * factorial(1)`
- `factorial(1) = 1 * factorial(0)`
- `factorial(0) = 1` (Base Case)
- The function then returns values step-by-step as the call stack unwinds:
    - `factorial(1) = 1`
    - `factorial(2) = 2 * 1 = 2`
    - `factorial(3) = 3 * 2 = 6`

#### ***Key Concepts**:*

- **Base Case**: The condition that stops the recursion, preventing infinite calls.
- **Recursive Case**: The case where the function calls itself with a modified argument.

---

### **2. Fibonacci Series**

#### ***Concept**:*

The **Fibonacci series** is a sequence of numbers in which each number is the sum of the two preceding ones, typically starting with 0 and 1. The series is defined as:

- `F(0) = 0`
- `F(1) = 1`
- `F(n) = F(n - 1) + F(n - 2)` for `n > 1`

This sequence is a classic example of a problem that can be solved using recursion.

#### ***Recursive Approach**:*

1. **Base Case 1**: If `n == 0`, return 0.
2. **Base Case 2**: If `n == 1`, return 1.
3. **Recursive Case**: Otherwise, return `fibonacci(n - 1) + fibonacci(n - 2)`.

#### ***Pseudocode**:*

```
Function fibonacci(n):
    If n == 0:
        Return 0
    Else If n == 1:
        Return 1
    Else:
        Return fibonacci(n - 1) + fibonacci(n - 2)
```

#### ***Execution Flow (Example: `fibonacci(4)`)**:*

- `fibonacci(4) = fibonacci(3) + fibonacci(2)`
- `fibonacci(3) = fibonacci(2) + fibonacci(1)`
- `fibonacci(2) = fibonacci(1) + fibonacci(0)`
- **Base Cases**: `fibonacci(0) = 0`, `fibonacci(1) = 1`
- The function returns values as the stack unwinds:
    - `fibonacci(2) = 1 + 0 = 1`
    - `fibonacci(3) = 1 + 1 = 2`
    - `fibonacci(4) = 2 + 1 = 3`

#### ***Key Concepts**:*

- **Base Cases**: `F(0) = 0` and `F(1) = 1` are the stopping points.
- **Recursive Case**: The function calls itself twice (`n-1` and `n-2`) to calculate the Fibonacci number.

---

### **3. Sum of Natural Numbers**

#### ***Concept**:*

The **sum of natural numbers** is the sum of all integers from `1` to `n`. The formula for the sum of the first `n` natural numbers is:

- `S(n) = 1 + 2 + 3 + ... + n`

This problem can also be solved recursively, where the sum of numbers from `n` down to `0` is calculated step by step.

#### ***Recursive Approach**:*

1. **Base Case**: If `n == 0`, return 0.
2. **Recursive Case**: Otherwise, return `n + sumOfNaturalNumbers(n - 1)`.

#### ***Pseudocode**:*

```
Function sumOfNaturalNumbers(n):
    If n == 0:
        Return 0
    Else:
        Return n + sumOfNaturalNumbers(n - 1)
```

#### ***Execution Flow (Example: `sumOfNaturalNumbers(4)`)**:*

- `sumOfNaturalNumbers(4) = 4 + sumOfNaturalNumbers(3)`
- `sumOfNaturalNumbers(3) = 3 + sumOfNaturalNumbers(2)`
- `sumOfNaturalNumbers(2) = 2 + sumOfNaturalNumbers(1)`
- `sumOfNaturalNumbers(1) = 1 + sumOfNaturalNumbers(0)`
- **Base Case**: `sumOfNaturalNumbers(0) = 0`
- The function returns values as the stack unwinds:
    - `sumOfNaturalNumbers(1) = 1 + 0 = 1`
    - `sumOfNaturalNumbers(2) = 2 + 1 = 3`
    - `sumOfNaturalNumbers(3) = 3 + 3 = 6`
    - `sumOfNaturalNumbers(4) = 4 + 6 = 10`

#### ***Key Concepts**:*

- **Base Case**: The recursion stops when `n == 0`.
- **Recursive Case**: The function calls itself with a reduced argument (`n - 1`).

---
## **Recursion Tree and Stack**

When understanding recursion, both **recursion trees** and **recursion stacks** are crucial tools for visualizing how recursion works. However, they serve different purposes and emphasize different aspects of recursive processes. Let’s explore both concepts and when to use them:

### **1. Recursion Tree**

A **recursion tree** is a diagrammatic representation that illustrates how a recursive function expands, showing all the function calls made and their relationships in a **tree-like structure**.

#### **Purpose:**

- To understand **how the recursive calls split** into sub-problems.
- To visualize the **flow of recursion** and **repetition** of calls.
- Useful for analyzing **time complexity** (e.g., counting the number of calls).

#### **Key Features:**

- Represents recursive function calls as nodes in a tree.
- The root node is the **initial call**, and its children are the **subsequent recursive calls**.
- Leaf nodes correspond to the **base case** where recursion stops.

#### **Example: Fibonacci Recursion**

For the function:

```go
func fibonacci(n int) int {
    if n == 0 || n == 1 {
        return n
    }
    return fibonacci(n-1) + fibonacci(n-2)
}
```

A recursion tree for `fibonacci(4)` looks like this:

```
          fibonacci(4)
         /             \
   fibonacci(3)       fibonacci(2)
    /     \            /     \
fibonacci(2) fibonacci(1) fibonacci(1) fibonacci(0)
  /     \
fibonacci(1) fibonacci(0)
```

- Each node represents a function call.
- Base cases are at the leaves (`fibonacci(1)` and `fibonacci(0)`).

#### **When to Use a Recursion Tree:**

- When analyzing **how many times a recursive function is called**.
- To **trace dependencies** between recursive calls.
- Useful for understanding **divide-and-conquer algorithms** like merge sort or quick sort.

---

### **2. Recursion Stack**

A **recursion stack** represents the **state of the program's call stack** during recursive function execution. It is a sequential structure where **function calls are pushed and popped** based on the recursion flow.

#### **Purpose:**

- To understand the **order of function calls** and **how values are returned**.
- To track the **sequence of execution** and the **state of the program** at each step.
- Useful for debugging and understanding **space complexity**.

#### **Key Features:**

- Each recursive function call adds a new **stack frame** to the call stack.
- Frames are popped as base cases return their values.
- The stack grows **depth-first**, reflecting the **last-in, first-out (LIFO)** principle.

#### **Example: Print Reverse**

For the function:

```go
func printReverse(n int) {
    if n == 0 {
        return
    }
    printReverse(n - 1)
    fmt.Println(n)
}
```

For `printReverse(3)`, the call stack evolves as follows:

1. **Before Base Case (Recursive Calls):**
    
    ```
    Call Stack:
    printReverse(3)
    printReverse(2)
    printReverse(1)
    printReverse(0)  // Base case
    ```
    
2. **During Stack Unwinding (Returning):**
    
    ```
    Call Stack:       Output:
    printReverse(1)   1
    printReverse(2)   2
    printReverse(3)   3
    ```
    

- Each recursive call is pushed onto the stack.
- Once the base case is reached, calls are **popped** and executed in reverse order.

#### **When to Use a Recursion Stack:**

- When analyzing **execution order** and understanding how recursion unwinds.
- To debug and visualize **intermediate states** during recursion.
- Useful for algorithms where **space complexity** is a concern (e.g., tail recursion).

---

### **Comparison: Recursion Tree vs. Recursion Stack**

| **Aspect**             | **Recursion Tree**                             | **Recursion Stack**                                   |
| ---------------------- | ---------------------------------------------- | ----------------------------------------------------- |
| **Focus**              | Shows all function calls as a tree.            | Shows the actual sequence of calls and returns.       |
| **Use Case**           | Analyze function calls and time complexity.    | Analyze execution order and space complexity.         |
| **Representation**     | Tree-like structure with branches.             | Sequential stack frames in memory.                    |
| **Best For**           | Understanding recursion flow and dependencies. | Debugging and understanding how calls are executed.   |
| **Example Algorithms** | Divide-and-conquer (e.g., merge sort).         | Depth-first recursion (e.g., printing, backtracking). |

---

### **Which to Use?**

- Use **recursion trees** when studying **time complexity** or visualizing the structure of recursive calls.
- Use **recursion stacks** when analyzing **execution order**, **space complexity**, or debugging recursive functions.

Both tools are complementary and often used together for a comprehensive understanding of recursion.

---
## **Summary of Recursion Concepts:**

1. **Base Case**: The stopping condition for the recursion. Every recursive function must have a base case to avoid infinite recursion.
2. **Recursive Case**: The part of the function where it calls itself with a different argument, moving toward the base case.
3. **Call Stack**: Recursion utilizes the call stack, where each recursive call adds a new layer to the stack. As the base case is reached, the stack begins to unwind, returning results step-by-step.

### **Advantages of Recursion**:

- Recursive solutions are often simpler and more elegant for problems that have repetitive subproblems (like factorials, Fibonacci numbers, and sums).
- Recursion allows complex problems to be broken down into simpler subproblems.

### **Disadvantages of Recursion**:

- **Performance**: Recursive solutions can be less efficient in terms of memory and time compared to iterative solutions.
- **Stack Overflow**: Deep recursion (too many recursive calls) can lead to a stack overflow error if the base case is not reached in time.

### **Applications of Recursion**:

- Calculating factorials and Fibonacci numbers
- Solving problems in data structures like trees and graphs (e.g., tree traversals)
- Divide-and-conquer algorithms (e.g., quicksort, mergesort)
- Backtracking problems (e.g., N-Queens problem, Sudoku solver)

### **Conclusion**:

1. **Base Case:** Always define one to prevent infinite recursion.
2. **Recursive Case:** Simplify the problem towards the base case.
3. **Call Stack:** Understand its role and how recursion utilizes it.
4. **Efficiency:** Recursion can be inefficient for large problems; iterative solutions or optimizations like **memoization** may be better.
