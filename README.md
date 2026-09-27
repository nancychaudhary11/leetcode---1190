# LeetCode 1190 - Reverse Substrings Between Each Pair of Parentheses

## Problem

Given a string `s` that contains lowercase English letters and parentheses, reverse the strings inside each matching pair of parentheses, starting from the innermost pair.

Return the final string with all parentheses removed.

## Example

**Input:**

```text
(u(love)i)
```

**Output:**

```text
iloveu
```

## Approach

We use a **Stack + StringBuilder**.

* When we find `(`, push the current StringBuilder into the stack and start a new StringBuilder.
* When we find a letter, append it to the current StringBuilder.
* When we find `)`, reverse the current StringBuilder, pop the previous StringBuilder, and append the reversed string to it.
* Continue until the complete string is formed.

## Java Code

```java
import java.util.*;

class Solution {
    public String reverseParentheses(String s) {
        Stack<StringBuilder> stack = new Stack<>();
        StringBuilder current = new StringBuilder();

        for (char ch : s.toCharArray()) {

            if (ch == '(') {
                stack.push(current);
                current = new StringBuilder();
            }

            else if (ch == ')') {
                StringBuilder previous = stack.pop();

                current.reverse();

                previous.append(current);
                current = previous;
            }

            else {
                current.append(ch);
            }
        }

        return current.toString();
    }
}
```

## Dry Run

Input:

```text
(u(love)i)
```

1. `(` → push `""`
2. `u` → current = `"u"`
3. `(` → push `"u"`
4. `love` → current = `"love"`
5. `)` → reverse `"love"` → `"evol"`
6. Append to `"u"` → `"uevol"`
7. `i` → `"uevoli"`
8. `)` → reverse `"uevoli"` → `"iloveu"`

**Final Answer:**

```text
iloveu
```

## Key Concept

```text
'('     → PUSH previous string
letter  → APPEND
')'     → REVERSE + POP + APPEND
```

The innermost parentheses are processed first because they close first.

## Complexity

* **Time:** O(n²) in the worst case
* **Space:** O(n)

## Topics

* Stack
* StringBuilder
* String Manipulation
* Parentheses
* Simulation

## LeetCode

**Problem:** 1190. Reverse Substrings Between Each Pair of Parentheses
**Language:** Java
