# Methods của primitives

JavaScript cho phép làm việc với primitives (strings, numbers ..) như kiểu chúng là objects.

Nó cung cấp các method có thể gọi được trên primitives, chúng ta sẽ học ngay bây giờ, nhưng chúng ta sẽ xem xét tại sao lại như thế. Bởi dù sao primitive không phải là objects.

[cut]

Chúng ta cùng phân biệt những điểm chính giữa primitives và objects.

Một object
: có khả năng lưu trữ nhiều giá trị trong các properties.
Có thể được tạo ra bằng cách `{}`, Ví dụ: `{name: "John", age: 30}`. Có nhiều kiểu Object khác trong JavaScript, Ví dụ. functions là objects.

Một trong những điều hay nhất về objects là ta có thể lưu một hàm vào properties:

```js run
let john = {
  name: "John",
  sayHi: function() {
    alert("Hi buddy!");
  }
};

john.sayHi(); // Hi buddy!
```

Ở đây ta tạo ra object `john` với method `sayHi`.

Một vài Object built-in có sẵn trong JS, ví dụ dates, errors, HTML elements ... Nó có các properties và methods khác nhau.

Nhưng, các tính năng đó đều phải trả giá!

Objects nặng hơn primitives, chúng chiếm nhiều tài nguyên hệ thống hơn. Nhưng chúng lại rất hữu ích trong lập trình, JavaScript engines đang cố gắng cải thiện chúng, để giảm sự tiêu tốn về tài nguyên hệ thống.

## Một primitive là một object

Đây là nghịch lý trong JavaScript:

- Có vài thứ ta muốn làm với primitive, và những việc đó sẽ dễ dàng hơn nếu có sẵn các method.
- Primitives phải nhanh và nhẹ như chúng vốn có.

Và giải pháp là:

1. Primitives vẫn là primitive. Một giá trị đơn như mong muốn.
2. JS cho phép truy cập các methods và properties của strings, numbers, booleans và symbols.
3. Khi điều này xảy ra một "object tạm thời - object wrapper" được tạo ra cung cấp chức năng này, sau đó nó được xóa đi.

"Object wrappers" khác nhau cho mỗi loại primitive, gồm: `String`, `Number`, `Boolean` và `Symbol`. Như vậy chúng cũng cung cấp các methods khác nhau.

Ví dụ, có method [str.toUpperCase()](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) trả về một string được viết hoa.

Như này:

```js run
let str = "Hello";

alert( str.toUpperCase() ); // HELLO
```

Đây là những gì xảy ra khi ta gọi `str.toUpperCase()`:

1. Chuỗi `str` là một primitive. Vì vậy khi ta truy cập property của nó, một object tạm thời được tạo ra, với những method hữu ích như `toUpperCase()`.
2. Gọi method này, nó chạy và trả về chuỗi `str` được viết hoa.
3. Object tạm bị xóa, để lại primitive `str` như ban đầu.

Vì vậy primitives có thể cung cấp các methods, nhưng chúng nhẹ hơn.

JavaScript engine đã và đang cải thiện rất nhiều quá trình này. Nó thậm chí không tạo ra Object tạm như đã nói, tuy nhiên ở đây ta vẫn đề cập đến cho dễ hiểu.

Number có các method của nó, ví dụ, [toFixed(n)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) để làm tròn số:

```js run
let n = 1.23456;

alert( n.toFixed(2) ); // 1.23
```

Ta sẽ học nhiều về các method của string, number ở bài <info:number> và <info:string>.


````warn header="Constructors `String/Number/Boolean` chỉ được dùng nội bộ"
các NNLT khác như Java tạo ra "wrapper objects" cho primitives một cách rõ ràng bởi cú pháp `new Number(1)` hoặc `new Boolean(false)`.

Trong JavaScript, cũng có thể, Nhưng **không được khuyến khích**. Chúng dành cho một số thứ quái đản khác.

Ví dụ:

```js run
alert( typeof 1 ); // "number"

alert( typeof new Number(1) ); // "object"!
```

Và, `zero`, là một object, nên:

```js run
let zero = new Number(0);

if (zero) { // zero is true, because it's an object
  alert( "zero is truthy?!?" );
}
```

Sử dụng hàm `String/Number/Boolean` không có `new` cho một số thứ hữu dụng. chúng convert giá trị sang kiểu: string, number, hoặc boolean (primitive).

Ví dụ:
```js
let num = Number("123"); // convert a string to number
```
````


````warn header="null/undefined không có methods"
Kiểu primitives đặc biệt `null` và `undefined` là ngoại lệ. Chúng không có "wrapper objects" tương ứng và không cung cấp các methods. Trong một ngữ nghĩa nào đó chúng là "the most primitive - nguyên thủy nhất".

VD:

```js run
alert(null.test); // error
````

## Tổng kết

- Primitives ngoại trừ `null` và `undefined` cung cấp một số methods hữu ích. Ta sẽ học sau.
- Chính thức, các method này hoạt động thông qua các object tạm thời, Nhưng JavaScript engines đang tối ưu hết sức, nên sẽ không tiêu tốn tài nguyên cho lắm khi sử dụng chúng.
