## 283.移动零

**方法一：**

使用双指针，左指针指向当前已经处理好的序列的尾部，右指针指向待处理序列的头部。

右指针不断向右移动，每次右指针指向非零数，则将左右指针对应的数交换，同时左指针右移。

注意到以下性质：

1. 左指针左边均为非零数；

2. 右指针左边直到左指针处均为零。

可以演化如下：
```
[0,1,0,3,12]

[0,1,0,3,12] left 0 right 0

[0,1,0,3,12] left 0 right 1

[1,0,0,3,12] left 1 right 2

[1,3,0,0,12] left 2 right 3

[1,3,12,0,0] left 3 right 4
```

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int len = nums.length;
        int left = 0;
        int right = 0;
        for (right = 0; right < len; right ++) {
            int val = nums[right];
            if (val != 0) {
                swap(nums, right, left);
                left++;
            }
        }
    }
    public void swap (int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```