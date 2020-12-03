## 104

**方法一：递归**

`max(l,r)+1`

每个节点比较左右最大深度


```js
var maxDepth = function(root) {
  if (!root) return 0;
  return 1 + Math.max(maxDepth(root.left), maxDepth(root.right))
};
```



**方法二：广度遍历优先**


假设有树
```
      [3]             <- currentTarget = [3]
    [9] [20]          <- currentTarget = [9, 20]
[10]   [15] [7]       <- current = [10, 15, 7]
```

`currentTarget`为每层树的所有节点，每次遍历。

遍历currentTarget的所有子节点，把子节点记录到新的`newCurrentTarget`下次切换到`currentTarget`


```js
var maxDepth = function(root) {
  if (!root) return 0;
  let currentTarget = [root];
  let count = 0;
  while (currentTarget.length > 0) {
    let size = currentTarget.length
    let newCurrentTarget = [];
    while (size > 0) {
      let current = currentTarget[size - 1];
      if (current.left) {
        newCurrentTarget.push(current.left)
      }
      if (current.right) {
        newCurrentTarget.push(current.right)
      }
      size --;
      if (size === 0) {
          currentTarget = newCurrentTarget
      };
    }
    count++
  }
  return count;
}
```