# Vòng lặp: while và for

Thỉnh thoảng chúng ta cần lặp lại các hành động tương tự nhiều lần.

Ví dụ in ra tên hàng trong một list các mặt hàng, hay in ra các số từ 1 đên 100.

*Loops* - Vòng lặp được sử dụng để thực hiện các công việc này.

[cut]

## Vòng lặp "while"

Cú pháp:

```js
while (condition) {
  // code
  // so-called "loop body"
}
```

Khi `condition` là `true`, thì `code` trong phần thân của vòng lặp sẽ được thực thi.

Ví dụ, in ra `i` khi `i < 3`:

```js run
let i = 0;
while (i < 3) { // shows 0, then 1, then 2
  alert( i );
  i++;
}
```

Một lần thực thi code trong phần thân vòng lặp được gọi là *an iteration*. Vòng lặp trong ví dụ trên có 3 iterations.

Nếu không có lệnh `i++` trong ví dụ trên, vòng lặp sẽ lặp (theo lý thuyết) mãi mãi. Trong thực tế trình duyệt sẽ có cách để stop những vòng lặp mãi mãi, và nếu code ở phần JavaScript-server-side chúng ta có thể chấm dứt tiến trình (kill the process).

Không chỉ riêng biểu thức so sánh, một biểu thức bất kỳ hay một giá trị có thể là btđk của vòng lặp. Chúng sẽ được đánh giá và convert sang boolean bởi `while`.

Ví dụ cách viết ngắn hơn cho `while (i != 0)` là `while (i)`:

```js run
let i = 3;
*!*
while (i) { // when i becomes 0, the condition becomes falsy, and the loop stops
*/!*
  alert( i );
  i--;
}
```

````smart header="Có thể bõ cặp `{…}` ngoặc nếu chỉ có một lệnh trong thân"

```js run
let i = 3;
*!*
while (i) alert(i--);
*/!*
```
````

## Vòng lặp "do..while"

Btđk nằm phía *dưới* phần thân của vòng lặp `do..while`, cú pháp:

```js
do {
  // loop body
} while (condition);
```

Vòng lặp thực thi code trong phần thân trước, sau đó kiểm tra đk nếu là truthy, thực hiện code một lần nữa.

Ví dụ:

```js run
let i = 0;
do {
  alert( i );
  i++;
} while (i < 3);
```

Cú pháp này ít khi được sử dụng trừ khi bạn muốn phần body được thực thi **ít nhất 1 lần** bất kể btđk là truthy. Thông thường thì `while(…) {…}` hay được dùng hơn.

## Vòng lặp "for"

Vòng lặp `for` là vòng lặp hay được sử dụng nhất.

Cú pháp:

```js
for (begin; condition; step) {
  // ... loop body ...
}
```

Chúng ta sẽ học về 3 thành phần của `for` qua các ví dụ. Ví dụ bên dưới lệnh `alert(i)` được thực thi với `i` chạy từ `0` đến (nhưng ko bao gồm) `3`:

```js run
for (let i = 0; i < 3; i++) { // shows 0, then 1, then 2
  alert(i);
}
```

Chúng ta cùng xem xét `for` theo từng phần:

| part  |          |                                                                            |
|-------|----------|----------------------------------------------------------------------------|
| begin | `i = 0`    | Thực hiện một lần khi bước vào vòng lặp.                                      |
| condition | `i < 3`| Kiểm tra trước khi thực thi iteration, Nếu `false` thì dừng vòng lặp.              |
| step| `i++`      | Thực thi sau mỗi iteration, nhưng trước khi kiểm tra đk. |
| body | `alert(i)`| chạy lặp đi lặp lại nếu đk là truthy                         |


Thuật toán của vòng lặp hoạt động như thế này:
```
Run begin
→ (if condition → run body and run step)
→ (if condition → run body and run step)
→ (if condition → run body and run step)
→ ...
```


Đối với ví dụ trên:

```js
// for (let i = 0; i < 3; i++) alert(i)

// run begin
let i = 0
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// ...finish, because now i == 3
```

````smart header="khai báo biến inline"
Biến `i` được khai báo trong vòng loop. Đó được gọi là khai báo biến "inline". Những biến này chỉ sử dụng được trong vòng lặp.

```js run
for (*!*let*/!* i = 0; i < 3; i++) {
  alert(i); // 0, 1, 2
}
alert(i); // error, no such variable
```

Thay vì khai báo biến, cũng có thể sử dụng biến có sẵn:

```js run
let i = 0;

for (i = 0; i < 3; i++) { // use an existing variable
  alert(i); // 0, 1, 2
}

alert(i); // 3, visible, because declared outside of the loop
```

````


### Lược bỏ thành phần

Có thể lược bỏ bất cứ thành phần nào của `for`.

Ví dụ chúng ta lược bỏ `begin` nếu không cần giá trị khởi tạo.

Like here:

```js run
let i = 0; // we have i already declared and assigned

for (; i < 3; i++) { // no need for "begin"
  alert( i ); // 0, 1, 2
}
```

Lược bõ `step`:

```js run
let i = 0;

for (; i < 3;) {
  alert( i++ );
}
```

Vòng lặp trên giống như `while (i < 3)`.

Có thể lược bỏ tất cả để tạo ra một vòng lặp vô hạn:

```js
for (;;) {
  // repeats without limits
}
```

Chú ý trong `for` dùng 2 dấu `;` nếu không sẽ báo lỗi cú pháp.

## Thoát vòng lặp

Bình thường thì vòng lặp kết thúc khi đk là falsy.

Nhưng chúng ta cũng có thể dừng vòng lặp bất cứ khi nào bằng một chỉ thị đặc biệt có tên là `break`.

Ví dụ vòng lặp hỏi người dùng nhập vào một dãy số, và sẽ thoát nếu không có số nào được nhập vào:

```js
let sum = 0;

while (true) {

  let value = +prompt("Enter a number", '');

*!*
  if (!value) break; // (*)
*/!*

  sum += value;

}
alert( 'Sum: ' + sum );
```

Chỉ thị `break` được chạy ở dòng `(*)` nếu user nhập vào dòng trống hoặc nhấn cancel. Nó dừng vòng lặp ngay lập tức, và đưa chương trình đến dòng code tiếp theo sau vòng lặp.  `alert`.

Sự kết hợp của "infinite loop" và `break` hay dùng cho các trường hợp đk ko phải được kiểm tra ở đầu hay cuối vòng lặp, mà ở giữa vòng lặp hay bất cứ đâu trong body.

## Chỉ thị Continue [#continue]

Chỉ thị `continue` dừng lại iteration hiện thời và chuyển vòng lặp đến lần lặp mới .

Sử dụng `continue` để in ra các số lẽ:

```js run no-beautify
for (let i = 0; i < 10; i++) {

  // if true, skip the remaining part of the body
  *!*if (i % 2 == 0) continue;*/!*

  alert(i); // 1, then 3, 5, 7, 9
}
```

Với giá trị `i` chẵn, chỉ thị `continue` dừng sự thực thi trong body, chuyển vòng lặp qua iteration tiếp theo. Cho nên lệnh `alert` chỉ được gọi cho các giá trị lẽ.

````smart header="Chỉ thị `continue` giảm việc nesting trong code"
Vòng lặp trên có thể viết:

```js
for (let i = 0; i < 10; i++) {

  if (i % 2) {
    alert( i );
  }

}
```

Hai cách dùng ở trên là tương đương nhau.

Nhưng nếu mã code trong `if` nhiều hơn thì code của ta sẽ khó đọc hơn vì nó thụt vào.
````

````warn header="Không dùng `break/continue` bên phải '?'"
Không được dùng trong biểu thức với `'?'`. Chỉ thị `break/continue` không được chấp nhận ở đây.

Ví dụ ta có code:

```js
if (i > 5) {
  alert(i);
} else {
  continue;
}
```

...Và viết lại với `?`:


```js no-beautify
(i > 5) ? alert(i) : *!*continue*/!*; // continue not allowed here
```

...sẽ không chạy được. Code sẽ báo lỗi cú pháp:


Đây là lý do đừng sử dụng `'?'` thay cho `if`.
````

## Đánh nhãn cho break/continue

Thỉnh thoảng ta muốn break vòng lặp nào đó trong nhiều vòng lặp chồng nhau.

Ví du hai vòng lặp chồng nhau `i` và `j`:

```js run no-beautify
for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // what if I want to exit from here to Done (below)?

  }
}

alert('Done!');
```

Chúng ta cần stop vòng lặp nếu user nhấn cancels hoặc không nhập vào gì cả.

Nếu dùng `break` sau `input` chỉ thoát được vòng lặp chứa nó. Chứ không thoát cả 2 vòng lặp. Sử dụng *label* để giải quyết vấn đề này.

Một nhã *label* là một cái tên đặt cho vòng lặp, cú pháp:
```js
labelName: for (...) {
  ...
}
```

Chỉ thị `break <labelName>` thoát khỏi vòng lặp có tên là labelName.

Như thế này:

```js run no-beautify
*!*outer:*/!* for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // if an empty string or canceled, then break out of both loops
    if (!input) *!*break outer*/!*; // (*)

    // do something with the value...
  }
}
alert('Done!');
```

Ở ví dụ trên `break outer` tìm vòng lặp nào có tên là `outer` và thoát khỏi nó.

và chương trình nhảy từ `(*)` sang `alert('Done!')`.

Có thể viết ra các dòng như này:

```js no-beautify
outer:
for (let i = 0; i < 3; i++) { ... }
```

Chỉ thị `continue` cũng có thể dùng với label. 

Chỉ thị `break/continue` chỉ hoạt động được trong loops.

Ví dụ như thế này sẽ báo lỗi:
```js
break label;  // jumps to label? No.

label: for (...)
```

````

## Tóm tắt

Chúng ta đã học 3 loại vòng lặp:

- `while` -- đk được kiểm tra trước mỗi iteration.
- `do..while` -- đk được kiểm tra sau mỗi iteration.
- `for (;;)` -- đk được kiểm tra trước mỗi iteration, có thêm phần step settings sau mỗi iteration.

Sử dụng vòng lặp vô hạn với `while(true)` , những vòng lặp như thế này có thể dùng chỉ thị `break` để dừng lại.

Chỉ thị `continue` để bõ qua iteration hiện thời và tiếp tục lần lặp mới.

`Break/continue` hỗ trợ label. Label là cách để `break/continue` thoát khỏi các vòng lặp chồng nhau.
