# Các phép logic

Có ba phép logic trong JavaScript: `||` (OR), `&&` (AND), `!` (NOT).

Mặc dù được gọi là "logic", nhưng có thể dùng trên bất cứ kiểu dữ liệu nào không riêng gì Boolean. Kết quả trả về cũng có thể là bất cứ kiểu dữ liệu nào.

[cut]

## || (OR)

Phép hoặc "OR" được thể hiện bằng hai dấu gạch thẳng đứng như bên dưới:

```js
result = a || b;
```

Trong lập trình cổ điển, phép OR chỉ sử dụng trên kiểu Boolean. nếu có bất cứ tham số nào có giá trị là `true`, thì trả về `true`, ngược lại trả về `false`.

Trong JavaScript phép OR có chút khác biệt và mạnh mẽ hơn. Nhưng trước hết ta tìm hiểu OR sử dụng trên Boolean.

Có bốn khả năng như bên dưới:

```js run
alert( true || true );   // true
alert( false || true );  // true
alert( true || false );  // true
alert( false || false ); // false
```

Giá trị trả về là `true` trừ trường hợp tất cả toán hạng đều là `false`.

Nếu có toán hạng không phải kiểu Boolean, nó sẽ được chuyển đổi thành Boolean.

Ví dụ number `1` chuyển thành `true`, và number `0` -- là `false`:

```js run
if (1 || 0) { // works just like if( true || false )
  alert( 'truthy!' );
}
```

Hầu hết trường hợp, OR `||` được sử dụng cùng câu lệnh `if` để kiểm tra có có giá trị nào là `true` hay không.

Ví dụ:

```js run
let hour = 9;

*!*
if (hour < 10 || hour > 18) {
*/!*
  alert( 'The office is closed.' );
}
```

Chúng ta có thể sử dụng nhiều btđk hơn:

```js run
let hour = 12;
let isWeekend = true;

if (hour < 10 || hour > 18 || isWeekend) {
  alert( 'The office is closed.' ); // it is the weekend
}
```

## OR tìm kiếm giá trị true đầu tiên

Đây là điểm khác biệt giữa JavaScipt và lập trình cổ điển đã nói ở trên.

Sự khác biệt như sau:

```js
result = value1 || value2 || value3;
```

Phép OR `"||"` sẽ được thực hiện như sau:

- Đánh giá các toán hạng từ trái sang phải.
- Chuyển đổi từng toán hạng sang kiểu Boolean. Nếu thấy có toán hạng là `true`, phép toán kết thúc, trả về giá trị nguyên bản khi chưa chuyển đổi (orginal value) của toán hạng đó.
- Nếu tất cả toán hạng đều là `false` thì trả về toán hạng cuối cùng.

Nói cách khác phép OR `"||"` trả về giá trị `truthy` đầu tiên. Hoặc trả về giá trị cuối cùng nếu tất cả toán hạng là `falsy`.
Nhắc lại một chút:
- `truthy` ám chỉ các giá trị mà khi convert sang Boolean thì sẽ được `true`. Ví dụ như 1, "fdsfsf", "0",...
- `falsy` ám chỉ các giá trị mà khi convert sang Boolean thì sẽ được `fasle`. Ví dụ như null, 0, "", ....

Ví dụ:

```js run
alert( 1 || 0 ); // 1 (1 is truthy)
alert( true || 'no matter what' ); // (true is truthy)

alert( null || 1 ); // 1 (1 is the first truthy value)
alert( null || 0 || 1 ); // 1 (the first truthy value)
alert( undefined || null || 0 ); // 0 (all falsy, returns the last value)
```

1. **Lấy giá trị truthy từ các toán hạng hoặc biểu thức.**

    Tưởng tượng bạn có nhiều biến, và các biến này có thể có giá trị là `null/undefined`. Và chúng ta cần chọn biến đầu tiên có giá trị mà ta cần.

    Chúng ta sử dụng phép `||` :

    ```js run
    let currentUser = null;
    let defaultUser = "John";

    *!*
    let name = currentUser || defaultUser || "unnamed";
    */!*

    alert( name ); // selects "John" – the first truthy value
    ```

    Nếu cả `currentUser` và `defaultUser` là falsy thì giá trị `"unnamed"` sẽ là kết quả.
2. **đánh giá ngắn mạch**

    Toán hạng có thể là các giá trị, cũng có thể là các biểu thức trừu tượng. OR sẽ đánh giá chúng từ trái sang phải. Sự đánh giá này sẽ dừng lại khi thấy giá trị truthy đầu tiên, và giá trị đó sẽ được trả về. Quá trình này gọi là đánh giá ngắn mạch "a short-circuit evaluation", bởi vì sự đánh giá này là ngắn nhất có thể từ trái sang phải.
    "Ngắn mạch" từ này hay dùng trong ngành điện. Các bạn có thể google xem nhé.

    Điều này được thấy rõ khi biểu thức được đưa ra như là đối số thứ hai có tác dụng phụ. Giống như một phép gán biến.

    Chạy đoạn code sau, ta sẽ thấy `x` không được gán giá trị:

    ```js run no-beautify
    let x;

    *!*true*/!* || (x = 1);

    alert(x); // undefined, because (x = 1) not evaluated
    ```

    ...và nếu toán hạng đầu tiên là `false`, sau đó `OR` đánh giá toán hạng thứ hai, chính là biểu thức `(x = 1)`, và `x` sẽ được gán giá trị.:

    ```js run no-beautify
    let x;

    *!*false*/!* || (x = 1);

    alert(x); // 1
    ```

    Phép gán ở trên chỉ là một ví dụ đơn giản, ta còn có thể dùng nhiều biểu thức phức tạp hơn.

    Như bạn thấy hầu hết các trường hợp đều "ngắn hơn là dùng `if`".

    Nói chung là tùy trường hợp dùng OR cho ngắn hay dùng `if` để code dễ hiểu hơn là tùy ở bạn.

## && (AND)

Phép AND thể hiện bằng hai dấu và `&&`:

```js
result = a && b;
```

Trong lập trình cổ điển phép AND trả về `true` nếu cả hai toán hạng là truthy và trả về `false` nếu ngược lại:

```js run
alert( true && true );   // true
alert( false && true );  // false
alert( true && false );  // false
alert( false && false ); // false
```

Ví dụ với `if`:

```js run
let hour = 12;
let minute = 30;

if (hour == 12 && minute == 30) {
  alert( 'Time is 12:30' );
}
```

tương tự OR, AND có thể dùng trên bất kỳ kiểu dữ liệu nào:

```js run
if (1 && 0) { // evaluated as true && false
  alert( "won't work, because the result is falsy" );
}
```


## AND tìm giá trị falsy đầu tiên

Xem ví dụ:

```js
result = value1 && value2 && value3;
```

Phép AND `"&&"` sẽ thực hiện như sau:

- Đánh giá các toán hạng từ trái sang phải.
- Chuyển đổi từng toán hạng sang Boolean. Nếu gặp giá trị `false`, kết thúc phép toán và trả về orginal value của toán hạng đó.
- Nếu tất cả toán hạng là truthy, trả về toán hạng cuối cùng.

Nói cách khác, AND trả về giá trị falsy đầu tiên. Hoặc trả về toán hạng cuối cùng nếu tất cả toán hạng đều là truthy

Quy tắc này tương tự OR. Khác biệt là AND trả về giá trị *falsy* đầu tiên trong khi OR trả về giá trị *truthy* đầu tiên.

Ví dụ:

```js run
// if the first operand is truthy,
// AND returns the second operand:
alert( 1 && 0 ); // 0
alert( 1 && 5 ); // 5

// if the first operand is falsy,
// AND returns it. The second operand is ignored
alert( null && 5 ); // null
alert( 0 && "no matter what" ); // 0
```

Giá trị falsy đầu tiên được trả về:

```js run
alert( 1 && 2 && null && 3 ); // null
```

Nếu tất cả là truthy, giá trị cuối cùng được trả về:

```js run
alert( 1 && 2 && 3 ); // 3, the last one
```

````smart header="AND `&&` được thực thi trước OR `||`"
Phép AND `&&` có độ ưu tiên cao hơn phép OR `||`.

Xem vd bên dưới `1 && 0` sẽ được thực thi trước:

```js run
alert( 5 || 1 && 0 ); // 5
```
````

Tương tự OR, Phép AND `&&` thỉnh thoảng được dùng để thay thế `if`.

Ví dụ:

```js run
let x = 1;

(x > 0) && alert( 'Greater than zero!' );
```

Hành động phía sau `&&` chỉ được thực thi nếu `(x > 0)` là đúng.

Nó tương đương với:

```js run
let x = 1;

if (x > 0) {
  alert( 'Greater than zero!' );
}
```

Dùng `&&` thấy ngắn hơn dùng `if`. Nhưng dùng `if` rõ ràng và dễ đọc hơn.

Cho nên hãy sử dụng cho đúng mục đích.

## ! (NOT)

Phép phủ định NOT được thể hiện bằn dấu chấm than `"!"`.

Cấu trúc ngữ pháp khá đơn giản:

```js
result = !value;
```

Nó là phép toán một ngôi có nguyên tắc đơn giản như sau:

1. Chuyển đổi toán hạng thành Boolean: `true/false`.
2. Trả về giá trị ngược lại.

Ví dụ:

```js run
alert( !true ); // false
alert( !0 ); // true
```

Sử dụng hai lần phép NOT `!!` thỉnh thoảng được sử dụng để convert giá trị thành Boolean:

```js run
alert( !!"non-empty string" ); // true
alert( !!null ); // false
```

Vì phủ định của phủ định là khẳng định mà.

Có cách đơn giản hơn là sử dụng hàm `Boolean` có sẵn trong JS:

```js run
alert( Boolean("non-empty string") ); // true
alert( Boolean(null) ); // false
```
