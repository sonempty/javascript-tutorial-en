importance: 4

---

# Có cần dùng "else" không?

Hàm sẽ trả về `true` nếu `age` lớn hơn `18`.

Ngược lại thì người dùng nên đi hỏi phụ huynh :D :

```js
function checkAge(age) {
  if (age > 18) {
    return true;
*!*
  } else {
    // ...
    return confirm('Did parents allow you?');
  }
*/!*
}
```

Có khác gì không nếu bõ `else` ?

```js
function checkAge(age) {
  if (age > 18) {
    return true;
  }
*!*
  // ...
  return confirm('Did parents allow you?');
*/!*
}
```

Hai hàm trên có khác gì nhau không, và tại sao?
