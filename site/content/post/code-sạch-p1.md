---
title: 'Code sạch, p1'
date: 2019-10-15T16:57:30.317Z
description: 'Code đẹp vừa giúp ích cho mình, cho gia đình và cho xã hội.'
image: /img/20191011_152847.jpg
tags:
  - Development
---
![discuss #1](/img/20191011_152847.jpg "discuss #1")

Sau buổi Discuss đầu tiên với chủ đề `Code sạch`, đánh giá dựa trên tính hiện tại chúng tôi đưa ra các vấn đề sau:

# **Đặt tên biến, tên hàm không có ý nghĩa**

Tên không có ý nghĩa là những tên không mang ý nghĩa của giá trị gán cho nó hay không khơi gợi thông tin về biến đó.

Đặt tên có ý nghĩa giúp code dễ đọc hơn với người khác hoặc với chính mình sau 1 thời gian đọc lại, ngoài ra cắt giảm được phần comment code, phần mà vốn dĩ các LTV đều lười.

Ví dụ, đặt tên biến cho ngày hết hạn:

Tên có ý nghĩa: `expiredAt = datetime.now()`

Tên không có ý nghĩa: `d = datetime.now()`

Việc đặt tên không có ý nghĩa thường xuyên xảy ra, nguyên nhân của vấn đề này thường do:

* Lười, ẩu.
* Không nghĩ ra tên phù hợp, do vốn từ vựng tiếng Anh ít để đặt tên.

Để khác phục vấn đề này, chúng ta có vài phương án như sau:

* Đặt theo hoạt động, ý nghĩa của hàm.
* Đặt tên ở dạng nói được. VD: `create_invoice` thay cho `create_inv`
* Đặt tên để có thể search được. VD nếu chỉ đặt tên là `me` khi search sẽ dễ dính với các từ như time, memory, hoặc đặt 1 ký tự thì khi search càng khó khăn hơn
* Tên hàm chứa động từ, attribute chứa tính từ, ...

Về cấu trúc, có thể dùng kiểu snake case hoặc camel case, tùy theo ngôn ngữ, convention sử dụng: viDuCamelCase, vi_du_snake_case.

Tham khảo:

* <https://dmitripavlutin.com/coding-like-shakespeare-practical-function-naming-conventions/>
* <https://viblo.asia/p/clean-code-chapter-2-dat-ten-co-y-nghia-gGJ59jwrKX2>

# Hàm, file quá dài

Nội dung hàm quá dài thường do chưa nhiều logic xử lý, việc này làm code khó đọc, khó maintain, khó debug khi có lỗi xảy ra.

Nên:

* Mỗi hàm chỉ chứa 1 logic xử lý
* Nếu như logic quá dài tức là vẫn có thể chia thành logic nhỏ hơn
* Hàm chỉ nên dài khoảng 20-30 dòng. Tức là khoảng trong 1 màn hình của 1 màn hình có chiều cao 720px (độ phân dải HD)

Cách nhận biết hàm quá phức tạp, cần phải chia thành hàm con:

* Hàm có nhiều vòng for/if lồng vào nhau. Càng nhiều indenation trong code, code đó càng phức tạp
* Hàm có nhiều dòng trắng. Thông thường để code dễ nhìn giữa các block code thường cách nhau bằng dòng trắng, vì vậy hàm sử dụng nhiều dòng trắng ⇒ có nhiều block ⇒ phức tạp.
* Hàm sử dụng nhiều one-line-solution. Các ngôn ngữ hiện tại có support nhiều phương án viết logic trên 1 dòng. VD `return level4 != null ? GetResources().Where(r => (r.Level2 == (int)level2) && (r.Level3 == (int)level3) && (r.Level4 == (int)level4)).ToList() : level3 != null ? GetResources().Where(r => (r.Level2 == (int)level2) && (r.Level3 == (int)level3)).ToList() : level2 != null ? GetResources().Where(r => (r.Level2 == (int)level2)).ToList() : GetAllResourceList();`. Lạm dụng việc nay sẽ gây quá phức tạp cho việc đọc hiểu, chưa kể việc handle error, exception.

Tham khảo:

* <https://stackoverflow.com/questions/475675/when-is-a-function-too-long>
* <https://stackoverflow.com/questions/611304/how-many-lines-of-code-should-a-function-procedure-method-have>

# Dùng linter theo từng ngôn ngữ

> lint, or a linter, is a tool that analyzes source code to flag programming errors, bugs, stylistic errors, and suspicious constructs

Linter sinh ra để đảm bảo các lập trình viên tuân theo 1 coding style chung. Các Code Editor hoặc IDE đều có tích hợp sẵn, bạn chỉ việc cài và sử dụng. Tùy thuộc ngôn ngữ, dự án sẽ sử dụng các chuẩn riêng. VD:

* Python: PEP8
* JS: eslint

Việc sử dụng lint hay gặp phải các vấn đề sau:

* Developer bypass các rule của linter. Nếu như phải bypass quá nhiều, developer nên liên hệ với người chịu trách nhiệm dự án để bỏ qua rule đó.
* Sử dụng không thống nhất linter. Trong 1 dự án, có những người sử dụng pep8 có người sử dụng flake8, người lại dùng pylint, việc này sẽ gây ra conflict vì các linter sẽ bắt lỗi chồng chéo lên nhau. VD: 2 linter sẽ bắt indent code ở 2 kiểu khác nhau.


```
from Tkinter import (
    Tk, Frame, Button, Entry, Canvas, Text,
    LEFT, DISABLED, NORMAL, RIDGE, END,
)
```

Hoặc

```
from Tkinter import (Tk, Frame, Button, Entry, Canvas, Text,
                     LEFT, DISABLED, NORMAL, RIDGE, END)
```

Do vậy, trong cùng 1 dự án, team nên thống nhất việc sử dụng linter với nhau.

# Magic number

![magic number](/img/untitled.png "magic number")

> A magic number is a direct usage of a number in the code.

Như ví dụ trong đoạn code ở ảnh mình họa bên trên, nếu dùng thẳng `85072278` vào code, nó sẽ được viết như sau:

```
if (pid == "85072278") {
	_reboot()
}
```

Do đó sẽ rất khó theo dõi `85072278` là cái gì, nó ảnh hưởng đến tính dễ đọc của code. Nếu được viết lại với việc bỏ magic number đi:

```
#define LINUX_REBOOT_PID "85072278"
if (pid == LINUX_REBOOT_PID) {
	_reboot()
}
```

Lúc này, trông `85072278`  có ý nghĩa hơn rồi.

Tham khảo:

* <https://stackoverflow.com/questions/47882/what-is-a-magic-number-and-why-is-it-bad>

# Hàm chỉ định rõ arguments

![function argument](/img/untitled-1-.png "function argument")

Việc chỉ định đõ argument cho hàm mang lại các giá trị:

* Việc tra cứu, sử dụng hàm rõ ràng hơn
* Các IDE đều tích hợp auto-completion, auto-suggestion khi sử dụng hàm trong code, ở các tính năng đó, IDE sẽ nói luôn hàm này cần truyền tham số gì, bạn không cần xem lại hàm đó nữa.

# Dùng gì thì import cái đó

Việc import dư thừa không những gây lãng phí tài nguyên (tốn dung lượng ổ cứng, tốn thời gian download - với file JS,...) mà còn có thể gây ra các lỗi không kiểm soát được của những phần code import mà không dùng.

 VD:

* Nếu chỉ dùng vài icon của font-awesome, có thể xem xét dùng ảnh để thay thế cho việc import cả font-awesome vào
* Với CK-editor nếu chỉ dùng bộ editor đơn giản thì bỏ các plugin về quản lý file đi, các phần này rất hay gây ra các lỗi security, khiến bị khai thác, mất kiểm soát máy chủ.

# Dùng i18n

Việc dùng i18n không những kill được vấn đề về Magic number mà còn:

* Dễ dàng tích hợp đa ngôn ngữ
* Việc tìm kiếm, sửa nội dung đoạn text dễ dàng hơn
