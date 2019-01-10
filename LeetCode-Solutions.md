# 001. Two Sum

Tag: _hash table_, _array_

Before thought: two loops. 

After thought: didn't think of hashtable. Need to understand why hashtable's amortized time complexity is O(1);

## Brute Force
```Java
// 33ms
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[j] == target - nums[i]) {
                return new int[] { i, j };
            }
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

## Two-pass hash table

```Java
// 8 ms
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap();
        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }
        
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            if (map.containsKey(complement) && i != map.get(complement)) {
                return new int[] {i, map.get(complement)};
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```
## One pass hash table
Similar to above solution. Do hash table lookup as you move along the loop


# 007. Reverse Integer

Initial thought: 
1. strip out sign (+/-); 
2. divide number by 10 and take mod, push mod value to queue. Then print queue from left to right, do not push if the first digit is 0. 

```Java
// 28ms
public int reverse(int x) {
    int sign = Integer.signum(x);
    int posnum = Math.abs(x);
    
    int rev = 0;
    while ( x != 0) {
        int pop = x % 10;
        x /= 10;
        
        if (rev > Integer.MAX_VALUE/10 || (rev == Integer.MAX_VALUE/10 && pop > 7)) return 0;
        if (rev < Integer.MIN_VALUE/10 || (rev == Integer.MIN_VALUE/10 && pop < -8)) return 0;
        
        rev = rev*10 + pop;
    }
    return rev;
}
```

After thought: 
- reverse string can be done in the loop itself
- didn't consider overflow when reassemble the number. 

Complexity Analysis:
- Time: O(log10(x)). There are roughly Log10(x) digits in x
- Space: O(1)


# 009. Palindrome Number

Initial thought:
- Read integer from left to right, convert it to the string
- reverse string. If equals, then palindrome true, otherwise, false. 

```Java
class Solution {
    public boolean isPalindrome(int x) {
        String xStr = Integer.toString(x);
        int len = xStr.length(); 
        // string length method needs (), array doesn't.
        
        StringBuilder sb = new StringBuilder();
        for (int i = len-1; i >= 0; i--) {
            sb.append(xStr.charAt(i));
        }
        
        // evaluate whether strings are equal, cannot use == operator. String.equals() is the right choice.
        return xStr.equals(sb.toString()); 
    }
}
```

If we cannot use convert the number to string, we have to consider the number overflow issue.

The solution suggested algorithm:
- convert only the last half of the number and then compare it to the first half. If they are equal, then the number is a palindrome. 
- edge case, all negative numbers are not palindrome. return false directly. 

```Java
public boolean isPalindrome(int x) {
    if (x < 0) {
        // negative number is not palindrome. return directly.
        return false;
    }
    int len = (int) Math.ceil(Math.log10(x));
    int rev = 0;
    for (int i = 0; i < len / 2; i++) {
        int temp = x % 10;
        x /= 10;
        rev = rev * 10 + temp;
    }
    // if length is even, shift off the middle digit by an extra devide.
    if (len % 2 > 0) {
        x /= 10;
    }
    return rev == x ? true : false;
}
```

The above solution works for majority of numbers. One edge case is missed. When input is `1`, output is false. 

```Java
public boolean isPalindrome(int x) {
    if (x < 0) {
        // negative number is not palindrome. return directly.
        return false;
    }
    if (x < 10) {
        // missed an edge case. When input is single digit, it's palindrome
        return true;
    }
    int len = (int) Math.ceil(Math.log10(x));
    int rev = 0;
    for (int i = 0; i < len / 2; i++) {
        int temp = x % 10;
        x /= 10;
        rev = rev * 10 + temp;
    }
    // if length is not even, shift off the middle digit by an extra devide.
    if (len % 2 > 0) {
        x /= 10;
    }
    return rev == x ? true : false;
}
```

Instead of using length of a number, here is the official answer to determine whether the half of the number is reached. 

> Now the question is, how do we know that we've reached the half of the number?

> Since we divided the number by 10, and multiplied the reversed number by 10, when the original number is less than the reversed number, it means we've processed half of the number digits.
```

Complexity Analysis:
- Time: O(log10(x)). There are roughly Log10(x) digits in x
- Space: O(1)