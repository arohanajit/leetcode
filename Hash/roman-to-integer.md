# 13. Roman to Integer

## Question
Hint
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, 2 is written as II in Roman numeral, just two ones added together. 12 is written as XII, which is simply X + II. The number 27 is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer.

## My Solution
class Solution:
    def romanToInt(self, s: str) -> int:
        vals = {"I":1,"V":5,"X":10,"L":50,"C":100,"D":500,"M":1000}
        res = 0
        i = len(s)-1
        while(i>-1):
            if i-1<0:
                print(f"0. i:{i} val:{s[i]}")
                res+=vals[s[i]]
                break
            else:
                print(f"i: {i}")
                if vals[s[i-1]]>=vals[s[i]]:
                    print(f"1. val: {s[i-1]}{s[i]} s[i]:{vals[s[i]]} s[i-1]:{vals[s[i-1]]}")
                    res+=vals[s[i]]
                    i-=1
                else:
                    print(f"2. val: {s[i-1]}{s[i]} s[i]:{vals[s[i]]} s[i-1]:{vals[s[i-1]]}")
                    res+=vals[s[i]]-vals[s[i-1]]
                    i-=2
                print(f"res: {res}")
        print(res)
        return res

### Initial Thoughts
Recognizing that the numerals are usually written from largest to smallest, except in subtraction scenarios, informs the decision to parse the string from right to left, which simplifies identifying and handling these exceptions.

### Algorithm Steps
- Map Symbols to Values: First, create a dictionary mapping each Roman numeral symbol to its corresponding integer value.
- Initialize Variables: Start with a result variable set to 0 to accumulate the integer values and an index to traverse the string from the last character to the first.
- Traverse the String Backwards:
- If at the start of the string, add the corresponding value of the symbol to the result.
- Otherwise, compare the current symbol with the one before it:
- If the previous symbol has a value greater than or equal to the current, add the current symbol's value to the result.
- If the previous symbol's value is smaller, subtract the previous symbol's value from the current and add the result to the total. This handles the special cases of subtraction.
- Adjust the index accordingly, moving two places back for a subtraction case and one place otherwise.
- Final Calculation: After the loop completes, the result contains the integer value of the Roman numeral.

### Challenges and Solutions
The primary challenge was correctly handling the cases where subtraction is used without making the logic overly complex or inefficient. By deciding to parse the string from right to left, it became straightforward to decide when to add values together and when to subtract, based on simple comparisons between consecutive symbols.

### Optimization and Efficiency
This solution is both time-efficient and space-efficient:

- Time Complexity: O(n), where n is the length of the Roman numeral string, as each symbol in the string is visited once.
- Space Complexity: O(1), since the storage is constant, not depending on the input size but only a small fixed-size dictionary and a few auxiliary variables.