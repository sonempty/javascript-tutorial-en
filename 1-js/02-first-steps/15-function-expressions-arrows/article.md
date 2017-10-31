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

Note that we could also have used a Function Expression to declare `sayHi`, in the first line:

```js
let sayHi = function() { ... };

let func = sayHi;
// ...
```

Everything would work the same. Even more obvious what's going on, right?


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

Sometimes that's handy to declare a local function only needed in that block alone. But that feature may also cause problems.

For instance, let's imagine that we need to declare a function `welcome()` depending on the `age` variable that we get in run time. And then we plan to use it some time later.

The code below doesn't work:

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

That's because a Function Declaration is only visible inside the code block in which it resides.

Here's another example:

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

What can we do to make `welcome` visible outside of `if`?

The correct approach would be to use a Function Expression and assign `welcome` to the variable that is declared outside of `if` and has the proper visibility.

Now it works as intended:

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

Or we could simplify it even further using a question mark operator `?`:

```js run
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  function() { alert("Hello!"); } :
  function() { alert("Greetings!"); };

*!*
welcome(); // ok now
*/!*
```


```smart header="When to choose Function Declaration versus Function Expression?"
As a rule of thumb, when we need to declare a function, the first to consider is Function Declaration syntax, the one we used before. It gives more freedom in how to organize our code, because we can call such functions before they are declared.

It's also a little bit easier to look up `function f(…) {…}` in the code than `let f = function(…) {…}`. Function Declarations are more "eye-catching".

...But if a Function Declaration does not suit us for some reason (we've seen an example above), then Function Expression should be used.
```


## Arrow functions [#arrow-functions]

There's one more very simple and concise syntax for creating functions, that's often better than Function Expressions. It's called "arrow functions", because it looks like this:


```js
let func = (arg1, arg2, ...argN) => expression
```

...This creates a function `func` that has arguments `arg1..argN`, evaluates the `expression` on the right side with their use and returns its result.

In other words, it's roughly the same as:

```js
let func = function(arg1, arg2, ...argN) {
  return expression;
}
```

...But much more concise.

Let's see an example:

```js run
let sum = (a, b) => a + b;

/* The arrow function is a shorter form of:

let sum = function(a, b) {
  return a + b;
};
*/

alert( sum(1, 2) ); // 3

```

If we have only one argument, then parentheses can be omitted, making that even shorter:

```js run
// same as
// let double = function(n) { return n * 2 }
*!*
let double = n => n * 2;
*/!*

alert( double(3) ); // 6
```

If there are no arguments, parentheses should be empty (but they should be present):

```js run
let sayHi = () => alert("Hello!");

sayHi();
```

Arrow functions can be used in the same way as Function Expressions.

For instance, here's the rewritten example with `welcome()`:

```js run
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
  () => alert('Hello') :
  () => alert("Greetings!");

welcome(); // ok now
```

Arrow functions may appear unfamiliar and not very readable at first, but that quickly changes as the eyes get used to the structure.

They are very convenient for simple one-line actions, when we're just too lazy to write many words.

```smart header="Multiline arrow functions"

The examples above took arguments from the left of `=>` and evaluated the right-side expression with them.

Sometimes we need something a little bit more complex, like multiple expressions or statements. It is also possible, but we should enclose them in figure brackets. Then use a normal `return` within them.

Like this:

```js run
let sum = (a, b) => {  // the figure bracket opens a multiline function
  let result = a + b;
*!*
  return result; // if we use figure brackets, use return to get results
*/!*
};

alert( sum(1, 2) ); // 3
```

```smart header="More to come"
Here we praised arrow functions for brevity. But that's not all! Arrow functions have other interesting features. We'll return to them later in the chapter <info:arrow-functions>.

For now, we can already use them for one-line actions and callbacks.
```

## Summary

- Functions are values. They can be assigned, copied or declared in any place of the code.
- If the function is declared as a separate statement in the main code flow, that's called a "Function Declaration".
- If the function is created as a part of an expression, it's called a "Function Expression".
- Function Declarations are processed before the code block is executed. They are visible everywhere in the block.
- Function Expressions are created when the execution flow reaches them.


In most cases when we need to declare a function, a Function Declaration is preferable, because it is visible prior to the declaration itself. That gives us more flexibility in code organization, and is usually more readable.

So we should use a Function Expression only when a Function Declaration is not fit for the task. We've seen a couple of examples of that in this chapter, and will see more in the future.

Arrow functions are handy for one-liners. They come in two flavors:

1. Without figure brackets: `(...args) => expression` -- the right side is an expression: the function evaluates it and returns the result.
2. With figure brackets: `(...args) => { body }` -- brackets allow us to write multiple statements inside the function, but we need an explicit `return` to return something.
