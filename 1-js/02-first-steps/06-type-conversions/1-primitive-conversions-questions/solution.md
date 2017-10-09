
```js no-beautify
"" + 1 + 0 = "10" // (1)
"" - 1 + 0 = -1 // (2)
true + false = 1
6 / "3" = 2
"2" * "3" = 6
4 + 5 + "px" = "9px"
"$" + 4 + 5 = "$45"
"4" - 2 = 2
"4px" - 2 = NaN
7 / 0 = Infinity
" -9\n" + 5 = " -9\n5"
" -9\n" - 5 = -14
null + 1 = 1 // (3)
undefined + 1 = NaN // (4)
```

1. Phép cộng với một chuỗi `"" + 1` chuyển đổi `1` về kiểu string: `"" + 1 = "1"`, tiếp theo `"1" + 0`, cho ra kq như trên.
2. Phép trừ  `"-"` thì luôn chuyển đổi sang number, nó chuyển đổi `""` thành `0`.
3. `null` thành `0` sau khi ép kiểu number.
4. `undefined` thành `NaN` sau khi ép kiểu number.
