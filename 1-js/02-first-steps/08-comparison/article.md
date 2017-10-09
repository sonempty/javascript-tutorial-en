# Các phép so sánh

Một số phép so sánh chúng ta học được từ toán học như:

- Lớn hơn, nhỏ hơn: <code>a &gt; b</code>, <code>a &lt; b</code>.
- Lớn hơn hoặc bằng, nhỏ hơn hoặc bằng: <code>a &gt;= b</code>, <code>a &lt;= b</code>.
- So sánh bằng `a == b` (chú ý hai dấu `'='` nhé. Một dấu `a = b` là phép gán).
- Không bằng (hay khác). Trong toán học là dấu <code>&ne;</code>, Trong JavaScript là dấu bằng với sự phủ định: <code>a != b</code>.

[cut]

## Boolean là kết quả của phép so sánh

Tất cả các phép toán đều trả về giá trị nào đó, và với phép so sánh nó trả về giá trị đúng/sai.

- `true` -- có ý nghĩa là "yes", "đúng" hay "sự thật".
- `false` -- có ý nghĩa là "no", "sai" hay "sự dối trá".

Ví dụ:

```js run
alert( 2 > 1 );  // true (correct)
alert( 2 == 1 ); // false (wrong)
alert( 2 != 1 ); // true (correct)
```

Giá trị trả về của một phép so sánh có thể gán luôn cho biến nào đó:

```js run
let result = 5 > 4; // assign the result of the comparison
alert( result ); // true
```

## So sánh chuỗi

Chuỗi lớn hơn nếu nó nằm sau trong bảng chữ cái (hoặc bảng mã).

Sự so sánh sẽ tiến hành theo từng chữ cái, từ trái sang phải.

VD:

```js run
alert( 'Z' > 'A' ); // true
alert( 'Glow' > 'Glee' ); // true
alert( 'Bee' > 'Be' ); // true
```

Quy tắc so sánh chuỗi đơn giản như sau:

1. So sánh ký tự đầu tiên của hai chuỗi.
2. Thằng nào lớn hơn thì chuỗi đó lớn hơn.
3. Nếu bằng nhau thì so sánh ký tự tiếp theo.
4. Cứ tiếp tục như thế.
5. Nếu một chuỗi đã hết ký tự mà vẫn bằng nhau. Thì chuỗi nào dài hơn chuỗi đó sẽ lớn hơn

Ở ví dụ trên `'Z' > 'A'` trả về kết quả ngay bước đầu tiên.

Chuỗi `"Glow"` và `"Glee"` được so sánh từng ký tự:

1. `G` bằng `G`.
2. `l` bằng `l`.
3. `o` lớn hơn `e`. Xong, vậy chuỗi `"Glow"` lớn hơn.

```smart header="Không phải bảng chữ cái mà là bãng mã Unicode"
Thực ra so sánh chuỗi không phải theo bãng chữ cái thông thường.

Ví dụ chữ viết hoa `"A"` sẽ không bằng với `"a"`. Chữ `"a"` sẽ lớn hơn. Bởi vì nó có *mã* lớn hơn theo bãng mã (Unicode). Chúng ta sẽ tìm hiểu kỹ hơn ở chương <info:string>.
```

## So sánh hai kiểu dữ liệu khác nhau

Khi so sánh khác kiểu, nó sẽ convert thành number.

ví dụ:

```js run
alert( '2' > 1 ); // true, string '2' becomes a number 2
alert( '01' == 1 ); // true, string '01' becomes a number 1
```

Với boolean, `true` trở thành `1` và `false` là `0`, đã học rồi:

```js run
alert( true == 1 ); // true
alert( false == 0 ); // true
```

````smart header="Một kết quả thú vị"
Có thể cùng một lúc:

- Hai giá trị bằng nhau.
- Một là `true` kiểu boolean và `false` cũng là kiểu boolean.

Ví dụ:

```js run
let a = 0;
alert( Boolean(a) ); // false

let b = "0";
alert( Boolean(b) ); // true

alert(a == b); // true!
```
Bạn nào thấy có gì đó sai sai thì đọc lại bài 6 nhé, đã học rồi.

````

## Strict equality - bằng (một cách nghiêm ngặt)

Ta thấy phép so sánh `"=="` có vấn đề sau: nó không phân biệt được sự khác nhau giữ `0` và `false`:

```js run
alert( 0 == false ); // true
```

Điều tương tự xảy ra với một chuỗi rỗng:

```js run
alert( '' == false ); // true
```

Đó là bởi vì các toán hạng trong phép  `==` đã được ép kiểu sang number rồi. Một chuỗi rỗng hay `false`, đều chuyển đổi thành `0`.

Để tìm sự khác biệt giữa `0` và `false` chúng ta làm sao đây?

**Phép `===` so sánh sự bằng nhau mà không chuyển đổi kiểu.**

Nói cách khác nếu `a` và `b` khác kiểu dữ liệu thì `a === b` luôn luôn trả về `false` .

VD:

```js run
alert( 0 === false ); // false, because the types are different
```

Có một sự tương đương đối với cặp phép toán `!==` và `!=` nhé.

## So sánh với null và undefined

Xem trường hợp sau.

Khi so sánh `null` và `undefined` với các kiểu dữ liệu khác.


Với phép `===`
: Hai giá trị là khác nhau bởi vì chúng thuộc kiểu dữ liệu là chính nó.

    ```js run
    alert( null === undefined ); // false
    ```

Với phép `==`
: Có một quy định đặc biệt cho phép `null` và `undefined` bằng nhau, nhưng không bằng với bất kỳ giá trị nào khác.

    ```js run
    alert( null == undefined ); // true
    ```

Với so sánh toán học và các phép so sánh khác `< > <= >=`
: Giá trị `null/undefined` sẽ được chuyển đổi sang number: `null` thành `0`, `undefined` thành `NaN`.

Nào chúng ta xem một số sự đặc biệt dưới đây, phần này khá là quan trọng đấy

### Kết quả kỳ lạ: null và 0

So sánh `null` và `0`:

```js run
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) *!*true*/!*
```

Thấy vl chưa các bạn.

Nguyên nhân là phép `==` và các phép so sánh `> < >= <=` làm việc khác nhau. Các phép so sánh convert `null` thành number, và kq là `0`. đó là vì sao (3) `null >= 0` là đúng và (1) `null > 0` là sai.

Còn lại phép `==` cho `undefined` và `null` thì theo nguyên tắc như đã nói ở trên rồi, hai thằng này chỉ bằng nhau và không bằng bất cứ thằng nào khác. Do đó nên `null == 0` là sai.

### Không thể so sánh được undefined

Giá trị `undefined` không nên đem ra so sánh ở bất kỳ trường hợp nào:

```js run
alert( undefined > 0 ); // false (1)
alert( undefined < 0 ); // false (2)
alert( undefined == 0 ); // false (3)
```

Luôn luôn là false!

Chúng ta giải thích các kết quả:

- `(1)` và `(2)` return `false` vì `undefined` được convert thành `NaN`. Và `NaN` là một số đặc biệt. Trong mọi phép so sánh với `NaN` đều sẽ trả về `false` .
- `(3)` returns `false`, vì `undefined` chỉ bằng `null` ngoài ra chẳng bằng thằng nào khác.

### Những vấn đề cần tránh

Tại sao chúng ta học những ví dụ này? Chúng ta có nên nhớ những đặc thù này không? Vâng, không thực sự. Trên thực tế, những điều khó hiểu này sẽ dần dần trở nên quen thuộc theo thời gian, nhưng có một cách để không bị dính vào những đặc thù này.

Không nên so sánh với `undefined/null` trừ trường hợp dùng phép `===` với sự cẩn thận nhất có thể.

Không sử dụng các phép so sánh `>= > < <=` với giá trị có thể là `null/undefined`, trừ khi bạn biết mình đang làm gì. Nếu các biến có thể trả về `null/undefined` thì tốt nhất hãy tách chúng ra.

## Tổng kết

- Các phép so sánh trả về giá trị logic.
- String được so sánh từ trái sang phải, theo thứ tự trong bảng mã Unicode.
- Khi so sánh hai giá trị khác kiểu dữ liệu, thì chúng sẽ được convert thành number trước (Chú ý ngoại lệ của phép `==`).
- Values `null` and `undefined` equal `==` each other and do not equal any other value.
- Cẩn thận khi so sánh `>` hoặc `<` với các giá trị có thể là `null/undefined`. Nên tách `null/undefined` ra.
