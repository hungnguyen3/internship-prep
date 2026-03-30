# Day 3: Live Coding Practice + Mock Interview (5 giờ)

> *Ngày 3: Luyện giải LeetCode Easy bằng Java và mô phỏng phỏng vấn thật. Đây là ngày quan trọng nhất — tập trung vào thực hành!*

---

## Block 1 (3h) — LeetCode Easy Practice / Luyện Giải Bài

---

### Strategy for Live Coding — Chiến Lược Khi Code Trực Tiếp

> *Interviewer không chỉ xem kết quả — họ muốn thấy CÁCH BẠN SUY NGHĨ. Nói ra những gì bạn đang nghĩ!*

**5 bước làm bài live coding:**

```
Bước 1: ĐỌC KỸ đề bài. Hỏi lại nếu chưa hiểu.
        "Just to confirm, the input is ___ and I need to return ___?"

Bước 2: GIẢI THÍCH cách làm TRƯỚC khi code.
        "My approach is to use a HashMap because ___"

Bước 3: VIẾT CODE sạch, đặt tên biến rõ ràng.

Bước 4: TEST bằng ví dụ, xét trường hợp đặc biệt (edge case).
        "Let me trace through the example: ___"

Bước 5: PHÂN TÍCH độ phức tạp (Big O).
        "This solution is O(n) time and O(n) space because ___"
```

**Mẹo:** Nếu bị kẹt, nói ra suy nghĩ của bạn. "I'm thinking about using a brute force approach first, then optimizing" — điều này TỐT HƠN im lặng!

---

### Big O Notation — Cách Đánh Giá Hiệu Suất

> *Big O cho biết "khi dữ liệu tăng, code chạy CHẬM bao nhiêu?"*

**Hình dung như này:** Bạn tìm 1 người trong danh sách:

| Big O | Tên gọi | Giống như... | Ví dụ |
|---|---|---|---|
| O(1) | Hằng số | Mở tủ lạnh lấy đồ — **luôn nhanh** bất kể bao nhiêu đồ | Truy cập array theo index: `arr[5]` |
| O(log n) | Logarithm | Tìm từ trong từ điển — **mở giữa, bỏ nửa** | Binary search |
| O(n) | Tuyến tính | Đọc từng trang sách — **đọc hết 1 lượt** | Duyệt mảng 1 vòng for |
| O(n log n) | | Sắp xếp thông minh | Merge sort, `Arrays.sort()` |
| O(n²) | Bình phương | So sánh **mỗi người với mỗi người** trong lớp | 2 vòng for lồng nhau |

```java
// O(1) — luôn nhanh như nhau
int first = arr[0];

// O(n) — 1 vòng lặp
for (int num : arr) { ... }

// O(n²) — 2 vòng lặp lồng nhau
for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++) { ... }
```

---

### Các Bài Tập

> *Mỗi bài có: đề bài đơn giản, cách nghĩ, lời giải, và giải thích từng dòng.*

---

#### Arrays & Strings — Mảng & Chuỗi

---

##### Two Sum — Tìm 2 số có tổng bằng target

- [ ] **Two Sum** ([LeetCode #1](https://leetcode.com/problems/two-sum/))

**Đề bài:** Cho mảng số nguyên và 1 số `target`. Tìm 2 số trong mảng có tổng bằng `target`. Trả về index của chúng.

```
Input:  nums = [2, 7, 11, 15], target = 9
Output: [0, 1]        (vì nums[0] + nums[1] = 2 + 7 = 9)
```

**Cách nghĩ:**
> Nghĩ như này: Bạn có 100 đồng và cần tìm 2 món hàng cộng lại = 100 đồng.
> Thay vì so TỪNG CẶP (chậm), bạn đi qua từng món và hỏi: "Có món nào = 100 - giá_món_này không?"
> Dùng HashMap để nhớ những món đã thấy.

```java
public int[] twoSum(int[] nums, int target) {
    // HashMap lưu: {giá trị → vị trí}
    // Giống như "sổ tay ghi nhớ" — mỗi số đã gặp, ghi lại vị trí của nó
    Map<Integer, Integer> soTay = new HashMap<>();

    for (int i = 0; i < nums.length; i++) {
        int canTim = target - nums[i];    // Số cần tìm để cộng với nums[i] = target

        if (soTay.containsKey(canTim)) {  // Đã gặp số này trước đó chưa?
            return new int[] { soTay.get(canTim), i };  // Tìm thấy! Trả về 2 vị trí
        }

        soTay.put(nums[i], i);  // Chưa tìm thấy, ghi số này vào sổ tay
    }
    return new int[] {};  // Không tìm thấy
}

// Chạy thử: nums = [2, 7, 11, 15], target = 9
// i=0: canTim = 9-2 = 7, soTay chưa có 7, ghi {2:0}
// i=1: canTim = 9-7 = 2, soTay CÓ 2! → trả về [0, 1] ✓
```

**Độ phức tạp:** O(n) thời gian, O(n) bộ nhớ — duyệt mảng 1 lần, dùng HashMap để tra nhanh.

---

##### Valid Anagram — Kiểm Tra Anagram

- [ ] **Valid Anagram** ([LeetCode #242](https://leetcode.com/problems/valid-anagram/))

**Đề bài:** Cho 2 chuỗi, kiểm tra xem chuỗi này có phải là hoán vị (đổi chỗ chữ cái) của chuỗi kia không.

```
Input:  s = "anagram", t = "nagaram"
Output: true        (cùng các chữ cái, chỉ khác thứ tự)

Input:  s = "rat", t = "car"
Output: false       (khác chữ cái)
```

**Cách nghĩ:**
> Giống như đếm bi màu. Cho 2 túi bi, muốn biết 2 túi có giống nhau không?
> Đếm số lượng từng màu trong túi 1, rồi trừ đi số lượng từng màu trong túi 2.
> Nếu cuối cùng tất cả đều = 0 thì 2 túi giống nhau.

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;  // Khác độ dài thì chắc chắn không

    int[] dem = new int[26];  // 26 ô cho 26 chữ cái a-z

    for (int i = 0; i < s.length(); i++) {
        dem[s.charAt(i) - 'a']++;  // Gặp chữ trong s: CỘNG 1
        dem[t.charAt(i) - 'a']--;  // Gặp chữ trong t: TRỪ 1
    }

    // Nếu mọi ô đều = 0 thì 2 chuỗi có cùng số lượng mỗi chữ cái
    for (int c : dem) {
        if (c != 0) return false;
    }
    return true;
}

// 'a' - 'a' = 0 (ô thứ 0), 'b' - 'a' = 1 (ô thứ 1), ...
// Mẹo: s.charAt(i) - 'a' chuyển chữ cái thành số 0-25
```

**Độ phức tạp:** O(n) thời gian, O(1) bộ nhớ (mảng 26 phần tử là hằng số).

---

##### Reverse String — Đảo Ngược Chuỗi

- [ ] **Reverse String** ([LeetCode #344](https://leetcode.com/problems/reverse-string/))

**Đề bài:** Đảo ngược mảng ký tự tại chỗ (không tạo mảng mới).

```
Input:  ['h','e','l','l','o']
Output: ['o','l','l','e','h']
```

**Cách nghĩ:**
> Giống như xếp hàng người: người đầu đổi chỗ với người cuối, người thứ 2 đổi chỗ với người gần cuối... cho đến khi gặp nhau ở giữa.
> Dùng 2 "con trỏ": 1 ở đầu (left), 1 ở cuối (right), tiến dần vào giữa.

```java
public void reverseString(char[] s) {
    int left = 0;               // Con trỏ đầu
    int right = s.length - 1;   // Con trỏ cuối

    while (left < right) {       // Khi 2 con trỏ chưa gặp nhau
        // Đổi chỗ 2 phần tử
        char tam = s[left];      // Giữ tạm phần tử bên trái
        s[left] = s[right];      // Đặt phần tử bên phải vào bên trái
        s[right] = tam;          // Đặt phần tử tạm vào bên phải

        left++;                  // Tiến con trỏ trái sang phải
        right--;                 // Lùi con trỏ phải sang trái
    }
}

// Chạy thử: ['h','e','l','l','o']
// left=0, right=4: đổi h ↔ o → ['o','e','l','l','h']
// left=1, right=3: đổi e ↔ l → ['o','l','l','e','h']
// left=2, right=2: left == right, DỪNG → ['o','l','l','e','h'] ✓
```

**Độ phức tạp:** O(n) thời gian, O(1) bộ nhớ — chỉ dùng 1 biến tạm.

---

##### Merge Sorted Array — Gộp 2 Mảng Đã Sắp Xếp

- [ ] **Merge Sorted Array** ([LeetCode #88](https://leetcode.com/problems/merge-sorted-array/))

**Đề bài:** Gộp mảng `nums2` vào `nums1` (đã sắp xếp sẵn). `nums1` có đủ chỗ trống ở cuối.

```
Input:  nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
```

**Cách nghĩ:**
> Giống như gộp 2 hàng người ĐÃ xếp theo chiều cao.
> MẸO: Bắt đầu từ CUỐI (người cao nhất) thay vì từ đầu — vì cuối nums1 còn trống!

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1;      // Con trỏ cuối phần có dữ liệu của nums1
    int j = n - 1;      // Con trỏ cuối của nums2
    int k = m + n - 1;  // Con trỏ cuối toàn bộ nums1 (bao gồm chỗ trống)

    // Điền từ cuối lên đầu
    while (j >= 0) {    // Còn phần tử trong nums2 cần gộp
        if (i >= 0 && nums1[i] > nums2[j]) {
            nums1[k] = nums1[i];  // nums1 lớn hơn, đặt vào cuối
            i--;
        } else {
            nums1[k] = nums2[j];  // nums2 lớn hơn (hoặc nums1 hết), đặt vào cuối
            j--;
        }
        k--;
    }
}

// Chạy thử: nums1 = [1,2,3,_,_,_], nums2 = [2,5,6]
// k=5: so sánh 3 vs 6 → 6 lớn hơn → [1,2,3,_,_,6], j=1
// k=4: so sánh 3 vs 5 → 5 lớn hơn → [1,2,3,_,5,6], j=0
// k=3: so sánh 3 vs 2 → 3 lớn hơn → [1,2,_,3,5,6], i=1
// k=2: so sánh 2 vs 2 → bằng nhau → [1,2,2,3,5,6], j=-1 → DỪNG ✓
```

**Độ phức tạp:** O(m+n) thời gian, O(1) bộ nhớ.

---

#### HashMap & HashSet

---

##### Contains Duplicate — Kiểm Tra Trùng Lặp

- [ ] **Contains Duplicate** ([LeetCode #217](https://leetcode.com/problems/contains-duplicate/))

**Đề bài:** Kiểm tra mảng có phần tử nào xuất hiện 2 lần không.

```
Input:  [1, 2, 3, 1]
Output: true         (số 1 xuất hiện 2 lần)
```

**Cách nghĩ:**
> Giống như điểm danh học sinh. Mỗi khi gọi tên, ghi vào sổ. Nếu tên ĐÃ CÓ trong sổ rồi thì → trùng!
> Dùng HashSet như "quyển sổ điểm danh".

```java
public boolean containsDuplicate(int[] nums) {
    Set<Integer> daGap = new HashSet<>();  // "Quyển sổ điểm danh"

    for (int num : nums) {
        if (!daGap.add(num)) {  // add() trả về false nếu ĐÃ TỒN TẠI
            return true;         // Tìm thấy trùng lặp!
        }
    }
    return false;  // Duyệt hết mà không trùng
}

// Chạy thử: [1, 2, 3, 1]
// num=1: daGap = {1}, add thành công
// num=2: daGap = {1,2}, add thành công
// num=3: daGap = {1,2,3}, add thành công
// num=1: 1 ĐÃ CÓ trong set! add() trả về false → return true ✓
```

**Độ phức tạp:** O(n) thời gian, O(n) bộ nhớ.

---

##### Build Array from Permutation — Xây Mảng Từ Hoán Vị

- [ ] **Build Array from Permutation** ([LeetCode #1920](https://leetcode.com/problems/build-array-from-permutation/))

**Đề bài:** Cho mảng `nums` là một hoán vị (permutation) của các số 0 đến n-1. Tạo mảng `ans` sao cho `ans[i] = nums[nums[i]]`.

```
Input:  nums = [0, 2, 1, 5, 3, 4]
Output: [0, 1, 2, 4, 5, 3]

Giải thích:
ans[0] = nums[nums[0]] = nums[0] = 0
ans[1] = nums[nums[1]] = nums[2] = 1
ans[2] = nums[nums[2]] = nums[1] = 2
ans[3] = nums[nums[3]] = nums[5] = 4
ans[4] = nums[nums[4]] = nums[3] = 5
ans[5] = nums[nums[5]] = nums[4] = 3
```

**Cách nghĩ:**
> Giống như trò chơi "theo dấu mũi tên" 2 lần.
> Lần 1: nhìn vào ô hiện tại để biết phải đi đến ô nào.
> Lần 2: nhìn vào ô đó để lấy giá trị.
> `nums[i]` cho bạn "địa chỉ", rồi bạn đến địa chỉ đó lấy "hàng".

```java
public int[] buildArray(int[] nums) {
    int n = nums.length;
    int[] ans = new int[n];  // Tạo mảng kết quả cùng kích thước

    for (int i = 0; i < n; i++) {
        ans[i] = nums[nums[i]];  // Bước 1: nums[i] cho vị trí
                                  // Bước 2: nums[vị_trí] cho giá trị
    }
    return ans;
}

// Chạy thử: nums = [0, 2, 1, 5, 3, 4]
// i=0: nums[0]=0, nums[0]=0  → ans[0] = 0
// i=1: nums[1]=2, nums[2]=1  → ans[1] = 1
// i=2: nums[2]=1, nums[1]=2  → ans[2] = 2
// i=3: nums[3]=5, nums[5]=4  → ans[3] = 4
// i=4: nums[4]=3, nums[3]=5  → ans[4] = 5
// i=5: nums[5]=4, nums[4]=3  → ans[5] = 3
// → [0, 1, 2, 4, 5, 3] ✓
```

**Độ phức tạp:** O(n) thời gian, O(n) bộ nhớ.

**Mẹo phỏng vấn:** Nếu interviewer hỏi "làm được O(1) space không?", bạn có thể dùng trick: encode 2 giá trị vào 1 ô bằng phép chia `nums[i] = nums[i] + (nums[nums[i]] % n) * n`, rồi cuối cùng chia cho n. Nhưng cách trên là đủ tốt cho Easy!

---

##### First Unique Character — Tìm Ký Tự Đầu Tiên Không Trùng

- [ ] **First Unique Character** ([LeetCode #387](https://leetcode.com/problems/first-unique-character-in-a-string/))

**Đề bài:** Tìm ký tự đầu tiên chỉ xuất hiện 1 lần. Trả về index của nó.

```
Input:  "leetcode"
Output: 0           (chữ 'l' chỉ xuất hiện 1 lần, ở vị trí 0)

Input:  "aabb"
Output: -1          (mọi chữ đều trùng)
```

**Cách nghĩ:**
> Lượt 1: đếm số lần xuất hiện của mỗi chữ cái.
> Lượt 2: tìm chữ đầu tiên có số lần = 1.

```java
public int firstUniqChar(String s) {
    int[] dem = new int[26];  // đếm số lần xuất hiện của a-z

    // Lượt 1: đếm
    for (char c : s.toCharArray()) {
        dem[c - 'a']++;
    }

    // Lượt 2: tìm chữ đầu tiên chỉ xuất hiện 1 lần
    for (int i = 0; i < s.length(); i++) {
        if (dem[s.charAt(i) - 'a'] == 1) {
            return i;  // Tìm thấy!
        }
    }
    return -1;  // Không có chữ nào unique
}
```

---

#### Linked List — Danh Sách Liên Kết

> *Linked List giống như đoàn tàu hoả: mỗi toa (node) chứa hàng hoá (data) và móc nối sang toa kế tiếp (next).*

---

##### Reverse Linked List — Đảo Ngược Danh Sách Liên Kết

- [ ] **Reverse Linked List** ([LeetCode #206](https://leetcode.com/problems/reverse-linked-list/))

**Đề bài:** Đảo ngược linked list.

```
Input:  1 → 2 → 3 → 4 → 5
Output: 5 → 4 → 3 → 2 → 1
```

**Cách nghĩ:**
> Giống như đổi hướng mũi tên giữa các toa tàu.
> Đi từ đầu đến cuối, mỗi toa thay vì trỏ sang toa SAU thì đổi lại trỏ sang toa TRƯỚC.

```java
public ListNode reverseList(ListNode head) {
    ListNode truoc = null;     // Toa trước đó (ban đầu chưa có)
    ListNode hienTai = head;   // Toa đang xét

    while (hienTai != null) {
        ListNode tiepTheo = hienTai.next;  // Nhớ toa tiếp theo (kẻo mất)
        hienTai.next = truoc;              // Đổi hướng: trỏ VỀ PHÍA TRƯỚC
        truoc = hienTai;                   // Tiến "trước" lên
        hienTai = tiepTheo;               // Tiến "hiện tại" lên
    }
    return truoc;  // "trước" bây giờ là đầu của list mới
}

// Chạy thử: 1 → 2 → 3 → null
//
// Ban đầu:  trước=null, hiệnTại=1
// Bước 1:   1 → null        trước=1, hiệnTại=2
// Bước 2:   2 → 1 → null   trước=2, hiệnTại=3
// Bước 3:   3 → 2 → 1 → null  trước=3, hiệnTại=null → DỪNG
// Kết quả:  3 → 2 → 1 ✓
```

---

##### Merge Two Sorted Lists — Gộp 2 List Đã Sắp Xếp

- [ ] **Merge Two Sorted Lists** ([LeetCode #21](https://leetcode.com/problems/merge-two-sorted-lists/))

**Đề bài:** Gộp 2 sorted linked list thành 1.

```
Input:  1 → 2 → 4,  1 → 3 → 4
Output: 1 → 1 → 2 → 3 → 4 → 4
```

**Cách nghĩ:**
> Giống như xếp 2 cỗ bài đã sắp xếp thành 1 cỗ: luôn lấy lá bài NHỎ HƠN đặt vào.

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode giaDau = new ListNode(0);  // Node "giả" làm điểm bắt đầu
    ListNode hienTai = giaDau;

    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) {       // l1 nhỏ hơn hoặc bằng
            hienTai.next = l1;         // Lấy từ l1
            l1 = l1.next;
        } else {                       // l2 nhỏ hơn
            hienTai.next = l2;         // Lấy từ l2
            l2 = l2.next;
        }
        hienTai = hienTai.next;
    }

    // Nối phần còn lại (list nào chưa hết)
    hienTai.next = (l1 != null) ? l1 : l2;

    return giaDau.next;  // Bỏ node giả, trả về node thật đầu tiên
}
```

---

#### Stack — Ngăn Xếp

---

##### Valid Parentheses — Kiểm Tra Ngoặc Hợp Lệ

- [ ] **Valid Parentheses** ([LeetCode #20](https://leetcode.com/problems/valid-parentheses/))

**Đề bài:** Kiểm tra chuỗi ngoặc có hợp lệ không.

```
Input:  "()"     Output: true
Input:  "()[]{}" Output: true
Input:  "(]"     Output: false
Input:  "([)]"   Output: false
Input:  "{[]}"   Output: true
```

**Cách nghĩ:**
> Giống như xếp hộp: mỗi khi MỞ ngoặc thì đặt hộp mới lên. Mỗi khi ĐÓNG ngoặc thì lấy hộp trên cùng ra — phải KHỚP với ngoặc mở tương ứng.
> Dùng Stack (xếp chồng) — Last In, First Out (vào sau ra trước).

```java
public boolean isValid(String s) {
    Stack<Character> nganXep = new Stack<>();

    for (char c : s.toCharArray()) {
        // Gặp ngoặc MỞ: đẩy ngoặc ĐÓNG tương ứng vào stack
        if (c == '(') nganXep.push(')');
        else if (c == '{') nganXep.push('}');
        else if (c == '[') nganXep.push(']');

        // Gặp ngoặc ĐÓNG: kiểm tra có khớp với đỉnh stack không
        else if (nganXep.isEmpty() || nganXep.pop() != c) {
            return false;  // Stack rỗng (thừa ngoặc đóng) hoặc không khớp
        }
    }

    return nganXep.isEmpty();  // Phải hết sạch (không thừa ngoặc mở)
}

// Chạy thử: "{[]}"
// '{' → push '}',    stack: [}]
// '[' → push ']',    stack: [}, ]]
// ']' → pop ']' ✓,   stack: [}]
// '}' → pop '}' ✓,   stack: []
// Stack rỗng → true ✓
```

---

#### Tree — Cây Nhị Phân

> *Cây nhị phân giống như cây gia phả: mỗi người (node) có tối đa 2 con (left, right). Người trên cùng là "gốc" (root), người không có con là "lá" (leaf).*

```
        1          ← root (gốc)
       / \
      2   3        ← mỗi node có tối đa 2 con
     / \
    4   5          ← leaf (lá) — không có con
```

```java
// Cấu trúc 1 node trong cây
class TreeNode {
    int val;            // giá trị
    TreeNode left;      // con trái
    TreeNode right;     // con phải
    TreeNode(int val) { this.val = val; }
}
```

---

##### Merge Two Binary Trees — Gộp 2 Cây Nhị Phân

- [ ] **Merge Two Binary Trees** ([LeetCode #617](https://leetcode.com/problems/merge-two-binary-trees/))

**Đề bài:** Cho 2 cây nhị phân, gộp lại thành 1 cây. Nếu 2 node trùng vị trí thì cộng giá trị, nếu chỉ 1 bên có thì giữ nguyên.

```
Cây 1:       Cây 2:       Kết quả:
    1            2             3       (1+2)
   / \          / \           / \
  3   2        1   3         4   5     (3+1, 2+3)
 /              \           / \
5                4         5   4
```

**Cách nghĩ:**
> Giống như trộn 2 bản vẽ bằng cách chồng lên nhau.
> Ở mỗi vị trí: nếu cả 2 bản đều có điểm thì cộng lại, nếu chỉ 1 bên có thì giữ nguyên, nếu cả 2 đều trống thì bỏ qua.
> Dùng **đệ quy** (recursion) — xử lý từng node, rồi gọi lại chính mình cho cây con trái và cây con phải.

```java
public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
    // Trường hợp cơ sở: nếu 1 trong 2 cây rỗng, trả về cây còn lại
    if (root1 == null) return root2;  // Cây 1 rỗng → giữ cây 2
    if (root2 == null) return root1;  // Cây 2 rỗng → giữ cây 1

    // Cả 2 đều có → cộng giá trị
    root1.val += root2.val;

    // Gọi đệ quy cho cây con trái và phải
    root1.left = mergeTrees(root1.left, root2.left);
    root1.right = mergeTrees(root1.right, root2.right);

    return root1;  // Trả về cây đã gộp
}

// Chạy thử với ví dụ trên:
// mergeTrees(1, 2): val = 1+2 = 3
//   left: mergeTrees(3, 1): val = 3+1 = 4
//     left: mergeTrees(5, null): trả về 5
//     right: mergeTrees(null, 4): trả về 4
//   right: mergeTrees(2, 3): val = 2+3 = 5
// Kết quả: 3 → (4→(5,4), 5) ✓
```

**Độ phức tạp:** O(n) thời gian (duyệt mỗi node 1 lần), O(n) bộ nhớ (call stack của đệ quy).

**Mẹo phỏng vấn:** Đây là bài tuyệt vời để cho thấy bạn hiểu **đệ quy** — giải thích rằng mỗi lần gọi hàm xử lý 1 node, rồi "tin tưởng" đệ quy sẽ lo phần còn lại.

---

##### Increasing Order Search Tree — Chuyển BST Thành Danh Sách Tăng Dần

- [ ] **Increasing Order Search Tree** ([LeetCode #897](https://leetcode.com/problems/increasing-order-search-tree/))

**Đề bài:** Cho cây BST (Binary Search Tree — cây tìm kiếm nhị phân, bên trái luôn nhỏ hơn, bên phải luôn lớn hơn). Sắp xếp lại thành cây chỉ có nhánh phải (giống danh sách), theo thứ tự tăng dần.

```
Input:              Output:
      5                1
     / \                \
    3   6                2
   / \   \                \
  2   4   8                3
 /       / \                \
1       7   9                4
                              \
                               5
                                \
                                 6 → 7 → 8 → 9
```

**Cách nghĩ:**
> BST có tính chất đặc biệt: duyệt **in-order** (trái → gốc → phải) sẽ ra thứ tự tăng dần.
> Giống như đọc sách từ trái sang phải — bên trái luôn nhỏ hơn.
> Duyệt in-order, mỗi node gặp được thì nối vào bên phải của node trước đó.

```java
TreeNode hienTai;  // Con trỏ đến node đang xây dựng

public TreeNode increasingBST(TreeNode root) {
    TreeNode giaDau = new TreeNode(0);  // Node giả làm điểm bắt đầu
    hienTai = giaDau;

    duyetInOrder(root);  // Duyệt cây theo thứ tự tăng dần

    return giaDau.right;  // Bỏ node giả, trả về cây thật
}

void duyetInOrder(TreeNode node) {
    if (node == null) return;

    duyetInOrder(node.left);    // 1. Đi sang trái trước (số nhỏ)

    // 2. Xử lý node hiện tại
    node.left = null;           // Xoá nhánh trái (vì cây kết quả chỉ có nhánh phải)
    hienTai.right = node;       // Nối node này vào bên phải
    hienTai = node;             // Tiến con trỏ lên

    duyetInOrder(node.right);   // 3. Đi sang phải (số lớn)
}

// Chạy thử với cây [5,3,6,2,4,null,8,1,null,null,null,7,9]:
// In-order duyệt ra: 1, 2, 3, 4, 5, 6, 7, 8, 9
// Kết quả: 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 (chỉ nhánh phải) ✓
```

**Độ phức tạp:** O(n) thời gian, O(n) bộ nhớ (chiều cao cây trong call stack).

**Kiến thức cần nhớ — 3 cách duyệt cây:**
| Tên | Thứ tự | Giống như... |
|---|---|---|
| **In-order** | Trái → Gốc → Phải | Đọc sách trái sang phải → **ra thứ tự tăng dần** trong BST |
| **Pre-order** | Gốc → Trái → Phải | Khám phá mê cung — đi thẳng trước, rẽ trái, rẽ phải |
| **Post-order** | Trái → Phải → Gốc | Dọn dẹp phòng — dọn con trước, dọn cha sau |

---

##### Second Minimum Node In a Binary Tree — Node Nhỏ Thứ 2

- [ ] **Second Minimum Node In a Binary Tree** ([LeetCode #671](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/))

**Đề bài:** Cho cây nhị phân đặc biệt: mỗi node có 0 hoặc 2 con, và `root.val = min(child1.val, child2.val)`. Tìm giá trị nhỏ thứ 2 trong cây. Trả về -1 nếu không có.

```
Input:       2              Input:    2
            / \                      / \
           2   5                    2   2
          / \
         5   7
Output: 5 (nhỏ thứ 2)      Output: -1 (tất cả giống nhau)
```

**Cách nghĩ:**
> Root luôn là giá trị NHỎ NHẤT (vì mỗi cha = min của 2 con).
> Vậy ta chỉ cần tìm giá trị NHỎ NHẤT mà KHÁC root.
> Duyệt toàn bộ cây, mỗi node mà giá trị > root.val thì so sánh xem có phải nhỏ nhất không.
> Mẹo: nếu gặp node > root.val thì KHÔNG CẦN đi sâu hơn (vì con của nó chắc chắn >= nó).

```java
public int findSecondMinimumValue(TreeNode root) {
    // result lưu giá trị nhỏ thứ 2 tìm được, -1 nếu chưa tìm thấy
    long result = Long.MAX_VALUE;  // dùng long để tránh trùng với Integer.MAX_VALUE
    int nhoNhat = root.val;        // root luôn là giá trị nhỏ nhất

    result = tim(root, nhoNhat, result);

    return result == Long.MAX_VALUE ? -1 : (int) result;
}

long tim(TreeNode node, int nhoNhat, long ketQua) {
    if (node == null) return ketQua;

    // Nếu node > nhỏ nhất → ứng viên cho "nhỏ thứ 2"
    if (node.val > nhoNhat) {
        ketQua = Math.min(ketQua, node.val);  // Cập nhật nếu nhỏ hơn kết quả hiện tại
        return ketQua;  // Không cần đi sâu hơn (con >= cha)
    }

    // node.val == nhoNhat → cần tìm tiếp ở con
    ketQua = tim(node.left, nhoNhat, ketQua);
    ketQua = tim(node.right, nhoNhat, ketQua);

    return ketQua;
}

// Chạy thử: cây [2, 2, 5, 5, 7]
//         2
//        / \
//       2   5      ← 5 > 2, ứng viên! ketQua = 5. Không đi sâu.
//      / \
//     5   7        ← 5 > 2, ketQua = min(5,5) = 5. 7 > 2, ketQua = min(5,7) = 5.
// → Kết quả: 5 ✓
```

**Độ phức tạp:** O(n) thời gian (trường hợp xấu nhất duyệt hết), O(n) bộ nhớ (call stack).

---

#### Math & Other — Toán & Khác

---

##### Palindrome Number — Số Đối Xứng

- [ ] **Palindrome Number** ([LeetCode #9](https://leetcode.com/problems/palindrome-number/))

**Đề bài:** Kiểm tra số nguyên có đọc xuôi và ngược giống nhau không.

```
Input: 121   Output: true   (đọc ngược vẫn là 121)
Input: -121  Output: false  (đọc ngược là 121-)
Input: 10    Output: false  (đọc ngược là 01)
```

**Cách nghĩ:**
> Đảo ngược số, rồi so sánh với số gốc. Giống như viết số ra giấy rồi lật ngược.

```java
public boolean isPalindrome(int x) {
    if (x < 0) return false;  // Số âm không bao giờ đối xứng

    int goc = x;
    int daoNguoc = 0;

    while (x > 0) {
        int chuSoCuoi = x % 10;                   // Lấy chữ số cuối: 121 % 10 = 1
        daoNguoc = daoNguoc * 10 + chuSoCuoi;     // Đắp vào số đảo ngược
        x = x / 10;                                // Bỏ chữ số cuối: 121 / 10 = 12
    }

    return goc == daoNguoc;
}

// Chạy thử: x = 121
// Bước 1: cuối=1, đảoNgược=1,   x=12
// Bước 2: cuối=2, đảoNgược=12,  x=1
// Bước 3: cuối=1, đảoNgược=121, x=0
// 121 == 121 → true ✓
```

---

##### FizzBuzz

- [ ] **FizzBuzz** ([LeetCode #412](https://leetcode.com/problems/fizz-buzz/))

**Đề bài:** In số từ 1 đến n: chia hết cho 3 in "Fizz", chia hết cho 5 in "Buzz", chia hết cho cả 2 in "FizzBuzz".

```
Input:  n = 15
Output: ["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]
```

**Cách nghĩ:**
> Kiểm tra từ điều kiện CHẶT NHẤT trước (chia hết cho 15) đến LỎNG HƠN (chia hết cho 3, chia hết cho 5).

```java
public List<String> fizzBuzz(int n) {
    List<String> ketQua = new ArrayList<>();

    for (int i = 1; i <= n; i++) {
        if (i % 15 == 0) {       // Chia hết cho CẢ 3 VÀ 5 → kiểm tra TRƯỚC
            ketQua.add("FizzBuzz");
        } else if (i % 3 == 0) { // Chỉ chia hết cho 3
            ketQua.add("Fizz");
        } else if (i % 5 == 0) { // Chỉ chia hết cho 5
            ketQua.add("Buzz");
        } else {                  // Không chia hết cho gì
            ketQua.add(String.valueOf(i));
        }
    }
    return ketQua;
}
```

---

#### Bonus Problems — Bài Thêm (Nếu Còn Thời Gian)

---

##### Best Time to Buy and Sell Stock — Mua Bán Cổ Phiếu

- [ ] **Best Time to Buy and Sell Stock** ([LeetCode #121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/))

**Đề bài:** Cho mảng giá cổ phiếu theo ngày, tìm lợi nhuận lớn nhất khi mua 1 ngày và bán 1 ngày SAU ĐÓ.

```
Input:  [7, 1, 5, 3, 6, 4]
Output: 5              (Mua ngày 2 giá 1, bán ngày 5 giá 6 → lời 5)
```

**Cách nghĩ:**
> Đi qua từng ngày: nhớ GIÁ THẤP NHẤT đã thấy, tính lợi nhuận nếu bán HÔM NAY, cập nhật lợi nhuận lớn nhất.

```java
public int maxProfit(int[] prices) {
    int giaThapNhat = Integer.MAX_VALUE;  // Giá thấp nhất đã thấy
    int loiNhuanMax = 0;                  // Lợi nhuận lớn nhất

    for (int gia : prices) {
        giaThapNhat = Math.min(giaThapNhat, gia);                // Cập nhật giá thấp nhất
        loiNhuanMax = Math.max(loiNhuanMax, gia - giaThapNhat);  // Lợi nhuận nếu bán hôm nay
    }
    return loiNhuanMax;
}

// Chạy thử: [7, 1, 5, 3, 6, 4]
// giá=7: thấp=7, lời=0
// giá=1: thấp=1, lời=0    (1-1=0)
// giá=5: thấp=1, lời=4    (5-1=4)
// giá=3: thấp=1, lời=4    (3-1=2, giữ 4)
// giá=6: thấp=1, lời=5    (6-1=5) ← MAX
// giá=4: thấp=1, lời=5    (4-1=3, giữ 5)
// → 5 ✓
```

---

##### Maximum Subarray — Mảng Con Có Tổng Lớn Nhất

- [ ] **Maximum Subarray** ([LeetCode #53](https://leetcode.com/problems/maximum-subarray/))

**Đề bài:** Tìm mảng con liên tiếp có tổng lớn nhất.

```
Input:  [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6              (mảng con [4, -1, 2, 1] có tổng = 6)
```

**Cách nghĩ (Thuật toán Kadane):**
> Tại mỗi bước, hỏi: "Nên TIẾP TỤC cộng dồn từ trước, hay BẮT ĐẦU MỚI từ đây?"
> Nếu tổng hiện tại + phần tử mới < chỉ phần tử mới thì bắt đầu mới.

```java
public int maxSubArray(int[] nums) {
    int tongHienTai = nums[0];  // Tổng của mảng con đang xét
    int tongMax = nums[0];      // Tổng lớn nhất đã tìm thấy

    for (int i = 1; i < nums.length; i++) {
        // Tiếp tục cộng dồn, hoặc bắt đầu mới?
        tongHienTai = Math.max(nums[i], tongHienTai + nums[i]);
        tongMax = Math.max(tongMax, tongHienTai);
    }
    return tongMax;
}
```

---

##### Climbing Stairs — Leo Cầu Thang

- [ ] **Climbing Stairs** ([LeetCode #70](https://leetcode.com/problems/climbing-stairs/))

**Đề bài:** Leo n bậc thang, mỗi bước leo 1 hoặc 2 bậc. Có bao nhiêu cách?

```
Input: n=3  Output: 3  (3 cách: 1+1+1, 1+2, 2+1)
```

**Cách nghĩ:**
> Để đến bậc n, bạn có thể từ bậc n-1 (bước 1 bậc) hoặc từ bậc n-2 (bước 2 bậc).
> Vậy: số_cách(n) = số_cách(n-1) + số_cách(n-2) — giống dãy Fibonacci!

```java
public int climbStairs(int n) {
    if (n <= 2) return n;

    int haiBuocTruoc = 1;  // số_cách(1) = 1
    int motBuocTruoc = 2;  // số_cách(2) = 2

    for (int i = 3; i <= n; i++) {
        int hienTai = motBuocTruoc + haiBuocTruoc;  // Fibonacci
        haiBuocTruoc = motBuocTruoc;
        motBuocTruoc = hienTai;
    }
    return motBuocTruoc;
}
```

---

## Block 2 (2h) — Mock Interview / Phỏng Vấn Thử

---

### Vòng 1: Mô Phỏng Đầy Đủ (30 phút)

- [ ] **Bật đồng hồ 30 phút và làm như phỏng vấn thật:**
  - [ ] 5 phút: Tự giới thiệu bằng tiếng Anh
  - [ ] 10 phút: Tự hỏi và trả lời các câu hỏi kỹ thuật (xen kẽ Anh/Việt):
    - "What is OOP?"
    - "Explain the difference between ArrayList and LinkedList"
    - "What is REST API?"
    - "Tell me about your project"
  - [ ] 15 phút: Giải 1 bài LeetCode Easy (chọn bất kỳ ở trên)
  - [ ] Review: Phần nào tốt? Phần nào cần cải thiện?

---

### Vòng 2: Tập Trung Vào Điểm Yếu (30 phút)

- [ ] Học lại khái niệm nào còn lủng
- [ ] Luyện giải thích code bằng lời — tưởng tượng đang nói với interviewer
- [ ] Giải thêm 1 bài LeetCode với đồng hồ

---

### Vòng 3: Speed Run (30 phút)

- [ ] Giải Two Sum trong 5 phút
- [ ] Giải Valid Parentheses trong 5 phút
- [ ] Giải thích OOP trong 2 phút (thành tiếng, bằng tiếng Anh)
- [ ] Giải thích project trong 2 phút (thành tiếng)

---

### Ôn Lại Lần Cuối (30 phút)

- [ ] Đọc lại tất cả khái niệm Day 1 một lượt
- [ ] Đọc lại các câu trả lời Day 2 một lượt
- [ ] Chắc chắn mình có thể giải thích TỰ NHIÊN (không đọc)

---

## Nhắc Nhở Ngày Phỏng Vấn

- [ ] Ngủ sớm đêm trước
- [ ] Kiểm tra camera, micro, internet
- [ ] Có nước uống và giấy bút bên cạnh
- [ ] Mở sẵn IDE/editor và LeetCode trước khi phỏng vấn
- [ ] **NÓI RA SUY NGHĨ** khi làm code — họ muốn nghe cách bạn tư duy
- [ ] Không biết thì nói "I'm not sure, but I think..." — trung thực tốt hơn im lặng
- [ ] Nói thật về project — họ sẽ hỏi sâu, đừng phịnh
- [ ] Thuật ngữ kỹ thuật dùng tiếng Anh OK, giải thích ý tưởng bằng ngôn ngữ nào thoải mái hơn

---

> **Chúc bạn phỏng vấn thành công! Bạn đã chuẩn bị 15 tiếng — hãy tự tin vào bản thân!**
