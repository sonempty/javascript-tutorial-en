# Constructor, toán tử "new"

Cú pháp `{...}` cho phép tạo ra một object. Nhưng khi muốn tạo ra nhiều objects tương tự nhau, Ví dụ những users hay menu items ...thì ta làm thế nào?

Chúng ta sẽ sử dụng hàm cấu trúc "Constructer function" và toán tử `"new"`.

[cut]

## Constructor function

Constructor functions là một hàm như bình thường. Với 2 quy ước sau:

1. Tên hàm bắt đầu bằng một chữ viết hoa.
2. Chúng chỉ được thực thi với toán tử `"new"`.

Ví dụ:

```js run
function User(name) {
  this.name = name;
  this.isAdmin = false;
}

*!*
let user = new User("Jack");
*/!*

alert(user.name); // Jack
alert(user.isAdmin); // false
```

Khi hàm được thực thi bởi `new User(...)`, nó sẽ thực hiện các bước sau:

1. Tạo ra một object rỗng và gán cho `this`.
2. Thực thi các câu lệnh trong function body. Thường là chỉnh sửa `this`, add thêm các properties.
3. Trả về `this`.

Nói cách khác, `new User(...)` sẽ thực hiện như sau:

```js
function User(name) {
*!*
  // this = {};  (implicitly)
*/!*

  // add properties to this
  this.name = name;
  this.isAdmin = false;

*!*
  // return this;  (implicitly)
*/!*
}
```

Và kết quả `new User("Jack")` là một object như này:

```js
let user = {
  name: "Jack",
  isAdmin: false
};
```

Bây giờ nếu muốn tạo ra một user mới, ta dùng `new User("Ann")`, `new User("Alice")` .... Sẽ ngắn hơn và cũng dể đọc hơn khi dùng object literal.

Đó là mục đích chính của constructer -- để có thể sử dụng lại việc tạo ra object.

Chú ý -- về mặt kỹ thuậ, bất kỳ một hàm nào đều có thể dùng như constructor. Đó là: bất kỳ hàm nào đều có thể dùng với `new`, Nó sẽ thực hiện theo các bước như đã nói. Viết hoa chữ cái đầu tiên của hàm là một quy ước, để cho rõ ràng rằng nó cần được dùng với `new`.

````smart header="new function() { ... }"
Nếu cần tạo ra một và chỉ một object phức tạp:

```js
let user = new function() {
  this.name = "John";
  this.isAdmin = false;

  // ...other code for user creation
  // maybe complex logic and statements
  // local variables etc
};
```

Constructor sẽ không thể tái sử dụng, vì nó không được lưu vào đâu hết, chỉ tạo ra và sử dụng. .Vì vậy, trick này nhằm mục đích đóng gói code mà constructer được sử dụng một lần duy nhất.
````

## Dual-syntax constructors: new.target

Trong hàm, ta có thể kiểm tra liệu constructer có được gọi với toán tử `new` hay không, sử dụng `new.target` property.

Nó là rỗng nếu gọi hàm mà không có toán tử `new`:

```js run
function User() {
  alert(new.target);
}

// without new:
User(); // undefined

// with new:
new User(); // function User { ... }
```

Có thể sử dụng `new` hoặc không với cú pháp bên dưới:

```js run
function User(name) {
  if (!new.target) { // if you run me without new
    return new User(name); // ...I will add new for you
  }

  this.name = name;
}

let john = User("John"); // redirects call to new User
alert(john.name); // John
```

Cách này thỉnh thoảng được sử dụng trong một số thu viện để làm code linh hoạt hơn. Có lẽ không hay lắm nếu sử dụng ở bất kỳ đâu, bởi vì bỏ qua `new` sẽ làm cho code không được minh bạch. Với `new` chúng ta có thể hiểu là : à, có một object mới được tạo ra.

## Return trong constructors

Bình thường, constructer không có câu lệnh `return`. Vì nó tự động trả về `this` sau khi thực hiện function body rồi.

Nhưng nếu có `return` thì quy tắc sẽ như sau:

- Nếu `return` một object thì ok. ko return `this` nữa.
- Nếu `return` về một primitive, thì bõ qua.

Nói cách khác, lệnh `return` về một object thì chấp nhận, nếu không thì return `this`.

Ví dụ:

```js run
function BigUser() {

  this.name = "John";

  return { name: "Godzilla" };  // <-- returns an object
}

alert( new BigUser().name );  // Godzilla, got that object ^^
```

Ví dụ `return` bị bõ qua:

```js run
function SmallUser() {

  this.name = "John";

  return; // finishes the execution, returns this

  // ...

}

alert( new SmallUser().name );  // John
```

Thông thường constructer không có câu lệnh `return`. Ở đây chúng tôi đề cập đến các hành vi đặc biệt mà trả về objects chủ yếu vì sự toàn vẹn của chương trình.

````smart header="Bõ qua cặp dấu ngoặc nhọn"
Ta có thể bõ cặp ngoặc nhọn nếu không có tham số:

```js
let user = new User; // <-- no parentheses
// same as
let user = new User();
```

Nhưng không nên làm như vậy vì nó sẽ khó nhìn và khó hiểu.
````

## Methods trong constructor

Sử dụng constructor functions để tạo ra các object mang lại rất nhiều tính linh hoạt. Constructor function có thể có các tham số để định nghĩa việc tổ chức một object, và chúng ta sẽ để cái gì vào đó.

Tất nhiên ta có thể add không chỉ là các properties vào `this`, methods cũng có thể add vào.

Ví dụ, `new User(name)` tạo ra một đối tượng với tham số `name` và method `sayHi`:

```js run
function User(name) {
  this.name = name;

  this.sayHi = function() {
    alert( "My name is: " + this.name );
  };
}

*!*
let john = new User("John");

john.sayHi(); // My name is: John
*/!*

/*
john = {
   name: "John",
   sayHi: function() { ... }
}
*/
```

## Tổng kết

- Constructor functions hay ngắn gọn là constructors, là một hàm bình thường như bao hàm khác. Nhưng theo quy ước nên đặt tên có chữ cái đầu tiên được viết hoa.
- Constructor được gọi với toán tử `new`. Nó sẽ tạo ra một object rỗng {} và gán cho `this` thực hiện phần thân hàm và trả về `this`.

Ta sử dụng Constructer để tạo ra các objects tương tự nhau.

JavaScript có sẵn một số constructer như: `Date`, `Set` (học sau).

```smart header="Objects, ta sẽ quay trở lại!"
Chương này ta học cơ bản về object và constructer thôi. Nó cần thiết cho việc học các chương tiếp theo.

Sau đó ta quay trở lại <info:object-oriented-programming> và học thêm sâu hơn với *kế thừa* và Classes.
```
