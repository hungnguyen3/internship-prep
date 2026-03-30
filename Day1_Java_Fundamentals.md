# Day 1: Java Fundamentals (5 giờ)

> *Ngày 1: Nền tảng Java cơ bản — hiểu sâu các khái niệm OOP, từ khóa, xử lý lỗi, và các kiểu dữ liệu quan trọng.*

---

## Block 1 (2.5h) — Core Java / Java Cơ Bản

---

### 1. OOP — Lập Trình Hướng Đối Tượng

> *OOP là cách tổ chức code theo "đối tượng" — giống như ngoài đời thực, mọi thứ đều là một đối tượng có thuộc tính và hành động.*

---

#### Encapsulation — Đóng Gói

- [ ] **Encapsulation / Đóng gói**

> *Đóng gói là giấu thông tin bên trong và chỉ cho người ngoài truy cập qua các "cửa" (method) mà mình cho phép.*

**Hình dung như này:** Nghĩ về một **cây ATM**. Bạn không thể mở máy ATM ra và tự lấy tiền. Bạn phải bấm nút (method) để rút tiền, và máy ATM tự kiểm tra số dư (private field) cho bạn.

```java
public class ATM {
    private double soDu;  // người ngoài KHÔNG thể trực tiếp thay đổi số dư

    public double xemSoDu() {
        return soDu;       // chỉ xem được qua method này
    }

    public void rutTien(double soTien) {
        if (soTien > 0 && soTien <= soDu) {
            soDu -= soTien;  // máy ATM tự trừ tiền
        }
    }
}
// Bạn KHÔNG thể làm: atm.soDu = 1000000; <-- LỖI! private
// Bạn CHỈ có thể:     atm.rutTien(500);   <-- OK, qua method
```

**Tại sao cần?** Bảo vệ dữ liệu, tránh bị thay đổi sai. Giống như ngân hàng không cho bạn tự sửa số dư.

---

#### Inheritance — Kế Thừa

- [ ] **Inheritance / Kế thừa**

> *Kế thừa là khi một class "con" được thừa hưởng tất cả thuộc tính và hành động của class "cha", và có thể thêm cái mới hoặc thay đổi cái cũ.*

**Hình dung như này:** Nghĩ về **gia đình**. Con cái kế thừa gen từ cha mẹ (màu mắt, chiều cao), nhưng con có thể có thêm đặc điểm riêng (tài năng, sở thích).

```java
// Cha — Động Vật có thể ăn, ngủ
public class DongVat {
    String ten;

    public void an() {
        System.out.println(ten + " đang ăn");
    }

    public void ngu() {
        System.out.println(ten + " đang ngủ");
    }
}

// Con — Chó kế thừa ăn, ngủ TỪ DongVat, và thêm sủa (bark)
public class Cho extends DongVat {
    public void sua() {
        System.out.println(ten + " đang sủa: Gâu gâu!");
    }
}

// Sử dụng:
Cho cun = new Cho();
cun.ten = "Lucky";
cun.an();   // "Lucky đang ăn"   <-- kế thừa từ DongVat
cun.ngu();  // "Lucky đang ngủ"  <-- kế thừa từ DongVat
cun.sua();  // "Lucky đang sủa: Gâu gâu!"  <-- riêng của Cho
```

**Tại sao cần?** Tái sử dụng code — không cần viết lại `an()` và `ngu()` cho mỗi loài động vật.

---

#### Polymorphism — Đa Hình

- [ ] **Polymorphism / Đa hình**

> *Đa hình là "cùng một hành động nhưng mỗi đối tượng thực hiện khác nhau".*

**Hình dung như này:** Nghĩ về nút **"Play"** trên điện thoại. Bấm Play trên Spotify thì phát nhạc, bấm Play trên YouTube thì phát video, bấm Play trên game thì bắt đầu chơi. **Cùng một nút "Play"**, nhưng mỗi app làm khác nhau.

**2 loại:**

**a) Overloading (Nạp chồng) — cùng tên, khác tham số:**
```java
// Giống như quán cơm có nhiều loại cơm:
// gọi "cơm" thì ra cơm trắng, gọi "cơm gà" thì ra cơm gà
class QuanCom {
    void nauCom() {
        System.out.println("Cơm trắng");
    }
    void nauCom(String loai) {
        System.out.println("Cơm " + loai);  // "Cơm gà"
    }
    void nauCom(String loai, int soLuong) {
        System.out.println(soLuong + " đĩa cơm " + loai);
    }
}
```

**b) Overriding (Ghi đè) — class con làm khác class cha:**
```java
class DongVat {
    void keu() {
        System.out.println("...");
    }
}

class Meo extends DongVat {
    @Override
    void keu() {
        System.out.println("Meo meo!");  // Mèo kêu khác
    }
}

class Cho extends DongVat {
    @Override
    void keu() {
        System.out.println("Gâu gâu!");  // Chó kêu khác
    }
}

// Đây là "phép màu" của đa hình:
DongVat a = new Meo();  // biến kiểu DongVat, nhưng đối tượng là Meo
DongVat b = new Cho();  // biến kiểu DongVat, nhưng đối tượng là Cho
a.keu();  // "Meo meo!"  — Java biết gọi method của Meo
b.keu();  // "Gâu gâu!"  — Java biết gọi method của Cho
```

---

#### Abstraction — Trừu Tượng

- [ ] **Abstraction / Trừu tượng**

> *Trừu tượng là chỉ cho thấy "cần làm gì" mà giấu đi "làm như thế nào".*

**Hình dung như này:** Khi bạn **lái xe**, bạn chỉ cần biết: bấm ga để tăng tốc, bấm thắng để dừng. Bạn không cần biết bên trong động cơ hoạt động ra sao. Cái "giấu đi" phía bên trong đó chính là trừu tượng.

```java
// Abstract class — như bản vẽ thiết kế, chưa phải sản phẩm hoàn chỉnh
abstract class PhuongTien {
    String ten;

    // Method trừu tượng — chỉ nói "phải làm gì", CHƯA nói "làm thế nào"
    abstract void diChuyen();

    // Method bình thường — đã có sẵn cách làm
    void dung() {
        System.out.println(ten + " đã dừng lại");
    }
}

class OTo extends PhuongTien {
    @Override
    void diChuyen() {
        System.out.println(ten + " chạy trên đường");  // Ô tô tự định nghĩa cách đi
    }
}

class Thuyen extends PhuongTien {
    @Override
    void diChuyen() {
        System.out.println(ten + " chạy trên nước");   // Thuyền đi khác ô tô
    }
}
```

---

### Abstract Class vs Interface

- [ ] **Khi nào dùng cái nào?**

> *Abstract class giống như "bản vẽ thiết kế có sẵn một số phần đã làm". Interface giống như "hợp đồng — chỉ nói phải làm gì, không làm sẵn gì cả".*

**Hình dung như này:**
- **Abstract class** = Bạn mua nhà thô (có sẵn tường, sàn), bạn chỉ cần trang trí thêm. **Chia sẻ thuộc tính chung.**
- **Interface** = Bạn ký hợp đồng với chủ nhà "phải trả tiền điện mỗi tháng". Hợp đồng chỉ ghi "phải làm gì", không ghi "làm thế nào". **Định nghĩa khả năng.**

| Đặc điểm | Abstract Class | Interface |
|---|---|---|
| Method | Có thể có method đã viết sẵn + method trừu tượng | Chỉ có method trừu tượng (trước Java 8) |
| Thuộc tính | Có thể có biến bình thường | Chỉ có hằng số (`public static final`) |
| Constructor | Có | Không |
| Kế thừa | Chỉ kế thừa 1 (`extends`) | Implement nhiều (`implements`) |
| Dùng khi | Các class con có điểm chung | Định nghĩa "khả năng" mà nhiều class có thể làm |

```java
// Abstract class — các phương tiện có chung "tên" và "dừng()"
abstract class PhuongTien {
    String ten;
    abstract void diChuyen();
    void dung() { System.out.println("Dừng lại!"); }
}

// Interface — khả năng "có thể sạc điện"
interface CoTheSacDien {
    void sacPin();  // chỉ nói "phải có khả năng sạc", không nói cách sạc
}

// Ô tô điện: vừa là phương tiện, vừa có thể sạc điện
class OToDien extends PhuongTien implements CoTheSacDien {
    @Override
    void diChuyen() { System.out.println("Chạy bằng điện"); }

    @Override
    public void sacPin() { System.out.println("Đang sạc..."); }
}
```

---

### Access Modifiers — Phạm Vi Truy Cập

- [ ] **4 mức độ truy cập**

> *Giống như các lớp bảo mật của một toà nhà.*

**Hình dung như này:**
- `public` = **Cửa chính** — ai cũng vào được
- `protected` = **Thẻ nhân viên + gia đình** — nhân viên và người nhà (class con) mới vào
- default (không ghi gì) = **Thẻ nhân viên** — chỉ nhân viên cùng công ty (package) mới vào
- `private` = **Phòng riêng có khoá** — chỉ chính mình (class đó) mới vào

| Modifier | Trong class | Cùng package | Class con | Mọi nơi |
|---|---|---|---|---|
| `public` | OK | OK | OK | OK |
| `protected` | OK | OK | OK | KHÔNG |
| default | OK | OK | KHÔNG | KHÔNG |
| `private` | OK | KHÔNG | KHÔNG | KHÔNG |

```java
public class NguoiDung {
    public String ten;           // ai cũng thấy
    protected String email;      // cùng package + class con thấy
    String soDienThoai;          // chỉ cùng package thấy (default)
    private String matKhau;      // chỉ class NguoiDung thấy
}
```

---

### String vs StringBuilder vs StringBuffer

- [ ] **3 cách làm việc với chuỗi**

> *String giống như viết bút bi (không xoá được, muốn sửa phải viết trang mới). StringBuilder giống như viết bút chì (xoá sửa thoải mái, nhưng chỉ 1 người viết). StringBuffer giống như bảng trắng (xoá sửa được, nhiều người có thể viết cùng lúc an toàn).*

| | String | StringBuilder | StringBuffer |
|---|---|---|---|
| Thay đổi được? | KHÔNG (immutable) | CÓ (mutable) | CÓ (mutable) |
| An toàn đa luồng? | CÓ (vì không đổi) | KHÔNG | CÓ (synchronized) |
| Tốc độ nối chuỗi | CHẬM | NHANH NHẤT | CHẬM hơn StringBuilder |
| Khi nào dùng? | Chuỗi ít thay đổi | Nối chuỗi nhiều (1 luồng) | Nối chuỗi nhiều (đa luồng) |

```java
// String — mỗi lần "+" tạo ra object MỚI (tốn bộ nhớ)
String s = "Xin";
s = s + " chào";  // tạo String mới "Xin chào", String cũ "Xin" bị bỏ
s = s + " bạn";   // lại tạo String mới "Xin chào bạn"
// => Tạo 3 object! Rất tốn bộ nhớ nếu làm nhiều

// StringBuilder — chỉnh sửa NGAY TRÊN object cũ (nhanh, tiết kiệm)
StringBuilder sb = new StringBuilder("Xin");
sb.append(" chào");  // vẫn là object cũ, chỉ thêm vào
sb.append(" bạn");   // vẫn là object cũ
String ketQua = sb.toString();  // "Xin chào bạn"
// => Chỉ 1 object từ đầu đến cuối!
```

**Mẹo nhớ:** Phỏng vấn hỏi → trả lời "dùng StringBuilder khi nối nhiều chuỗi trong vòng lặp, dùng String cho chuỗi ít thay đổi".

---

### == vs .equals() vs hashCode()

- [ ] **So sánh trong Java**

> *`==` hỏi "hai cái này có phải CÙNG MỘT THỨ không?" (cùng địa chỉ). `.equals()` hỏi "hai cái này có GIỐNG NHAU không?" (cùng nội dung).*

**Hình dung như này:** Bạn và bạn bạn cùng có iPhone 15 màu đen.
- `==` hỏi: "Hai cái điện thoại này có phải LÀ MỘT cái không?" → **KHÔNG**, là 2 cái khác nhau
- `.equals()` hỏi: "Hai cái điện thoại này có GIỐNG nhau không?" → **CÓ**, cùng model, cùng màu

```java
// Tạo 2 chuỗi giống nhau nhưng khác object
String a = new String("hello");
String b = new String("hello");

a == b;       // false — 2 object KHÁC NHAU trong bộ nhớ
a.equals(b);  // true  — CÙNG NỘI DUNG "hello"

// Đặc biệt: String pool (Java tối ưu hoá)
String c = "hello";
String d = "hello";
c == d;       // true — Java trỏ cả 2 vào CÙNG 1 chỗ trong String pool

// hashCode() — "mã số" của object, dùng cho HashMap/HashSet
// Quy tắc: nếu a.equals(b) == true thì a.hashCode() == b.hashCode()
```

**Mẹo phỏng vấn:** LUÔN dùng `.equals()` để so sánh nội dung String. Chỉ dùng `==` cho kiểu nguyên thuỷ (int, double, boolean...).

---

### Exception Handling — Xử Lý Lỗi

- [ ] **Checked vs Unchecked Exception**

> *Exception là lỗi xảy ra khi chương trình đang chạy. Giống như khi bạn đang lái xe, có thể gặp: đèn đỏ (checked — biết trước, phải chuẩn bị), hoặc chó vọt ra (unchecked — bất ngờ, không lường trước).*

**Hình dung như này:**
- **Checked Exception** = **Đèn đỏ, ba-ri-e** — bạn BIẾT TRƯỚC có thể gặp, PHẢI chuẩn bị xử lý (try-catch hoặc throws). VD: đọc file có thể không tìm thấy file (`IOException`).
- **Unchecked Exception** = **Ổ gà bất ngờ chạy ra** — không lường trước, thường do lỗi lập trình. VD: chia cho 0 (`ArithmeticException`), gọi method trên null (`NullPointerException`).
- **Error** = **Động đất** — quá nghiêm trọng, không nên bắt. VD: hết RAM (`OutOfMemoryError`).

```
Throwable (gốc)
├── Exception (lỗi có thể xử lý)
│   ├── IOException, SQLException...         <-- Checked (PHẢI bắt)
│   └── RuntimeException                     <-- Unchecked (KHÔNG bắt buộc)
│       ├── NullPointerException
│       ├── ArrayIndexOutOfBoundsException
│       └── ArithmeticException
└── Error (quá nghiêm trọng, KHÔNG nên bắt)
    ├── OutOfMemoryError
    └── StackOverflowError
```

```java
// try-catch-finally giống như:
// try    = "thử làm cái này"
// catch  = "nếu lỗi thì xử lý như này"
// finally = "dù gì cũng làm cái này cuối cùng"

try {
    int[] mang = {1, 2, 3};
    System.out.println(mang[10]);   // LỖI! Chỉ có index 0-2
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Lỗi: Vượt quá chỉ số mảng! " + e.getMessage());
} finally {
    System.out.println("Đoạn này LUÔN chạy, dù có lỗi hay không");
}

// Tự định nghĩa Exception riêng
class HetTienException extends Exception {
    public HetTienException(String msg) {
        super(msg);
    }
}

// Sử dụng:
void rutTien(double soTien) throws HetTienException {
    if (soTien > soDu) {
        throw new HetTienException("Số dư không đủ!");
    }
    soDu -= soTien;
}
```

---

## Block 2 (2.5h) — Collections & Modern Java

---

### Collections Framework — Các Cấu Trúc Dữ Liệu

- [ ] **List, Set, Map — ba anh em nhà Collections**

> *Nghĩ về Collections như các loại "hộp đựng đồ" khác nhau, mỗi loại có đặc điểm riêng.*

**Hình dung như này:**
- **List** = **Danh sách đi chợ** — có thứ tự, cho phép trùng lặp (mua 2 kg gạo OK). *Danh sách có thứ tự, cho phép phần tử trùng.*
- **Set** = **Bộ sưu tập tem** — KHÔNG cho trùng (mỗi con tem là duy nhất). *Tập hợp không cho phép trùng.*
- **Map** = **Danh bạ điện thoại** — mỗi tên (key) ứng với 1 số điện thoại (value). *Cặp key-value, key không trùng.*

```
List (có thứ tự, cho trùng)
├── ArrayList  — giống mảng có thể lớn dần
│   Truy cập nhanh O(1), chèn/xoá chậm O(n)
│   Dùng khi: đọc nhiều, ít chèn/xoá giữa
│
└── LinkedList — giống chuỗi mắt xích
    Truy cập chậm O(n), chèn/xoá nhanh O(1)
    Dùng khi: chèn/xoá nhiều ở đầu/giữa

Set (không trùng)
├── HashSet       — nhanh nhất, KHÔNG có thứ tự
├── LinkedHashSet — giữ thứ tự chèn vào
└── TreeSet       — tự động sắp xếp

Map (key → value)
├── HashMap       — nhanh nhất, KHÔNG có thứ tự
├── LinkedHashMap — giữ thứ tự chèn vào
└── TreeMap       — sắp xếp theo key
```

```java
// === LIST — Danh sách đi chợ ===
List<String> diCho = new ArrayList<>();
diCho.add("Gạo");
diCho.add("Thịt");
diCho.add("Gạo");    // OK! cho trùng lặp
// diCho = ["Gạo", "Thịt", "Gạo"]
diCho.get(0);         // "Gạo" — truy cập theo index

// === SET — Bộ sưu tập tem ===
Set<String> tem = new HashSet<>();
tem.add("Tem Việt Nam");
tem.add("Tem Nhật Bản");
tem.add("Tem Việt Nam");  // KHÔNG thêm! đã có rồi
// tem = {"Tem Việt Nam", "Tem Nhật Bản"} — chỉ 2 phần tử

// === MAP — Danh bạ điện thoại ===
Map<String, String> danhBa = new HashMap<>();
danhBa.put("Mẹ", "0901234567");
danhBa.put("Ba", "0907654321");
danhBa.get("Mẹ");     // "0901234567"
danhBa.getOrDefault("Chị", "Không có"); // "Không có"

// Duyệt qua Map
for (Map.Entry<String, String> entry : danhBa.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```

**Mẹo phỏng vấn:** "ArrayList cho truy cập nhanh, LinkedList cho chèn/xoá nhanh. HashMap khi cần tìm theo key, TreeMap khi cần sắp xếp."

---

### Comparable vs Comparator

- [ ] **2 cách sắp xếp**

> *Comparable = "tôi tự biết cách so sánh mình với người khác". Comparator = "nhờ người khác so sánh giúp".*

**Hình dung như này:**
- **Comparable** = Học sinh tự biết so điểm của mình với bạn khác (so sánh tự nhiên, mặc định)
- **Comparator** = Giáo viên quyết định sắp xếp theo tiêu chí nào: theo điểm, theo tên, theo tuổi...

```java
// Comparable — class TỰ định nghĩa cách so sánh
class SinhVien implements Comparable<SinhVien> {
    String ten;
    double diem;

    @Override
    public int compareTo(SinhVien other) {
        // So sánh theo điểm (tự nhiên)
        return Double.compare(this.diem, other.diem);
    }
}
Collections.sort(danhSach); // tự động dùng compareTo

// Comparator — NGƯỜI NGOÀI định nghĩa cách so sánh
// Muốn sắp xếp theo tên thay vì điểm? Dùng Comparator:
danhSach.sort(Comparator.comparing(sv -> sv.ten));

// Sắp xếp theo điểm giảm dần?
danhSach.sort(Comparator.comparingDouble(sv -> sv.diem).reversed());
```

---

### Generics — Kiểu Tổng Quát

- [ ] **Tại sao cần Generics?**

> *Generics giống như "nhãn dán" trên hộp — biết trước bên trong là gì, tránh nhầm.*

**Hình dung như này:** Nghĩ về **hộp đựng đồ**. Hộp không dán nhãn thì bạn mở ra có thể là gì cũng được (nguy hiểm!). Hộp dán nhãn "SÁCH" thì bạn biết chắc bên trong là sách.

```java
// KHÔNG có Generics — giống hộp không dán nhãn
List hop = new ArrayList();
hop.add("Xin chào");
hop.add(123);         // chèn số vào cũng được! Nguy hiểm!
String s = (String) hop.get(1); // LỖI lúc chạy! 123 không phải String

// CÓ Generics — giống hộp dán nhãn "String"
List<String> hopSach = new ArrayList<>();
hopSach.add("Xin chào");
// hopSach.add(123);  // LỖI NGAY lúc viết code! Compiler báo lỗi
String s = hopSach.get(0);  // Không cần ép kiểu, an toàn
```

---

### Keywords: final, static, this, super

- [ ] **4 từ khoá quan trọng**

> *Mỗi từ khoá có ý nghĩa khác nhau tuỳ vào chỗ dùng.*

**Hình dung như này:**
- `final` = **Hợp đồng đã ký** — không thay đổi được nữa
- `static` = **Bảng thông báo chung** — ai cũng thấy, thuộc về lớp (không cần tạo đối tượng)
- `this` = **"Tôi"** — trỏ đến chính đối tượng hiện tại
- `super` = **"Cha tôi"** — trỏ đến class cha

```java
class Lop {
    static int soHocSinh = 0;      // CHUNG cho tất cả đối tượng Lop
    final String TEN_TRUONG = "NAB Academy";  // KHÔNG đổi được

    String giaoVien;

    Lop(String giaoVien) {
        this.giaoVien = giaoVien;   // this = "tôi" (đối tượng này)
        soHocSinh++;
    }
}

class LopChuyenToan extends Lop {
    LopChuyenToan(String giaoVien) {
        super(giaoVien);            // super = gọi constructor cha
    }
}

// static — gọi KHÔNG cần tạo đối tượng
System.out.println(Lop.soHocSinh);  // gọi trực tiếp trên class
```

| Từ khoá | Trên biến | Trên method | Trên class |
|---|---|---|---|
| `final` | Không gán lại được | Không ghi đè được | Không kế thừa được |
| `static` | Chung cho mọi đối tượng | Thuộc về class, không cần đối tượng | Chỉ dùng cho inner class |

---

### Java 8+ Features — Tính Năng Mới

---

#### Lambda Expressions

- [ ] **Lambda — viết function ngắn gọn**

> *Lambda là cách viết hàm "không tên" siêu ngắn. Thay vì viết cả class chỉ để làm 1 việc, bạn viết 1 dòng.*

**Hình dung như này:** Thay vì viết thư tay dài dòng (anonymous class), bạn gửi tin nhắn ngắn (lambda).

```java
// TRƯỚC Java 8 — "viết thư tay" dài dòng
Comparator<String> comp = new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
};

// SAU Java 8 — "gửi tin nhắn" ngắn gọn
Comparator<String> comp = (a, b) -> a.compareTo(b);

// Ứng dụng hàng ngày:
List<String> ten = Arrays.asList("Cường", "An", "Bình");
ten.forEach(t -> System.out.println(t));          // in từng tên
ten.sort((a, b) -> a.compareTo(b));               // sắp xếp
```

---

#### Stream API

- [ ] **Stream — xử lý danh sách theo "dòng chảy"**

> *Stream giống như dây chuyền nhà máy: nguyên liệu (data) đi qua nhiều công đoạn (filter, map, sort...) và ra thành phẩm.*

```java
List<Integer> diem = Arrays.asList(3, 7, 5, 9, 2, 8, 6, 4);

// Tìm các điểm >= 5, sắp xếp tăng dần, in ra
diem.stream()                          // bắt đầu dây chuyền
    .filter(d -> d >= 5)               // lọc: chỉ lấy điểm >= 5
    .sorted()                          // sắp xếp: 5, 6, 7, 8, 9
    .forEach(d -> System.out.print(d + " "));

// Tính tổng điểm
int tong = diem.stream()
    .reduce(0, Integer::sum);          // 0 + 3 + 7 + ... = 44

// Lấy danh sách tên sinh viên điểm cao
List<String> gioi = sinhViens.stream()
    .filter(sv -> sv.diem >= 8.0)      // lọc sinh viên giỏi
    .map(sv -> sv.ten)                 // lấy tên
    .collect(Collectors.toList());     // gom thành List
```

---

#### Optional

- [ ] **Optional — tránh NullPointerException**

> *Optional giống như "hộp quà" — có thể có quà bên trong, hoặc rỗng. Bạn phải kiểm tra trước khi mở.*

```java
// Thay vì:
String ten = layTen();       // có thể trả về null!
ten.toUpperCase();           // NẾU null → NullPointerException!

// Dùng Optional:
Optional<String> ten = Optional.ofNullable(layTen());
String ketQua = ten.orElse("Không rõ");           // nếu null thì dùng "Không rõ"
ten.ifPresent(t -> System.out.println(t));         // chỉ in nếu có giá trị
String inHoa = ten.map(String::toUpperCase)
                  .orElse("N/A");
```

---

### Basic Multithreading — Đa Luồng Cơ Bản

- [ ] **Thread vs Runnable**

> *Đa luồng giống như một quán ăn có nhiều nhân viên phục vụ cùng lúc, thay vì chỉ có 1 người.*

```java
// Cách 1: extends Thread
class NhanVien extends Thread {
    public void run() {
        System.out.println("Nhân viên đang phục vụ...");
    }
}
new NhanVien().start();

// Cách 2: implements Runnable (TỐT HƠN — vì còn có thể extends class khác)
Runnable viecLam = () -> System.out.println("Đang làm việc...");
new Thread(viecLam).start();

// synchronized — đảm bảo chỉ 1 luồng được truy cập tại 1 thời điểm
// Giống như phòng tắm chỉ có 1 người vào
synchronized void rutTien() {
    soDu -= soTien;
}
```

---

## Checklist Cuối Ngày 1

- [ ] Tôi có thể giải thích 4 trụ OOP bằng tiếng Anh và tiếng Việt
- [ ] Tôi hiểu sự khác nhau giữa abstract class và interface
- [ ] Tôi biết khi nào dùng ArrayList, LinkedList, HashMap, HashSet
- [ ] Tôi hiểu == vs .equals(), String vs StringBuilder
- [ ] Tôi biết try-catch-finally và checked vs unchecked exception
- [ ] Tôi có thể viết lambda và dùng Stream API cơ bản
