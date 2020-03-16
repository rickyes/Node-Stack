## 二分搜索 （ binary search ）

一种基于 `有序不重复数组` 查找特定元素的搜索算法。

- 原理

> 从中间元素开始搜索，比较和需要和查找元素的大小，如果比要查询的元素大/小，则下次从低位到中间位/中间位到高位之间继续寻找，一直查找到和需要查询的元素相等。

- 代码实现

``` js

const search = (list, item) => {
  let low = 0;
  let high = list.length - 1;
  while (low <= high) {
    // 取中间位置索引, 防止溢出
    const mid = low + ((high - low) >> 1);
    if (list[mid] > item) {
      // 大于查询的元素，中间位减一，查找范围改为 低位 <-> 中间位-1
      high = mid - 1;
    } else if (list[mid] < item) {
      // 小于查询的元素，中间位加一，查找范围改为 中间位+1 <-> 高位
      low = mid + 1;
    } else {
      // 等于查询的元素，则返回当前索引
      return mid;
    }
  }
  // 检索不到返回 -1
  return -1;
}
```

#### 寻找数组中最大元素

> 数组满足规则 A[0] < A[1] ... < A[N] > A[N-1] > A[N-2]

``` js
const searchMax = (list) => {
  let low = 0;
  let high = list.length - 1;
  while (low <= high) {
    let mid = low + ((high - low) >> 1);
    if ((list[mid] > list[mid - 1]) && (list[mid] < list[mid + 1])) {
      low = mid + 1;
    } else if ((list[mid] > list[mid - 1]) && (list[mid] > list[mid + 1])) {
      return mid;
    } else {
      high = mid - 1;
    } 
  }
  return -1;
};
```