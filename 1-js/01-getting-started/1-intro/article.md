# Giới thiệu về ngôn ngữ JavaScript

Hãy xem những điểm đặc biệt về JavaScript, và chúng ta sẽ làm được gì với JavaScript.

## JavaScript là cái méo gì?

*JavaScript* ban đầu được tạo ra để *"Làm cho trang web sống động hơn (make webpages alive)"*.

Các chương trình trong ngôn ngữ này được gọi là *kịch bản(scripts)*. Chúng được nhúng trong HTML và được thực thi một cách tự động khi trang web được tải.

Scripts được viết và thực thi như văn bản thuần túy (plain text) mà không cần trình biên dịch, hay bất cứ sự chuẩn bị nào như các ngôn ngữ lập trình khác.

Về khía cạnh này, JavaScript rất khác với [Java](http://en.wikipedia.org/wiki/Java).

```smart header="Tại sao là <u>Java</u>Script?"
Khi JavaScript được tạo ra, ban đầu nó có tên là "LiveScript". Nhưng tại thời điểm đó, ngôn ngữ Java đang rất thông dụng và nổi tiếng, vì vậy nó được đặt lại tên là JavaSctips để ăn hôi tên tuổi của Java. Này gọi là thấy sang bắt quàng làm họ ấy mà.

Nhưng khi phát triển, JavaScript đã trở thành một ngôn ngữ hoàn toàn độc lập, với các đặc tả riêng được gọi là [ECMAScript ](http://en.wikipedia.org/wiki/ECMAScript), và nói chung thì JavaScript và Java chẳng có liên quan gì đến nhau.
```

Hiện nay, JavaScript không chỉ chạy trên trình duyệt (front-end), mà còn chạy được trên máy chủ (back-end), hoặc trên bất kỳ thiết bị nào có hỗ trợ một chương trình đặc biệt được gọi nôm na là cỗ máy JavaScript [the JavaScript engine](https://en.wikipedia.org/wiki/JavaScript_engine).

Trên trình duyệt bạn sử dụng như Chrome, FireFox, Edge...đã nhúng sẵn JavaScript Engine rồi, đôi lúc người ta cũng hay gọi là "JavaScript virtual machine" (Máy ảo JavaScript) - Dịch ra nghe chuối VCL

Engine nó cũng có nhiều loại. Mỗi engines khác nhau lại có "kiểu code" khác nhau, Ví dụ:

- [V8](https://en.wikipedia.org/wiki/V8_(JavaScript_engine)) -- trên Chrome và Opera.
- [SpiderMonkey](https://en.wikipedia.org/wiki/SpiderMonkey) -- trên Firefox.
- ...và một số engine khác như "Trident", "Chakra" cho các phiên bản IE, "ChakraCore" cho Microsoft Edge, "Nitro" và "SquirrelFish" cho Safari, vân vân.

Nên nhớ những điều trên nhé, bởi vì có khi cần dùng hoặc debug. Ví dụ "tính năng X nào đó được hỗ trợ bởi Engine V8", thì sẽ chạy được trên Chrome và Opera.

```smart header="engines hoạt động như thế nào?"

Để tìm hiểu sâu về Engine thì phức tạp vãi lúa. Nhưng nôm na thì có ba bước cơ bản sau khi bạn chạy code.

1. Engine đọc và phân tích code của bạn.
2. Biên dịch code sang ngôn ngữ máy.
3. Và chạy thôi. Khá là nhanh.

Quá trình này được Engine tối ưu hóa theo từng giai đoạn bên trên. Nó theo dõi code được biên dịch và chạy như thế nào, phân tích các dữ liệu này để tối ưu. Cuối cùng thì cho ra kết quả là code JavaScript thường chạy rất là nhanh.
```

## JavaScript trên trình duyệt Web có thể làm gì?

JavaScript là một ngôn ngữ an toàn. Nó không cho truy nhập vào CPU và bộ nhớ máy, bởi vì ban đầu nó được tạo ra để chỉ làm việc với trình duyệt Web.

Khả năng của JavaScript phụ thuộc rất nhiều vào môi trường chạy JavaScript. Ví dụ, , [Node.JS](https://wikipedia.org/wiki/Node.js) hỗ trợ các chức năng cho phép JavaScript đọc / ghi các tập tin tùy ý, thực hiện các yêu cầu mạng, vv

Trên trình duyệt Web, JavaScript có thể làm bất cứ thứ gì liên quan đến trang web, cũng như tương tác với người dùng và máy chủ Web.

Ví dụ, trên trình duyệt JavaScript có thể:

- Tạo các thẻ HTML vào trang web, thay đổi nội dung, chỉnh sửa styles.
- Phản hồi các thao tác của người dùng, chạy các hành động khi click chuột, di chuyển con trỏ, nhấn phím.
- Gửi các yêu cầu đến máy chủ nào đó qua mạng, download và upload files (Cái mà người ta hay gọi là [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)) và [COMET](https://en.wikipedia.org/wiki/Comet_(programming)) ).
- Truy vấn và cài đặt cookies, hỏi người dùng vài câu hỏi, đưa ra các thông báo trên trang web....
- Lưu trữ dữ liệu (username, password, form mẫu....) trên trình duyệt Web của bạn.

## JavaScript không thể làm được gì trên trình duyệt Web?

Khả năng của JavaScript trong trình duyệt được giới hạn vì sự an toàn của người dùng. Mục đích là để ngăn chặn các trang web độc hại truy cập thông tin cá nhân hoặc đánh cắp dữ liệu của người dùng.

Ví dụ:

- JavaScript trên Website không thể đọc / ghi / copy các tập tin trên ổ đĩa, không thể thực thi các chương trình. Và không có quyền truy cập trực tiếp vào các chức năng của hệ điều hành.

    Các trình duyệt hiện đại cho phép JavaScript làm việc với các tệp, nhưng quyền truy cập bị hạn chế và chỉ được cung cấp nếu người dùng thực hiện các hành động nhất định, như kéo-thả (dropping) một file vào cửa sổ trình duyệt hoặc chọn file qua thẻ `<input>`.

    Có nhiều cách để tương tác với webcam/ camera/ micro và các thiết bị khác nhưng chúng cần có sự cho phép rõ ràng của người dùng. Vì vậy, một trang Web kích hoạt JavaScript không thể lén kích hoạt webcam, ghi hình và gửi thông tin cho [NSA](https://en.wikipedia.org/wiki/National_Security_Agency).
- Các tabs/windows không nhận biết lẫn nhau. Kể cả trong trường hợp từ Tab này bạn chạy JavaScript mở ra một tab khác, cũng không thể nếu mở các trang web khác nhai (khác địa chỉ, protocol hoặc port).

    Để có thể trao đổi dữ liệu giữa hai tab với nhau thì 2 trang web mở trên 2 tab này phải có các đoạn script đặc biệt để trao đổi dữ liệu qua lại.

    Sự giới hạn này đảm bảo an toàn cho người dùng. Ví dụ bạn mở trang web `http://anysite.com` ở một tab và vào `http://gmail.com` ở tab khác. Sẽ ko thể đọc trộm gmail được.
- JavaScript có thể dễ dàng truyền tải dữ liệu với máy chủ Web đang mở. Còn khả năng nhận dữ liệu từ các trang web / tên miền khác bị chặn. Nếu muốn mở, đòi hỏi sự đồng ý rõ ràng (thể hiện trong tiêu đề HTTP) từ phía xa. Một lần nữa, đó là những hạn chế về an toàn và bảo mật.

![](limitations.png)

Các giới hạn đó không tồn tại nếu JavaScript được sử dụng bên ngoài trình duyệt, ví dụ trên máy chủ. Các trình duyệt hiện đại cũng cho phép cài đặt plugin / tiện ích mở rộng có thể nhận được giấy phép mở rộng.

## Điều gì làm cho JavaScript trở nên độc nhất vô nhị?

Có ít nhất ba điều sau:

```compare
+ Tích hợp hoàn toàn với HTML/CSS.
+ Những việc đơn giản được thực hiện một cách đơn giản.
+ Được hỗ trợ bởi hầu hết các trình duyệt ở cấu hình mặc định.
```
Ba điều này chỉ tồn tại trong JavaScript mà không phải là một công nghệ nào khác trên trình duyệt..

Điều này làm cho JavaScript trở nên độc nhất vô nhị. Và đó là lý do tại sao JavaScript là công cụ phổ biến nhất để tạo các giao diện trình duyệt web.

Khi lên kế hoạch học tập một công nghệ mới, điều này có lợi cho việc kiểm tra nhu cầu sử dụng, đặc điểm công nghệ. Vì vậy để bắt kịp với thế giới, hãy chuyển sang các xu hướng hiện đại nhất bao gồm đặc tả mới (như ES6, ES7...) và khả năng tương thích trình duyệt hiện tại cũng như tương lai.


## Các ngôn ngữ dựa trên JavaScript

Cú pháp của JavaScript không phải luôn phù hợp với nhu cầu của mọi người. Vì mỗi người lại muốn có những tính năng khác nhau, làm các dự án khác nhau.

Gần đây có rất nhiều ngôn ngữ mới xuất hiện, code của chúng được được chuyển đổi sang JavaScript trước khi chạy trong trình duyệt.

Các công cụ hiện đại làm cho quá trình chuyển đổi tự động và rất nhanh, thực sự cho phép các nhà phát triển code mã bằng một ngôn ngữ khác và nó sẽ được hệ thống dịch sang JavaScript tự động hoàn toàn.

Ví dụ về các ngôn ngữ này:

- [CoffeeScript](http://coffeescript.org/) cú pháp tương tự JavaScript nhưng ngắn hơn, cho phép để viết code chính xác hơn và rõ ràng. Giống như Rub vậy.
- [TypeScript](http://www.typescriptlang.org/) tập trung vào việc "gõ dữ liệu một cách chặt chẽ", để đơn giản hóa sự phát triển và hỗ trợ của các hệ thống phức tạp. Nó được phát triển bởi Microsoft.
- [Dart](https://www.dartlang.org/) là một ngôn ngữ độc lập có Engine riêng chạy ở môi trường không phải trình duyệt (như ứng dụng dành cho thiết bị di động). Nó ban đầu được cung cấp bởi Google như là một sự thay thế cho JavaScript, nhưng đến nay, các trình duyệt yêu cầu nó chuyển đổi sang JavaScript trước khi chạy.

Còn có nhiều nữa. Tất nhiên ngay cả khi chúng ta sử dụng một trong những ngôn ngữ đó, chúng ta cũng nên biết JavaScript, để thực sự hiểu những gì chúng ta đang làm.

## Tóm tắt lại

- JavaScript ban đầu được tạo ra như là một ngôn ngữ duy nhất của trình duyệt, nhưng bây giờ nó được sử dụng trong nhiều môi trường khác nữa.
- Tại thời điểm này, JavaScript là ngôn ngữ duy nhất, phổ biến nhất mà các trình duyệt đều sử dụng và tích hợp hoàn toàn với HTML / CSS.
- Có nhiều ngôn ngữ được chuyển tải từ JavaScript và cung cấp một số tính năng nhất định. Chúng tôi khuyên bạn nên xem xét chúng, ít nhất một thời gian ngắn, sau khi đã pro JavaScript rồi.
