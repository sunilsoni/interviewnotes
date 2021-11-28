
# Anagram

Given two strings str1 and str2, write a function to determine whether str2 is an anagram of str1.


Example 1:
```log
Input: s = "anagram", t = "nagaram"
Output: true
```

Example 2:
```log
Input: s = "rat", t = "car"
Output: false
```

You can assume that the string contains only lowercase letters.

**Advanced:**

What if the input string contains unicode characters? Can you adjust your solution to deal with this situation?

## **Problem analysis**

Alphabetic eccentrics mean that if two strings are eccentrics of each other, then the number and types of characters in the two strings are the same. The difference is the position and sequence of each character. The easiest way is to directly sort the strings according to certain rules, and then traverse the comparison. This method saves space, but because it involves sorting, the time complexity is just that O(nlgn).

There is also a method similar to counting and sorting, which is to count the number of all characters in a string, and then compare another string. This can reduce the time complexity to O(n)that, if the string in this question If it only contains lowercase letters, we can open up an array with a length of 26, so that no extra space is needed, but if the input string contains unicode characters, because the unicode character set is too large, the constant level array becomes less Preferably, we can consider using a structure like a hash table for storage. The logic is the same as before, but the space complexity here is no longer O(1), butO(n)

## Code implementation (sorting)
```java
 public boolean isAnagram(String s, String t) {
        if ((s == null) || (t == null) || (t.length() != s.length())) {
            return false;
        }
        char[] sArr1 = s.toCharArray();
        char[] sArr2 = t.toCharArray();
        Arrays.sort(sArr1);
        Arrays.sort(sArr2);
        return Arrays.equals(sArr1, sArr2);
        }

```

## Code implementation (hash)
```java
 public boolean isAnagram(String s, String t) {
        if ((s == null) || (t == null) || (t.length() != s.length())) {
            return false;
        }

        int n = s.length();

        Map<Character, Integer> counts = new HashMap<>();

        for (int i = 0; i < n; ++i) {
            counts.put(s.charAt(i), counts.getOrDefault(s.charAt(i), 0) + 1);
        }

        for (int i = 0; i < n; ++i) {
            counts.put(t.charAt(i), counts.getOrDefault(t.charAt(i), 0) - 1);
            if (counts.getOrDefault(t.charAt(i), -1) < 0) {
                return false;
            }
        }

        return true;
        }

```







