# Garbage collection

Quản lý bộ nhớ trong JavaScript được thực hiện tự động và chúng ta sẽ không nhìn thấy. Chúng ta tạo ra primitives, objects, functions... và tất cả chúng đều sẽ chiếm giữ tài nguyên bộ nhớ.

JavaScript engine sẽ phát hiện và xóa đi những thứ không còn hữu dụng để giải phóng bộ nhớ như thế nào?

[cut]

## Khả năng tiếp cận - reachability

Khái niệm chính trong JavaScript để quản lý bộ nhớ là *reachability*.

Các giá trị có thể truy cập được là các giá trị có lưu trong bộ nhớ. Chúng được gọi là *reachable*

1. Có một tập hợp các giá trị reachable, và không thể xóa được.

    Ví dụ:

    - Local variables và parameters của hàm đang thực thi.
    - Variables và parameters của hàm khác trong nested calls.
    - Biến Global.
    - (Và một số thứ khác nữa)

    Những giá trị này được gọi là giá trị gốc - *roots*.

2. Những thứ khác được xem là reachable nếu nó có thể truy cập được từ một hoặc một chuỗi sự tham chiếu vào roots.

    Ví dụ, Có một object trong local variable, và object này có các property tham chiếu đến object khác, Vậy object này là reachable. Và những objects mà nó tham chiếu đến cũng là reachable.

Đây là một background process (chạy trong background) trong JavaScript engine, nó được gọi là [garbage collector](https://en.wikipedia.org/wiki/Garbage_collection_(computer_science)). Nó theo dõi các đối tượng và xóa đi nếu chúng unreachable

## Một ví dụ đơn giản

Đây là một ví dụ đơn giản:

```js
// user has a reference to the object
let user = {
  name: "John"
};
```

![](memory-user-john.png)

Ở đây mũi tên mô tả một tham chiếu đối tượng. Biến global `"user"` tham chiếu đến đổi tượng `{name: "John"}` (ta gọi đối tượng này là John cho ngắn gọn). Key `"name"` của property của John lưu trữ một giá trị primitive, vậy nó nằm trong object.

Nếu giá trị của `user` bị ghi đè, sự tham chiếu sẽ mất đi:

```js
user = null;
```

![](memory-user-john-lost.png)

Bây giờ John đã trở thành unreachable. Không có cách nào để sử dụng (gọi) nó, không có tham chiếu đến nó. Garbage collector sẽ xóa nó để giải phóng tài nguyên bộ nhớ.

## Hai sự tham chiếu

Giờ ta copy ( bằng tham chiếu) `user` cho `admin`:

```js
// user has a reference to the object
let user = {
  name: "John"
};

*!*
let admin = user;
*/!*
```

![](memory-user-john-admin.png)

Nếu ta làm tương tự:
```js
user = null;
```

...Thì John vẫn reachable thông qua biến global `admin`, cho nên nó vẫn tồn tại trong bộ nhớ mà không bị xóa đi. Nếu ghi đè `admin`, thì John sẽ bị xóa đi.

## Liên kết objects

Một ví dụ phức tạp hơn:

```js
function marry(man, woman) {
  woman.husband = man;
  man.wife = woman;

  return {
    father: man,
    mother: woman
  }
}

let family = marry({
  name: "John"
}, {
  name: "Ann"
});
```

Hàm `marry` có hai đối tượng tham chiếu lẫn nhau, và return một đối tượng khác chứa giá trị nằm trong hai đối tượng đó.

Kết quả lưu trong bộ nhớ sẽ như thế này:

![](family.png)

Vậy, tất cả đối tượng là reachable.

Ta xóa đi hai tham chiếu:

```js
delete family.father;
delete family.mother.husband;
```

![](family-delete-refs.png)

Nếu chỉ delete một tham chiếu, thì tất cả object vẫn reachable.

Nếu delete cả hai thì ta thấy John sẽ unreachable:

![](family-no-father.png)

Tham chiếu từ John ra (outgoing reference) không có ý nghĩa. Chỉ có tham chiếu vào (incoming) mới làm đối tượng reachable. Vì vậy John hiện tại sẽ unreachable và sẽ bị xóa đi.

Sau khi garbage collection:

![](family-no-father-2.png)

## Unreachable island

Island dịch ra là đảo, ốc đảo. Ở đây ám chỉ một khu vực chứa các object liên kết.
Ta có thể khiến một island trở thành unreachable:

```js
family = null;
```

Trong bộ nhớ sẽ như thế này:

![](family-no-family.png)

Ví dụ này chứng minh tầm quan trọng của khả năng tiếp cận như thế nào.

Hiển nhiên rằng John và Ann liên kết với nhau, cả hai đều có tham chiếu incoming. Nhưng chưa đủ.

Object `"family"` chứa cả Ann và john không liên kết đến root, không có tham chiếu incoming nào đến nó, cho nên nó unreachable và sẽ bị xóa.

## Thuật toán trong garbage collection

Thuật toán cơ bản trong garbage collection là  đánh dấu và quét - "mark-and-sweep".

"garbage collection" hoạt động theo các bước:

- Đánh dấu (mark) và ghi nhớ các roots.
- Đánh dấu tất cả các references của roots
- Xem xét và đánh dấu tất cả các tham chiếu đến các objects đã được đánh dấu ở bước 2. Tất cả các object đã được đánh dấu sẽ được ghi nhớ và không xem xét lại trong tương lai.
- ...cứ tiếp tục như thế cho đến khi đánh giá tất cả object (reachable từ roots).
- Tất cả object không được đánh dấu sẽ bị xóa đi.

Minh họa các bước như dưới đây:

![](garbage-collection-1.png)

Ta thấy "unreachable island" nằm bên phải. Giờ xem "mark-and-sweep" của garbage collector xác định nó như thế nào.

Bước một là đánh dấu roots:

![](garbage-collection-2.png)

Tiếp là tham chiếu của root:

![](garbage-collection-3.png)

...Và tham chiếu của các object vừa rồi:

![](garbage-collection-4.png)

Giờ các object không được xem xét (không được đánh dấu) là unreachable và bị xóa:

![](garbage-collection-5.png)

Đó là cách garbage collection hoạt động.

JavaScript engines có nhiều cải tiến để garbage collection hoạt động nhanh, hiệu quả mà không ảnh hưởng đến việc thực thi chương trình của bạn.

Những cải tiến đó là:

- **Generational collection** -- objects được chia làm hai loại: "mới" và "cũ". Many  objects appear, do their job and die fast, they can be cleaned up aggressively. Those that survive for long enough, become "old" and are examined less often.
- **Incremental collection** -- if there are many objects, and we try to walk and mark the whole object set at once, it may take some time and introduce visible delays in the execution. So the engine tries to split the garbage collection into pieces. Then the pieces are executed one by one, separately. That requires some extra bookkeeping between them to track changes, but we have many tiny delays instead of a big one.
- **Idle-time collection** -- the garbage collector tries to run only while the CPU is idle, to reduce the possible effect on the execution.

There are other optimizations and flavours of garbage collection algorithms. As much as I'd like to describe them here, I have to hold off, because different engines implement different tweaks and techniques. And, what's even more important, things change as engines develop, so going deeper "in advance", without a real need is probably not worth that. Unless, of course, it is a matter of pure interest, then there will be some links for you below.

## Summary

The main things to know:

- Garbage collection is performed automatically. We cannot force or prevent it.
- Objects are retained in memory while they are reachable.
- Being referenced is not the same as being reachable (from a root): a pack of interlinked objects can become unreachable as a whole.

Modern engines implement advanced algorithms of garbage collection.

A general book "The Garbage Collection Handbook: The Art of Automatic Memory Management" (R. Jones et al) covers some of them.

If you are familiar with low-level programming, the more detailed information about V8 garbage collector is in the article [A tour of V8: Garbage Collection](http://jayconrod.com/posts/55/a-tour-of-v8-garbage-collection).

[V8 blog](http://v8project.blogspot.com/) also publishes articles about changes in memory management from time to time. Naturally, to learn the garbage collection, you'd better prepare by learning about V8 internals in general and read the blog of [Vyacheslav Egorov](http://mrale.ph) who worked as one of V8 engineers. I'm saying: "V8", because it is best covered with articles in the internet. For other engines, many approaches are similar, but garbage collection differs in many aspects.

In-depth knowledge of engines is good when you need low-level optimizations. It would be wise to plan that as the next step after you're familiar with the language.  
