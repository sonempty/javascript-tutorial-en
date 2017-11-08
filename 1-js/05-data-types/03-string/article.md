# Strings

Trong JavaScript, dữ liệu văn bản được lưu trữ dưới dạng strings. Kể cả các chữ cái đơn.

Định dạng string luôn là kiểu [UTF-16](https://en.wikipedia.org/wiki/UTF-16), Nó không gắn liền với mã hóa trang web.

[cut]

## Quotes

String được bao quanh bởi cặp dấu nháy đơn - single quotes hoặc nháy kép - double quotes hoặc backticks:

```js
let single = 'single-quoted';
let double = "double-quoted";

let backticks = `backticks`;
```

Single và double quotes là như nhau. Backticks là một template cho phép ta nhúng biến, biểu thức vào, bao gồm cả gọi hàm:

```js run
function sum(a, b) {
  return a + b;
}

alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3.
```

Sử dụng backticks cũng cho phép viết String trên nhiều dòng:

```js run
let guestList = `Guests:
 * John
 * Pete
 * Mary
`;

alert(guestList); // a list of guests, multiple lines
```

Nếu dùng single hoặc double quotes như ví dụ bên trên sẽ báo lỗi:
```js run
let guestList = "Guests:  // Error: Unexpected token ILLEGAL
  * John";
```


Backticks cũng cho phép ta sử dụng "template function" . Cú pháp: <code>func&#96;string&#96;</code>. Hàm `func` được gọi, nhận string và biểu thức được nhúng vào, sau đó xử lý chúng. Có thể tìm hiểu thêm tại [docs](mdn:JavaScript/Reference/Template_literals#Tagged_template_literals). Cái này được gọi là "tagged templates". Tính năng này cũng hiếm khi được sử dụng.


## Các ký tự đặc biệt

Ký tự `\n` đại diện cho xuống hàng:

```js run
let guestList = "Guests:\n * John\n * Pete\n * Mary";

alert(guestList); // a multiline list of guests
```

Ví dụ viết String trên 2 hàng bằng hai cách:

```js run
alert( "Hello\nWorld" ); // two lines using a "newline symbol"

// two lines using a normal newline and backticks
alert( `Hello
World` );
```

Một vài ký tự đặc biệt khác:

| Character | Description |
|-----------|-------------|
|`\b`|Backspace|
|`\f`|Form feed|
|`\n`|New line|
|`\r`|Carriage return|
|`\t`|Tab|
|`\uNNNN`|Một ký tự Unicode hex code `NNNN`, Ví dụ `\u00A9` -- là dấu bản quyền `©`.|
|`\u{NNNNNNNN}`|Một vài ký tự Unicode đặc biệt, chiếm 4 bytes. Nó cần được nằm trong cặp ngoặc nhọn.|

Vài ví dụ với unicode:

```js run
alert( "\u00A9" ); // ©
alert( "\u{20331}" ); // 佫, a rare chinese hieroglyph (long unicode)
alert( "\u{1F60D}"); // 😍, a smiling face symbol (another long unicode)
```

Một ký tự đặc biệt được bắt đầu bởi dấu `\`. Nó được gọi là ký tự thoát "escape character".

Cũng sử dụng khi string có dấu nháy.

For instance:

```js run
alert( 'I*!*\'*/!*m the Walrus!' ); // *!*I'm*/!* the Walrus!
```

Ta phải sử dụng `\'`, vì nó cũng đại diện cho bắt đầu và kết thúc string.

Tất nhiên nếu khác thì không cần sử dụng:

```js run
alert( `I'm the Walrus!` ); // I'm the Walrus!
```

Dấu `\` sẽ không hiển thị, nó chỉ dùng để thể hiện cho JS là biết là bắt đầu một ký tự đặc biệt. Trong bộ nhớ sẽ không có `\`.

Khi cần in ra dấu `\`trong string?

Ta dùng 2 dấu `\\`:

```js run
alert( `The backslash: \\` ); // The backslash: \
```

## String length


`length` property thể hiện độ dài của string:

```js run
alert( `My\n`.length ); // 3
```

Chú ý `\n` chỉ tính là một ký tự, nên ví dụ trên có độ dài là `3`.

```warn header="`length` là một property"
Đừng sử dụng nhầm `str.length()` thay vì `str.length`, như những ngôn ngữ khác.

Chú ý `str.length` là một property, không phải là một hàm. Nên khi gọi không có cặp dấu ngoặc tròn.
```

## Truy cập các phần tử của string

Lấy ký tự ở vị trí `pos`, sử dụng ngoặc vuông `[pos]` hoặc dùng method [str.charAt(pos)](mdn:js/String/charAt). Ký tự đầu tiên có vị trí bằng `0`:

```js run
let str = `Hello`;

// the first character
alert( str[0] ); // H
alert( str.charAt(0) ); // H

// the last character
alert( str[str.length - 1] ); // o
```
Dùng charAt là theo các bản JS cũ. bản ES6 nên dùng []
Sự khác nhau giữa chúng là, `[pos]` trả về `undefined`, và `charAt(pos)` trả về `''` khi không có vị trí `pos`.

```js run
let str = `Hello`;

alert( str[1000] ); // undefined
alert( str.charAt(1000) ); // '' (an empty string)
```

Duyệt qua string bằng `for..of`:

```js run
for(let char of "Hello") {
  alert(char); // H,e,l,l,o (char becomes "H", then "e", then "l" etc)
}
```

## Strings là immutable

Strings là không thể thay đổi trong JavaScript.

Ví dụ:

```js run
let str = 'Hi';

str[0] = 'h'; // error
alert( str[0] ); // doesn't work
```

Cho nên chỉ có thể gán lại, chứ không thể thay đổi:

```js run
let str = 'Hi';

str = 'h' + str[1];  // replace the string

alert( str ); // hi
```


## Viết hoa, thường

Methods [toLowerCase()](mdn:js/String/toLowerCase) và [toUpperCase()](mdn:js/String/toUpperCase) thay đổi kiểu hoa, thường của string:

```js run
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
```

hoặc, chỉ thay đổi một ký tự:

```js
alert( 'Interface'[0].toLowerCase() ); // 'i'
```

## tìm substring

Có nhiều cách để tìm một chuỗi con - substring trong một string cho trước.

### str.indexOf

Đầu tiên là method [str.indexOf(substr, pos)](mdn:js/String/indexOf).

Tìm `substr` trong `str`, bắt đầu từ vị trí `pos`, trả về vị trí chứa subtring hoặc `-1` nếu không tìm thấy.

Ví dụ:

```js run
let str = 'Widget with id';

alert( str.indexOf('Widget') ); // 0, because 'Widget' is found at the beginning
alert( str.indexOf('widget') ); // -1, not found, the search is case-sensitive

alert( str.indexOf("id") ); // 1, "id" is found at the position 1 (..idget with id)
```

Tham số `pos` là optional, mặc định bằng `0`.

Ví dụ, vị trí của `"id"` đầu tiên là `1`. tìm tiếp thì ta sử dụng với `pos` là `2`:

```js run
let str = 'Widget with id';

alert( str.indexOf('id', 2) ) // 12
```


Nếu muốn tìm hết, ta dùng `indexOf` trong vòng lặp.

```js run
let str = 'As sly as a fox, as strong as an ox';

let target = 'as'; // let's look for it

let pos = 0;
while (true) {
  let foundPos = str.indexOf(target, pos);
  if (foundPos == -1) break;

  alert( `Found at ${foundPos}` );
  pos = foundPos + 1; // continue the search from the next position
}
```

Cách ngắn hơn:

```js run
let str = "As sly as a fox, as strong as an ox";
let target = "as";

*!*
let pos = -1;
while ((pos = str.indexOf(target, pos + 1)) != -1) {
  alert( pos );
}
*/!*
```

```smart header="`str.lastIndexOf(pos)`"
Có một method tương tự [str.lastIndexOf(pos)](mdn:js/String/lastIndexOf), nó tìm từ cuối đến đầu string.

kết quả sẽ đảo ngược.
```

Có một sự bất tiện nhỏ với `indexOf` trong `if`. Như thế này:

```js run
let str = "Widget with id";

if (str.indexOf("Widget")) {
    alert("We found it"); // doesn't work!
}
```

Lệnh `alert` sẽ không được chạy vì `str.indexOf("Widget")` trả về `0`. Vì trong `if`, `0` là `false`.

Nên ta kiểm tra với `-1`, như này:

```js run
let str = "Widget with id";

*!*
if (str.indexOf("Widget") != -1) {
*/!*
    alert("We found it"); // works now!
}
```

````smart header="Phép nhị phân NOT"
Sử dụng toán tử [bitwise NOT](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators#Bitwise_NOT) `~`. Nó convert sang số nguyên dạng 32 bit (removes the decimal part if exists) và đảo ngược giá trị các bit.

Với số nguyên 32-bit, gọi `~n` tương đương `-(n+1)` (do định dạng IEEE-754).

Ví dụ:

```js run
alert( ~2 ); // -3, the same as -(2+1)
alert( ~1 ); // -2, the same as -(1+1)
alert( ~0 ); // -1, the same as -(0+1)
*!*
alert( ~-1 ); // 0, the same as -(-1+1)
*/!*
```

Ta thấy, `~n` là bằng `0` khi và chỉ khi `n == -1`.

Nên `if ( ~str.indexOf("...") )` là thứ ta cần cho ví dụ trên:

```js run
let str = "Widget";

if (~str.indexOf("Widget")) {
  alert( 'Found it!' ); // works
}
```

Tuy nhiên, việc viết như thế không được khuyến khích vì nó không rõ ràng

Just remember: `if (~str.indexOf(...))` reads as "if found".
````

### includes, startsWith, endsWith

Những methods này là có trong bản JS mới. Method [str.includes(substr, pos)](mdn:js/String/includes) trả về `true/false` phụ thuộc vào ciệc liệu `str` có bao gồm `substr` hay không.

Nếu không quan tâm đến `pos`:

```js run
alert( "Widget with id".includes("Widget") ); // true

alert( "Hello".includes("Bye") ); // false
```

`pos` trong `str.includes` thể hiện vị trị bắt đầu tìm kiếm:

```js run
alert( "Midget".includes("id") ); // true
alert( "Midget".includes("id", 3) ); // false, from position 3 there is no "id"
```

Methods [str.startsWith](mdn:js/String/startsWith) và [str.endsWith](mdn:js/String/endsWith):

```js run
alert( "Widget".startsWith("Wid") ); // true, "Widget" starts with "Wid"
alert( "Widget".endsWith("get") );   // true, "Widget" ends with "get"
```

## Lấy một substring

Có 3 methods trong JavaScript để lấy substring: `substring`, `substr` và `slice`.

`str.slice(start [, end])`
: Trả về một phần của str từ vị trí `start` đến (không bao gồm) `end`.

    Ví dụ:

    ```js run
    let str = "stringify";
    alert( str.slice(0,5) ); // 'strin', the substring from 0 to 5 (not including 5)
    alert( str.slice(0,1) ); // 's', from 0 to 1, but not including 1, so only character at 0
    ```

    Nếu không có tham số `end` thì `slice` chạy đến cuối string:

    ```js run
    let str = "st*!*ringify*/!*";
    alert( str.slice(2) ); // ringify, from the 2nd position till the end
    ```

    Giá trị ấm cho `start/end` được sử dụng, nó có ý nghĩa sẽ bắt đầu từ cuối tring:

    ```js run
    let str = "strin*!*gif*/!*y";

    // start at the 4th position from the right, end at the 1st from the right
    alert( str.slice(-4, -1) ); // gif
    ```


`str.substring(start [, end])`
: trả về một phần của string *giữa* `start` và `end`.

    Tương tự `slice`, nhưng chấp nhận `start` lớn hơn `end`.

    Ví dụ:


    ```js run
    let str = "st*!*ring*/!*ify";

    // these are same for substring
    alert( str.substring(2, 6) ); // "ring"
    alert( str.substring(6, 2) ); // "ring"

    // ...but not for slice:
    alert( str.slice(2, 6) ); // "ring" (the same)
    alert( str.slice(6, 2) ); // "" (an empty string)

    ```

    Số âm không được chấp nhận (không giống slice) nó sẽ xem như là `0`.


`str.substr(start [, length])`
: Trả về một phần của string, bắt đầu từ `start`, với  `length` ký tự.

    Ngược lại với các method trước, nó dùng `length` thay vì vị trí:

    ```js run
    let str = "st*!*ring*/!*ify";
    alert( str.substr(2, 4) ); // ring, from the 2nd position get 4 characters
    ```

    `start` có thể là số âm, nghĩa là đếm từ cuối string:

    ```js run
    let str = "strin*!*gi*/!*fy";
    alert( str.substr(-4, 2) ); // gi, from the 4th position get 2 characters
    ```

Let's recap these methods to avoid any confusion:

| method | selects... | negatives |
|--------|-----------|-----------|
| `slice(start, end)` | from `start` to `end` | allows negatives |
| `substring(start, end)` | between `start` and `end` | negative values mean `0` |
| `substr(start, length)` | from `start` get `length` characters | allows negative `start` |


```smart header="Nên dùng thằng nào?"
Dùng tất, nhưng thường thì sử dụng `slice` cho hầu hết các trường hợp.
```

## So sánh strings

Đã học trong chương <info:comparison>, strings được so sánh từng ký tự theo thứ tự trong bãng chữ cái.

Mặc dù, có một số sự kỳ quặc.

1. Chữ viết thường luôn lớn hơn chữ viết hoa:

    ```js run
    alert( 'a' > 'Z' ); // true
    ```

2. Chữ cái với dấu âm không sử dụng được:

    ```js run
    alert( 'Österreich' > 'Zealand' ); // true
    ```

    Đây là một kết quả kỳ lạ khi sắp xếp tên các quốc gia. Thường thì người ta mong muốn `Zealand` nằm ở sau `Österreich` trong danh sách.

Để hiểu những gì xảy ra ta xem lại các biểu diễn string trong JavaScript.

String được mã hóa theo định dạng [UTF-16](https://en.wikipedia.org/wiki/UTF-16). Đó là: Mỗi ký tự sẽ có một mã số. Có một method đặc biệt để lấy được mã số này.

`str.codePointAt(pos)`
: Trả về mã ký tự ở vị trí `pos`:

    ```js run
    // different case letters have different codes
    alert( "z".codePointAt(0) ); // 122
    alert( "Z".codePointAt(0) ); // 90
    ```

`String.fromCodePoint(code)`
: Tạo ra một ký tự với mã số là `code`

    ```js run
    alert( String.fromCodePoint(90) ); // Z
    ```

    Ta cũng có thể sử dụng mã Unicode với `\u` và hex code:

    ```js run
    // 90 is 5a in hexadecimal system
    alert( '\u005a' ); // Z
    ```

Giờ ta xem các ký tự với mã từ `65..220` :

```js run
let str = '';

for (let i = 65; i <= 220; i++) {
  str += String.fromCodePoint(i);
}
alert( str );
// ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
// ¡¢£¤¥¦§¨©ª«¬­®¯°±²³´µ¶·¸¹º»¼½¾¿ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖ×ØÙÚÛÜ
```

Thấy không, chữ hoa trước, rồi đến một vài ký tự đặc biệt, rồi đến chữ thường.

Giờ ta rõ ràng tại sao `a > Z`.

Ký tự được so sánh bởi mã của nó. Mã lớn hơn thì lớn hơn,  `a` (97) lớn hơn `Z` (90).

- Chữ thường lớn hơn chữ hoa.
- Các chữ cái `Ö` là một phần của bãng chữ cái, và nó có mã lớn hơn cả `a` đến `z`.


### Sự so sánh đúng

Thuật toán đúng để so sánh String là phức tạp hơn rất nhiều so với những gì chúng ta thấy. Vì bãng chữ cái sẽ khác nhau với các ngôn ngữ khác nhau. Một chữ cái có thể có mã code khác nhau tùy thuộc ngôn ngữ.

Nên, trình duyệt cần biết là ngôn ngữ nào được sử dụng để so sánh.

May mắn thay, các trình duyệt ngày nay (IE10- cần [Intl.JS](https://github.com/andyearnshaw/Intl.js/)) hỗ trợ chuẩn quốc tế [ECMA 402](http://www.ecma-international.org/ecma-402/1.0/ECMA-402.pdf).

Nó cung cấp một method đặc biệt để so sánh trong tất cả các ngôn ngữ.

Gọi là [str.localeCompare(str2)](mdn:js/String/localeCompare):

- Trả về `1` nếu `str` lớn hơn `str2` theo quy tắc ngôn ngữ đó.
- Trả về  `-1` nếu `str` nhở hơn `str2`.
- Trả về  `0` nếu bằng.

Ví dụ:

```js run
alert( 'Österreich'.localeCompare('Zealand') ); // -1
```

Method này có hai tham số được định nghĩa trong [the documentation](mdn:js/String/localeCompare), cho phép đặc tả ngôn ngữ (mặc định được lấy từ môi trường) và tạo ra các quy tắc, ví dụ `"a"` và `"á"` là như nhau...

## Internals, Unicode

```warn header="Kiến thức nâng cao"
Phần này sẽ hữu ích nếu bạn sử dụng emoji, ký hiệu toán học, chữ tượng hình hoặc các ký tự đặc biệt.

Có thể bõ qua nếu bạn không cần chúng.
```

### Surrogate pairs

Most symbols have a 2-byte code. Letters in most european languages, numbers, and even most hieroglyphs, have a 2-byte representation.

But 2 bytes only allow 65536 combinations and that's not enough for every possible symbol. So rare symbols are encoded with a pair of 2-byte characters called "a surrogate pair".

The length of such symbols is `2`:

```js run
alert( '𝒳'.length ); // 2, MATHEMATICAL SCRIPT CAPITAL X
alert( '😂'.length ); // 2, FACE WITH TEARS OF JOY
alert( '𩷶'.length ); // 2, a rare chinese hieroglyph
```

Note that surrogate pairs did not exist at the time when JavaScript was created, and thus are not correctly processed by the language!

We actually have a single symbol in each of the strings above, but the `length` shows a length of `2`.

`String.fromCodePoint` and `str.codePointAt` are few rare methods that deal with surrogate pairs right. They recently appeared in the language. Before them, there were only [String.fromCharCode](mdn:js/String/fromCharCode) and [str.charCodeAt](mdn:js/String/charCodeAt). These methods are actually the same as `fromCodePoint/codePointAt`, but don't work with surrogate pairs.

But, for instance, getting a symbol can be tricky, because surrogate pairs are treated as two characters:

```js run
alert( '𝒳'[0] ); // strange symbols...
alert( '𝒳'[1] ); // ...pieces of the surrogate pair
```

Note that pieces of the surrogate pair have no meaning without each other. So the alerts in the example above actually display garbage.

Technically, surrogate pairs are also detectable by their codes: if a character has the code in the interval of `0xd800..0xdbff`, then it is the first part of the surrogate pair. The next character (second part) must have the code in interval `0xdc00..0xdfff`. These intervals are reserved exclusively for surrogate pairs by the standard.

In the case above:

```js run
// charCodeAt is not surrogate-pair aware, so it gives codes for parts

alert( '𝒳'.charCodeAt(0).toString(16) ); // d835, between 0xd800 and 0xdbff
alert( '𝒳'.charCodeAt(1).toString(16) ); // dcb3, between 0xdc00 and 0xdfff
```

You will find more ways to deal with surrogate pairs later in the chapter <info:iterable>. There are probably special libraries for that too, but nothing famous enough to suggest here.

### Diacritical marks and normalization

In many languages there are symbols that are composed of the base character with a mark above/under it.

For instance, the letter `a` can be the base character for: `àáâäãåā`. Most common "composite" character have their own code in the UTF-16 table. But not all of them, because there are too many possible combinations.

To support arbitrary compositions, UTF-16 allows us to use several unicode characters. The base character and one or many "mark" characters that "decorate" it.

For instance, if we have `S` followed by the special "dot above" character (code `\u0307`), it is shown as Ṡ.

```js run
alert( 'S\u0307' ); // Ṡ
```

If we need an additional mark above the letter (or below it) -- no problem, just add the necessary mark character.

For instance, if we append a character "dot below" (code `\u0323`), then we'll have "S with dots above and below": `Ṩ`.

For example:

```js run
alert( 'S\u0307\u0323' ); // Ṩ
```

This provides great flexibility, but also an interesting problem: two characters may visually look the same, but be represented with different unicode compositions.

For instance:

```js run
alert( 'S\u0307\u0323' ); // Ṩ, S + dot above + dot below
alert( 'S\u0323\u0307' ); // Ṩ, S + dot below + dot above

alert( 'S\u0307\u0323' == 'S\u0323\u0307' ); // false
```

To solve this, there exists a "unicode normalization" algorithm that brings each string to the single "normal" form.

It is implemented by [str.normalize()](mdn:js/String/normalize).

```js run
alert( "S\u0307\u0323".normalize() == "S\u0323\u0307".normalize() ); // true
```

It's funny that in our situation `normalize()` actually brings together a sequence of 3 characters to one: `\u1e68` (S with two dots).

```js run
alert( "S\u0307\u0323".normalize().length ); // 1

alert( "S\u0307\u0323".normalize() == "\u1e68" ); // true
```

In reality, this is not always the case. The reason being that the symbol `Ṩ` is "common enough", so UTF-16 creators included it in the main table and gave it the code.

If you want to learn more about normalization rules and variants -- they are described in the appendix of the Unicode standard: [Unicode Normalization Forms](http://www.unicode.org/reports/tr15/), but for most practical purposes the information from this section is enough.


## Tổng kết

- Có 3 kiểu quotes. Backticks chấp nhận viết string nhiều hàng và nhúng biến, biểu thức.
- Strings trong JavaScript được mã hóa theo bãng mã UTF-16.
- Sử dụng các ký tự đặc biệt như `\n` và chèn chữ bởi mã Univode với `\u...`.
- Lấy ký tự sử dụng: `[]`.
- Lấy substring dùng: `slice` hoặc `substring`.
- Viết hoa/thường dùng: `toLowerCase/toUpperCase`.
- Tìm substring dùng: `indexOf`, or `includes/startsWith/endsWith` for simple checks.
- So sánh string dùng: `localeCompare`.

Một số methods hữu ích với strings:

- `str.trim()` -- bõ ("trims") các dấu space ở đầu và cuối string.
- `str.repeat(n)` -- repeats string `n` lần.
- ...Và nhiều hơn, xem tại [manual](mdn:js/String).

Strings cũng có methods để search/replace với biểu thức chính quy - regular expressions. Nhưng ta sẽ học trong chương khác.
