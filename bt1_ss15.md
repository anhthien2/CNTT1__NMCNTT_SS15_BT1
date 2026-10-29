# PHẦN 1: PHÂN TÍCH - 3 HẬU QUẢ NAM ĐANG GẶP

**1. Mất dữ liệu vĩnh viễn do ghi đè - Lỗi Ctrl+S chí mạng:**  
Nam dùng kiểu lưu `v1, v2, final`. Khi bấm Ctrl+S đè lên file `final`, toàn bộ code cũ bị xóa sạch khỏi ổ cứng. Vì file chỉ nằm local `D:\Project\`, không có thùng rác phiên bản, nên không thể Undo. Đây chính là điểm yếu của lưu trữ truyền thống.

**2. Đơn điểm lỗi - Single Point of Failure:**  
Nam nói "file chỉ có trên máy em". Nếu máy hỏng, mất trộm, dính virus mã hóa thì cả dự án Smart Food chết theo. Không có bản sao lưu trên Cloud.

**3. Hỗn loạn phiên bản & không thể làm nhóm:**  
Gửi file qua Zalo `main_v1.py, main_v2_final.py, main_v2_final_THAT.py` khiến cả nhóm không biết đâu là bản mới nhất. Không có Version History, không thể xem ai sửa cái gì, không thể quay lại 1-click. Zalo còn tự nén và xóa file sau 1 thời gian.


# PHẦN 2: SỬA LỖI - QUY TRÌNH HYBRID WORKFLOW CHO NAM

Mục tiêu: Vẫn code nhanh trên máy cá nhân, nhưng mọi thứ tự động được backup và có lịch sử phiên bản.

**Quy trình 3 bước thiết lập:**

**Bước 1: Tạo kho lưu trữ đám mây có Version History**

-   Tạo 1 thư mục `D:\Project\` và đồng bộ nó với Google Drive / OneDrive / Dropbox bằng app Drive for Desktop.
-   Bật tính năng Delta Sync: Từ nay mỗi lần Ctrl+S, nó chỉ tải phần code thay đổi lên Cloud, không chậm máy.

**Bước 2: Dùng Git - Vũ khí xịn cho dân code[ Quan trọng nhất ]**  
Đây mới là cách để khôi phục 1-click mà đề bài yêu cầu.

1.  Trong VS Code, mở thư mục `D:\Project\` -> `Terminal -> git init`
2.  Tạo repo private trên GitHub tên `smart-food`
3.  Liên kết: `git remote add origin link-github`
4.  Thói quen mới thay vì Ctrl+S + gửi Zalo:
    -   Code xong 1 tính năng -> `Ctrl+S` -> `git add .` -> `git commit -m "xong chức năng đăng nhập"`
    -   `git push` -> Cả nhóm thấy ngay, không cần Zalo.

**Bước 3: Cách khôi phục khi lại lỡ tay xóa như tối qua**  
Chỉ cần 1-click, không hoảng loạn:

-   **Cách 1 (Google Drive):** Chuột phải vào file `code_final.py` trên Drive -> **Manage versions / Lịch sử phiên bản** -> Chọn phiên bản 1 tiếng trước -> **Restore**.
-   **Cách 2 (GitHub - Chuyên nghiệp):** Trên VS Code -> Tab Source Control -> Xem History -> Click vào commit trước đó -> **Restore**. Đoạn code bị xóa sẽ quay lại ngay lập tức.

**Kết quả:** Từ nay Nam không cần đặt tên `final_final` nữa. Máy cá nhân vẫn chạy nhanh, nhưng mọi bản lưu đều an toàn trên Cloud và có thể khôi phục 1-click.
