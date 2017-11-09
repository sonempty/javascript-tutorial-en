# Arrays 

Objects cho phép lưu trữ các bộ key-value.

Nhưng ta cần một * bộ có thứ tự - ordered collection*, với giá trị 1st, 2nd, 3rd ... Ví dụ ta cần lưu một bộ giá trị: users, goods, HTML elements ... 

Sẽ không thích hợp khi sử dụng object ở đây, Bởi vì nó không sắp xếp được các giá trị của nó. Ta không thể chèn vào một property mới “ở giữa” các property đã có.

Có một cấu trúc dữ liệu được gọi là mãng `Array`, để lưu trữ các bộ có thứ tự. 

[cut]

## Khai báo

Có hai cách tạo ra một Array rỗng:

```js
let arr = new Array();
let arr = [];
```

Cách thứ hai hay được sử dụng, ta có thể khởi tạo luôn các Array element:

```js
let fruits = ["Apple", "Orange", "Plum"];
```

Array elements được đánh số thứ tự, bắt đầu từ 0.

Ta truy xuất các element thông qua số thứ tự của nó trong dấu ngoặc vuông:

```js run
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits[0] ); // Apple
alert( fruits[1] ); // Orange
alert( fruits[2] ); // Plum
```

Gán lại giá trị cho element:

```js
fruits[2] = 'Pear'; // now ["Apple", "Orange", "Pear"]
```

...hoặc add thêm element cho array:

```js
fruits[3] = 'Lemon'; // now ["Apple", "Orange", "Pear", "Lemon"]
```

Tổng số element trong array là độ dài `length` của array:

```js run
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits.length ); // 3
```

Ta có thể `alert` toàn bộ array.

```js run
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits ); // Apple,Orange,Plum
```

element có thể là bất cứ loại dữ liệu nào.

Ví dụ:

```js run no-beautify
// mix of values
let arr = [ 'Apple', { name: 'John' }, true, function() { alert('hello'); } ];

// get the object at index 1 and then show its name
alert( arr[1].name ); // John

// get the function at index 3 and run it
arr[3](); // hello
```


````smart header="Trailing comma"
Một array, cũng như object, nên kết thúc bởi dấu phẩy:
```js 
let fruits = [
  "Apple", 
  "Orange", 
  "Plum"*!*,*/!*
];
```

"trailing comma" dễ dàng hơn cho việc insert/remove items, bởi vì tất cả các dòng đều như nhau.
````


## Methods pop/push, shift/unshift

Một hàng đợi [queue](https://en.wikipedia.org/wiki/Queue_(abstract_data_type)) là một trong những cách dùng array phổ biến. Trong khoa học máy tính, hàng đợi là một bộ thứ tự hỗ trợ các hành động:

- `push` nối một element vào cuối.
- `shift` lấy element đầu tiên, và loại nó ra khỏi queue, cho nên 2nd element sẽ trở thành 1st.

![](queue.png)

Arrays hỗ trợ cả hai hành động trên.

Trong thực tế ta gặp các queue rất nhiều, ví dụ một message list để in ra màn hình.

Có một cách sử dụng khác với arrays -- một cấu trúc dữ liệu có tên là ngăn xếp [stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)). 

Nó hỗ trợ hai hành động:

- `push` thêm element vào cuối stack.
- `pop` bõ element cuối stack.

element được thêm hay loại bõ đều ở cuối stack.

![](stack.png)

Với stack, element được đưa vào cuối cùng sẽ được lấy ra đầu tiên, nguyên tắc này gọi là LIFO (Last-In-First-Out). Với queue, ta có FIFO (First-In-First-Out).

Arrays trong JavaScript có thể hoạt động như queue và stack. Chúng cho phép add/remove elements theo phía bắt đầu lẫn cuối array. 

Trong khoa học máy tính, những cấu trúc dữ liệu như thế được gọi là hàng đợi hai đầu [deque](https://en.wikipedia.org/wiki/Double-ended_queue).

**Methods hoạt động theo element cuối array:**

`pop`
: Lấy element cuối cùng ra khỏi array, trả về chính element đó:

    ```js run
    let fruits = ["Apple", "Orange", "Pear"];

    alert( fruits.pop() ); // remove "Pear" and alert it

    alert( fruits ); // Apple, Orange
    ```

`push`
: thêm element vào cuối array, trả về length của array:

    ```js run
    let fruits = ["Apple", "Orange"];

    fruits.push("Pear");

    alert( fruits ); // Apple, Orange, Pear
    ```

    The call `fruits.push(...)` is equal to `fruits[fruits.length] = ...`.

**Methods that work with the beginning of the array:**

`shift`
: Lấy element đầu tiên ra khỏi array, trả về element đó:

    ```js
    let fruits = ["Apple", "Orange", "Pear"];

    alert( fruits.shift() ); // remove Apple and alert it

    alert( fruits ); // Orange, Pear
    ```

`unshift`
: thêm element vào đầu array, trả về length của array:

    ```js
    let fruits = ["Orange", "Pear"];

    fruits.unshift('Apple');

    alert( fruits ); // Apple, Orange, Pear
    ```

Methods `push` và `unshift` có thể add nhiều element trong một lần gọi:

```js run
let fruits = ["Apple"];

fruits.push("Orange", "Peach");
fruits.unshift("Pineapple", "Lemon");

// ["Pineapple", "Lemon", "Apple", "Orange", "Peach"]
alert( fruits );
```

## Internals

Array là một kiểu object đặc biệt. Cặp ngoặc vuông để truy xuất property `arr[0]` thực sự là đến từ cú pháp của object. Numbers được sử dụng làm keys. 

Object này được mở rộng để cung cấp thêm các method, cũng như `length` property. Nhưng về cơ bản thì array vẫn là một object.

Nên nhớ chỉ có 7 kiểu dữ liệu trong JavaScript. Array chỉ là object, và do đó các hành vi của nó tương tự object. 

Ví dụ, nó cũng được copy bởi tham chiếu:

```js run
let fruits = ["Banana"]

let arr = fruits; // copy by reference (two variables reference the same array)

alert( arr === fruits ); // true
 
arr.push("Pear"); // modify the array by reference

alert( fruits ); // Banana, Pear - 2 items now
```

...nhưng cái gì làm cho array trở nên đặc biệt? JavaScript Engine sẽ lưu trữ chúng trong một vùng nhớ liên tục, element này nối tiếp element khác, như cách ta tìm hiểu về JS engine tối ưu ở các chương trước, sử dụng array cũng giúp cho chương trình chạy nhanh hơn là object.

Nhưng sẽ là không ổn nếu ta sử dụng array theo cách của object.

Ví dụ, về kỹ thuật code như bên dưới vẫn chạy được:

```js
let fruits = []; // make an array

fruits[99999] = 5; // assign a property with the index far greater than its length

fruits.age = 25; // create a property with an arbitrary name
```

Điều này có thể, vì array vẫn là object, nên nó cũng có các property.

Nhưng JS Engine sẽ coi array như một object chính quy. Và những ưu điểm của aray trong việc tối ưu cho chương trình sẽ bị bõ qua.

Những cách lạm dụng array mà ta không nên sử dụng:

- Thêm một non-numeric property như `arr.test = 5`. 
- Tạo các lỗ trống: add `arr[0]` và sau đó `arr[1000]` (không có gì ở giữa chúng).
- Lấp đầy array theo thứ tự ngược `arr[1000]`, `arr[999]` ...

Hãy suy nghĩ array như với một bộ *dữ liệu có thứ tự*. Chúng cung cấp các method đặc biệt. Arrays được điều chỉnh trong JavaScript engines để làm việc với dữ liệu một cách liên tục, hãy sử dụng chúng với cách này. Nếu muốn sử dụng một key trừu tượng, hãy sử dụng nó với `{}`.

## Performance

Methods `push/pop` chạy rất nhanh, nhưng `shift/unshift` thì chậm.

![](array-speed.png)

Tại sao nhanh khi xử lý cuối array và chậm nếu method xử lý đầu aray? Ta sẽ xem xét điều gì xảy ra khi thực hiện các methods này:

```js
fruits.shift(); // take 1 element from the start
```

Sẽ không đủ nếu chỉ bõ element ở vị trí `0`. Các element khác cần được đánh số thứ tự lại.

Method `shift` sẽ làm 3 bước:

1. Xóa element có index `0`.
2. Di chuyển các element khác sang trái,  `1` đến `0`, từ `2` đến `1` ...
3. Cập nhật lại `length` property.

![](array-shift.png)

**Càng có nhiều element trong array, càng di chuyển nhiều , chương trình sẽ càng chậm.**

Tương tự với `unshift`: để thêm element vào đầu array, các element sẽ phải di chuyển sang phải.

Và với `push/pop`? Các element sẽ không phải di chuyển, mà chỉ thêm/xóa element cuối cùng, và cập nhật lại `length`.

Hoạt động của `pop`:

```js
fruits.pop(); // take 1 element from the end
```

![](array-pop.png)

**Method `pop` không cần di chuyển element, bởi vì chúng vẫn giữ nguyên index. Vì vậy nó chạy rất nhanh.**

Tương tự với method `push`.

## Loops

Một cách cổ xưa hay dùng là `for` với các indexes của array:

```js run
let arr = ["Apple", "Orange", "Pear"];

*!*
for (let i = 0; i < arr.length; i++) {
*/!*
  alert( arr[i] );
}
```

Nhưng ta có một cách khác hay hơn là, `for..of`:

```js run
let fruits = ["Apple", "Orange", "Plum"];

// iterates over array elements
for(let fruit of fruits) {
  alert( fruit ); 
}
```

Lệnh `for..of` không cho ra index của element, chỉ cho giá trị của element. Và hầu hết các trường hợp như thế là quá đủ.

Về mặt kỹ thuậ, vì array là một object nên có thể sử dụng `for..in`:

```js run
let arr = ["Apple", "Orange", "Pear"];

*!*
for (let key in arr) {
*/!*
  alert( arr[key] ); // Apple, Orange, Pear
}
```

Nhưng đó thực sự là một ý tưởng tồi. Có những vấn đề tiềm ẩn:

1. Vòng lặp `for..in` lặp qua *tất cả properties*, không chỉ là các numeric property.

    Và trong array sẽ có nhiều property khác như length, các method....

2. Vòng lặp `for..in` được tối ưu cho các object tiêu chuẩn, không phải arrays, và do đó sẽ bị chậm 10-100 lần. Tất nhiên vẫn rất nhanh, nhưng nếu như ta dùng một triệu lần như thế thì chương trình sẽ chậm đi quá nhiều đúng không.

Nói tóm lại, chỉ nên dùng `for..in` đối với arrays.


## Nói về "length"

`length` property tự động cập nhật khi ta chỉnh sửa array. Nói tóm lại, giá trị của nó bằng với index lớn nhất, chứ không phải là đếm số index.

Ví dụ:

```js run
let fruits = [];
fruits[123] = "Apple";

alert( fruits.length ); // 124
```

Chú ý là không sử dụng như ví dụ trên, lấy ra để hiểu vấn đề thôi. 

Một sự thú vị khác với `length` property là có thể ghi đè.

Nếu ta tăng giá trị của length sẽ chẳng có gì xảy ra, nhưng nếu ta giảm giá trị của length, array sẽ bị cắt đi một phần:

```js run
let arr = [1, 2, 3, 4, 5];

arr.length = 2; // truncate to 2 elements
alert( arr ); // [1, 2]

arr.length = 5; // return length back
alert( arr[3] ); // undefined: the values do not return
```

Nên cách đơn giản nhất để xóa một array là: `arr.length=0`.


## new Array() [#new-array]

Có một cú pháp khác để tạo ra một array:

```js
let arr = *!*new Array*/!*("Apple", "Pear", "etc");
```

Nó ít được sử dụng, vì dùng`[]` sẽ ngắn gọn hơn.

Nếu `new Array` được gọi với một tham số là số nguyên *sẽ không có items, nhưng độ dài của aray chính là số nguyên đó*.

Xem ví dụ:

```js run
let arr = new Array(2); // will it create an array of [2] ?

alert( arr[0] ); // undefined! no elements.

alert( arr.length ); // length 2
```

Trong code trên, `new Array(number)` có các element đều là `undefined`.

Để tránh những điều trên, nên dùng cặp ngoặc vuông để tạo ra array.

## Mãng nhiều chiều

Arrays có thể có các item là arrays. Ta dùng nó để biễu diễn mãng nhiều chiều, như ma trận:

```js run
let matrix = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];

alert( matrix[1][1] ); // the central element
```

## toString

Arrays có method `toString` riêng của nó, trả về các elements được phân tách bởi dấu phẩy.

ví dụ:


```js run
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // true
```

Thử:

```js run
alert( [] + 1 ); // "1"
alert( [1] + 1 ); // "11"
alert( [1,2] + 1 ); // "1,21"
```

Arrays không có `Symbol.toPrimitive`, và `valueOf`, Chúng chỉ có `toString` conversion, nên ở đây `[]` trở thành một chuỗi rỗng '', và `[1]` thành `"1"` và `[1,2]` thành `"1,2"`.

Khi dùng toán tử `"+"`, nếu có một toán hạng là string thì sẽ convert thành string:

```js run
alert( "" + 1 ); // "1"
alert( "1" + 1 ); // "11"
alert( "1,2" + 1 ); // "1,21"
```

## Tổng kết

Array là một objects đặc biệt, dùng lưu trữ dữ liệu có thứ tự.

- Khai báo:

    ```js
    // square brackets (usual)
    let arr = [item1, item2...];

    // new Array (exceptionally rare)
    let arr = new Array(item1, item2...);
    ```

    Gọi `new Array(number)` tạo ra một array với length = number, nhưng không có elements.

- `length` property là độ dài của arrat. Nó bằng index lớn nhất, và tự cập nhật khi array thay đổi. 
- Nếu giảm giá trị `length`, array sẽ bị cắt bỏ một phần.

Ta sử dụng array như một deque:

- `push(...items)` thêm `items` vào cuối.
- `pop()` xóa item ở cuối và trả về item đó.
- `shift()` xóa item ở đầu và trả về item đó.
- `unshift(...items)` thêm item ở đầu.

Lặp qua các element của array:
  - `for(let i=0; i<arr.length; i++)` -- chạy nhanh, theo phong cách cũ.
  - `for(let item of arr)` -- chạy nhanh, theo cách hiện đại,
  - `for(let i in arr)` -- đừng bao giờ dùng cách này.

Ta sẽ học thêm nhiều method của array ở chương <info:array-methods>.

