# Longest Valid Parentheses

## Solution
There are numerous solutions listed on the [solution page](https://leetcode.com/problems/longest-valid-parentheses/solution/).

However, I think two of them were particularly elegent.
- Stack (`time: O(N), space: O(N)`)
- Two Scan (`time: O(N), space: O(1)`)

### Stack
Push the parentheses into the stack.
```python
if stack.top() == '(' and cur_parenthesis == ')':
    stack.pop()
else:
    stack.push(cur_parenthesis)
```
After you've done this for all parentheses, the only ones left in the stack will be invalid parentheses.  
And the spaces between the invalid parentheses are valid sequences.  
Then finding the longest one would be a breeze.  

However, be cautious of the edge case of an empty stack.  
So I'll push a start char before pushing the parentheses, and push an end char after pushing the parentheses.  
So that there would be at least two char can be used to calculate the space.

### Two Scan
You can find the longest valid sequence by performing a left-to-right scan with two pointers.

The scan goes like this:
1. set your left at a '('
2. from left, scanning your right pointer, 
    and calculate the parentheses counter with '(': +1, ')': -1
3. when the counter is
    - == 0, record the length, continue
    - \> 0, continue
    - < 0, set left = right + 1, back to 1.

However, you must be aware that something is missing.  
That is, your left pointer is always on a `first '('`. (a `'('` to the right of a `')'`)  
You can't find a sequence starts with a `non-first '('`. (a `'('` to the right of a `'('`)  
Consider the case of `'(()'`.

And this can be solved by scanning the sequence from right to left again.  

Here's the proof.  

Assume the longest sequence starts with a `non-first '('` at index `i` and ends at index `j`.  
According to the assumption, the char at `i-1` would be `'('` .  
Then the char at `j+1` would not be a `')'`, otherwise `i-1`~`j+1` would be a longer sequence.  
So if we scan it from right to left, the `')'` at `j` would definitely be a `first ')'`.
