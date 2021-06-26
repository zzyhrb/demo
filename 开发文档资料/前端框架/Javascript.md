## javascript vs Jquery

## 常见方法使用

### 1 slice() 用法

```javascript
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1,3);
输出人员结果 :Orange,Lemon
```



### 2. sort() 方法

``` javascript
//sort() 方法用于对数组的元素进行排序。
返回值
对数组的引用。请注意，数组在原数组上进行排序，不生成副本。

说明
如果调用该方法时没有使用参数，将按字母顺序对数组中的元素进行排序，说得更精确点，是按照字符编码的顺序进行排序。要实现这一点，首先应把数组的元素都转换成字符串（如有必要），以便进行比较。

如果想按照其他标准进行排序，就需要提供比较函数，该函数要比较两个值，然后返回一个用于说明这两个值的相对顺序的数字。比较函数应该具有两个参数 a 和 b，其返回值如下：

若 a 小于 b，在排序后的数组中 a 应该出现在 b 之前，则返回一个小于 0 的值。
若 a 等于 b，则返回 0。
若 a 大于 b，则返回一个大于 0 的值。

//案例 （返回值 由大到小）
 this.allData.sort((a,b)=>{
            return a.value-b.value
  })




```

