# Hàm - Functions

Chúng ta thường thực hiện nhiều hành động tương tự nhau lặp đi lặp lại trong chương trình của mình.

Ví dụ hiển thị những câu chào khác nhau mỗi lần người dùng đăng nhập.

Hàm là những khối gạch chính xây dựng nên chương trình. Chúng thực hiện các hành động tương tự nhau mà không lặp lại.

[cut]

Ở các bài học trước chúng ta đã thấy các hàm built-in (có sẵn trong trình duyệt) như `alert(message)`, `prompt(message, default)` và `confirm(question)`. Tuy nhiên chúng ta hoàn toàn có thể tạo ra các hàm của riêng mình.

## Khai báo hàm - Function Declaration

Để tạo ra hàm và sử dụng chúng, trước tiên cần *khai báo hàm*.

Như thế này:

```js
function showMessage() {
  alert( 'Hello everyone!' );
}
```

Từ khóa `function` đầu tiên, tiếp theo là *tên của hàm*, tiếp là các *tham số* trong cặp dấu ngoặc (hoặc không có tham số như ví dụ trên) và cuối cùng là các dòng code trong hàm, được gọi là "thân hàm".

![](function_basics.png)

Chúng ta gọi hàm lên để sử dụng bằng tên của chúng: `showMessage()`.

Ví dụ:

```js run
function showMessage() {
  alert( 'Hello everyone!' );
}

*!*
showMessage();
showMessage();
*/!*
```

Gọi `showMessage()` sẽ thực thi code trong thân hàm. Ở ví dụ trên bạn sẽ thấy xuất hiện hai thông báo.

Như ví dụ trên, ta thấy mục đích chính của hàm là: tránh lặp đi lặp lại việc viết code.

Nếu muốn thay đổi message hoặc cách mà nó hiển thị, bạn chỉ cần sửa code một lần . Phần output của hàm được gọi sau đó sẽ thay đổi theo.

## Biến cục bộ - Local variables

Biến khai báo trong hàm chỉ được nhìn thấy trong hàm đó.

Ví dụ:

```js run
function showMessage() {
*!*
  let message = "Hello, I'm JavaScript!"; // local variable
*/!*

  alert( message );
}

showMessage(); // Hello, I'm JavaScript!

alert( message ); // <-- Error! The variable is local to the function
```

## Biến ngoại vi - Outer variables

Hàm có thể truy xuất đến các biến bên ngoài hàm:

```js run no-beautify
let *!*userName*/!* = 'John';

function showMessage() {
  let message = 'Hello, ' + *!*userName*/!*;
  alert(message);
}

showMessage(); // Hello, John
```

Cũng có thể gán giá trị khác cho biến ngoại vi.

Ví dụ:

```js run
let *!*userName*/!* = 'John';

function showMessage() {
  *!*userName*/!* = "Bob"; // (1) changed the outer variable

  let message = 'Hello, ' + *!*userName*/!*;
  alert(message);
}

alert( userName ); // *!*John*/!* before the function call

showMessage();

alert( userName ); // *!*Bob*/!*, the value was modified by the function
```

Biến ngoại vi chỉ được truy xuất nếu không có biến cục bộ nào cùng tên. Vì vậy đừng quên `let`.

Nếu trong hàm có một biến cục bộ trùng tên với một biến ngoại vi bên ngoài thì chúng là hai biến khác nhau nhé. Ví dụ bên dưới với biến `userName`:

```js run
let userName = 'John';

function showMessage() {
*!*
  let userName = "Bob"; // declare a local variable
*/!*

  let message = 'Hello, ' + userName; // *!*Bob*/!*
  alert(message);
}

// the function will create and use it's own userName
showMessage();

alert( userName ); // *!*John*/!*, unchanged, the function did not access the outer variable
```

```smart header="Global variables"
Tất cả các biến mà không được khai báo trong bất cứ hàm nào, như biến `userName` ở ví dụ trên, được gọi là biến *global*.

Biến global có thể được truy xuất bởi bất cứ hàm nào (trừ khi có biến local cùng tên).

Bình thường, trong hàm ta khai báo các biến có liên quan đến công việc của hàm đó, và biến global chỉ liên quan đến chương trình chung, và cần được truy xuất ở bất kỳ đâu. Các chương trình hiện nay thường chỉ có một vài, hoặc không có biến global nào. Hầu hết các biến sẽ được viết lại thành local.
```

## Tham số - Parameters

Chúng ta có thể truyền bất cứ giá trị nào vào hàm thông qua tham số, và các giá trị cụ thể đó, khi được truyền vào hàm thì ta gọi là *đối số - arguments* .

Trong ví dụ bên dưới, chúng ta có hai tham số là: `from` và `text`. các đối số là 'Ann', 'Hello!', và "What's up?"

```js run
function showMessage(*!*from, text*/!*) { // arguments: from, text
  alert(from + ': ' + text);
}

*!*
showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)
*/!*
```

Khi ta gọi hàm ở dòng code `(*)` và `(**)`, Giá trị của đối số sẽ được gán vào biến cục bộ `from` và `text`. Sau đó hàm sẽ sử dụng chúng.

Thêm một ví dụ nữa bên dưới: chúng ta có biến global `from` và được truyền vào hàm. Chú ý rằng: hàm sẽ gán lại giá trị cho biến cục bộ `from` trong thân hàm, nhưng giá trị của biến global `from` bên ngoài vẫn sẽ không thay đổi. Bởi vì đơn giản là hai biến này khác nhau, và khi truyền biến global `from` vào hàm thì hàm sẽ chỉ copy giá trị của nó.


```js run
function showMessage(from, text) {

*!*
  from = '*' + from + '*'; // make "from" look nicer
*/!*

  alert( from + ': ' + text );
}

let from = "Ann";

showMessage(from, "Hello"); // *Ann*: Hello

// the value of "from" is the same, the function modified a local copy
alert( from ); // Ann
```

## Giá trị mặc định - Default values

Ví dụ hàm có 3 tham số, mà khi bạn gọi hàm bạn chỉ truyền vào 2 đối số, vậy tham số còn lại sẽ nhận giá trị `undefined`.

Xem ví dụ bên dưới với hàm `showMessage(from, text)`, có thể gọi hàm chỉ với một tham số:

```js
showMessage("Ann");
```

Sẽ không có lỗi xảy ra, kết quả sẽ là `"Ann: undefined"`. không truyền đối số cho `text`, cho nên `text === undefined`.

Để `text` có một giá trị mặc định, khi khai báo hàm ta truyền luôn giá trị mặc định vào bởi phép gán `=`:

```js run
function showMessage(from, *!*text = "no text given"*/!*) {
  alert( from + ": " + text );
}

showMessage("Ann"); // Ann: no text given
```

OK, bây giờ nếu không truyền đối số cho `text` thì nó sẽ nhận giá trị là `"no text given"`

Ở đây `"no text given"` là một chuỗi đơn giản, nhưng ta có thể đặt bất cứ giá trị phức tạo nào:

```js run
function showMessage(from, text = anotherFunction()) {
  // anotherFunction() only executed if no text given
  // its result becomes the value of text
}
```


````smart header="Default parameters old-style"
Các phiên bản JS cũ không hỗ trợ default parameters. Nên bạn có thể dùng cách khác như bên dưới.

```js
function showMessage(from, text) {
*!*
  if (text === undefined) {
    text = 'no text given';
  }
*/!*

  alert( from + ": " + text );
}
```

...Or the `||` operator:

```js
function showMessage(from, text) {
  // if text is falsy then text gets the "default" value
  text = text || 'no text given';
  ...
}
```


````


## Giá trị trả về

Hàm sẽ trả về một giá trị nào đó.

Ví dụ với hàm cộng hai số:

```js run no-beautify
function sum(a, b) {
  *!*return*/!* a + b;
}

let result = sum(1, 2);
alert( result ); // 3
```

Chỉ thị `return` có thể nằm ở bất kỳ đâu trong hàm. Khi hàm gặp chỉ thị này, nó sẽ dừng thực thi, và trả về giá trị của biểu thức nằm nay sau `return`. Ở ví dụ trên là giá trị của biểu thức `a + b`

Có thể có nhiều `return` trong hàm:

```js run
function checkAge(age) {
  if (age > 18) {
*!*
    return true;
*/!*
  } else {
*!*
    return confirm('Got a permission from the parents?');
*/!*
  }
}

let age = prompt('How old are you?', 18);

if ( checkAge(age) ) {
  alert( 'Access granted' );
} else {
  alert( 'Access denied' );
}
```

Có thể dùng `return` một mình, không có biểu thức nào ở sau. Đó là sự ngầm định kết thúc hàm.

Ví dụ:

```js
function showMovie(age) {
  if ( !checkAge(age) ) {
*!*
    return;
*/!*
  }

  alert( "Showing you the movie" ); // (*)
  // ...
}
```

Ở ví dụ trên `checkAge(age)` trả về `false`, nên `showMovie` không thực thi lệnh `alert`.

````smart header="Hàm mà không có, hoặc không có gì theo sau `return` sẽ trả về `undefined`"

VD:

```js run
function doNothing() { /* empty */ }

alert( doNothing() === undefined ); // true
```

VD:

```js run
function doNothing() {
  return;
}

alert( doNothing() === undefined ); // true
```
````

````warn header="Không xuống dòng giữa `return` và biểu thức đằng sau"
Nếu biểu thức sau `return` quá dài, Tìm cách tách ra hợp lý, chứ đừng như bên dưới:

```js
return
 (some + long + expression + or + whatever * f(a) + f(b))
```
Sẽ không chạy, vì JavaScript sẽ tự thêm dấu chấm phẩy sau `return`. Và code trên sẽ thành ra như bên dưới:

```js
return*!*;*/!*
 (some + long + expression + or + whatever * f(a) + f(b))
```

````

## Đặt tên cho hàm [#function-naming]

Hàm là một hành động. Cho nên sử dụng động từ để đặt tên cho nó. Tên cần ngắn gọn, chính xác và mô tả được những gì mà hàm thực hiện. Để cho người đọc dễ hiểu, dễ nhớ và thể hiện đẳng cấp pro của LTV ( :D, sống ảo tí ).

Đó là cách đặt tên phổ biến của các LTV trên tg hiện nay.

Ví dụ hàm bắt đầu bằng `"show"` sẽ show lên cái gì đó.

Hàm bắt đầu bằng (hay còn gọi là tiền tố - prefix):

- `"get…"` -- return a value,
- `"calc…"` -- calculate something,
- `"create…"` -- create something,
- `"check…"` -- check something and return a boolean, etc.

Ví dụ:

```js no-beautify
showMessage(..)     // shows a message
getAge(..)          // returns the age (gets it somehow)
calcSum(..)         // calculates a sum and returns the result
createForm(..)      // creates a form (and usually returns it)
checkPermission(..) // checks a permission, returns true/false
```

Với những tiền tố như trên, chỉ cần nhìn lướt qua tên hàm, đại khái bạn biết hàm đó sẽ làm gì và trả về giá trị gì.

```smart header="MỘT hàm -- MỘT hành động"
Một hàm chỉ làm một hành động theo tên của nó, đừng ôm đồm thêm.

Hai hành động khác nhau thì nên khai báo hai hàm khác nhau, cho dù hành động này có thể gọi hành động kia (trường hợp này ta khai báo hàm thứ ba để thực hiện hai hành động).

Một vài ví dụ:

- `getAge` -- would be bad if it shows an `alert` with the age (should only get).
- `createForm` -- would be bad if it modifies the document, adding a form to it (should only create it and return).
- `checkPermission` -- would be bad if displays the `access granted/denied` message (should only perform the check and return the result).

Ý nghĩa của các prefixes là rất quan trọng, các bạn nên nắm chắc nó, biết được prefixes nào được dùng và không được dùng trong trường hợp cụ thể. 
Các hàm có chung prefixes thường sẽ có chung một ý nghĩa nào đó. Ví dụ `getUserName` lấy tên người dùng, thường sẽ trả về một string chính là tên người dùng. Nó chung prefix với `getUserAge` lấy tuổi, trả về number. Chúng có điểm chung là đều lấy thông tin người dùng cả.
```

```smart header="Hàm có tên cực kỳ ngắn"
Hàm được sử dụng  *quá thường xuyên* thường có tên cực kỳ ngắn.

Ví dụ, framework [jQuery](http://jquery.com) có hàm `$`, Thư viện [LoDash](http://lodash.com/) có hàm `_`.

Đây là những ngoại lệ. Nói chung tên hàm nên ngắn gọn, nhưng mang tính mô tả.
```

## Functions == Comments

Hàm nên ngắn gọn và làm chính xác một hành động. Nhưng có đôi khi cái hành động này nó quá lớn, viết vào một hàm thì hơi khoai, bảo trì khó, mà đọc hiểu càng khó. Vậy ta nên chia nhỏ nó ra, có thể việc này không dễ dàng gì, nhưng nên làm.

Ví dụ so sánh hàm `showPrimes(n)` khai báo theo hai cách bên dưới. Hàm này show ra các số nguyên tố [prime numbers](https://en.wikipedia.org/wiki/Prime_number) nhỏ hơn `n`.

Cách khai báo đầu tiên:

```js
function showPrimes(n) {
  nextPrime: for (let i = 2; i < n; i++) {

    for (let j = 2; j < i; j++) {
      if (i % j == 0) continue nextPrime;
    }

    alert( i ); // a prime
  }
}
```

Cách thứ hai, sử dụng thêm một hàm `isPrime(n)` để kiểm tra một số có phải là số nguyên tố hay không trước, rồi bỏ vào hàm `showPrimes` sau:

```js
function showPrimes(n) {

  for (let i = 2; i < n; i++) {
    *!*if (!isPrime(i)) continue;*/!*

    alert(i);  // a prime
  }
}

function isPrime(n) {
  for (let i = 2; i < n; i++) {
    if ( n % i == 0) return false;
  }
  return true;
}
```

Rõ ràng cách thứ hai đọc vào dễ hiểu hơn đúng không?  Mặc dù có thể hàm (`isPrime`) cũng sẽ chẳng được dùng lại ở đâu cả. Code có thể dài hơn nhưng đọc vào dễ hiểu, dễ test, dễ bảo trì.

## Tóm tắt

Hàm được khai báo theo cú pháp:

```js
function name(parameters, delimited, by, comma) {
  /* code */
}
```

- Giá trị đối số được truyền vào tham số trong hàm bằng cách copy vào biến local.
- Hàm có thể truy xuất đến biến ngoại vi. Nhưng chỉ sử dụng bên trong hàm đó. Code bên ngoài hàm không thể truy xuất đến các biến local trong hàm.
- Hàm trả về giá trị cụ thể nào đó. Nếu không thì nó sẽ trả về `undefined`.

Trong hàm nên chỉ sử dụng biến local, không nên sử dụng biến ngoại vi.

Chú ý đừng quên từ khóa khai báo biến trong hàm, chứ không là nó tạo/edit biến global.

Đặt tên cho hàm:

- Nên ngắn gọn, chính xác và có tính mô tả.
- Hàm là một hành động, cho nên dùng động từ để đặt tên.
- Sử dụng prefixes như `create…`, `show…`, `get…`, `check…`. và `.......` theo phong cách chung của tg.

Hàm là một bài học rất quan trọng. Bài này chỉ cơ bản thôi, nhưng bạn cần nắm chắc, chúng ta sẽ đi sâu hơn trong các bài sau.
