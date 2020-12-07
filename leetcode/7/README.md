## 7

**方法一：**

刚开始做的时候思路是把整个整数翻转成字符串，做2个`flag`(一个判断翻转是否到非0，另一个判断符号)。

用循环取模，取出最后一位(`x % 10`)，在最后把当前位给去掉(`parseInt(x / 10)`)，每次进行累加，并且不需要去做非0判断的`flag`。除此之外，有个边界条件判断[-2147483648, 2147483647]。判断大于小于还比较简单，难在判断最后的个位数，如果假设当前最大值是21478364，此时如果pop = 9就会形成 `21478364*10 + 9`爆栈，所以限定在7以内，如果当前最小值是 -21474836，此时如果pop = -9。就会导致 `-21474836 * 10 - 9` 也会爆栈。




```js
/**
 * @param {number} x
 * @return {number}
 */
function reverse(x) {
    let acc = 0
    // 2147483647
    // -2147483648
    const MAX_NUM = 214748364
    const MIN_NUM = -214748364

    

    while (x!==0) {
        let pop = x % 10
        if (acc > MAX_NUM || (acc === MAX_NUM && pop > 7)) {
            return 0;
        }

        if (acc < MIN_NUM || (acc === MIN_NUM && pop < -8)) {
            return 0;
        }
        
        acc = acc * 10 + pop
        x = parseInt(x / 10)
    }
    return acc
}
```