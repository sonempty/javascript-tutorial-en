# Biến số - Variables

Hầu hết thời gian ứng dụng JavaScript sẽ làm việc với các thông tin. Ví dụ:
1. Một shop online -- Thông tin có thể bao gồm hàng hóa, đơn hàng, kho bãi, giỏ hàng người dùng mua... 
2. Một ứng dụng Chat -- Thông tin bao gồm người sử dụng, tin nhắn ....

Biến sẽ được sử dụng để lưu trữ tất cả các thông tin trên.

[cut]

## Biến số

Một biến [variable](https://en.wikipedia.org/wiki/Variable_(computer_science)) là một cái tên và lưu trữ thông tin nào đó.

Để tạo ra biến trong JavaScript, cần dùng từ khóa `let`.

Câu lệnh phía dưới tạo ra (khai báo) một biến có tên là "message":

```js
let message;
```

Chúng ta gán cho nó một giá trị bằng phép gán `=`:

```js
let message;

*!*
message = 'Hello'; // gán một chuỗi cho biến
*/!*
```

Chuỗi này sẽ được lưu trong vùng bộ nhớ có địa chỉ liên kết với biến. Chúng ta sử dụng biến như sau:

```js run
let message;
message = 'Hello!';

*!*
alert(message); // shows the variable content
*/!*
```

Để ngắn gọn thì chúng ta có thể khai báo biến đồng thời gán giá trị cho nó trên một dòng:

```js run
let message = 'Hello!'; // define the variable and assign the value

alert(message); // Hello!
```

Có thể khai báo nhiều biến trên một dòng:

```js no-beautify
let user = 'John', age = 25, message = 'Hello';
```

Nhìn gọn hơn nhưng việc này không khuyến khích. Để dễ đọc hơn, nên khai báo mỗi biến trên một dòng.

Tốn nhiều dòng nhưng sẽ dễ đọc hơn:

```js
let user = 'John';
let age = 25;
let message = 'Hello';
```

Nhiều người hay khai báo biến như thế này:
```js no-beautify
let user = 'John',
  age = 25,
  message = 'Hello';
```

...thậm chí như này:

```js no-beautify
let user = 'John'
  , age = 25
  , message = 'Hello';
```

Về kỹ thuật thì các cách trên đều như nhau, nói chung là sở thích cá nhân và thẫm mỹ mỗi người.


````smart header="`var` thay vì `let`"
Trong JS cũ bạn thường thấy từ khóa: `var` thay vì `let`:

```js
*!*var*/!* message = 'Hello';
```

Từ khóa `var` gần giống như `let`. Cũng là khai báo biến nhưng nó đã xưa rồi.

Có một sự khác biệt tinh tế giữa `let` và `var`, nhưng hiện tại không phải là vấn đề gì, chúng ta sẽ quan tâm việc này chi tiết hơn ở chương <info:var>.
````

## Một vài ví dụ về biến trong cuộc sống

Chúng ta có thể dễ dàng nắm bắt khái niệm về một "biến số" nếu chúng ta tưởng tượng nó như là một "hộp" chứa đồ, với nhãn dán là duy nhất là tên biến, và cái thứ mà nó chứa đựng là giá trị của nó.

Ví dụ biến `message` là một cái hộp có nhãn là `"message"` và giá trị `"Hello!"` nằm trong nó:

![](variable.png)

Chúng ta có thể đặt bất cứ thứ gì vào hộp hay nói cách khác là gán bất kỳ giá trị nào cho biến:

```js run
let message;

message = 'Hello!';

message = 'World!'; // value changed

alert(message);
```

Khi thay đổi giá trị, giá trị cũ sẽ bị xóa khỏi biến:

![](variable-change.png)

Chúng ta có thể khai báo 2 biến và copy giá trị biến này cho biến kia.

```js run
let hello = 'Hello world!';

let message;

*!*
// copy 'Hello world' from hello into message
message = hello;
*/!*

// now two variables hold the same data
alert(hello); // Hello world!
alert(message); // Hello world!
```

```smart header="Ngôn ngữ hàm"
Có thể bạn sẽ thấy thú vị khi biết có  [ngôn ngữ lập trình hàm](https://en.wikipedia.org/wiki/Functional_programming) cấm việc thay đổi giá trị biến. Ví dụ, [Scala](http://www.scala-lang.org/) hoặc [Erlang](http://www.erlang.org/).

Trong các ngôn ngữ đó biến không bao giờ thay đổi giá trị. Chỉ có cách tạo ra biến mới để lưu trữ giá trị khác.

Hơn thế nữa, có những lĩnh vực như tính toán song song, trong đó sự hạn chế này lại là ưu điểm. Học một ngôn ngữ như vậy (ngay cả khi không có kế hoạch sử dụng nó sớm) được khuyến khích để mở rộng tầm nhìn của bạn.
```

## Đặt tên biến [#variable-naming]

Có hai nguyên tắc đặt tên biến trong JavaScript:

1. Tên biến chỉ gồm các chữ cái, chữ số và có thể có thêm 2 ký tự `$` và `_`.
2. Ký tự đầu tiên không thể là chữ số.

ví dụ về tên đúng:

```js
let userName;
let test123;
```

Khi tên biến gồm nhiều từ, [camelCase](https://en.wikipedia.org/wiki/CamelCase) là cách hay dùng. Từ tiếp theo sau từ đầu tiên sẽ viết hoa chữ cái đầu tiên, ví dụ: `myVeryLongName`.

Dấu đô la `'$'` và gạch dưới `'_'` là các ký tự tiêu chuẩn như các chữ cái, không có ý nghĩa đặc biệt gì khác.

Ví dụ tên đúng:

```js run untrusted
let $ = 1; // declared a variable with the name "$"
let _ = 2; // and now a variable with the name "_"

alert($ + _); // 3
```

Ví dụ tên sai:

```js no-beautify
let 1a; // cannot start with a digit

let my-name; // a hyphen '-' is not allowed in the name
```

```smart header="Viết hoa và viết thường"
Biến `apple` và `AppLE` -- là hai biến khác nhau.
```

````smart header="Sử dụng các ngôn ngữ không phải tiếng Anh để đặt tên không được khuyến khích"
ví dụ:

```js
let имя = '...';
let 我 = '...';
let Cửa_hàng = 'xxx';
```

Về mặt kỹ thuật, không có lỗi ở đây, tên như vậy được cho phép, nhưng có một truyền thống quốc tế để sử dụng tiếng Anh trong các tên biến. Ngay cả khi chúng ta viết một kịch bản nhỏ. Những người từ các nước khác có thể cần phải đọc nó.
````

````warn header="Các tên đã được sử dụng"
Có những từ không được lấy ra để đặt tên vì nó là từ khóa đã được JS sử dụng rồi.

ví dụ, từ `let`, `class`, `return`, `function` .

Đoạn code sau sẽ xảy ra lỗi cú pháp:

```js run no-beautify
let let = 5; // can't name a variable "let", error!
let return = 5; // also can't name it "return", error!
```
````

````warn header="Phép gán không sử dụng `use strict`"

Thông thường, chúng ta cần xác định một biến trước khi sử dụng nó. Nhưng trước đây, về mặt kỹ thuật, có thể tạo ra một biến bằng cách gán một giá trị, mà không cần khai báo `let`. Điều này vẫn hoạt động được nếu chúng ta không đặt `use strict`. Các hành vi sẽ được giữ tương thích với các kịch bản cũ.

```js run no-strict
// note: no "use strict" in this example

num = 5; // the variable "num" is created if didn't exist

alert(num); // 5
```

Code dưới sẽ gây lỗi vì có strict mode:

```js run untrusted
"use strict";

*!*
num = 5; // error: num is not defined
*/!*
```

````

## Hằng số

Để khai báo hằng (không thể thay đổi giá trị) dùng từ khóa `const` thay vì `let`:

```js
const myBirthday = '18.04.1982';
```

Có thể coi hằng là biến được khai báo bằng từ khóa `const` . Hằng thì không thể thay đổi giá trị, ví dụ code sau sẽ lỗi:

```js run
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // error, can't reassign the constant!
```

Khi bạn chắc chắn rằng một biến sẽ không bao giờ thay đổi giá trị thì nên dùng `const` để đảm bảo cho nó, và cũng là để cho người khác đọc code của bạn có thể thấy điều đó.


### Hằng với tên được viết hoa

Có một thực tế phổ biến để sử dụng hằng số làm tên cho các giá trị khó nhớ được biết đến trước khi thực hiện.

Các hằng số này được đặt tên bằng chữ hoa và dấu gạch dưới.

Ví dụ:

```js run
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";

// ...when we need to pick a color
let color = COLOR_ORANGE;
alert(color); // #FF7F00
```

Ưu điểm:

- `COLOR_ORANGE` dễ nhớ hơn là `"#FF7F00"`.
- `"#FF7F00"` dễ bị gõ sai hơn `COLOR_ORANGE`.
- Khi đọc code, `COLOR_ORANGE` có ngữ nghĩa hơn `#FF7F00`.

Khi nào nên dùng chữ hoa đặt tên cho biến, khi nào nên dùng chữ thường? Chúng ta cùng làm rõ.

Trường hợp là hằng số và chúng ta không biết giá trị khởi tạo ban đầu của nó. Mặc dù là giá trị này sẽ không thay đổi.

Ví dụ:
```js
const pageLoadTime = /* Thời gian để load một trang web */;
```

Giá trị của hằng `pageLoadTime` không được biết trước khi chúng ta tải trang web. Nhưng sau khi được gán, nó sẽ không thay đổi

Trong các trường còn lại, các giá trị khó nhớ thì sử dụng hằng với tên được viết hoa và dấu gạch dưới.  

## Đặt tên mọi thứ sao cho đúng

Nói về biến thì việc này vô cùng quan trọng.

Hãy đặt tên cho hợp lý, bõ thời gian suy nghĩ nếu cần.

Đặt tên biến là một kỹ năng quan trọng và phức tạp trong lập trình. Nhìn qua tên biến là biết được code được viết bởi gà hay pro :D.

Trong các dự án thật, hầu hết thời gian là dùng để chỉnh sửa và mở rộng code đã có sẵn. Và khi chúng ta nhìn lại code đã làm, sẽ dễ dang hơn để tìm thông tin thích hợp và đặt tên cho biến.

Hãy suy nghĩ để đặt tên thích hợp cho biến, việc này sẽ cực kỳ có ích cho bạn sau này.

Một vài cách ha như sau:

- Sử dụng các tên dễ đọc cho con người như `userName` hay `shoppingCart`.
- Tránh xa các chữ viết tắt hay tên ngắn `a`, `b`, `c`, trừ khi ban thực sự biết bạn đang làm gì.
- Đặt tên có ý nghĩa và súc tích nhất có thể. Ví dụ tên chả có ý nghĩa gì như `data` và `value`. Tên như vậy chả nói lên điều gì, trừ khi dùng trong một ngữ cảnh đặc biệt nào đó.
- Đồng ý với các quy định trong dự án hoặc phong cách bạn hay dùng. Nếu người dùng truy cập trang web của bạn được đặt tên là "user" thì nên dùng các biến liên quan như `currentUser` hoặc `newUser`, chứ không nên dùng `currentVisitor` hoặc `newManInTown`.

Nghe đơn giản không? Thực sự nó đơn giản mà. Nhưng trong thực tế để tạo ra các tên biến có tính mô tả sát sao và súc tích cũng không dễ đâu. Quất thôi

```smart header="Sử dụng lại hay tạo mới?"
Ghi chú cuối cùng. Một số lập trình viên rất lười, họ sử dụng lại các biến thay vì khai báo biến mới.
Kết quả là biến giống như cái thùng trong các ví dụ trước. Ai vứt cái gì vào cũng được, chả ai biết trong đó có gì.

Các bố này tiết kiệm được một chút công sức khai báo nhưng lại mất cả đống thời gian để debug lỗi sau này.

Các trình chỉnh sửa của JavaScript và trình duyệt hiện đại tối ưu hóa mã khá tốt, vì vậy nó sẽ không tạo ra các vấn đề hiệu năng. Sử dụng các biến khác nhau cho các giá trị khác nhau thậm chí có thể giúp engine tối ưu hóa tốt hơn.
```

## Tổng kết

Chúng ta có thể khai báo biến để lưu trữ thông tin bằng cách dùng `var` hoặc `let` hoặc `const`.

- `let` -- là cách khai báo hiện đại. Code nên được dùng ở chế độ strict mode để dùng `let` trong Chrome (V8).
- `var` -- là cách khai báo xưa cũ. Thường chúng ta sẽ không sử dụng, Nhưng chúng ta sẽ tìm hiểu sự khác biệt của `var` và `let` trong chương <info:var>.
- `const` -- giống như `let`, nhưng giá trị của biến sẽ không bao giờ thay đổi.

Biến nên được đặt tên sao cho dễ hiểu nhất, dễ nhận biết nhất biến này dùng để làm gì, lưu giữ thông tin gì.
