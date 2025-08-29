# Quản lý sách
Môn học: Lập Trình Web PTIT

Yêu cầu dự án: Tạo Web quản lý sách (Người bán, người mua, các thao tác quản lý sách, mua sách, thanh toán, ...)

Chi tiết: [Link YouTube](https://youtu.be/XwT-syuvcQU?si=BLijGWfBIddWHMIJ)

(Dưới đây nêu một vài điểm đáng chú ý)
# Công nghệ
SpringBoot

Thymleaf

Jpa + mySQL

Lombok

Spring Security

Common Validator

# Cách UpLoad Ảnh

**Cách lưu ảnh từ view xuống DB**
Trong entity Book thêm 1 field có kiểu dữ liệu MultipartFile để xử lý ảnh trên view, 1 file có kiểu dữ liệu byte[] lưu ảnh trong DB.

Trên view tạo thẻ input có th:field tương ứng field MultipartFile.

Ở server: set field byte[] của book = newBook.getFileData().getBytes(); gọi save của bookRepository

**Cách load ảnh lên**
Trên view, phần ảnh gắn link có request “bookImage”, tham số id = id của book.

Bên controller xử lý bằng method productImage.

# Cách lưu Cart (Giỏ hàng)
Sử dụng Session (getCartInSession): Lưu trữ Cart tạm thời, Nếu Sign out thì Cart được Reset

**Logic xử lý**

CartInfo: Kiểm tra xem sách tồn tại trong giỏ hay chưa (Nếu chưa phải set số lượng ban đầu là 0).

Sau đó số lượng = số lượng ban đầu của sách đó trong giỏ + số lượng sách mới thêm.

Nếu số lượng <= 0 thì loại bỏ khỏi giỏ, ngược lại thêm mới số lượng đó.

Khi đặt hàng xong: thực hiện xóa cartInfo trong session (method removeCartInSession của classUtils).

# Đánh giá của khách hàng 
Lấy id_book, username ; Set các giá trị book, user, và thời gian comment của user đó rồi save trong repository.

**Lưu star**: Tạo 1 input trên html, khi ấn Star -> xác định vị trí của ngôi sao và lưu ở input đó (lấy số Star)

