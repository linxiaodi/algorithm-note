## 180

**第一种**

别人说的太好了，没啥好补充的：https://leetcode-cn.com/problems/rotate-array/solution/xuan-zhuan-shu-zu-yuan-di-huan-wei-xiang-xi-tu-jie/

```ts
function rotate(nums: number[], k: number) {
  k  = k % nums.length;
  let count = 0; // 交换位置的次数
  for (let start = 0; count < nums.length; start++) {
    let cur = start;
    let pre = nums[cur];
    do {
      let nextIndex = (cur + k) % nums.length;
      let tem = nums[nextIndex]
      nums[nextIndex] = pre;
      pre = tem;
      cur = nextIndex;
      count ++;
    } while (start !== cur)
  }
}

```

**第二种:数组反转**

第一次：反转 所有数字
第二次：反转 0 到 k
第三次：反转 k 到 nums.length - 1

```ts
function rotate(nums: number[], k: number) {
  k  = k % nums.length;
  function reverse(nums: number[], start: number, end: number) {
    while (start < end) {
      let tem = nums[start]
      nums[start] = nums[end]
      nums[end] = tem
      start ++
      end --
    }
  }
  reverse(nums, 0, nums.length - 1);
  reverse(nums, 0, k - 1);
  reverse(nums, k, nums.length - 1);
}

```