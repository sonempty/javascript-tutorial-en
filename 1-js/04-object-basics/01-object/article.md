
# Objects

Như đã học ở chương <info:types>, Có 7 kiểu dữ liệu trong JavaScript. Trong đó có 6 loại là nguyên thủy "primitive", bởi vì giá trị của nó chỉ bao gồm một thứ (số, chuỗi hay gì đó).

Ngược lại, objects được dùng để lưu trữ các bộ dữ liệu khác nhau và phức tạp hơn. Trong JavaScript, objects hầu như có mặt tại hầu hết khía cạnh của ngôn ngữ. Cho nên ta cần học kỹ trước khi tìm hiểu JavaScript sâu hơn.

[cut]

Một object được tạo ra bằng cặp dấu ngoặc nhọn `{…}` với các *thuộc tính - properties*. Một property là một cặp "key: value" , với `key` là một string (cũng được gọi là "tên của thuộc tính - property name"), và `value` có thể là bất cứ cái gì.

Ta có thể tưởng tượng Object là một cái tủ tài liệu. Mỗi tài liệu có tên của nó (key), nội dung tài liệu là value. Sẽ dễ tìm được tài liệu nếu nó có tên.

![](object.png)

Một object rỗng ("tủ này không có tài liệu nào") có thể tạo ra bằng hai cách:

```js
let user = new Object(); // "object constructor" syntax
let user = {};  // "object literal" syntax
```

![](object-user-empty.png)

Thông thường thì ta sử dụng `{...}`, cách này gọi là *object literal*.

## Literals và properties

Literals hiểu nôm na là *các giá trị mà thể hiện chính nó*. Search Google để tìm hiểu thêm. Mình cũng chả hiểu lắm :D

Có thể đưa ngay các properties vào `{...}` dưới dạng cặp "key: value":

```js
let user = {     // an object
  name: "John",  // by key "name" store value "John"
  age: 30        // by key "age" store value 30
};
```

Một property thì có một key (cũng được gọi là "tên" hoặc "định danh") trước dấu hai chấm `":"` và sau dấu hai chấm là value.

trong `user` object, có hai properties:

1. Property đầu tiên có tên là `"name"` và giá trị là `"John"`.
2. Property thứ hai có tên là `"age"` và giá trị là `30`.

Tưởng tượng `user` object là một cái tủ tài liệu và có hai tài liệu được đánh nhãn là "name" và "age".

![user object](object-user.png)

Chúng ta có thể thêm, lấy ra, đọc tài liệu bất cứ khi nào.

Truy xuất giá trị của property bằng cách dùng dấu chấm:

```js
// get fields of the object:
alert( user.name ); // John
alert( user.age ); // 30
```

Giá trị có thể là bất kỳ kiểu dữ liệu nào:

```js
user.isAdmin = true;
```

![user object 2](object-user-isadmin.png)

Xóa property sử dụng `delete`:

```js
delete user.age;
```

![user object 3](object-user-delete.png)

Key có thể là nhiều từ, nhưng cần có cặp dấu nháy đơn hoặc kép:

```js
let user = {
  name: "John",
  age: 30,
  "likes birds": true  // multiword property name must be quoted
};
```

![](object-user-props.png)


````smart header="Trailing comma"
Property cuối cùng nên có dấu phẩy:
```js
let user = {
  name: "John",
  age: 30*!*,*/!*
}
```
Dấu phẩy này gọi là "trailing" hoặc "hanging" comma. Làm cho việc add/remove/move quanh các properties dễ dàng hơn, bởi vì tất cả các dòng là như nhau.
````

## Dấu ngoặc vuông

Đối với properties dài, không dùng được với dấu chấm:

```js run
// this would give a syntax error
user.likes birds = true
```

Bởi vì dấu chấm thì đòi hỏi key phải là một biến định danh. Đó là: không có dấu space hay các dấu không hợp lệ.

Cách thay thế là sử dụng cặp dấu ngoặc vuông:


```js run
let user = {};

// set
user["likes birds"] = true;

// get
alert(user["likes birds"]); // true

// delete
delete user["likes birds"];
```

Chú ý key dùng trong dấu ngoặc vuông phải đặt trong cặp dấu nháy đơn hoặc kép (Để thể hiện đó là một string).

Trong cặp dấu ngoặc vuông có thể đặt một biến hay một biểu thức nào đó:

```js
let key = "likes birds";

// same as user["likes birds"] = true;
user[key] = true;
```

Một số trường hợp `key` phụ thuộc vào cái gì đó chưa biết. Ví dụ nhập vào từ người dùng, nếu truy xuất bằng dấu chấm thì không được.

Ví dụ:

```js run
let user = {
  name: "John",
  age: 30
};

let key = prompt("What do you want to know about the user?", "name");

// access by variable
alert( user[key] ); // John (if enter "name")
```


### Computed properties

Dùng dấu ngoặc vuông trong object literal. Đó gọi là *computed properties*.

Ví dụ:

```js run
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
*!*
  [fruit]: 5, // the name of the property is taken from the variable fruit
*/!*
};

alert( bag.apple ); // 5 if fruit="apple"
```

Việc này đơn giản là: `[fruit]` nghĩa là key của property sẽ lấy từ biến `fruit`.

Cho nên nếu nhập vào `"apple"`, `bag` sẽ thành `{apple: 5}`.

Về bản chất, nó tương đương với:
```js run
let fruit = prompt("Which fruit to buy?", "apple");
let bag = {};

// take property name from the fruit variable
bag[fruit] = 5;
```

...nhưng nhìn pro hơn.

Có thể sử dụng biểu thức phức tạp hơn trong dấu ngoặc vuông:

```js
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

Cặp dấu ngoặc vuông có vẽ mạnh mẽ hơn dùng dấu chấm. Nhưng khi code thì có vẻ cồng kềnh hơn

Vì vậy nếu property đơn giản thì dùng dấu chấm, còn phức tạp lằng nhằng thì dùng cặp ngoặc vuông.



````smart header="Các từ khóa có thể dùng làm key"
Ví dụ "for", "let", "return" ... dùng đặt tên biến thì không được nhưng dùng làm key thì vẫn ok.

```js run
let obj = {
  for: 1,
  let: 2,
  return: 3
}

alert( obj.for + obj.let + obj.return );  // 6
```

Cơ bản thì key có thể đặt tên gì cũng được ngoại trừ: `"__proto__"` Nó là tổ tiên của các Object, và không thể gán một giá trị non-object được:

```js run
let obj = {};
obj.__proto__ = 5;
alert(obj.__proto__); // [object Object], didn't work as intended
```

Bạn thấy gán `5` cho `__proto_` sẽ bị bõ qua.

Đó có thể sẽ là một bug trong code. Cho nên bạn cần chú ý.

Trường hợp user nhập vào "__proto__" làm key chẳng hạn, và phép gán sẽ không có tác dụng.

Có cách để sử dụng `__proto__` như một property bình thường, chúng ta sẽ học sau, trước mắt cứ biết vậy đã.

Có một cấu trúc dữ liệu khác [Map](info:map-set-weakmap-weakset), sẽ được học trong bài <info:map-set-weakmap-weakset>, nó hỗ trợ các key tùy ý.
````


## Property viết tắt

Trong code thực tế, ta hay sử dụng các biến có sẵn làm value, và key có cùng tên với biến luôn.

Ví dụ:

```js run
function makeUser(name, age) {
  return {
    name: name,
    age: age
    // ...other properties
  };
}

let user = makeUser("John", 30);
alert(user.name); // John
```

Ở ví dụ trên, properties có tên giống với tham số. Kiểu dùng này là rất phổ biến, và ta có một cách để viết ngắn gọn hơn *property viết tắt*.

Thay vì `name:name` ta viết `name`, như này:

```js
function makeUser(name, age) {
*!*
  return {
    name, // same as name: name
    age   // same as age: age
    // ...
  };
*/!*
}
```

Có thể dùng property viết tắt trong Object (các biến này đã tồn tại trước):

```js
let user = {
  name,  // same as name:name
  age: 30
};
```

## Kiểm tra sự tồn tại

Có thể truy cập trên bất kỳ property nào, nết property không tồn tại thì sẽ trả về `undefined` chứ không bị lỗi. Vậy làm sao để kiểm tra Object có một property nào đó hay không ?

```js run
let user = {};

alert( user.noSuchProperty === undefined ); // true means "no such property"
```

Phép toán `"in"` dùng để kiểm tra một property có tồn tại hay không.

Cú pháp:
```js
"key" in object
```

Ví dụ:

```js run
let user = { name: "John", age: 30 };

alert( "age" in user ); // true, user.age exists
alert( "blabla" in user ); // false, user.blabla doesn't exist
```

Chú ý, bên trái `in` phải là *property name*. Thường là string trong dấu nháy.

Không có dấu nháy để thể hiện đó là string thì có nghĩa đó là biến, ví dụ:

```js run
let user = { age: 30 };

let key = "age";
alert( *!*key*/!* in user ); // true, takes the name from key and checks for such property
```

````smart header="Sử dụng \"in\" để kiểm tra các property có giá trị `undefined`"
Thông thường, phép so sánh bằng nghiêm ngặt `"=== undefined"` sẽ ok. Nhưng có nhiều trường hợp sẽ sai, dùng `"in"` sẽ luôn ok.

Đó là trường hợp property tồn tại, nhưng giá trị của nó là `undefined`:

```js run
let obj = {
  test: undefined
};

alert( obj.test ); // it's undefined, so - no such property?

alert( "test" in obj ); // true, the property does exist!
```


Trong ví dụ trên `obj.test` tồn tại. Nên `in` hoạt động đúng.

Tình huống trên hiếm khi xảy ra vì `undefined` thường hiếm khi được dùng để gán giá trị cho biến. Người ta thường sử dụng `null` cho cho các giá trị "chưa biết" hoặc "rỗng". Vì thế `in` cũng thường ít khi được dùng.
````


## Vòng lặp "for..in"

Lặp qua các keys của Object thì ta dùng: `for..in`. Nó khác với `for(;;)` đã học trước đó nhé.

Cú pháp:

```js
for(key in object) {
  // executes the body for each key among object properties
}
```

Ví dụ, in ra các keys, values của `user`:

```js run
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for(let key in user) {
  // keys
  alert( key );  // name, age, isAdmin
  // values for the keys
  alert( user[key] ); // John, 30, true
}
```

Chú ý, tất cả các cấu trúc "for" cho phép khai bái biến ở trong vòng lặp, ví dụ trên là `let key`.

Cũng có thể dùng một biến có tên bất kỳ thay vì `key`. Ví dụ, `"for(let prop in obj)"` cũng được sử dụng rộng rãi.


### Sắp xếp Object

Các đối tượng có được sắp xếp hay không? Nói cách khác, khi ta loop qua một Object, thì sẽ theo thứ tự từ trên xuống dưới hay như nào ?

Câu trả lời là: "Được sắp xếp theo cách đặc biệt": property có key là số nguyên sẽ được sắp xếp và cũng nhảy lên trước. Còn lại thì theo thứ tự từ trên xuống.

Ví dụ Object với mã vùng điện thoại các quốc gia:

```js run
let codes = {
  "49": "Germany",
  "41": "Switzerland",
  "44": "Great Britain",
  // ..,
  "1": "USA"
};

*!*
for(let code in codes) {
  alert(code); // 1, 41, 44, 49
}
*/!*
```

Khi chạy code ta sẽ thấy:

- USA (1) in ra trước.
- Tiếp theo là Switzerland (41) và tiếp đến các mã vùng khác.

Như vậy các property đã được sắp xếp, bởi vì chúng là số nguyên `1, 41, 44, 49`.

````smart header="Integer properties? nó là cái gì?"
"integer property" là cái key dạng "interger" như ví dụ trên. Có thể convert sang number mà không thay đổi gì.

vậy, "49" là một integer property, bởi vì nó có thể convert sang number và ngược lại. Nhưng "+49" và "1.2" thì không:

```js run
// Math.trunc is a built-in function that removes the decimal part
alert( String(Math.trunc(Number("49"))) ); // "49", same, integer property
alert( String(Math.trunc(Number("+49"))) ); // "49", not same ⇒ not integer property
alert( String(Math.trunc(Number("1.2"))) ); // "1", not same ⇒ not integer property
```
````

...Nếu key là non-integer thì nó sẽ theo thứ tự từ trên xuống:

```js run
let user = {
  name: "John",
  surname: "Smith"
};
user.age = 25; // add one more

*!*
// non-integer properties are listed in the creation order
*/!*
for (let prop in user) {
  alert( prop ); // name, surname, age
}
```

Vì vậy với ví dụ về phone codes ở trên, ta có thể "cheat" bằng cách đưa key về dạng non-integer. Thêm dấu `"+"` đằng trước là ok.

Như này:

```js run
let codes = {
  "+49": "Germany",
  "+41": "Switzerland",
  "+44": "Great Britain",
  // ..,
  "+1": "USA"
};

for(let code in codes) {
  alert( +code ); // 49, 41, 44, 1
}
```

Nó sẽ in ra theo thứ tự như mong muốn.

## Copying bằng tham chiếu (reference)

Sự khác nhau cơ bản giữa objects và primitives là nó lưu trữ và copy giá trị bằng tham chiếu (by reference).

Kiểu dữ liệu primitive: strings, numbers, booleans -- được gán/copy "bởi giá trị của nó".

Ví dụ:

```js
let message = "Hello!";
let phrase = message;
```

Kết quả là hai biến sẽ cùng lưu trữ giá trị `"Hello!"`.

![](variable-copy-value.png)

Objects không giống như thế.

**Một biến không lưu trữ giá trị của Object, Nó là "địa chỉ trong bộ nhớ", hay nói cách khác là "một tham chiếu".**

Hơi khó hiểu đúng không, xem ví dụ sẽ rõ:

```js
let user = {
  name: "John"
};
```

![](variable-contains-reference.png)

Ở đây, Object được lưu ở địa chỉ nào đó trong bộ nhớ. Và biến `user` sẽ tham chiếu "reference" đến đó.

**Khi copy một Object là copy sự tham chiếu đến giá trị được lưu.**

Ví dụ:

```js no-beautify
let user = { name: "John" };

let admin = user; // copy the reference
```

Chúng ta có hai biến, và hai biến này cùng tham chiếu đến một object:

![](variable-copy-reference.png)

Chúng ta có thể truy xuất, chỉnh sửa giá trị bởi bất cứ biến nào:

```js run
let user = { name: 'John' };

let admin = user;

*!*
admin.name = 'Pete'; // changed by the "admin" reference
*/!*

alert(*!*user.name*/!*); // 'Pete', changes are seen from the "user" reference
```

Ví dụ trên cho ta thấy rằng chỉ có một object duy nhất.

### So sánh bởi tham chiếu

Phép `==` và `===` đối với Object hoạt động tương tự.

**Hai object là bằng nhau nếu chúng là một.**

Ví dụ hai biến cùng tham chiếu đến một object thì bằng nhau:

```js run
let a = {};
let b = a; // copy the reference

alert( a == b ); // true, both variables reference the same object
alert( a === b ); // true
```

Hai Object độc lập thì không bằng nhau, cho dù chúng nhìn thì như nhau:

```js run
let a = {};
let b = {}; // two independent objects

alert( a == b ); // false
```

Vì vậy so sánh hai object `obj1 > obj2` hoặc object với primitive `obj == 5`, objects sẽ được convert sang primitives. Chúng ta sẽ học về việc so sánh object ngay bây giờ, nhưng lưu ý là việc so sánh object hiếm khi dùng đến và thường sẽ dễ tạo lỗi cho code nếu không hiểu rõ.

### Const object

Một object được khai báo bởi từ khóa `const` *vẫn có thể thay đổi*.

Ví dụ:

```js run
const user = {
  name: "John"
};

*!*
user.age = 25; // (*)
*/!*

alert(user.age); // 25
```

Bạn nghĩ rằng dòng `(*)` sẽ báo lỗi? không lỗi nhé, chẳng có vấn đề gì. Bởi vì `const` set giá trị cho `user`. Và ở đây `user` lưu trữ tham chiếu đến một object. Dòng `(*)` thay đổi object, chứ không phải `user`.

Chỉ có lỗi nếu bạn gán `user` cho một thứ khác, ví dụ:

```js run
const user = {
  name: "John"
};

*!*
// Error (can't reassign user)
*/!*
user = {
  name: "Pete"
};
```

...Nhưng sẽ ra sao nếu dùng `const` cho object properties? và `user.age = 25` sẽ báo lỗi. Có thể được nhé, chúng ta sẽ học ở chương <info:property-descriptors>.

## Cloning và merging, Object.assign

Copy một object chỉ là tạo ra một reference đến cùng một object.

Nhưng muốn copy một object ra thành một object riêng biệt thì làm sao?

Có thể làm được nhé, nhưng hơi khó khăn, trong Javascript không có sẵn các phương thức để làm việc đó. Mà thật sự thì cũng ít khi có nhu cầu. Copy bởi reference thường dùng nhiều hơn trong đa số trường hợp.

Nhưng nếu thật sự cần làm, thì ta loop qua object và copy từng key, value là được.

Ví dụ:

```js run
let user = {
  name: "John",
  age: 30
};

*!*
let clone = {}; // the new empty object

// let's copy all user properties into it
for (let key in user) {
  clone[key] = user[key];
}
*/!*

// now clone is a fully independant clone
clone.name = "Pete"; // changed the data in it

alert( user.name ); // still John in the original object
```

Cũng có thể dùng [Object.assign](mdn:js/Object/assign) copy cho lẹ.

Cú pháp:

```js
Object.assign(dest[, src1, src2, src3...])
```

- Tham số `dest`, và `src1, ..., srcN` là các objects.
- Nó copy tất cả property của `src1, ..., srcN` vào `dest`. và cuối cùng trả về `dest` (sau khi đã thay đổi).

Ví dụ merge nhiều objects vào một object:
```js
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

*!*
// copies all properties from permissions1 and permissions2 into user
Object.assign(user, permissions1, permissions2);
*/!*

// now user = { name: "John", canView: true, canEdit: true }
```

Nếu object (`user`) có sẵn property cùng tên, nó sẽ bị ghi đè:

```js
let user = { name: "John" };

// overwrite name, add isAdmin
Object.assign(user, { name: "Pete", isAdmin: true });

// now user = { name: "Pete", isAdmin: true }
```

Ta sử dụng `Object.assign` thay thế cho loop để copy một cách ngắn gọn:

```js
let user = {
  name: "John",
  age: 30
};

*!*
let clone = Object.assign({}, user);
*/!*
```

Đến nay ta chỉ dùng kiểu primitive cho properties của `user` . Nếu muốn gán object cho property ta phải làm sao?

Như này:
```js run
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

alert( user.sizes.height ); // 182
```

Bây giờ copy `clone.sizes = user.sizes` lại không đủ rồi, vì `user.sizes` là một object và nó sẽ copy kiểu reference. Vì vậy `clone` và `user` đều có chung sizes mà không phải là 2 sizes độc lập:

Ví dụ:
```js run
let user = {
  name: "John",
  sizes: {
    height: 182,
    width: 50
  }
};

let clone = Object.assign({}, user);

alert( user.sizes === clone.sizes ); // true, same object

// user and clone share sizes
user.sizes.width++;       // change a property from one place
alert(clone.sizes.width); // 51, see the result from the other one
```

Để fix, thì ta loop qua key của user và `user[key]` và nếu là object thì loop tiếp. Việc này được gọi là "deep cloning".

Có một thuật toán để deep cloning cho nhiều trường hợp phức tạp hơn, được gọi là [Structured cloning algorithm](https://w3c.github.io/html/infrastructure.html#internal-structured-cloning-algorithm). Và để cho dễ dàng tiện lợi hơn, ta có thể dùng thư viện [lodash](https://lodash.com), với phương thức deep cloning có sẵn [_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep).



## Tổng kết

Objects là mảng kết hợp với nhiều tính năng riêng.

Chúng gồm các properties (cặp key-value), mà:
- Property keys phải là strings hoặc symbols (thường là strings).
- Values là bất cứ giá trị nào.

Truy xuất property ta dùng:
- Dấu chấm: `obj.property`.
- Cặp ngoặc vuông `obj["property"]`. Nó cho phép lấy key từ một biến có sẵn `obj[varWithKey]`.

Các phép toán:
- Xóa property: `delete obj.prop`.
- Kiểm tra tồn tại: `"key" in obj`.
- Lặp qua Object: `for(let key in obj)`.

Objects được gán hay copy bởi tham chiếu. Nói cách khác một biến lưu trữ object là tham chiếu đến địa chỉ của object đó trên bộ nhớ. 

Để thực sự copy (clone) một object, ta dùng `Object.assign` hoặc  [_.cloneDeep(obj)](https://lodash.com/docs#cloneDeep).

Những gì chúng ta học trong bài này là  "plain object" hay nói gọi là `Object`.

Có nhiều loại objects khác trong JavaScript:

- `Array` : mãng,
- `Date` để lưu trữ dữ liệu thời gian,
- `Error` lưu trữ lỗi.
- ...và nhiều nữa.

Chúng ta sẽ học thêm nhiều về Object. Thỉnh thoảng người ta nói "kiểu Array" hay "Kiểu Date", Nhưng chính thức thì chúng đều là Object, chẳng qua là một sự mở rộng nào đó mà thôi.

Objects trong JavaScript là rất mạnh mẽ. Bài này khá dài nhưng thật ra chỉ là chút da lông ngoài bề mặt mà thôi. Tính năng của Object còn khổng lồ lắm. Ta sẽ học từng phần, từ từ thôi, ko cần xoắn :D
