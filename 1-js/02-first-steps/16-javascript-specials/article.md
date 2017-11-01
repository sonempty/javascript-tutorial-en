# JavaScript specials

Bài này tóm tắt lại tất cả những gì đã học, chú trọng đến những điểm đặc biệt.

[cut]

## Cấu trúc code

Các câu lệnh được phân cách với nhau bằng dấu chấm phẩy:

```js run no-beautify
alert('Hello'); alert('World');
```

Thông thường cũng có thể bõ qua dấu chấm phẩy bằng cách xuống hàng:

```js run no-beautify
alert('Hello')
alert('World')
```

Đó gọi là "tự động chèn dấu chấm phẩy". Trong một số trường hợp sẽ lỗi, ví dụ:

```js run
alert("There will be an error after this message")

[1, 2].forEach(alert)
```

Hầu hết các phong cách code đều khuyên dùng dấu chấm phẩy.

Dấu chấm phẩy không dùng sau các code blocks `{...}` và cấu trúc cú pháp như vòng lặp, if...:

```js
function f() {
  // no semicolon needed after function declaration
}

for(;;) {
  // no semicolon needed after the loop
}
```

...Nhưng dù có thêm dấu chấm phẩy thì cũng sẽ không có lỗi gì, nó sẽ được bỏ qua.

Tìm hiểu thêm tại: <info:structure>.

## Strict mode

Để hỗ trợ đầy đủ các tính năng trong phiên bản JavaScript hiện đại nhất, nên sử dụng `"use strict"` ở đầu script.

```js
'use strict';

...
```

Chỉ thị này phải nằm đầu tiên của script hoặc hàm.

Nếu không có `"use strict"`, code vẫn chạy, nhưng một số tính năng sẽ chạy theo cách cũ, chúng ta thì luôn muốn mọi thứ mới mẽ và cập nhật đúng không.

Một số tính năng mới (như classes sẽ được học trong các bài sau) được bật strict mode một cách ngầm định.

Xem thêm tại: <info:strict-mode>.

## Biến

Được khai báo bởi từ khóa:

- `let`
- `const` (hằng số, không thể thay đổi giá trị)
- `var` (theo cách cũ, sẽ học sau)

Tên của biến bao gồm:
- Chữ cái và chữ số, Nhưng chữ đầu tiên không thể là số.
- Ký tự `$` và `_` .
- Các ký tự không phải Latin, nhưng ít khi được sử dụng.

Biến là kiểu động, nghĩa là có thể gán bất cứ giá trị gì cho nó:

```js
let x = 5;
x = "John";
```

Có 7 kiểu dữ liệu:

- `number` cho số nguyên và dấu chấm động,
- `string` cho chuỗi,
- `boolean` cho các giá trị logic: `true/false`,
- `null` -- kiểu `null`, có nghĩa là "rỗng" hoặc "không tồn tại",
- `undefined` -- kiểu `undefined`, nghĩa là "chưa được gán giá trị",
- `object` và `symbol` -- cho dữ liệu phức tạp hơn và định danh duy nhất, hiện tại ta chưa học đến.

Phép `typeof` trả về kiểu dữ liệu của giá trị, với hai ngoại lệ:
```js
typeof null == "object" // error in the language
typeof function(){} == "function" // functions are treated specially
```

Xem thêm tại: <info:variables> và <info:types>.

## Tương tác

Chúng ta sử dụng trình duyệt làm môi trường làm việc, và có một vài hàm UI cơ bản:

[`prompt(question[, default])`](mdn:api/Window/prompt)
: Hỏi một `câu hỏi`, trả về những gì mà user nhập vào hoặc `null` nếu user nhấn "cancel".

[`confirm(question)`](mdn:api/Window/confirm)
: Hỏi một `câu hỏi` và user có thể chọn Ok hoặc Cancel. Trả về `true/false`.

[`alert(message)`](mdn:api/Window/alert)
: In ra một `message`.

Các hàm trên đều là *modal*, Nghĩa là dừng sự thực thi của chương trình cho đến khi nhận được tương tác từ user.

Ví dụ:

```js run
let userName = prompt("Your name?", "Alice");
let isTeaWanted = confirm("Do you want some tea?");

alert( "Visitor: " + userName ); // Alice
alert( "Tea wanted: " + isTeaWanted ); // true
```

Xem thêm: <info:alert-prompt-confirm>.

## Phép toán

JavaScript hỗ trợ các phép toán sau:

Số học
: Hay dùng: `* + - /`, `%` cho phép chia dư và `**` cho phép lũy thừa.

    Phép `+` cộng hai chuỗi. và nếu có một toán hạng là string thì toán hạng còn lại cũng sẽ được convert sang string:

    ```js run
    alert( '1' + 2 ); // '12', string
    alert( 1 + '2' ); // '12', string
    ```

Phép gán
: Phép gán đơn giản: `a = b` và kết hợp `a *= 2`.

Phép nhị phân
: Xem thêm [docs](mdn:/JavaScript/Reference/Operators/Bitwise_Operators) nếu cần.

Phép toán ba ngôi
: Có duy nhất một phép toán là: `cond ? resultA : result B`. nếu `cond` là đúng thì trả về `resultA`, ngược lại trả về `resultB`.

Phép Logic
: Phép toán logic AND `&&` và OR `||` trả về giá trị mà phép toán dừng lại.

Phép so sánh
: So sánh bằng `==` cho các giá trị khác kiểu, conver chúng thành số (ngoại trừ `null` và `undefined` chỉ bằng chính chúng), vì thế, các giá trị ở ví dụ dưới là bằng nhau:

    ```js run
    alert( 0 == false ); // true
    alert( 0 == '' ); // true
    ```

    Các phép so sánh khác cũng convert sang kiểu số.

    Phép so sánh bằng nghiêm ngặt `===` không convert: khác kiểu thì sẽ không bằng:

    Giá trị `null` và `undefined` là đặc biệt: chúng chỉ `==` chúng và không `==` thứ gì khác.

    Phép so sánh lớn hơn, nhỏ hơn so sánh hai chuỗi theo từng ký tự , các kiểu khác thì convert sang number.

Phép logic
: Có thêm một số phép logic khác, như `?`.

Xem thêm tại: <info:operators>, <info:comparison>, <info:logical-operators>.

## Vòng lặp

- Chúng ta đã học ba loại vòng lặp:

    ```js
    // 1
    while (condition) {
      ...
    }

    // 2
    do {
      ...
    } while (condition);

    // 3
    for(let i = 0; i < 10; i++) {
      ...
    }
    ```

- Biến được khai báo trong `for(let...)` chỉ được sử dụng trong vòng lặp. Nhưng chúng ta có thể bõ qua `let` để sử dụng một biến đã có sẵn.
- Chỉ thị `break/continue` để thoát hoặc tiếp tục vòng lặp. Sử dụng "label" đối với các vòng lặp lồng nhau.

Xem thêm tại: <info:while-for>.

Cuối cùng chúng ta sẽ học thêm nhiều kiểu vòng lặp và sử dụng với Object.

## Cấu trúc "switch"

Cấu trúc "switch" để thay thế khi cần dùng nhiều "if". Nó sử dụng `===` để so sánh điều kiện.

Ví dụ:

```js run
let age = prompt('Your age?', 18);

switch (age) {
  case 18:
    alert("Won't work"); // the result of prompt is a string, not a number

  case "18":
    alert("This works!");
    break;

  default:
    alert("Any value not equal to one above");
}
```

Xem thêm tại: <info:switch>.

## Hàm

Chúng ta đã học ba cách để tạo ra hàm trong JavaScript:

1. Function Declaration: Khai báo hàm trong main code flow

    ```js
    function sum(a, b) {
      let result = a + b;

      return result;
    }
    ```

2. Function Expression: Khai báo hàm trong biểu thức phép gán

    ```js
    let sum = function(a, b) {
      let result = a + b;

      return result;
    }
    ```

    Function expression có tên, như `sum = function name(a, b)`, nhưng tên này `name` chỉ dùng được bên trong hàm.

3. Arrow functions:

    ```js
    // expression at the right side
    let sum = (a, b) => a + b;

    // or multi-line syntax with { ... }, need return here:
    let sum = (a, b) => {
      // ...
      return a + b;
    }

    // without arguments
    let sayHi = () => alert("Hello");

    // with a single argument
    let double = n => n * 2;
    ```


- Hàm có biến cục bộ: Là các biến được khai báo bên trong thân hàm, và chỉ sử dụng được bên trong hàm đó.
- Tham số có giá trị mặc định: `function sum(a = 1, b = 2) {...}`.
- Hàm có thể trả về giá trị nào đó. Nếu không có lệnh `return` thì trả về `undefined`.


| Function Declaration | Function Expression |
|----------------------|---------------------|
| Chỉ dùng được trong code block | Được tạo ra khi JS thực thi đến code tạo ra nó |
|   - | Có thể có tên, chỉ dùng được trong hàm |

Xem thêm <info:function-basics>, <info:function-expressions-arrows>.

## Tiếp theo

Tóm tắt những tính năng cơ bản trong JavaScript. Tiếp theo các bài sau sẽ học các tính năng nâng cao của JavaScript.
