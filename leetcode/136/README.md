## 136. 只出现一次的数字

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

**方法一：位运算**

位运算能极大地减少空间的使用。

复习一下位运算

按位与： a & b

| a | b | a & b |
| -- | -- | -- |
| 0 | 0 | 0 |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 1 | 1 |

按位或：a | b

| a | b | a \| b |
| -- | -- | -- |
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 1 |

按位异或：a ^ b

| a | b | a ^ b |
| -- | -- | -- |
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 0 |

一般用于多选和场景判断。

按位非：NOT a

| a | NOT a |
| -- | -- |
| 0 | 1 |
| 1 | 0 |

假设有符合属性 CUTE ('0001')， SMART ('0010'), SMALL ('0100')，如果一个动物既有 CUTE, SMART, SMALL 则properties: '01110'。

```javascript
const CUTE = parseInt('0001', 2)
const SMART = parseInt('0010', 2)
const SMALL = parseInt('0100', 2)

class Cat {
  constructor(properties) {
    this.properties = properties || 0;
  }
  setCute() {
    this.properties |= CUTE
  }
  clearCute() {
    this.properties &= (~CUTE)
  }
  isCute() {
    return (this.properties & CUTE) !== 0;
  }
  setSmart() {
    this.properties |= SMART
  }
  clearSmart() {
    this.properties &= (~SMART)
  }
  isSmart() {
    return (this.properties & SMART) !== 0;
  }
  // ...
}
```


```java
class Solution {
    public int singleNumber(int[] nums) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum = sum ^ nums[i];
        }
        return sum;
    }
}
```