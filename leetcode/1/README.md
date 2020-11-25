## 1

**方法一：枚举**

两次循环，每次分别取不同的数。相加判断。

时间复杂度O(N^2)

空间复杂度O(1)

```
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
  for (let i = 0; i < nums.length - 1; i++) {
    const firstPicked = nums[i];
    for (let j = i + 1; j < nums.length; j++) {
      const secondPicked = nums[j]
      if (firstPicked + secondPicked ===  target) return [i, j]
    }
  }
};
```

**方法二：哈希表**

循环一次，每次哈希表记录`[target - 当前的数值]`: [当前的下标]，把每个数值丢到哈希表里面匹配。如果命中，可以拿到之前的索引下标。

时间复杂度O(N)

空间复杂度O(N)


```
var twoSum = function (nums, target) {
  const map = {};
  for (let i = 0; i < nums.length; i++) {
    const val = nums[i];
    if (val.toString() in map) {
      return [map[val], i]
    }
    map[target - val] = i;
  }
};
```