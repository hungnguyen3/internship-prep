# Day 1: Java Fundamentals (5 hours / 5 gio)

> *Day 1: Core Java foundations — deep understanding of OOP concepts, keywords, error handling, and important data types.*
>
> *Ngay 1: Nen tang Java co ban — hieu sau cac khai niem OOP, tu khoa, xu ly loi, va cac kieu du lieu quan trong.*

---

## Block 1 (2.5h) — Core Java / Java Co Ban

---

### 1. OOP — Object-Oriented Programming / Lap Trinh Huong Doi Tuong

> *OOP is a way of organizing code around "objects" — just like in real life, everything is an object with properties and actions.*
>
> *OOP la cach to chuc code theo "doi tuong" — giong nhu ngoai doi thuc, moi thu deu la mot doi tuong co thuoc tinh va hanh dong.*

---

#### Encapsulation — Dong Goi

- [ ] **Encapsulation / Dong goi**

> *Encapsulation means hiding internal data and only allowing outside access through controlled "doors" (methods).*
>
> *Dong goi la giau thong tin ben trong va chi cho nguoi ngoai truy cap qua cac "cua" (method) ma minh cho phep.*

**Imagine this:** Think of an **ATM machine**. You can't open it and take money directly. You must press buttons (methods) to withdraw, and the ATM checks your balance (private field) for you.

**Hinh dung nhu nay:** Nghi ve mot **cay ATM**. Ban khong the mo may ATM ra va tu lay tien. Ban phai bam nut (method) de rut tien, va may ATM tu kiem tra so du (private field) cho ban.

```java
public class ATM {
    private double soDu;  // nguoi ngoai KHONG the truc tiep thay doi so du

    public double xemSoDu() {
        return soDu;       // chi xem duoc qua method nay
    }

    public void rutTien(double soTien) {
        if (soTien > 0 && soTien <= soDu) {
            soDu -= soTien;  // may ATM tu tru tien
        }
    }
}
// Ban KHONG the lam: atm.soDu = 1000000; <-- LOI! private
// Ban CHI co the:     atm.rutTien(500);   <-- OK, qua method
```

**Why?** Protects data from being changed incorrectly. Like a bank doesn't let you edit your own balance.

**Tai sao can?** Bao ve du lieu, tranh bi thay doi sai. Giong nhu ngan hang khong cho ban tu sua so du.

---

#### Inheritance — Ke Thua

- [ ] **Inheritance / Ke thua**

> *Inheritance is when a "child" class inherits all properties and actions from a "parent" class, and can add new ones or change existing ones.*
>
> *Ke thua la khi mot class "con" duoc thua huong tat ca thuoc tinh va hanh dong cua class "cha", va co the them cai moi hoac thay doi cai cu.*

**Imagine this:** Think of a **family**. Children inherit genes from their parents (eye color, height), but children can also have their own unique traits (talents, hobbies).

**Hinh dung nhu nay:** Nghi ve **gia dinh**. Con cai ke thua gen tu cha me (mau mat, chieu cao), nhung con co the co them dac diem rieng (tai nang, so thich).

```java
// Cha — Dong Vat co the an, ngu
public class DongVat {
    String ten;

    public void an() {
        System.out.println(ten + " dang an");
    }

    public void ngu() {
        System.out.println(ten + " dang ngu");
    }
}

// Con — Cho ke thua an, ngu TU DongVat, va them sua (bark)
public class Cho extends DongVat {
    public void sua() {
        System.out.println(ten + " dang sua: Gau gau!");
    }
}

// Su dung:
Cho cun = new Cho();
cun.ten = "Lucky";
cun.an();   // "Lucky dang an"   <-- ke thua tu DongVat
cun.ngu();  // "Lucky dang ngu"  <-- ke thua tu DongVat
cun.sua();  // "Lucky dang sua: Gau gau!"  <-- rieng cua Cho
```

**Why?** Code reuse — no need to rewrite `an()` and `ngu()` for every type of animal.

**Tai sao can?** Tai su dung code — khong can viet lai `an()` va `ngu()` cho moi loai dong vat.

---

#### Polymorphism — Da Hinh

- [ ] **Polymorphism / Da hinh**

> *Polymorphism means "the same action but each object performs it differently".*
>
> *Da hinh la "cung mot hanh dong nhung moi doi tuong thuc hien khac nhau".*

**Imagine this:** Think of the **"Play" button** on your phone. Pressing Play on Spotify plays music, pressing Play on YouTube plays video, pressing Play on a game starts the game. **Same "Play" button**, but each app does it differently.

**Hinh dung nhu nay:** Nghi ve nut **"Play"** tren dien thoai. Bam Play tren Spotify thi phat nhac, bam Play tren YouTube thi phat video, bam Play tren game thi bat dau choi. **Cung mot nut "Play"**, nhung moi app lam khac nhau.

**2 types / 2 loai:**

**a) Overloading — same name, different parameters / Nap chong — cung ten, khac tham so:**
```java
// Giong nhu quan com co nhieu loai com:
// goi "com" thi ra com trang, goi "com ga" thi ra com ga
class QuanCom {
    void nauCom() {
        System.out.println("Com trang");
    }
    void nauCom(String loai) {
        System.out.println("Com " + loai);  // "Com ga"
    }
    void nauCom(String loai, int soLuong) {
        System.out.println(soLuong + " dia com " + loai);
    }
}
```

**b) Overriding — child class does it differently from parent class / Ghi de — class con lam khac class cha:**
```java
class DongVat {
    void keu() {
        System.out.println("...");
    }
}

class Meo extends DongVat {
    @Override
    void keu() {
        System.out.println("Meo meo!");  // Meo keu khac
    }
}

class Cho extends DongVat {
    @Override
    void keu() {
        System.out.println("Gau gau!");  // Cho keu khac
    }
}

// Day la "phep mau" cua da hinh:
DongVat a = new Meo();  // bien kieu DongVat, nhung doi tuong la Meo
DongVat b = new Cho();  // bien kieu DongVat, nhung doi tuong la Cho
a.keu();  // "Meo meo!"  — Java biet goi method cua Meo
b.keu();  // "Gau gau!"  — Java biet goi method cua Cho
```

---

#### Abstraction — Truu Tuong

- [ ] **Abstraction / Truu tuong**

> *Abstraction means showing only "what needs to be done" while hiding "how it is done".*
>
> *Truu tuong la chi cho thay "can lam gi" ma giau di "lam nhu the nao".*

**Imagine this:** When you **drive a car**, you only need to know: press gas to accelerate, press brake to stop. You don't need to know how the engine works internally. The "hiding" of the internals is abstraction.

**Hinh dung nhu nay:** Khi ban **lai xe**, ban chi can biet: bam ga de tang toc, bam thang de dung. Ban khong can biet ben trong dong co hoat dong ra sao. Cai "giau di" phia ben trong do chinh la truu tuong.

```java
// Abstract class — nhu ban ve thiet ke, chua phai san pham hoan chinh
abstract class PhuongTien {
    String ten;

    // Abstract method — chi noi "phai lam gi", CHUA noi "lam the nao"
    abstract void diChuyen();

    // Normal method — da co san cach lam
    void dung() {
        System.out.println(ten + " da dung lai");
    }
}

class OTo extends PhuongTien {
    @Override
    void diChuyen() {
        System.out.println(ten + " chay tren duong");  // O to tu dinh nghia cach di
    }
}

class Thuyen extends PhuongTien {
    @Override
    void diChuyen() {
        System.out.println(ten + " chay tren nuoc");   // Thuyen di khac o to
    }
}
```

---

### Abstract Class vs Interface

- [ ] **When to use which? / Khi nao dung cai nao?**

> *Abstract class is like a "blueprint with some parts already built". Interface is like a "contract — it only says what must be done, nothing is pre-built".*
>
> *Abstract class giong nhu "ban ve thiet ke co san mot so phan da lam". Interface giong nhu "hop dong — chi noi phai lam gi, khong lam san gi ca".*

**Imagine this / Hinh dung nhu nay:**
- **Abstract class** = You buy an unfinished house (walls and floors are ready), you just need to decorate. **Shares common properties.**
- **Abstract class** = Ban mua nha tho (co san tuong, san), ban chi can trang tri them. **Chia se thuoc tinh chung.**
- **Interface** = You sign a contract with the landlord "must pay electricity every month". The contract only states "what to do", not "how to do it". **Defines capabilities.**
- **Interface** = Ban ky hop dong voi chu nha "phai tra tien dien moi thang". Hop dong chi ghi "phai lam gi", khong ghi "lam the nao". **Dinh nghia kha nang.**

| Feature / Dac diem | Abstract Class | Interface |
|---|---|---|
| Method | Can have implemented methods + abstract methods / Co the co method da viet san + method truu tuong | Only abstract methods (before Java 8) / Chi co method truu tuong (truoc Java 8) |
| Properties / Thuoc tinh | Can have normal variables / Co the co bien binh thuong | Only constants (`public static final`) / Chi co hang so (`public static final`) |
| Constructor | Yes / Co | No / Khong |
| Inheritance / Ke thua | Extend only 1 (`extends`) / Chi ke thua 1 (`extends`) | Implement many (`implements`) / Implement nhieu (`implements`) |
| Use when / Dung khi | Child classes share common features / Cac class con co diem chung | Define "capabilities" that many classes can have / Dinh nghia "kha nang" ma nhieu class co the lam |

```java
// Abstract class — phuong tien co chung "ten" va "dung()"
abstract class PhuongTien {
    String ten;
    abstract void diChuyen();
    void dung() { System.out.println("Dung lai!"); }
}

// Interface — kha nang "co the sac dien"
interface CoTheSacDien {
    void sacPin();  // chi noi "phai co kha nang sac", khong noi cach sac
}

// O to dien: vua la phuong tien, vua co the sac dien
class OToDien extends PhuongTien implements CoTheSacDien {
    @Override
    void diChuyen() { System.out.println("Chay bang dien"); }

    @Override
    public void sacPin() { System.out.println("Dang sac..."); }
}
```

---

### Access Modifiers — Pham Vi Truy Cap

- [ ] **4 access levels / 4 muc do truy cap**

> *Like the security layers of a building.*
>
> *Giong nhu cac lop bao mat cua mot toa nha.*

**Imagine this / Hinh dung nhu nay:**
- `public` = **Front door** — anyone can enter / **Cua chinh** — ai cung vao duoc
- `protected` = **Employee + family badge** — employees and family (child classes) can enter / **The nhan vien + gia dinh** — nhan vien va nguoi nha (class con) moi vao
- default (nothing written) = **Employee badge** — only employees in the same company (package) can enter / **The nhan vien** — chi nhan vien cung cong ty (package) moi vao
- `private` = **Locked private room** — only yourself (that class) can enter / **Phong rieng co khoa** — chi chinh minh (class do) moi vao

| Modifier | In class / Trong class | Same package / Cung package | Child class / Class con | Everywhere / Moi noi |
|---|---|---|---|---|
| `public` | OK | OK | OK | OK |
| `protected` | OK | OK | OK | NO / KHONG |
| default | OK | OK | NO / KHONG | NO / KHONG |
| `private` | OK | NO / KHONG | NO / KHONG | NO / KHONG |

```java
public class NguoiDung {
    public String ten;           // ai cung thay
    protected String email;      // cung package + class con thay
    String soDienThoai;          // chi cung package thay (default)
    private String matKhau;      // chi class NguoiDung thay
}
```

---

### String vs StringBuilder vs StringBuffer

- [ ] **3 ways to work with strings / 3 cach lam viec voi chuoi**

> *String is like writing with a pen (can't erase, have to write a new page to fix it). StringBuilder is like writing with a pencil (easy to erase and fix, but only one person writes). StringBuffer is like a whiteboard (can erase and fix, and multiple people can safely write at the same time).*
>
> *String giong nhu viet but bi (khong xoa duoc, muon sua phai viet trang moi). StringBuilder giong nhu viet but chi (xoa sua thoai mai, nhung chi 1 nguoi viet). StringBuffer giong nhu bang trang (xoa sua duoc, nhieu nguoi co the viet cung luc an toan).*

| | String | StringBuilder | StringBuffer |
|---|---|---|---|
| Mutable? / Thay doi duoc? | NO (immutable) / KHONG (immutable) | YES (mutable) / CO (mutable) | YES (mutable) / CO (mutable) |
| Thread-safe? / An toan da luong? | YES (because immutable) / CO (vi khong doi) | NO / KHONG | YES (synchronized) / CO (synchronized) |
| Concatenation speed / Toc do noi chuoi | SLOW / CHAM | FASTEST / NHANH NHAT | SLOWER than StringBuilder / CHAM hon StringBuilder |
| When to use? / Khi nao dung? | Strings that rarely change / Chuoi it thay doi | Lots of concatenation (single-thread) / Noi chuoi nhieu (1 luong) | Lots of concatenation (multi-thread) / Noi chuoi nhieu (da luong) |

```java
// String — moi lan "+" tao ra object MOI (ton bo nho)
String s = "Xin";
s = s + " chao";  // tao String moi "Xin chao", String cu "Xin" bi bo
s = s + " ban";   // lai tao String moi "Xin chao ban"
// => Tao 3 object! Rat ton bo nho neu lam nhieu

// StringBuilder — chinh sua NGAY TREN object cu (nhanh, tiet kiem)
StringBuilder sb = new StringBuilder("Xin");
sb.append(" chao");  // van la object cu, chi them vao
sb.append(" ban");   // van la object cu
String ketQua = sb.toString();  // "Xin chao ban"
// => Chi 1 object tu dau den cuoi!
```

**Interview tip:** Use StringBuilder when concatenating many strings in a loop, use String for strings that rarely change.

**Meo nho:** Phong van hoi -> tra loi "dung StringBuilder khi noi nhieu chuoi trong vong lap, dung String cho chuoi it thay doi".

---

### == vs .equals() vs hashCode()

- [ ] **Comparison in Java / So sanh trong Java**

> *`==` asks "are these two the SAME THING?" (same address). `.equals()` asks "are these two IDENTICAL?" (same content).*
>
> *`==` hoi "hai cai nay co phai CUNG MOT THU khong?" (cung dia chi). `.equals()` hoi "hai cai nay co GIONG NHAU khong?" (cung noi dung).*

**Imagine this:** You and your friend both have a black iPhone 15.
- `==` asks: "Are these two phones the SAME ONE?" -> **NO**, they are 2 different phones
- `.equals()` asks: "Are these two phones IDENTICAL?" -> **YES**, same model, same color

**Hinh dung nhu nay:** Ban va ban ban cung co iPhone 15 mau den.
- `==` hoi: "Hai cai dien thoai nay co phai LA MOT cai khong?" -> **KHONG**, la 2 cai khac nhau
- `.equals()` hoi: "Hai cai dien thoai nay co GIONG nhau khong?" -> **CO**, cung model, cung mau

```java
// Tao 2 chuoi giong nhau nhung khac object
String a = new String("hello");
String b = new String("hello");

a == b;       // false — 2 object KHAC NHAU trong bo nho
a.equals(b);  // true  — CUNG NOI DUNG "hello"

// Dac biet: String pool (Java toi uu hoa)
String c = "hello";
String d = "hello";
c == d;       // true — Java tro ca 2 vao CUNG 1 cho trong String pool

// hashCode() — "ma so" cua object, dung cho HashMap/HashSet
// Quy tac: neu a.equals(b) == true thi a.hashCode() == b.hashCode()
```

**Interview tip:** ALWAYS use `.equals()` to compare String content. Only use `==` for primitives (int, double, boolean...).

**Meo phong van:** LUON dung `.equals()` de so sanh noi dung String. Chi dung `==` cho kieu nguyen thuy (int, double, boolean...).

---

### Exception Handling — Xu Ly Loi

- [ ] **Checked vs Unchecked Exception**

> *An Exception is an error that occurs while a program is running. Like when you're driving, you might encounter: a red light (checked — predictable, must prepare), or a dog jumping out (unchecked — unexpected, can't anticipate).*
>
> *Exception la loi xay ra khi chuong trinh dang chay. Giong nhu khi ban dang lai xe, co the gap: den do (checked — biet truoc, phai chuan bi), hoac cho vot ra (unchecked — bat ngo, khong luong truoc).*

**Imagine this / Hinh dung nhu nay:**
- **Checked Exception** = **Red light, barrier** — you KNOW IN ADVANCE it might happen, MUST prepare to handle it (try-catch or throws). E.g.: reading a file that might not exist (`IOException`).
- **Checked Exception** = **Den do, ba-ri-e** — ban BIET TRUOC co the gap, PHAI chuan bi xu ly (try-catch hoac throws). VD: doc file co the khong tim thay file (`IOException`).
- **Unchecked Exception** = **A pothole that appears suddenly** — unpredictable, usually caused by programming mistakes. E.g.: divide by 0 (`ArithmeticException`), calling a method on null (`NullPointerException`).
- **Unchecked Exception** = **O ga bat ngo chay ra** — khong luong truoc, thuong do loi lap trinh. VD: chia cho 0 (`ArithmeticException`), goi method tren null (`NullPointerException`).
- **Error** = **Earthquake** — too serious, should not be caught. E.g.: out of RAM (`OutOfMemoryError`).
- **Error** = **Dong dat** — qua nghiem trong, khong nen bat. VD: het RAM (`OutOfMemoryError`).

```
Throwable (root / goc)
+-- Exception (errors that can be handled / loi co the xu ly)
|   +-- IOException, SQLException...         <-- Checked (MUST catch / PHAI bat)
|   +-- RuntimeException                     <-- Unchecked (NOT required / KHONG bat buoc)
|       +-- NullPointerException
|       +-- ArrayIndexOutOfBoundsException
|       +-- ArithmeticException
+-- Error (too serious, should NOT catch / qua nghiem trong, KHONG nen bat)
    +-- OutOfMemoryError
    +-- StackOverflowError
```

```java
// try-catch-finally giong nhu:
// try    = "try doing this" / "thu lam cai nay"
// catch  = "if error, handle it like this" / "neu loi thi xu ly nhu nay"
// finally = "do this no matter what at the end" / "du gi cung lam cai nay cuoi cung"

try {
    int[] mang = {1, 2, 3};
    System.out.println(mang[10]);   // LOI! Chi co index 0-2
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Loi: Vuot qua chi so mang! " + e.getMessage());
} finally {
    System.out.println("Doan nay LUON chay, du co loi hay khong");
}

// Tu dinh nghia Exception rieng
class HetTienException extends Exception {
    public HetTienException(String msg) {
        super(msg);
    }
}

// Su dung:
void rutTien(double soTien) throws HetTienException {
    if (soTien > soDu) {
        throw new HetTienException("So du khong du!");
    }
    soDu -= soTien;
}
```

---

## Block 2 (2.5h) — Collections & Modern Java

---

### Collections Framework — Data Structures / Cac Cau Truc Du Lieu

- [ ] **List, Set, Map — the three pillars of Collections / ba anh em nha Collections**

> *Think of Collections as different types of "storage containers", each with its own characteristics.*
>
> *Nghi ve Collections nhu cac loai "hop dung do" khac nhau, moi loai co dac diem rieng.*

**Imagine this / Hinh dung nhu nay:**
- **List** = **Shopping list** — ordered, allows duplicates (buying 2 kg of rice is OK). *Ordered list, allows duplicate elements.*
- **List** = **Danh sach di cho** — co thu tu, cho phep trung lap (mua 2 kg gao OK). *Danh sach co thu tu, cho phep phan tu trung.*
- **Set** = **Stamp collection** — NO duplicates (each stamp is unique). *Collection that doesn't allow duplicates.*
- **Set** = **Bo suu tap tem** — KHONG cho trung (moi con tem la duy nhat). *Tap hop khong cho phep trung.*
- **Map** = **Phone contacts** — each name (key) maps to 1 phone number (value). *Key-value pairs, keys are unique.*
- **Map** = **Danh ba dien thoai** — moi ten (key) ung voi 1 so dien thoai (value). *Cap key-value, key khong trung.*

```
List (ordered, allows duplicates / co thu tu, cho trung)
+-- ArrayList  — like an auto-growing array / giong mang co the lon dan
|   Fast access O(1), slow insert/delete O(n)
|   Truy cap nhanh O(1), chen/xoa cham O(n)
|   Use when: read-heavy, few mid-list insert/delete
|   Dung khi: doc nhieu, it chen/xoa giua
|
+-- LinkedList — like a chain of links / giong chuoi mat xich
    Slow access O(n), fast insert/delete O(1)
    Truy cap cham O(n), chen/xoa nhanh O(1)
    Use when: frequent insert/delete at head/middle
    Dung khi: chen/xoa nhieu o dau/giua

Set (no duplicates / khong trung)
+-- HashSet       — fastest, NO ordering / nhanh nhat, KHONG co thu tu
+-- LinkedHashSet — preserves insertion order / giu thu tu chen vao
+-- TreeSet       — auto-sorted / tu dong sap xep

Map (key -> value)
+-- HashMap       — fastest, NO ordering / nhanh nhat, KHONG co thu tu
+-- LinkedHashMap — preserves insertion order / giu thu tu chen vao
+-- TreeMap       — sorted by key / sap xep theo key
```

```java
// === LIST — Shopping list / Danh sach di cho ===
List<String> diCho = new ArrayList<>();
diCho.add("Gao");
diCho.add("Thit");
diCho.add("Gao");    // OK! cho trung lap
// diCho = ["Gao", "Thit", "Gao"]
diCho.get(0);         // "Gao" — truy cap theo index

// === SET — Stamp collection / Bo suu tap tem ===
Set<String> tem = new HashSet<>();
tem.add("Tem Viet Nam");
tem.add("Tem Nhat Ban");
tem.add("Tem Viet Nam");  // KHONG them! da co roi
// tem = {"Tem Viet Nam", "Tem Nhat Ban"} — chi 2 phan tu

// === MAP — Phone contacts / Danh ba dien thoai ===
Map<String, String> danhBa = new HashMap<>();
danhBa.put("Me", "0901234567");
danhBa.put("Ba", "0907654321");
danhBa.get("Me");     // "0901234567"
danhBa.getOrDefault("Chi", "Khong co"); // "Khong co"

// Duyet qua Map
for (Map.Entry<String, String> entry : danhBa.entrySet()) {
    System.out.println(entry.getKey() + ": " + entry.getValue());
}
```

**Interview tip:** "ArrayList for fast access, LinkedList for fast insert/delete. HashMap when you need to look up by key, TreeMap when you need sorting."

**Meo phong van:** "ArrayList cho truy cap nhanh, LinkedList cho chen/xoa nhanh. HashMap khi can tim theo key, TreeMap khi can sap xep."

---

### Comparable vs Comparator

- [ ] **2 ways to sort / 2 cach sap xep**

> *Comparable = "I know how to compare myself with others". Comparator = "ask someone else to compare for me".*
>
> *Comparable = "toi tu biet cach so sanh minh voi nguoi khac". Comparator = "nho nguoi khac so sanh giup".*

**Imagine this / Hinh dung nhu nay:**
- **Comparable** = A student knows how to compare their own score with another student (natural ordering, default)
- **Comparable** = Hoc sinh tu biet so diem cua minh voi ban khac (so sanh tu nhien, mac dinh)
- **Comparator** = A teacher decides which criteria to sort by: by score, by name, by age...
- **Comparator** = Giao vien quyet dinh sap xep theo tieu chi nao: theo diem, theo ten, theo tuoi...

```java
// Comparable — class TU dinh nghia cach so sanh
class SinhVien implements Comparable<SinhVien> {
    String ten;
    double diem;

    @Override
    public int compareTo(SinhVien other) {
        // So sanh theo diem (tu nhien)
        return Double.compare(this.diem, other.diem);
    }
}
Collections.sort(danhSach); // tu dong dung compareTo

// Comparator — NGUOI NGOAI dinh nghia cach so sanh
// Muon sap xep theo ten thay vi diem? Dung Comparator:
danhSach.sort(Comparator.comparing(sv -> sv.ten));

// Sap xep theo diem giam dan?
danhSach.sort(Comparator.comparingDouble(sv -> sv.diem).reversed());
```

---

### Generics — Generic Types / Kieu Tong Quat

- [ ] **Why do we need Generics? / Tai sao can Generics?**

> *Generics are like "labels" on a box — you know in advance what's inside, avoiding mistakes.*
>
> *Generics giong nhu "nhan dan" tren hop — biet truoc ben trong la gi, tranh nham.*

**Imagine this:** Think of **storage boxes**. A box without a label could contain anything when you open it (dangerous!). A box labeled "BOOKS" guarantees books inside.

**Hinh dung nhu nay:** Nghi ve **hop dung do**. Hop khong dan nhan thi ban mo ra co the la gi cung duoc (nguy hiem!). Hop dan nhan "SACH" thi ban biet chac ben trong la sach.

```java
// KHONG co Generics — giong hop khong dan nhan
List hop = new ArrayList();
hop.add("Xin chao");
hop.add(123);         // chen so vao cung duoc! Nguy hiem!
String s = (String) hop.get(1); // LOI luc chay! 123 khong phai String

// CO Generics — giong hop dan nhan "String"
List<String> hopSach = new ArrayList<>();
hopSach.add("Xin chao");
// hopSach.add(123);  // LOI NGAY luc viet code! Compiler bao loi
String s = hopSach.get(0);  // Khong can ep kieu, an toan
```

---

### Keywords: final, static, this, super

- [ ] **4 important keywords / 4 tu khoa quan trong**

> *Each keyword has a different meaning depending on where it is used.*
>
> *Moi tu khoa co y nghia khac nhau tuy vao cho dung.*

**Imagine this / Hinh dung nhu nay:**
- `final` = **A signed contract** — cannot be changed anymore / **Hop dong da ky** — khong thay doi duoc nua
- `static` = **A shared bulletin board** — everyone can see it, belongs to the class (no need to create an object) / **Bang thong bao chung** — ai cung thay, thuoc ve lop (khong can tao doi tuong)
- `this` = **"Me"** — refers to the current object itself / **"Toi"** — tro den chinh doi tuong hien tai
- `super` = **"My parent"** — refers to the parent class / **"Cha toi"** — tro den class cha

```java
class Lop {
    static int soHocSinh = 0;      // CHUNG cho tat ca doi tuong Lop
    final String TEN_TRUONG = "NAB Academy";  // KHONG doi duoc

    String giaoVien;

    Lop(String giaoVien) {
        this.giaoVien = giaoVien;   // this = "toi" (doi tuong nay)
        soHocSinh++;
    }
}

class LopChuyenToan extends Lop {
    LopChuyenToan(String giaoVien) {
        super(giaoVien);            // super = goi constructor cha
    }
}

// static — goi KHONG can tao doi tuong
System.out.println(Lop.soHocSinh);  // goi truc tiep tren class
```

| Keyword / Tu khoa | On variable / Tren bien | On method / Tren method | On class / Tren class |
|---|---|---|---|
| `final` | Cannot be reassigned / Khong gan lai duoc | Cannot be overridden / Khong ghi de duoc | Cannot be inherited / Khong ke thua duoc |
| `static` | Shared across all objects / Chung cho moi doi tuong | Belongs to the class, no object needed / Thuoc ve class, khong can doi tuong | Only for inner classes / Chi dung cho inner class |

---

### Java 8+ Features — New Features / Tinh Nang Moi

---

#### Lambda Expressions

- [ ] **Lambda — writing functions in a concise way / viet function ngan gon**

> *Lambda is a way to write "anonymous" functions super concisely. Instead of writing a whole class just to do 1 thing, you write 1 line.*
>
> *Lambda la cach viet ham "khong ten" sieu ngan. Thay vi viet ca class chi de lam 1 viec, ban viet 1 dong.*

**Imagine this:** Instead of writing a long handwritten letter (anonymous class), you send a short text message (lambda).

**Hinh dung nhu nay:** Thay vi viet thu tay dai dong (anonymous class), ban gui tin nhan ngan (lambda).

```java
// TRUOC Java 8 — "viet thu tay" dai dong
Comparator<String> comp = new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return a.compareTo(b);
    }
};

// SAU Java 8 — "gui tin nhan" ngan gon
Comparator<String> comp = (a, b) -> a.compareTo(b);

// Ung dung hang ngay:
List<String> ten = Arrays.asList("Cuong", "An", "Binh");
ten.forEach(t -> System.out.println(t));          // in tung ten
ten.sort((a, b) -> a.compareTo(b));               // sap xep
```

---

#### Stream API

- [ ] **Stream — processing lists as a "flow" / xu ly danh sach theo "dong chay"**

> *Stream is like a factory assembly line: raw materials (data) go through multiple stages (filter, map, sort...) and produce a finished product.*
>
> *Stream giong nhu day chuyen nha may: nguyen lieu (data) di qua nhieu cong doan (filter, map, sort...) va ra thanh pham.*

```java
List<Integer> diem = Arrays.asList(3, 7, 5, 9, 2, 8, 6, 4);

// Tim cac diem >= 5, sap xep tang dan, in ra
diem.stream()                          // bat dau day chuyen
    .filter(d -> d >= 5)               // loc: chi lay diem >= 5
    .sorted()                          // sap xep: 5, 6, 7, 8, 9
    .forEach(d -> System.out.print(d + " "));

// Tinh tong diem
int tong = diem.stream()
    .reduce(0, Integer::sum);          // 0 + 3 + 7 + ... = 44

// Lay danh sach ten sinh vien diem cao
List<String> gioi = sinhViens.stream()
    .filter(sv -> sv.diem >= 8.0)      // loc sinh vien gioi
    .map(sv -> sv.ten)                 // lay ten
    .collect(Collectors.toList());     // gom thanh List
```

---

#### Optional

- [ ] **Optional — avoiding NullPointerException / tranh NullPointerException**

> *Optional is like a "gift box" — it might have a gift inside, or it might be empty. You must check before opening.*
>
> *Optional giong nhu "hop qua" — co the co qua ben trong, hoac rong. Ban phai kiem tra truoc khi mo.*

```java
// Thay vi:
String ten = layTen();       // co the tra ve null!
ten.toUpperCase();           // NEU null -> NullPointerException!

// Dung Optional:
Optional<String> ten = Optional.ofNullable(layTen());
String ketQua = ten.orElse("Khong ro");           // neu null thi dung "Khong ro"
ten.ifPresent(t -> System.out.println(t));         // chi in neu co gia tri
String inHoa = ten.map(String::toUpperCase)
                  .orElse("N/A");
```

---

### Basic Multithreading — Da Luong Co Ban

- [ ] **Thread vs Runnable**

> *Multithreading is like a restaurant with many servers working at the same time, instead of just one person.*
>
> *Da luong giong nhu mot quan an co nhieu nhan vien phuc vu cung luc, thay vi chi co 1 nguoi.*

```java
// Cach 1: extends Thread
class NhanVien extends Thread {
    public void run() {
        System.out.println("Nhan vien dang phuc vu...");
    }
}
new NhanVien().start();

// Cach 2: implements Runnable (BETTER — because you can still extend another class)
// Cach 2: implements Runnable (TOT HON — vi con co the extends class khac)
Runnable viecLam = () -> System.out.println("Dang lam viec...");
new Thread(viecLam).start();

// synchronized — ensures only 1 thread can access at a time
// synchronized — dam bao chi 1 luong duoc truy cap tai 1 thoi diem
// Like a bathroom that only allows 1 person in
// Giong nhu phong tam chi co 1 nguoi vao
synchronized void rutTien() {
    soDu -= soTien;
}
```

---

## End of Day 1 Checklist / Checklist Cuoi Ngay 1

- [ ] I can explain the 4 OOP pillars in both English and Vietnamese / Toi co the giai thich 4 tru OOP bang tieng Anh va tieng Viet
- [ ] I understand the difference between abstract class and interface / Toi hieu su khac nhau giua abstract class va interface
- [ ] I know when to use ArrayList, LinkedList, HashMap, HashSet / Toi biet khi nao dung ArrayList, LinkedList, HashMap, HashSet
- [ ] I understand == vs .equals(), String vs StringBuilder / Toi hieu == vs .equals(), String vs StringBuilder
- [ ] I know try-catch-finally and checked vs unchecked exceptions / Toi biet try-catch-finally va checked vs unchecked exception
- [ ] I can write lambdas and use basic Stream API / Toi co the viet lambda va dung Stream API co ban
