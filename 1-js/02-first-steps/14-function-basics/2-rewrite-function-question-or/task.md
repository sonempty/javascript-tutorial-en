importance: 4

---

# Viết lại hàm dùng phép '?' hoặc phép '||'


```js
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    return confirm('Do you have your parents permission to access this page?');
  }
}
```

Viết lại hàm `checkAge`, sử dụng:

1. Phép `'?'`
2. Phép OR `||`
