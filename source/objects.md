# <center>物件 Object<center>
----------------

>* javascript 基本的type，除了number、string、boolean、null、undefined，其他所有type都為object。
>* object 是 屬性的集合，屬性具有name跟value。  

### **物件實字 object literal**

object literal提供一種建立新物件更便利方式

``` js
var obj = { "name" : "thomas" , "age" : 18} ; // object literal寫法
```

object裡可以是number、string、boolean、array、object

``` js
var obj = {
"num" : 1 ,
"str" : "string" ,
"boo" : true ,
"array" : [1,2,3,4] ,
"obj2" : 
	{
    	"a" : 1 ,
		"b" : "abc"
	}
}
```

### **擷取 Interception**

從object要取值有兩種方法
* 用 中括號[" "] 圍起一段字串運算式
* **用 點. 指定object.name 也可取值    (推薦用這種，較簡潔易懂)**

``` js
var obj = { "name" : "thomas" , "age" : 18}
obj["name"]  // "thomas"
obj.name     // "thomas"
```

若對於不存在成員取值，會產生undefined

``` js
var obj = { "name" : "thomas" , "age" : 18}
obj.weight     // undefined
```

### **更新 update**

物件裡的value可重新assign，但如果object裡已有該屬性名稱，則會replace value。

``` js
var obj = { "name" : "thomas" , "age" : 18} ;
obj.name = "simon"  ;

obj.name  ;    //simon
```

若物件裡找不到要賦值的屬性名稱，則會增加到物件裡

``` js
var obj = { "name" : "thomas" , "age" : 18} ;
obj.weight = "60" ;     

obj  ;      //Object {name: "thomas", age: 18, weight: "60"}
```

### **參考 reference**

物件不會被複製。

``` js
var a = {name : "thomas" , age : 18} ;
var b = a ;
b.name = "simon" ;
 
a.name ;       //simon
```

``` js
var a = {} , b = {} , c = {} ;  //各自指向不同位置
var a = b = c = {} ;            //均指向同一個位置
```

### **原型 prototype**

* 每個object都連繫到一個object.prototype，由此可繼承屬性。

對原型的聯繫，再更新時沒有效用，當我們改變物件時，物件的原型並未受到影響。

* 原型的關係是動態關係。 如果在某個prototype修改一個屬性，所有以它為基礎的物件都會立刻看到修改後的樣子。


### **反映 reflect**

typeof運算子在判斷特性的型別時大有幫助 :

``` js
var obj = {
"num" : 1 ,
"str" : "string" ,
"boo" : true ,
"array" : [1,2,3,4] ,
"obj2" : 
	{
    	"a" : 1 ,
		"b" : "abc"
	}
}
typeof obj.num //"number"
typeof obj.str //"string"
typeof obj.boo //"boolean"
typeof obj.a   //"undefined"
```

但由於prototype chain關係，也會不小心把Object.prototype的方法一起檢視 

``` js
var typeof obj.toString  //"function"
```

所以為了避免這種問題發生，可用hasOwnProperty()來解決，hasOwnProperty()方法不會檢查prototype chain。

``` js
obj.hasOwnProperty("num") ;         //true
obj.hasOwnProperty("toString") ;    //false
```

### **列舉 reflect**

可利用for in來檢視object裡的屬性明細(name和value)，

``` js
var obj = { "name" : "thomas" , "age" : 18 , "weight" : 60} ;
var name ;
for (name in obj)
{
  if (typeof obj[name] !== 'function')
    {
	console.log(name + ":" + obj[name]);
    }   
}
// name:thomas
// age:18
// weight:60
```

但for in無法保證按照順序印出，若想要確定順序，則可用for取代for in

### **刪除 delete**

delete運算子可從物件中移除屬性

``` js
var obj = { "name" : "thomas" , "age" : 18}
delete obj.name

obj.name  // undefined
obj       // Object {age: 18}
```
