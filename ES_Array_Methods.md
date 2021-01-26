<h3 style="color: yellowgreen">☆在ES6中常用数组遍历方法:</h3>

| 对象调用的方法                                           | 作用                     | 返回值                  |
| -------------------------------------------------------- | ------------------------ | ----------------------- |
| `for...of`                                               | 遍历数组 \| 不可遍历对象 | 数组值                  |
| Array.from(object, mapFunction, thisValue)               | 伪数组\|可遍历对象转数组 | 新数组                  |
| `Array.of()`                                             | 将一组值转换为数组       | 新数组                  |
| Array.copyWithin(target, start, end)                     | 将数组复制到其他位置     | 新数组                  |
| Array.find(callback(currentValue, index, arr),thisValue) | 检测数组是否含有某元素   | 符合条件元素 /undefined |
| Array.findIndex(callback(value,index,arr),thisArg)       | 检测数组是否含有某元素   | 符合条件元素(下标) / -1 |
| `Array.entries()`                                        | 遍历数组的键名和键值     | 迭代数组                |
| `Array.keys()`                                           | 遍历数组的键名           | 迭代数组（包含A-key）   |
| `Array.values()`                                         | 遍历数组键值             | 迭代数组（包含A-value） |
| Array.fill(value, start, end)                            | 给定值，填充数组         | 新数组                  |


1. for...of（不可循环对象，只能循环数组）

   ```js
   let a = [1,2,3];
   for(let value of a){
     console.log(value)  // 结果依次为1，2，3
   }
   ```

2. Array.from（伪数组和可遍历对象<包括ES6新增的数据结构Set和Map>转为真正的数组）

   ```js
   let arrayLike = {
       '0': 'a',
       '1': 'b',
       '2': 'c',
       length: 3
   };
   let arr2 = Array.from(arrayLike); // ['a', 'b', 'c']
   ```

3. Array.of（将一组值，转换为数组）

   ```js
   Array.of(3, 11, 8) // [3,11,8]
   Array.of(3) // [3]
   Array.of(3).length // 1
   ---
   这个方法的主要目的，是弥补数组构造函数Array()的不足:
   Array() // []
   Array(3) // [, , ,]
   Array(3, 11, 8) // [3, 11, 8]
   ```

4. copyWithin（在当前数组内部，将制定位置的数组复制到其他位置，会覆盖原数组项，返回当前数组。该方法，会修改当前数组。）

   ```js
   参数: target --必选 索引从该位置开始替换数组项
   　　	start --可选 索引从该位置开始读取数组项，默认为0.如果为负值，则从右往左读。
   　　　end --可选 索引到该位置停止读取的数组项，默认是Array.length,如果是负值，表示倒数
   //
   const num = [1,2,3,4,5,6,7,8,9,10];  
   const num1 = [1,2,3,4,5,6,7,8,9,10]; 
   const num2 = [1,2,3,4,5,6,7,8,9,10]; 
   
   console.log(num.copyWithin(1,3,5));  
   //[1, 4, 5, 4,  5, 6, 7, 8, 9, 10]
   console.log(num1.copyWithin(1,3)); //omitting the parameter end 
   //[1, 4,  5, 6,  7, 8, 9, 10, 9, 10]
   console.log(num2.copyWithin(1)); //omitting the parameters start and end  
   //[1, 1, 2, 3, 4, 5, 6, 7, 8, 9] 
   ```

5. find（检测数组是否含有某元素 | 返回该元素 若无返回 undefined）

   ```js
   //find (找元素) 返回值是将匹配到的第一个数组元素返回，匹配不到返回 undefined 
   let num = 99
   let arr = [1, 2, 3, 45, 99, 89, 99, 9, 10]
   let res1 = arr.find(function(item, index){
       return item === num
   })
   console.log(res1) //99
   ----- 例子2：-----
   let arr = [5,22,19,25,34];    
   let result=arr.find(x=>x>20);    
   console.log(result);  //22
   ```

6. findIndex（检测数组是否含有某元素 | 返回该元素**下标** 若无返回 -1）

   ```js
   //findIndex(找索引) 返回的满足条件的第一个数组元素的下标(索引) 匹配不到返回 -1
   let num = 99
   let arr = [1, 2, 3, 45, 99, 89, 99, 9, 10]
   let res2 = arr.findIndex(function(item, index){
       return item === num
   })
   console.log(res2) //4
   ----- 例子2：-----
   let arr=[5,22,19,25,34];    
   let result=arr.findIndex(x=>x>20);    
   console.log(result)  //1
   ```

7. entries（遍历数组的键名和键值）

   ```js
   //返回迭代数组。迭代数组中每个值 前一个是索引值作为 key， 数组后一个值作为 value。
   let arr = [1,2,3,4]
   let arr1 = arr.entries()
   for (let e of arr1) {
       console.log(e);   // [0,1] [1,2] [2,3] [3,4]
   }
   ```

8. keys（遍历数组的键名）

   ```js
   let arr = [1,2,3,4]
   let arr2 = arr.keys()
   for (let key of arr2) {
       console.log(key);   // 0,1,2,3
   }
   ```

9. values（遍历数组键值）

   ```js
   let arr = [1,2,3,4]
   let arr1 = arr.values()
   for (let val of arr1) {
        console.log(val);   // 1,2,3,4
   }
   ```

10. fill（使用给定的值，填充一个数组, 注意：填充完后会改变原数组）

  ```js
  // target --必选 待填充的元素
  // start  --可选 开始填充的位置-索引 默认为0
  // end    --可选 终止填充的位置-索引（不包括该位置) 默认是Array.length
  let colours = ["Red", "Yellow", "Blue", "Black"];  
  let show = colours.fill("Green",2,4);  
  console.log(...show);  //Red Yellow Green Green
  --- 例子2 ---
  let arr = [1,2,3,4,5]
  let arr1 = arr.fill(5)
  console.log(arr1)  // [5, 5, 5, 5, 5]
  console.log(arr)   // [5, 5, 5, 5, 5]
  --
  let arr2 = arr.fill(5,2)
  console.log(arr2)  // [1, 2, 5, 5, 5]
  let arr3 = arr.fill(5,1,3)
  console.log(arr3)  // [1, 5, 5, 4, 5]
  ```

-----

<h3 style="color: yellowgreen">☆在其他ES中常用数组遍历方法:</h3>

| 对象调用的方法                                               | 特点                     | 返回值            |
| ------------------------------------------------------------ | ------------------------ | ----------------- |
| 原始 for 循环语句                                            |                          |                   |
| ES5 - array.forEach(function(value, index, array){})         | 遍历                     | 无                |
| ES5 - array.map(function(value, index, array){})             | 遍历&返回                | 新数组            |
| ES5 - array.filter(function(value, index, array){ return 条件 }) | 过滤&返回                | 新数组            |
| ES3 - array.some(function(value, index, array){return 条件}) | 返回布尔值               | Boolean           |
| ES5 - array.every(function(value, index, array){ return 条件}) | 返回布尔值               | Boolean           |
| ES5 - array.reduce(function(sum, value, index, array) {}, 0) | 累计运算                 | 累计结果          |
| ES5 - **正向** indexOf                                       | 遍历获取对应下标         | 对比成功的下标    |
| ES5 - **逆向** lastIndexOf                                   | 遍历获取对应下标         | 对比成功的下标    |
| for...in 循环语句                                            | 遍历对象&数组            | O:key值 \| A:下标 |
| ES7 - Array.includes(element, start)                         | 判断数中是否包含给定的值 | Boolean           |


1. 原始 for 循环语句

   ```js
   //原始 for 循环语句 容易理解；缺点：比较繁琐，需要定义额外更多的变量，
   let a = [1,2,3];
   for(let i=0;i<a.length;i++){
       console.log(a[i]);  //结果依次为1，2，3
   }
   //写法改良版：
   let a = [1,2,3];
   for(let i=a.length;i--;){
       console.log(a[i]);  //结果依次为3，2，1
   }
   //性能改良版：
   let a = [1,2,3];
   for(let i = 0,len=a.length; i < len; i++) {
      console.log(a[i]);  //结果依次为1，2，3
   }
   ```

2. forEach (单纯遍历 没有返回值)

   ```js
   let arr = [1, 3, 4, 33, 2]
   let result1 = arr.forEach(function(item, index, array){
       return item > 1 //即便写了 return 也没有返回值
   })
   ```

3. map (数组循环 会将每次循环结果 保存到新数组中)

   ```js
   let arr = [1, 3, 4, 33, 2]
   let result2 = arr.map(function(item, index, array){
       return item * 2
   })
   console.log(result2)  //[2, 6, 8, 66, 4]
   -
   如果 return item < 2, 新数组为 存有 true false 的新数组
   //[true, false, false, false, false]
   ```

4. filter（将满足条件的数组元素 过滤到一个新数组中）

   ```js
   let arr = [1, 3, 4, 33, 2]
   let result3 = arr.filter(function(item, index, array){
       return item > 3
   })
   console.log(result3) //[4, 33]
   ```

5. some（**只要有一个**数组元素 **满足**，就返回 **true**(且终止循环<效率高>)）

   ```js
   // 返回值: 布尔值
   let arr = [1, 2, 3, 12, 34, 687, 2125]
   let res3 = arr.some(function(val, index){
     return val > 8
   })
   console.log(res3); //true
   ```

6. every（**只要有一个**数组元素 **不满足**，就返回 **false**(且终止循环<效率高>)）

   ```js
   // 返回值: 布尔值
   let arr = [1, 2, 3, 12, 34, 687, 2125]
   let res3 = arr.every(function(val, index){
     return val > 8
   })
   console.log(res3); //false
   ```

7. reduce（用于累计运算）

   ```js
   //参数1 是累计运算初始值，参数234 和别的方法参数一样
   let res = arr.reduce(function(sum, val, index, array){
       return sum + val
   }, 0) //默认初始值没有 则以arr[0]开始
   console.log(res);
   ```

8. indexOf（在数组循环过程中会和传入的参数比对，若比对成功，终止循环，返回对比成功的下标）

   ```js
   let a = [1,2,3];
   let b = a.indexOf(2);
   console.log(a);         // 结果为[ 1, 2, 3 ]
   console.log(b);         // 结果为1
   ```

9. lastIndexOf（lastIndexOf 方法和 indexOf 作用一致，但查找方向不同，indexOf 是正向查找，lastIndexOf 是逆向查找，找到后返回成功的下标）

   ```js
   let a = [1,2,3,1];
   let b = a.lastIndexOf(1);
   console.log(a);         // 结果为[ 1, 2, 3, 1 ]
   console.log(b);         // 结果为3
   ```

10. for...in（for...in 遍历数组时是遍历数组的下标值，而在遍历对象的时候遍历的是 key 值）

  ```js
  let a = [1,2,3];
  for(let key in a){
    console.log(key); //结果为依次为0，1，2
  }
  let b = {0:1,1:2,2:3};
  for(let key in b){
    console.log(key); //结果为依次为0，1，2
  }
  ```

11. includes（判断数中是否包含给定的值）

    ```js
    let arr = [1,2,3,4,5]
    let arr1 = arr.includes(2)  
    console.log(arr1)   // ture
    let arr2 = arr.includes(9) 
    console.log(arr2)    // false
    let arr3 = [1,2,3,NaN].includes(NaN)
    console.log(arr3)  // true
    -
    //与indexOf()的区别：
    1 indexOf()返回的是数值，而includes()返回的是布尔值
    2 indexOf() 不能判断NaN，返回为-1 ，includes()则可以判断
    ```

-

Reference：

1. **夜里的太阳** *《ES5和ES6数组遍历方法详解》* - segmentfault

   https://segmentfault.com/a/1190000010203337

2. **热爱前端的17号诶** *《最新数组方法（包括es6）》* - cnblogs

3. *ES6 Array methods* https://www.javatpoint.com/es6-array-methods
