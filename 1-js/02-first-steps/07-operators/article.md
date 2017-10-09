# Các phép toán

Một vài phép toán chúng ta đã biết khi học ở trường. Như `+`, `-`, `*`, `/`, và vv.

Trong chương này chúng ta sẽ tập trung vào các ngoại lệ, hay sự khác biệt trong các phép toán trong JS và toán học.

[cut]

## Quy tắc: Một ngôi "unary", hai ngôi "binary" và toán hạng "operand"

Trước khi tiếp tục, chúng ta hãy nắm bắt các thuật ngữ phổ biến.

- *Toán hạng - An operand* -- là đối tượng của phép toán. Ví dụ trong phép nhân `5 * 2` có hai toán hạng: toán hạng bên trái là `5`, và toán hạng bên phải là `2`. Thỉnh thoảng người ta cũng gọi là tham số "arguments" thay vì toán hạng "operands".
- Phép toán là một ngôi *unary* nếu chỉ có 1 toán hạng. Ví dụ phép `"-"` đổi dấu một số:

    ```js run
    let x = 1;

    *!*
    x = -x;
    */!*
    alert( x ); // -1, unary negation was applied
    ```
- Phép toán là hai ngôi *binary* nếu có 2 toán hạng, tương tự n ngôi nếu có n toán hạng:

    ```js run no-beautify
    let x = 1, y = 3;
    alert( y - x ); // 2, binary minus subtracts values
    ```

    Chúng ta chủ yếu nói đến sự khác nhau giữa hai phép toán: the unary negation (phép đổi dấu) và the binary subtraction (phép trừ hai số).

## phép + là một phép toán hai ngôi - binary +

Chúng ta sẽ xem xem JS khác tóa học như thế nào.

Thông thường phép `'+'` để cộng các số.

nhưng nếu binary `+` mà có 1 toán hạng là string, thì thành phép nối chuỗi:

```js
let s = "my" + "string";
alert(s); // mystring
```

Chú ý là nếu có 1 toán hạng là string thì toán hạng kia sẽ được chuyển đổi thành string.

Ví dụ:

```js run
alert( '1' + 2 ); // "12"
alert( 2 + '1' ); // "21"
```

Trong JS phép `"+"` hơi đặc biệt. Các phép toán học khác chỉ làm việc với number, Còn phép + có thể làm việc với number và string.

Ví dụ phép trừ và phép chia:

```js run
alert( 2 - '1' ); // 1
alert( '6' / '2' ); // 3
```

## Ép kiểu number, unary +

Phép `+` có thể là phép toán 2 ngôi hoặc cũng có thể là 1 ngôi.

Phép `+` một ngôi đơn giản là chính nó. Tương tự như toán học vậy.

Ví dụ:

```js run
// No effect on numbers
let x = 1;
alert( +x ); // 1

let y = -2;
alert( +y ); // -2

*!*
// Converts non-numbers
alert( +true ); // 1
alert( +"" );   // 0
*/!*
```

Nó tương đương với `Number(...)`, nhưng viết ngắn hơn.

Nhu cầu chuyển đổi string sang số là khá nhiều. VD: Viết chương trình cộng 2 số được nhập từ bàn phím. Hay chuyển đổi giá trị nào đó từ form HTML

VD:

```js run
let apples = "2";
let oranges = "3";

alert( apples + oranges ); // "23", the binary plus concatenates strings
```

Nếu muốn là number thì ta làm như sau:

```js run
let apples = "2";
let oranges = "3";

*!*
// both values converted to numbers before the binary plus
alert( +apples + +oranges ); // 5
*/!*

// the longer variant
// alert( Number(apples) + Number(oranges) ); // 5
```

Theo quan điểm toán học, viết các dấu + như vậy có vẻ là lạ, nhưng trên quan điểm tin học, điều đó là bình thường: unary + được ưu tiên trước, chuyển đổi strings sang numbers, và sau đó binary + sẽ cộng chúng lại.

Tại sao phép toán một ngôi lại được tính trước phép toán hai ngôi? Vì theo quy ước nó được ưu tiên hơn *higher precedence*.

## Độ ưu tiên của các phép toán

Nếu một biểu thức có nhiều phép toán thì thằng nào tính trước, thằng nào tính sau?

Ở trường các bạn được học là nhân chia trước, cộng trừ sau. Ví dụ `1 + 2 * 2` cho ra kết quả là 5, ta nói phép nhân có độ ưu tiên cao hơn phép cộng.

Biểu thức trong ngoặc thì sẽ tính trước, Ví dụ trên nếu muốn phép cộng tính trước thì ta viết `(1 + 2) * 2`.

Trong JavaScript. Phép toán có độ ưu tiên cao hơn thì được thực thi trước, nếu có độ ưu tiên bằng nhau thì thực thi từ trái sang phải.

Chi tiết độ ưu tiên các bạn có thể xem tại [precedence table](https://developer.mozilla.org/en/JavaScript/Reference/operators/operator_precedence) Không cần bạn phải nhớ chi tiết, Đơn giản chỉ cần nhớ là phép toán một ngôi sẽ có độ ưu tiên cao hơn phép toán hai ngôi:

| Độ ưu tiên | Phép toán | ký tự |
|------------|------|------|
| ... | ... | ... |
| 16 | Cộng một ngôi | `+` |
| 16 | đổi dấu | `-` |
| 14 | nhân | `*` |
| 14 | chia | `/` |
| 13 | cộng | `+` |
| 13 | trừ | `-` |
| ... | ... | ... |
| 3 | gán | `=` |
| ... | ... | ... |

Ta có thể thấy "Phép cộng một ngôi" có độ ưu tiên là `16`, cao hơn phép cộng hai ngôi có độ ưu tiên `13` . Đó là lý do tại sao trong biểu thức `"+apples + +oranges"` Phép cộng một ngôi được tính trước.

## Phép gán

Chú ý rằng phép gán `=` cũng là một phép toán. Và nó có độ ưu tiên khá thấp là `3`.

Đó là lý do tại sao khi ta gán, ví dụ `x = 2 * 2 + 1`, thì giá trị được tính toán trước rồi mới gán `=` cho `x`.

```js
let x = 2 * 2 + 1;

alert( x ); // 5
```

Cũng có thể gán chồng nhau nhiều lần như thế nào:

```js run
let a, b, c;

*!*
a = b = c = 2 + 2;
*/!*

alert( a ); // 4
alert( b ); // 4
alert( c ); // 4
```

Gán chồng nhau sẽ thực hiện từ phải qua trái `2 + 2` ra `4` gán cho `c`, `b` rồi đến `a`.

````smart header="Phép gán `\"=\"` trả về giá trị"
Các phép toán trả về giá trị là kết quả của phép toán đó. ví dụ `5 + 5` kết quả là 10, và cũng là `return 10`. Tương tự phép gán cũng thế.

Ví dụ `x = value` gán `value` cho `x` *và cũng: return value*.

Ví dụ phức tạp hơn:

```js run
let a = 1;
let b = 2;

*!*
let c = 3 - (a = b + 1);
*/!*

alert( a ); // 3
alert( c ); // 0
```

In the example above, the result of `(a = b + 1)` is the value which is assigned to `a` (that is `3`). It is then used to subtract from `3`.

Funny code, isn't it? We should understand how it works, because sometimes we can see it in 3rd-party libraries, but shouldn't write anything like that ourselves. Such tricks definitely don't make the code clearer and readable.
````

## Remainder %

The remainder operator `%` despite its look does not have a relation to percents.

The result of `a % b` is the remainder of the integer division of `a` by `b`.

For instance:

```js run
alert( 5 % 2 ); // 1 is a remainder of 5 divided by 2
alert( 8 % 3 ); // 2 is a remainder of 8 divided by 3
alert( 6 % 3 ); // 0 is a remainder of 6 divided by 3
```

## Exponentiation **

The exponentiation operator `**` is a recent addition to the language.

For a natural number `b`, the result of `a ** b` is `a` multiplied by itself `b` times.

For instance:

```js run
alert( 2 ** 2 ); // 4  (2 * 2)
alert( 2 ** 3 ); // 8  (2 * 2 * 2)
alert( 2 ** 4 ); // 16 (2 * 2 * 2 * 2)
```

The operator works for non-integer numbers of `a` and `b` as well, for instance:

```js run
alert( 4 ** (1/2) ); // 2 (power of 1/2 is the same as a square root, that's maths)
alert( 8 ** (1/3) ); // 2 (power of 1/3 is the same as a cubic root)
```

## Increment/decrement

<!-- Can't use -- in title, because built-in parse turns it into – -->

Increasing or decreasing a number by one is among the most common numerical operations.

So, there are special operators for that:

- **Increment** `++` increases a variable by 1:

    ```js run no-beautify
    let counter = 2;
    counter++;      // works same as counter = counter + 1, but shorter
    alert( counter ); // 3
    ```
- **Decrement** `--` decreases a variable by 1:

    ```js run no-beautify
    let counter = 2;
    counter--;      // works same as counter = counter - 1, but shorter
    alert( counter ); // 1
    ```

```warn
Increment/decrement can be applied only to a variable. An attempt to use it on a value like `5++` will give an error.
```

Operators `++` and `--` can be placed both after and before the variable.

- When the operator goes after the variable, it is called a "postfix form": `counter++`.
- The "prefix form" is when the operator stands before the variable: `++counter`.

Both of these records do the same: increase `counter` by `1`.

Is there any difference? Yes, but we can only see it if we use the returned value of `++/--`.

Let's clarify. As we know, all operators return a value. Increment/decrement is not an exception here. The prefix form returns the new value, while the postfix form returns the old value (prior to increment/decrement).

To see the difference, here's the example:

```js run
let counter = 1;
let a = ++counter; // (*)

alert(a); // *!*2*/!*
```

Here in the line `(*)` the prefix call `++counter` increments `counter` and returns the new value that is `2`. So the `alert` shows `2`.

Now let's use the postfix form:

```js run
let counter = 1;
let a = counter++; // (*) changed ++counter to counter++

alert(a); // *!*1*/!*
```

In the line `(*)` the *postfix* form `counter++` also increments `counter`, but returns the *old* value (prior to increment). So the `alert` shows `1`.

To summarize:

- If the result of increment/decrement is not used, then there is no difference in which form to use:

    ```js run
    let counter = 0;
    counter++;
    ++counter;
    alert( counter ); // 2, the lines above did the same
    ```
- If we'd like to increase the value *and* use the result of the operator right now, then we need the prefix form:

    ```js run
    let counter = 0;
    alert( ++counter ); // 1
    ```
- If we'd like to increment, but use the previous value, then we need the postfix form:

    ```js run
    let counter = 0;
    alert( counter++ ); // 0
    ```

````smart header="Increment/decrement among other operators"
Operators `++/--` can be used inside an expression as well. Their precedence is higher than most other arithmetical operations.

For instance:

```js run
let counter = 1;
alert( 2 * ++counter ); // 4
```

Compare with:

```js run
let counter = 1;
alert( 2 * counter++ ); // 2, because counter++ returns the "old" value
```

Though technically allowable, such notation usually makes the code less readable. One line does multiple things -- not good.

While reading the code, a fast "vertical" eye-scan can easily miss such `counter++`, and it won't be obvious that the variable increases.

The "one line -- one action" style is advised:

```js run
let counter = 1;
alert( 2 * counter );
counter++;
```
````

## Bitwise operators

Bitwise operators treat arguments as 32-bit integer numbers and work on the level of their binary representation.

These operators are not JavaScript-specific. They are supported in most programming languages.

The list of operators:

- AND ( `&` )
- OR ( `|` )
- XOR ( `^` )
- NOT ( `~` )
- LEFT SHIFT ( `<<` )
- RIGHT SHIFT ( `>>` )
- ZERO-FILL RIGHT SHIFT ( `>>>` )

These operators are used very rarely. To understand them, we should delve into low-level number representation, and it would not be optimal to do that right now. Especially because we won't need them any time soon. If you're curious, you can read the [Bitwise Operators](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators) article in MDN. It would be more practical to do that when a real need arises.

## Modify-in-place

We often need to apply an operator to a variable and store the new result in it.

For example:

```js
let n = 2;
n = n + 5;
n = n * 2;
```

This notation can be shortened using operators `+=` and `*=`:

```js run
let n = 2;
n += 5; // now n = 7 (same as n = n + 5)
n *= 2; // now n = 14 (same as n = n * 2)

alert( n ); // 14
```

Short "modify-and-assign" operators exist for all arithmetical and bitwise operators: `/=`, `-=` etc.

Such operators have the same precedence as a normal assignment, so they run after most other calculations:

```js run
let n = 2;

n *= 3 + 5;

alert( n ); // 16  (right part evaluated first, same as n *= 8)
```

## Comma

The comma operator `','` is one of most rare and unusual operators. Sometimes it's used to write shorter code, so we need to know it in order to understand what's going on.

The comma operator allows us to evaluate several expressions, dividing them with a comma `','`. Each of them is evaluated, but the result of only the last one is returned.

For example:

```js run
*!*
let a = (1 + 2, 3 + 4);
*/!*

alert( a ); // 7 (the result of 3 + 4)
```

Here, the first expression `1 + 2` is evaluated, and its result is thrown away, then `3 + 4` is evaluated and returned as the result.

```smart header="Comma has a very low precedence"
Please note that the comma operator has very low precedence, lower than `=`, so parentheses are important in the example above.

Without them: `a = 1 + 2, 3 + 4` evaluates `+` first, summing the numbers into `a = 3, 7`, then the assignment operator `=` assigns    `a = 3`, and then the number after the comma `7` is not processed anyhow, so it's ignored.
```

Why do we need such an operator which throws away everything except the last part?

Sometimes people use it in more complex constructs to put several actions in one line.

For example:

```js
// three operations in one line
for (*!*a = 1, b = 3, c = a * b*/!*; a < 10; a++) {
 ...
}
```

Such tricks are used in many JavaScript frameworks, that's why we mention them. But usually they don't improve the code readability, so we should think well before writing like that.
