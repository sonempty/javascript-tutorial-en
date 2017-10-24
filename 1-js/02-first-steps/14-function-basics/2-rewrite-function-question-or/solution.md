Dùng `'?'`:

```js
function checkAge(age) {
  return (age > 18) ? true : confirm('Did parents allow you?');
}
```

Dùng OR `||` :

```js
function checkAge(age) {
  return (age > 18) || confirm('Did parents allow you?');
}
```

Cặp dấu ngoặc bao quanh `age > 18` có thể bõ, nhưng nên viết vào cho dễ đọc.
