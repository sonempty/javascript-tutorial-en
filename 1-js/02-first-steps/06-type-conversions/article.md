# Ép kiểu

Trong JS, các phép toán và hàm thường thực hiện chuyển đổi giá trị về đúng kiểu dữ liệu trước khi thực hiện tính toán. Chúng ta gọi đó là ép kiểu hay "type conversion".

Ví dụ, `alert` sẽ tự động chuyển đổi bất cứ giá trị nào thành `string` trước khi show ra màn hình. Hay các phép tính toán toán học thì convert giá trị về kiểu số.

Trong nhiều trường hợp chúng ta cần sự chuyển đổi này một cách rõ ràng để code được chính xác.

[cut]

```smart header="Chưa nói về Object"
Chương này chưa nói về Object. Học về các kiểu primitives trước. Sau đó sẽ học về Object và học luôn ép kiểu trên Object ở chương <info:object-toprimitive>.
```

## ToString

Ép kiểu string xảy ra khi cần một giá trị đưa vào là string.

Ví dụ, `alert(value)` sẽ show lên giá trị của `value`.

Chúng ta cũng có thể dùng `String(value)` để ép kiểu sang string:

```js run
let value = true;
alert(typeof value); // boolean

*!*
value = String(value); // now value is a string "true"
alert(typeof value); // string
*/!*
```

Ép kiểu string là chuyển đổi nguyên dạng. VD: `false` thành `"false"`, `null` thành `"null"` vv.

## ToNumber

Ép kiểu number xảy ra trong các hàm hoặc biểu thức toán học.

Ví dụ khi dùng phép chia `/` trên các giá trị không phải number:

```js run
alert( "6" / "2" ); // 3, strings are converted to numbers
```

Cũng có thể dùng `Number(value)` để chuyển đổi `value` sang kiểu number một cách rõ ràng:

```js run
let str = "123";
alert(typeof str); // string

let num = Number(str); // becomes a number 123

alert(typeof num); // number
```

Chuyển đổi number một cách rõ ràng thường được dùng khi input dạng text và chúng ta mong muốn nhận được là một giá trị số.

Nếu chuỗi nhập vào là không phải "dạng số" thì sẽ trả về `NaN`, Ví dụ:

```js run
let age = Number("an arbitrary string instead of a number");

alert(age); // NaN, conversion failed
```

Quy tắc ép kiểu number:

| Value |  Becomes... |
|-------|-------------|
|`undefined`|`NaN`|
|`null`|`0`|
|<code>true&nbsp;and&nbsp;false</code> | `1` và `0` |
| `string` | Dấu space bắt đầu chuỗi bị loại bõ. Nếu chuỗi là rỗng thì trả về `0`. Ngược lại sẽ tiến hành chuyển đổi. Nếu có lỗi sẽ trả về `NaN`. |

Ví dụ:

```js run
alert( Number("   123   ") ); // 123
alert( Number("123z") );      // NaN (error reading a number at "z")
alert( Number(true) );        // 1
alert( Number(false) );       // 0
```

Lưu ý rằng `null` và `undefined` sẽ được chuyển đổi khác nhau: `null` trả về 0, trong khi `undefined` trả về `NaN`.

````smart header="Phép '+' nối chuỗi"
Hầu hết các phép tính toán học sẽ chuyển đổi giá trị sang số. ngoại truwfp phép `+`. Nếu có một số hạng là string, thì sẽ chuyển đổi sang string, và tiến hành nối chuỗi.

Ví dụ:

```js run
alert( 1 + '2' ); // '12' (string to the right)
alert( '1' + 2 ); // '12' (string to the left)
```

Điều này xảy ra chỉ khi một trong hai số hạng là string.
````

## ToBoolean

Ép kiểu logic thì đơn giản hơn.

Xảy ra trong các phép logic, hoặc chuyển đổi một cách rõ ràng với `Boolean(value)`.

Quy ước:

- Các giá trị thể hiện sự trống rỗng như `0`, một chuỗi rỗng, `null`, `undefined` và `NaN` sẽ trả về `false`.
- Các giá trị khác trả về `true`.

Ví dụ:

```js run
alert( Boolean(1) ); // true
alert( Boolean(0) ); // false

alert( Boolean("hello") ); // true
alert( Boolean("") ); // false
```

````warn header="Chú ý là chuỗi `\"0\"` trả về `true`"
Một số NNLT (như PHP) thì chuỗi `"0"` trả về `false`, khác với JavaScript nhé.

```js run
alert( Boolean("0") ); // true
alert( Boolean(" ") ); // spaces, also true (any non-empty string is true)
```
````


## Tóm tắt

Có ba kiểu ép kiểu phổ biến: to string, to number và to boolean.

**`ToString`** -- xảy ra khi cần output dạng string. hoặc có thể dùng `String(value)`. Sự chuyển đổi là nguyên bản.

**`ToNumber`** -- Xảy ra trong các phép tính toán toán học . hoặc có thể dùng `Number(value)`.

Sự chuyển đổi  number tuân theo nguyên tắc:

| Value |  Becomes... |
|-------|-------------|
|`undefined`|`NaN`|
|`null`|`0`|
|<code>true&nbsp;/&nbsp;false</code> | `1 / 0` |
| `string` | chuyển đổi như sô được nhập vào dạng text, bỏ qua khoảng trắng hai đầu. Chuỗi rỗng "" trả về `0`. Có lỗi trả về `NaN`. |

**`ToBoolean`** -- Xảy ra trong các tính toán logic, hoặc có thể dùng `Boolean(value)`.

Theo nguyên tắc:

| Value |  Becomes... |
|-------|-------------|
|`0`, `null`, `undefined`, `NaN`, `""` |`false`|
|Giá trị khác| `true` |


Hầu hết các quy tắc đều dễ hiểu và dễ nhớ, nhưng có một vài điểm mà mọi người hay nhầm lẫn như sau:

- `undefined` trả về `NaN` là một số, cứ không phải trả về `0`.
- `"0"` và chuỗi toàn dấu space `"   "` trả `true` trong ép kiểu boolean.

Ép kiểu Object không nói ở bài này, chúng ta sẽ học ở chương <info:object-toprimitive>.
