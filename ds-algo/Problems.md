
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
//Time Complexity O(nlgn)
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
//Time Complexity O(n)
//space complexity here is  butO(n)
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

# Find the median of two positively ordered arrays

Given two positive (small to large) arrays of size m and n, nums1 and nums2. Please find the median of these two positive arrays, and the time complexity of the algorithm is required to be O(log(m + n)). You can assume that nums1 and nums2 will not be empty at the same time.

## What is the median of an array
The middle element is found by ordering all elements in sorted order and picking out the one in the middle (or if there are two middle numbers, taking the mean of those two numbers).

```log
Example 1 :
nums1 = [ 1 , 3 ]
nums2 = [2]
    
The median is 2.0
    
Example 2 :
nums1 = [ 1 , 2 ]
nums2 = [3, 4]
    
The median is ( 2  +  3 ) / 2  =  2.5

```

## Problem analysis

## Code

```java
 /* Time complexity is O(log(min(x,y))
 * Space complexity is O(1)
  */
public class MedianOfTwoSortedArrayOfDifferentLength {

    public double findMedianSortedArrays(int input1[], int input2[]) {
        //if input1 length is greater than switch them so that input1 is smaller than input2.
        if (input1.length > input2.length) {
            return findMedianSortedArrays(input2, input1);
        }
        int x = input1.length;
        int y = input2.length;

        int low = 0;
        int high = x;
        while (low <= high) {
            int partitionX = (low + high)/2;
            int partitionY = (x + y + 1)/2 - partitionX;

            //if partitionX is 0 it means nothing is there on left side. Use -INF for maxLeftX
            //if partitionX is length of input then there is nothing on right side. Use +INF for minRightX
            int maxLeftX = (partitionX == 0) ? Integer.MIN_VALUE : input1[partitionX - 1];
            int minRightX = (partitionX == x) ? Integer.MAX_VALUE : input1[partitionX];

            int maxLeftY = (partitionY == 0) ? Integer.MIN_VALUE : input2[partitionY - 1];
            int minRightY = (partitionY == y) ? Integer.MAX_VALUE : input2[partitionY];

            if (maxLeftX <= minRightY && maxLeftY <= minRightX) {
                //We have partitioned array at correct place
                // Now get max of left elements and min of right elements to get the median in case of even length combined array size
                // or get max of left for odd length combined array size.
                if ((x + y) % 2 == 0) {
                    return ((double)Math.max(maxLeftX, maxLeftY) + Math.min(minRightX, minRightY))/2;
                } else {
                    return (double)Math.max(maxLeftX, maxLeftY);
                }
            } else if (maxLeftX > minRightY) { //we are too far on right side for partitionX. Go on left side.
                high = partitionX - 1;
            } else { //we are too far on left side for partitionX. Go on right side.
                low = partitionX + 1;
            }
        }

        //Only we we can come here is if input arrays were not sorted. Throw in that scenario.
        throw new IllegalArgumentException();
    }

    public static void main(String[] args) {
        int[] x = {1, 3, 8, 9, 15};
        int[] y = {7, 11, 19, 21, 18, 25};

        MedianOfTwoSortedArrayOfDifferentLength mm = new MedianOfTwoSortedArrayOfDifferentLength();
        mm.findMedianSortedArrays(x, y);//11.0
    }
}

```

## Code (Brute Force approach)

```java
  public static double findMedianSortedArraysBruteForceApproach(int[] firstArray, int[] secondArray) {
        int firstArrayLength = firstArray.length;
        int secondArrayLength = secondArray.length;

        int[] combinedArray = new int[firstArrayLength + secondArrayLength];
        int k = 0;
        for (int i : firstArray) {
            combinedArray[k++] = i;
        }

        for (int i : secondArray) {
            combinedArray[k++] = i;
        }

        Arrays.sort(combinedArray);
        double median;
        if (combinedArray.length % 2 == 0) {
            median = combinedArray[combinedArray.length / 2];
        } else {
            median = (combinedArray[(combinedArray.length - 1) / 2]
                    + combinedArray[(combinedArray.length + 1) / 2]) / 2;
        }

        return median;

    }
```

Ref : 
- https://github.com/sunilsoni/interview-notes-code/blob/master/src/main/java/com/interview/notes/code/LeetCode/MedianOfTwoSortedArrayOfDifferentLength.java
- https://github.com/MisterBooo/LeetCodeAnimation/blob/master/0004-median-of-two-sorted-arrays/Article/0004-median-of-two-sorted-arrays.md



# Subarray Sum Equals K

Given an array of integers nums and an integer k, return the total number of continuous subarrays whose sum equals to k.


## Problem analysis

```log
Example 1:

Input: nums = [1,1,1], k = 2
Output: 2

```
```log
Example 2:

Input: nums = [1,2,3], k = 3
Output: 2
```

## Code - Optimization by Hashmap
```java
    public int subarraySumOptimizationHashmap(int[] nums, int k) {
        int count = 0, sum = 0;
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);

        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum - k))
                count += map.get(sum - k);
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
}

```




## Code - Brute Force approach

```java
   public int subarraySum(int[] nums, int k) {
        int count = 0;

        int[] sum = new int[nums.length + 1];
        sum[0] = 0;
        for (int i = 1; i <= nums.length; i++)
            sum[i] = sum[i - 1] + nums[i - 1];

        for (int start = 0; start < sum.length; start++) {
            for (int end = start + 1; end < sum.length; end++) {
                if (sum[end] - sum[start] == k)
                    count++;
            }
        }

        return count;
    }

```



Ref : https://leetcode.com/problems/subarray-sum-equals-k/discuss/803317/Java-Solution-with-Detailed-Explanation


