# EduLinks – Kho học liệu Tin học trực tuyến

## 1. Chuẩn bị
Cài VS Code và tiện ích Live Server. Tạo tài khoản tại https://console.firebase.google.com/ và https://app.netlify.com/.

## 2. Firebase
1. Firebase Console > Add project > tạo dự án.
2. Project settings (biểu tượng bánh răng) > Your apps > Web (`</>`) > Register app > sao chép `firebaseConfig` vào `firebase-config.js` (thay toàn bộ giá trị mẫu).
3. Build > Authentication > Get started > Sign-in method > Email/Password > Enable. Vào Users > Add user tạo email và mật khẩu quản trị (không lưu mật khẩu trong mã nguồn).
4. Trong Authentication > Users, sao chép **User UID** của tài khoản quản trị. Điền UID này vào `ADMIN_UID` trong `firebase-config.js`.
5. Build > Firestore Database > Create database > chọn vị trí phù hợp > tạo. Chọn tab Rules, dán nội dung `firestore.rules`, thay `THAY_UID_ADMIN` bằng cùng UID ở bước 4, bấm Publish. **Không để rules ở chế độ test công khai ghi.**
6. Authentication > Settings > Authorized domains: thêm domain Netlify sau khi triển khai nếu cần. `localhost` cũng phải được cho phép khi thử nghiệm trên máy (nếu không có, thêm thủ công).

## 3. Chạy bằng VS Code
Mở thư mục dự án trong VS Code. Nhấp phải `index.html` > Open with Live Server. Không mở bằng đường dẫn `file://` vì website dùng ES modules. Kết nối Internet là bắt buộc để tải Firebase SDK và dữ liệu.

## 4. Triển khai Netlify
Vào https://app.netlify.com/ > Add new project > Deploy manually (hoặc chức năng kéo thả thư mục). Kéo thả thư mục chứa `index.html`, `style.css`, `script.js`, `firebase-config.js`. Truy cập URL Netlify để kiểm tra. Đảm bảo cấu hình Firebase và Firestore Rules đã được xuất bản.

## 5. Phân quyền
- Người xem: không cần đăng nhập, xem/tìm kiếm/mở link, đánh dấu yêu thích cục bộ và xuất JSON.
- Quản trị: đăng nhập Email/Password, thêm/sửa/xóa và nhập JSON lên Firestore.
- Quyền ghi **được kiểm tra trên máy chủ bởi Firestore Rules**, không chỉ bằng việc ẩn nút trong giao diện.
- `firebase-config.js` chứa cấu hình công khai, không chứa mật khẩu hay khóa quản trị dịch vụ.

## 6. Dữ liệu cũ
Trên phiên bản EduLinks cá nhân, chọn **Sao lưu** để tải JSON. Trong phiên bản Firebase, đăng nhập quản trị và chọn **Khôi phục** để nhập các học liệu lên Firestore. Nhập dữ liệu sẽ thêm/cập nhật theo ID; không tự xóa học liệu hiện có.

## 7. Lưu ý
Gói miễn phí Firebase/Netlify có hạn mức. Chỉ chia sẻ URL học liệu công khai và hợp pháp; không đăng dữ liệu cá nhân học sinh. Dữ liệu Firestore lưu trực tuyến, còn danh sách yêu thích chỉ lưu trên trình duyệt từng người. Nếu thay đổi tài khoản quản trị, phải cập nhật UID ở cả file cấu hình và Firestore Rules.
