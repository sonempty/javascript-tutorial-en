# Function expressions và arrows function

[cut]

Cú pháp khai báo hàm bài trước chúng ta học được gọi là *Function Declaration*:

```js
function sayHi() {
  alert( "Hello" );
}
```

Có một cú pháp khác để tạo ra hàm, đó là *Function Expression* - biểu thức hàm.

Như thế này:

```js
let sayHi = function() {
  alert( "Hello" );
};
```

Ở trên, hàm được tạo ra và gán cho biến, giống như phép gán với các giá trị khác. Không có vấn đề gì với hàm được định nghĩa, nó là một giá trị được lưu trữ trong biến `sayHi`.


Nghĩa là: "Tạo ra một hàm và gán nó vào một biến có tên là `sayHi`".

Thậm chí có thể in ra code của hàm `alert`:

```js run
function sayHi() {
  alert( "Hello" );
}

*!*
alert( sayHi ); // shows the function code
*/!*
```

Chú ý dòng cuối cùng không thực thi hàm, bởi vì không có cặp ngoặc sau `sayHi`. Có nhiều ngôn ngữ lập trình khi gọi tên hàm thì sẽ thực thi hàm luôn, nhưng JavaScript thì không như thế.

Trong JavaScript, hàm là một giá trị, có thể sử dụng như các giá trị khác. Ví dụ bên trên show ra một chuỗi, cũng chính là code của hàm.

Đó là một giá trị đặc biệt, về mặt ý nghĩa ta có thể gọi hàm `sayHi()`.

Nhưng nó vẫn là một giá trị. Nên ta có thể dùng như kiểu các giá trị khác.

Ta có thể copy hàm cho biến khác:

```js run no-beautify
function sayHi() {   // (1) create
  alert( "Hello" );
}

let func = sayHi;    // (2) copy

func(); // Hello     // (3) run the copy (it works)!
sayHi(); // Hello    //     this still works too (why wouldn't it)
```

Here's what happens above in detail:

1. Function Declaration `(1)` tạo ra hàm và gán vào biến `sayHi`.
2. Dòng `(2)` copy giá trị của `sayhi` vào biến `func`.

    Chú ý một lần nữa: Không có cặp dấu ngoặc tròn sau `sayHi`. Nếu có `func = sayHi()` sẽ thực hiện gán giá trị là  *kết quả của một lần gọi của hàm* `sayHi()` vào biến `func`.
3. Giờ có thể gọi hàm bằng cả hai cách `sayHi()` và `func()`.

Chú ý rằng chúng ta cũng đã sử dụng Function Expression để khai báo `sayHi`, ở dòng đầu tiên:

```js
let sayHi = function() { ... };

let func = sayHi;
// ...
```

Mọi thứ đều hoạt động bình thường, thậm chí rõ ràng hơn đúng không?


````smart header="Tại sao có dấu chấm phẩy khi kết thúc Function Expression?"
Tại sao có dấu chấm phẩy `;` khi kết thúc Function Expression? còn Function Declaration thì không:

```js
function sayHi() {
  // ...
}

let sayHi = function() {
  // ...
}*!*;*/!*
```

Câu trả lời đơn giản là:
- Không cần thiết có dấu `;` ở cuối các khối code và các cấu trúc ngữ pháp như `if { ... }`, `for {  }`, `function f { }` ...
- Một Function Expression được sử dụng trong câu lệnh: `let sayHi = ...;`, như một giá trị. Nó không phải là khối lệnh. Dấu chấm phẩy `;` được khuyên dùng khi kết thúc câu lệnh, không quan tâm nó là giá trị gì. Vì vậy, ở đây dấu chẩm phẩy không liên quan gì đến Function Expression, nó chỉ kết thúc cho một câu lệnh.
````

## Hàm Callback

Sử dụng hàm như một đối số để truyền vào trong hàm khác, sử dụng function expressions.

Chúng ta viết hàm `ask(question, yes, no)` với ba tham số:

`question`
: câu hỏi

`yes`
: hàm sẽ thực thi nếu câu trả lời là "Yes"

`no`
: hàm sẽ thực thi nếu câu trả lời là "No"

Hàm sẽ hỏi một `question` và, tùy thuộc câu trả lời mà ta sẽ gọi hàm `yes()` hay `no()`:

```js run
*!*
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}
*/!*

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// usage: functions showOk, showCancel are passed as arguments to ask
ask("Do you agree?", showOk, showCancel);
```

Ở ví dụ trên ta viết gọn hàm bằng cách sử dụng function-comment đã học ở bài trước. Cách viết như vậy là rất phổ biến hiện nay. Sự khác biệt duy nhất giữa ví dụ ở trên và code trong thực tế là trong thực tế các hàm sẽ phức tạp hơn chứ không đơn giản chỉ `confirm`, `alert`, câu hỏi cũng sẽ hiển thị một cách đẹp đẽ hơn. Nhưng đó là câu chuyện khác.

**Các tham số của hàm `ask` được gọi là *callback functions* hay đơn giản là *callbacks*.**

Ý tưởng ở đây là các hàm đó sẽ được gọi sau nếu như cần thiết. Trong ví dụ trên, `showOk` là hàm callback cho câu trả lời "yes", và `showCancel` cho câu trả lời "no".

Chúng ta sử dụng Function Expressions để viết các hàm trên gọn hơn:

```js run no-beautify
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

*!*
ask(
  "Do you agree?",
  function() { alert("You agreed."); },
  function() { alert("You canceled the execution."); }
);
*/!*
```


Ở trên, hàm được khai báo bên trong `ask(...)` call. Chúng nó không có tên, và được gọi là *vô danh - anonymous*. Những hàm như thế này không thể sử dụng bên ngoài `ask` (vì nó không được gán cho biến nào), nhưng đó là những gì bạn muốn.

Code như trên nhìn rất tự nhiên, đó là linh hồn của JavaScript.


```smart header="Một hàm là một giá trị đại diện cho một hành động \"action\""
Các giá trị thông thường như chuỗi hoặc số đại diện cho *dữ liệu*.

Một hàm có thể được coi là một *hành động*.
```


## Function Expression và Function Declaration

Cùng so sánh Function Declarations và Expressions.

Đầu tiên là cú pháp: how to see what is what in the code.

- *Function Declaration:* một hàm, được khai báo trong một câu lệnh, trong main code.

    ```js
    // Function Declaration
    function sum(a, b) {
      return a + b;
    }
    ```
- *Function Expression:* một hàm, được tạo ra trong biểu thức hoặc trong cấu trúc cú pháp khác.

    Ở đây, hàm được tạo ra trong về phải của biểu thức của một phép gán:
    ```js
    // Function Expression
    let sum = function(a, b) {
      return a + b;
    };
    ```

Sự khác nhau tiếp theo là *khi nào* hàm sẽ được JavaScript engine tạo ra.

**Một Function Expression được tạo ra khi chương trình chạy đến code này, và từ đó về sau ta có thể sử dụng được hàm.**

Khi chương trình chạy đến vế phải của biểu thức `let sum = function…` -- Đi thôi, hàm được tạo ra và có thể sử dụng rồi (gán, gọi ,...).

Function Declarations thì khác.

**Một Function Declaration có thể được sử dụng trong toàn bộ script/code block.**

Nói cách khác, Khi JavaScript *chuẩn bị* chạy script hoặc một code block, đầu tiên nó sẽ tìm tất cả Function Declarations sau đó tạo ra các hàm này.

Sau khi tất cả Function Declaration đã thực hiện xong, script/code block mới thực thi.

Kết quả là hàm có thể gọi trước khi Function Declaration.

Ví dụ:

```js run refresh untrusted
*!*
sayHi("John"); // Hello, John
*/!*

function sayHi(name) {
  alert( `Hello, ${name}` );
}
```

Function Declaration `sayHi` được tạo ra khi JavaScript chuẩn bị chạy chương trình.

...Nếu là một Function Expression, sẽ không chạy được:

```js run refresh untrusted
*!*
sayHi("John"); // error!
*/!*

let sayHi = function(name) {  // (*) no magic any more
  alert( `Hello, ${name}` );
};
```

Function Expressions chỉ được tạo ra khi chương trình thực thi đến nó.

**Khi một Function Declaration nằm trong một code block, nó chỉ có thể được sử dụng bên trong block đó.**

Đôi khi khai báo hàm trong một block code có vẽ tiện hơn. Nhưng có thể sẽ xảy ra lỗi.

Ví dụ bên dưới với hàm `welcome()` code sau sẽ lỗi:

```js run
let age = prompt("What is your age?", 18);

// conditionally declare a function
if (age < 18) {

  function welcome() {
    alert("Hello!");
  }

} else {

  function welcome() {
    alert("Greetings!");
  }

}

// ...use it later
*!*
welcome(); // Error: welcome is not defined
*/!*
```

Bởi vì Function Declaration chỉ dùng được trong code block.

Một ví dụ khác:

```js run
let age = 16; // take 16 as an example

if (age < 18) {
*!*
  welcome();               // \   (runs)
*/!*
                           //  |
  function welcome() {     //  |  
    alert("Hello!");       //  |  Function Declaration is available
  }                        //  |  everywhere in the block where it's declared
                           //  |
*!*
  welcome();               // /   (runs)
*/!*

} else {

  function welcome() {     //  for age = 16, this "welcome" is never created
    alert("Greetings!");
  }
}

// Here we're out of figure brackets,
// so we can not see Function Declarations made inside of them.

*!*
welcome(); // Error: welcome is not defined
*/!*
```

Chúng ta sẽ làm gì để `welcome` có thể dùng được bên ngoài `if`?

Sử dụng Function Expression và gán `welcome` vào một biến được khai báo bên ngoài `if`.

Bây giờ nó hoạt động như dự định:

```js run
let age = prompt("What is your age?", 18);

let welcome;

if (age < 18) {

  welcome = function() {
    alert("Hello!");
  };

} else {

  welcome = function() {
    alert("Greetings!");
  };

}

*!*
welcome(); // ok now
*/!*
```

Hoặc đơn giản hơn là sử dụng phép `?`:

```js run
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  function() { alert("Hello!"); } :
  function() { alert("Greetings!"); };

*!*
welcome(); // ok now
*/!*
```


```smart header="Khi nào dùng Function Declaration và Function Expression?"
Như một quy luật, khi cần khai báo hàm, đầu tiên ta xem xét cú pháp Function Declaration, liệu hàm có dùng trước khi khai báo hay không. Nó sẽ làm cho bạn code thoải mái hơn, không lo đến việc dùng hàm trước khi khai báo.

Cũng dễ nhìn và dễ tìm hơn với `function f(…) {…}` so với `let f = function(…) {…}`.

...Nhưng Function Declaration không thích hợp vì một số lý do (ta đã xem xét ở trên), Do đó nên dùng Function Expression.
```


## Arrow functions [#arrow-functions]

Có một cú pháp ngắn gọn hơn và tốt hơn Function Expressions để khai báo hàm . Nó được gọi là "arrow functions", Vì có dấu mũi tên như này:


```js
let func = (arg1, arg2, ...argN) => expression
```

...Cú pháp này tạo ra một hàm `func` với các tham số `arg1..argN`, phần `expression` bên phải chính là giá trị trả về của hàm, cũng là phần thân hàm.

Nói cách khác, cách khai báo ở trên tương đương với:

```js
let func = function(arg1, arg2, ...argN) {
  return expression;
}
```

...nhưng ngắn gọn hơn.

Ví dụ:

```js run
let sum = (a, b) => a + b;

/* The arrow function is a shorter form of:

let sum = function(a, b) {
  return a + b;
};
*/

alert( sum(1, 2) ); // 3

```

Nếu chỉ có một tham số, thì có thể bõ luôn cặp dấu ngoặc như bên dưới cho ngắn gọn hơn:

```js run
// same as
// let double = function(n) { return n * 2 }
*!*
let double = n => n * 2;
*/!*

alert( double(3) ); // 6
```

Nếu không có tham số nào, vẫn phải có cặp dấu ngoặc:

```js run
let sayHi = () => alert("Hello!");

sayHi();
```

Arrow functions được dùng giống như cách dùng Function Expressions.

Ví dụ với hàm `welcome()` ở các ví dụ trước có thể viết lại như sau:

```js run
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  () => alert('Hello') :
  () => alert("Greetings!");

welcome(); // ok now
```

Arrow functions có thể không thân thiện lắm khi bạn mới tiếp xúc, nhưng từ từ sẽ quen.

Chúng rất tiện lợi với các hàm đơn giản, khi bạn lười code.

```smart header="Multiline arrow functions"

Đôi khi hàm phức tạp hơn với nhiều biểu thức và câu lệnh. Nếu dùng arrow function thì cần dùng cặp ngoặc nhọn, và sử dụng `return` bên trong.

ví dụ:

```js run
let sum = (a, b) => {  // the figure bracket opens a multiline function
  let result = a + b;
*!*
  return result; // if we use figure brackets, use return to get results
*/!*
};

alert( sum(1, 2) ); // 3
```

```smart header="Nhiều hơn nữa"
Bài này chỉ giới thiệu ngắn gọn về Arrow function, thực ra còn nhiều cách thức và ý nghĩa khi sử dụng nữa. Chúng ta sẽ tìm hiểu kỹ hơn ở bài <info:arrow-functions>.

Bây giờ chúng ta sử dụng nó cho one-line actions và callbacks.
```

## Tóm tắt

- Hàm cũng là giá trị. Có thể được gán, copy và khai báo ở bất kỳ đâu.
- Nếu hàm được khai báo trong câu lệnh phân biệt ở main code, thì gọi là "Function Declaration".
- Nếu hàm được tạo ra như là một phần của biểu thức  thì gọi là "Function Expression".
- Function Declarations được xử lý trước khi code đươc thực thi. Cho nên có thể dùng hàm trước hoặc sau code khai báo hàm.
- Function Expressions được tạo ra khi thực thi đến đoạn code chứa nó.


Function Declaration thì dễ dùng, dễ đọc hơn, không phải lo đến chuyện trước sau.

Nhưng nên sử dụng Function Expression vì nó thích hợp hơn cho các nhiệm vụ cần được thực thi.

Arrow functions cho các one-line-action. Nó đơn giản, và có hai dạng như bên dưới:

1. Không có cặp ngoặc nhọn: `(...args) => expression` -- bên phải là một biểu thức: hàm sẽ đánh giá và trả về giá trị của biểu thức này.
2. Có cặp ngoặc nhọn: `(...args) => { body }` -- để dùng nhiều biểu thức, câu lệnh hơn trong thân hàm, cần khai báo rõ ràng `return`.
