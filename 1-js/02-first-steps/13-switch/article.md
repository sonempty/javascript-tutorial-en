# Câu lệnh "switch"

Lệnh `switch` thay thế cho việc sử dụng nhiều `else if`.

[cut]

## Cú pháp

Lệnh `switch` có một hoặc nhiều khối lệnh `case` và một khối `default`.

Như thế này:

```js no-beautify
switch(x) {
  case 'value1':  // if (x === 'value1')
    ...
    [break]

  case 'value2':  // if (x === 'value2')
    ...
    [break]

  default:
    ...
    [break]
}
```

- Giá trị của `x` được kiểm tra có bằng (===) với giá trị trong `case` (ở đây là, `value1`) và tiếp theo (`value2`) cứ tiếp tục như thế.
- Nếu bằng, `switch` thực thi khối lệnh trong `case` đó, cho đến khi lệnh `break` được gọi (hoặc kết thúc `switch`).
- Nếu không có `case` nào thỏa mãn,  `default` được thực thi (nếu nó tồn tại).

## Ví dụ

Một ví dụ với `switch` :

```js run
let a = 2 + 2;

switch (a) {
  case 3:
    alert( 'Too small' );
    break;
*!*
  case 4:
    alert( 'Exactly!' );
    break;
*/!*
  case 5:
    alert( 'Too large' );
    break;
  default:
    alert( "I don't know such values" );
}
```

Ở đây `switch` bắt đầu so sánh `a` từ `case` đầu tiên là `3`. phép so sánh này `false`.

Tiếp theo là `4`. đúng, nên thực thi khối lệnh trong `case 4`.

**Nếu không có `break` thì sẽ thực thi code trong các `case` tiếp theo mà không cần kiểm tra.**

Ví dụ: không có `break`:

```js run
let a = 2 + 2;

switch (a) {
  case 3:
    alert( 'Too small' );
*!*
  case 4:
    alert( 'Exactly!' );
  case 5:
    alert( 'Too big' );
  default:
    alert( "I don't know such values" );
*/!*
}
```

Trong ví dụ trên ta thấy thực hiện 3 lần lệnh `alert`:

```js
alert( 'Exactly!' );
alert( 'Too big' );
alert( "I don't know such values" );
```

````smart header="Biểu thức có thể là tham số của `switch/case`"
Cả `switch` và `case` chấp nhận các biểu thức.

Ví dụ:

```js run
let a = "1";
let b = 0;

switch (+a) {
*!*
  case b + 1:
    alert("this runs, because +a is 1, exactly equals b+1");
    break;
*/!*

  default:
    alert("this doesn't run");
}
```
Ở đây `+a` trả về `1`, so sánh với `b + 1` trong `case`, thấy bằng nhau nên code được thực thi.
````

## Nhóm các "case"

Nhiều giá trị `case` có cùng code thực thi có thể được nhóm lại.

Ví dụ `case 3` và `case 5` cùng thực thi một hành động:

```js run no-beautify
let a = 2 + 2;

switch (a) {
  case 4:
    alert('Right!');
    break;

*!*
  case 3:                    // (*) grouped two cases
  case 5:
    alert('Wrong!');
    alert("Why don't you take a math class?");
    break;
*/!*

  default:
    alert('The result is strange. Really.');
}
```

Case `3` và `5` cùng hiển thị lệnh alert như nhau.

Nhóm cases là một hiệu ứng phụ của việc làm cách nào `switch/case` hoạt động khi không có `break`. Ở đây `case 3` bắt đầu ở dòng `(*)` và chuyển qua `case 5`, bởi vì không có `break`.

## Vấn đề kiểu dữ liệu

Phép so sánh là `===` (strict). Nên các giá trị phải có cùng kiểu dữ liệu.

Xem xét code sau:

```js run
let arg = prompt("Enter a value?")
switch (arg) {
  case '0':
  case '1':
    alert( 'One or zero' );
    break;

  case '2':
    alert( 'Two' );
    break;

  case 3:
    alert( 'Never executes!' );
    break;
  default:
    alert( 'An unknown value' )
}
```

1. Với `0`, `1`, lệnh `alert` đầu tiên sẽ chạy.
2. Với `2` lệnh `alert` thứ hai sẽ chạy.
3. Nhưng với `3`, kết quả trả về của `prompt` là chuỗi `"3"`, không `===` với số `3`. nên `case 3` sẽ không chạy! nên cuối cùng `default` sẽ chạy.
