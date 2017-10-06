# Chế độ hiện đại Strict mode, "use strict"

Trong một thời gian dài JavaScript đã được phát triển mà không có vấn đề gì về tương thích. Các tính năng mới được thêm vào ngôn ngữ, đồng thời chức năng cũ không thay đổi.

Điều này có lợi ích là không bao giờ phá vỡ mã nguồn hiện có. Nhưng nhược điểm là bất kỳ sai lầm hoặc một quyết định không hoàn hảo nào đó se bị mắc kẹt trong ngôn ngữ mãi mãi.

Cho đến năm 2009 khi ECMAScript 5 (ES5) ra đời. Nó bổ sung các tính năng mới cho ngôn ngữ và sửa đổi một số các tính năng hiện có. Để giữ mã cũ có thể làm việc, hầu hết các sửa đổi được tắt theo mặc định. Một nhu cầu cho phép enable các thay đổi này với một chỉ thị đặc biệt là dùng `"use strict"`- hay sử dụng nghiêm ngặt

[cut]

## "use strict"

Chỉ thị này nhìn có vẻ giống một chuỗi ký tự: `"use strict"` hoặc `'use strict'`. Khi sử dụng chế độ này bằng cách đặt chỉ thị này vào đầu script của bạn, nó có ý nghĩa là code sẽ được chạy theo cách hiện đại.

Ví dụ:

```js
"use strict";

// this code works the modern way
...
```

Chúng ta sẽ học về hàm (một cách để nhóm các câu lệnh) sớm thôi.

Nhìn code phía dưới, lưu ý rằng `` use strict`` có thể được đặt ở đầu hàm (hầu hết các loại hàm) thay vì toàn bộ script. Sau đó chế độ nghiêm ngặt được bật trong chức năng đó. Nhưng thường mọi người sử dụng nó cho toàn bộ script.


````warn header="Ensure that \"use strict\" is at the top"
Chắc chắn rằng `"use strict"` được đặt vào đầu script, nếu không strict mode sẽ không hoạt động.

Ví dụ strict mode sẽ không hoạt động:

```js no-strict
alert("some code");
// "use strict" below is ignored, must be on the top

"use strict";

// strict mode is not activated
```

Chỉ có ghi chú có thể đặt trước `"use strict"`.
````

```warn header="Không có cách nào để hủy `use strict`"
Không có chỉ thị `"no use strict"` hay tương tự như thế.

Khi đã dùng strict mode, không có cách nào quay lại và hủy bõ giữa chừng.
```

## Luôn luôn sử dụng "use strict"

Sự khác biệt giữa `"use strict"` và  "chế độ mặc định" là `"use strict"` được đảm bảo hơn.

Trong các chương kế tiếp, khi chúng ta học về các tính năng của JS, chúng ta sẽ thực hiện các ghi chú về sự khác biệt của chế độ nghiêm ngặt. May mắn thay, không có quá thay đổi. Và chúng thực sự làm cho code của chúng ta tốt hơn.

Nói chung:

1. Dùng chỉ thị `"use strict"` để engine chạy ở chế độ hiện đại, thay đổi các hành vi của một vài tính năng có sẵn. Chúng ta sẽ thấy rõ hơn khi học các bài tiếp theo.
2. Chế độ nghiêm ngặt được bật lên bằng cách đặt `"use strict"` vào đầu script. Cũng có vài tính năng như "classes" và "modules" được bật strict mode một cách tự động.
3. Chế độ nghiêm ngặt được hỗ trợ bởi hầu hết các trình duyệt hiện nay.
4. Khuyên bạn nên dùng `"use strict"`. Tất cả các ví dụ trong tài liệu này đều dùng strict mode, rất rất hiếm khi dùng kiểu mặc định.
