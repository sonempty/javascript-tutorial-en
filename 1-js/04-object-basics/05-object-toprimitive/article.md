
# Object to primitive conversion

Chuyện gì xảy ra khi cộng `obj1 + obj2`, trừ `obj1 - obj2` hoặc in ra bằng `alert(obj)`?

Có một số method trong object sẽ thực hiện việc convert object sang primitive.

Trong chương <info:type-conversions> chúng ta đã học nguyên tắc để convert number, string, boolean. Nhưng chưa học về việc chuyển đổi Object sang primitive.

[cut]

Đối với object sẽ không chuyển đổi qua boolean, vì tất cả object đều là `true` cho nên ta chỉ xét việc convert sang string và number.

Chuyển đổi sang number khi thực hiện các phép toán số học. Ví dụ, `Date` objects (Sẽ học trong chương <info:date>) có thể thực hiện phép trừ, và kết quả của `date1 - date2` là khoảng thời gian giữa 2 dates đó.

Chuyển đổi sang string -- thường sử dụng trong một số phương thức nào đó cần string như `alert(obj)` ...

## ToPrimitive

Convert object sang kiểu primitive ta sử dụng thuật toán `ToPrimitive` ([specification](https://tc39.github.io/ecma262/#sec-toprimitive)).

Thuật toán này cho phép ta chỉnh sửa theo mong muốn việc convert bằng method có sẵn trong object.

Tùy thuộc vào ngữ cảnh, chuyển đổi có cái gọi là "hint".

Có ba biến thể:

`"string"`
: khi cần một sự chuyển đổi sang string, ví dụ `alert`:

    ```js
    // output
    alert(obj);

    // using object as a property key
    anotherObj[obj] = 123;
    ```

`"number"`
: Khi cần một number, ví dụ:

    ```js
    // explicit conversion
    let num = Number(obj);

    // maths (except binary plus)
    let n = +obj; // unary plus
    let delta = date1 - date2;

    // less/greater comparison
    let greater = user1 > user2;
    ```

`"default"`
: Khi một số ít toán tử chưa biết là sẽ cần chuyển đổi sang kiểu nào.

    Ví dụ toán tử `+` có thể dùng với string (nối chuỗi) và numbers (phép cộng số học), hoặc phép `==` với string, number hoặc symbol.

    ```js
    // binary plus
    let total = car1 + car2;

    // obj == string/number/symbol
    if (user == 1) { ... };
    ```

    Toán tử lớn hơn / nhỏ hơn `<>` cũng có thể sử dụng với string hoặc number. Nhưng nó sẽ sử dụng với "number" hint, không phải "default". Bởi nguyên nhân lịch sử.

    Trong thực tế tất cả built-in objects ngoại trừ một trường hợp (`Date` object, sẽ học sau) nhận `"default"` conversion giống như `"number"`. Và có lẽ chúng ta nên làm như vậy.

Chú ý: chỉ có 3 kiểu hints. không có "boolean" hint (tất objects là `true` trong boolean) hay gì khác. Và nếu ta cho `"default"` và `"number"` giống nhau, Như hầu hết các object built-ins, thì chúng ta chỉ có hai kiểu convert.

**Để convert, JavaScript sẽ gọi cả ba object methods:**

1. Gọi `obj[Symbol.toPrimitive](hint)` nếu method tồn tại,
2. Nếu không thì, nếu "hint" là `"string"`
    - Gọi `obj.toString()` và `obj.valueOf()`, bất cứ method nào tồn tại.
3. Nếu không thì, nếu "hint" là `"number"` hoặc `"default"`
    - Gọi `obj.toString()` và `obj.valueOf()`, bất cứ method nào tồn tại.

## Symbol.toPrimitive

Phương thức đầu tiên `Symbol.toPrimitive`. Đây là một built-in có tên gọi là `Symbol.toPrimitive` cần được đặt tên cho phương thức chuyển đổi:

```js
obj[Symbol.toPrimitive] = function(hint) {
  // return a primitive value
  // hint = one of "string", "number", "default"
}
```

Ví dụ với `user`:

```js run
let user = {
  name: "John",
  money: 1000,

  [Symbol.toPrimitive](hint) {
    alert(`hint: ${hint}`);
    return hint == "string" ? `{name: "${this.name}"}` : this.money;
  }
};

// conversions demo:
alert(user); // hint: string -> {name: "John"}
alert(+user); // hint: number -> 1000
alert(user + 500); // hint: default -> 1500
```

Như ta thấy ở trên, `user` tự định ngĩa việc convert nó. Method `user[Symbol.toPrimitive]` thực hiện việc chuyển đổi cho tất cả các trường hợp.


## toString/valueOf

Methods `toString` và `valueOf` có từ các bản JS cũ. Chúng không phải là symbols (symbols không tồn tại trong JS cũ), chúng cũng cung cấp cách thức để thực hiện việc convert.

Nếu không có `Symbol.toPrimitive` thì JavaScript sẽ sử dụng chúng:

- `toString -> valueOf` cho "string" hint.
- `valueOf -> toString` ngược lại.

Ví dụ `user` thực hiện convert như đã nói bằng việc kết hợp cả `toString` và `valueOf`:

```js run
let user = {
  name: "John",
  money: 1000,

  // for hint="string"
  toString() {
    return `{name: "${this.name}"}`;
  },

  // for hint="number" or "default"
  valueOf() {
    return this.money;
  }

};

alert(user); // toString -> {name: "John"}
alert(+user); // valueOf -> 1000
alert(user + 500); // valueOf -> 1500
```

Nếu muốn convert sang primitive cho tất cả trường hợp, ta chỉ dùng `toString`, như này:

```js run
let user = {
  name: "John",

  toString() {
    return this.name;
  }
};

alert(user); // toString -> John
alert(user + 500); // toString -> John500
```

Nếu không có `Symbol.toPrimitive` và `valueOf`, thì `toString` sẽ xử lý tất cả primitive conversions.


## ToPrimitive và ToString/ToNumber

Điều quan trọng cần biết về tất cả các phương pháp chuyển đổi nguyên thủy là chúng không nhất thiết trả về nguyên thủy "gợi ý"..

Không có sự kiểm soát nào cho `toString()` trả về chính xác một string, hay `Symbol.toPrimitive` method trả về number khi hint == "number".

**Điều bắt buộc duy nhất: các methods đó phải trả về một primitive.**

ví dụ:

- Mathematical operations (ngoại trừ + ) biểu diễn `ToNumber` conversion:

    ```js run
    let obj = {
      toString() { // toString handles all conversions in the absence of other methods
        return "2";
      }
    };

    alert(obj * 2); // 4, ToPrimitive gives "2", then it becomes 2
    ```

- Binary plus kiểm tra primitive -- nếu là string thì nối chuỗi, ngược lại biểu diễn `ToNumber` và thực hiện phép cộng numbers.

    String example:
    ```js run
    let obj = {
      toString() {
        return "2";
      }
    };

    alert(obj + 2); // 22 (ToPrimitive returned string => concatenation)
    ```

    Number example:
    ```js run
    let obj = {
      toString() {
        return true;
      }
    };

    alert(obj + 2); // 3 (ToPrimitive returned boolean, not string => ToNumber)
    ```

```smart header="Historical notes"
Vì lý do lịch sử, methods `toString` hoặc `valueOf` *nên* trả về một primitive: nếu trả về một object, sẽ không có lỗi, nhưng sẽ bị bõ qua (giống như method đó không tồn tại).

Tương phản, `Symbol.toPrimitive` *phải* trả về primitive, nếu không sẽ có lỗi.
```

## Tổng kết

Object-to-primitive conversion được gọi tự động, nhưng một vài bởi một số hàm built-in và toán tử cần một giá trị primitive.

Có 3 kiểu gợi ý (hints) cho việc convert:
- `"string"` (cho `alert` và một số string conversion khác)
- `"number"` (cho toán học)
- `"default"` (một vài toán tử)

The specification describes explicitly which operator uses which hint. There are very few operators that "don't know what to expect" and use the `"default"` hint. Usually for built-in objects `"default"` hint is handled the same way as `"number"`, so in practice the last two are often merged together.

The conversion algorithm is:

1. Call `obj[Symbol.toPrimitive](hint)` if the method exists,
2. Otherwise if hint is `"string"`
    - try `obj.toString()` and `obj.valueOf()`, whatever exists.
3. Otherwise if hint is `"number"` or `"default"`
    - try `obj.valueOf()` and `obj.toString()`, whatever exists.

In practice, it's often enough to implement only `obj.toString()` as a "catch-all" method for all conversions that return a "human-readable" representation of an object, for logging or debugging purposes.  
