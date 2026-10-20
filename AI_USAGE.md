# AI Usage Log

## 1. Công cụ AI
Tên công cụ: Chat GPT

## 2. Mục đích sử dụng
- Phân tích giao diện trang chi tiết sản phẩm từ ảnh chụp màn hình.
- Đọc và giải thích mã HTML, CSS, JavaScript của bài.
- Gợi ý hướng kiểm tra và sửa lỗi ở phần chọn màu sắc.
- Hướng dẫn đưa bài lên GitHub và bật GitHub Pages.

## 3. Prompt đã sử dụng
- Prompt 1: Hỗ trợ thiết kế giao diện phù hợp
- Prompt 2: Hỗ trợ viết đoạn mã nguồn
- Prompt 3: Hướng dẫn kiểm tra giao diện ở trên di động
- Prompt 4: Hướng dẫn sửa lỗi ở mục hiện màu sắc


## 4. Kết quả AI đề xuất
- AI đề xuất các hướng kiểm tra nguyên nhân: lỗi JavaScript trong Console chặn các dòng phía sau, `id="selected-color"` bị sai hoặc bị xóa, hoặc trình duyệt đang dùng bản file cũ (cache).
- AI đề xuất cách sửa tương ứng với từng nguyên nhân, kèm lời nhắc chỉ ghi lỗi mà tôi đã tự tái hiện được.

## 5. Kiểm tra và điều chỉnh
- Lỗi tôi tự phát hiện: khi bấm nút "Đen", dòng chữ "Màu sắc: ..." phía trên không đổi thành "Đen", nên người dùng không biết mình đã chọn đúng màu hay chưa.
- Đã kiểm tra: mở trang trên Chrome, nhấn Ctrl+F5, bấm nút "Đen" rồi "Trắng" và quan sát dòng chữ "Màu sắc". Mở DevTools (F12): tab Console để xem lỗi JavaScript, tab Elements để kiểm tra thẻ `<strong id="selected-color">`. Kết quả quan sát: [ghi điều bạn thật sự thấy, ví dụ: Console báo lỗi ... / thẻ strong bị mất id ...].
- Cách sửa: bổ sung đoạn code ở index và css. Sau khi sửa, bấm "Đen" thì chữ thành "Đen", bấm "Trắng" thì chữ thành "Trắng".

## 6. Phần tôi hiểu và có thể giải thích
- `<strong id="selected-color">` (HTML): nơi hiển thị tên màu đang chọn. `id` là "địa chỉ" để JavaScript tìm đúng phần tử này.
- `data-color` (HTML): thuộc tính lưu tên màu ("Trắng", "Đen") trên mỗi nút để JavaScript đọc.
- `addEventListener("click", ...)` (JavaScript): lắng nghe thao tác bấm vào nút chọn màu.
- `button.dataset.color` (JavaScript): đọc giá trị `data-color` của nút vừa được bấm.
- `querySelector("#selected-color").textContent = ...` (JavaScript): tìm thẻ có id `selected-color` rồi ghi tên màu mới vào. Nếu không tìm thấy phần tử hoặc có lỗi trước dòng này thì chữ sẽ không đổi.
- Class `.selected` và `aria-pressed` (JavaScript + CSS): JavaScript gỡ rồi gắn lại class `.selected`, CSS dùng class này để tô viền xanh cho nút đang chọn; `aria-pressed` báo trạng thái cho phần mềm đọc màn hình.
- Vai trò CSS: CSS không quyết định nội dung chữ, chỉ định dạng cách hiển thị (viền xanh, nền, cỡ chữ).
