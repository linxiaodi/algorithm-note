## 206


**方法一：双指针**

[1 -> 2 -> 3 -> 4] left = null right = 1, 1.next = null

[1 <- 2 -> 3 -> 4] left = 1 right = 2, 2.next = 1

[1 <- 2 <- 3 -> 4] left = 2 right = 3, 3.next = 2

[1 <- 2 <- 3 <- 4] left = 3 right = 4, 4.next = 3


```js
var reverseList = function(head) {
    let left = null;
    let right = head
    while (right) {
        let temp = right.next
        right.next = left
        left = right
        right = temp
    }
    return left
};
```

**方法二：递归**

递归比较绕，递到最后一层，往外的时候翻转当前的前驱节点。

[1, 2, 3, 4]

-- 1.next.next = 1, 1.next = null

reverseList 2 -- 2.next.next = 2 === 3.next = 2, 2.next = null

reverseList 3 -- 3.next.next = 3 === 4.next = 3, 3.next = null

reverseList 4



```js
var reverseList = function(head) {
    if (!head || head.next === null) {
        return head
    }
    let hasReverseNode = reverseList(head.next)
    // 翻转
    head.next.next = head
    head.next = null
    return hasReverseNode
};
```