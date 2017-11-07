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
Vấn đề này cũng xảy ra trong các NNLT khác.

PHP, Java, C, Perl, Ruby cũng có cùng vấn đề vì chúng định dạng Number theo các tương tự. 
```

Chúng ta có thể làm việc được với vấn đề này ? chắc rồi, có một số cách:

1. Ta làm tròn số với method [toFixed(n)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed):

    ```js run
    let sum = 0.1 + 0.2;
    alert( sum.toFixed(2) ); // 0.30
    ```

    Chú ý rằng `toFixed` trả về một string. Nó đảm bảo rằng trả về đúng 2 chữ số phần thập phân cho ví dụ ở trên. Đó chính là những gì ta cần với trường hợp shop bán hàng online, `$0.30`. Với những trường hợp cần number, thêm dấu + đằng trước để convert sang number:

    ```js run
    let sum = 0.1 + 0.2;
    alert( +sum.toFixed(2) ); // 0.3
    ```

2. Đưa về dạng số nguyên để tính toán, sau đó lại trả kết quả về dạng thập phân:

    ```js run
    alert( (0.1 * 10 + 0.2 * 10) / 10 ); // 0.3
    ```

    Nó hoạt động vì `0.1 * 10 = 1` và `0.2 * 10 = 2` là hai số nguyên, sẽ không có sai số. 

````smart header="The funny thing"
Chạy dòng code dưới:

```js run
// Hello! I'm a self-increasing number! 
alert( 9999999999999999 ); // shows 10000000000000000
```

Đây cũng là một vấn đề tương tự: Sai số. 64 bits cho number, 52 bits để lưu giá trị, với các số quá lớn là không đủ. Cho nên các chữ số không quan trọng sẽ bị bõ qua

JavaScript sẽ không báo lỗi. Nó sẽ đưa về theo định dạng số đã mô tả. Nhưng, định dạng này không đủ lớn.
````

```smart header="Hai số `0`"
Có một cái funny nữa là có hai số không: `0` và `-0`.

Ta đã biết có một bits để lưu dấu của số, nên ta có các số đều có số âm và số dương, bao gồm cẩ số `0`. 

Trong nhiều trường hợp sự phân biệt này là không đáng nhắc đến vì phép toán sẽ cho ra cùng một kết quả.
```



## Kiểm tra: isFinite và isNaN

Có nhớ hai số đặc biệt không?

- `Infinity` (và `-Infinity`) là vô cực nó lớn hơn (nhỏ hơn) bất kỳ số nào.
- `NaN` đại diện cho lỗi.

Chúng là một `number`, nhưng không "bình thường", cho nên có hàm để kiểm tra:


- `isNaN(value)` convert tham số sang number và xem có phải là `NaN` hay không:

    ```js run
    alert( isNaN(NaN) ); // true
    alert( isNaN("str") ); // true
    ```

    Chúng ta có cần hàm này không? ta có thể dùng phép so sánh `=== NaN`? Không được nhé vì `NaN` là duy nhất và nó không bằng thằng nào hết, bao gồm chính nó:

    ```js run
    alert( NaN === NaN ); // false
    ```

- `isFinite(value)` converts tham số thành number, trả về `true` nếu là một số bình thường, không phải `NaN/Infinity/-Infinity`:

    ```js run
    alert( isFinite("15") ); // true
    alert( isFinite("str") ); // false, because a special value: NaN
    alert( isFinite(Infinity) ); // false, because a special value: Infinity
    ```

Thỉnh thoảng `isFinite` để dùng để xác nhận một string có phải là một số bình thường hay không:


```js run
let num = +prompt("Enter a number", '');

// will be true unless you enter Infinity, -Infinity or not a number
alert( isFinite(num) );
```

Chú ý string rỗng hoặc chỉ gồm các dấu space là `0` trong tất cả các hàm số học, bao gồm cả `isFinite`.  

```smart header="So sánh với `Object.is`"

Là một built-in method [Object.is](mdn:js/Object/is) so sánh giá trị với `===`, nhưng tin cậy hơn vì hai trường hợp biên:

1. Hoạt động với `NaN`: `Object.is(NaN, NaN) === true`, Rất tốt. 
2. Giá trị `0` và `-0` là khác nhau: `Object.is(0, -0) === false`, mặc dù hiếm khi dùng, nhưng về mặt kỹ thuật thì đúng là như thế.

Còn lại tất cả các trường hợp khác, `Object.is(a, b)` là tương đương với `a === b`. 

Cách so sánh nay được JavaScript sử dụng rất nhiều trong các tính năng của nó.  `Object.is` (internally called [SameValue](https://tc39.github.io/ecma262/#sec-samevalue)).
```


## parseInt và parseFloat

Conver qua number sử dụng `+` hoặc `Number()` là nghiêm ngặt. Nếu giá trị không chính xác hoàn toàn là số, nó sẽ fail:

```js run
alert( +"100px" ); // NaN
```

Ngoại lệ duy nhất là các dấu space ở đầu hoặc cuối chuỗi, vì nó sẽ bị bõ qua.

Trong thực tế ta có nhiều giá trị dạng `"100px"` hoặc `"12pt"` trong CSS. Hay tiền tệ của các nước sẽ có ký hiệu đằng sau như `"19€"` cần một cách để convert các giá trị dạng này ra số.

Đó là tác dụng của `parseInt` và `parseFloat` được dùng.

Chúng đọc các số đầu tiên trong một chuỗi. Hàm `parseInt` trả về integer, `parseFloat` trả về số dấu chấm động:

```js run
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12, only the integer part is returned
alert( parseFloat('12.3.4') ); // 12.3, the second point stops the reading
```

Các tình huống `parseInt/parseFloat` trả về `NaN`:

```js run
alert( parseInt('a123') ); // NaN, the first symbol stops the process
```

````smart header="Tham số thứ hai trong `parseInt(str, radix)`"
Hàm `parseInt()` có một tham số tùy chọn. thể hiện cơ số, nên `parseInt` có thể convert sang hex numbers, binary numbers ...:

```js run
alert( parseInt('0xff', 16) ); // 255
alert( parseInt('ff', 16) ); // 255, without 0x also works

alert( parseInt('2n9c', 36) ); // 123456
```
````

## Một số hàm toán học khác

JavaScript có object built-in [Math](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Math) bao gồm một thư viện các hàm toán học và hằng số.

Một vài ví dụ:

`Math.random()`
: Trả về một số ngẫu nhiên từ `0` tới `1` (không bao gồm 1)

    ```js run
    alert( Math.random() ); // 0.1234567894322
    alert( Math.random() ); // 0.5435252343232
    alert( Math.random() ); // ... (any random numbers)
    ```

`Math.max(a, b, c...)` / `Math.min(a, b, c...)`
: Trả về giá trị lớn nhất / nhỏ nhất trong các tham số.

    ```js run
    alert( Math.max(3, 5, -10, 0, 1) ); // 5
    alert( Math.min(1, 2) ); // 1
    ```

`Math.pow(n, power)`
: hàm mũ

    ```js run
    alert( Math.pow(2, 10) ); // 2 in power 10 = 1024
    ```

Có nhiều hàm và hằng số toán học trong `Math` object xem thêm tại (https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Math) object.

## Tổng kết

Để viết một số lớn:

- Dùng `"e"` ví dụ: `123e6` là `123000000` , `123e-3` là 0.123 .

Trong các hệ cơ số khác nhau:

- hex (`0x`), octal (`0o`) và binary (`0b`)
- `parseInt(str, base)` biểu diễn một str số nguyên theo cơ số base: `2 ≤ base ≤ 36`.
- `num.toString(base)` converts một số sang string là số theo cơ số `base`.

Conver các giá trị dạng `12pt` và `100px` sang số:

- Dùng `parseInt/parseFloat`

Cho phân số:

- Làm tròn sử dụng `Math.floor`, `Math.ceil`, `Math.trunc`, `Math.round` hoặc `num.toFixed(precision)`.
- Chú ý sai số.

Một số hàm toán học khác:

- Xem thêm Object [Math](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Math).


