Dùng `if`:

```js
function min(a, b) {
  if (a < b) {
    return a;
  } else {
    return b;
  }
}
```

Pro hơn thì dùng `'?'`:

```js
function min(a, b) {
  return a < b ? a : b;
}
```

P.S. Trường hợp `a == b` thì trả về `a` hay `b` cũng như nhau, nên chả ảnh hưởng gì.
