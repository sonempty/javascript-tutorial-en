# Các phép toán

Một vài phép toán chúng ta đã biết khi học ở trường. Như `+`, `-`, `*`, `/`, và vv.

Trong chương này chúng ta sẽ tập trung vào các ngoại lệ, hay sự khác biệt trong các phép toán trong JS và toán học.

[cut]

## Quy tắc: Một ngôi "unary", hai ngôi "binary" và toán hạng "operand"

Trước khi tiếp tục, chúng ta hãy nắm bắt các thuật ngữ phổ biến.

- *Toán hạng - An operand* -- là đối tượng của phép toán. Ví dụ trong phép nhân `5 * 2` có hai toán hạng: toán hạng bên trái là `5`, và toán hạng bên phải là `2`. Thỉnh thoảng người ta cũng gọi là tham số "arguments" thay vì toán hạng "operands".
- Phép toán là một ngôi *unary* nếu chỉ có 1 toán hạng. Ví dụ phép `"-"` đổi dấu một số:

    ```js run
    let x = 1;

    *!*
    x = -x;
    */!*
    alert( x ); // -1, unary negation was applied
    ```
- Phép toán là hai ngôi *binary* nếu có 2 toán hạng, tương tự n ngôi nếu có n toán hạng:

    ```js run no-beautify
    let x = 1, y = 3;
    alert( y - x ); // 2, binary minus subtracts values
    ```

    Chúng ta chủ yếu nói đến sự khác nhau giữa hai phép toán: the unary negation (phép đổi dấu) và the binary subtraction (phép trừ hai số).

## phép + là một phép toán hai ngôi - binary +

Chúng ta sẽ xem xem JS khác tóa học như thế nào.

Thông thường phép `'+'` để cộng các số.

nhưng nếu binary `+` mà có 1 toán hạng là string, thì thành phép nối chuỗi:

```js
let s = "my" + "string";
alert(s); // mystring
```

Chú ý là nếu có 1 toán hạng là string thì toán hạng kia sẽ được chuyển đổi thành string.

Ví dụ:

```js run
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

Trong JS phép `"+"` hơi đặc biệt. Các phép toán học khác chỉ làm việc với number, Còn phép + có thể làm việc với number và string.

Ví dụ phép trừ và phép chia:

```js run
alert( 2 - '1' ); // 1
alert( '6' / '2' ); // 3
```

## Ép kiểu number, unary +

Phép `+` có thể là phép toán 2 ngôi hoặc cũng có thể là 1 ngôi.

Phép `+` một ngôi đơn giản là chính nó. Tương tự như toán học vậy.

Ví dụ:

```js run
// No effect on numbers
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

*!*
// Converts non-numbers
alert( +true ); // 1
alert( +"" );   // 0
*/!*
```

Nó tương đương với `Number(...)`, nhưng viết ngắn hơn.

Nhu cầu chuyển đổi string sang số là khá nhiều. VD: Viết chương trình cộng 2 số được nhập từ bàn phím. Hay chuyển đổi giá trị nào đó từ form HTML

VD:

```js run
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", the binary plus concatenates strings
```

Nếu muốn là number thì ta làm như sau:

```js run
let apples = "2";
let oranges = "3";

*!*
// both values converted to numbers before the binary plus
alert( +apples + +oranges ); // 5
*/!*

// the longer variant
// alert( Number(apples) + Number(oranges) ); // 5
```

Theo quan điểm toán học, viết các dấu + như vậy có vẻ là lạ, nhưng trên quan điểm tin học, điều đó là bình thường: unary + được ưu tiên trước, chuyển đổi strings sang numbers, và sau đó binary + sẽ cộng chúng lại.

Tại sao phép toán một ngôi lại được tính trước phép toán hai ngôi? Vì theo quy ước nó được ưu tiên hơn *higher precedence*.

## Độ ưu tiên của các phép toán

Nếu một biểu thức có nhiều phép toán thì thằng nào tính trước, thằng nào tính sau?

Ở trường các bạn được học là nhân chia trước, cộng trừ sau. Ví dụ `1 + 2 * 2` cho ra kết quả là 5, ta nói phép nhân có độ ưu tiên cao hơn phép cộng.

Biểu thức trong ngoặc thì sẽ tính trước, Ví dụ trên nếu muốn phép cộng tính trước thì ta viết `(1 + 2) * 2`.

Trong JavaScript. Phép toán có độ ưu tiên cao hơn thì được thực thi trước, nếu có độ ưu tiên bằng nhau thì thực thi từ trái sang phải.

Chi tiết độ ưu tiên các bạn có thể xem tại [precedence table](https://developer.mozilla.org/en/JavaScript/Reference/operators/operator_precedence) Không cần bạn phải nhớ chi tiết, Đơn giản chỉ cần nhớ là phép toán một ngôi sẽ có độ ưu tiên cao hơn phép toán hai ngôi:

| Độ ưu tiên | Phép toán | ký tự |
|------------|------|------|
| ... | ... | ... |
| 16 | Cộng một ngôi | `+` |
| 16 | đổi dấu | `-` |
| 14 | nhân | `*` |
| 14 | chia | `/` |
| 13 | cộng | `+` |
| 13 | trừ | `-` |
| ... | ... | ... |
| 3 | gán | `=` |
| ... | ... | ... |

Ta có thể thấy "Phép cộng một ngôi" có độ ưu tiên là `16`, cao hơn phép cộng hai ngôi có độ ưu tiên `13` . Đó là lý do tại sao trong biểu thức `"+apples + +oranges"` Phép cộng một ngôi được tính trước.

## Phép gán

Chú ý rằng phép gán `=` cũng là một phép toán. Và nó có độ ưu tiên khá thấp là `3`.

Đó là lý do tại sao khi ta gán, ví dụ `x = 2 * 2 + 1`, thì giá trị được tính toán trước rồi mới gán `=` cho `x`.

```js
let x = 2 * 2 + 1;

alert( x ); // 5
```

Cũng có thể gán chồng nhau nhiều lần như thế nào:

```js run
let a, b, c;

*!*
a = b = c = 2 + 2;
*/!*

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

Gán chồng nhau sẽ thực hiện từ phải qua trái `2 + 2` ra `4` gán cho `c`, `b` rồi đến `a`.

````smart header="Phép gán `\"=\"` trả về giá trị"
Các phép toán trả về giá trị là kết quả của phép toán đó. ví dụ `5 + 5` kết quả là 10, và cũng là `return 10`. Tương tự phép gán cũng thế.

Ví dụ `x = value` gán `value` cho `x` *và cũng: return value*.

Ví dụ phức tạp hơn:

```js run
let a = 1;
let b = 2;

*!*
let c = 3 - (a = b + 1);
*/!*

alert( a ); // 3
alert( c ); // 0
```

Ở ví dụ trên, kết quả `(a = b + 1)` là giá trị gán cho `a` (đó là `3`). sau đó thực hiện phép trừ  `3 - 3`.

Code trên cho vui để hiểu thêm thôi, chứ không nên viết kiểu thách đố như vậy không hay lắm.
````

## Phép thặng dư %

Phép thặng dư `%` , không phải là phần trăm đâu nhé :D .

Kết quả của `a % b` là phân dư của phép chia nguyên `a` cho `b`.

ví dụ:

```js run
alert( 5 % 2 ); // 1 is a remainder of 5 divided by 2
alert( 8 % 3 ); // 2 is a remainder of 8 divided by 3
alert( 6 % 3 ); // 0 is a remainder of 6 divided by 3
```

## Lũy thừa **

Phép lũy thừa `**` vừa được thêm vào JS mới đây.

Với số nguyên `b`, kết quả của `a ** b` là `a` lũy thừa `b`.

Ví dụ:

```js run
alert( 2 ** 2 ); // 4  (2 * 2)
alert( 2 ** 3 ); // 8  (2 * 2 * 2)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2)
```

Cũng có thể thực hiện trên các số không nguyên `a` và `b` như ví dụ:

```js run
alert( 4 ** (1/2) ); // 2 (power of 1/2 is the same as a square root, that's maths)
alert( 8 ** (1/3) ); // 2 (power of 1/3 is the same as a cubic root)
```

## Increment/decrement

<!-- Can't use -- in title, because built-in parse turns it into – -->

Tăng một đơn vị ++ và giảm 1 đơn vị -- .

Ví dụ:

- **Increment** `++` tăng giá trị biến lên 1:

    ```js run no-beautify
    let counter = 2;
    counter++;      // works same as counter = counter + 1, but shorter
    alert( counter ); // 3
    ```
- **Decrement** `--` giảm giá trị đi 1:

    ```js run no-beautify
    let counter = 2;
    counter--;      // works same as counter = counter - 1, but shorter
    alert( counter ); // 1
    ```

```warn
Increment/decrement chỉ tác động lên biến. Nếu dùng vào hằng VD `5++` sẽ báo lỗi.
```

Phép `++` và `--` có thể dùng trước hoặc sau biến.

- Nếu dùng sau thì gọi là "postfix form": `counter++`.
- gọi là "prefix form" nếu dùng trước `++counter`.

Cả hai cách đều là tăng `counter` lên `1`.

Hai cách dùng `++/--` có gì khác nhau không? Có khác, nhưng chúng ta chỉ thây sự khác biệt này khi dùng với `return` .

Như chúng ta đã biết, phép toán nào cũng trả về giá trị nào đó. Increment/decrement cũng không ngoại lệ. Dùng kiểu prefix form trả về giá trị mới, trong khi postfix form trả về giá trị cũ (trước khi tăng/giảm).

Để xem sự khác biệt này, cùng xem ví dụ sau:

```js run
let counter = 1;
let a = ++counter; // (*)

alert(a); // *!*2*/!*
```

Dòng `(*)` Dùng kiểu  prefix form `++counter` tăng `counter` lên một đơn vị và trả về *giá trị mới* là `2` và sau đó gán cho `a`. nên `alert` show ra `2`.

Bây giờ dùng thử postfix form:

```js run
let counter = 1;
let a = counter++; // (*) changed ++counter to counter++

alert(a); // *!*1*/!*
```

Dòng `(*)` Dùng kiểu *postfix* form `counter++` cũng tăng `counter` lên 1, nhưng trả về *giá trị cũ* (trước khi tăng). Nên `alert` show ra `1`.

Tổng kết:

- Nếu kết quả của phép increment/decrement không được sử dụng ngay thì không thấy sự khác biệt giữa hai kiểu dùng:

    ```js run
    let counter = 0;
    counter++;
    ++counter;
    alert( counter ); // 2, the lines above did the same
    ```
- Nếu muốn tăng/giảm giá trị của biến và *dùng ngay* lập tức kết quả mới này thì dùng kiểu prefix form:

    ```js run
    let counter = 0;
    alert( ++counter ); // 1
    ```
- Nếu tăng/giảm giá trị của biến nhưng vẫn sử dụng giá trị của nó khi chưa tăng/giảm thì dùng kiểu postfix form:

    ```js run
    let counter = 0;
    alert( counter++ ); // 0
    ```

````smart header="Increment/decrement giữa các phép toán khác"
Phép `++/--` có thể sử dụng trong biểu thức. Độ ưu tiên của nó cao hơn các phép tính toán toán học.

Ví dụ:

```js run
let counter = 1;
alert( 2 * ++counter ); // 4
```

So sánh với:

```js run
let counter = 1;
alert( 2 * counter++ ); // 2, because counter++ returns the "old" value
```

Mặc dù không có lỗi gì, nhưng tính toán nhiều thứ trên một dòng thì khó đọc - not good. Nên viết tách ra.

Nên dùng code kiểu "one line -- one action" - một dòng một hành động:

```js run
let counter = 1;
alert( 2 * counter );
counter++;
```
````

## Phép toán nhị phân

Phép toán nhị phân đưa các tham số về dạng 32 bits số nguyên và thực hiện trên các bits đó.

Phép toán nhị phân không phải là đặc trưng của JS, nó chủ yếu cho các ngôn ngữ khác.

Các phép toán nhị phân:

- AND ( `&` )
- OR ( `|` )
- XOR ( `^` )
- NOT ( `~` )
- LEFT SHIFT ( `<<` )
- RIGHT SHIFT ( `>>` )
- ZERO-FILL RIGHT SHIFT ( `>>>` )

Trong JS hiếm khi bạn dùng đến các phép toán nhị phân. Nếu muốn hiểu thêm, có thể đọc tài liệu này [Bitwise Operators](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators).

## Modify-in-place

Chúng ta thường cần sử dụng giá trị của biến sau một phép tính toán ở trên biến đó.

Ví dụ:

```js
let n = 2;
n = n + 5;
n = n * 2;
```

Có thể thực hiện nhanh việc này bằng `+=` và `*=`:

```js run
let n = 2;
n += 5; // now n = 7 (same as n = n + 5)
n *= 2; // now n = 14 (same as n = n * 2)

alert( n ); // 14
```

Kiểu như trên gọi là phép "modify-and-assign" , nó cũng hỗ trợ hầu hết các phép toán khác như: `/=`, `-=` etc.

Các phép toán kiểu này có độ ưu tiên như phép gán, VD:

```js run
let n = 2;

n *= 3 + 5;

alert( n ); // 16  (right part evaluated first, same as n *= 8)
```

## Dấu phẩy - Comma

Dấu `','` là một phép toán hiếm khi được dùng. Nhưng thỉnh thoảng vẫn được sử dụng để viết code ngắn hơn

Phép comma `','` để chia cách các biểu thức, nhưng sẽ chỉ lấy giá trị cuối cùng.

Ví dụ:

```js run
*!*
let a = (1 + 2, 3 + 4);
*/!*

alert( a ); // 7 (the result of 3 + 4)
```

Ở đây, biểu thức `1 + 2` được tính toán nhưng kq bị bõ đi, sau đó `3 + 4` được tính toán và trả về.

```smart header="Comma có độ ưu tiên rất thấp"
thấp hơn cả phép gán `=`, nên cần cặp dấu ngoặc như bạn thấy ở trên.

Nếu không có cặp dấu ngoặc: `a = 1 + 2, 3 + 4` thực hiện `+` trước, và sẽ thành `a = 3, 7`, sau đó `=` gán `a = 3`, và cuối cùng số `7` được trả về cho biểu thức này. (a vẫn = 3 nhé)
```

Vậy tại sao lại dùng comma, đằng nào kq cũng bị bõ đi trừ biểu thức cuối cùng mà?

Thỉnh thoảng người ta dùng nó để đưa vào những biểu thức phức tạp, thực hiện một loạt hành động trên một dòng.

ví dụ:

```js
// three operations in one line
for (*!*a = 1, b = 3, c = a * b*/!*; a < 10; a++) {
 ...
}
```

Mẹo này hay được dùng trong các JS FrameWork hiện nay, nên mình đưa ra đây cho các bạn biết.
