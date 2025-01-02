# Details

## Bảng Address

- id (PK): Khóa chính duy nhất của bảng.
- entity_type: Xác định loại đối tượng liên quan đến địa chỉ, ví dụ: "Client", "Store", "Supplier".
- entity_id: ID của đối tượng liên quan (Client ID, Store ID, hoặc Supplier ID).
- street: Đường và số nhà.
- ward: Phường/xã.
- district: Quận/huyện.
- city: Thành phố.
- created_at: Thời điểm tạo địa chỉ.
- updated_at: Thời điểm cập nhật gần nhất.

***Ràng buộc***

- entity_type và entity_id kết hợp thành một liên kết (FK) tới bảng tương ứng, ví dụ: Client, Store, hoặc Supplier.
- entity_type có thể là ENUM để giới hạn giá trị (Client, Store, Supplier).

## Bảng Store

- id (PK): Khóa chính duy nhất của cửa hàng.
- name: Tên cửa hàng.
- image_id: Id hình ảnh của cửa hàng.
- address_id (FK → Address.id): Liên kết đến bảng Address để lưu thông tin địa chỉ của cửa hàng.
- phone_number: Số điện thoại của cửa hàng.
- email: Địa chỉ email của cửa hàng.
- opening_hours: Giờ mở cửa của cửa hàng.
- closing_hours: Giờ đóng cửa của cửa hàng.
- store_manager_id (FK → Staff.id): ID của nhân viên quản lý cửa hàng (liên kết với bảng Staff).
- created_at: Thời gian tạo cửa hàng.
- updated_at: Thời gian cập nhật cửa hàng gần nhất.

## Bảng Storage (Kho)

- id (PK): Khóa chính, ID của kho.
- name: Tên kho (ví dụ: "Kho 1", "Kho chính").
- address_id (FK → Address.id): Liên kết đến bảng Address để lưu thông tin địa chỉ của kho.
- capacity: Dung lượng của kho, có thể là số lượng sản phẩm hoặc diện tích.
- created_at: Ngày tạo kho.
- updated_at: Ngày cập nhật kho.

## Bảng Shelf (Kệ)

- id (PK): Khóa chính, ID của kệ.
- storage_id (FK → Storage.id): Liên kết đến kho mà kệ thuộc về.
- name: Tên kệ (ví dụ: "Kệ 1", "Kệ 2").
- capacity: Dung lượng của kệ (số lượng sản phẩm mà kệ có thể chứa).
- location: Vị trí của kệ trong kho (ví dụ: "Tầng 1, góc trái").
- created_at: Ngày tạo kệ.
- updated_at: Ngày cập nhật kệ.

<!-- TODO: ERD -->
## Bảng Image

- id (PK): ID của hình ảnh (Khóa chính).
- type: Loại đối tượng mà hình ảnh liên quan đến (ví dụ: Product, Ingredient, Post, Store, v.v.). Trường này sẽ giúp phân loại hình ảnh theo các nhóm đối tượng khác nhau.
- image_url: Đường dẫn (URL) của hình ảnh (hoặc đường dẫn tệp trong hệ thống).
- alt_text: Văn bản thay thế (alt text) của hình ảnh, giúp cải thiện SEO và trải nghiệm người dùng (dùng khi hình ảnh không thể tải được).
- created_at: Ngày tạo hình ảnh.
- updated_at: Ngày cập nhật hình ảnh.

## Bảng Supplier (Đại lý cung cấp)

- id (PK): Khóa chính, ID của đại lý cung cấp.
- name: Tên đại lý cung cấp (ví dụ: "Đại lý ABC").
- image_id: Id hình ảnh của đại lý cung cấp.
- contact_person: Người đại diện liên hệ của đại lý (ví dụ: "Nguyễn Văn A").
- email: Địa chỉ email của đại lý.
- phone: Số điện thoại của đại lý.
- address_id: Địa chỉ của đại lý.
- website: Website của đại lý (nếu có).
- created_at: Ngày tạo đại lý cung cấp.
- updated_at: Ngày cập nhật thông tin đại lý

## Bảng Category (Danh mục)

- id (PK): ID của danh mục.
- name: Tên danh mục.
- type: Loại danh mục (Product hoặc Ingredient).
- description: Mô tả chi tiết về danh mục.
- image_id: Id hình ảnh của danh mục.
- parent_id: Nếu danh mục có phân cấp (Danh mục cha). Có thể sử dụng để tạo các danh mục con (ví dụ: "Đồ uống" có thể có các danh mục con như "Trà", "Cà phê").
- created_at: Ngày tạo danh mục.
- updated_at: Ngày cập nhật danh mục.

## Bảng Product (Sản phẩm)

- id (PK): Khóa chính, ID của sản phẩm.
- name: Tên sản phẩm (ví dụ: "Sữa chua dâu", "Trà sữa Matcha").
- category_id (FK → Category.id): Liên kết đến loại sản phẩm (ví dụ: "Thức uống", "Tráng miệng").
- price: Giá bán của sản phẩm.
- description: Mô tả chi tiết về sản phẩm.
- image_id: Id hình ảnh của sản phẩm.
- is_box: Trường boolean để chỉ định liệu sản phẩm có phải là một combo không.
- parent_id: Nếu là một combo, trường này sẽ trỏ đến một sản phẩm box. (Chỉ có giá trị khi sản phẩm là thành phần trong combo).
- created_at: Ngày tạo sản phẩm.
- updated_at: Ngày cập nhật sản phẩm

## Bảng Ingredients (Nguyên liệu)

- id (PK): Khóa chính, ID của nguyên liệu.
- name: Tên nguyên liệu (ví dụ: "Trà xanh", "Đường", "Sữa").
- category_id (FK → Category.id): Liên kết đến loại nguyên liệu.
- description: Mô tả nguyên liệu (nếu cần).
- quantity_available: Số lượng nguyên liệu hiện có.
- unit: Đơn vị đo lường (ví dụ: "kg", "lít", "g").
- stock_quantity: Số lượng nguyên liệu còn trong kho.
- created_at: Ngày tạo nguyên liệu.
- updated_at: Ngày cập nhật nguyên liệu.

## Bảng Import (Nhập kho)

- id (PK): Khóa chính, ID của giao dịch nhập kho.
- supplier_id (FK → Supplier.id): Liên kết đến nhà cung cấp.
- import_date: Ngày nhập kho.
- total_amount: Tổng giá trị của lô hàng nhập kho.
- created_by: Người tạo giao dịch nhập kho (ví dụ: nhân viên kho).
- created_at: Ngày tạo giao dịch nhập kho.
- updated_at: Ngày cập nhật giao dịch nhập kho.

## Bảng Import_Ingredients (Liên kết giữa Import và Ingredients)

- import_id (FK → Import.id): Liên kết đến giao dịch nhập kho.
- ingredient_id (FK → Ingredients.id): Liên kết đến nguyên liệu.
- storage_id để biết nguyên liệu được nhập vào kho nào hoặc xuất từ kho nào.
- quantity: Số lượng nguyên liệu nhập vào kho.
- unit_price: Giá trị của một đơn vị nguyên liệu nhập kho.
- expiration_date: Ngày hết hạn của nguyên liệu nhập kho (nếu có).
- batch_number: Mã lô nguyên liệu nhập kho, giúp phân biệt các lô nguyên liệu nhập kho khác nhau.
- created_at: Ngày tạo giao dịch xuất kho.
- updated_at: Ngày cập nhật giao dịch xuất kho.

## Bảng Export (Xuất kho)

- id (PK): Khóa chính, ID của giao dịch xuất kho.
- export_date: Ngày xuất kho.
- created_by: Người tạo giao dịch xuất kho.
- created_at: Ngày tạo giao dịch xuất kho.
- updated_at: Ngày cập nhật giao dịch xuất kho.

## Bảng Export_Ingredients (Liên kết giữa Export và Ingredients)

- export_id (FK → Export.id): Liên kết đến giao dịch xuất kho.
- ingredient_id (FK → Ingredients.id): Liên kết đến sản phẩm.
- storage_id để biết nguyên liệu được nhập vào kho nào hoặc xuất từ kho nào.
- quantity: Số lượng sản phẩm đã xuất.
- batch_number: Mã lô sản phẩm đã xuất kho.
- created_at: Ngày tạo giao dịch xuất kho.
- updated_at: Ngày cập nhật giao dịch xuất kho.

## Bảng Khách hàng (Customer)

- id (PK): ID của khách hàng.
- first_name: Tên.
- last_name: Họ.
- email: Địa chỉ email của khách hàng.
- phone: Số điện thoại của khách hàng.
- address_id: Địa chỉ giao hàng.
- points: Tổng điểm khách hàng tích lũy.
- created_at: Ngày tạo.
- updated_at: Ngày cập nhật.

## Bảng Permission

- id: ID của quyền.
- name: Tên quyền (ví dụ: View Product, Edit Product).
- description: Mô tả quyền.
- bit_value: Giá trị bit mà quyền này đại diện. Sử dụng phép toán bitwise để xác định quyền.
- created_at: Thời gian tạo.
- updated_at: Thời gian cập nhật.

```mermaid
erDiagram
PERMISSION {
        int id PK
        string name
        string description
        int bit_value
        date created_at
        date updated_at
    }

    PERMISSION {
        1 "View Product" "Xem sản phẩm" 1 "2025-01-01" "2025-01-02"
        2 "Edit Product" "Sửa sản phẩm" 2 "2025-01-01" "2025-01-02"
        3 "Delete Product" "Xóa sản phẩm" 4 "2025-01-01" "2025-01-02"
        4 "Manage Customers" "Quản lý khách hàng" 8 "2025-01-01" "2025-01-02"
        5 "View Orders" "Xem đơn hàng" 16 "2025-01-01" "2025-01-02"
    }
```

## Bảng Role

- id: ID của vai trò.
- name: Tên vai trò (ví dụ: Admin, Sales Staff).
- description: Mô tả vai trò.
- permission_value: Sử dụng giá trị bitwise để lưu trữ các quyền mà vai trò này có. Ví dụ: Admin có quyền 1 + 2 + 4 + 8 + 16 = 31, Sales Staff có quyền 1 + 2 + 4 + 8 = 15.
- created_at: Thời gian tạo.
- updated_at: Thời gian cập nhật.

```mermaid
id name description permission_value created_at updated_at
1 Admin Quản trị viên 31 2025-01-01 2025-01-02
2 Sales Staff Nhân viên bán hàng 15 2025-01-01 2025-01-02
```

```python
permission_value = 15  # 00001111
has_view_product = permission_value & 1  # 00001111 & 00000001 = 00000001, tức là có quyền View Product

has_delete_product = permission_value & 4  # 00001111 & 00000100 = 00000100, tức là có quyền Delete Product
```

## Bảng Nhân viên (Employee)

- id: ID của nhân viên.
- name: Tên nhân viên.
- email: Email của nhân viên.
- phone: Số điện thoại của nhân viên.
- role_id (FK): Khóa ngoại tham chiếu đến bảng Role để xác định quyền của nhân viên.
- created_at: Thời gian tạo.
- updated_at: Thời gian cập nhật.

## Bảng Transaction_Points

- id: ID của giao dịch điểm.
- customer_id (FK): Khóa ngoại tham chiếu đến bảng Customer để xác định khách hàng nhận điểm thưởng.
- points: Số điểm mà khách hàng nhận được hoặc bị trừ.
- description: Mô tả lý do nhận điểm (ví dụ: Mua hàng, chương trình khuyến mãi).
- emoloyee_id: Nhân viên đổi điểm (chỉ tồn tại khi do nhân viên đổi)
- voucher_id: id voucher đã đổi (chỉ tồn tại khi đổi voucher)
- type: Loại giao dịch điểm (ví dụ: đổi voucher, tích điểm)
- created_at: Thời gian tạo.
- updated_at: Thời gian cập nhật.

## Bảng Product_Discount

- id: ID của chương trình giảm giá.
- product_id (FK): Khóa ngoại tham chiếu đến bảng Product (Sản phẩm).
- discount: Giá trị giảm giá.
- quantity_limit: giới hạn về số lượng.
- type: type có thể là ENUM: "percentage", "fixed" (tồn tại 1 trong 2 phương thức % hay giá tiền)
- start_date và end_date: Thời gian áp dụng giảm giá.
- created_at và updated_at: Thời gian tạo và cập nhật thông tin giảm giá

## Bảng Voucher

- id: ID của voucher.
- code: Mã voucher.
- customer_id (FK): Khóa ngoại tham chiếu đến bảng Customer để xác định khách hàng sở hữu voucher.
- discount_amount: Số tiền giảm.
- amount_limit: Giới hạn về số tiền cần để áp dụng.
- max_discount: giá trị giới hạn được giảm giá (áp dụng cho giảm giá theo %)
- type: type có thể là ENUM: "percentage", "fixed" (tồn tại 1 trong 2 phương thức % hay giá tiền)
- start_date và end_date: Thời gian áp dụng voucher.
- status: Trạng thái sử dụng voucher (khi apply và đặt hàng voucher sẽ tính là đã dùng).
- created_at và updated_at: Thời gian tạo và cập nhật voucher.

## Bảng Order

- id: ID của đơn hàng.
- customer_id (FK): Khóa ngoại tham chiếu đến bảng Customer để xác định khách hàng đặt đơn hàng.
- employee_id: Nhân viên lập hóa đơn(tồn tại nếu nhân viên là người lập -> bán tại cửa hàng)
- total_amount: Tổng số tiền của đơn hàng sau khi áp dụng các chương trình giảm giá hoặc voucher.
- voucher_id (FK): Khóa ngoại tham chiếu đến bảng Voucher, nếu đơn hàng có sử dụng voucher.
- status: Trạng thái của đơn hàng (ví dụ: Pending, Completed).
- created_at và updated_at: Thời gian tạo và cập nhật đơn hàng.

## Bảng Order_Detail

- order_id: ID của đơn hàng.
- product_id (FK): Khóa ngoại tham chiếu đến bảng Customer để xác định khách hàng đặt đơn hàng.
- unit_price: Đơn giá của sản phẩm tại thời điểm mua.
- quantity: Nhân viên lập hóa đơn(tồn tại nếu nhân viên là người lập -> bán tại cửa hàng)
- created_at và updated_at: Thời gian tạo và cập nhật đơn hàng.

## Bảng Schedule

- id (PK): ID của lịch làm việc.
- employee_id (FK): Khóa ngoại tham chiếu đến bảng Employee.
- shift: Loại ca làm việc (Morning, Afternoon, Night).
- work_date để quản lý lịch làm việc hàng ngày
- start_time: Thời gian bắt đầu ca làm việc.
- end_time: Thời gian kết thúc ca làm việc.
- created_at: Thời gian tạo lịch làm việc.
- updated_at: Thời gian cập nhật lịch làm việc.

## Bảng Cart

- id (PK): ID của giỏ hàng.
- customer_id (FK): Khóa ngoại tham chiếu đến bảng Customer.
- created_at: Thời gian tạo giỏ hàng.
- updated_at: Thời gian cập nhật giỏ hàng.

## Bảng Cart_Detail

- id (PK): ID của chi tiết giỏ hàng.
- cart_id (FK): Khóa ngoại tham chiếu đến bảng Cart.
- product_id (FK): Khóa ngoại tham chiếu đến bảng Product.
- quantity: Số lượng sản phẩm trong giỏ.
- created_at: Thời gian thêm sản phẩm vào giỏ.
- updated_at: Thời gian cập nhật chi tiết giỏ hàng.

## Bảng Form

- id (PK): ID của báo cáo.
- employee_id (FK): Khóa ngoại tham chiếu đến bảng Employee.
- form_type: Loại báo cáo (e.g., nghỉ phép, hư hại, mất mát).
- description: Mô tả chi tiết về báo cáo.
- status: Trạng thái báo cáo (Pending, Approved, Rejected).
- created_at: Thời gian tạo báo cáo.
- updated_at: Thời gian cập nhật báo cáo.

## Bảng Form_Detail

- id (PK): ID chi tiết báo cáo.
- form_id (FK): Khóa ngoại tham chiếu đến bảng Form.
- product_id (FK): Khóa ngoại tham chiếu đến bảng Product (nếu áp dụng).
- quantity: Số lượng sản phẩm bị mất hoặc hư hỏng.
- reason: Lý do chi tiết (nếu cần).
- created_at: Thời gian tạo bản ghi chi tiết báo cáo.
- updated_at: Thời gian cập nhật bản ghi chi tiết báo cáo.

## Bảng Post

- id INT (PK) ID của bài đăng.
- title VARCHAR(255) Tiêu đề của bài đăng.
- content TEXT Nội dung chi tiết của bài đăng.
- status ENUM Trạng thái của bài đăng (Draft, Published, Hidden).
- published_at DATETIME Thời gian bài đăng được xuất bản.
- author_id INT (FK) Khóa ngoại tham chiếu đến bảng Employee.
- created_at DATETIME Thời gian tạo bài đăng.
- updated_at DATETIME Thời gian cập nhật bài đăng.

## Bảng Section

- id INT (PK) ID của phần trong bài đăng.
- post_id INT (FK) Khóa ngoại tham chiếu đến bảng Post.
- title VARCHAR(255) Tiêu đề của phần.
- content TEXT Nội dung của phần.
- position INT Thứ tự hiển thị của phần trong bài đăng.
- created_at DATETIME Thời gian tạo phần.
- updated_at DATETIME Thời gian cập nhật phần.

## Bảng Post_Category_Assignment

- id INT (PK) ID của bản ghi.
- post_id INT (FK) Khóa ngoại tham chiếu đến bảng Post.
- category_id INT (FK) Khóa ngoại tham chiếu đến bảng Post_Category.
- created_at DATETIME Thời gian tạo phần.
- updated_at DATETIME Thời gian cập nhật phần.

## OrderUpdatedHistory, ProductUpdatedHistory, và EmployeeUpdatedHistory
