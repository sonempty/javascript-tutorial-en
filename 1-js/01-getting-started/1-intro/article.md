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

Engines are complicated. But the basics are easy.

1. Engine (embedded if it's a browser) đọc và phân tích code của bạn.
2. Then it converts ("compiles") the script to the machine language.
3. And then the machine code runs, pretty fast.

The engine applies optimizations on every stage of the process. It even watches the compiled script as it runs, analyzes the data that flows through it and applies optimizations to the machine code based on that knowledge. At the end, scripts are quite fast.
```

## What can in-browser JavaScript do?

The modern JavaScript is a "safe" programming language. It does not provide low-level access to memory or CPU, because it was initially created for browsers which do not require it.

The capabilities greatly depend on the environment that runs JavaScript. For instance, [Node.JS](https://wikipedia.org/wiki/Node.js) supports functions that allow JavaScript to read/write arbitrary files, perform network requests etc.

In-browser JavaScript can do everything related to webpage manipulation, interaction with the user and the webserver.

For instance, in-browser JavaScript is able to:

- Add new HTML to the page, change the existing content, modify styles.
- React to user actions, run on mouse clicks, pointer movements, key presses.
- Send requests over the network to remote servers, download and upload files (so-called [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)) and [COMET](https://en.wikipedia.org/wiki/Comet_(programming)) technologies).
- Get and set cookies, ask questions to the visitor, show messages.
- Remember the data on the client-side ("local storage").

## What CAN'T in-browser JavaScript do?

JavaScript's abilities in the browser are limited for the sake of the user's safety. The aim is to prevent an evil webpage from accessing private information or harming the user's data.

The examples of such restrictions are:

- JavaScript on a webpage may not read/write arbitrary files on the hard disk, copy them or execute programs. It has no direct access to OS system functions.

    Modern browsers allow it to work with files, but the access is limited and only provided if the user does certain actions, like "dropping" a file into a browser window or selecting it via an `<input>` tag.

    There are ways to interact with camera/microphone and other devices, but they require a user's explicit permission. So a JavaScript-enabled page may not sneakily enable a web-camera, observe the surroundings and send the information to the [NSA](https://en.wikipedia.org/wiki/National_Security_Agency).
- Different tabs/windows generally do not know about each other. Sometimes they do, for example when one window uses JavaScript to open the other one. But even in this case, JavaScript from one page may not access the other if they come from different sites (from a different domain, protocol or port).

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
