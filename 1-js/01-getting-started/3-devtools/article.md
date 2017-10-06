# Developer console

Code thì thường hay có lỗi. Có thể sai lỗi chính tả, thiếu code, không hỗ trợ chức năng....và khi lỗi thường sẽ có thông báo là lỗi gì trên màn hình console.

Tuy nhiên trên trình duyệt thì sẽ không thấy được các thông báo lỗi này để mà từ đó chúng ta có được thông tin và đi tìm xem đang lỗi chỗ nào. Vậy phải làm sao đây ?

Để xem các thông tin lỗi này trên trình duyệt có nhúng sẵn chức năng gọi là "công cụ cho nhà phát triển" "developer tools".

Các lập trình viên thường chọn Developer Tool trên Chrome hoặc FireFox. Vì 2 thằng này pro nhất so với tất cả Developer tool khác.

Developer tools thực sự mạnh mẽ và có nhiều chức năng. Chúng ta sẽ học cách sử dụng Developer Tool bên dưới.

[cut]

## Google Chrome

Mở trang này lên [bug.html](bug.html). Yên tâm, méo có Virus đâu

Có lỗi xảy ra trên trang này tuy nhiên chúng ta chẳng thấy được. Giờ mở Developer Tool lên xem nào.

Nhấn `key:F12` hoặc chuột phải và chọn `inspect`.

Nhìn nó sẽ như này:

![chrome](chrome.png)

Ở tab console sẽ thấy nó thông báo lỗi.

- Cái dòng thông báo màu đỏ đó chính là 1 cái lỗi. Nó nói là "lalala" không được định nghĩa.
- Tiếp, click vào cái link màu xanh `bug.html:12` 12 ở đây là dòng code đang lỗi.

Bên dưới thông báo lỗi là dấu nhắc lệnh màu xanh `>` . Gõ các câu lệnh JavaScript vào đây và nhấn `key:Enter` để chạy (`key:Shift+Enter` để nhập nhiều dòng lệnh).

Ok thấy lỗi rồi thì quay lại Code Editor và sửa lại dòng code số 12 trong file bug.html đi.
Sau này sẽ tìm hiểu sâu hơn về debug trên Chrome tại <info:debugging-chrome>.


## Firefox, Edge và những thằng khác

Nói chung là tương tự thôi, có thể nhìn giao diện nó hơi khác chút.

## Safari

Safari (Trình duyệt của máy MAC) thì hơi khác chút. Cần mở chức năng "Develop menu" trước.

Mở Preferences --> "Advanced" Đánh dấu vào cái checkbox như hình:

![safari](safari.png)

Nhấn `key:Cmd+Opt+C` để mở Developer Tool nhé. Thân ái.

## Tóm tắt

- Developer tools giúp chúng ta thấy được lỗi, chạy lệnh và nhiều chức năng khác.
- Mở Developer tool bằng cách nhấn `key:F12` đối với đa số trình duyệt trên Windows. Chrome cho Mac nhấn `key:Cmd+Opt+J`, Safari: `key:Cmd+Opt+C` (nhớ mở chức năng này lên đã).

Bây giờ chúng ta đã có công cụ và môi trường sẵn sàng để học tập. Trong phần kế tiếp, chúng ta sẽ đến với JavaScript.
