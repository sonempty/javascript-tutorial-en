# Phép điều kiện: if, '?'

Ở đây mình dịch là *phép* điều kiện chứ không phải là biểu thức điều kiện, điều này có dụng ý là `?` vẫn là một operator như các phép toán mà chúng ta đã học ở bài trước.

Thỉnh thoảng chúng ta cần thực thi các hành động khác nhau tùy thuộc vào kết quả của một biểu thức nào đó.

Chúng ta dùng câu lệnh `if` cho các hành động phức tạp, hoặc phép điều kiện `"?"` cho các hành động đơn giản.

[cut]

## Câu lệnh "if"

Lệnh "if" nhận vào một biểu thức điều kiện, tính toán biểu thức đó, nếu kết quả là `true` thì thực hiện các hành động.

Ví dụ:

```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

*!*
if (year == 2015) alert( 'You are right!' );
*/!*
```

Ở ví dụ trên, biểu thức điều kiện đơn giản là: `year == 2015`.

Nếu có nhiều hành động được thực thi, ta viết chúng vào block (trong cặp dấu {} ):

```js
if (year == 2015) {
  alert( "That's correct!" );
  alert( "You're so smart!" );
}
```

Nên dùng cặp ngoặc nhọn cho `if`, cho dù chỉ có một câu lệnh, như thế sẽ dễ đọc hơn.

## Chuyển đổi Boolean

Lệnh `if (…)` thực hiện biểu thức điều kiện trong cặp dấu ngoặc và convert kết quả sang kiểu boolean.

Xem lại các quy tắc ép kiểu ở chương <info:type-conversions>:

- Số `0`, chuỗi rỗng `""`, `null`, `undefined` và `NaN` sẽ chuyển đổi thành `false`.
- Giá trị khác chuyển đổi thành `true`.

Vì vậy code bên dưới sẽ không được thực thi:

```js
if (0) { // 0 is falsy
  ...
}
```

...và ví dụ bên dưới, code được thực thi:

```js
if (1) { // 1 is truthy
  ...
}
```

Cũng có thể dùng một biểu thức được convert trước thành Boolean vào `if` :

```js
let cond = (year == 2015); // equality evaluates to true or false

if (cond) {
  ...
}
```

## Mệnh đề "else"

Lệnh `if` có thể chứa thêm mệnh đề "else" phía sau. Code trong `else block` sẽ được thực thi nếu biểu thức điều kiện là `false`.

Ví dụ:
```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year == 2015) {
  alert( 'You guessed it right!' );
} else {
  alert( 'How can you be so wrong?' ); // any value except 2015
}
```

## Sử dụng "else if" cho nhiều btđk

Khi có nhiều btđk chúng ta dùng mệnh đề `else if` .

VD:

```js run
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year < 2015) {
  alert( 'Too early...' );
} else if (year > 2015) {
  alert( 'Too late' );
} else {
  alert( 'Exactly!' );
}
```

Ở code trên, JavaScript đầu tiên sẽ kiểm tra btdk `year < 2015`. Nếu sai thì tiếp tục kiểm tra btđk `year > 2015`, nếu sai tiếp thì thực thi lệnh `alert`.

Có thể có thêm nhiều `else if` . Và kết thúc là `else` (optional).

## phép '?'

Thỉnh thoảng chúng ta cần gán giá trị cho biến phụ thuộc vào điều kiện nào đó.

Ví dụ:

```js run no-beautify
let accessAllowed;
let age = prompt('How old are you?', '');

*!*
if (age > 18) {
  accessAllowed = true;
} else {
  accessAllowed = false;
}
*/!*

alert(accessAllowed);
```

Chúng ta sẽ dùng `?` cho ví dụ trên, code sẽ ngắn và đơn giản hơn.

Phép toán `"?"` là phép toán duy nhất trong JS mà có 3 toán hạng.

Cú pháp như sau:
```js
let result = condition ? value1 : value2
```

Biểu thức điều kiện `condition` được kiểm tra, nếu đúng thì `value1` được trả về, ngược lại sẽ trả về `value2`.

Ví dụ:

```js
let accessAllowed = (age > 18) ? true : false;
```

Về mặt kỹ thuật chúng ta có thể bõ đi cặp dấu ngoặc bao `age > 18`. Phép `?` có độ ưu tiên khá thấp, do đó phép `>` sẽ được thực thi trước, vì vậy kết quả cuối cùng sẽ không thay đổi:

```js
// the comparison operator "age > 18" executes first anyway
// (no need to wrap it into parentheses)
let accessAllowed = age > 18 ? true : false;
```

...Nhưng cặp dấu ngoặc làm code dễ đọc hơn. Do đó bạn nên sử dụng.

````smart
Trong ví dụ trên có thể bõ đi `?` bởi vì phép so sánh cũng sẽ trả về giá trị `true/false`:

```js
// the same
let accessAllowed = age > 18;
```
````

## Sử dụng nhiều phép '?'

Sử dụng nhiều phép `"?"` cho phép trả về giá trị phụ thuộc vào btđk.

Ví dụ:
```js run
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';

alert( message );
```

Mới nhìn vào hơi khó hiểu. Nhìn kỹ và cố gắng hiểu thì bạn sẽ thấy thực ra chỉ là một chuỗi các bước kiểm tra mà thôi

1. Đầu tiên kiểm tra btđk `age < 3`.
2. Nếu true -- trả về `'Hi, baby!'`, trả về `age < 18`. Đây sẽ thực hiện tiếp kiểm tra biểu thức này
3. Nếu true -- trả về `'Hello!'`, ngược lại thì tiếp tục kiểm tra `age < 100`.
4. Nếu true -- trả về `'Greetings!'`, ngược lại thì trả về `'What an unusual age!'`.

Các bước trên cũng áp dụng tương tự đối với `if..else`:

```js
if (age < 3) {
  message = 'Hi, baby!';
} else if (a < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
```

## Non-traditional use of '?'

Sometimes the question mark `'?'` is used as a replacement for `if`:

```js run no-beautify
let company = prompt('Which company created JavaScript?', '');

*!*
(company == 'Netscape') ?
   alert('Right!') : alert('Wrong.');
*/!*
```

Depending on the condition `company == 'Netscape'`, either the first or the second part after `"?"` gets executed and shows the alert.

We don't assign a result to a variable here. The idea is to execute different code depending on the condition.

**It is not recommended to use the question mark operator in this way.**

The notation seems to be shorter than `if`, which appeals to some programmers. But it is less readable.

Here is the same code with `if` for comparison:

```js run no-beautify
let company = prompt('Which company created JavaScript?', '');

*!*
if (company == 'Netscape') {
  alert('Right!');
} else {
  alert('Wrong.');
}
*/!*
```

Our eyes scan the code vertically. The constructs which span several lines are easier to understand than a long horizontal instruction set.

The idea of a question mark `'?'` is to return one or another value depending on the condition. Please use it for exactly that. There is `if` to execute different branches of the code.
