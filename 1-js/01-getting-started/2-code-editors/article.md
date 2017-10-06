# Trình biên soạn - Code editors

Là nơi chiếm nhiều thời gian nhất của lập trình viên. Với một dự án lớn, nhiều file nhiều ngôn ngữ, cần tích hợp đủ thứ, cần chạy thử, debug, kiểm tra lỗi chính tả....tất nhiên là bạn không thể làm tay, mở từng file, kiểm tra từng code được rồi đúng không. Rất tốn thời gian và công sức. Vì vậy cần Coder Editor.

Có 2 loại chính: IDE và lightweight editors. Ai thích dùng loại nào thì dùng.

[cut]

## IDE

Thuật ngữ [IDE] (https://en.wikipedia.org/wiki/Integrated_development_environment) (Môi trường phát triển tích hợp) có nghĩa là một trình soạn thảo mạnh mẽ với nhiều tính năng thường hoạt động trên "toàn bộ dự án". Như đã nói, đó không chỉ là một biên tập viên, mà còn là một "môi trường phát triển" đầy đủ.

IDE tải dự án (có thể là nhiều tệp, file), và sau đó cho phép điều hướng giữa các tệp tin, cung cấp tự động hoàn thành dựa trên toàn bộ dự án, tích hợp với hệ thống quản lý phiên bản (như [git] (https://git-scm.com/) ), một môi trường thử nghiệm và công cụ khác.

Có thể tham khảo một số IDE bên dưới:

- IntelliJ editors: [WebStorm](http://www.jetbrains.com/webstorm/) cho phát triển frontend và [PHPStorm (PHP)](http://www.jetbrains.com/phpstorm/), [IDEA (Java)](http://www.jetbrains.com/idea/), [RubyMine (Ruby)](http://www.jetbrains.com/ruby/) nếu muốn dùng thêm các ngôn ngữ khác.
- Visual Studio nếu bạn là lập trình viên .NET, bản này miễn phí nhé ([Visual Studio Community](https://www.visualstudio.com/vs/community/))
- Bộ IDE của Eclipse, như [Aptana](http://www.aptana.com/) và Zend Studio.
- [Komodo IDE](http://www.activestate.com/komodo-ide) nhẹ và miễn phí [Komodo Edit](http://www.activestate.com/komodo-edit).
- [Netbeans](http://netbeans.org/).

Tất cả các IDE được liệt kê ở trên dùng được trên Windows và Mac và các IDE khác ngoài ra Visual Studio dùng được trên Linux.

Hầu hết các IDE đều phải trả phí, nhưng có cho thời gian dùng thử. Chi phí của họ thường không đáng kể so với mức lương của nhà phát triển đủ điều kiện, vì vậy chỉ cần chọn mức giá tốt nhất cho bạn. (Lừa đó, mắc lòi ra :D)

## Lightweight editors - trình biên tập nhẹ

"Lightweight editors" không mạnh mẽ như IDE, nhưng mà nó nhẹ, nhanh và đơn giản.

Chủ yếu dùng để mở và chỉnh sửa file.

Sự khác biệt chính giữa "Lightweight editors" và "IDE" là một IDE hoạt động ở cấp độ dự án, vì vậy nó sẽ tải nhiều dữ liệu hơn khi bắt đầu, phân tích cấu trúc dự án nếu cần thiết. Lightweight editors nhanh hơn nhiều vì load tệp riêng lẽ.
Trong thực tế, các Lightweight editors có thể có rất nhiều plugin bao gồm cả phân tích cú pháp, tự động hoàn thành lệnh, vì vậy không có ranh giới rõ ràng giữa Lightweight editors và IDE.

Một số Lightweight editors đáng được chú ý:

- [Visual Studio Code](https://code.visualstudio.com/) (cross-platform, free).
- [Atom](https://atom.io/) (cross-platform, free).
- [Sublime Text](http://www.sublimetext.com) (cross-platform, shareware).
- [Notepad++](https://notepad-plus-plus.org/) (Windows, free).
- Vim và Emacs cũng tàm tạm, nếu bạn quen với style của Linux

## Tác giả dùng cái gì ?

Sở thích cá nhân của tác giả là có cả một IDE cho các dự án và một trình soạn thảo nhẹ để chỉnh sửa tập tin nhanh chóng và dễ dàng.

Tôi dùng:

- [WebStorm](http://www.jetbrains.com/webstorm/) cho JS, và nếu trong dự án có cả ngôn ngữ khác nữa thì tôi dùng thêm các sản phẩm của Jetbrains như [PHPStorm](http://www.jetbrains.com/phpstorm/) (PHP), [IDEA](http://www.jetbrains.com/idea/) (Java), [RubyMine](http://www.jetbrains.com/ruby/) (Ruby).
- lightweight editor -- tôi dùng [Sublime Text](http://www.sublimetext.com) hoặc [Atom](https://atom.io/).

Nếu bạn không biết chọn gì, thì chọn đại Atom đi :D.

## Đừng tranh luận chọn dùng Editor nào nhé

Các Code Editor trong danh sách ở trên là được tôi hoặc bạn bè của tôi cho rằng các nhà phát triển giỏi đã và đang sử dụng trong một thời gian dài và họ khuyến khích người khác sử dụng.

Có nhiều Editor vĩ đại khác trong thế giới lập trình rộng lớn của chúng ta. Vui lòng chọn một trong những bạn thích nhất.

Việc lựa chọn một trình soạn thảo, giống như bất kỳ công cụ nào khác, là một việc cá nhân và phụ thuộc vào các dự án, thói quen, sở thích cá nhân của bạn.
