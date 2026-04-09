# Day 3: Live Coding Practice + Mock Interview (5 Hours)

# Day 3: Live Coding Practice + Mock Interview (5 giờ)

> *Day 3: Practice solving LeetCode Easy problems in Java and simulate a real interview. This is the most important day — focus on hands-on practice!*
>
> *Ngày 3: Luyện giải LeetCode Easy bằng Java và mô phỏng phỏng vấn thật. Đây là ngày quan trọng nhất — tập trung vào thực hành!*

---

## Block 1 (3h) — LeetCode Easy Practice / Luyện Giải Bài

---

### Strategy for Live Coding — Chiến Lược Khi Code Trực Tiếp

> *The interviewer doesn't just look at the result — they want to see HOW YOU THINK. Say out loud what you're thinking!*
>
> *Interviewer không chỉ xem kết quả — họ muốn thấy CÁCH BẠN SUY NGHĨ. Nói ra những gì bạn đang nghĩ!*

**5 steps for live coding / 5 bước làm bài live coding:**

```
Step 1 / Bước 1: READ the problem carefully. Ask again if unclear.
                 ĐỌC KỸ đề bài. Hỏi lại nếu chưa hiểu.
                 "Just to confirm, the input is ___ and I need to return ___?"

Step 2 / Bước 2: EXPLAIN your approach BEFORE coding.
                 GIẢI THÍCH cách làm TRƯỚC khi code.
                 "My approach is to use a HashMap because ___"

Step 3 / Bước 3: WRITE clean code with clear variable names.
                 VIẾT CODE sạch, đặt tên biến rõ ràng.

Step 4 / Bước 4: TEST with examples, consider edge cases.
                 TEST bằng ví dụ, xét trường hợp đặc biệt (edge case).
                 "Let me trace through the example: ___"

Step 5 / Bước 5: ANALYZE time/space complexity (Big O).
                 PHÂN TÍCH độ phức tạp (Big O).
                 "This solution is O(n) time and O(n) space because ___"
```

**Tip:** If you're stuck, say your thoughts out loud. "I'm thinking about using a brute force approach first, then optimizing" — this is BETTER than silence!

**Mẹo:** Nếu bị kẹt, nói ra suy nghĩ của bạn. "I'm thinking about using a brute force approach first, then optimizing" — điều này TỐT HƠN im lặng!

---

### Big O Notation — Cách Đánh Giá Hiệu Suất

> *Big O tells you "as data grows, how much SLOWER does the code run?"*
>
> *Big O cho biết "khi dữ liệu tăng, code chạy CHẬM bao nhiêu?"*

**Imagine this:** You're looking for a person in a list:

**Hình dung như này:** Bạn tìm 1 người trong danh sách:

| Big O | Name / Tên gọi | Like... / Giống như... | Example / Ví dụ |
|---|---|---|---|
| O(1) | Constant / Hằng số | Open fridge to grab something — **always fast** regardless of how much is inside / Mở tủ lạnh lấy đồ — **luôn nhanh** bất kể bao nhiêu đồ | Access array by index: `arr[5]` |
| O(log n) | Logarithm | Find word in dictionary — **open middle, discard half** / Tìm từ trong từ điển — **mở giữa, bỏ nửa** | Binary search |
| O(n) | Linear / Tuyến tính | Read every page of a book — **read through once** / Đọc từng trang sách — **đọc hết 1 lượt** | One for-loop through array |
| O(n log n) | | Smart sorting / Sắp xếp thông minh | Merge sort, `Arrays.sort()` |
| O(n²) | Quadratic / Bình phương | Compare **every person with every other person** in class / So sánh **mỗi người với mỗi người** trong lớp | 2 nested for-loops |

```java
// O(1) — always equally fast / luôn nhanh như nhau
int first = arr[0];

// O(n) — 1 loop / 1 vòng lặp
for (int num : arr) { ... }

// O(n²) — 2 nested loops / 2 vòng lặp lồng nhau
for (int i = 0; i < n; i++)
    for (int j = 0; j < n; j++) { ... }
```

---

### Problems / Các Bài Tập

> *Each problem has: simple problem statement, how to think, solution, and line-by-line explanation.*
>
> *Mỗi bài có: đề bài đơn giản, cách nghĩ, lời giải, và giải thích từng dòng.*

---

#### Arrays & Strings — Mảng & Chuỗi

---

##### Two Sum — Tìm 2 số có tổng bằng target

- [ ] **Two Sum** ([LeetCode #1](https://leetcode.com/problems/two-sum/))

**Problem:** Given an integer array and a number `target`. Find 2 numbers in the array that sum to `target`. Return their indices.

**Đề bài:** Cho mảng số nguyên và 1 số `target`. Tìm 2 số trong mảng có tổng bằng `target`. Trả về index của chúng.

```
Input:  nums = [2, 7, 11, 15], target = 9
Output: [0, 1]        (because nums[0] + nums[1] = 2 + 7 = 9)
                      (vì nums[0] + nums[1] = 2 + 7 = 9)
```

**How to think:** You have 100 dollars and need to find 2 items that add up to 100. Instead of comparing EVERY PAIR (slow), you go through each item and ask: "Is there an item = 100 - this_item's_price?" Use a HashMap to remember items you've already seen.

**Cách nghĩ:** Bạn có 100 đồng và cần tìm 2 món hàng cộng lại = 100 đồng. Thay vì so TỪNG CẶP (chậm), bạn đi qua từng món và hỏi: "Có món nào = 100 - giá_món_này không?" Dùng HashMap để nhớ những món đã thấy.

```java
public int[] twoSum(int[] nums, int target) {
    // HashMap stores: {value → index}
    // Like a "notebook" — for each number seen, record its position
    // HashMap lưu: {giá trị → vị trí}
    // Giống như "sổ tay ghi nhớ" — mỗi số đã gặp, ghi lại vị trí của nó
    Map<Integer, Integer> notebook = new HashMap<>();

    for (int i = 0; i < nums.length; i++) {
        int need = target - nums[i];    // Number needed to sum to target
                                         // Số cần tìm để cộng với nums[i] = target

        if (notebook.containsKey(need)) {  // Have we seen this number before?
                                            // Đã gặp số này trước đó chưa?
            return new int[] { notebook.get(need), i };  // Found! Return 2 positions
                                                          // Tìm thấy! Trả về 2 vị trí
        }

        notebook.put(nums[i], i);  // Not found yet, record this number
                                    // Chưa tìm thấy, ghi số này vào sổ tay
    }
    return new int[] {};  // Not found / Không tìm thấy
}

// Trace / Chạy thử: nums = [2, 7, 11, 15], target = 9
// i=0: need = 9-2 = 7, notebook doesn't have 7, record {2:0}
// i=1: need = 9-7 = 2, notebook HAS 2! → return [0, 1] ✓
```

**Complexity / Độ phức tạp:** O(n) time, O(n) space — traverse array once, use HashMap for fast lookup. / O(n) thời gian, O(n) bộ nhớ — duyệt mảng 1 lần, dùng HashMap để tra nhanh.

---

##### Valid Anagram — Kiểm Tra Anagram

- [ ] **Valid Anagram** ([LeetCode #242](https://leetcode.com/problems/valid-anagram/))

**Problem:** Given 2 strings, check if one is an anagram (rearranged letters) of the other.

**Đề bài:** Cho 2 chuỗi, kiểm tra xem chuỗi này có phải là hoán vị (đổi chỗ chữ cái) của chuỗi kia không.

```
Input:  s = "anagram", t = "nagaram"
Output: true        (same letters, different order / cùng các chữ cái, chỉ khác thứ tự)

Input:  s = "rat", t = "car"
Output: false       (different letters / khác chữ cái)
```

**How to think:** Like counting colored marbles. Given 2 bags, want to know if they're identical? Count each color in bag 1, subtract each color in bag 2. If all counts are 0 at the end, they're the same.

**Cách nghĩ:** Giống như đếm bi màu. Cho 2 túi bi, muốn biết 2 túi có giống nhau không? Đếm số lượng từng màu trong túi 1, rồi trừ đi số lượng từng màu trong túi 2. Nếu cuối cùng tất cả đều = 0 thì 2 túi giống nhau.

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;  // Different length = definitely not
                                                  // Khác độ dài thì chắc chắn không

    int[] count = new int[26];  // 26 slots for 26 letters a-z
                                 // 26 ô cho 26 chữ cái a-z

    for (int i = 0; i < s.length(); i++) {
        count[s.charAt(i) - 'a']++;  // Letter from s: ADD 1 / Gặp chữ trong s: CỘNG 1
        count[t.charAt(i) - 'a']--;  // Letter from t: SUBTRACT 1 / Gặp chữ trong t: TRỪ 1
    }

    // If every slot is 0, both strings have the same letter counts
    // Nếu mọi ô đều = 0 thì 2 chuỗi có cùng số lượng mỗi chữ cái
    for (int c : count) {
        if (c != 0) return false;
    }
    return true;
}
```

**Complexity / Độ phức tạp:** O(n) time, O(1) space (26-element array is constant). / O(n) thời gian, O(1) bộ nhớ (mảng 26 phần tử là hằng số).

---

##### Reverse String — Đảo Ngược Chuỗi

- [ ] **Reverse String** ([LeetCode #344](https://leetcode.com/problems/reverse-string/))

**Problem:** Reverse a character array in-place (don't create a new array).

**Đề bài:** Đảo ngược mảng ký tự tại chỗ (không tạo mảng mới).

```
Input:  ['h','e','l','l','o']
Output: ['o','l','l','e','h']
```

**How to think:** Like lining people up: the first person swaps with the last, the second swaps with the second-to-last... until they meet in the middle. Use 2 "pointers": one at the start (left), one at the end (right), moving toward the center.

**Cách nghĩ:** Giống như xếp hàng người: người đầu đổi chỗ với người cuối, người thứ 2 đổi chỗ với người gần cuối... cho đến khi gặp nhau ở giữa. Dùng 2 "con trỏ": 1 ở đầu (left), 1 ở cuối (right), tiến dần vào giữa.

```java
public void reverseString(char[] s) {
    int left = 0;               // Left pointer / Con trỏ đầu
    int right = s.length - 1;   // Right pointer / Con trỏ cuối

    while (left < right) {       // While pointers haven't met / Khi 2 con trỏ chưa gặp nhau
        // Swap the two elements / Đổi chỗ 2 phần tử
        char temp = s[left];
        s[left] = s[right];
        s[right] = temp;

        left++;                  // Move left pointer right / Tiến con trỏ trái sang phải
        right--;                 // Move right pointer left / Lùi con trỏ phải sang trái
    }
}

// Trace / Chạy thử: ['h','e','l','l','o']
// left=0, right=4: swap h ↔ o → ['o','e','l','l','h']
// left=1, right=3: swap e ↔ l → ['o','l','l','e','h']
// left=2, right=2: left == right, STOP → ['o','l','l','e','h'] ✓
```

**Complexity / Độ phức tạp:** O(n) time, O(1) space — only 1 temp variable. / O(n) thời gian, O(1) bộ nhớ — chỉ dùng 1 biến tạm.

---

##### Merge Sorted Array — Gộp 2 Mảng Đã Sắp Xếp

- [ ] **Merge Sorted Array** ([LeetCode #88](https://leetcode.com/problems/merge-sorted-array/))

**Problem:** Merge `nums2` into `nums1` (both already sorted). `nums1` has extra space at the end.

**Đề bài:** Gộp mảng `nums2` vào `nums1` (đã sắp xếp sẵn). `nums1` có đủ chỗ trống ở cuối.

```
Input:  nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
```

**How to think:** Like merging 2 lines of people already sorted by height. TRICK: Start from the END (tallest person) instead of the start — because the end of nums1 is empty!

**Cách nghĩ:** Giống như gộp 2 hàng người ĐÃ xếp theo chiều cao. MẸO: Bắt đầu từ CUỐI (người cao nhất) thay vì từ đầu — vì cuối nums1 còn trống!

```java
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1;      // Pointer at end of nums1's data / Con trỏ cuối phần có dữ liệu của nums1
    int j = n - 1;      // Pointer at end of nums2 / Con trỏ cuối của nums2
    int k = m + n - 1;  // Pointer at end of entire nums1 / Con trỏ cuối toàn bộ nums1

    // Fill from end to start / Điền từ cuối lên đầu
    while (j >= 0) {
        if (i >= 0 && nums1[i] > nums2[j]) {
            nums1[k] = nums1[i];  // nums1 is larger, place at end
            i--;
        } else {
            nums1[k] = nums2[j];  // nums2 is larger (or nums1 exhausted), place at end
            j--;
        }
        k--;
    }
}

// Trace / Chạy thử: nums1 = [1,2,3,_,_,_], nums2 = [2,5,6]
// k=5: compare 3 vs 6 → 6 larger → [1,2,3,_,_,6], j=1
// k=4: compare 3 vs 5 → 5 larger → [1,2,3,_,5,6], j=0
// k=3: compare 3 vs 2 → 3 larger → [1,2,_,3,5,6], i=1
// k=2: compare 2 vs 2 → equal   → [1,2,2,3,5,6], j=-1 → STOP ✓
```

**Complexity / Độ phức tạp:** O(m+n) time, O(1) space.

---

#### HashMap & HashSet

---

##### Contains Duplicate — Kiểm Tra Trùng Lặp

- [ ] **Contains Duplicate** ([LeetCode #217](https://leetcode.com/problems/contains-duplicate/))

**Problem:** Check if any element appears more than once in the array.

**Đề bài:** Kiểm tra mảng có phần tử nào xuất hiện 2 lần không.

```
Input:  [1, 2, 3, 1]
Output: true         (number 1 appears twice / số 1 xuất hiện 2 lần)
```

**How to think:** Like taking attendance. Each time you call a name, write it down. If the name is ALREADY in the list → duplicate! Use a HashSet as an "attendance book".

**Cách nghĩ:** Giống như điểm danh học sinh. Mỗi khi gọi tên, ghi vào sổ. Nếu tên ĐÃ CÓ trong sổ rồi thì → trùng! Dùng HashSet như "quyển sổ điểm danh".

```java
public boolean containsDuplicate(int[] nums) {
    Set<Integer> seen = new HashSet<>();  // "Attendance book" / "Quyển sổ điểm danh"

    for (int num : nums) {
        if (!seen.add(num)) {  // add() returns false if ALREADY EXISTS
                                // add() trả về false nếu ĐÃ TỒN TẠI
            return true;        // Found duplicate! / Tìm thấy trùng lặp!
        }
    }
    return false;  // No duplicates found / Duyệt hết mà không trùng
}

// Trace / Chạy thử: [1, 2, 3, 1]
// num=1: seen = {1}, add OK
// num=2: seen = {1,2}, add OK
// num=3: seen = {1,2,3}, add OK
// num=1: 1 ALREADY in set! add() returns false → return true ✓
```

**Complexity / Độ phức tạp:** O(n) time, O(n) space.

---

##### Build Array from Permutation — Xây Mảng Từ Hoán Vị

- [ ] **Build Array from Permutation** ([LeetCode #1920](https://leetcode.com/problems/build-array-from-permutation/))

**Problem:** Given array `nums` which is a permutation of numbers 0 to n-1. Build array `ans` where `ans[i] = nums[nums[i]]`.

**Đề bài:** Cho mảng `nums` là một hoán vị (permutation) của các số 0 đến n-1. Tạo mảng `ans` sao cho `ans[i] = nums[nums[i]]`.

```
Input:  nums = [0, 2, 1, 5, 3, 4]
Output: [0, 1, 2, 4, 5, 3]

Explanation / Giải thích:
ans[0] = nums[nums[0]] = nums[0] = 0
ans[1] = nums[nums[1]] = nums[2] = 1
ans[2] = nums[nums[2]] = nums[1] = 2
ans[3] = nums[nums[3]] = nums[5] = 4
ans[4] = nums[nums[4]] = nums[3] = 5
ans[5] = nums[nums[5]] = nums[4] = 3
```

**How to think:** Like a game of "follow the arrows" twice. Step 1: look at the current cell to find which cell to go to. Step 2: look at THAT cell to get the value. `nums[i]` gives you the "address", then you go to that address to pick up the "goods".

**Cách nghĩ:** Giống như trò chơi "theo dấu mũi tên" 2 lần. Lần 1: nhìn vào ô hiện tại để biết phải đi đến ô nào. Lần 2: nhìn vào ô đó để lấy giá trị. `nums[i]` cho bạn "địa chỉ", rồi bạn đến địa chỉ đó lấy "hàng".

```java
public int[] buildArray(int[] nums) {
    int n = nums.length;
    int[] ans = new int[n];  // Create result array of same size
                              // Tạo mảng kết quả cùng kích thước

    for (int i = 0; i < n; i++) {
        ans[i] = nums[nums[i]];  // Step 1: nums[i] gives position
                                  // Step 2: nums[position] gives value
                                  // Bước 1: nums[i] cho vị trí
                                  // Bước 2: nums[vị_trí] cho giá trị
    }
    return ans;
}

// Trace / Chạy thử: nums = [0, 2, 1, 5, 3, 4]
// i=0: nums[0]=0, nums[0]=0  → ans[0] = 0
// i=1: nums[1]=2, nums[2]=1  → ans[1] = 1
// i=2: nums[2]=1, nums[1]=2  → ans[2] = 2
// i=3: nums[3]=5, nums[5]=4  → ans[3] = 4
// i=4: nums[4]=3, nums[3]=5  → ans[4] = 5
// i=5: nums[5]=4, nums[4]=3  → ans[5] = 3
// → [0, 1, 2, 4, 5, 3] ✓
```

**Complexity / Độ phức tạp:** O(n) time, O(n) space.

**Interview tip:** If interviewer asks "can you do O(1) space?", you can use a trick: encode 2 values in 1 cell using `nums[i] = nums[i] + (nums[nums[i]] % n) * n`, then divide by n at the end. But the above approach is good enough for Easy!

**Mẹo phỏng vấn:** Nếu interviewer hỏi "làm được O(1) space không?", bạn có thể dùng trick: encode 2 giá trị vào 1 ô bằng phép chia `nums[i] = nums[i] + (nums[nums[i]] % n) * n`, rồi cuối cùng chia cho n. Nhưng cách trên là đủ tốt cho Easy!

---

##### First Unique Character — Tìm Ký Tự Đầu Tiên Không Trùng

- [ ] **First Unique Character** ([LeetCode #387](https://leetcode.com/problems/first-unique-character-in-a-string/))

**Problem:** Find the first character that appears only once. Return its index.

**Đề bài:** Tìm ký tự đầu tiên chỉ xuất hiện 1 lần. Trả về index của nó.

```
Input:  "leetcode"
Output: 0           (letter 'l' appears only once, at position 0)
                    (chữ 'l' chỉ xuất hiện 1 lần, ở vị trí 0)

Input:  "aabb"
Output: -1          (every letter is repeated / mọi chữ đều trùng)
```

**How to think:** Pass 1: count how many times each letter appears. Pass 2: find the first letter with count = 1.

**Cách nghĩ:** Lượt 1: đếm số lần xuất hiện của mỗi chữ cái. Lượt 2: tìm chữ đầu tiên có số lần = 1.

```java
public int firstUniqChar(String s) {
    int[] count = new int[26];  // count occurrences of a-z / đếm số lần xuất hiện của a-z

    // Pass 1: count / Lượt 1: đếm
    for (char c : s.toCharArray()) {
        count[c - 'a']++;
    }

    // Pass 2: find first letter appearing only once
    // Lượt 2: tìm chữ đầu tiên chỉ xuất hiện 1 lần
    for (int i = 0; i < s.length(); i++) {
        if (count[s.charAt(i) - 'a'] == 1) {
            return i;  // Found! / Tìm thấy!
        }
    }
    return -1;  // No unique letter / Không có chữ nào unique
}
```

---

#### Linked List — Danh Sách Liên Kết

> *A Linked List is like a train: each car (node) holds cargo (data) and is linked to the next car (next).*
>
> *Linked List giống như đoàn tàu hoả: mỗi toa (node) chứa hàng hoá (data) và móc nối sang toa kế tiếp (next).*

---

##### Reverse Linked List — Đảo Ngược Danh Sách Liên Kết

- [ ] **Reverse Linked List** ([LeetCode #206](https://leetcode.com/problems/reverse-linked-list/))

**Problem:** Reverse a linked list.

**Đề bài:** Đảo ngược linked list.

```
Input:  1 → 2 → 3 → 4 → 5
Output: 5 → 4 → 3 → 2 → 1
```

**How to think:** Like reversing the direction of arrows between train cars. Go from start to end, and for each car, instead of pointing to the NEXT car, reverse it to point to the PREVIOUS one.

**Cách nghĩ:** Giống như đổi hướng mũi tên giữa các toa tàu. Đi từ đầu đến cuối, mỗi toa thay vì trỏ sang toa SAU thì đổi lại trỏ sang toa TRƯỚC.

```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null;      // Previous car (none at start) / Toa trước đó (ban đầu chưa có)
    ListNode curr = head;      // Current car / Toa đang xét

    while (curr != null) {
        ListNode next = curr.next;  // Remember next car (don't lose it!) / Nhớ toa tiếp theo (kẻo mất)
        curr.next = prev;           // Reverse: point BACKWARD / Đổi hướng: trỏ VỀ PHÍA TRƯỚC
        prev = curr;                // Move "prev" forward / Tiến "trước" lên
        curr = next;                // Move "curr" forward / Tiến "hiện tại" lên
    }
    return prev;  // "prev" is now the head of the new list
                   // "prev" bây giờ là đầu của list mới
}

// Trace / Chạy thử: 1 → 2 → 3 → null
//
// Start:    prev=null, curr=1
// Step 1:   1 → null        prev=1, curr=2
// Step 2:   2 → 1 → null   prev=2, curr=3
// Step 3:   3 → 2 → 1 → null  prev=3, curr=null → STOP
// Result:   3 → 2 → 1 ✓
```

---

##### Merge Two Sorted Lists — Gộp 2 List Đã Sắp Xếp

- [ ] **Merge Two Sorted Lists** ([LeetCode #21](https://leetcode.com/problems/merge-two-sorted-lists/))

**Problem:** Merge 2 sorted linked lists into 1.

**Đề bài:** Gộp 2 sorted linked list thành 1.

```
Input:  1 → 2 → 4,  1 → 3 → 4
Output: 1 → 1 → 2 → 3 → 4 → 4
```

**How to think:** Like merging 2 sorted decks of cards into one: always take the SMALLER card and place it in.

**Cách nghĩ:** Giống như xếp 2 cỗ bài đã sắp xếp thành 1 cỗ: luôn lấy lá bài NHỎ HƠN đặt vào.

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    ListNode dummy = new ListNode(0);  // Fake node as starting point / Node "giả" làm điểm bắt đầu
    ListNode curr = dummy;

    while (l1 != null && l2 != null) {
        if (l1.val <= l2.val) {
            curr.next = l1;     // Take from l1 / Lấy từ l1
            l1 = l1.next;
        } else {
            curr.next = l2;     // Take from l2 / Lấy từ l2
            l2 = l2.next;
        }
        curr = curr.next;
    }

    // Attach remaining nodes / Nối phần còn lại (list nào chưa hết)
    curr.next = (l1 != null) ? l1 : l2;

    return dummy.next;  // Skip fake node, return real first node
                         // Bỏ node giả, trả về node thật đầu tiên
}
```

---

#### Stack — Ngăn Xếp

---

##### Valid Parentheses — Kiểm Tra Ngoặc Hợp Lệ

- [ ] **Valid Parentheses** ([LeetCode #20](https://leetcode.com/problems/valid-parentheses/))

**Problem:** Check if a string of brackets is valid.

**Đề bài:** Kiểm tra chuỗi ngoặc có hợp lệ không.

```
Input:  "()"     Output: true
Input:  "()[]{}" Output: true
Input:  "(]"     Output: false
Input:  "([)]"   Output: false
Input:  "{[]}"   Output: true
```

**How to think:** Like stacking boxes: each time you OPEN a bracket, place a new box on top. Each time you CLOSE a bracket, take the top box off — it must MATCH the corresponding opening bracket. Use a Stack — Last In, First Out.

**Cách nghĩ:** Giống như xếp hộp: mỗi khi MỞ ngoặc thì đặt hộp mới lên. Mỗi khi ĐÓNG ngoặc thì lấy hộp trên cùng ra — phải KHỚP với ngoặc mở tương ứng. Dùng Stack (xếp chồng) — Last In, First Out (vào sau ra trước).

```java
public boolean isValid(String s) {
    Stack<Character> stack = new Stack<>();

    for (char c : s.toCharArray()) {
        // Opening bracket: push the matching CLOSING bracket onto stack
        // Gặp ngoặc MỞ: đẩy ngoặc ĐÓNG tương ứng vào stack
        if (c == '(') stack.push(')');
        else if (c == '{') stack.push('}');
        else if (c == '[') stack.push(']');

        // Closing bracket: check if it matches the top of stack
        // Gặp ngoặc ĐÓNG: kiểm tra có khớp với đỉnh stack không
        else if (stack.isEmpty() || stack.pop() != c) {
            return false;  // Stack empty (extra closing) or mismatch
        }
    }

    return stack.isEmpty();  // Must be empty (no leftover opening brackets)
                              // Phải hết sạch (không thừa ngoặc mở)
}

// Trace / Chạy thử: "{[]}"
// '{' → push '}',    stack: [}]
// '[' → push ']',    stack: [}, ]]
// ']' → pop ']' ✓,   stack: [}]
// '}' → pop '}' ✓,   stack: []
// Stack empty → true ✓
```

---

#### Tree — Cây Nhị Phân

> *A binary tree is like a family tree: each person (node) has at most 2 children (left, right). The person at the top is the "root", people with no children are "leaves".*
>
> *Cây nhị phân giống như cây gia phả: mỗi người (node) có tối đa 2 con (left, right). Người trên cùng là "gốc" (root), người không có con là "lá" (leaf).*

```
        1          ← root (gốc)
       / \
      2   3        ← each node has at most 2 children / mỗi node có tối đa 2 con
     / \
    4   5          ← leaf (lá) — no children / không có con
```

```java
// Structure of 1 node in a tree / Cấu trúc 1 node trong cây
class TreeNode {
    int val;            // value / giá trị
    TreeNode left;      // left child / con trái
    TreeNode right;     // right child / con phải
    TreeNode(int val) { this.val = val; }
}
```

---

##### Merge Two Binary Trees — Gộp 2 Cây Nhị Phân

- [ ] **Merge Two Binary Trees** ([LeetCode #617](https://leetcode.com/problems/merge-two-binary-trees/))

**Problem:** Given 2 binary trees, merge them into 1. If 2 nodes overlap, sum their values. If only one side has a node, keep it.

**Đề bài:** Cho 2 cây nhị phân, gộp lại thành 1 cây. Nếu 2 node trùng vị trí thì cộng giá trị, nếu chỉ 1 bên có thì giữ nguyên.

```
Tree 1:      Tree 2:      Result / Kết quả:
    1            2             3       (1+2)
   / \          / \           / \
  3   2        1   3         4   5     (3+1, 2+3)
 /              \           / \
5                4         5   4
```

**How to think:** Like overlaying 2 drawings on top of each other. At each position: if both have a dot, add them; if only one side has a dot, keep it; if both are empty, skip. Use **recursion** — process each node, then call yourself for the left and right subtrees.

**Cách nghĩ:** Giống như trộn 2 bản vẽ bằng cách chồng lên nhau. Ở mỗi vị trí: nếu cả 2 bản đều có điểm thì cộng lại, nếu chỉ 1 bên có thì giữ nguyên, nếu cả 2 đều trống thì bỏ qua. Dùng **đệ quy** (recursion) — xử lý từng node, rồi gọi lại chính mình cho cây con trái và cây con phải.

```java
public TreeNode mergeTrees(TreeNode root1, TreeNode root2) {
    // Base case: if one tree is empty, return the other
    // Trường hợp cơ sở: nếu 1 trong 2 cây rỗng, trả về cây còn lại
    if (root1 == null) return root2;
    if (root2 == null) return root1;

    // Both exist → sum values / Cả 2 đều có → cộng giá trị
    root1.val += root2.val;

    // Recursively merge left and right subtrees
    // Gọi đệ quy cho cây con trái và phải
    root1.left = mergeTrees(root1.left, root2.left);
    root1.right = mergeTrees(root1.right, root2.right);

    return root1;  // Return merged tree / Trả về cây đã gộp
}

// Trace / Chạy thử:
// mergeTrees(1, 2): val = 1+2 = 3
//   left: mergeTrees(3, 1): val = 3+1 = 4
//     left: mergeTrees(5, null): return 5 / trả về 5
//     right: mergeTrees(null, 4): return 4 / trả về 4
//   right: mergeTrees(2, 3): val = 2+3 = 5
// Result: 3 → (4→(5,4), 5) ✓
```

**Complexity / Độ phức tạp:** O(n) time (visit each node once), O(n) space (recursion call stack). / O(n) thời gian (duyệt mỗi node 1 lần), O(n) bộ nhớ (call stack của đệ quy).

**Interview tip:** This is a great problem to show you understand **recursion** — explain that each function call handles 1 node, then "trusts" the recursion to handle the rest.

**Mẹo phỏng vấn:** Đây là bài tuyệt vời để cho thấy bạn hiểu **đệ quy** — giải thích rằng mỗi lần gọi hàm xử lý 1 node, rồi "tin tưởng" đệ quy sẽ lo phần còn lại.

---

##### Increasing Order Search Tree — Chuyển BST Thành Danh Sách Tăng Dần

- [ ] **Increasing Order Search Tree** ([LeetCode #897](https://leetcode.com/problems/increasing-order-search-tree/))

**Problem:** Given a BST (Binary Search Tree — left is always smaller, right is always larger). Rearrange into a tree with only right branches (like a list), in increasing order.

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

**How to think:** BSTs have a special property: **in-order** traversal (left → root → right) produces values in ascending order. Like reading a book left to right — the left side is always smaller. Traverse in-order, and for each node visited, attach it to the right of the previous node.

**Cách nghĩ:** BST có tính chất đặc biệt: duyệt **in-order** (trái → gốc → phải) sẽ ra thứ tự tăng dần. Giống như đọc sách từ trái sang phải — bên trái luôn nhỏ hơn. Duyệt in-order, mỗi node gặp được thì nối vào bên phải của node trước đó.

```java
TreeNode current;  // Pointer to node being built / Con trỏ đến node đang xây dựng

public TreeNode increasingBST(TreeNode root) {
    TreeNode dummy = new TreeNode(0);  // Fake node as starting point / Node giả làm điểm bắt đầu
    current = dummy;

    inOrderTraversal(root);  // Traverse tree in ascending order / Duyệt cây theo thứ tự tăng dần

    return dummy.right;  // Skip fake node, return real tree / Bỏ node giả, trả về cây thật
}

void inOrderTraversal(TreeNode node) {
    if (node == null) return;

    inOrderTraversal(node.left);    // 1. Go left first (smaller numbers)
                                     //    Đi sang trái trước (số nhỏ)

    // 2. Process current node / Xử lý node hiện tại
    node.left = null;               // Remove left branch (result only has right branches)
                                     // Xoá nhánh trái (vì cây kết quả chỉ có nhánh phải)
    current.right = node;           // Attach this node to the right / Nối node này vào bên phải
    current = node;                 // Move pointer forward / Tiến con trỏ lên

    inOrderTraversal(node.right);   // 3. Go right (larger numbers)
                                     //    Đi sang phải (số lớn)
}

// Trace / Chạy thử:
// In-order traversal produces: 1, 2, 3, 4, 5, 6, 7, 8, 9
// Result: 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8 → 9 (right-only) ✓
```

**Complexity / Độ phức tạp:** O(n) time, O(n) space (tree height in call stack). / O(n) thời gian, O(n) bộ nhớ (chiều cao cây trong call stack).

**Key knowledge — 3 ways to traverse a tree: / Kiến thức cần nhớ — 3 cách duyệt cây:**

| Name / Tên | Order / Thứ tự | Like... / Giống như... |
|---|---|---|
| **In-order** | Left → Root → Right / Trái → Gốc → Phải | Reading left to right → **ascending order** in BST / Đọc sách trái sang phải → **ra thứ tự tăng dần** trong BST |
| **Pre-order** | Root → Left → Right / Gốc → Trái → Phải | Exploring a maze — go straight first, then left, then right / Khám phá mê cung — đi thẳng trước, rẽ trái, rẽ phải |
| **Post-order** | Left → Right → Root / Trái → Phải → Gốc | Cleaning a room — clean children first, then parent / Dọn dẹp phòng — dọn con trước, dọn cha sau |

---

##### Second Minimum Node In a Binary Tree — Node Nhỏ Thứ 2

- [ ] **Second Minimum Node In a Binary Tree** ([LeetCode #671](https://leetcode.com/problems/second-minimum-node-in-a-binary-tree/))

**Problem:** Given a special binary tree: each node has 0 or 2 children, and `root.val = min(child1.val, child2.val)`. Find the second minimum value. Return -1 if none exists.

**Đề bài:** Cho cây nhị phân đặc biệt: mỗi node có 0 hoặc 2 con, và `root.val = min(child1.val, child2.val)`. Tìm giá trị nhỏ thứ 2 trong cây. Trả về -1 nếu không có.

```
Input:       2              Input:    2
            / \                      / \
           2   5                    2   2
          / \
         5   7
Output: 5 (2nd smallest)   Output: -1 (all the same / tất cả giống nhau)
```

**How to think:** The root is ALWAYS the smallest value (because each parent = min of its 2 children). So we just need to find the SMALLEST value that is DIFFERENT from root. Traverse the tree; for any node with value > root.val, compare it to see if it's the smallest candidate. Trick: if you find a node > root.val, you DON'T NEED to go deeper (its children are guaranteed >= it).

**Cách nghĩ:** Root luôn là giá trị NHỎ NHẤT (vì mỗi cha = min của 2 con). Vậy ta chỉ cần tìm giá trị NHỎ NHẤT mà KHÁC root. Duyệt toàn bộ cây, mỗi node mà giá trị > root.val thì so sánh xem có phải nhỏ nhất không. Mẹo: nếu gặp node > root.val thì KHÔNG CẦN đi sâu hơn (vì con của nó chắc chắn >= nó).

```java
public int findSecondMinimumValue(TreeNode root) {
    long result = Long.MAX_VALUE;  // Use long to avoid clash with Integer.MAX_VALUE
                                    // Dùng long để tránh trùng với Integer.MAX_VALUE
    int smallest = root.val;       // Root is always the smallest / root luôn là giá trị nhỏ nhất

    result = search(root, smallest, result);

    return result == Long.MAX_VALUE ? -1 : (int) result;
}

long search(TreeNode node, int smallest, long result) {
    if (node == null) return result;

    // If node > smallest → candidate for "second smallest"
    // Nếu node > nhỏ nhất → ứng viên cho "nhỏ thứ 2"
    if (node.val > smallest) {
        result = Math.min(result, node.val);  // Update if smaller than current result
        return result;  // No need to go deeper (children >= parent)
                         // Không cần đi sâu hơn (con >= cha)
    }

    // node.val == smallest → keep searching in children
    // node.val == nhỏ nhất → cần tìm tiếp ở con
    result = search(node.left, smallest, result);
    result = search(node.right, smallest, result);

    return result;
}

// Trace / Chạy thử: tree [2, 2, 5, 5, 7]
//         2
//        / \
//       2   5      ← 5 > 2, candidate! result = 5. Don't go deeper.
//      / \
//     5   7        ← 5 > 2, result = min(5,5) = 5. 7 > 2, result = min(5,7) = 5.
// → Result: 5 ✓
```

**Complexity / Độ phức tạp:** O(n) time (worst case traverse all), O(n) space (call stack). / O(n) thời gian (trường hợp xấu nhất duyệt hết), O(n) bộ nhớ (call stack).

---

#### Math & Other — Toán & Khác

---

##### Palindrome Number — Số Đối Xứng

- [ ] **Palindrome Number** ([LeetCode #9](https://leetcode.com/problems/palindrome-number/))

**Problem:** Check if an integer reads the same forwards and backwards.

**Đề bài:** Kiểm tra số nguyên có đọc xuôi và ngược giống nhau không.

```
Input: 121   Output: true   (reversed is still 121 / đọc ngược vẫn là 121)
Input: -121  Output: false  (reversed is 121- / đọc ngược là 121-)
Input: 10    Output: false  (reversed is 01 / đọc ngược là 01)
```

**How to think:** Reverse the number, then compare with the original. Like writing a number on paper and flipping it.

**Cách nghĩ:** Đảo ngược số, rồi so sánh với số gốc. Giống như viết số ra giấy rồi lật ngược.

```java
public boolean isPalindrome(int x) {
    if (x < 0) return false;  // Negative numbers are never palindromes
                                // Số âm không bao giờ đối xứng

    int original = x;
    int reversed = 0;

    while (x > 0) {
        int lastDigit = x % 10;                    // Get last digit: 121 % 10 = 1
        reversed = reversed * 10 + lastDigit;       // Build reversed number
        x = x / 10;                                 // Remove last digit: 121 / 10 = 12
    }

    return original == reversed;
}

// Trace / Chạy thử: x = 121
// Step 1: lastDigit=1, reversed=1,   x=12
// Step 2: lastDigit=2, reversed=12,  x=1
// Step 3: lastDigit=1, reversed=121, x=0
// 121 == 121 → true ✓
```

---

##### FizzBuzz

- [ ] **FizzBuzz** ([LeetCode #412](https://leetcode.com/problems/fizz-buzz/))

**Problem:** Print numbers 1 to n: divisible by 3 → "Fizz", by 5 → "Buzz", by both → "FizzBuzz".

**Đề bài:** In số từ 1 đến n: chia hết cho 3 in "Fizz", chia hết cho 5 in "Buzz", chia hết cho cả 2 in "FizzBuzz".

```
Input:  n = 15
Output: ["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]
```

**How to think:** Check from the STRICTEST condition first (divisible by 15) to LOOSER ones (divisible by 3, by 5).

**Cách nghĩ:** Kiểm tra từ điều kiện CHẶT NHẤT trước (chia hết cho 15) đến LỎNG HƠN (chia hết cho 3, chia hết cho 5).

```java
public List<String> fizzBuzz(int n) {
    List<String> result = new ArrayList<>();

    for (int i = 1; i <= n; i++) {
        if (i % 15 == 0) {       // Divisible by BOTH 3 AND 5 → check FIRST
            result.add("FizzBuzz");
        } else if (i % 3 == 0) { // Only divisible by 3
            result.add("Fizz");
        } else if (i % 5 == 0) { // Only divisible by 5
            result.add("Buzz");
        } else {                  // Not divisible by either
            result.add(String.valueOf(i));
        }
    }
    return result;
}
```

---

#### Bonus Problems — Bài Thêm (If Time Permits / Nếu Còn Thời Gian)

---

##### Best Time to Buy and Sell Stock — Mua Bán Cổ Phiếu

- [ ] **Best Time to Buy and Sell Stock** ([LeetCode #121](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/))

**Problem:** Given stock prices by day, find the maximum profit from buying on one day and selling on a LATER day.

**Đề bài:** Cho mảng giá cổ phiếu theo ngày, tìm lợi nhuận lớn nhất khi mua 1 ngày và bán 1 ngày SAU ĐÓ.

```
Input:  [7, 1, 5, 3, 6, 4]
Output: 5              (Buy day 2 at price 1, sell day 5 at price 6 → profit 5)
                       (Mua ngày 2 giá 1, bán ngày 5 giá 6 → lời 5)
```

**How to think:** Go through each day: remember the LOWEST price seen so far, calculate profit if selling TODAY, update max profit.

**Cách nghĩ:** Đi qua từng ngày: nhớ GIÁ THẤP NHẤT đã thấy, tính lợi nhuận nếu bán HÔM NAY, cập nhật lợi nhuận lớn nhất.

```java
public int maxProfit(int[] prices) {
    int minPrice = Integer.MAX_VALUE;  // Lowest price seen / Giá thấp nhất đã thấy
    int maxProfit = 0;                 // Maximum profit / Lợi nhuận lớn nhất

    for (int price : prices) {
        minPrice = Math.min(minPrice, price);               // Update lowest price
        maxProfit = Math.max(maxProfit, price - minPrice);   // Profit if selling today
    }
    return maxProfit;
}

// Trace / Chạy thử: [7, 1, 5, 3, 6, 4]
// price=7: min=7, profit=0
// price=1: min=1, profit=0    (1-1=0)
// price=5: min=1, profit=4    (5-1=4)
// price=3: min=1, profit=4    (3-1=2, keep 4)
// price=6: min=1, profit=5    (6-1=5) ← MAX
// price=4: min=1, profit=5    (4-1=3, keep 5)
// → 5 ✓
```

---

##### Maximum Subarray — Mảng Con Có Tổng Lớn Nhất

- [ ] **Maximum Subarray** ([LeetCode #53](https://leetcode.com/problems/maximum-subarray/))

**Problem:** Find the contiguous subarray with the largest sum.

**Đề bài:** Tìm mảng con liên tiếp có tổng lớn nhất.

```
Input:  [-2, 1, -3, 4, -1, 2, 1, -5, 4]
Output: 6              (subarray [4, -1, 2, 1] has sum = 6)
                       (mảng con [4, -1, 2, 1] có tổng = 6)
```

**How to think (Kadane's Algorithm):** At each step, ask: "Should I CONTINUE adding from before, or START FRESH from here?" If currentSum + newElement < newElement alone, then start fresh.

**Cách nghĩ (Thuật toán Kadane):** Tại mỗi bước, hỏi: "Nên TIẾP TỤC cộng dồn từ trước, hay BẮT ĐẦU MỚI từ đây?" Nếu tổng hiện tại + phần tử mới < chỉ phần tử mới thì bắt đầu mới.

```java
public int maxSubArray(int[] nums) {
    int currentSum = nums[0];  // Sum of current subarray / Tổng của mảng con đang xét
    int maxSum = nums[0];      // Largest sum found / Tổng lớn nhất đã tìm thấy

    for (int i = 1; i < nums.length; i++) {
        // Continue accumulating, or start fresh?
        // Tiếp tục cộng dồn, hoặc bắt đầu mới?
        currentSum = Math.max(nums[i], currentSum + nums[i]);
        maxSum = Math.max(maxSum, currentSum);
    }
    return maxSum;
}
```

---

##### Climbing Stairs — Leo Cầu Thang

- [ ] **Climbing Stairs** ([LeetCode #70](https://leetcode.com/problems/climbing-stairs/))

**Problem:** Climb n stairs, each step you climb 1 or 2 stairs. How many distinct ways?

**Đề bài:** Leo n bậc thang, mỗi bước leo 1 hoặc 2 bậc. Có bao nhiêu cách?

```
Input: n=3  Output: 3  (3 ways: 1+1+1, 1+2, 2+1 / 3 cách: 1+1+1, 1+2, 2+1)
```

**How to think:** To reach step n, you can come from step n-1 (climb 1) or step n-2 (climb 2). So: ways(n) = ways(n-1) + ways(n-2) — just like Fibonacci!

**Cách nghĩ:** Để đến bậc n, bạn có thể từ bậc n-1 (bước 1 bậc) hoặc từ bậc n-2 (bước 2 bậc). Vậy: số_cách(n) = số_cách(n-1) + số_cách(n-2) — giống dãy Fibonacci!

```java
public int climbStairs(int n) {
    if (n <= 2) return n;

    int twoStepsBefore = 1;  // ways(1) = 1 / số_cách(1) = 1
    int oneStepBefore = 2;   // ways(2) = 2 / số_cách(2) = 2

    for (int i = 3; i <= n; i++) {
        int current = oneStepBefore + twoStepsBefore;  // Fibonacci
        twoStepsBefore = oneStepBefore;
        oneStepBefore = current;
    }
    return oneStepBefore;
}
```

---

## Block 2 (2h) — Mock Interview / Phỏng Vấn Thử

---

### Round 1: Full Simulation (30 minutes) / Vòng 1: Mô Phỏng Đầy Đủ (30 phút)

- [ ] **Set a 30-min timer and do it like a real interview: / Bật đồng hồ 30 phút và làm như phỏng vấn thật:**
  - [ ] 5 min: Self-introduction in English / 5 phút: Tự giới thiệu bằng tiếng Anh
  - [ ] 10 min: Ask yourself technical questions (mix English/Vietnamese): / 10 phút: Tự hỏi và trả lời các câu hỏi kỹ thuật (xen kẽ Anh/Việt):
    - "What is OOP?"
    - "Explain the difference between ArrayList and LinkedList"
    - "What is REST API?"
    - "Tell me about your project"
  - [ ] 15 min: Solve 1 LeetCode Easy (pick any above) / 15 phút: Giải 1 bài LeetCode Easy (chọn bất kỳ ở trên)
  - [ ] Review: What went well? What needs work? / Phần nào tốt? Phần nào cần cải thiện?

---

### Round 2: Focus on Weak Spots (30 minutes) / Vòng 2: Tập Trung Vào Điểm Yếu (30 phút)

- [ ] Re-study any shaky concepts / Học lại khái niệm nào còn lủng
- [ ] Practice explaining code out loud — imagine talking to the interviewer / Luyện giải thích code bằng lời — tưởng tượng đang nói với interviewer
- [ ] Solve 1 more LeetCode problem with a timer / Giải thêm 1 bài LeetCode với đồng hồ

---

### Round 3: Speed Run (30 minutes) / Vòng 3: Speed Run (30 phút)

- [ ] Solve Two Sum in 5 minutes / Giải Two Sum trong 5 phút
- [ ] Solve Valid Parentheses in 5 minutes / Giải Valid Parentheses trong 5 phút
- [ ] Explain OOP in 2 minutes (out loud, in English) / Giải thích OOP trong 2 phút (thành tiếng, bằng tiếng Anh)
- [ ] Explain your project in 2 minutes (out loud) / Giải thích project trong 2 phút (thành tiếng)

---

### Final Review (30 minutes) / Ôn Lại Lần Cuối (30 phút)

- [ ] Read through all Day 1 concepts once / Đọc lại tất cả khái niệm Day 1 một lượt
- [ ] Read through all Day 2 answers once / Đọc lại các câu trả lời Day 2 một lượt
- [ ] Make sure you can explain things NATURALLY (without reading) / Chắc chắn mình có thể giải thích TỰ NHIÊN (không đọc)

---

## Interview Day Reminders / Nhắc Nhở Ngày Phỏng Vấn

- [ ] Get a good night's sleep / Ngủ sớm đêm trước
- [ ] Test your camera, mic, and internet / Kiểm tra camera, micro, internet
- [ ] Have water and pen/paper nearby / Có nước uống và giấy bút bên cạnh
- [ ] Open your IDE/editor and LeetCode before the call / Mở sẵn IDE/editor và LeetCode trước khi phỏng vấn
- [ ] **THINK OUT LOUD** when coding — they want to hear how you think / **NÓI RA SUY NGHĨ** khi làm code — họ muốn nghe cách bạn tư duy
- [ ] If you don't know, say "I'm not sure, but I think..." — honesty is better than silence / Không biết thì nói "I'm not sure, but I think..." — trung thực tốt hơn im lặng
- [ ] Be genuine about your projects — they'll ask follow-ups, so don't bluff / Nói thật về project — họ sẽ hỏi sâu, đừng phịnh
- [ ] Technical terms in English are fine; explain ideas in whichever language you're more comfortable with / Thuật ngữ kỹ thuật dùng tiếng Anh OK, giải thích ý tưởng bằng ngôn ngữ nào thoải mái hơn

---

> **Good luck with your interview! You've prepared 15 hours — believe in yourself!**
>
> **Chúc bạn phỏng vấn thành công! Bạn đã chuẩn bị 15 tiếng — hãy tự tin vào bản thân!**
