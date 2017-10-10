# Một số lệnh tương tác: alert, prompt, confirm

Bài này chúng ta học về các hàm `alert`, `prompt` and `confirm`.

[cut]

## alert

Cú pháp:

```js
alert(message);
```

Show một tin nhắn lên màn hình cho đến khi người dùng nhấn "OK".

Ví dụ:

```js run
alert("Hello");
```

Một cửa sổ nhỏ với dòng chữ `hello` xuất hiện, nó được gọi là *modal window*. Từ "modal" có nghĩa là người dùng không thể tương tác với các thành phần khác của trang web, vd như nhấn phím bất kỳ, cho đến khi click vào nút "OK".

## prompt

Hàm `prompt` có hai tham số:

```js no-beautify
result = prompt(title[, default]);
```

Nó cũng show một modal window với một tin nhắn và một input field để nhập liệu và nút OK/CANCEL.

`title`
: Tin nhắn show lên có người dùng.

`default`
: tham số phụ, giá trị mặc định của input field.

Người dùng gõ bất kỳ cái gì và nhấn OK. Hoặc thoát bằng nút CANCEL hoặc phím `key:Esc`.

Khi gọi `prompt` sẽ trả về text được nhập vào trong input form hoặc trả về `null` nếu bị canceled.

Ví dụ:

```js run
let age = prompt('How old are you?', 100);

alert(`You are ${age} years old!`); // You are 100 years old!
```

````warn header="IE: Luôn luôn đặt giá trị `default`"
Tham số này là phụ, nhưng chúng ta nên gán giá trị cho nó vì nếu không Internet Explorer sẽ insert chuỗi `"undefined"`vào prompt.

Chạy code này trên Internet Explorer để xem:

```js run
let test = prompt("Test");
```

Do đó để ngọt hơn trên IE, cần bõ default vào:

```js run
let test = prompt("Test", ''); // <-- for IE
```
````

## confirm

Cú pháp:

```js
result = confirm(question);
```

Hàm `confirm` show ra một modal window với `câu hỏi` và hai nút OK và CANCEL.

Kết quả là `true` nếu click OK và `false` cho CANCEL.

Ví dụ:

```js run
let isBoss = confirm("Are you the boss?");

alert( isBoss ); // true if OK is pressed
```

## Tóm tắt

Chúng ta đã học về 3 hàm đặc trưng của trình duyệt để tương tác với người dùng:

`alert`
: show một tin nhắn.

`prompt`
: Hỏi người dùng nhập vào dữ liệu, nếu CANCEL hoặc `key:Esc` trình duyệt trả về `null`.

`confirm`
: Show một tin nhắn và đợi người dùng nhấn "OK" hoặc "CANCEL". returns `true` nếu nhấn OK và `false` nếu CANCEL/`key:Esc`.

Tất cả 3 hàm trên đều là modal: Dừng lại sự thực thi của chương trình cho đến khi tin nhắn được xử lý xong.

Có hai sự giới hạn:

1. Vị trí của modal window do trình duyệt quyết định. thường là chính giữa màn hình.
2. Giao diện của modal windown do trình duyệt quyết định, chúng ta không sửa được.

Đây là ba cách đơn giản nhất, còn nhiều cách tương tác với người dùng nữa, nhưng chỉ màu mè hơn chút thôi. Cơ bản dùng 3 thằng này là đủ rồi.
