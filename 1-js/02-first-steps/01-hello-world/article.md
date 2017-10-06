# Hello, world!

Hướng dẫn mà bạn đang đọc là cơ bản cốt lõi của JavaScript, dùng được trên mọi nền tảng. Thêm nữa, bạn sẽ học về Node.JS và các nền tảng khác sử dụng JavaScript.

Chúng ta sẽ học và thực hành các đoạn mã JavaScript ngay trên trình duyệt. Tuy nhiên chúng ta sẽ dùng các câu lênh đặc trưng của trình duyệt (như `alert`) ở mức tối thiểu, do đó nên bạn không cần mất thời gian đi tìm hiểu sâu về các câu lệnh như thế này, thay vì đó hãy tập trung vào một môi trường khác như Node.JS. Các câu lệnh đặc trưng và chi tiết của trình duyệt sẽ được giải thích trong phần [tiếp theo] (/ ui) của hướng dẫn này.

Đầu tiên, hãy xem cách để nhúng một đoạn mã JavaScript vào một trang web. Đối với các môi trường phía máy chủ như Node.JS, bạn chỉ có thể thực hiện nó bằng cửa sổ lệnh ví dụ như `" node my.js "`.


[cut]

## Thẻ "script"

Một chương trình JavaScript được chèn vào tài liệu HTML bằng cách dùng thẻ `<script>`.

Ví dụ:

```html run height=100
<!DOCTYPE HTML>
<html>

<body>

  <p>Before the script...</p>

*!*
  <script>
    alert( 'Hello, world!' );
  </script>
*/!*

  <p>...After the script.</p>

</body>

</html>
```

```online
Bạn có thể chạy ví dụ này bằng cách click vào nút "Play" ở gõ trên bên phải.
```

Thẻ `<script>` chứa các dòng lệnh JavaScript và sẽ được thực thi một cách tự động khi trình duyệt được tải.


## The modern markup

Thẻ `<script>` có vài thuộc tính nhưng ngày nay ít được sử dụng, chúng ta cùng điểm qua một chút:

 Thuộc tính `type` : <code>&lt;script <u>type</u>=...&gt;</code>

 : Tiêu chuẩn cũ HTML4 yêu cầu các thẻ `<script>` phải có thuộc tính này . Thông thường hay dùng là `type="text/javascript"`. Tiêu chuẩn HTML hiện đại ngày nay thì mặc định `type` như trên. Bạn không cần điền nữa.

 Thuộc tính `language` : <code>&lt;script <u>language</u>=...&gt;</code>
  : Thuộc tính này thể hiện là đoạn Script chèn vào thuộc ngôn ngữ nào. Hiện nay thì không cần thiết nữa, JavaScript là mặc định. Không cần dùng thuộc tính này nữa.

Chú thích trước và sau Script.
: Trong các Ebook hoặc hướng dẫn trên web từ thời xa xưa bạn hay thấy như thế này:

    ```html no-beautify
    <script type="text/javascript"><!--
        ...
    //--></script>
    ```

    Các chú thích này là để ẩn code trong trường hợp trình duyệt không hỗ trợ JavaScript. Tuy nhiên khoảng 15 năm trở lại đây thì mọi trình duyệt đều hỗ trợ JavaScript. Nên bạn không cần để ý đến thuộc tính này. Mà nói chung cũng chả còn trang web nào như thế nữa đâu.


## scripts bên ngoài tài liệu HTML

Nếu có quá nhiều đoạn mã JavaScript trên Website. Bạn có thể tách nó ra các file riêng biệt.

Các file này chúng ta sẽ nhúng vào tài liệu HTML bằng thuộc tính `src` :

```html
<script src="/đường/dẫn/đến/file/script.js"></script>
```

Ở đây `/đường/dẫn/đến/file/script.js` là đường dẫn tuyệt đối đến file script.js (tính từ site root).

Cũng có thể dùng đường dẫn tương đối, ví dụ `src="script.js"` nghĩa là `"script.js"` nằm trong thư mục hiện hành.

Cũng có thể điền URL đầy đủ đến Script nếu nó được lưu Online ở đâu đó trên mạng:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.2.0/lodash.js"></script>
```

Add nhiều file thì dùng nhiều thẻ như bên dưới:

```html
<script src="/js/script1.js"></script>
<script src="/js/script2.js"></script>
…
```

```smart
Theo nguyên tắc, chỉ có các tập lệnh đơn giản nhất được đưa vào tài liệu HTML. Những tệp tin phức tạp hơn nằm trong các tệp riêng biệt.

Lợi ích của việc tách code ra riêng biệt các file là trình duyệt sẽ tải xuống và sau đó lưu trữ trong [cache](https://en.wikipedia.org/wiki/Web_cache). 

Sau đó nếu tải lại trang web thì sẽ rất nhanh vì không cần tải các script nữa, nó lưu trong cache rồi.

Điều này sẽ tiết kiệm băng thông và làm trang web chạy nhanh hơn.
```

````warn header="Nếu `src` được sử dụng thì nội dung giữa 2 thẻ `script` sẽ bị bỏ qua."
Thẻ `<script>` không thể vừa có thuộc tính `src` lại vừa có code phía trong.

Ví dụ:

```html
<script *!*src*/!*="file.js">
  alert(1); // dòng code này sẽ không chạy
</script>
```

Bạn phải chọn một trong hai cách,  `<script src="…">` hoặc `<script>` với code bên trong.

Ví dụ bên trên có thể sửa lại bằng cách tách ra làm hai như sau:

```html
<script src="file.js"></script>
<script>
  alert(1);
</script>
```
````

## Tổng kết

- Chúng ta sử dụng thẻ `<script>` để chèn mã JavaScript vào trang web.
- Thuộc tính `type` và `language` là không cần thiết.
- Script được lưu trong file nào đó được chèn vào HTML bằng cách `<script src="path/to/script.js"></script>`.


Có rất nhiều thứ để tìm hiểu về các kịch bản của trình duyệt và sự tương tác của chúng với trang web. Nhưng chúng ta hãy nhớ rằng phần này của hướng dẫn này dành cho ngôn ngữ JavaScript, hãy tập trung vào JS. Chúng tôi sẽ sử dụng một trình duyệt như một cách để chạy JavaScript, để tiện hơn cho việc học trực tuyến.
