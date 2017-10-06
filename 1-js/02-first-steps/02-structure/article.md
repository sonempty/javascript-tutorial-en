# Cấu trúc code

Đầu tiên chúng ta sẽ học về các khối lệnh.

[cut]

## Câu lệnh

Câu lệnh (Statements) là cấu trúc ngữ pháp và lệnh để thực hiện một hành động.

Chúng ta đã được thấy câu lệnh `alert('Hello, world!')`, để show ra một câu chào lên màn hình rồi.

Một chương trình thường sẽ có nhiều câu lệnh và chúng thường được tách biệt nhau bởi dấu chấm phẩy.

Ví dụ:

```js run no-beautify
alert('Hello'); alert('World');
```

Thông thường mỗi câu lệnh nên viết trên một dòng cho dễ đọc:

```js run no-beautify
alert('Hello');
alert('World');
```

## Dấu chấm phấy (Semicolons [#semicolon])

Có thể bõ qua dấu chấm phẩy nếu xuống hàng.

Như thế này:

```js run no-beautify
alert('Hello')
alert('World')
```

Đây được gọi là dấu chấm phẩy không tường minh, xem thêm tại đây [automatic semicolon insertion](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion).

**Trong nhiều trường hợp xuống dòng có thể thay thế cho dấu chấm phẩy nhưng "KHÔNG PHẢI LUÔN LUÔN ĐÚNG"!**

Ví dụ:

```js run no-beautify
alert(3 +
1
+ 2);
```

kết quả output là `6`, Vì JavaScript không tự chèn dấu chấm phẩy nếu kết thúc dòng là `"+"`.

**Nhưng có những tình huống mà JavaScript sai lầm khi chèn dấu chấm phẩy.**

Lỗi xảy ra trong những trường hợp này khá khó tìm và khắc phục.

````smart header="An example of an error"
Nếu bạn tò mò thì xem ví dụ dưới đây:

```js run
[1, 2].forEach(alert)
```

Nếu không biết các ký tự `[]` và hàm `forEach` thì chúng ta sẽ học sau, không cần mất công tìm hiểu. Bạn chỉ cần biết đoạn mã trên sẽ thông báo ra màn hình  `1`, và sau đó là `2`.

Bây giờ thêm câu lệnh `alert` đằng trước và *KHÔNG* dùng dấu chấm phẩy để kết thúc câu lệnh này:

```js run no-beautify
alert("There will be an error")

[1, 2].forEach(alert)
```

Nếu chạy bạn sẽ thấy lệnh `alert` sẽ show ra màn hình, sau đó thì sẽ có thông báo lỗi.

Ok giờ ta sẽ sửa bằng cách thêm dấu chấm phẩy sau lệnh `alert`:
```js run
alert("All fine now");

[1, 2].forEach(alert)  
```

Giờ sẽ thấy thông báo "All fine now" sau đó là `1` và `2`.


Lỗi xảy ra do JavaScript ngụ ý là không chèn dấu chấm phẩy trước cặp ngoặc vuông `[...]`.

Vì vậy code được engine nhìn thấy như một câu lệnh đơn như thế này:

```js run no-beautify
alert("There will be an error")[1, 2].forEach(alert)
```

Và lỗi xảy ra.
````

Bạn nên đặt dấu chấm phẩy giữa các câu lệnh ngay cả khi chúng được phân cách bằng dòng mới. Quy tắc này được cộng đồng chấp nhận rộng rãi. Chúng ta hãy lưu ý một lần nữa - * có thể * bỏ dấu chấm phẩy trong hầu hết trường hợp. Nhưng để an toàn hơn - đặc biệt là cho người mới bắt đầu - hãy sử dụng dấu chấm phẩy.

## Ghi chú

Theo thời gian, chương trình sẽ mở rộng và phức tạp hơn. Việc thêm các ghi chú và mô tả vào để người đọc có thể gợi nhớ những ý nghĩa nào đó là cần thiết. VD bạn code xong để một thời gian dài không sử dụng, sau này đọc lại thì chả hiểu chương trình mình đã viết nó chạy như nào và làm gì. Nếu có ghi chú trước đó thì khỏe rồi, đọc phát là nhớ lại ngay.

Ghi chú có thể viết ở bất kỳ đâu trong chương trình, Engine sẽ bõ qua chúng.

**Ghi chú một dòng thì dùng 2 dấu gạch chéo như này `//`.**

Ví dụ:
```js run
// Đây là một ghi chú
alert('Hello');

alert('World'); // Câu lệnh này để thông báo bla bla...
```

**Ghi chú trên nhiều dòng bắt đầu bằng <code>/&#42;</code> và kết thúc bằng <code>&#42;/</code>.**

Như thế này:

```js run
/* Đây là ví dụ.
Về việc ghi chú trên nhiều dòng.
*/
alert('Hello');
alert('World');
```

Nội dung ghi chú giữa hai cặp <code>/&#42; ... &#42;/</code> sẽ được engine bõ qua.

Đôi khi nó được dùng để vô hiệu hóa một đoạn code:

```js run
/* ghi chú dòng code này
alert('Hello');
*/
alert('World');
```

```smart header="Use hotkeys!"
Hầu hết các Editor sử dụng phím tắt `key:Ctrl+/` cho ghi chú một dòng và `key:Ctrl+Shift+/` -- cho ghi chú nhiều dòng (nhớ bôi đen một đoạn code nào đó trước). Đối với MAC dùng phím `key:Cmd` thay cho `key:Ctrl`.
```

````warn header="Ghi chú chồng nhau không được hỗ trợ!"
Ghi chú `/*...*/` phía trong ghi chú khác `/*...*/`.

sẽ làm code báo lỗi ngay:

```js run no-beautify
/*
  /* nested comment ?!? */
*/
alert( 'World' );
```
````

Xin vui lòng, đừng ngần ngại ghi chú code của bạn.

Ghi chú làm tăng độ dài code, nhưng đó không phải là vấn đề. Có rất nhiều công cụ giảm thiểu mã trước khi public lên máy chủ. Chúng sẽ xóa ghi chú, vì vậy ghi chú sẽ không xuất hiện trong các tập lệnh làm việc. Cho nên việc ghi chú sẽ không có tác động tiêu cực nào.

Trong bài tiếp theo <info:coding-style> chúng ta sẽ học cách viết ghi chú sao cho chuẩn và đẹp.
