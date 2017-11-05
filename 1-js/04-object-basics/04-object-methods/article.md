# Object methods, "this"

Objects thường được tạo ra và đại diện cho một thực thể nào đó trong thế giới thực, như users, orders và vv...:

```js
let user = {
  name: "John",
  age: 30
};
```

Trong thế giới thực, một user có thể có các hành động: chọn mặt hàng nào đó trong shopping cart, login, logout ...

Các hành động đó được đại diện bởi  một hàm trong properties. Và hàm đó ta gọi là **Method**

[cut]

## Ví dụ về methods

Ta tạo một hành động nói xin chào cho `user`:

```js run
let user = {
  name: "John",
  age: 30
};

*!*
user.sayHi = function() {
  alert("Hello!");
};
*/!*

user.sayHi(); // Hello!
```

Sử dụng Function Expression và gán cho property `user.sayHi` của user.

Hàm mà là một property của object thi được gọi là *method*.

Vậy ở đây ta có method `sayHi` của object `user`.

Tất nhiên ta cũng có thể khai báo hàm trước rồi gán vào property sau:

```js run
let user = {
  // ...
};

*!*
// first, declare
function sayHi() {
  alert("Hello!");
};

// then add as a method
user.sayHi = sayHi;
*/!*

user.sayHi(); // Hello!
```

```smart header="Lập trình hướng đối tượng"
Khi ta dùng một đối tượng để đại diện cho một thực thể thật, đó gọi là lập trình hướng đối tượng [object-oriented programming](https://en.wikipedia.org/wiki/Object-oriented_programming), viết tắt là "OOP".

OOP là một khái niệm lớn, nó là một môn học căn bản cho các lập trình viên. Thường thi nếu học lập trình bài bản , bạn nên học qua về OOP. Nó dạy cho bạn cách đặt tên, thuộc tính, cấu trúc ....một thực thể như thế nào khi đưa vào lập trình.
```
### Method shorthand

Tương tự như Property shorthand như đã học, có thể khai báo một method ngắn gọn như bên dưới:

```js
// these objects do the same

let user = {
  sayHi: function() {
    alert("Hello");
  }
};

// method shorthand looks better, right?
let user = {
*!*
  sayHi() { // same as "sayHi: function()"
*/!*
    alert("Hello");
  }
};
```

Ta có thể bõ qua từ khóa `"function"` chỉ viết `sayHi()`.

Thực ra thì hai cách trên không hoàn toàn tương tự. Có một sự khác nhau tinh tế liên quan đến tính kế thừa của object (sẽ học sau), Nhưng hiện tại ta chưa cần quan tâm. Viết kiểu shorthand được khuyến khích sử dụng hơn nhé.

## "this" trong methods

Khi tạo ra một method, điều hay xảy ra là ta cần lấy thông tin từ một property khác trong cùng object.

Ví dụ `user.sayHi()` cần lấy tên của `user` để in ra câu chào.

**Để truy cập object, method sử dụng từ khóa `this`.**

Giá trị của `this` là object "trước dấu chấm", được sử dụng để gọi method.

Ví dụ:

```js run
let user = {
  name: "John",
  age: 30,

  sayHi() {
*!*
    alert(this.name);
*/!*
  }

};

user.sayHi(); // John
```

Khi thực thi `user.sayHi()`, Giá trị của `this` chính là `user`.

Về mặt kỹ thuật ta có thể dùng chính object đó thay cho `this`:

```js
let user = {
  name: "John",
  age: 30,

  sayHi() {
*!*
    alert(user.name); // "user" instead of "this"
*/!*
  }

};
```

...Nhưng như thế sẽ không đáng tin cậy, khi ta copy `user` cho một biến khác `admin = user` và ghi đè `user`, khi đó sẽ truy cập sai object.

Ví dụ:

```js run
let user = {
  name: "John",
  age: 30,

  sayHi() {
*!*
    alert( user.name ); // leads to an error
*/!*
  }

};


let admin = user;
user = null; // overwrite to make things obvious

admin.sayHi(); // Whoops! inside sayHi(), the old name is used! error!
```

Nếu sử dụng `this.name` thay vì `user.name` thì `alert` sẽ chạy ok.

## "this" không bị ràng buộc

Trong JavaScript, "this" không giống các NNLT khác. Nó có thể dùng trong bất cứ hàm nào.

Không có lỗi cú pháp trong code bên dưới:

```js
function sayHi() {
  alert( *!*this*/!*.name );
}
```

Giá trị của `this` được đánh giá khi chạy chương trình, nó có thể là bất cứ cái gì.

Ví dụ, cùng một hàm nhưng có thể có "this" khác nhau khi gọi hàm ở các object khác nhau:

```js run
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
  alert( this.name );
}

*!*
// use the same functions in two objects
user.f = sayHi;
admin.f = sayHi;
*/!*

// these calls have different this
// "this" inside the function is the object "before the dot"
user.f(); // John  (this == user)
admin.f(); // Admin  (this == admin)

admin['f'](); // Admin (dot or square brackets access the method – doesn't matter)
```

Thực tế ta có thể gọi this mà không cần chứa trong object nào:

```js run
function sayHi() {
  alert(this);
}

sayHi(); // undefined
```

Trường hợp trên `this` là `undefined` trong "strict mode". Nếu truy cập `this.name`, sẽ báo lỗi.

Trong non-strict mode (Không có `use strict`) giá trị của `this` sẽ là *global object* (`window` nếu dùng trình duyệt chạy code). Đây là một hành vi mang tính lịch sử mà `"use strict"` sử dụng.

Chú ý là dùng `this` mà không phải trong một object là không nên, đó là một sai lầm trong code. Nếu một hàm có `this`, thì nó nên được gọi trong một ngữ cảnh object.

```smart header="Hậu quả của việc không ràng buộc `this`"
Các NNLT khác thường sẽ ràng buộc `this`, chúng thường định nghĩa method trong object với `this`.

Trong JavaScript `this` là "free", Giá trị của `this` sẽ được đánh giá khi chạy code, nhưng việc đó sẽ đưa đến câu hỏi là giá trị đó là object nào ??

Nó rất linh hoạt vì `this` dùng cho object nào cũng được, nhưng cũng đồng nghĩa với việc sẽ dễ xảy ra lỗi hơn.

Ở đây không so sánh JavaScript sử dụng `this` so với các NNLT khác là tốt hay xấu. Mà ta cần hiểu nó hoạt động như thế nào để sử dụng một cách hiệu quả
```

## Internals: Reference Type

```warn header="In-depth language feature"
Phần này là phần nâng cao. Nếu bạn muốn có thể bõ qua. Vâng, tác giả bõ qua luôn, bạn nào muốn thì đọc tiếng anh nhé. Hê hê
```

An intricate method call can lose `this`, for instance:

```js run
let user = {
  name: "John",
  hi() { alert(this.name); },
  bye() { alert("Bye"); }
};

user.hi(); // John (the simple call works)

*!*
// now let's call user.hi or user.bye depending on the name
(user.name == "John" ? user.hi : user.bye)(); // Error!
*/!*
```

On the last line there is a ternary operator that chooses either `user.hi` or `user.bye`. In this case the result is `user.hi`.

The method is immediately called with parentheses `()`. But it doesn't work right!

You can see that the call results in an error, cause the value of `"this"` inside the call becomes `undefined`.

This works (object dot method):
```js
user.hi();
```

This doesn't (evaluated method):
```js
(user.name == "John" ? user.hi : user.bye)(); // Error!
```

Why? If we want to understand why it happens, let's get under the hood of how `obj.method()` call works.

Looking closely, we may notice two operations in `obj.method()` statement:

1. First, the dot `'.'` retrieves the property `obj.method`.
2. Then parentheses `()` execute it.

So, how does the information about `this` gets passed from the first part to the second one?

If we put these operations on separate lines, then `this` will be lost for sure:

```js run
let user = {
  name: "John",
  hi() { alert(this.name); }
}

*!*
// split getting and calling the method in two lines
let hi = user.hi;
hi(); // Error, because this is undefined
*/!*
```

Here `hi = user.hi` puts the function into the variable, and then on the last line it is completely standalone, and so there's no `this`.

**To make `user.hi()` calls work, JavaScript uses a trick -- the dot `'.'` returns not a function, but a value of the special [Reference Type](https://tc39.github.io/ecma262/#sec-reference-specification-type).**

The Reference Type is a "specification type". We can't explicitly use it, but it is used internally by the language.

The value of Reference Type is a three-value combination `(base, name, strict)`, where:

- `base` is the object.
- `name` is the property.
- `strict` is true if `use strict` is in effect.

The result of a property access `user.hi` is not a function, but a value of Reference Type. For `user.hi` in strict mode it is:

```js
// Reference Type value
(user, "hi", true)
```

When parentheses `()` are called on the Reference Type, they receive the full information about the object and it's method, and can set the right `this` (`=user` in this case).

Any other operation like assignment `hi = user.hi` discards the reference type as a whole, takes the value of `user.hi` (a function) and passes it on. So any further operation "loses" `this`.

So, as the result, the value of `this` is only passed the right way if the function is called directly using a dot `obj.method()` or square brackets `obj[method]()` syntax (they do the same here).

## Arrow functions have no "this"

Arrow functions are special: they don't have their "own" `this`. If we reference `this` from such a function, it's taken from the outer "normal" function.

For instance, here `arrow()` uses `this` from the outer `user.sayHi()` method:

```js run
let user = {
  firstName: "Ilya",
  sayHi() {
    let arrow = () => alert(this.firstName);
    arrow();
  }
};

user.sayHi(); // Ilya
```

That's a special feature of arrow functions, it's useful when we actually do not want to have a separate `this`, but rather to take it from the outer context. Later in the chapter <info:arrow-functions> we'll go more deeply into arrow functions.


## Summary

- Functions được khai báo trong một property được gọi là "methods".
- Methods cho phép object có các "hành động" như `object.doSomething()`.
- Methods có thể tham chiếu đến object bằng `this`.

Giá trị của `this` được định nghĩa ở run-time.
- Khi khai báo một hàm có thể dùng `this`, Nhưng `this` sẽ không có giá trị cho đến khi gọi hàm.
- Hàm đó có thể được copy bởi nhiều object.
- Khi hàm được gọi trong cú pháp của "method": `object.method()`, giá trị của `this` chính là `object`.

Chú ý Arrow-function không có `this`. Khi `this` được gọi trong Arrow-function, nó sẽ là `this` của hàm chứa arrow-function đó.
