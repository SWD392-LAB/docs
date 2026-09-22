# **ĐẶC TẢ USE CASE — HỆ THỐNG AIVES**

### ***(AI-powered Viva Exam System)***

---

## 👥 **1. Danh sách Actor**

| \# | Actor | Loại | Mô tả |
| :---- | :---- | :---- | :---- |
| 1 | Sinh viên | Người dùng chính | Thí sinh tham gia thi vấn đáp |
| 2 | Giảng viên | Người dùng chính | Ra đề, coi thi, đánh giá và duyệt điểm cuối cùng |
| 3 | Quản trị viên | Người dùng chính | Quản lý hệ thống, phân quyền, cấu hình |
| 4 | AI Giám khảo ảo (AI Engine) | Actor phụ (hệ thống) | Sinh câu hỏi hỏi xoáy, hỗ trợ chấm điểm, ghi transcript |
| 5 | Dịch vụ TTS (Text-to-Speech) | Actor phụ (hệ thống) | Chuyển văn bản câu hỏi thành giọng nói |
| 6 | Dịch vụ STT (Speech-to-Text) | Actor phụ (hệ thống) | Chuyển giọng nói của sinh viên thành văn bản theo thời gian gần thực |
| 7 | Hệ thống Đào tạo của trường | Actor phụ (hệ thống) | Tiếp nhận bảng điểm được xuất ra từ AIVES |

---

## 📋 **2. Danh sách Use Case**

| Mã | Tên Use Case | Actor chính | Nhóm |
| :---- | :---- | :---- | :---- |
| UC-00 | Đăng nhập | Sinh viên, Giảng viên, Quản trị viên | Dùng chung |
| UC-01 | Tham gia buổi thi vấn đáp | Sinh viên | Nhóm 1 |
| UC-02 | Trả lời câu hỏi bằng giọng nói | Sinh viên | Nhóm 1 |
| UC-03 | Đọc câu hỏi bằng giọng nói (TTS) | Dịch vụ TTS | Nhóm 1 |
| UC-04 | Chuyển giọng nói sang văn bản (STT) | Dịch vụ STT | Nhóm 1 |
| UC-05 | Sinh câu hỏi hỏi xoáy (adaptive follow-up) | AI Giám khảo ảo | Nhóm 1 |
| UC-06 | Giám sát buổi thi | Giảng viên | Nhóm 1 |
| UC-07 | Ghi transcript buổi thi | AI Giám khảo ảo | Nhóm 1 |
| UC-08 | Xem báo cáo kết quả thi | Sinh viên | Nhóm 2 |
| UC-09 | Duyệt điểm cuối cùng | Giảng viên | Nhóm 2 |
| UC-10 | Hỗ trợ chấm điểm theo rubric | AI Giám khảo ảo | Nhóm 2 |
| UC-11 | Xem thống kê lớp học | Giảng viên | Nhóm 2 |
| UC-12 | Xuất bảng điểm theo mẫu trường | Giảng viên | Nhóm 2 |
| UC-13 | Quản lý tài khoản | Quản trị viên | Nhóm 3 |
| UC-14 | Phân quyền giảng viên & môn học | Quản trị viên | Nhóm 3 |
| UC-15 | Cấu hình ngôn ngữ STT/TTS | Quản trị viên | Nhóm 3 |
| UC-16 | Soạn / sinh câu hỏi | Giảng viên | Nhóm 3 |
| UC-17 | Cấu hình buổi thi | Giảng viên | Nhóm 3 |

---

## 🔍 **3. Đặc tả chi tiết**

### **UC-00 — Đăng nhập**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Sinh viên, Giảng viên, Quản trị viên |
| Mô tả | Người dùng đăng nhập vào hệ thống bằng tài khoản được cấp để truy cập các chức năng tương ứng với vai trò của mình |
| Điều kiện tiên quyết | Người dùng đã có tài khoản hợp lệ trong hệ thống |
| Luồng sự kiện chính | 1\. Người dùng mở trang đăng nhập AIVES. 2\. Người dùng nhập tên đăng nhập và mật khẩu. 3\. Hệ thống xác thực thông tin. 4\. Hệ thống chuyển hướng vào giao diện tương ứng với vai trò (sinh viên/giảng viên/quản trị viên). |
| Luồng rẽ nhánh / ngoại lệ | 3a. Sai tài khoản/mật khẩu → hệ thống hiển thị thông báo lỗi, cho phép nhập lại (tối đa 5 lần trước khi tạm khoá tài khoản). |
| Hậu điều kiện | Người dùng ở trạng thái đã đăng nhập, phiên làm việc (session) được tạo |

---

### **UC-01 — Tham gia buổi thi vấn đáp**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Sinh viên |
| Mô tả | Sinh viên vào phòng thi ảo để bắt đầu phiên thi vấn đáp do AI điều khiển |
| Điều kiện tiên quyết | 1\. Sinh viên đã đăng nhập (UC-00).2\. Buổi thi/ca thi đã được Giảng viên tạo và cấu hình hoàn tất (UC-17).3\. Đến đúng khung giờ thi và thiết bị đạt yêu cầu (micro/camera). |
| Luồng sự kiện chính | 1\. Sinh viên chọn ca thi trong danh sách.2\. Hệ thống kiểm tra điều kiện dự thi (đúng giờ, đúng người).3\. Hệ thống khởi tạo phiên thi và bắt đầu ghi transcript (UC-07).4\. AI Giám khảo ảo đọc câu hỏi đầu tiên thông qua TTS (bao gồm UC-03).5\. Sinh viên trả lời (chuyển sang UC-02). |
| Luồng rẽ nhánh / ngoại lệ | 2a. Sai lịch thi / không đủ điều kiện → hệ thống từ chối và thông báo lý do.3a. Mất kết nối trong lúc khởi tạo → hệ thống cho phép vào lại phiên thi (resume) trong thời gian cho phép. |
| Hậu điều kiện | Phiên thi ở trạng thái "đang diễn ra", đồng hồ đếm thời gian bắt đầu chạy |
| Quan hệ | include UC-03 (Đọc câu hỏi bằng giọng nói); include UC-07 (Ghi transcript buổi thi) |

---

### **UC-02 — Trả lời câu hỏi bằng giọng nói**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Sinh viên |
| Mô tả | Sinh viên trả lời câu hỏi của AI bằng giọng nói trong thời gian giới hạn cho mỗi câu |
| Điều kiện tiên quyết | Đang trong phiên thi (UC-01); câu hỏi hiện tại đã được đọc xong |
| Luồng sự kiện chính | 1\. Hệ thống bắt đầu đếm ngược thời gian trả lời cho câu hỏi hiện tại. 2\. Sinh viên nói câu trả lời. 3\. Hệ thống chuyển giọng nói sang văn bản theo thời gian gần thực (include UC-04). 4\. AI phân tích nội dung câu trả lời. 5\. Nếu câu trả lời còn mơ hồ/thiếu ý/mâu thuẫn và chưa đạt số lượt hỏi xoáy tối đa, AI sinh câu hỏi làm rõ (extend UC-05) và quay lại bước đọc câu hỏi. 6\. Nếu không, hệ thống chuyển sang câu hỏi tiếp theo hoặc kết thúc phiên thi. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Hết thời gian trả lời mà sinh viên chưa trả lời xong → hệ thống tự động dừng ghi âm, ghi nhận là "không trả lời"/"trả lời một phần". 3a. STT không nhận diện được giọng nói (nhiễu, phát âm không rõ) → hệ thống yêu cầu sinh viên nói lại một lần. |
| Hậu điều kiện | Câu trả lời (văn bản \+ bản ghi âm) được lưu vào transcript, gắn với câu hỏi tương ứng |
| Quan hệ | *include* UC-04 (Chuyển giọng nói sang văn bản); *extend* bởi UC-05 (Sinh câu hỏi hỏi xoáy) |

---

### **UC-03 — Đọc câu hỏi bằng giọng nói (TTS)**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Dịch vụ TTS |
| Mô tả | Chuyển nội dung văn bản của câu hỏi (do giảng viên soạn hoặc AI sinh ra) thành giọng nói phát cho sinh viên nghe |
| Điều kiện tiên quyết | Có văn bản câu hỏi cần đọc; đã cấu hình ngôn ngữ đọc (UC-15) |
| Luồng sự kiện chính | 1\. Hệ thống gửi văn bản câu hỏi đến dịch vụ TTS. 2\. Dịch vụ TTS tổng hợp giọng nói theo ngôn ngữ đã cấu hình. 3\. Hệ thống phát âm thanh cho sinh viên. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Dịch vụ TTS không phản hồi/lỗi → hệ thống hiển thị câu hỏi dạng văn bản thay thế và ghi log sự cố. |
| Hậu điều kiện | Câu hỏi đã được truyền đạt tới sinh viên (dạng âm thanh) |

---

### **UC-04 — Chuyển giọng nói sang văn bản (STT)**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Dịch vụ STT |
| Mô tả | Chuyển câu trả lời bằng giọng nói của sinh viên thành văn bản theo thời gian gần thực để AI phân tích |
| Điều kiện tiên quyết | Đang thu âm câu trả lời của sinh viên; đã cấu hình ngôn ngữ nhận diện (UC-15) |
| Luồng sự kiện chính | 1\. Hệ thống truyền luồng âm thanh đến dịch vụ STT theo thời gian thực. 2\. Dịch vụ STT trả về văn bản tương ứng, bao gồm các thuật ngữ chuyên ngành. 3\. Hệ thống hiển thị/lưu văn bản để AI xử lý tiếp. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Độ trễ vượt ngưỡng cho phép → hệ thống cảnh báo nguy cơ ảnh hưởng nhịp vấn đáp tự nhiên (liên quan yêu cầu phi chức năng "độ trễ thấp"). 2b. Nhận diện sai thuật ngữ chuyên ngành → văn bản vẫn được lưu nhưng đánh dấu độ tin cậy thấp để giảng viên đối chiếu khi cần. |
| Hậu điều kiện | Văn bản câu trả lời sẵn sàng để AI sinh câu hỏi hỏi xoáy hoặc chấm điểm |

---

### **UC-05 — Sinh câu hỏi hỏi xoáy (adaptive follow-up)**

| Mục | Nội dung |
| :---- | :---- |
| Actor | AI Giám khảo ảo |
| Mô tả | Dựa trên nội dung câu trả lời vừa nhận được, AI sinh câu hỏi làm rõ/hỏi xoáy giống cách giảng viên hỏi thêm khi câu trả lời còn mơ hồ, thiếu ý hoặc mâu thuẫn. Đây là chức năng thể hiện rõ nhất "trí tuệ" của hệ thống |
| Điều kiện tiên quyết | Đã có văn bản câu trả lời (UC-04); số lượt hỏi xoáy cho câu hỏi hiện tại chưa đạt giới hạn tối đa đã cấu hình (UC-17) |
| Luồng sự kiện chính | 1\. AI phân tích văn bản câu trả lời để phát hiện điểm mơ hồ, thiếu ý hoặc mâu thuẫn. 2\. AI sinh một câu hỏi làm rõ phù hợp ngữ cảnh. 3\. Câu hỏi mới được chuyển cho TTS đọc lại cho sinh viên (UC-03). 4\. Hệ thống tăng bộ đếm số lượt hỏi xoáy của câu hỏi hiện tại. |
| Luồng rẽ nhánh / ngoại lệ | 1a. Câu trả lời đã đầy đủ, rõ ràng → AI quyết định không hỏi xoáy, chuyển sang câu hỏi kế tiếp. 4a. Đã đạt số lượt hỏi xoáy tối đa → hệ thống buộc chuyển sang câu hỏi tiếp theo dù câu trả lời chưa hoàn chỉnh. |
| Hậu điều kiện | Câu hỏi hỏi xoáy (nếu có) được thêm vào transcript của phiên thi |
| Quan hệ | *extend* UC-02 (Trả lời câu hỏi bằng giọng nói) |

---

### **UC-06 — Giám sát buổi thi**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Giảng viên |
| Mô tả | Giảng viên theo dõi trực tiếp diễn biến buổi thi vấn đáp do AI điều khiển, có thể can thiệp khi cần |
| Điều kiện tiên quyết | Giảng viên đã đăng nhập; buổi thi đang diễn ra |
| Luồng sự kiện chính | 1\. Giảng viên mở màn hình giám sát của một hoặc nhiều phòng thi. 2\. Hệ thống hiển thị theo thời gian thực: câu hỏi hiện tại, văn bản câu trả lời, thời gian còn lại. 3\. Giảng viên có thể tạm dừng/kết thúc sớm phiên thi nếu cần. |
| Luồng rẽ nhánh / ngoại lệ | 3a. Giảng viên can thiệp dừng thi → hệ thống ghi lý do can thiệp vào transcript. |
| Hậu điều kiện | Giảng viên nắm được tình trạng buổi thi; hành động can thiệp (nếu có) được ghi log |

---

### **UC-07 — Ghi transcript buổi thi**

| Mục | Nội dung |
| :---- | :---- |
| Actor | AI Giám khảo ảo |
| Mô tả | Lưu vết toàn bộ quá trình thi (câu hỏi, câu trả lời, câu hỏi xoáy, thời gian, điểm gợi ý) làm bằng chứng khách quan khi có khiếu nại điểm |
| Điều kiện tiên quyết | Phiên thi đã bắt đầu (UC-01) |
| Luồng sự kiện chính | 1\. Với mỗi câu hỏi/câu trả lời/sự kiện trong phiên thi, hệ thống ghi lại nội dung, mốc thời gian và người/thực thể liên quan. 2\. Dữ liệu được lưu trữ an toàn, gắn với mã phiên thi. 3\. Khi kết thúc phiên thi, transcript được đóng và không thể chỉnh sửa. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Sự cố lưu trữ → hệ thống lưu tạm cục bộ và đồng bộ lại khi kết nối phục hồi. |
| Hậu điều kiện | Transcript đầy đủ, bất biến (immutable) của phiên thi được lưu trữ, phục vụ tra cứu và giải quyết khiếu nại |

---

### **UC-08 — Xem báo cáo kết quả thi**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Sinh viên |
| Mô tả | Sinh viên xem lại kết quả sau khi thi: điểm từng câu, nhận xét của AI |
| Điều kiện tiên quyết | Buổi thi đã kết thúc; điểm đã được giảng viên duyệt (UC-09) |
| Luồng sự kiện chính | 1\. Sinh viên vào mục "Kết quả thi". 2\. Hệ thống hiển thị điểm từng câu hỏi, nhận xét của AI cho từng câu. 3\. Sinh viên có thể xem lại transcript câu hỏi/câu trả lời tương ứng. |
| Luồng rẽ nhánh / ngoại lệ | 1a. Điểm chưa được giảng viên duyệt → hệ thống hiển thị trạng thái "đang chờ duyệt điểm", chưa cho xem điểm chi tiết. |
| Hậu điều kiện | Sinh viên nắm được kết quả thi |

---

### **UC-09 — Duyệt điểm cuối cùng**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Giảng viên |
| Mô tả | Giảng viên xem điểm gợi ý của AI cho từng câu trả lời, có thể điều chỉnh và là người quyết định điểm số cuối cùng — đảm bảo yêu cầu "quyền quyết định thuộc về con người" |
| Điều kiện tiên quyết | Buổi thi đã kết thúc; AI đã đưa ra gợi ý chấm điểm theo rubric (UC-10) |
| Luồng sự kiện chính | 1\. Giảng viên mở danh sách bài thi cần duyệt. 2\. Hệ thống hiển thị điểm gợi ý của AI theo từng tiêu chí rubric, kèm transcript liên quan. 3\. Giảng viên xem xét, có thể chỉnh sửa điểm từng câu. 4\. Giảng viên xác nhận duyệt điểm cuối cùng. |
| Luồng rẽ nhánh / ngoại lệ | 3a. Giảng viên không đồng ý với gợi ý AI → nhập điểm khác và ghi chú lý do (phục vụ minh bạch khi có khiếu nại). |
| Hậu điều kiện | Điểm chính thức được ghi nhận, sinh viên có thể xem báo cáo (UC-08) |
| Quan hệ | *include* UC-10 (Hỗ trợ chấm điểm theo rubric) |

---

### **UC-10 — Hỗ trợ chấm điểm theo rubric**

| Mục | Nội dung |
| :---- | :---- |
| Actor | AI Giám khảo ảo |
| Mô tả | AI phân tích transcript và đề xuất điểm số cho từng câu trả lời dựa trên rubric do giảng viên thiết lập, chỉ mang tính tham khảo |
| Điều kiện tiên quyết | Transcript buổi thi đã hoàn tất (UC-07); rubric chấm điểm đã được thiết lập |
| Luồng sự kiện chính | 1\. Hệ thống đối chiếu từng câu trả lời với các tiêu chí trong rubric. 2\. AI tính điểm gợi ý và sinh nhận xét cho từng câu. 3\. Kết quả gợi ý được chuyển cho giảng viên duyệt (UC-09). |
| Luồng rẽ nhánh / ngoại lệ | 1a. Câu trả lời thiếu dữ liệu (do sự cố STT) → AI đánh dấu "không đủ dữ liệu để chấm tự động", đề nghị giảng viên nghe lại bản ghi âm gốc. |
| Hậu điều kiện | Điểm gợi ý và nhận xét theo từng câu sẵn sàng để giảng viên duyệt |

---

### **UC-11 — Xem thống kê lớp học**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Giảng viên |
| Mô tả | Giảng viên xem thống kê toàn lớp: câu hỏi khó nhất, tỷ lệ trả lời tốt, phân bố điểm |
| Điều kiện tiên quyết | Đã có ít nhất một buổi thi của lớp/môn học đã hoàn tất và được duyệt điểm |
| Luồng sự kiện chính | 1\. Giảng viên chọn lớp/môn học cần xem thống kê. 2\. Hệ thống tổng hợp và hiển thị: phân bố điểm, câu hỏi có tỷ lệ trả lời kém nhất, tỷ lệ sinh viên bị hỏi xoáy nhiều. 3\. Giảng viên có thể lọc theo tiêu chí (ca thi, nhóm câu hỏi...). |
| Luồng rẽ nhánh / ngoại lệ | 1a. Chưa đủ dữ liệu (chưa buổi thi nào hoàn tất) → hệ thống thông báo chưa có dữ liệu thống kê. |
| Hậu điều kiện | Giảng viên có cái nhìn tổng quan để cải thiện ngân hàng câu hỏi/đề thi |

---

### **UC-12 — Xuất bảng điểm theo mẫu trường**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Giảng viên |
| Mô tả | Xuất bảng điểm của lớp/môn học theo đúng mẫu quy định của trường để nộp cho Hệ thống Đào tạo |
| Điều kiện tiên quyết | Toàn bộ điểm của lớp/ca thi đã được duyệt (UC-09) |
| Luồng sự kiện chính | 1\. Giảng viên chọn lớp/môn học và mẫu bảng điểm cần xuất. 2\. Hệ thống tổng hợp điểm đã duyệt vào đúng định dạng mẫu. 3\. Hệ thống xuất file và/hoặc gửi trực tiếp tới Hệ thống Đào tạo của trường. |
| Luồng rẽ nhánh / ngoại lệ | 1a. Còn sinh viên chưa được duyệt điểm → hệ thống cảnh báo danh sách thiếu trước khi xuất. |
| Hậu điều kiện | Bảng điểm đúng mẫu được tạo ra và/hoặc chuyển tới Hệ thống Đào tạo |

---

### **UC-13 — Quản lý tài khoản**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Quản trị viên |
| Mô tả | Tạo mới, chỉnh sửa, khoá/mở khoá tài khoản của giảng viên và sinh viên |
| Điều kiện tiên quyết | Quản trị viên đã đăng nhập |
| Luồng sự kiện chính | 1\. Quản trị viên chọn chức năng quản lý tài khoản. 2\. Quản trị viên tạo mới/chỉnh sửa/khoá tài khoản. 3\. Hệ thống cập nhật và (nếu tạo mới) gửi thông tin đăng nhập cho người dùng. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Tài khoản/email đã tồn tại → hệ thống báo lỗi trùng lặp. |
| Hậu điều kiện | Danh sách tài khoản được cập nhật |

---

### **UC-14 — Phân quyền giảng viên & môn học**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Quản trị viên |
| Mô tả | Gán giảng viên phụ trách cho từng môn học/lớp học phần, quy định phạm vi dữ liệu giảng viên được truy cập |
| Điều kiện tiên quyết | Tài khoản giảng viên và danh mục môn học đã tồn tại trong hệ thống |
| Luồng sự kiện chính | 1\. Quản trị viên chọn môn học/lớp học phần. 2\. Quản trị viên gán giảng viên phụ trách. 3\. Hệ thống cập nhật quyền truy cập tương ứng cho giảng viên đó. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Giảng viên đã được gán ở lớp khác trùng lịch → hệ thống cảnh báo xung đột lịch. |
| Hậu điều kiện | Giảng viên chỉ truy cập được dữ liệu của môn học/lớp được phân công |

---

### **UC-15 — Cấu hình ngôn ngữ STT/TTS**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Quản trị viên |
| Mô tả | Thiết lập ngôn ngữ (Việt/Anh) áp dụng cho việc đọc câu hỏi (TTS) và nhận diện câu trả lời (STT) theo môn học/lớp thi |
| Điều kiện tiên quyết | Quản trị viên đã đăng nhập |
| Luồng sự kiện chính | 1\. Quản trị viên chọn môn học/lớp thi cần cấu hình. 2\. Quản trị viên chọn ngôn ngữ áp dụng cho STT và TTS. 3\. Hệ thống lưu cấu hình, áp dụng cho các buổi thi liên quan. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Ngôn ngữ chọn chưa được hỗ trợ bởi dịch vụ STT/TTS hiện tại → hệ thống thông báo và giữ nguyên cấu hình cũ. |
| Hậu điều kiện | Các phiên thi mới của môn học/lớp áp dụng đúng ngôn ngữ đã cấu hình |

---

### **UC-16 — Soạn / sinh câu hỏi**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Giảng viên |
| Mô tả | Giảng viên tự soạn câu hỏi hoặc yêu cầu hệ thống hỗ trợ sinh câu hỏi cho ngân hàng đề thi vấn đáp |
| Điều kiện tiên quyết | Giảng viên đã đăng nhập và được phân quyền môn học tương ứng (UC-14) |
| Luồng sự kiện chính | 1\. Giảng viên chọn môn học và chủ đề câu hỏi. 2\. Giảng viên nhập câu hỏi thủ công hoặc yêu cầu hệ thống gợi ý sinh câu hỏi. 3\. Giảng viên xem, chỉnh sửa và lưu vào ngân hàng câu hỏi. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Câu hỏi do hệ thống gợi ý không phù hợp → giảng viên chỉnh sửa hoặc loại bỏ trước khi lưu. |
| Hậu điều kiện | Ngân hàng câu hỏi của môn học được cập nhật, sẵn sàng sử dụng cho các buổi thi (UC-01) |

---

### **UC-17 — Cấu hình buổi thi**

| Mục | Nội dung |
| :---- | :---- |
| Actor | Giảng viên |
| Mô tả | Thiết lập các tham số cho một buổi/ca thi: giới hạn thời gian trả lời mỗi câu, số lượt hỏi xoáy tối đa, ngân hàng câu hỏi sử dụng, rubric chấm điểm |
| Điều kiện tiên quyết | Đã có ngân hàng câu hỏi (UC-16); giảng viên được phân quyền môn học (UC-14) |
| Luồng sự kiện chính | 1\. Giảng viên tạo ca thi mới, chọn danh sách sinh viên tham gia. 2\. Giảng viên thiết lập: thời gian trả lời tối đa/câu, số lượt hỏi xoáy tối đa/câu, ngân hàng câu hỏi, rubric chấm điểm. 3\. Hệ thống lưu cấu hình và lên lịch ca thi. |
| Luồng rẽ nhánh / ngoại lệ | 2a. Thông số nhập không hợp lệ (ví dụ thời gian ≤ 0\) → hệ thống báo lỗi, yêu cầu nhập lại. |
| Hậu điều kiện | Ca thi sẵn sàng để sinh viên tham gia đúng theo cấu hình (áp dụng trong UC-01, UC-02, UC-05) |

---

# **USE CASE SPECIFICATION — AIVES**

### ***(AI-powered Viva Exam System)***

---

## 👥 **1. Actor List**

| \# | Actor | Type | Description |
| :---- | :---- | :---- | :---- |
| 1 | Student | Primary actor | Examinee taking the oral exam |
| 2 | Lecturer | Primary actor | Sets questions, proctors exams, evaluates and approves final scores |
| 3 | Administrator | Primary actor | Manages the system, permissions, and configuration |
| 4 | AI Virtual Examiner (AI Engine) | Secondary actor (system) | Generates follow-up questions, supports scoring, logs the transcript |
| 5 | TTS Service (Text-to-Speech) | Secondary actor (system) | Converts question text into speech |
| 6 | STT Service (Speech-to-Text) | Secondary actor (system) | Converts the student's spoken answer into text in near real-time |
| 7 | Academic Affairs System | Secondary actor (system) | Receives the grade sheet exported from AIVES |

---

## 📋 **2. Use Case List**

| ID | Use Case Name | Primary Actor | Group |
| :---- | :---- | :---- | :---- |
| UC-00 | Log in | Student, Lecturer, Administrator | Shared |
| UC-01 | Join oral exam session | Student | Group 1 |
| UC-02 | Answer question by voice | Student | Group 1 |
| UC-03 | Read question aloud (TTS) | TTS Service | Group 1 |
| UC-04 | Convert speech to text (STT) | STT Service | Group 1 |
| UC-05 | Generate adaptive follow-up question | AI Virtual Examiner | Group 1 |
| UC-06 | Monitor exam session | Lecturer | Group 1 |
| UC-07 | Log exam transcript | AI Virtual Examiner | Group 1 |
| UC-08 | View exam report | Student | Group 2 |
| UC-09 | Approve final score | Lecturer | Group 2 |
| UC-10 | Support scoring based on rubric | AI Virtual Examiner | Group 2 |
| UC-11 | View class statistics | Lecturer | Group 2 |
| UC-12 | Export grade sheet (school template) | Lecturer | Group 2 |
| UC-13 | Manage user accounts | Administrator | Group 3 |
| UC-14 | Assign lecturer / course roles | Administrator | Group 3 |
| UC-15 | Configure STT/TTS language | Administrator | Group 3 |
| UC-16 | Create / generate questions | Lecturer | Group 3 |
| UC-17 | Configure exam session settings | Lecturer | Group 3 |

---

## 🔍 **3. Detailed Specifications**

### **UC-00 — Log in**

| Field | Content |
| :---- | :---- |
| Actor | Student, Lecturer, Administrator |
| Description | The user logs into the system with an assigned account to access the functions corresponding to their role |
| Preconditions | The user already has a valid account in the system |
| Main Flow | 1\. The user opens the AIVES login page. 2\. The user enters username and password. 3\. The system authenticates the credentials. 4\. The system redirects the user to the interface matching their role (student/lecturer/administrator). |
| Alternative / Exception Flows | 3a. Incorrect username/password → the system shows an error message and allows re-entry (up to 5 attempts before the account is temporarily locked). |
| Postconditions | The user is in a logged-in state; a session is created |

---

### **UC-01 — Join oral exam session**

| Field | Content |
| :---- | :---- |
| Actor | Student |
| Description | The student enters the virtual exam room to start an AI-driven oral exam session |
| Preconditions | 1\. The student has successfully logged in (UC-00).2\. The exam session has been fully configured and scheduled by the lecturer (UC-17).3\. The scheduled exam time slot has arrived, and the student's device has a working microphone. |
| Main Flow | 1\. The student selects the exam session from the list.2\. The system verifies eligibility (correct time, correct identity).3\. The system initializes the exam session and starts logging the transcript (UC-07).4\. The AI Virtual Examiner reads the first question aloud via TTS (includes UC-03).5\. The student answers (proceeds to UC-02). |
| Alternative / Exception Flows | 2a. Wrong schedule / not eligible → the system rejects entry and shows the reason.3a. Connection lost during initialization → the system allows the student to resume the session within the allowed time. |
| Postconditions | The exam session is in "in progress" state; the countdown timer starts |
| Relationships | include UC-03 (Read question aloud); include UC-07 (Log exam transcript) |

---

### **UC-02 — Answer question by voice**

| Field | Content |
| :---- | :---- |
| Actor | Student |
| Description | The student answers the AI's question by voice within the time limit set for each question |
| Preconditions | The student is in an active exam session (UC-01); the current question has finished being read aloud |
| Main Flow | 1\. The system starts the countdown for the answer time of the current question. 2\. The student speaks the answer. 3\. The system converts speech to text in near real-time (includes UC-04). 4\. The AI analyzes the content of the answer. 5\. If the answer is still vague/incomplete/contradictory and the maximum number of follow-ups has not been reached, the AI generates a clarifying question (extends UC-05) and returns to the question-reading step. 6\. Otherwise, the system moves on to the next question or ends the session. |
| Alternative / Exception Flows | 2a. Time runs out before the student finishes answering → the system automatically stops recording and marks the answer as "no answer" / "partial answer". 3a. STT fails to recognize the speech (noise, unclear pronunciation) → the system asks the student to repeat once. |
| Postconditions | The answer (text \+ audio recording) is saved to the transcript, linked to the corresponding question |
| Relationships | *include* UC-04 (Convert speech to text); *extended by* UC-05 (Generate adaptive follow-up question) |

---

### **UC-03 — Read question aloud (TTS)**

| Field | Content |
| :---- | :---- |
| Actor | TTS Service |
| Description | Converts the text content of a question (either written by the lecturer or generated by the AI) into speech played back to the student |
| Preconditions | The question text is available; the reading language has been configured (UC-15) |
| Main Flow | 1\. The system sends the question text to the TTS service. 2\. The TTS service synthesizes speech in the configured language. 3\. The system plays the audio for the student. |
| Alternative / Exception Flows | 2a. The TTS service is unresponsive/fails → the system displays the question as text instead and logs the incident. |
| Postconditions | The question has been conveyed to the student (as audio) |

---

### **UC-04 — Convert speech to text (STT)**

| Field | Content |
| :---- | :---- |
| Actor | STT Service |
| Description | Converts the student's spoken answer into text in near real-time so the AI can analyze it |
| Preconditions | The student's answer is currently being recorded; the recognition language has been configured (UC-15) |
| Main Flow | 1\. The system streams the audio to the STT service in real time. 2\. The STT service returns the corresponding text, including domain-specific terminology. 3\. The system displays/stores the text for further AI processing. |
| Alternative / Exception Flows | 2a. Latency exceeds the allowed threshold → the system flags a risk to the natural pace of the exam (related to the "low latency" non-functional requirement). 2b. Domain-specific terms are misrecognized → the text is still saved but flagged as low-confidence for the lecturer to cross-check if needed. |
| Postconditions | The answer text is ready for the AI to generate a follow-up question or scoring |

---

### **UC-05 — Generate adaptive follow-up question**

| Field | Content |
| :---- | :---- |
| Actor | AI Virtual Examiner |
| Description | Based on the content of the answer just received, the AI generates a clarifying/probing question, the same way a lecturer would ask further when an answer is vague, incomplete, or contradictory. This is the function that most clearly demonstrates the system's "intelligence" |
| Preconditions | The answer text is available (UC-04); the maximum number of follow-ups configured for the current question (UC-17) has not yet been reached |
| Main Flow | 1\. The AI analyzes the answer text to detect vagueness, missing points, or contradictions. 2\. The AI generates a context-appropriate clarifying question. 3\. The new question is sent to TTS to be read aloud to the student (UC-03). 4\. The system increments the follow-up counter for the current question. |
| Alternative / Exception Flows | 1a. The answer is already complete and clear → the AI decides not to ask a follow-up and moves to the next question. 4a. The maximum number of follow-ups has been reached → the system forces a move to the next question even if the answer is still incomplete. |
| Postconditions | The follow-up question (if any) is added to the exam session transcript |
| Relationships | *extends* UC-02 (Answer question by voice) |

---

### **UC-06 — Monitor exam session**

| Field | Content |
| :---- | :---- |
| Actor | Lecturer |
| Description | The lecturer observes the progress of an AI-driven oral exam session in real time and can intervene when necessary |
| Preconditions | The lecturer has logged in; the exam session is in progress |
| Main Flow | 1\. The lecturer opens the monitoring screen for one or more exam rooms. 2\. The system displays, in real time: the current question, the answer text, and the remaining time. 3\. The lecturer may pause/end the session early if needed. |
| Alternative / Exception Flows | 3a. The lecturer intervenes to stop the exam → the system logs the reason for the intervention in the transcript. |
| Postconditions | The lecturer is aware of the exam's status; any intervention (if any) is logged |

---

### **UC-07 — Log exam transcript**

| Field | Content |
| :---- | :---- |
| Actor | AI Virtual Examiner |
| Description | Records the entire exam process (questions, answers, follow-up questions, timing, suggested scores) as objective evidence in case of a grade appeal |
| Preconditions | The exam session has started (UC-01) |
| Main Flow | 1\. For every question/answer/event during the session, the system records the content, timestamp, and related entity. 2\. The data is stored securely, linked to the session ID. 3\. When the session ends, the transcript is finalized and becomes immutable. |
| Alternative / Exception Flows | 2a. A storage failure occurs → the system saves data locally as a buffer and syncs it once the connection is restored. |
| Postconditions | A complete, immutable transcript of the exam session is stored, supporting lookup and grade-appeal resolution |

---

### **UC-08 — View exam report**

| Field | Content |
| :---- | :---- |
| Actor | Student |
| Description | The student reviews the exam results afterward: score per question and the AI's comments |
| Preconditions | The exam session has ended; the score has been approved by the lecturer (UC-09) |
| Main Flow | 1\. The student goes to the "Exam Results" section. 2\. The system displays the score for each question and the AI's comments for each one. 3\. The student may review the transcript of the corresponding question/answer. |
| Alternative / Exception Flows | 1a. The score has not yet been approved by the lecturer → the system shows a "pending approval" status and does not yet display detailed scores. |
| Postconditions | The student knows their exam results |

---

### **UC-09 — Approve final score**

| Field | Content |
| :---- | :---- |
| Actor | Lecturer |
| Description | The lecturer reviews the AI's suggested score for each answer, may adjust it, and is the one who makes the final scoring decision — ensuring the "human decision authority" requirement |
| Preconditions | The exam session has ended; the AI has produced a rubric-based scoring suggestion (UC-10) |
| Main Flow | 1\. The lecturer opens the list of exams to review. 2\. The system displays the AI's suggested score per rubric criterion, along with the relevant transcript. 3\. The lecturer reviews and may edit the score for each question. 4\. The lecturer confirms and approves the final score. |
| Alternative / Exception Flows | 3a. The lecturer disagrees with the AI's suggestion → enters a different score and notes the reason (for transparency in case of appeal). |
| Postconditions | The official score is recorded; the student can view the report (UC-08) |
| Relationships | *include* UC-10 (Support scoring based on rubric) |

---

### **UC-10 — Support scoring based on rubric**

| Field | Content |
| :---- | :---- |
| Actor | AI Virtual Examiner |
| Description | The AI analyzes the transcript and proposes a score for each answer based on the rubric set by the lecturer; this is for reference only |
| Preconditions | The exam transcript is complete (UC-07); the scoring rubric has been set up |
| Main Flow | 1\. The system compares each answer against the rubric criteria. 2\. The AI calculates a suggested score and generates comments for each question. 3\. The suggested results are forwarded to the lecturer for approval (UC-09). |
| Alternative / Exception Flows | 1a. An answer is missing data (due to an STT failure) → the AI flags it as "insufficient data for automatic scoring" and recommends the lecturer listen to the original recording. |
| Postconditions | Suggested scores and comments per question are ready for the lecturer's approval |

---

### **UC-11 — View class statistics**

| Field | Content |
| :---- | :---- |
| Actor | Lecturer |
| Description | The lecturer views class-wide statistics: hardest questions, good-answer rate, score distribution |
| Preconditions | At least one exam session of the class/course has been completed and its scores approved |
| Main Flow | 1\. The lecturer selects the class/course to view statistics for. 2\. The system aggregates and displays: score distribution, questions with the lowest answer-quality rate, the rate of students receiving multiple follow-ups. 3\. The lecturer may filter by criteria (exam session, question group...). |
| Alternative / Exception Flows | 1a. Not enough data (no session completed yet) → the system reports that no statistics are available. |
| Postconditions | The lecturer gains an overview to improve the question bank/exam design |

---

### **UC-12 — Export grade sheet (school template)**

| Field | Content |
| :---- | :---- |
| Actor | Lecturer |
| Description | Exports the class/course grade sheet in the format required by the school, for submission to the Academic Affairs System |
| Preconditions | All scores for the class/session have been approved (UC-09) |
| Main Flow | 1\. The lecturer selects the class/course and the grade sheet template to export. 2\. The system compiles the approved scores into the exact template format. 3\. The system exports the file and/or sends it directly to the school's Academic Affairs System. |
| Alternative / Exception Flows | 1a. Some students' scores are not yet approved → the system warns about the missing list before exporting. |
| Postconditions | A correctly formatted grade sheet is produced and/or transferred to the Academic Affairs System |

---

### **UC-13 — Manage user accounts**

| Field | Content |
| :---- | :---- |
| Actor | Administrator |
| Description | Create, edit, lock/unlock lecturer and student accounts |
| Preconditions | The administrator has logged in |
| Main Flow | 1\. The administrator opens the account management function. 2\. The administrator creates/edits/locks an account. 3\. The system updates the record and (if newly created) sends login credentials to the user. |
| Alternative / Exception Flows | 2a. The account/email already exists → the system shows a duplicate error. |
| Postconditions | The account list is updated |

---

### **UC-14 — Assign lecturer / course roles**

| Field | Content |
| :---- | :---- |
| Actor | Administrator |
| Description | Assigns a lecturer to a course/class, defining the scope of data that lecturer can access |
| Preconditions | Lecturer accounts and the course catalog already exist in the system |
| Main Flow | 1\. The administrator selects a course/class. 2\. The administrator assigns the responsible lecturer. 3\. The system updates the corresponding access permissions for that lecturer. |
| Alternative / Exception Flows | 2a. The lecturer is already assigned to another class with a conflicting schedule → the system warns of a scheduling conflict. |
| Postconditions | The lecturer can only access data for the assigned course/class |

---

### **UC-15 — Configure STT/TTS language**

| Field | Content |
| :---- | :---- |
| Actor | Administrator |
| Description | Sets the language (Vietnamese/English) used for reading questions aloud (TTS) and recognizing answers (STT), per course/exam session |
| Preconditions | The administrator has logged in |
| Main Flow | 1\. The administrator selects the course/exam session to configure. 2\. The administrator selects the language to apply for STT and TTS. 3\. The system saves the configuration and applies it to the related exam sessions. |
| Alternative / Exception Flows | 2a. The selected language is not yet supported by the current STT/TTS service → the system shows a notice and keeps the previous configuration. |
| Postconditions | New exam sessions for the course/class use the configured language |

---

### **UC-16 — Create / generate questions**

| Field | Content |
| :---- | :---- |
| Actor | Lecturer |
| Description | The lecturer writes questions manually or requests system-assisted question generation for the oral exam question bank |
| Preconditions | The lecturer has logged in and been assigned to the corresponding course (UC-14) |
| Main Flow | 1\. The lecturer selects the course and question topic. 2\. The lecturer enters a question manually or requests the system to suggest a generated question. 3\. The lecturer reviews, edits, and saves it to the question bank. |
| Alternative / Exception Flows | 2a. The system-suggested question is not suitable → the lecturer edits or discards it before saving. |
| Postconditions | The course's question bank is updated and ready to be used in exam sessions (UC-01) |

---

### **UC-17 — Configure exam session settings**

| Field | Content |
| :---- | :---- |
| Actor | Lecturer |
| Description | Sets the parameters for an exam session: maximum answer time per question, maximum number of follow-ups, question bank used, and scoring rubric |
| Preconditions | A question bank already exists (UC-16); the lecturer is assigned to the course (UC-14) |
| Main Flow | 1\. The lecturer creates a new exam session and selects the participating students. 2\. The lecturer configures: maximum answer time per question, maximum follow-ups per question, question bank, and scoring rubric. 3\. The system saves the configuration and schedules the session. |
| Alternative / Exception Flows | 2a. Invalid input (e.g. time ≤ 0\) → the system shows an error and asks for re-entry. |
| Postconditions | The exam session is ready for students to join according to the configuration (applied in UC-01, UC-02, UC-05) |

---


**UC-01** Join oral exam session — *include* → **UC-03** Read question aloud (TTS)

**UC-01** Join oral exam session — *include* → **UC-07** Log exam transcript

**UC-02** Answer question by voice — *include* → **UC-04** Convert speech to text (STT)

**UC-02** Answer question by voice — *extended by* **UC-05** Generate adaptive follow-up question

**UC-05** Generate adaptive follow-up question — *extends* → **UC-02** Answer question by voice

**UC-09** Approve final score — *include* → **UC-10** Support scoring based on rubric

