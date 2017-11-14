# Array methods

Arrays cung cấp nhiều methods giúp ta làm việc dễ hơn, trong chương này ta sẽ phân nhóm chúng.

[cut]

## Add/remove items

Ta đã biết các methods làm việc với đầu và cuối Array:

- `arr.push(...items)` -- adds items to the end,
- `arr.pop()` -- extracts an item from the end,
- `arr.shift()` -- extracts an item from the beginning,
- `arr.unshift(...items)` -- adds items to the beginning.

Đây là một số methods khác.

### splice

Làm sao để xóa một element từ array?

Array là một objects, nên ta có thể dùng `delete`:

```js run
let arr = ["I", "go", "home"];

delete arr[1]; // remove "go"

alert( arr[1] ); // undefined

// now arr = ["I",  , "home"];
alert( arr.length ); // 3
```

Element bị xóa nhưng array vẫn có 3 elements, ta có thể thấy `arr.length == 3`.

Đó là tự nhiên, bởi vì `delete obj.key` xóa value theo `key`. Nhưng với array ta muốn xóa element một cách thực sự.

Method [arr.splice(str)](mdn:js/Array/splice) cho phép ta add/remove/insert các element vào array.

Cú pháp:

```js
arr.splice(index[, deleteCount, elem1, ..., elemN])
```

Bắt đầu tự vị trí `index`: removes `deleteCount` elements và sau đó inserts `elem1, ..., elemN` vào đó. Trả về một array bị remove.

Xem các ví dụ:

```js run
let arr = ["I", "study", "JavaScript"];

*!*
arr.splice(1, 1); // from index 1 remove 1 element
*/!*

alert( arr ); // ["I", "JavaScript"]
```

Dễ phải ko, bắt đầu từ vị trí index `1` xóa đi `1` element.

Ví dụ tiếp:

```js run
let arr = [*!*"I", "study", "JavaScript",*/!* "right", "now"];

// remove 3 first elements and replace them by another
arr.splice(0, 3, "Let's", "dance")

alert( arr ) // now [*!*"Let's", "dance"*/!*, "right", "now"]
```

Ở đây ta thấy `splice` trả về một array gồm các element bị xóa:

```js run
let arr = [*!*"I", "study",*/!* "JavaScript", "right", "now"];

// remove 2 first elements
let removed = arr.splice(0, 2);

alert( removed ); // "I", "study" <-- array of removed elements
```

`splice` method có thể dùng để insert element. Ta set `deleteCount` bằng `0`:

```js run
let arr = ["I", "study", "JavaScript"];

// from index 2
// delete 0
// then insert "complex" and "language"
arr.splice(2, 0, "complex", "language");

alert( arr ); // "I", "study", "complex", "language", "JavaScript"
```

````smart header="Index âm được chấp nhận"
Đây là một array methods khác, index âm được chấp nhận. Chúng xác định vị trí bắt đầu từ cuối array:

```js run
let arr = [1, 2, 5]

// from index -1 (one step from the end)
// delete 0 elements,
// then insert 3 and 4
arr.splice(-1, 0, 3, 4);

alert( arr ); // 1,2,3,4,5
```
````

### slice

Method [arr.slice](mdn:js/Array/slice) đơn giản hơn `arr.splice`.

Cú pháp:

```js
arr.slice(start, end)
```

Trả về một array chứa các element từ index `"start"` đến `"end"` (không bao gồm `"end"`). Cả `start` và `end` có thể âm, trường hợp này sẽ tính từ cuối array.

Nó giống `str.slice`, nhưng trả về subarrays thay vì substrings.

Ví dụ:

```js run
let str = "test";
let arr = ["t", "e", "s", "t"];

alert( str.slice(1, 3) ); // es
alert( arr.slice(1, 3) ); // e,s

alert( str.slice(-2) ); // st
alert( arr.slice(-2) ); // s,t
```

### concat

Method [arr.concat](mdn:js/Array/concat) kết hợp các array với nhau thành một.

Cú pháp:

```js
arr.concat(arg1, arg2...)
```

Có thể chứa nhiều tham số arg - với bất kỳ giá trị nào.

Kết quả là một array mới bao gồm `arr`, tiếp theo là `arg1`, `arg2` ...

Nếu `arg` là một array hoặc có `Symbol.isConcatSpreadable` property, thì tất cả element của nó sẽ được copy. Ngược lại sẽ copy chính `arg` đó.

Ví dụ:

```js run
let arr = [1, 2];

// merge arr with [3,4]
alert( arr.concat([3, 4])); // 1,2,3,4

// merge arr with [3,4] and [5,6]
alert( arr.concat([3, 4], [5, 6])); // 1,2,3,4,5,6

// merge arr with [3,4], then add values 5 and 6
alert( arr.concat([3, 4], 5, 6)); // 1,2,3,4,5,6
```

Thông thường chỉ copy array, các object khác cho dù giống aray cũng được copy nguyên object thành một element:

```js run
let arr = [1, 2];

let arrayLike = {
  0: "something",
  length: 1
};

alert( arr.concat(arrayLike) ); // 1,2,[object Object]
//[1, 2, arrayLike]
```

...nhưng nếu array-like object có `Symbol.isConcatSpreadable` property, thì các element của nó sẽ được copy:

```js run
let arr = [1, 2];

let arrayLike = {
  0: "something",
  1: "else",
*!*
  [Symbol.isConcatSpreadable]: true,
*/!*
  length: 2
};

alert( arr.concat(arrayLike) ); // 1,2,something,else
```

## Tìm kiếm trong array

Dưới là các method tìm kiếm trong array.

### indexOf/lastIndexOf và includes

Methods [arr.indexOf](mdn:js/Array/indexOf), [arr.lastIndexOf](mdn:js/Array/lastIndexOf) và [arr.includes](mdn:js/Array/includes) có cú pháp và bản chất và cách hoạt động tương tự nhau:

- `arr.indexOf(item, from)` tìm `item` từ vị trí index `from`, trả về vị trí được tìm thấy, ngược lại trả về `-1`.
- `arr.lastIndexOf(item, from)` -- tương tự, nhưng tìm từ phải qua trái.
- `arr.includes(item, from)` -- tìm `item` từ vị trí `from`, trả về `true` nếu tìm thấy.

Ví dụ:

```js run
let arr = [1, 0, false];

alert( arr.indexOf(0) ); // 1
alert( arr.indexOf(false) ); // 2
alert( arr.indexOf(null) ); // -1

alert( arr.includes(1) ); // true
```

Những methods này sử dụng phép so sánh `===`. Cho nên nếu ta tìm kiếm `false`, nó sẽ tìm chính xác `false` chứ không phải zero.

Nếu chỉ muốn tìm có hay không, và không cần biết index, nên dùng `arr.includes(item)`


### find và findIndex

Tưởng tượng ta có một array chứa các objects. Làm sao tìm được object thỏa mãn một điều kiện nào đó?

Ta sử dụng method [arr.find](mdn:js/Array/find).

Cú pháp:
```js
let result = arr.find(function(item, index, array) {
  // should return true if the item is what we are looking for
});
```

function sẽ được gọi lặp đi lặp lại cho mỗi element của array:

- `item` là element.
- `index` là index của element trên.
- `array` là chính array đó.

Nếu nó trả về `true`, việc tìm kiếm kết thúc, `item` tìm thấy được trả về. Nếu không tìm thấy thì trả về `undefined`.

Ví dụ, tìm object trong array có `id == 1`:

```js run
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

let user = users.find(item => item.id == 1);

alert(user.name); // John
```

Trong thực tế, một array chứa các object rất hay được sử dụng, vì lẽ đó method `find` là rất hữu ích.

Chú ý rằng với ví dụ trên, `find` chỉ có một tham số `item => item.id == 1`. Các tham số khác của hàm `find` hiếm khi được sử dụng.

Method [arr.findIndex](mdn:js/Array/findIndex) là tương tự nhưng nó trả về vị trí index thay vì trả về element.

### filter

`find` method tìm một item đơn (đầu tiên) làm cho function trả về `true`.

Nếu như tìm nhiều element thỏa mãn điều kiện, ta dùng [arr.filter(fn)](mdn:js/Array/filter).

Cú pháp tương tự `find`, nhưng nó trả về một array chứa các item thỏa mãn điều điệu:

```js
let results = arr.filter(function(item, index, array) {
  // should return true if the item passes the filter
});
```

For instance:

```js run
let users = [
  {id: 1, name: "John"},
  {id: 2, name: "Pete"},
  {id: 3, name: "Mary"}
];

// returns array of the first two users
let someUsers = users.filter(item => item.id < 3);

alert(someUsers.length); // 2
```

## Biến đổi một array

Phần này ta tìm hiểu các methods biến đổi hoặc sắp xếp lại một array.


### map

[arr.map](mdn:js/Array/map) method thường rất hay được sử dụng.

Cú pháp:

```js
let result = arr.map(function(item, index, array) {
  // returns the new value instead of item
})
```

Gọi hàm với mỗi element của array, trả về một array chứa kết quả.

Ví dụ:

```js run
let lengths = ["Bilbo", "Gandalf", "Nazgul"].map(item => item.length)
alert(lengths); // 5,7,6
```

### sort(fn)

Method [arr.sort](mdn:js/Array/sort) sắp xếp lại array *trong vị trí*.

Ví dụ:

```js run
let arr = [ 1, 2, 15 ];

// the method reorders the content of arr (and returns it)
arr.sort();

alert( arr );  // *!*1, 15, 2*/!*
```

Có thấy kỳ lạ không?

Sắp xếp thành `1, 15, 2`. Sai, nhưng tại sao?

**Item được sắp xếp theo String ở mặc định.**

Theo nghĩa đen, tất cả item sẽ được convert sang string, sau đó so sánh. Vì vậy `"2" > "15"`.

Để sắp xếp như mong muốn, ta cần tạo ra một hàm với hai tham số, và truyền hàm đó cho `arr.sort()`.

Như thế này:
```js
function compare(a, b) {
  if (a > b) return 1;
  if (a == b) return 0;
  if (a < b) return -1;
}
```

Ví dụ:

```js run
function compareNumeric(a, b) {
  if (a > b) return 1;
  if (a == b) return 0;
  if (a < b) return -1;
}

let arr = [ 1, 2, 15 ];

*!*
arr.sort(compareNumeric);
*/!*

alert(arr);  // *!*1, 2, 15*/!*
```

Bây giờ nó hoạt động như mong muốn.

Method `arr.sort(fn)` tự thực hiện các thuật toán phân loại. Ta không cần quan tâm nó hoạt động bằng cách nào (Một cách sắp xếp tối ưu [quicksort](https://en.wikipedia.org/wiki/Quicksort) hầu hết thời gian). Nó sẽ lướt qua array, thực hiện các phép so sánh theo hàm `fn` mà ta cung cấp để thực hiện các phép so sánh.

Nhân tiện, nếu chúng ta muốn biết những element nào được so sánh -- không có gì xuất hiện khi alert chúng:

```js run
[1, -2, 15, 2, 0, 8].sort(function(a, b) {
  alert( a + " <> " + b );
});
```

Thuật toán có thể so sánh một phần tử nhiều lần trong tiến trình (process), nhưng nó sẽ cố gắng thực hiện càng ít phép so sánh nhất có thể.


````smart header="Hàm so sánh có thể trả về bất cứ số nào"
Thật sự, hàm so sánh chỉ cần trả về số dương để ngụ rằng "lớn hơn" số âm "nhỏ hơn".

Có thể viết ngắn hơn như sau:

```js run
let arr = [ 1, 2, 15 ];

arr.sort(function(a, b) { return a - b; });

alert(arr);  // *!*1, 2, 15*/!*
```
````

````smart header="Arrow functions là tốt nhất"
Có nhớ [arrow functions](info:function-expression#arrow-functions)? Ta có thể sử dụng để làm hàm so sánh:

```js
arr.sort( (a, b) => a - b );
```

Nó hoạt động như các cách khác.
````

### Đảo ngược - reverse

Method [arr.reverse](mdn:js/Array/reverse) đảo ngược thứ tự trong mảng `arr`.

Ví dụ:

```js run
let arr = [1, 2, 3, 4, 5];
arr.reverse();

alert( arr ); // 5,4,3,2,1
```

Nó trả về `arr` sau khi đã đảo thứ tự.

### split và join

method [str.split(delim)](mdn:js/String/split) phân tách các string vào một array bởi sự phân cách `delim`.

Trong ví dụ dưới ta tách string bởi 1 dấu phẩy và 1 dấu space:

```js run
let names = 'Bilbo, Gandalf, Nazgul';

let arr = names.split(', ');

for (let name of arr) {
  alert( `A message to ${name}.` ); // A message to Bilbo  (and other names)
}
```

`split` method có một tham số tùy chọn là một number -- giới hạn của array length. Nếu được truyền vào, sẽ bõ qua các element khi array đã đủ số element:

```js run
let arr = 'Bilbo, Gandalf, Nazgul, Saruman'.split(', ', 2);

alert(arr); // Bilbo, Gandalf
```

````smart header="Split thành các chữ cái"
Gọi `split('')` sẽ tách từng chữ vào trong array:

```js run
let str = "test";

alert( str.split('') ); // t,e,s,t
```
````

Method [arr.join(str)](mdn:js/Array/join) ngược lại với `split`. Nó tạo ra string từ các `arr` items với dấu phân cách là `str`.

Ví dụ:

```js run
let arr = ['Bilbo', 'Gandalf', 'Nazgul'];

let str = arr.join(';');

alert( str ); // Bilbo;Gandalf;Nazgul
```

### reduce/reduceRight

Khi ta lặp (iterate) qua một array -- ta có thể dùng `forEach`.

Khi ta muốn lặp và trả về data theo mỗi element -- ta dùng `map`.

Methods [arr.reduce](mdn:js/Array/reduce) và [arr.reduceRight](mdn:js/Array/reduceRight) cũng tương tự như thế, nhưng là một chút phức tạp hơn. Chúng được sử dụng để tính toán một giá trị đơn dựa trên mảng.

Cú pháp:

```js
let value = arr.reduce(function(previousValue, item, index, arr) {
  // ...
}, initial);
```

Hàm được áp dụng cho các elements. Bạn nên chú ý, tham số hay dùng bắt đầu từ vị trí thứ 2:

- `item` -- array item.
- `index` -- index của item.
- `arr` -- chính là array.

Vẫn tương tự `forEach/map`. nhưng có thêm tham số:

- `previousValue` -- là kết quả của function call trước đó, `initial` khởi tạo cho lần function call đầu tiên.

Cách dễ nhất để nắm bắt đó là bằng ví dụ.

Ở đây ta tính tổng của một mảng:

```js run
let arr = [1, 2, 3, 4, 5]

let result = arr.reduce((sum, current) => sum + current, 0);

alert(result); // 15
```

Ở đây chúng tôi đã sử dụng biến thể phổ biến nhất của `reduce` với chỉ hai tham số.

Chúng ta xem chuyện gì xảy ra.

1. Lần đầu chạy, `sum` là có giá trị khởi tạo - initial (tham số cuối cùng trong `reduce`), bằng `0`, và `current` là element đầu tiên của arr, bằng `1`. Nên kết quả là `1`, gán cho `sum`
2. Lần thứ hai chạy, `sum = 1`, Ta cộng với element thứ hai là `2` , kết quả là `3`, gán cho `sum`
3. Lần thứ ba chạy, `sum = 3` ...

Sơ đồ:

![](reduce.png)

Hoặc xem bảng:

|   |`sum`|`current`|`result`|
|---|-----|---------|---------|
|the first call|`0`|`1`|`1`|
|the second call|`1`|`2`|`3`|
|the third call|`3`|`3`|`6`|
|the fourth call|`6`|`4`|`10`|
|the fifth call|`10`|`5`|`15`|


Ta có thể thấy kết quả của lần gọi trước là tham số của lần gọi tiếp theo.

Ta có thể bõ qua giá trị khởi tạo:

```js run
let arr = [1, 2, 3, 4, 5];

// removed initial value from reduce (no 0)
let result = arr.reduce((sum, current) => sum + current);

alert( result ); // 15
```

Kết quả vẫn thế. Bởi vì nếu không có giá trị khởi tạo, thì `reduce` lấy giá trị element đầu tiên làm giá trị khởi tạo, và lặp tiếp từ element thứ hai.

Chý ý nếu `arr` là rỗng, thì `reduce` sẽ lỗi nếu không thiết lập giá trị khởi tạo.

Ví dụ:

```js run
let arr = [];

// Error: Reduce of empty array with no initial value
// if the initial value existed, reduce would return it for the empty arr.
arr.reduce((sum, current) => sum + current);
```


Tốt nhất là nên thiết lập giá trị khởi tạo.

Method [arr.reduceRight](mdn:js/Array/reduceRight) cũng tương tự như vậy nhưng thực hiện từ phải sang trái.


## Iterate: forEach

Method [arr.forEach](mdn:js/Array/forEach) cho phép gọi một hàm với mỗi element của array.

Cú pháp:
```js
arr.forEach(function(item, index, array) {
  // ... do something with item
});
```

Ví dụ show mỗi element của array:

```js run
// for each element call alert
["Bilbo", "Gandalf", "Nazgul"].forEach(alert);
```

Hay phức tạp hơn:

```js run
["Bilbo", "Gandalf", "Nazgul"].forEach((item, index, array) => {
  alert(`${item} is at index ${index} in ${array}`);
});
```

Kết quả của hàm sẽ bị bõ đi (hàm return cái gì cũng không quan tâm).

## Array.isArray

Arrays Không phải là một kiểu riêng. Chúng cũng là objects.

nên `typeof` không giúp ta phân biệt được một array hay không:

```js run
alert(typeof {}); // object
alert(typeof []); // same
```

...Nhưng array có một method để kiểm tra: [Array.isArray(value)](mdn:js/Array/isArray). Nó trả về `true` nếu `value` thực sự là array, và `false` ngược lại.

```js run
alert(Array.isArray({})); // false

alert(Array.isArray([])); // true
```

## "thisArg"

Hầu hết các array method mà có gọi hàm -- như `find`, `filter`, `map`, với một ngoại lệ là `sort`, chấp nhận tham số tùy chọn `thisArg`.

Tham số này ta chưa học, vì thực sự nó ít khi được dùng. Nhưng để cho hoàn thiện, ta nên biết về nó.

Đây là cú pháp đầy đủ:

```js
arr.find(func, thisArg);
arr.filter(func, thisArg);
arr.map(func, thisArg);
// ...
// thisArg is the optional last argument
```

Giá trị của tham  số `thisArg` là `this` cho `func`.

Ví dụ ta dùng một object method để làm hàm filter và `thisArg` sẽ dùng cho việc này:

```js run
let user = {
  age: 18,
  younger(otherUser) {
    return otherUser.age < this.age;
  }
};

let users = [
  {age: 12},
  {age: 16},
  {age: 32}
];

*!*
// find all users younger than user
let youngerUsers = users.filter(user.younger, user);
*/!*

alert(youngerUsers.length); // 2
```

Ta dùng `user.younger` như một hàm filter và cung cấp `user` như một ngữ cảnh cho nó. Nếu không có ngữ cảnh, `users.filter(user.younger)` sẽ gọi `user.younger` như một standalone function, với `this=undefined`.

## Tổng kết

Một cheatsheet cho array methods:

- Để add/remove elements:
  - `push(...items)` -- adds items to the end,
  - `pop()` -- extracts an item from the end,
  - `shift()` -- extracts an item from the beginning,
  - `unshift(...items)` -- adds items to the beginning.
  - `splice(pos, deleteCount, ...items)` -- at index `pos` delete `deleteCount` elements and insert `items`.
  - `slice(start, end)` -- creates a new array, copies elements from position `start` till `end` (not inclusive) into it.
  - `concat(...items)` -- returns a new array: copies all members of the current one and adds `items` to it. If any of `items` is an array, then its elements are taken.

- To search among elements:
  - `indexOf/lastIndexOf(item, pos)` -- look for `item` starting from position `pos`, return the index or `-1` if not found.
  - `includes(value)` -- returns `true` if the array has `value`, otherwise `false`.
  - `find/filter(func)` -- filter elements of through the function, return first/all values that make it return `true`.
  - `findIndex` is like `find`, but returns the index instead of a value.

- To transform the array:
  - `map(func)` -- creates a new array from results of calling `func` for every element.
  - `sort(func)` -- sorts the array in-place, then returns it.
  - `reverse()` -- reverses the array in-place, then returns it.
  - `split/join` -- convert a string to array and back.
  - `reduce(func, initial)` -- calculate a single value over the array by calling `func` for each element and passing an intermediate result between the calls.

- To iterate over elements:
  - `forEach(func)` -- calls `func` for every element, does not return anything.

- Additionally:
  - `Array.isArray(arr)` checks `arr` for being an array.

Of all these methods only `sort`, `reverse` and `splice` modify the array itself, the other ones only return a value.

These methods are the most used ones, they cover 99% of use cases. But there are few others:

- [arr.some(fn)](mdn:js/Array/some)/[arr.every(fn)](mdn:js/Array/every) checks the array.

  The function `fn` is called on each element of the array similar to `map`. If any/all results are `true`, returns `true`, otherwise `false`.

- [arr.fill(value, start, end)](mdn:js/Array/fill) -- fills the array with repeating `value` from index `start` to `end`.

- [arr.copyWithin(target, start, end)](mdn:js/Array/copyWithin) -- copies its elements from position `start` till position `end` into *itself*, at position `target` (overwrites existing).

For the full list, see the [manual](mdn:js/Array).

From the first sight it may seem that there are so many methods, quite difficult to remember. But actually that's much easier than it seems.

Look through the cheatsheet just to be aware of them. Then solve the tasks of this chapter to practice, so that you have experience with array methods.

Afterwards whenever you need to do something with an array, and you don't know how -- come here, look at the cheatsheet and find the right method. Examples will help you to write it correctly. Soon you'll automatically remember the methods, without specific efforts from your side.
