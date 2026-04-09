# Day 1: Java Fundamentals (5 hours / 5 giờ)

> *Day 1: Core Java foundations — deep understanding of OOP concepts, keywords, error handling, and important data types.*
>
> *Ngày 1: Nền tảng Java cơ bản — hiểu sâu các khái niệm OOP, từ khoá, xử lý lỗi, và các kiểu dữ liệu quan trọng.*

---

## Block 1 (2.5h) — Core Java / Java Cơ Bản

---

### 1. OOP — Object-Oriented Programming / Lập Trình Hướng Đối Tượng

> *OOP is a way of organizing code around "objects" — just like in real life, everything is an object with properties and actions.*
>
> *OOP là cách tổ chức code theo "đối tượng" — giống như ngoài đời thực, mọi thứ đều là một đối tượng có thuộc tính và hành động.*

---

#### Encapsulation — Đóng Gói

- [ ] **Encapsulation / Đóng gói**

> *Encapsulation means hiding internal data and only allowing outside access through controlled "doors" (methods).*
>
> *Đóng gói là giấu thông tin bên trong và chỉ cho người ngoài truy cập qua các "cửa" (method) mà mình cho phép.*

**Imagine this:** Think of an **ATM machine**. You can't open it and take money directly. You must press buttons (methods) to withdraw, and the ATM checks your balance (private field) for you.

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

**Why?** Protects data from being changed incorrectly. Like a bank doesn't let you edit your own balance.

**Tại sao cần?** Bảo vệ dữ liệu, tránh bị thay đổi sai. Giống như ngân hàng không cho bạn tự sửa số dư.

---

#### Inheritance — Kế Thừa

- [ ] **Inheritance / Kế thừa**

> *Inheritance is when a "child" class inherits all properties and actions from a "parent" class, and can add new ones or change existing ones.*
>
> *Kế thừa là khi một class "con" được thừa hưởng tất cả thuộc tính và hành động của class "cha", và có thể thêm cái mới hoặc thay đổi cái cũ.*

**Imagine this:** Think of a **family**. Children inherit genes from their parents (eye color, height), but children can also have their own unique traits (talents, hobbies).

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

**Why?** Code reuse — no need to rewrite `an()` and `ngu()` for every type of animal.

**Tại sao cần?** Tái sử dụng code — không cần viết lại `an()` và `ngu()` cho mỗi loài động vật.

---

#### Polymorphism — Đa Hình

- [ ] **Polymorphism / Đa hình**

> *Polymorphism means "the same action but each object performs it differently".*
>
> *Đa hình là "cùng một hành động nhưng mỗi đối tượng thực hiện khác nhau".*

**Imagine this:** Think of the **"Play" button** on your phone. Pressing Play on Spotify plays music, pressing Play on YouTube plays video, pressing Play on a game starts the game. **Same "Play" button**, but each app does it differently.

**Hình dung như này:** Nghĩ về nút **"Play"** trên điện thoại. Bấm Play trên Spotify thì phát nhạc, bấm Play trên YouTube thì phát video, bấm Play trên game thì bắt đầu chơi. **Cùng một nút "Play"**, nhưng mỗi app làm khác nhau.

**2 types / 2 loại:**

**a) Overloading — same name, different parameters / Nạp chồng — cùng tên, khác tham số:**
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

**b) Overriding — child class does it differently from parent class / Ghi đè — class con làm khác class cha:**
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
        System.out.println("Gau gau!");  // Chó kêu khác
    }
}

// Đây là "phép màu" của đa hình:
DongVat a = new Meo();  // biến kiểu DongVat, nhưng đối tượng là Meo
DongVat b = new Cho();  // biến kiểu DongVat, nhưng đối tượng là Cho
a.keu();  // "Meo meo!"  — Java biết gọi method của Meo
b.keu();  // "Gau gau!"  — Java biết gọi method của Cho
```

---

#### Abstraction — Trừu Tượng

- [ ] **Abstraction / Trừu tượng**

> *Abstraction means showing only "what needs to be done" while hiding "how it is done".*
>
> *Trừu tượng là chỉ cho thấy "cần làm gì" mà giấu đi "làm như thế nào".*

**Imagine this:** When you **drive a car**, you only need to know: press gas to accelerate, press brake to stop. You don't need to know how the engine works internally. The "hiding" of the internals is abstraction.

**Hình dung như này:** Khi bạn **lái xe**, bạn chỉ cần biết: bấm ga để tăng tốc, bấm thắng để dừng. Bạn không cần biết bên trong động cơ hoạt động ra sao. Cái "giấu đi" phía bên trong đó chính là trừu tượng.

```java
// Abstract class — như bản vẽ thiết kế, chưa phải sản phẩm hoàn chỉnh
abstract class PhuongTien {
    String ten;

    // Abstract method — chỉ nói "phải làm gì", CHƯA nói "làm thế nào"
    abstract void diChuyen();

    // Normal method — đã có sẵn cách làm
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

- [ ] **When to use which? / Khi nào dùng cái nào?**

> *Abstract class is like a "blueprint with some parts already built". Interface is like a "contract — it only says what must be done, nothing is pre-built".*
>
> *Abstract class giống như "bản vẽ thiết kế có sẵn một số phần đã làm". Interface giống như "hợp đồng — chỉ nói phải làm gì, không làm sẵn gì cả".*

**Imagine this / Hình dung như này:**
- **Abstract class** = You buy an unfinished house (walls and floors are ready), you just need to decorate. **Shares common properties.**
- **Abstract class** = Bạn mua nhà thô (có sẵn tường, sàn), bạn chỉ cần trang trí thêm. **Chia sẻ thuộc tính chung.**
- **Interface** = You sign a contract with the landlord "must pay electricity every month". The contract only states "what to do", not "how to do it". **Defines capabilities.**
- **Interface** = Bạn ký hợp đồng với chủ nhà "phải trả tiền điện mỗi tháng". Hợp đồng chỉ ghi "phải làm gì", không ghi "làm thế nào". **Định nghĩa khả năng.**

| Feature / Đặc điểm | Abstract Class | Interface |
|---|---|---|
| Method | Can have implemented methods + abstract methods / Có thể có method đã viết sẵn + method trừu tượng | Only abstract methods (before Java 8) / Chỉ có method trừu tượng (trước Java 8) |
| Properties / Thuộc tính | Can have normal variables / Có thể có biến bình thường | Only constants (`public static final`) / Chỉ có hằng số (`public static final`) |
| Constructor | Yes / Có | No / Không |
| Inheritance / Kế thừa | Extend only 1 (`extends`) / Chỉ kế thừa 1 (`extends`) | Implement many (`implements`) / Implement nhiều (`implements`) |
| Use when / Dùng khi | Child classes share common features / Các class con có điểm chung | Define "capabilities" that many classes can have / Định nghĩa "khả năng" mà nhiều class có thể làm |

```java
// Abstract class — phương tiện có chung "tên" và "dừng()"
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

- [ ] **4 access levels / 4 mức độ truy cập**

> *Like the security layers of a building.*
>
> *Giống như các lớp bảo mật của một toà nhà.*

**Imagine this / Hình dung như này:**
- `public` = **Front door** — anyone can enter / **Cửa chính** — ai cũng vào được
- `protected` = **Employee + family badge** — employees and family (child classes) can enter / **Thẻ nhân viên + gia đình** — nhân viên và người nhà (class con) mới vào
- default (nothing written) = **Employee badge** — only employees in the same company (package) can enter / **Thẻ nhân viên** — chỉ nhân viên cùng công ty (package) mới vào
- `private` = **Locked private room** — only yourself (that class) can enter / **Phòng riêng có khoá** — chỉ chính mình (class đó) mới vào

| Modifier | In class / Trong class | Same package / Cùng package | Child class / Class con | Everywhere / Mọi nơi |
|---|---|---|---|---|
| `public` | OK | OK | OK | OK |
| `protected` | OK | OK | OK | NO / KHÔNG |
| default | OK | OK | NO / KHÔNG | NO / KHÔNG |
| `private` | OK | NO / KHÔNG | NO / KHÔNG | NO / KHÔNG |

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

- [ ] **3 ways to work with strings / 3 cách làm việc với chuỗi**

> *String is like writing with a pen (can't erase, have to write a new page to fix it). StringBuilder is like writing with a pencil (easy to erase and fix, but only one person writes). StringBuffer is like a whiteboard (can erase and fix, and multiple people can safely write at the same time).*
>
> *String giống như viết bút bi (không xoá được, muốn sửa phải viết trang mới). StringBuilder giống như viết bút chì (xoá sửa thoải mái, nhưng chỉ 1 người viết). StringBuffer giống như bảng trắng (xoá sửa được, nhiều người có thể viết cùng lúc an toàn).*

| | String | StringBuilder | StringBuffer |
|---|---|---|---|
| Mutable? / Thay đổi được? | NO (immutable) / KHÔNG (immutable) | YES (mutable) / CÓ (mutable) | YES (mutable) / CÓ (mutable) |
| Thread-safe? / An toàn đa luồng? | YES (because immutable) / CÓ (vì không đổi) | NO / KHÔNG | YES (synchronized) / CÓ (synchronized) |
| Concatenation speed / Tốc độ nối chuỗi | SLOW / CHẬM | FASTEST / NHANH NHẤT | SLOWER than StringBuilder / CHẬM hơn StringBuilder |
| When to use? / Khi nào dùng? | Strings that rarely change / Chuỗi ít thay đổi | Lots of concatenation (single-thread) / Nối chuỗi nhiều (1 luồng) | Lots of concatenation (multi-thread) / Nối chuỗi nhiều (đa luồng) |

```java
// String — mỗi lần "+" tạo ra object MỚI (tốn bộ nhớ)
String s = "Xin";
s = s + " chao";  // tạo String mới "Xin chào", String cũ "Xin" bị bỏ
s = s + " ban";   // lại tạo String mới "Xin chào bạn"
// => Tạo 3 object! Rất tốn bộ nhớ nếu làm nhiều

// StringBuilder — chỉnh sửa NGAY TRÊN object cũ (nhanh, tiết kiệm)
StringBuilder sb = new StringBuilder("Xin");
sb.append(" chao");  // vẫn là object cũ, chỉ thêm vào
sb.append(" ban");   // vẫn là object cũ
String ketQua = sb.toString();  // "Xin chao ban"
// => Chỉ 1 object từ đầu đến cuối!
```

**Interview tip:** Use StringBuilder when concatenating many strings in a loop, use String for strings that rarely change.

**Mẹo nhớ:** Phỏng vấn hỏi -> trả lời "dùng StringBuilder khi nối nhiều chuỗi trong vòng lặp, dùng String cho chuỗi ít thay đổi".

---

### == vs .equals() vs hashCode()

- [ ] **Comparison in Java / So sánh trong Java**

> *`==` asks "are these two the SAME THING?" (same address). `.equals()` asks "are these two IDENTICAL?" (same content).*
>
> *`==` hỏi "hai cái này có phải CÙNG MỘT THỨ không?" (cùng địa chỉ). `.equals()` hỏi "hai cái này có GIỐNG NHAU không?" (cùng nội dung).*

**Imagine this:** You and your friend both have a black iPhone 15.
- `==` asks: "Are these two phones the SAME ONE?" -> **NO**, they are 2 different phones
- `.equals()` asks: "Are these two phones IDENTICAL?" -> **YES**, same model, same color

**Hình dung như này:** Bạn và bạn bạn cùng có iPhone 15 màu đen.
- `==` hỏi: "Hai cái điện thoại này có phải LÀ MỘT cái không?" -> **KHÔNG**, là 2 cái khác nhau
- `.equals()` hỏi: "Hai cái điện thoại này có GIỐNG nhau không?" -> **CÓ**, cùng model, cùng màu

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

**Interview tip:** ALWAYS use `.equals()` to compare String content. Only use `==` for primitives (int, double, boolean...).

**Mẹo phỏng vấn:** LUÔN dùng `.equals()` để so sánh nội dung String. Chỉ dùng `==` cho kiểu nguyên thuỷ (int, double, boolean...).

---

### Exception Handling — Xử Lý Lỗi

- [ ] **Checked vs Unchecked Exception**

> *An Exception is an error that occurs while a program is running. Like when you're driving, you might encounter: a red light (checked — predictable, must prepare), or a dog jumping out (unchecked — unexpected, can't anticipate).*
>
> *Exception là lỗi xảy ra khi chương trình đang chạy. Giống như khi bạn đang lái xe, có thể gặp: đèn đỏ (checked — biết trước, phải chuẩn bị), hoặc chó vọt ra (unchecked — bất ngờ, không lường trước).*

**Imagine this / Hình dung như này:**
- **Checked Exception** = **Red light, barrier** — you KNOW IN ADVANCE it might happen, MUST prepare to handle it (try-catch or throws). E.g.: reading a file that might not exist (`IOException`).
- **Checked Exception** = **Đèn đỏ, ba-ri-e** — bạn BIẾT TRƯỚC có thể gặp, PHẢI chuẩn bị xử lý (try-catch hoặc throws). VD: đọc file có thể không tìm thấy file (`IOException`).
- **Unchecked Exception** = **A pothole that appears suddenly** — unpredictable, usually caused by programming mistakes. E.g.: divide by 0 (`ArithmeticException`), calling a method on null (`NullPointerException`).
- **Unchecked Exception** = **Ổ gà bất ngờ chạy ra** — không lường trước, thường do lỗi lập trình. VD: chia cho 0 (`ArithmeticException`), gọi method trên null (`NullPointerException`).
- **Error** = **Earthquake** — too serious, should not be caught. E.g.: out of RAM (`OutOfMemoryError`).
- **Error** = **Động đất** — quá nghiêm trọng, không nên bắt. VD: hết RAM (`OutOfMemoryError`).

```
Throwable (root / gốc)
+-- Exception (errors that can be handled / lỗi có thể xử lý)
|   +-- IOException, SQLException...         <-- Checked (MUST catch / PHẢI bắt)
|   +-- RuntimeException                     <-- Unchecked (NOT required / KHÔNG bắt buộc)
|       +-- NullPointerException
|       +-- ArrayIndexOutOfBoundsException
|       +-- ArithmeticException
+-- Error (too serious, should NOT catch / quá nghiêm trọng, KHÔNG nên bắt)
    +-- OutOfMemoryError
    +-- StackOverflowError
```

```java
// try-catch-finally giống như:
// try    = "try doing this" / "thử làm cái này"
// catch  = "if error, handle it like this" / "nếu lỗi thì xử lý như này"
// finally = "do this no matter what at the end" / "dù gì cũng làm cái này cuối cùng"

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

### Collections Framework — Data Structures / Các Cấu Trúc Dữ Liệu

- [ ] **List, Set, Map — the three pillars of Collections / ba anh em nhà Collections**

> *Think of Collections as different types of "storage containers", each with its own characteristics.*
>
> *Nghĩ về Collections như các loại "hộp đựng đồ" khác nhau, mỗi loại có đặc điểm riêng.*

**Imagine this / Hình dung như này:**
- **List** = **Shopping list** — ordered, allows duplicates (buying 2 kg of rice is OK). *Ordered list, allows duplicate elements.*
- **List** = **Danh sách đi chợ** — có thứ tự, cho phép trùng lặp (mua 2 kg gạo OK). *Danh sách có thứ tự, cho phép phần tử trùng.*
- **Set** = **Stamp collection** — NO duplicates (each stamp is unique). *Collection that doesn't allow duplicates.*
- **Set** = **Bộ sưu tập tem** — KHÔNG cho trùng (mỗi con tem là duy nhất). *Tập hợp không cho phép trùng.*
- **Map** = **Phone contacts** — each name (key) maps to 1 phone number (value). *Key-value pairs, keys are unique.*
- **Map** = **Danh bạ điện thoại** — mỗi tên (key) ứng với 1 số điện thoại (value). *Cặp key-value, key không trùng.*

```
List (ordered, allows duplicates / có thứ tự, cho trùng)
+-- ArrayList  — like an auto-growing array / giống mảng có thể lớn dần
|   Fast access O(1), slow insert/delete O(n)
|   Truy cập nhanh O(1), chèn/xoá chậm O(n)
|   Use when: read-heavy, few mid-list insert/delete
|   Dùng khi: đọc nhiều, ít chèn/xoá giữa
|
+-- LinkedList — like a chain of links / giống chuỗi mắt xích
    Slow access O(n), fast insert/delete O(1)
    Truy cập chậm O(n), chèn/xoá nhanh O(1)
    Use when: frequent insert/delete at head/middle
    Dùng khi: chèn/xoá nhiều ở đầu/giữa

Set (no duplicates / không trùng)
+-- HashSet       — fastest, NO ordering / nhanh nhất, KHÔNG có thứ tự
+-- LinkedHashSet — preserves insertion order / giữ thứ tự chèn vào
+-- TreeSet       — auto-sorted / tự động sắp xếp

Map (key -> value)
+-- HashMap       — fastest, NO ordering / nhanh nhất, KHÔNG có thứ tự
+-- LinkedHashMap — preserves insertion order / giữ thứ tự chèn vào
+-- TreeMap       — sorted by key / sắp xếp theo key
```

```java
// === LIST — Shopping list / Danh sách đi chợ ===
List<String> diCho = new ArrayList<>();
diCho.add("Gao");
diCho.add("Thit");
diCho.add("Gao");    // OK! cho trùng lặp
// diCho = ["Gao", "Thit", "Gao"]
diCho.get(0);         // "Gao" — truy cập theo index

// === SET — Stamp collection / Bộ sưu tập tem ===
Set<String> tem = new HashSet<>();
tem.add("Tem Viet Nam");
tem.add("Tem Nhat Ban");
tem.add("Tem Viet Nam");  // KHÔNG thêm! đã có rồi
// tem = {"Tem Viet Nam", "Tem Nhat Ban"} — chỉ 2 phần tử

// === MAP — Phone contacts / Danh bạ điện thoại ===
Map<String, String> danhBa = new HashMap<>();
danhBa.put("Me", "0901234567");
danhBa.put("Ba", "0907654321");
danhBa.get("Me");     // "0901234567"
danhBa.getOrDefault("Chi", "Không có"); // "Không có"

// Duyệt qua Map
for (Map.Entry<String, String> entry : danhBa.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```

**Interview tip:** "ArrayList for fast access, LinkedList for fast insert/delete. HashMap when you need to look up by key, TreeMap when you need sorting."

**Mẹo phỏng vấn:** "ArrayList cho truy cập nhanh, LinkedList cho chèn/xoá nhanh. HashMap khi cần tìm theo key, TreeMap khi cần sắp xếp."

---

### Comparable vs Comparator

- [ ] **2 ways to sort / 2 cách sắp xếp**

> *Comparable = "I know how to compare myself with others". Comparator = "ask someone else to compare for me".*
>
> *Comparable = "tôi tự biết cách so sánh mình với người khác". Comparator = "nhờ người khác so sánh giúp".*

**Imagine this / Hình dung như này:**
- **Comparable** = A student knows how to compare their own score with another student (natural ordering, default)
- **Comparable** = Học sinh tự biết so điểm của mình với bạn khác (so sánh tự nhiên, mặc định)
- **Comparator** = A teacher decides which criteria to sort by: by score, by name, by age...
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

### Generics — Generic Types / Kiểu Tổng Quát

- [ ] **Why do we need Generics? / Tại sao cần Generics?**

> *Generics are like "labels" on a box — you know in advance what's inside, avoiding mistakes.*
>
> *Generics giống như "nhãn dán" trên hộp — biết trước bên trong là gì, tránh nhầm.*

**Imagine this:** Think of **storage boxes**. A box without a label could contain anything when you open it (dangerous!). A box labeled "BOOKS" guarantees books inside.

**Hình dung như này:** Nghĩ về **hộp đựng đồ**. Hộp không dán nhãn thì bạn mở ra có thể là gì cũng được (nguy hiểm!). Hộp dán nhãn "SÁCH" thì bạn biết chắc bên trong là sách.

```java
// KHÔNG có Generics — giống hộp không dán nhãn
List hop = new ArrayList();
hop.add("Xin chao");
hop.add(123);         // chèn số vào cũng được! Nguy hiểm!
String s = (String) hop.get(1); // LỖI lúc chạy! 123 không phải String

// CÓ Generics — giống hộp dán nhãn "String"
List<String> hopSach = new ArrayList<>();
hopSach.add("Xin chao");
// hopSach.add(123);  // LỖI NGAY lúc viết code! Compiler báo lỗi
String s = hopSach.get(0);  // Không cần ép kiểu, an toàn
```

---

### Keywords: final, static, this, super

- [ ] **4 important keywords / 4 từ khoá quan trọng**

> *Each keyword has a different meaning depending on where it is used.*
>
> *Mỗi từ khoá có ý nghĩa khác nhau tuỳ vào chỗ dùng.*

**Imagine this / Hình dung như này:**
- `final` = **A signed contract** — cannot be changed anymore / **Hợp đồng đã ký** — không thay đổi được nữa
- `static` = **A shared bulletin board** — everyone can see it, belongs to the class (no need to create an object) / **Bảng thông báo chung** — ai cũng thấy, thuộc về lớp (không cần tạo đối tượng)
- `this` = **"Me"** — refers to the current object itself / **"Tôi"** — trỏ đến chính đối tượng hiện tại
- `super` = **"My parent"** — refers to the parent class / **"Cha tôi"** — trỏ đến class cha

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

| Keyword / Từ khoá | On variable / Trên biến | On method / Trên method | On class / Trên class |
|---|---|---|---|
| `final` | Cannot be reassigned / Không gán lại được | Cannot be overridden / Không ghi đè được | Cannot be inherited / Không kế thừa được |
| `static` | Shared across all objects / Chung cho mọi đối tượng | Belongs to the class, no object needed / Thuộc về class, không cần đối tượng | Only for inner classes / Chỉ dùng cho inner class |

---

### Java 8+ Features — New Features / Tính Năng Mới

---

#### Lambda Expressions

- [ ] **Lambda — writing functions in a concise way / viết function ngắn gọn**

> *Lambda is a way to write "anonymous" functions super concisely. Instead of writing a whole class just to do 1 thing, you write 1 line.*
>
> *Lambda là cách viết hàm "không tên" siêu ngắn. Thay vì viết cả class chỉ để làm 1 việc, bạn viết 1 dòng.*

**Imagine this:** Instead of writing a long handwritten letter (anonymous class), you send a short text message (lambda).

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
List<String> ten = Arrays.asList("Cuong", "An", "Binh");
ten.forEach(t -> System.out.println(t));          // in từng tên
ten.sort((a, b) -> a.compareTo(b));               // sắp xếp
```

---

#### Stream API

- [ ] **Stream — processing lists as a "flow" / xử lý danh sách theo "dòng chảy"**

> *Stream is like a factory assembly line: raw materials (data) go through multiple stages (filter, map, sort...) and produce a finished product.*
>
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

- [ ] **Optional — avoiding NullPointerException / tránh NullPointerException**

> *Optional is like a "gift box" — it might have a gift inside, or it might be empty. You must check before opening.*
>
> *Optional giống như "hộp quà" — có thể có quà bên trong, hoặc rỗng. Bạn phải kiểm tra trước khi mở.*

```java
// Thay vì:
String ten = layTen();       // có thể trả về null!
ten.toUpperCase();           // NẾU null -> NullPointerException!

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

> *Multithreading is like a restaurant with many servers working at the same time, instead of just one person.*
>
> *Đa luồng giống như một quán ăn có nhiều nhân viên phục vụ cùng lúc, thay vì chỉ có 1 người.*

```java
// Cách 1: extends Thread
class NhanVien extends Thread {
    public void run() {
        System.out.println("Nhân viên đang phục vụ...");
    }
}
new NhanVien().start();

// Cách 2: implements Runnable (BETTER — because you can still extend another class)
// Cách 2: implements Runnable (TỐT HƠN — vì còn có thể extends class khác)
Runnable viecLam = () -> System.out.println("Đang làm việc...");
new Thread(viecLam).start();

// synchronized — ensures only 1 thread can access at a time
// synchronized — đảm bảo chỉ 1 luồng được truy cập tại 1 thời điểm
// Like a bathroom that only allows 1 person in
// Giống như phòng tắm chỉ có 1 người vào
synchronized void rutTien() {
    soDu -= soTien;
}
```

---

## End of Day 1 Checklist / Checklist Cuối Ngày 1

- [ ] I can explain the 4 OOP pillars in both English and Vietnamese / Tôi có thể giải thích 4 trụ OOP bằng tiếng Anh và tiếng Việt
- [ ] I understand the difference between abstract class and interface / Tôi hiểu sự khác nhau giữa abstract class và interface
- [ ] I know when to use ArrayList, LinkedList, HashMap, HashSet / Tôi biết khi nào dùng ArrayList, LinkedList, HashMap, HashSet
- [ ] I understand == vs .equals(), String vs StringBuilder / Tôi hiểu == vs .equals(), String vs StringBuilder
- [ ] I know try-catch-finally and checked vs unchecked exceptions / Tôi biết try-catch-finally và checked vs unchecked exception
- [ ] I can write lambdas and use basic Stream API / Tôi có thể viết lambda và dùng Stream API cơ bản
