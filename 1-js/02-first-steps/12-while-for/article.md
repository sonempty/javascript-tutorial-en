# Vòng lặp: while và for

Thỉnh thoảng chúng ta cần lặp lại các hành động tương tự nhiều lần.

Ví dụ in ra tên hàng trong một list các mặt hàng, hay in ra các số từ 1 đên 100.

*Loops* - Vòng lặp được sử dụng để thực hiện các công việc này.

[cut]

## Vòng lặp "while"

Cú pháp:

```js
while (condition) {
  // code
  // so-called "loop body"
}
```

Khi `condition` là `true`, thì `code` trong phần thân của vòng lặp sẽ được thực thi.

Ví dụ, in ra `i` khi `i < 3`:

```js run
let i = 0;
while (i < 3) { // shows 0, then 1, then 2
  alert( i );
  i++;
}
```

Một lần thực thi code trong phần thân vòng lặp được gọi là *an iteration*. Vòng lặp trong ví dụ trên có 3 iterations.

Nếu không có lệnh `i++` trong ví dụ trên, vòng lặp sẽ lặp (theo lý thuyết) mãi mãi. Trong thực tế trình duyệt sẽ có cách để stop những vòng lặp mãi mãi, và nếu code ở phần JavaScript-server-side chúng ta có thể chấm dứt tiến trình (kill the process).

Không chỉ riêng biểu thức so sánh, một biểu thức bất kỳ hay một giá trị có thể là btđk của vòng lặp. Chúng sẽ được đánh giá và convert sang boolean bởi `while`.

Ví dụ cách viết ngắn hơn cho `while (i != 0)` là `while (i)`:

```js run
let i = 3;
*!*
while (i) { // when i becomes 0, the condition becomes falsy, and the loop stops
*/!*
  alert( i );
  i--;
}
```

````smart header="Có thể bõ cặp `{…}` ngoặc nếu chỉ có một lệnh trong thân"

```js run
let i = 3;
*!*
while (i) alert(i--);
*/!*
```
````

## Vòng lặp "do..while"

Btđk nằm phía *dưới* phần thân của vòng lặp `do..while`, cú pháp:

```js
do {
  // loop body
} while (condition);
```

Vòng lặp thực thi code trong phần thân trước, sau đó kiểm tra btđk nếu là truthy, thực hiện code một lần nữa.

For example:

```js run
let i = 0;
do {
  alert( i );
  i++;
} while (i < 3);
```

This form of syntax is rarely used except when you want the body of the loop to execute **at least once** regardless of the condition being truthy. Usually, the other form is preferred: `while(…) {…}`.

## The "for" loop

The `for` loop is the most often used one.

It looks like this:

```js
for (begin; condition; step) {
  // ... loop body ...
}
```

Let's learn the meaning of these parts by example. The loop below runs `alert(i)` for `i` from `0` up to (but not including) `3`:

```js run
for (let i = 0; i < 3; i++) { // shows 0, then 1, then 2
  alert(i);
}
```

Let's examine the `for` statement part by part:

| part  |          |                                                                            |
|-------|----------|----------------------------------------------------------------------------|
| begin | `i = 0`    | Executes once upon entering the loop.                                      |
| condition | `i < 3`| Checked before every loop iteration, if fails the loop stops.              |
| step| `i++`      | Executes after the body on each iteration, but before the condition check. |
| body | `alert(i)`| Runs again and again while the condition is truthy                         |


The general loop algorithm works like this:
```
Run begin
→ (if condition → run body and run step)
→ (if condition → run body and run step)
→ (if condition → run body and run step)
→ ...
```

If you are new to loops, then maybe it would help if you go back to the example and reproduce how it runs step-by-step on a piece of paper.

Here's what exactly happens in our case:

```js
// for (let i = 0; i < 3; i++) alert(i)

// run begin
let i = 0
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// if condition → run body and run step
if (i < 3) { alert(i); i++ }
// ...finish, because now i == 3
```

````smart header="Inline variable declaration"
Here the "counter" variable `i` is declared right in the loop. That's called an "inline" variable declaration. Such variables are visible only inside the loop.

```js run
for (*!*let*/!* i = 0; i < 3; i++) {
  alert(i); // 0, 1, 2
}
alert(i); // error, no such variable
```

Instead of defining a variable, we can use an existing one:

```js run
let i = 0;

for (i = 0; i < 3; i++) { // use an existing variable
  alert(i); // 0, 1, 2
}

alert(i); // 3, visible, because declared outside of the loop
```

````


### Skipping parts

Any part of `for` can be skipped.

For example, we can omit `begin` if we don't need to do anything at the loop start.

Like here:

```js run
let i = 0; // we have i already declared and assigned

for (; i < 3; i++) { // no need for "begin"
  alert( i ); // 0, 1, 2
}
```

We can also remove the `step` part:

```js run
let i = 0;

for (; i < 3;) {
  alert( i++ );
}
```

The loop became identical to `while (i < 3)`.

We can actually remove everything, thus creating an infinite loop:

```js
for (;;) {
  // repeats without limits
}
```

Please note that the two `for` semicolons `;` must be present, otherwise it would be a syntax error.

## Breaking the loop

Normally the loop exits when the condition becomes falsy.

But we can force the exit at any moment. There's a special `break` directive for that.

For example, the loop below asks the user for a series of numbers, but "breaks" when no number is entered:

```js
let sum = 0;

while (true) {

  let value = +prompt("Enter a number", '');

*!*
  if (!value) break; // (*)
*/!*

  sum += value;

}
alert( 'Sum: ' + sum );
```

The `break` directive is activated in the line `(*)` if the user enters an empty line or cancels the input. It stops the loop immediately, passing the control to the first line after the loop. Namely, `alert`.

The combination "infinite loop + `break` as needed" is great for situations when the condition must be checked not in the beginning/end of the loop, but in the middle, or even in several places of the body.

## Continue to the next iteration [#continue]

The `continue` directive is a "lighter version" of `break`. It doesn't stop the whole loop. Instead it stops the current iteration and forces the loop to start a new one (if the condition allows).

We can use it if we're done on the current iteration and would like to move on to the next.

The loop above uses `continue` to output only odd values:

```js run no-beautify
for (let i = 0; i < 10; i++) {

  // if true, skip the remaining part of the body
  *!*if (i % 2 == 0) continue;*/!*

  alert(i); // 1, then 3, 5, 7, 9
}
```

For even values of `i` the `continue` directive stops body execution, passing the control to the next iteration of `for` (with the next number). So the `alert` is only called for odd values.

````smart header="The directive `continue` helps to decrease nesting level"
A loop that shows odd values could look like this:

```js
for (let i = 0; i < 10; i++) {

  if (i % 2) {
    alert( i );
  }

}
```

From a technical point of view it's identical to the example above. Surely, we can just wrap the code in the `if` block instead of `continue`.

But as a side-effect we got one more figure brackets nesting level. If the code inside `if` is longer than a few lines, that may decrease the overall readability.
````

````warn header="No `break/continue` to the right side of '?'"
Please note that syntax constructs that are not expressions cannot be used in `'?'`. In particular, directives `break/continue` are disallowed there.

For example, if we take this code:

```js
if (i > 5) {
  alert(i);
} else {
  continue;
}
```

...And rewrite it using a question mark:


```js no-beautify
(i > 5) ? alert(i) : *!*continue*/!*; // continue not allowed here
```

...Then it stops working. The code like this will give a syntax error:


That's just another reason not to use a question mark operator `'?'` instead of `if`.
````

## Labels for break/continue

Sometimes we need to break out from multiple nested loops at once.

For example, in the code below we loop over `i` and `j` prompting for coordinates `(i, j)` from `(0,0)` to `(3,3)`:

```js run no-beautify
for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // what if I want to exit from here to Done (below)?

  }
}

alert('Done!');
```

We need a way to stop the process if the user cancels the input.

The ordinary `break` after `input` would only break the inner loop. That's not sufficient. Labels come to the rescue.

A *label* is an identifier with a colon before a loop:
```js
labelName: for (...) {
  ...
}
```

The `break <labelName>` statement in the loop breaks out to the label.

Like here:

```js run no-beautify
*!*outer:*/!* for (let i = 0; i < 3; i++) {

  for (let j = 0; j < 3; j++) {

    let input = prompt(`Value at coords (${i},${j})`, '');

    // if an empty string or canceled, then break out of both loops
    if (!input) *!*break outer*/!*; // (*)

    // do something with the value...
  }
}
alert('Done!');
```

In the code above `break outer` looks upwards for the label named `outer` and breaks out of that loop.

So the control goes straight from `(*)` to `alert('Done!')`.

We can also move the label onto a separate line:

```js no-beautify
outer:
for (let i = 0; i < 3; i++) { ... }
```

The `continue` directive can also be used with a label. In this case the execution jumps to the next iteration of the labeled loop.

````warn header="Labels are not a \"goto\""
Labels do not allow us to jump into an arbitrary place of code.

For example, it is impossible to do this:
```js
break label;  // jumps to label? No.

label: for (...)
```

The call to a `break/continue` is only possible from inside the loop, and the label must be somewhere upwards from the directive.
````

## Summary

We covered 3 types of loops:

- `while` -- The condition is checked before each iteration.
- `do..while` -- The condition is checked after each iteration.
- `for (;;)` -- The condition is checked before each iteration, additional settings available.

To make an "infinite" loop, usually the `while(true)` construct is used. Such a loop, just like any other, can be stopped with the `break` directive.

If we don't want to do anything on the current iteration and would like to forward to the next one, the `continue` directive does it.

`Break/continue` support labels before the loop. A label is the only way for `break/continue` to escape the nesting and go to the outer loop.
