# Các kiểu dữ liệu - Data types

Biến trong JavaScript có thể chứa dữ liệu nào đó và đồng thời có thể thay đổi giá trị:

```js
// no error
let message = "hello";
message = 123456;
```

Ngôn ngữ lập trình như vậy được gọi là động "dynamically typed", có nghĩa là có nhiều kiểu dữ liệu trong ngôn ngữ, nhưng các biến không bị ràng buộc bởi chúng.

có 7 kiểu dữ liệu cơ bản trong JavaScript. Chúng ta học sơ qua về từng loại dữ liệu sau đó sẽ tìm hiểu kỹ mỗi loại ở các chương tiếp theo.

[cut]

## Kiểu số - number

```js
let n = 123;
n = 12.345;
```

Kiểu *number* bao gồm số nguyên và số thực.

Trên kiểu số có các phép toán như: nhân `*`, chia `/`, cộng `+`, trừ `-` và một số phép toán khác nữa.

Bên cạnh các số cụ thể còn có các số đặc biệt như: dương vô cùng - `Infinity`, âm vô cùng - `-Infinity` và số không xác định `NaN`.

- `Infinity` dương vô cùng [Infinity](https://en.wikipedia.org/wiki/Infinity) ∞. là một số dương lớn vô cùng.

    Chúng ta nhận được nó khi chia một số dương cho số 0:

    ```js run
    alert( 1 / 0 ); // Infinity
    ```

    Hoặc có thể dùng trực tiếp như này:

    ```js run
    alert( Infinity ); // Infinity
    ```
- `NaN` là số không xác định, hay là kết quả của một phép toán vô nghĩa trong toán học, hoặc phép toán lỗi:

    ```js run
    alert( "not a number" / 2 ); // NaN, such division is erroneous
    ```

    Một phép toán bất kỳ có chứa `NaN` sẽ trả về kết quả là `NaN`:

    ```js run
    alert( "not a number" / 2 + 5 ); // NaN
    ```

    Cho nên chỉ cần thấy `NaN` trong bất kỳ biểu thức nào thì kết quả trả về sẽ là Nan.

```smart header="Các phép toán là an toàn"
Tính toán toán học trong JavaScript là an toàn. Hơi khác với trong toán học, vì nó tồn tai các phép toán như: chia cho 0, phép toán trên các giá trị không phải là số.

Script sẽ không bao giờ lỗi và stop chương trình bởi các phép toán, vì cùng lắm là trả về `NaN`.
```

Các số đặc biệt cũng là kiểu số đấy nhé. Tất nhiên là trong JS chứ không phải trong thế giới thực.

Chúng ta sẽ học kỹ hơn ở chương <info:number>.

## Chuỗi - string

Chuỗi trong JavaScript phải đặt trong dấu nháy đơn hoặc nháy kép.

```js
let str = "Hello";
let str2 = 'Single quotes are ok too';
let phrase = `can embed ${str}`;
```

Trong JavaScript, Có ba kiểu dấu nháy.

1. Nháy kép: `"Hello"`.
2. Nháy đơn: `'Hello'`.
3. và dấu nháy Backticks: <code>&#96;Hello&#96;</code>.

Nháy đơn và nháy kép là dấu nháy đơn giản, có ý nghĩa như nhau trong JavaScript.

Backticks dấu nháy "chức năng mở rộng". Dạng như template vậy, nó cho phép nhúng biến vào trong biểu thức `${…}`, Ví dụ:

```js run
let name = "John";

// embed a variable
alert( `Hello, *!*${name}*/!*!` ); // Hello, John!

// embed an expression
alert( `the result is *!*${1 + 2}*/!*` ); // the result is 3
```

Biểu thức trong `${…}` sẽ được đánh giá và tính toán, sau đó kết quả sẽ là một phần của chuỗi. chúng ta có thể để vào bất cứ thứ gì: một biến `name` hoặc một biểu thức đơn giản như `1 + 2` hay nhiều thứ phức tạp hơn.

Chỉ backticks mới được nhé, nháy đơn hay nháy kép không chấp nhận kiểu nhúng này
```js run
alert( "the result is ${1 + 2}" ); // the result is ${1 + 2} (double quotes do nothing)
```

Chúng ta sẽ học kỹ hơn trong chương <info:string>.

```smart header="Không có kiểu ký tự - *character*."
Trong các ngôn ngữ khác như C sẽ có kiểu ký tự đơn `char`.

Trong JavaScript, Không có kiểu char như vậy mà chỉ có một kiểu `string` cho ký tự đơn hay một chuỗi dài nhiều ký tự.
```

## Kiểu logic - boolean

Kiểu boolean chỉ có hai giá trị là đúng: `true` và sai: `false`.

Thường được dùng để lưu các giá trị yes/no.

Ví dụ:

```js
let nameFieldChecked = true; // yes, name field is checked
let ageFieldChecked = false; // no, age field is not checked
```

Giá trị kiểu Boolean cũng là kết quả của một phép so sánh:

```js run
let isGreater = 4 > 1;

alert( isGreater ); // true (the comparison result is "yes")
```

Sẽ học kỹ hơn về Boolean trong chương <info:logical-operators>.

## Giá trị "null"

Giá trị đặc biệt `null` Không thuộc bất cứ một kiểu dữ liệu nào ở trên.

`null` thuộc kiểu null, hay nói cách khác kiểu null chỉ gồm một giá trị là `null` .
Có nhiều bạn nói null là kiểu Object, các bạn cứ đọc tiếp sẽ có phần giải thích nhé:

```js
let age = null;
```

Trong JavaScript `null` không phải là "tham chiếu đến một đối tượng không tồn tại" hoặc "con trỏ mà không trỏ đến bất cứ cái gì" như các ngôn ngữ khác.

Nó chỉ là một giá trị thể hiện sự không có gì: "nothing", trống rỗng: "empty" hoặc không biết giá trị: "value unknown".

Code bên trên người ta khai báo biến `age` là chưa biết hoặc không chứa giá trị vì một lý do nào đó.

## Giá trị chưa được định ngĩa - "undefined"

`undefined` thuộc kiểu undefined, kiểu như `null`.

`undefined` để thể hiện cho "chưa được gán giá trị".

Nếu một biến được khai báo nhưng chưa được gán giá trị nào, thì giá trị của biến đó chính là `undefined`:

```js run
let x;

alert(x); // shows "undefined"
```

Về mặt kỹ thuật, có thể gán giá trị `undefined` cho bất cứ biến nào:

```js run
let x = 123;

x = undefined;

alert(x); // "undefined"
```

...Nhưng không khuyến khích làm như thế. Bình thường chúng ta dùng `null` để thể hiện một biến có giá trị là trống "empty" hoặc chưa biết, và `undefined` chỉ để kiểm tra là biến đã được gán giá trị hay chưa.

## Kiểu đối tượng - Object và kiểu Symbol (méo biết dịch ra là gì)

Kiểu `object` là kiểu đặc biệt.

Tất cả các kiểu dữ liệu khác được gọi là kiểu nguyên thủy "primitive", bởi vì giá trị của chúng chưa những thành phần đơn lẽ. Ngược lại Objects chứa một bộ giá trị phức tạp. Chúng ta sẽ học thêm ở chương <info:object> sau khi có đủ hiểu biết về các kiểu primitives.

Kiểu `symbol` để tạo ra các giá trị duy nhất - unique identifiers cho Objects. Chúng ta chỉ nhắc đến tên nó ở đây cho biết vậy thôi, để sau khi học xong về kiểu Objects sẽ quay lại học về nó sẽ dễ hiểu hơn.

## Phép toán typeof [#type-typeof]

Phép toán `typeof` trả về kiểu dữ liệu của tham số. Người ta hay dùng để kiểm tra hay so kiểu dữ liệu.

Có thể dùng theo hai cách:

1. Như một phép toán: `typeof x`.
2. Như hàm: `typeof(x)`.

Hai cách này cho kết quả như nhau.

Gọi `typeof x` trả về một *String* là tên kiểu dữ liệu:

```js
typeof undefined // "undefined"

typeof 0 // "number"

typeof true // "boolean"

typeof "foo" // "string"

typeof Symbol("id") // "symbol"

*!*
typeof Math // "object"  (1)
*/!*

*!*
typeof null // "object"  (2)
*/!*

*!*
typeof alert // "function"  (3)
*/!*
```

The last three lines may need additional explanations:

1. `Math` là một đối tượng được JS xây dựng sẵn, chứa các phép tính toán học. Chúng ta sẽ tìm hiểu ở chương <info:number>. Lấy ra làm ví dụ ở đây cho kiểu Object thôi.
2. Kết quả của `typeof null` là `"object"`. Điều này là sai. Đó là lỗi chính thức được thừa nhận trong `typeof`, để giữ cho sự tương thích của nó. Tất nhiên, `null` không phải là một Object. Nó là một giá trị đặc biệt và thuộc kiểu null. Một lần nữa, khẳng định là tồn tại lỗi này trong JS nhé.
3. Kết quả của `typeof alert` là `"function"`, bởi vì `alert` là một hàm. Chúng ta sẽ học về hàm trong chương tiếp theo, và chúng ta sẽ thấy không có kiểu hàm đặc biệt nào trong JS. fuction là kiểu Object. Nhưng `typeof` xác định nó hơi khác. Thực sự thì là không đúng, nhưng như thế thì sẽ tiện lợi hơn khi dùng.


## Tóm tắt

Có 7 kiểu dữ liệu cơ bản trong JavaScript.

- `number` cho số nguyên và số thực.
- `string` cho chuỗi và ký tự.
- `boolean` cho đúng/sai `true`/`false`.
- `null` cho giá trị chưa rõ -- có kiểu là chính nó, giống thằng `null`.
- `undefined` cho chưa gán giá trị -- cũng là kiểu `undefined`.
- `object` cho các cấu trúc dữ liệu phức tạp.
- `symbol` cho định danh duy nhất.

Phép toán `typeof` cho chúng ta biết kiểu dữ liệu của tham số.

- có thể dùng theo hai cách: `typeof x` or `typeof(x)`.
- Trả về một string với hai dấu nháy kép, ví dụ: `"string"`.
- typeof `null` trả về `"object"` -- Đây là lỗi trong JS, thực sự nó không phải là Object.

Chương tiếp chúng ta sẽ tập trung vào các kiểu primitive sau khi đã quen thuộc sẽ nghiên cứu tiếp về objects.
