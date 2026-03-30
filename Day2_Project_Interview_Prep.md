# Day 2: Project Review + Interview Prep (5 giờ)

> *Ngày 2: Chuẩn bị cho phần trao đổi về project, kỹ năng giao tiếp kỹ thuật, và các câu hỏi phỏng vấn thường gặp.*

---

## Block 1 (2h) — CV & Project Preparation / Chuẩn Bị CV & Dự Án

---

### Self Introduction — Tự Giới Thiệu (English)

- [ ] **Luyện đọc thành tiếng 5 lần (tối đa 1-2 phút):**

> *Đây là phần đầu tiên của interview. HR nói 50% tiếng Anh, nên bạn phải chuẩn bị tự giới thiệu bằng tiếng Anh thật tự nhiên.*

```
"Hi, I'm [Your Name], a [year — e.g., third-year] student at [University]
majoring in [Major — e.g., Computer Science / Software Engineering].

I'm passionate about [your interest — e.g., backend development / web applications].

During my studies, I've built [1-2 projects], for example [Project Name],
where I used [tech stack — e.g., Java Spring Boot, MySQL].
My role was [your role] and the biggest challenge I faced was [challenge],
which I solved by [solution].

I'm really excited about the WeCamp program at NAB because
[reason — e.g., I want to learn how software is built at scale in a real banking environment,
and I believe NAB's mentorship program will help me grow as a developer]."
```

**Mẹo:** Không cần học thuộc, chỉ cần nhớ các ý chính. Nói tự nhiên như đang kể chuyện cho bạn nghe.

---

### Project Deep Dive — Chuẩn Bị Nói Về Dự Án

> *Interviewer sẽ hỏi sâu về project mà bạn ghi trong CV. Họ muốn biết bạn THỰC SỰ làm gì, không phải chỉ ghi cho đẹp.*

**Với MỖI project trong CV, chuẩn bị trả lời 5 câu hỏi sau:**

---

#### Project 1: _______________

- [ ] **1. Dự án này là gì? Bạn làm vai trò gì?**
  - (Miêu tả ngắn gọn 2-3 câu)
  - English: "This project is a ___. I was responsible for ___."
  - Tiếng Việt: "Dự án này là ___. Em phụ trách phần ___."

- [ ] **2. Tech stack là gì? Tại sao chọn nó?**
  - (Không chỉ liệt kê — giải thích LÝ DO)
  - English: "We used ___ because ___."
  - VD: "Chúng em dùng Spring Boot vì nó hỗ trợ tốt cho REST API và có nhiều thư viện sẵn. Database dùng MySQL vì dữ liệu có cấu trúc rõ ràng."

- [ ] **3. Thách thức lớn nhất là gì? Bạn giải quyết thế nào?**
  - (Đây là câu QUAN TRỌNG NHẤT — họ muốn thấy cách bạn suy nghĩ)
  - English: "The biggest challenge was ___. I solved it by ___."
  - VD: "Lúc đầu API bị chậm khi load nhiều dữ liệu. Em đã thêm phân trang (pagination) và dùng caching để giảm tải cho database."

- [ ] **4. Bạn học được gì từ dự án này?**
  - VD: "Em học được cách làm việc nhóm với Git, cách thiết kế database, và tầm quan trọng của việc viết test."

- [ ] **5. Nếu làm lại, bạn sẽ thay đổi gì?**
  - (Cho thấy bạn tự đánh giá được bản thân)
  - VD: "Em sẽ viết unit test ngay từ đầu, và dùng Docker để môi trường dev đồng nhất hơn."

---

#### Project 2: _______________

- [ ] **1. Dự án là gì? Vai trò?**
- [ ] **2. Tech stack & lý do?**
- [ ] **3. Thách thức & cách giải quyết?**
- [ ] **4. Bài học rút ra?**
- [ ] **5. Nếu làm lại thì thay đổi gì?**

---

#### Project 3: _______________

- [ ] **1. Dự án là gì? Vai trò?**
- [ ] **2. Tech stack & lý do?**
- [ ] **3. Thách thức & cách giải quyết?**
- [ ] **4. Bài học rút ra?**
- [ ] **5. Nếu làm lại thì thay đổi gì?**

---

### Questions to Ask the Interviewer — Câu Hỏi Cho Interviewer

- [ ] **Chuẩn bị 2-3 câu hỏi (cho thấy bạn quan tâm và nghiêm túc):**
  - "What does a typical day look like for a WeCamp intern?" *(Một ngày làm việc của WeCamp intern như thế nào?)*
  - "What tech stack does the team currently use?" *(Team đang sử dụng tech stack gì?)*
  - "What kind of mentorship or support do interns receive?" *(Intern được hỗ trợ và hướng dẫn như thế nào?)*
  - "What qualities do you look for in a successful WeCamp candidate?" *(Anh/chị tìm kiếm điều gì ở ứng viên WeCamp?)*

---

## Block 2 (1.5h) — Common Interview Questions / Câu Hỏi Phỏng Vấn Thường Gặp

---

### Java vs JavaScript

- [ ] **"Java và JavaScript khác nhau như thế nào?"**

> *Giống như "Car" và "Carpet" — chỉ giống tên, hoàn toàn khác nhau!*

| | Java | JavaScript |
|---|---|---|
| Kiểu dữ liệu | Static (khai báo kiểu trước) | Dynamic (tự động nhận kiểu) |
| Chạy trên | JVM (máy ảo Java) | Browser / Node.js |
| OOP | Class-based (chính thống) | Prototype-based |
| Đa luồng | Multi-threaded | Single-threaded (event loop) |
| Dùng cho | Backend, Android, Enterprise | Frontend web, Full-stack |
| Biên dịch | Compile ra bytecode trước | Interpret trực tiếp |

```java
// Java — phải khai báo kiểu
int tuoi = 22;           // PHẢI nói là "int"
String ten = "Minh";     // PHẢI nói là "String"
```

```javascript
// JavaScript — không cần khai báo kiểu
let tuoi = 22;           // tự hiểu là số
let ten = "Minh";        // tự hiểu là chuỗi
tuoi = "hai mươi hai";   // đổi thành chuỗi cũng được! (dynamic)
```

---

### REST API & HTTP

- [ ] **"REST API là gì?"**

> *REST API giống như thực đơn nhà hàng. Khách hàng (client) gọi món (request), bếp (server) làm và trả món (response). Mỗi món có mã số riêng (URL).*

**HTTP Methods — "Các loại yêu cầu":**

| Method | Giống như... | Mục đích | Ví dụ |
|---|---|---|---|
| **GET** | Xem thực đơn | Đọc dữ liệu | Xem danh sách sản phẩm |
| **POST** | Gọi món mới | Tạo dữ liệu mới | Tạo tài khoản mới |
| **PUT** | Đổi toàn bộ món | Cập nhật toàn bộ | Sửa toàn bộ thông tin user |
| **PATCH** | Thêm gia vị | Cập nhật 1 phần | Chỉ đổi tên user |
| **DELETE** | Huỷ món | Xoá dữ liệu | Xoá tài khoản |

**Status Codes — "Nhà hàng trả lời":**

| Code | Giống như... | Ý nghĩa |
|---|---|---|
| **200** | "Đây món ăn của bạn!" | OK — thành công |
| **201** | "Món mới đã được ghi!" | Created — tạo thành công |
| **400** | "Tôi không hiểu bạn gọi gì" | Bad Request — yêu cầu sai |
| **401** | "Bạn chưa đăng nhập/đặt bàn" | Unauthorized — chưa xác thực |
| **403** | "Bạn không được phép vào VIP" | Forbidden — không có quyền |
| **404** | "Món này không có trong thực đơn" | Not Found — không tìm thấy |
| **500** | "Bếp bị cháy rồi!" | Internal Server Error — lỗi server |

```
GET    /api/users          → Lấy danh sách user
GET    /api/users/123      → Lấy user có id = 123
POST   /api/users          → Tạo user mới
PUT    /api/users/123      → Cập nhật toàn bộ user 123
DELETE /api/users/123      → Xoá user 123
```

---

### Git Basics — Git Cơ Bản

- [ ] **"Bạn sử dụng Git như thế nào?"**

> *Git giống như "nút Undo/Save siêu cấp" cho code. Bạn có thể quay lại bất kỳ thời điểm nào, và nhiều người có thể cùng làm mà không đè lên nhau.*

**Hình dung như này:** Nghĩ về viết luận văn nhóm:
- `git clone` = **Copy luận văn** từ Google Drive về máy
- `git branch` = **Tạo bản nháp riêng** để viết phần của mình
- `git add` = **Đánh dấu** những thay đổi muốn giữ
- `git commit` = **Lưu lại** với ghi chú "đã viết xong phần 2"
- `git push` = **Đẩy lên** Google Drive cho mọi người thấy
- `git pull` = **Tải về** bản mới nhất từ Google Drive
- `git merge` = **Gộp** phần của mình vào bản chính

```bash
# Bắt đầu làm việc
git clone https://github.com/team/project.git   # copy repo về
cd project

# Tạo nhánh riêng để làm feature
git checkout -b feature/login                     # tạo nhánh mới

# Viết code xong, lưu lại
git add LoginService.java                         # đánh dấu file thay đổi
git commit -m "Add login feature with JWT token"  # lưu với ghi chú

# Đẩy lên remote
git push origin feature/login                     # đẩy lên GitHub

# Khi muốn gộp vào main
git checkout main
git pull origin main                              # lấy bản mới nhất
git merge feature/login                           # gộp code vào
```

**Branching Strategy (làm việc nhóm):**
- `main` — code chính, luôn chạy được
- `develop` — code đang phát triển
- `feature/xxx` — nhánh làm tính năng mới
- **Pull Request (PR)** — xin phép gộp code, người khác review trước khi merge

---

### MVC Pattern

- [ ] **"MVC là gì?"**

> *MVC chia ứng dụng thành 3 phần riêng biệt, mỗi phần lo 1 việc.*

**Hình dung như này:** Nghĩ về **nhà hàng**:
- **Model (Bếp)** = Nơi nấu ăn, xử lý nguyên liệu. Trong code: xử lý dữ liệu, business logic, liên hệ database.
- **View (Bàn ăn)** = Nơi khách thấy món ăn đẹp mắt. Trong code: giao diện người dùng (HTML, UI).
- **Controller (Phục vụ)** = Người nhận order từ khách, chuyển cho bếp, mang món ra. Trong code: nhận request, gọi logic, trả response.

```
Người dùng (Khách hàng)
    ↓  click/nhập liệu
Controller (Phục vụ) — nhận yêu cầu
    ↓  gọi xử lý
Model (Bếp) — xử lý dữ liệu, tính toán
    ↓  trả kết quả
View (Bàn ăn) — hiển thị cho người dùng
```

```java
// Model — xử lý dữ liệu
class SinhVien {
    private String ten;
    private double diem;
    // getters, setters, business logic...
}

// Controller — nhận request, điều phối
@RestController
class SinhVienController {
    @GetMapping("/sinhvien/{id}")
    public SinhVien layThongTin(@PathVariable int id) {
        return sinhVienService.timTheoId(id);
    }
}

// View — hiển thị (HTML/JSON trả về cho client)
```

---

### Dependency Injection — Tiêm Phụ Thuộc

- [ ] **"Dependency Injection là gì?"**

> *Thay vì tự đi mua nguyên liệu (tạo dependency), bạn được giao hàng tận nơi (inject dependency).*

**Hình dung như này:**

**KHÔNG có DI:** Bạn tự nấu ăn — phải tự đi chợ mua thịt, mua rau, mua gia vị. Bạn phụ thuộc vào chợ Cũ → khó thay đổi.
**CÓ DI:** Bạn gọi ship — người ta giao nguyên liệu tận nơi. Muốn đổi nguyên liệu? Chỉ cần đổi đơn hàng, không cần thay đổi cách nấu.

```java
// ===== KHÔNG có DI — "tự đi chợ" =====
class DichVuDonHang {
    // Tự tạo PaymentService — phụ thuộc cứng (hard to test, hard to change)
    private DichVuThanhToan thanhToan = new DichVuThanhToan();

    void xuLyDon() {
        thanhToan.thanhToan();
    }
}
// Vấn đề: muốn đổi sang VNPay? Phải SỬA code trong DichVuDonHang!

// ===== CÓ DI — "được giao tận nơi" =====
class DichVuDonHang {
    private DichVuThanhToan thanhToan;

    // ThanhToan được TRUYỀN VÀO từ bên ngoài (inject)
    DichVuDonHang(DichVuThanhToan thanhToan) {
        this.thanhToan = thanhToan;
    }
}
// Muốn đổi sang VNPay? Chỉ cần truyền object khác, KHÔNG sửa DichVuDonHang!

// ===== Spring Framework làm DI tự động =====
@Service
class DichVuDonHang {
    @Autowired  // Spring tự động "tiêm" DichVuThanhToan vào
    private DichVuThanhToan thanhToan;
}
```

**Lợi ích:** Dễ test (truyền mock object), dễ thay đổi, code sạch hơn.

---

### SQL Basics — SQL Cơ Bản

- [ ] **Joins — Nối bảng**

> *Join giống như ghép 2 bảng Excel lại với nhau dựa trên cột chung.*

**Hình dung như này:** Bạn có 2 bảng:
- Bảng `khách_hàng`: id, tên
- Bảng `đơn_hàng`: id, khách_hàng_id, sản_phẩm

| INNER JOIN | LEFT JOIN | RIGHT JOIN |
|---|---|---|
| Chỉ lấy khách hàng ĐÃ mua hàng | Lấy TẤT CẢ khách hàng, kể cả chưa mua | Lấy TẤT CẢ đơn hàng, kể cả đơn không có khách |
| Giao của 2 bảng | Toàn bộ bảng trái + phần giao | Toàn bộ bảng phải + phần giao |

```sql
-- INNER JOIN: Chỉ lấy khách hàng CÓ đơn hàng
SELECT kh.ten, dh.san_pham
FROM khach_hang kh
INNER JOIN don_hang dh ON kh.id = dh.khach_hang_id;
-- Kết quả: chỉ những khách hàng đã từng mua

-- LEFT JOIN: Lấy TẤT CẢ khách hàng, có mua hàng hay không
SELECT kh.ten, dh.san_pham
FROM khach_hang kh
LEFT JOIN don_hang dh ON kh.id = dh.khach_hang_id;
-- Kết quả: tất cả khách hàng, ai chưa mua thì san_pham = NULL
```

- [ ] **Indexing — Đánh chỉ mục**

> *Index giống như mục lục sách — thay vì đọc từ trang 1 đến trang 500, bạn tra mục lục là tìm thấy ngay.*

- **Lợi:** Truy vấn SELECT nhanh hơn nhiều
- **Hại:** INSERT/UPDATE chậm hơn (phải cập nhật mục lục)
- **Dùng khi:** Cột thường dùng trong WHERE, JOIN, ORDER BY

- [ ] **Normalization — Chuẩn hoá**

> *Giảm trùng lặp dữ liệu, giống như không viết địa chỉ công ty ở mỗi dòng nhân viên, mà tách riêng thành bảng công_ty.*

- **1NF:** Mỗi ô chỉ chứa 1 giá trị (không có danh sách trong 1 ô)
- **2NF:** 1NF + mỗi cột phụ thuộc vào TOÀN BỘ khoá chính
- **3NF:** 2NF + không có phụ thuộc gián tiếp (A → B → C thì tách B ra)

---

## Block 3 (1.5h) — English Technical Communication / Giao Tiếp Kỹ Thuật

---

### Useful English Phrases for Interview

- [ ] **Khi chưa hiểu câu hỏi:**
  - "Could you please repeat the question?"
  - "Just to clarify, are you asking about ___?"
  - "Let me make sure I understand — you want to know about ___?"

- [ ] **Khi giải thích kỹ thuật:**
  - "Basically, it works like this: ___"
  - "Think of it as ___ (analogy)"
  - "The main difference between A and B is ___"
  - "I chose ___ because ___"

- [ ] **Khi không biết:**
  - "I'm not entirely sure about that, but I think ___"
  - "I haven't worked with that directly, but I would approach it by ___"
  - "That's a great question. I don't know the exact answer, but I would look into ___"

- [ ] **Khi nói về project:**
  - "I was responsible for ___"
  - "The main challenge was ___"
  - "I solved it by ___"
  - "If I were to do it again, I would ___"

---

### Practice Questions — Tự Tập Trả Lời

- [ ] **Trả lời THÀNH TIẾNG (không đọc thầm!) các câu sau:**
  1. "Tell me about yourself" — giới thiệu bản thân (1-2 phút)
  2. "What is OOP? Can you explain the 4 pillars?" — giải thích 4 trụ OOP
  3. "What is the difference between ArrayList and LinkedList?" — so sánh
  4. "Explain the difference between `==` and `.equals()` in Java" — so sánh
  5. "What is a REST API?" — giải thích
  6. "Tell me about a project you're proud of" — kể về project
  7. "What is dependency injection and why is it useful?" — giải thích
  8. "Why do you want to join NAB WeCamp?" — lý do ứng tuyển

---

## Checklist Cuối Ngày 2

- [ ] Tôi có thể tự giới thiệu bằng tiếng Anh trong 1-2 phút
- [ ] Tôi có thể nói sâu về 2-3 project trong CV
- [ ] Tôi biết cách giải thích REST API, MVC, DI một cách đơn giản
- [ ] Tôi đã luyện trả lời các câu hỏi kỹ thuật THÀNH TIẾNG
- [ ] Tôi đã chuẩn bị 2-3 câu hỏi để hỏi người phỏng vấn
