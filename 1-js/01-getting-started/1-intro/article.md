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
- Các tabs/windows không nhận biết lẫn nhau. Kể cả trong trường hợp từ Tab này bạn chạy JavaScript mở ra một tab khác. But even in this case, JavaScript from one page may not access the other if they come from different sites (from a different domain, protocol or port).

    This is called the "Same Origin Policy". To work around that, *both pages* must contain a special JavaScript code that handles data exchange.

    The limitation is again for user's safety. A page from `http://anysite.com` which a user has opened must not be able to access another browser tab with the URL `http://gmail.com` and steal information from there.
- JavaScript can easily communicate over the net to the server where the current page came from. But its ability to receive data from other sites/domains is crippled. Though possible, it requires explicit agreement (expressed in HTTP headers) from the remote side. Once again, that's safety limitations.

![](limitations.png)

Such limits do not exist if JavaScript is used outside of the browser, for example on a server. Modern browsers also allow installing plugin/extensions which may get extended permissions.

## What makes JavaScript unique?

There are at least *three* great things about JavaScript:

```compare
+ Full integration with HTML/CSS.
+ Simple things done simply.
+ Supported by all major browsers and enabled by default.
```

Combined, these three things exist only in JavaScript and no other browser technology.

That's what makes JavaScript unique. That's why it's the most widespread tool to create browser interfaces.

While planning to learn a new technology, it's beneficial to check its perspectives. So let's move on to the modern trends that include new languages and browser abilities.


## Languages "over" JavaScript

The syntax of JavaScript does not suit everyone's needs. Different people want different features.

That's to be expected, because projects and requirements are different for everyone.

So recently a plethora of new languages appeared, which are *transpiled* (converted) to JavaScript before they run in the browser.

Modern tools make the transpilation very fast and transparent, actually allowing developers to code in another language and autoconverting it "under the hood".

Examples of such languages:

- [CoffeeScript](http://coffeescript.org/) is a "syntax sugar" for JavaScript, it introduces shorter syntax, allowing to write more precise and clear code. Usually Ruby devs like it.
- [TypeScript](http://www.typescriptlang.org/) is concentrated on adding "strict data typing", to simplify development and support of complex systems. It is developed by Microsoft.
- [Dart](https://www.dartlang.org/) is a standalone language that has its own engine that runs in non-browser environments (like mobile apps). It was initially offered by Google as a replacement for JavaScript, but as of now, browsers require it to be transpiled to JavaScript just like the ones above.

There are more. Of course even if we use one of those languages, we should also know JavaScript, to really understand what we're doing.

## Summary

- JavaScript was initially created as a browser-only language, but now it is used in many other environments as well.
- At this moment, JavaScript has a unique position as the most widely-adopted browser language with full integration with HTML/CSS.
- There are many languages that get "transpiled" to JavaScript and provide certain features. It is recommended to take a look at them, at least briefly, after mastering JavaScript.
