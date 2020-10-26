Các nguyên tắc `SOLID` vẫn thích hợp với ngày nay như nó đã từng trong những năm 90 (và thực sử trước đó). Điều này là do phần mềm đã không thay đổi nhiều trong ngần ấy năm – và đó là bởi vì phần mềm không có thay đổi nhiều kể từ năm 1945 khi Turing đã viết những dòng code đầu tiên cho một máy tính điện tử. Phần mềm vẫn là những câu lệnh `if`, các vòng lặp `while`, và các câu lệnh gán – Chuỗi, Lựa chọn và Lặp (_Sequence_, _Selection_, and _Iteration_).

Mọi thế hệ mới đều thích nghĩ rằng thế giới của họ rất khác so với thế hệ trước. Mọi thế hệ mới đều sai về điều đó; đó là điều mà mọi thế hệ mới đều học được khi thế hệ mới tiếp theo xuất hiện để cho họ biết mọi thứ đã thay đổi nhiều như thế nào. `<grin>`

Vì vậy, hãy cùng tìm hiểu từng nguyên tắc một.

## SRP: The Single Responsibility Princciple

```
Gather together the things that change for the same reasons. Separate things that change for different reasons.
Gộp những thay đổi vì cùng lý do. Tác những thứ thay đổi vì các lý do khác nhau.
```

Thật khó tưởng tượng rằng nguyên tắc này không liên quan đến phần mềm. Chúng ta không trộn điều lệ kinh doanh với GUI code. Chúng ta không trộn truy vấn SQL với các giao thức truyền thông. Chúng ta để tách riêng các code bị thay đổi vì những lý do khác nhau sao cho thay đổi ở một bộ phận không làm hỏng các bộ phận khác. Chúng ta đảm bảo rằng các modules thay đổi vì các lý do khác nhau không phụ thuộc làm rối nhau.

Microservices không giải quyết được vấn đề này. Bạn có thể toạ một microservice lộn xộn, hoặc một tập các microsevies lộn xộn nếu bạn trộn mã thay đổi vì những lý do khác nhau.

Các slide của Dan North hoàn toàn không hiểu vấn đề này và thuyết phục rằng anh ấy không hiểu nguyên tắc nào cả (hoặc rằng anh ấy đang mỉa mai, mà biết Dan thì khả năng này nhiều hơn). Trả lời của anh ấy với SRP là `“Viết code đơn giản”`. Tôi đồng ý. SRP là một trong những cách chúng ta giữ code đơn giản.

## OCP: The Open-Close Principle.

```
A Module should be open for extension but closed for modification.
Một module nên mở cho mở rộng nhưng đóng với việc sửa đổi.
```

Trong tất cả các nguyên tắc, cái ý tưởng rằng bất kỳ ai sẽ thắc mắc nguyên tắc này khiến tôi đầy lo sợ về tương lai của ngành công nghiệp của chúng ta. Tất nhiên chúng ta muốn tạo các mô-đun có thể mở rộng mà không cần sửa đổi chúng. Bạn có thể tưởng tượng làm việc trong một hệ thống không có tính độc lập về thiết bị, nơi mà việc ghi vào tệp đĩa về cơ bản khác với việc ghi vào máy in, màn hình hoặc ống dẫn? Chúng ta có muốn thấy câu lệnh `if` nằm rải rác trong mã của chúng ta để giải quyết tất cả các chi tiết nhỏ không?

Or… Chúng ta muốn tách các khái niệm trừu tượng khỏi các khái niệm chi tiết. Chúng ta muốn để phân tách các quy tắc kinh doanh khỏi các chi tiết khó chịu của GUI, và các giao thức truyền thông cũng như các hành vi bất kỳ tới database? Tất nhiên chúng ta sẽ làm như vậy.

Một lần nữa, các slide của Dan lại sai hoàn toàn. Khi các yêu cầu thay đổi chỉ một phần của mã hiện có bị sai. Phần lớn mã hiện tại vẫn đúng. Và chúng ta muốn đảm bảo rằng chúng ta không phải thay đổi những mã đúng chỉ để làm cho đoạn mã sai hoạt động trở lại. Câu trả lời của Dan là `"Viết mã đơn giản"`. Một lần nữa, tôi đồng ý. Và, trớ trêu thay, anh ấy đã đúng. Mã đơn giản là cả mở và đóng.

## LSP: The Liskov Substitution Principle.

```
A program that uses an interface must not be confused by an implementation of that interface.
Một chương trình sử dụng một giao diện không bị xáo trộn bởi một triển khai của giao diện đó.
```

Mọi người (bao gồm cả tôi) đã sai lầm rằng đây là về kế thừa. Không phải vậy. Nó là về kiểu con – `subtyping`. Tất cả các triển khai của giao diện là các kiểu con của một giao diện. Tất cả các loại vịt đều là kiểu con của một giao diện ngầm. Và mọi người dùng của giao diện cơ sở, dù được khai báo hay ngầm hiểu, phải đồng ý về ý nghĩa của giao diện đó. Nếu một triển khai xáo trộn người dùng của kiểu cơ sở thì câu lệnh `if/switch` sẽ phát sinh.

Nguyên tắc này là để giữ cho các nội dung trừu tượng sắc nét và rõ ràng. Không thể tin rằng đây là một khái niệm lỗi thời.

Các slide của Dan hoàn toàn chính xác về chủ đề này; anh ấy chỉ đơn giản là bỏ lỡ điểm của nguyên tắc. Mã đơn giản là mã duy trì các mối quan hệ kiểu con rõ ràng.

## ISP: The Interface Segregation Principle.

```
Keep interfaces small so that users don’t end up depending on things they don’t need.
Giữ giao diện nhỏ để người dùng không phụ thuộc vào những thứ họ không cần.
```

Chúng tôi vẫn làm việc với các ngôn ngữ đã biên dịch. Chúng tôi vẫn phụ thuộc vào ngày sửa đổi để xác định module nào nên được biên dịch lại và triển khai lại. Vì vậy, miễn là điều này đúng, chúng ta sẽ phải đối mặt với vấn đề rằng khi module A phụ thuộc vào module B tại thời điểm biên dịch, nhưng không phụ thuộc vào thời gian chạy, thì các thay đổi ở module B sẽ buộc phải biên dịch lại và triển khai lại module A.

Vấn đề này đặc biệt nghiêm trọng trong các ngôn ngữ kiểu tĩnh như Java, C #, C ++, GO, Swift, v.v. Các ngôn ngữ kiểu động bị ảnh hưởng ít hơn nhiều; nhưng vẫn không miễn khỏi. Sự tồn tại của Maven và Leiningen là bằng chứng cho điều đó.

Slide của Dan về chủ đề này có thể sai. Khách hàng phụ thuộc vào các phương thức mà họ không gọi, nếu chúng phải được biên dịch lại và triển khai lại khi một trong những phương thức đó được sửa đổi. Điểm cuối cùng của Dan về nguyên tắc này là ổn, cho đến nay. Có, nếu bạn có thể chia một lớp có hai giao diện thành hai lớp riêng biệt, thì bạn nên làm như vậy (SRP). Nhưng sự tách biệt như vậy thường không khả thi, thậm chí là không mong muốn.

## DIP: The Dependency Inversion Principle.

```
Depend in the direction of abstraction. High level modules should not depend upon low level details.
Phụ thuộc theo hướng trìu tượng hoá. Các module cấp cao không nên phụ thuộc và các chi tiết cấp thấp.
```

Khó tưởng tượng rằng một kiến trúc không sử dụng đáng kể nguyên tắc này. Chúng tôi không muốn các quy tắc kinh doanh cấp cao của mình phụ thuộc vào các chi tiết cấp thấp. Tôi hy vọng đó là điều hoàn toàn hiển nhiên. Chúng tôi không muốn các tính toán kiếm tiền cho chúng tôi bị ô nhiễm bởi SQL, hoặc xác thực cấp thấp, hoặc các vấn đề định dạng. Chúng tôi muốn cô lập các chi tiết trừu tượng cấp cao khỏi các chi tiết cấp thấp. Sự tách biệt đó đạt được bằng cách quản lý cẩn thận các phần phụ thuộc trong hệ thống sao cho tất cả các phần phụ thuộc mã nguồn, đặc biệt là những phần vượt qua ranh giới kiến trúc, đều hướng tới sự trừu tượng ở mức cao chứ không phải chi tiết ở mức thấp.

Trong mọi trường hợp, các slide của Dan đều kết thúc bằng: Chỉ cần viết mã đơn giản. Đây là lời khuyên tốt. Tuy nhiên, nếu nhiều năm đã dạy cho chúng ta bất cứ điều gì thì đó là sự đơn giản đòi hỏi các kỷ luật được hướng dẫn bởi các nguyên tắc. Đó là những nguyên tắc xác định sự đơn giản. Chính những nguyên tắc đó đã hạn chế các lập trình viên tạo ra mã nghiêng về tính đơn giản, hồn nhiên.

Cách tốt nhất để tạo ra một mớ hỗn độn phức tạp là nói với mọi người `“hãy đơn giản thôi”` và không hướng dẫn thêm cho họ.
