# Numbers

Tất cả số trong JavaScript được lưu trữ dưới dạng 64-bit [IEEE-754](http://en.wikipedia.org/wiki/IEEE_754-1985).

Chúng ta hãy tóm tắt lại và mở rộng những gì chúng ta biết về chúng.

## Nhiều cách để viết một number

Giả sử với số 1 tỷ, thường ta viết:

```js
let billion = 1000000000;
```

Trong thực tế thì viết như thế hay bị nhầm, và chúng ta cũng rất lười khi viết dài như vậy.

Trong JavaScript, ta có thể viết ngắn hơn bằng cách sử dụng chữ `"e"`:

```js run
let billion = 1e9;  // 1 billion, literally: 1 and 9 zeroes

alert( 7.3e9 );  // 7.3 billions (7,300,000,000)
```

`"e"` ở đây chính là `nhân với 10 mũ e`.

```js
1e3 = 1 * 1000
1.23e6 = 1.23 * 1000000 
```


`e` có thể là một số âm, ví dụ khi biểu diễn một mili giây: 

```js
let ms = 0.000001;
```

Sử dụng `e`:

```js
let ms = 1e-6; // six zeroes to the left from 1 
```

Nói cách khác, khi `e` âm có nghĩa là chia cho `10 mũ |e|`:

```js
// -3 divides by 1 with 3 zeroes
1e-3 = 1 / 1000 (=0.001)

// -6 divides by 1 with 6 zeroes
1.23e-6 = 1.23 / 1000000 (=0.00000123)
```

### Hex, binary và octal numbers
 
Số [Hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) (thập lục phân) thường biểu diễn màu sắc, mã hóa ký tự... So naturally, cách viết một số Hexa là bắt đầu bằng: `0x` và sau đó là số.

Ví dụ:

```js run
alert( 0xff ); // 255
alert( 0xFF ); // 255 (the same, case doesn't matter)
```

Số Binary (nhị phân) và octal (bát phân) ít khi được sử dụng, chúng bắt đầu bằng tiền tố `0b` và `0o`:


```js run
let a = 0b11111111; // binary form of 255
let b = 0o377; // octal form of 255

alert( a == b ); // true, the same number 255 at both sides
```

Nếu cần viết dưới dạng cơ số khác, ta dùng `parseInt` (sẽ học tới trong bài này).

## toString(base)

Method `num.toString(base)` trả về một chuỗi là số `num` viết trong cơ số `base`.

Ví dụ:
```js run
let num = 255;

alert( num.toString(16) );  // ff
alert( num.toString(2) );   // 11111111
```

Cơ số `base` có thể có giá trị từ `2` đến `36`. Giá trị mặc định là `10`.

Các cơ số hay được sử dụng là:

- **base=16** cho màu sắc, mã hóa ký tự...được dùng các chữ số từ `0..9` và `A..F`.
- **base=2** được dùng với các phép toán nhị phân, chỉ dùng hai chữ số `0` và `1`.
- **base=36** là lớn nhất, được dùng các chữ số từ `0..9` và `A..Z`. Các chữ cái latin được dùng để biểu diễn một số. Thường dùng khi cần biễu diễn một chuỗi số dài một cách ngắn hơn:

    ```js run
    alert( 123456..toString(36) ); // 2n9c
    ```

```warn header="Hai dấu chấm để gọi method"
Chú ý dùng hai dấu chấm `123456..toString(36)` không phải là lỗi đánh máy. Khi gọi một method từ number, như `toString` trong ví dụ trên thì cần sử dụng hai dấu chấm `..`.

Nếu dùng một dấu chấm: `123456.toString(36)` sẽ lỗi, bởi vì cú pháp JavaScript dùng một dấu chấm với ý nghĩa đó là phần thập phân. Và thêm một dấu chấm nữa, thì JavaScript biết rằng là không có phần thập phân và ta đang gọi method.

Cũng có thể viết `(123456).toString(36)`.
```

## Làm tròn

Đã có một hàm built-in cho việc làm tròn số:

`Math.floor`
: Làm tròn dưới: `3.1` trở thành `3`, và `-1.1` trở thành `-2`.

`Math.ceil`
: Làm tròn trên: `3.1` trở thành `4`, và `-1.1` trở thành `-1`.

`Math.round`
: Làm tròn đến giá trị gần nhất: `3.1` trở thành `3`, `3.6` trở thành `4` và `-1.1` trở thành `-1`.

`Math.trunc` (ko hỗ trợ trên trình duyệt Internet Explorer)
: Bõ phần thập phân: `3.1` trở thành `3`, `-1.1` trở thành `-1`.

Bảng tóm tắt:

|   | `Math.floor` | `Math.ceil` | `Math.round` | `Math.trunc` |
|---|---------|--------|---------|---------|
|`3.1`|  `3`    |   `4`  |    `3`  |   `3`   |
|`3.6`|  `3`    |   `4`  |    `4`  |   `3`   |
|`-1.1`|  `-2`    |   `-1`  |    `-1`  |   `-1`   |
|`-1.6`|  `-2`    |   `-1`  |    `-2`  |   `-1`   |


Những hàm trên chỉ làm tròn thành số nguyên, nếu muốn làm tròn đến số thập phân thứ `n-th` ta phải làm sao?

Ví dụ làm tròn `1.2345` với 2 chữ số thập phân, trở thành `1.23`.

Có hai cách:

1. Nhân và chia.

    Ví dụ làm tròn hai chữ số, ta nhân với `100`, rồi lại chia cho `100`.
    ```js run
    let num = 1.23456;

    alert( Math.floor(num * 100) / 100 ); // 1.23456 -> 123.456 -> 123 -> 1.23
    ```

2. Method [toFixed(n)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) làm tròn số đến `n` chữ số thập phân, biểu diễn thành một string chưa số đó.
        
    ```js run
    let num = 12.34;
    alert( num.toFixed(1) ); // "12.3"
    ```

    Tất cả các phép làm tròn, như `Math.round`:

    ```js run
    let num = 12.36;
    alert( num.toFixed(1) ); // "12.4"
    ```

    Chú ý, kết quả của phép `toFixed` là một string. Nếu phần thập hơn có ít chữ số hơn cần thiết, các số `0` sẽ được điền vào:

    ```js run
    let num = 12.34;
    alert( num.toFixed(5) ); // "12.34000", added zeroes to make exactly 5 digits 
    ```

    Ta có thể convert thành số bởi `Number()` hoặc `+num.toFixed(5)`.

## Sự tính toán không chính xác.

Number được biểu diễn dưới dạng 64-bit [IEEE-754](http://en.wikipedia.org/wiki/IEEE_754-1985), nên có chính xác 64 bit để lưu trữ một number: 52 bits để lưu các chữ số, 11 bits để lưu trữ các số sau dấu chấm thập phân (chúng = "0" nếu là số nguyên), và 1 bit cho dấu (âm hoặc dương).

Nếu số quá lớn, nó sẽ tràn 64-bit bộ nhớ, có khả năng cho ra một số infinity:

```js run
alert( 1e500 ); // Infinity 
```

Có một việc xảy ra khá thường xuyên, là mất chính xác trong các phép tính.

Ví dụ:

```js run
alert( 0.1 + 0.2 == 0.3 ); // *!*false*/!*
```

Đúng vậy, `0.1` cộng `0.2` không phải là `0.3`. 

Thật kỳ là, vậy kết quả là gì nếu không phải là `0.3`?

```js run
alert( 0.1 + 0.2 ); // 0.30000000000000004
```

Có nhiều hậu quả cho sự sai lệch này. Hãy tưởng tượng bạn có trang web bán hàng, khách hàng mua `$0.10` và `$0.20` hàng. Tổng cộng sẽ là `$0.30000000000000004`. Thật ngạc nhiên đúng không

Nhưng tại sao nó lại xảy ra?

Một number được lưu trữ dưới dạng các bít, một chuỗi số 0 và 1. Nhưng các phân số như `0.1`, `0.2` trong có vẽ đơn giản trong cơ số thập phân. Nhưng lại vô hạn trong phân số hay biễu diễn nhị phân.

Nói cách khác, `0.1` là gì? nó là 1 chia cho 10 `1/10`. Trong hệ số thập phân, các số như vậy là rất dễ dàng biểu diễn. So sánh chúng với: `1/3`. Nó là một số thập phân vô hạn `0.33333(3)`. 

Cho nên, phép chia cho `10` luôn bảo đảm hoạt động đúng trong hệ thập phân, nhưng phép chia cho `3` thì không. Cùng một lý do, trong hệ nhị phân, phép chia cho `2` luôn hoạt động đúng, nhưng `1/10` là một số vô hạn.

Không có cách nào để lưu trữ chính xác giá trị `0.1` hoặc `0.2`, giống như việc không có cách nào lưu trữ chính xác giá trị `1/3` trong hệ thập phân.

Định dạng số IEEE-754 giải quyết vấn đề này bằng cách làm tròn số. Phép làm tròn thông thường không show ra những sai số nhỏ bé, nên kết quả show ra là `0.3`. Nhưng hãy cẩn thận, kết quả có một sai số rất nhỏ.

Chúng ta có thể xem ví dụ sau đây:
```js run
alert( 0.1.toFixed(20) ); // 0.10000000000000000555
```

Khi chúng ta cộng hai số, các sai số nhỏ bé này cũng được cộng vào.

Đó là tại sao `0.1 + 0.2` không có kết quả chính xác là `0.3`.

```smart header="Không phải chỉ có JavaScript"
The same issue exists in many other programming languages.

PHP, Java, C, Perl, Ruby give exactly the same result, because they are based on the same numeric format. 
```

Can we work around the problem? Sure, there're a number of ways:

1. We can round the result with the help of a method [toFixed(n)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed):

    ```js run
    let sum = 0.1 + 0.2;
    alert( sum.toFixed(2) ); // 0.30
    ```

    Please note that `toFixed` always returns a string. It ensures that it has 2 digits after the decimal point. That's actually convenient if we have an e-shopping and need to show `$0.30`. For other cases, we can use the unary plus to coerce it into a number:

    ```js run
    let sum = 0.1 + 0.2;
    alert( +sum.toFixed(2) ); // 0.3
    ```

2. We can temporarily turn numbers into integers for the maths and then revert it back. It works like this:

    ```js run
    alert( (0.1 * 10 + 0.2 * 10) / 10 ); // 0.3
    ```

    This works because when we do `0.1 * 10 = 1` and `0.2 * 10 = 2` then both numbers become integers, and there's no precision loss. 

3. If we were dealing with a shop, then the most radical solution would be to store all prices in cents and use no fractions at all. But what if we apply a discount of 30%? In practice, totally evading fractions is rarely feasible, so the solutions above help avoid this pitfall.

````smart header="The funny thing"
Try running this:

```js run
// Hello! I'm a self-increasing number! 
alert( 9999999999999999 ); // shows 10000000000000000
```

This suffers from the same issue: a loss of precision. There are 64 bits for the number, 52 of them can be used to store digits, but that's not enough. So the least significant digits disappear.

JavaScript doesn't trigger an error in such events. It does its best to fit the number into the desired format, but unfortunately, this format is not big enough.
````

```smart header="Two zeroes"
Another funny consequence of the internal representation of numbers is the existence of two zeroes: `0` and `-0`.

That's because a sign is represented by a single bit, so every number can be positive or negative, including a zero. 

In most cases the distinction is unnoticeable, because operators are suited to treat them as the same.
```



## Tests: isFinite and isNaN

Remember these two special numeric values?

- `Infinite` (and `-Infinite`) is a special numeric value that is greater (less) than anything.
- `NaN` represents an error.

They belong to the type `number`, but are not "normal" numbers, so there are special functions to check for them:


- `isNaN(value)` converts its argument to a number and then tests it for being `NaN`:

    ```js run
    alert( isNaN(NaN) ); // true
    alert( isNaN("str") ); // true
    ```

    But do we need this function? Can't we just use the comparison `=== NaN`? Sorry, but the answer is no. The value `NaN` is unique in that it does not equal anything, including itself:

    ```js run
    alert( NaN === NaN ); // false
    ```

- `isFinite(value)` converts its argument to a number and returns `true` if it's a regular number, not `NaN/Infinity/-Infinity`:

    ```js run
    alert( isFinite("15") ); // true
    alert( isFinite("str") ); // false, because a special value: NaN
    alert( isFinite(Infinity) ); // false, because a special value: Infinity
    ```

Sometimes `isFinite` is used to validate whether a string value is a regular number:


```js run
let num = +prompt("Enter a number", '');

// will be true unless you enter Infinity, -Infinity or not a number
alert( isFinite(num) );
```

Please note that an empty or a space-only string is treated as `0` in all numeric functions including `isFinite`.  

```smart header="Compare with `Object.is`"

There is a special built-in method [Object.is](mdn:js/Object/is) that compares values like `===`, but is more reliable for two edge cases:

1. It works with `NaN`: `Object.is(NaN, NaN) === true`, that's a good thing. 
2. Values `0` and `-0` are different: `Object.is(0, -0) === false`, it rarely matters, but these values technically are different.

In all other cases, `Object.is(a, b)` is the same as `a === b`. 

This way of comparison is often used in JavaScript specification. When an internal algorithm needs to compare two values for being exactly the same, it uses `Object.is` (internally called [SameValue](https://tc39.github.io/ecma262/#sec-samevalue)).
```


## parseInt and parseFloat

Numeric conversion using a plus `+` or `Number()` is strict. If a value is not exactly a number, it fails:

```js run
alert( +"100px" ); // NaN
```

The sole exception is spaces at the beginning or at the end of the string, as they are ignored.

But in real life we often have values in units, like `"100px"` or `"12pt"` in CSS. Also in many countries the currency symbol goes after the amount, so we have `"19€"` and would like to extract a numeric value out of that.

That's what `parseInt` and `parseFloat` are for.

They "read" a number from a string until they can. In case of an error, the gathered number is returned. The function `parseInt` returns an integer, whilst `parseFloat` will return a floating-point number:

```js run
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12, only the integer part is returned
alert( parseFloat('12.3.4') ); // 12.3, the second point stops the reading
```

There are situations when `parseInt/parseFloat` will return `NaN`. It happens when no digits could be read:

```js run
alert( parseInt('a123') ); // NaN, the first symbol stops the process
```

````smart header="The second argument of `parseInt(str, radix)`"
The `parseInt()` function has an optional second parameter. It specifies the base of the numeral system, so `parseInt` can also parse strings of hex numbers, binary numbers and so on:

```js run
alert( parseInt('0xff', 16) ); // 255
alert( parseInt('ff', 16) ); // 255, without 0x also works

alert( parseInt('2n9c', 36) ); // 123456
```
````

## Other math functions

JavaScript has a built-in [Math](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Math) object which contains a small library of mathematical functions and constants.

A few examples:

`Math.random()`
: Returns a random number from 0 to 1 (not including 1)

    ```js run
    alert( Math.random() ); // 0.1234567894322
    alert( Math.random() ); // 0.5435252343232
    alert( Math.random() ); // ... (any random numbers)
    ```

`Math.max(a, b, c...)` / `Math.min(a, b, c...)`
: Returns the greatest/smallest from the arbitrary number of arguments.

    ```js run
    alert( Math.max(3, 5, -10, 0, 1) ); // 5
    alert( Math.min(1, 2) ); // 1
    ```

`Math.pow(n, power)`
: Returns `n` raised the given power

    ```js run
    alert( Math.pow(2, 10) ); // 2 in power 10 = 1024
    ```

There are more functions and constants in `Math` object, including trigonometry, which you can find in the [docs for the Math](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Math) object.

## Summary

To write big numbers:

- Append `"e"` with the zeroes count to the number. Like: `123e6` is `123` with 6 zeroes.
- A negative number after `"e"` causes the number to be divided by 1 with given zeroes. That's for one-millionth or such.

For different numeral systems:

- Can write numbers directly in hex (`0x`), octal (`0o`) and binary (`0b`) systems
- `parseInt(str, base)` parses an integer from any numeral system with base: `2 ≤ base ≤ 36`.
- `num.toString(base)` converts a number to a string in the numeral system with the given `base`.

For converting values like `12pt` and `100px` to a number:

- Use `parseInt/parseFloat` for the "soft" conversion, which reads a number from a string and then returns the value they could read before the error. 

For fractions:

- Round using `Math.floor`, `Math.ceil`, `Math.trunc`, `Math.round` or `num.toFixed(precision)`.
- Make sure to remember there's a loss of precision when working with fractions.

More mathematical functions:

- See the [Math](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Math) object when you need them. The library is very small, but can cover basic needs.


