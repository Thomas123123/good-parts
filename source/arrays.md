# <center>陣列 Array<center>
----------------
> 陣列是記憶體的一種線性分配。 組件根據計算偏移量(整數)而存取。 但很可惜，<font color = 'red'>**javascript沒有類似陣列的東西**<font>

javascript提供了**類似**陣列性格的object，它把陣列索引轉換成字串，比實際陣列慢，但更方便使用。  



### **陣列實字 array literal**

array literal提供一種建立新陣列更便利方式，index從0開始依序往後加

``` js
var arr = [1,2,3,4] // array literal寫法
arr[0]  // 1
arr[1]  // 2
arr[2]  // 3
arr[3]  // 4
```

array跟object一樣，允許多種type混合

``` js
var arr = ['string',123,true,null,undefined,[1,2],{"name":"thomas"},NaN];
```

### **length方法**

javascript陣列的length不會出現陣列上限的錯誤，如果你儲存的元素大於等於目前length的index，則length將補齊不足的index

``` js
var arr = [] ;
arr[10000] = 1 ;
arr.length       //10001
```

### **刪除 delete**

既然javascript的array其實是object，delete運算子即可用於移除陣列裡的元素

``` js
var arr = [1,2,3,4,5] ;
delete arr[2] ;

arr ;              // [1, 2, undefined × 1, 4, 5]
arr.length ;       // 5
```

不過這樣做會讓array留下破洞，我們通常會想把陣列元素補滿補齊，這時就可以用splice()，它可以刪除某些元素並以其他元素代替。
* splice() 須輸入兩個參數，第一個參數是欲刪除元素的index，第二個參數是欲刪除數量

``` js
var arr = [1,2,3,4,5] ;
arr.splice(2,1) ;       

arr ;                     // [1, 2, 4, 5]
arr.length ;              // 4
```

### **列舉 reflect**

要取陣列元素的值可以用for in (因為陣列是object 所以也有for in的方法)
* 不過good parts推薦使用for loop做這件事情，因為for in會有順序不依的現象發生

``` js
var arr = [1,2,3,4,5]
var i = 0
for (i=0 ; i<= arr.length ; i++){
  console.log(arr[i]) ;
}
 // 1
 // 2
 // 3
 // 4
 // 5
```

### **困惑之處**

javascript程式的常見錯誤之一，**<font color = "red">該用陣列的時候用物件，該用物件的時候用陣列<font>**。  

* **規則簡單 : 當property name是連續整數就用陣列 ; 除此之外皆用物件**

javascript沒有很好的陣列與物件區分機制。所以硬要區分的話，也是有辦法

``` js
var arr = [] ;
var obj = {} ;
var is_array = function (value) {
    return value &&
        typeof value === 'object' &&       
        typeof value.length === 'number' &&
        typeof value.splice === 'function'
};
is_array(arr) ;    // true
is_array(obj) ;    // false
```

### **陣列維度**

javascirpt陣列通常並未初始化(initialization)，如果配置一個新陣列，它將是空的。

所以如果想配置每個元素都以已知值開始的陣列(例如0)，我們可以嘗試用以下陣列配置

``` js
var dimen = function (dimension, initial)
{
  var a = [] , i ;
    for (i = 0 ; i < dimension ; i++)
    {
      a[i] = initial ;
    }
  return a ;
}

dimen(10,0)      // [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

javascript可具有以陣列組成的陣列 :  

``` js
var arr = [
    [1,2,3],
    [4,5,6],
    [7,8,9]
]

arr[1][2]     // 6
```

所以如果想配置每個元素都以已知值開始的二維陣列(例如0)，我們可以嘗試用以下陣列配置  

``` js
var arr = function (m, n, initial) {
    var a, i, j, mat = [];
    for (i = 0; i < m; i += 1) {
        a = [];
        for (j = 0; j < n; j += 1) {
            a[j] = initial;
        }
        mat[i] = a;
    }
    return mat;
};

arr(4,4,0)
```

