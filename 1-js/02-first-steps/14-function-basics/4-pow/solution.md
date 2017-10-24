
```js run demo
function pow(x, n) {
  let result = x;

  for (let i = 1; i < n; i++) {
    result *= x;
  }

  return result;
}

let x = prompt("x?", '');
let n = prompt("n?", '');

if (n <= 1) {
  alert(`Power ${n} is not supported,
    use an integer greater than 0`);
} else {
  alert( pow(x, n) );
}
```

Nếu Pro hơn thì hàm `pow(x, n)` được viết như sau:

```js
function pow(x, n) {
  return (n == 0) ? 1 : x * pow(x, n - 1);
}
```
