importance: 4

---

# Uppercase const?

Kiểm tra đoạn mã sau đây:

```js
const birthday = '18.04.1982';

const age = someCode(birthday);
```

Hằng số `birthday` và `age` được tính toán từ `birthday` từ một vài tính toán nào đó `someCode`.

Có nên đặt tên kiểu viết hoa cho `birthday`? và `age`? hay cả hai?

```js
const BIRTHDAY = '18.04.1982'; // make uppercase?

const AGE = someCode(BIRTHDAY); // make uppercase?
```

