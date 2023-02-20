# Search-Insert-Position
## 35. Search Insert Position

### Question:
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

```
Example 1:

Input: [1,3,5,6], 5
Output: 2

Example 2:

Input: [1,3,5,6], 2
Output: 1

Example 3:

Input: [1,3,5,6], 7
Output: 4

Example 4:

Input: [1,3,5,6], 0
Output: 0
```

### Thinking:

```Java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int len = nums.length;
        if(len == 0 || target <= nums[0]) return 0;
        int i = 0;
        for(i = 0; i < len - 1; i++){
            if(target > nums[i] && target <= nums[i+1])
                return i+1;
        }
        return len;
    }
}
```

### 二刷
还是出现了一次error， [1], 1。

```Java
class Solution {
    public int searchInsert(int[] nums, int target) {
        if(nums.length == 0 || nums[0] >= target) return 0;
        for(int i = 0; i < nums.length - 1; i++){
            if(nums[i] < target && nums[i + 1] >= target) return i + 1;
        }
        return nums.length;
    }
}
```

### Third Time
* Method 1: binary search AC 100%
	```Java
	class Solution {
		public int searchInsert(int[] nums, int target) {
			int low = 0, high = nums.length - 1;
			return bs(nums, low, high, target);
		}
		private int bs(int[] nums, int low, int high, int target){
			int mid = low + (high - low) / 2;
			if(target > nums[nums.length - 1]) return nums.length;
			if(mid == low || mid == high){
				if(target > nums[low]) return high;
				else return low;
			}
			if(nums[mid] == target) return mid;
			else if(nums[mid] > target) return bs(nums, low, mid, target);
			else return bs(nums, mid, high, target);
		}
	}
	```
