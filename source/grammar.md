# <center>文法 Grammar<center>
----------------

### **空格 Whitespace**  

``` js
varthat=this ;    // false
var that=this ;   // true
var that = this ; // true
```
var與that間的空格不可移除，但其他空格若拿掉也無所謂.

### **註解 annotation**

##### javascript註解形式有兩種 :  
區塊使用 /\*content\*/  
單行使用 //content  
  
* **區塊註解若遇regexp 需小心使用**  

``` js
/*
    var rm_a = /a*/.match(s);  //註解區塊不正確
*/
```

### **名稱 Name**  
  
<font color = "red">名稱不能用<strong>javscript保留字<strong>來命名<font>  
若不確定是否有不小心用到保留字，可在名稱前加上底線
  
#### <center>保留字 Reserved words</center>
|abstract|boolean|break|byte|case|
|:------:|:------:|:------:|:------:|:------:|
|catch|char|class|const|continue|
|debugger|default|delete|do|double|
|else|enum|export|extends|false|

名稱大多用於敘述(statement)、變數(variable)、參數(parameter)、特性名稱(property name)、運算子(operator)、和標籤(label)。  
  
### **數值 Number**

javascript只有一個數值(<font color = "red">number<font>)型別。  
每配置一個number就需配置64bit(8個byte)，相當於java的double type一樣大。  
但也因只有一種type，1跟1.0是相等的值，完全可以避免<font color="red">短整數溢位<font>。  
  
### **字串 String**

javascript建立的時候，Unicode還只是16位元的字元集，所以javascript所有字元都為16位元長度範圍
  
\ (反斜線) 為轉義字元，可處理字串內部一些特定符號或字母的轉義  
``` js
var str = "\n"   // 換行
var str = "\/"   // "/"
var str = "\u0041"  // "A" 
```
  
字串製造後就再也無法改變，但可利用 "+" 運算子將字串與字串相接，創造出新字串
``` js
"c" + "a" + "t" === "cat"  // true
```
  
### **敘述 Statements**
**敘述句**  

``` js
var a = 1 , b = 2 ;
``` 
  
**<font color = "red">敘述多半由上往下執行<font>**。執行順序能使用條件句敘述(if和switch)、迴圈敘述(while、for、do)、中斷性敘述(break、return、throw)及函式呼叫(function invocation)而異動。  
  
區塊是一組使用大括號( {} )圍起的敘述。**<font color="red">區塊建立新的scope在ES5裡不會產生獨立作用域<font>**，所以變數應該定義在函式頂端。
  
### **迴圈敘述句**  

---------------------

#### **if迴圈**
if敘述會根據運算式的值改變程式流向。若運算式結果為真，則執行then區塊，否則執行else分支

以下為falsy的值 : 
* false
* null
* undefined(未定義)
* "" (空字串)
* 0
* NaN 

**<font color = "red">所有其他值都被視為true，包括ture本身，字串"false"，"0"等。<font>**  

#### **switch迴圈**  
switch敘述呈現多向分支。運算式產生的結果去找到完全相符的case並執行該case下的敘述，若無相符案例則執行default敘述。  
  
**case子句後的敘述應為中斷性敘述，以免執行到下一個case**  

#### **while迴圈**
while敘述表達一個簡單迴圈。運算式結果為true，則執行區塊碼，運算式結果為false,則迴圈中斷。  

#### **for迴圈**

for迴圈為較複雜的迴圈。它有兩種形式  

* 一種為透過三個選用子句控制 : 初始句(initialization)、條件句(condition)、遞增句(increment)。
  首先完成初始句，指迴圈變數的初始化，再來判斷條件句，檢查迴圈變數是否符合條件，若為true則執行區塊碼，為false則中斷迴圈(**<font color = "red">\*若條件句無條件設定將回傳true形成無限迴圈**</font>)
  ，最後執行遞增句，當區塊碼執行完後再回到迴圈判斷條件句直到結果為false中斷迴圈。  
* 另一種為for in ，可列出物件資訊，每輪迴圈均把物件屬性的名稱指派給變數。  

``` js
var obj = {name : "thomas" , age : 18}
for (var a in obj){
  console.log(obj[a]);
}
// thomas
// 18
```

#### **do迴圈**  
  
do迴圈很像while，差異在於會<font color = "red">**先直接執行區塊碼，再判斷運算式結果**<font>，所以至少會執行一次區塊碼。  

---------------

#### **try敘述**  

try敘述執行一個區塊碼，並捕捉任何由區塊丟出來的exception。 catch子句定義了**接收exception的變數**。  

#### **throw敘述**

throw敘述負責發出exception。 當try區塊執行到throw時，控制權將交給catch句。

``` js
try{
throw "我錯了";
}catch(error){
console.log(error);
};
// 我錯了
```

可以透過一些方式去捕捉錯誤  

``` js
var x = 3 ;
try
  {
   if(x=="")     throw "empty";
   if(isNaN(x))  throw "not a number";
   if(x>10)      throw "too high";
   if(x<5)       throw "too low";
  }
catch(error)
  {
   console.log(error);
  }
// "too low"
```

#### **return敘述**

return敘述使函式提早回傳。 <font color = "red">**若未指定return裡的運算式，則回傳undefined。**<font>  

### **運算式 Expresstions**

運算式包括了 實字值(literal value，例如一個字串或數字)、內建值(true、false、null、undefined、NaN、Infinity)、new後接呼叫運算式、delete後接精確運算式、以括號圍起的運算式、接有字首詞運算子的運算式，或式接下列可能性的運算式；  
* 嵌入式運算子和其他運算式
* ? 三元運算子後接另一個運算式，接下來是 : ，再接上另一個運算式
* 一個呼叫式  
* 一個精確式  

#### 運算子優先順序  

最上面為優先順序最高的運算子，往下以此類推

|運算子代表號|中文解釋|
|:----:|:----:|
|.、[]、()|精確與呼叫|
|delete、new、typeof、+、-、!|單元運算子|
|*、/、%|乘、除、餘數|
|+、-|加/相連、減|
|>=、<=、>、<|不相等|
|===、!==|相等|
|&&|邏輯運算元 AND|
|?、:|三元|

#####字首運算子

|運算子符號|用途|
|:----:|:----:|
|typeof|顯示type|
|+|用於數值|
|-|負號|
|!|邏輯NOT|

* typeof有六種型態 : 'number'、'string'、'boolean'、'undefined'、'function'、'object'。
**<font color = "red">會遇到一種情況，運算元如果為陣列或null，則會顯示object<font>**  

#### **實字 Literal**

|實字種類|實字代表符號|實字寫法範例|
|:----:|:----:|:----:|
|數值實字||a = 1|
|字串實字|"  "  (一對雙引號或單引號)|str = "hello"|
|物件實字|{}  (大括號)|obj = {}|
|陣列實字|[]  (中括號)|arr = []|
|函式|(){}|function fun(){}|
|正規運算式|//|/[0~9]/gi|
