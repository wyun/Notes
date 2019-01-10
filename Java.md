# Java Notes

## Integer
[Doc](https://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html)
- Integer.MAX_VALUE: A constant holding the maximum value an int can have, 2^31-1.
- Integer.MIN_VALUE: A constant holding the minimum value an int can have, -2^31.

## Array

return a new array, specify the type, and give values in curly bracket, unlike square bracket in Perl
```Java
return new int[] {a, b c};
```

## Hash Table / Hash Map

- Create hash map: `Map<TYPE, TYPE> map = new HashMap()`
- Put K,V: `map.put(key, value)`
- Get key: `map.get(key)`
- Whether a key is defined: `map.containsKey(key)`

```Java
Map<Integer, Integer> map = new HashMap();
for (int i = 0; i < nums.length; i++) {
    map.put(nums[i], i); // store value
}

```

## Error

When no other return is available, return error. 
```Java
throw new IllegalArgumentException("No two sum solution");
```