LeetCode 1190 - Reverse Substrings Between Each Pair of Parentheses

Problem

Given a string containing lowercase English letters and parentheses, reverse the strings inside every matching pair of parentheses, starting from the innermost pair. Remove all parentheses from the final answer.

Example

Input

(u(love)i)

Output

iloveu

Approach

Use a stack of StringBuilder objects.

On (, push the current string and start a new StringBuilder.

On a letter, append it to the current string.

On ), reverse the current string.

Pop the previous string and append the reversed part to it.

Continue until the complete string is built.

Java

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

Dry Run

For (u(love)i):

( → push ""

u → u

( → push u

love → love

) → reverse love → evol, attach to u → uevol

i → uevoli

) → reverse → iloveu

Complexity

Time: O(n²) worst case due to repeated reversals.

Space: O(n).

Key Concept

Opening bracket → save the previous string.
Closing bracket → reverse the current string and attach it to the previous string.

Topic

Stack

StringBuilder

String Manipulation

Parentheses
