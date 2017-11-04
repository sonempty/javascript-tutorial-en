
# Kiểu Symbol

Object property Keys chỉ có thể là String hoặc Sybol. Không thể là numbers, booleans...

Trước giờ chúng ta chỉ sử dụng String để làm key, giờ ta sử dụng Sybol xem như thế nào nhé.

[cut]

## Symbols

Một giá trị "Symbol" đại diện cho định danh **duy nhất**.

Giá trị đó được tạo ra bởi `Symbol()`:

```js
// id is a new symbol
let id = Symbol();
```

Có thể thêm description cho Sybol (được gọi là symbol name), sẽ dễ dàng cho debug code:

```js
// id is a symbol with the description "id"
let id = Symbol("id");
```

Symbols được đảm bảo là duy nhất. cho dù có cùng description, chúng vẫn khác nhau. Description chỉ là cái label thôi, không có ảnh hưởng gì.

Ví dụ hai Sybols có cùng description -- Chúng không bằng nhau:

```js run
let id1 = Symbol("id");
let id2 = Symbol("id");

*!*
alert(id1 == id2); // false
*/!*
```

Nếu bạn có được học về "symbols" ở các NNLT khác rồi -- đừng nhầm lẫn. Symbol trong JavaScript là khác biệt với các NNLT khác.

````warn header="Symbols không bị convert sang string"
Nhiều giá trị trong JavaScript hỗ trợ việc convert qua string. Ví dụ `alert` sẽ convert giá trị truyền vào sang String. Symbols là đặc biệt, nó sẽ không bị tự động convert.

ví dụ:

```js run
let id = Symbol("id");
*!*
alert(id); // TypeError: Cannot convert a Symbol value to a string
*/!*
```

Nếu thực sự muốn in ra một Sysbol thì dùng `.toString()` :
```js run
let id = Symbol("id");
*!*
alert(id.toString()); // Symbol(id), now it works
*/!*
```

Đó là sự bảo bộ từ JS để tránh sự rối rắm. Và thực tế thì cũng chẳng ai đi convert Symbol sang String làm gì.

````

## Property ẩn

Symbols giúp tạo ra các property ẩn trong object, mà *thỉnh thoảng* không cho phép truy cập hay ghi đè.

Ví dụ muốn tạo ra một định danh cho `user`, sử dụng Sybol làm key:

```js run
let user = { name: "John" };
let id = Symbol("id");

user[id] = "ID Value";
alert( user[id] ); // we can access the data using the symbol as the key
```

Sử dụng `Symbol("id")` có ưu điểm gì so với dùng String `"id"`?

Giả sử một đoạn script khác muốn dùng property "id" của `user`, for its own purposes. Nó sẽ không ý thức được là là "id" của script nào khác hay không.

Nó tạo ra một `Symbol("id")`, như này:

```js
// ...
let id = Symbol("id");

user[id] = "Their id value";
```

Như thế sẽ không bị trùng nhau, vì Symbol luôn khác nhau, cho dù có cùng tên.

Nếu sử dụng string `"id"` thì trong trường hợp này sẽ bị trùng:

```js run
let user = { name: "John" };

// our script uses "id" property
user.id = "ID Value";

// ...if later another script the uses "id" for its purposes...

user.id = "Their id value"
// boom! overwritten! it did not mean to harm the colleague, but did it!
```

### Symbols trong một literal

Nếu sử dụng Symbol trong object literal, phải dùng cặp ngoặc vuông.

Như này:

```js
let id = Symbol("id");

let user = {
  name: "John",
*!*
  [id]: 123 // not just "id: 123"
*/!*
};
```
Bởi vì ta cần giá trị của biến `id` làm key, không phải string "id".

### Symbols bị bõ qua trong for..in

Symbolic properties không được truy xuất bởi vòng lặp `for..in`.

Ví dụ:

```js run
let id = Symbol("id");
let user = {
  name: "John",
  age: 30,
  [id]: 123
};

*!*
for (let key in user) alert(key); // name, age (no symbols)
*/!*

// the direct access by the symbol works
alert( "Direct: " + user[id] );
```

Đây chính là tính "ẩn" của property có key là Symbol.

Ngược lại, [Object.assign](mdn:js/Object/assign) sẽ copy cả string và symbol properties:

```js run
let id = Symbol("id");
let user = {
  [id]: 123
};

let clone = Object.assign({}, user);

alert( clone[id] ); // 123
```

````smart header="Property keys của các kiểu dữ liệu khác sẽ bị convert sang strings"
Ta chỉ dùng strings hoặc symbols làm key. Kiểu dữ liệu khác sẽ bị convert sang strings.

Ví dụ number `0` trở thành `"0"` nếu dùng làm property key:

```js run
let obj = {
  0: "test" // same as "0": "test"
};

// both alerts access the same property (the number 0 is converted to string "0")
alert( obj["0"] ); // test
alert( obj[0] ); // test (same property)
```
````

## Global symbols

Như chúng ta đã thấy, thông thường tất cả các symbols đều khác nhau, ngay cả khi chúng có cùng tên. Nhưng đôi khi chúng ta muốn các symbols có cùng tên là cùng một thực thể.

Ví dụ, các phần khác nhau của ứng dụng muốn truy cập chính xác cùng một symbol `" id "`.

Để làm điều đó ta dùng `Symbol.for(key)`.

Nó sẽ kiểm tra trong global registry, Nếu có sẵn Symbol có description là `key`, thì sẽ trả về Symbol đó, nếu không có thì tạo ra `Symbol(key)` mới và lưu vào registry.

Ví dụ:

```js run
// read from the global registry
let id = Symbol.for("id"); // if the symbol did not exist, it is created

// read it again
let idAgain = Symbol.for("id");

// the same symbol
alert( id === idAgain ); // true
```

Symbols trong registry được gọi là *global symbols*.

```

### Symbol.keyFor

Đối với global symbols, `Symbol.for(key)` trả về symbol bởi tên của nó, Còn `Symbol.keyFor(sym)` thì ngược lại, nó trả về tên của global symbol.

Ví dụ:

```js run
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// get name from symbol
alert( Symbol.keyFor(sym) ); // name
alert( Symbol.keyFor(sym2) ); // id
```

`Symbol.keyFor` chỉ dùng với global symbol trong registry. Nên nó không hoạt động với non-global symbols. Nếu Symbol không phải là global, nó trả về `undefined`.

Ví dụ:

```js run
alert( Symbol.keyFor(Symbol.for("name")) ); // name, global symbol

alert( Symbol.keyFor(Symbol("name2")) ); // undefined, the argument isn't a global symbol
```

## System symbols

Có sẵn một số "system" symbols trong JavaScript, sử dụng với hệ thống, ta có thể sử dụng nó để tinh chỉnh một số thứ.

Tìm hiểu ở đây [Well-known symbols](https://tc39.github.io/ecma262/#sec-well-known-symbols):

- `Symbol.hasInstance`
- `Symbol.isConcatSpreadable`
- `Symbol.iterator`
- `Symbol.toPrimitive`
- ...and so on.

Ví dụ, `Symbol.toPrimitive` cho phép mô tả Object để convert sang primitives. Sẽ học sau.

Các Symbol khác khi học đến bạn sẽ hiểu, giờ nói cũng chả hiểu gì đâu.

## Tổng kết

`Symbol` là một kiểu primitive sử dụng cho định danh duy nhất.

Symbols được tạo ra bởi `Symbol()` với một cái tên.

Symbols luôn có giá trị khác nhau, cho dù có cùng tên. Nếu muốn cùng-tên-cùng-symbol thì dùng global registry: `Symbol.for(key)`.

Symbols được dùng trong hai trường hợp:

1. Giấu đi object properties.
    If we want to add a property into an object that "belongs" to another script or a library, we can create a symbol and use it as a property key. A symbolic property does not appear in `for..in`, so it won't be occasionally listed. Also it won't be accessed directly, because another script does not have our symbol, so it will not occasionally intervene into its actions.

    So we can "covertly" hide something into objects that we need, but others should not see, using symbolic properties.

2. There are many system symbols used by JavaScript which are accessible as `Symbol.*`. We can use them to alter some built-in behaviors. For instance, later in the tutorial we'll use `Symbol.iterator` for [iterables](info:iterable), `Symbol.toPrimitive` to setup [object-to-primitive conversion](info:object-toprimitive) and so on.

Technically, symbols are not 100% hidden. There is a built-in method [Object.getOwnPropertySymbols(obj)](mdn:js/Object/getOwnPropertySymbols) that allows us to get all symbols. Also there is a method named [Reflect.ownKeys(obj)](mdn:js/Reflect/ownKeys) that returns *all* keys of an object including symbolic ones. So they are not really hidden. But most libraries, built-in methods and syntax constructs adhere to a common agreement that they are. And the one who explicitly calls the aforementioned methods probably understands well what he's doing.
