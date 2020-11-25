## 36

**方法一：**

9个横向的哈希表，9个纵向的哈希表，9宫格矩阵哈希表，每个元素都会对应一个横向的、纵向的哈希表，矩阵哈希表需要根据横向、纵向的索引去确定在哪一块。

`box = boxs[ceil(columnIndex / 3)][ceil(rowIndex / 3)]`

```
var isValidSudoku = function (board) {
  const rowMaps = [];
  const columnMaps = [];
  const boxMaps = [];
  for (let i = 0;i < 9;i++) {
    rowMaps.push(new Set())
    columnMaps.push(new Set())
  }

  for (let i = 0;i < 3;i++) {
    boxMaps.push([new Set(), new Set(), new Set()])
  }

  for (let row = 0; row < 9; row++) {
    for (let column = 0; column < 9; column++) {
      const boxColumn = Math.ceil((column + 1) / 3) - 1;
      const boxRow = Math.ceil((row + 1) / 3) - 1;
      // 找到第几个Box
      const hintBoxSet = boxMaps[boxRow][boxColumn];
      const hintRowSet = rowMaps[row];
      const hintColumnSet = columnMaps[column];
      const value = board[row][column];
      console.log(value)
      if (value !== '.') {
        if (hintBoxSet.has(value) || hintRowSet.has(value) || hintColumnSet.has(value)) {
          return false;
        }
        hintBoxSet.add(value);
        hintRowSet.add(value);
        hintColumnSet.add(value);
      }
    }
  }
  return true;
};
```