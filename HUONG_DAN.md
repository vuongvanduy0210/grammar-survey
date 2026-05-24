# 📘 Hướng dẫn sử dụng & chỉnh sửa Grammar Survey

> File này dành cho người không cần biết lập trình.
> Đọc xong là bạn có thể tự sửa câu, tự test, tự deploy.

---

## 📑 Mục lục

1. [Files trong thư mục này](#1-files-trong-thư-mục-này)
2. [Cấu trúc file experiment](#2-cấu-trúc-file-experiment)
3. [Setup lần đầu (GitHub + Vercel + DataPipe)](#3-setup-lần-đầu)
4. [Hướng dẫn sửa nội dung](#4-hướng-dẫn-sửa-nội-dung)
5. [Test sau khi sửa](#5-test-sau-khi-sửa)
6. [Lấy dữ liệu participants](#6-lấy-dữ-liệu-participants)
7. [Các lỗi thường gặp](#7-các-lỗi-thường-gặp)

---

## 1. Files trong thư mục này

| File | Tác dụng |
|---|---|
| `experiment_jspsych.html` | **File chính** — chứa toàn bộ survey. Đây là file bạn sửa khi muốn đổi nội dung. |
| `HUONG_DAN.md` | File hướng dẫn này |
| `Consent form +  PCIbex Farm (1).txt` | Phiên bản cũ trên PCIbex (không dùng nữa, giữ để tham khảo) |

---

## 2. Cấu trúc file experiment

Mở file `experiment_jspsych.html` bằng bất kỳ text editor nào (VS Code, Notepad, TextEdit, hoặc trực tiếp trong GitHub web editor).

File chia làm **2 phần** rõ ràng:

### 📝 Phần 1: NỘI DUNG — Có thể sửa thoải mái

Nằm ở đầu file, đánh dấu bằng box `📝 PHẦN NỘI DUNG — CHỈNH SỬA TẠI ĐÂY`. Trong đó có các block với icon:

| Icon | Block | Nội dung |
|---|---|---|
| 💾 | `DATAPIPE_EXPERIMENT_ID` | ID DataPipe (xem section 3 để lấy) |
| ⏱️ | `TIMER_SECONDS` | Thời gian mỗi câu (mặc định 10 giây) |
| ⏱️ | `IELTS_REJECT_SCORES` | Các điểm IELTS bị loại |
| ⏱️ | `IELTS_SCORE_OPTIONS` | Danh sách điểm hiển thị cho user chọn |
| 📋 | `CONSENT_HTML` | Text consent ở trang đầu |
| 🙏 | `IELTS_REJECT_HTML` | Text khi user IELTS thấp |
| ❓ | `BACKGROUND_QUESTIONS` | 9 câu hỏi background |
| 📖 | `JUDGMENT_INTRO_HTML` | Giới thiệu phần judgment |
| 🏋️ | `PRACTICE_SENTENCES` | 5 câu practice |
| ✅ | `PRACTICE_DONE_HTML` | Trang sau practice |
| 🎲 | `CONDITIONS` | 8 conditions — **không nên đổi** |
| 🎯 | `TARGET_SETS` | 8 sets × 8 câu target |
| 🃏 | `FILLERS` | 16 câu filler |
| 🎉 | `ENDING_HTML` | Trang kết thúc |

### ⚙️ Phần 2: LOGIC — Không cần đụng vào

Nằm sau box `⚙️ PHẦN LOGIC — KHÔNG CẦN CHỈNH`. Đây là code chạy survey (timer, randomization, save data). Sửa vào đây có thể gây lỗi, **không nên động vào**.

---

## 3. Setup lần đầu

Làm 1 lần, mất khoảng 15-20 phút. Sau đó chỉ cần sửa file trên GitHub là Vercel tự deploy.

### Bước A: Push code lên GitHub

#### A.1 Tạo repo mới

1. Vào https://github.com → bấm dấu **+** góc trên phải → **New repository**
2. Đặt tên: `grammar-survey` (hoặc tên gì bạn muốn)
3. Chọn **Public** (Vercel free tier yêu cầu public; private cần plan trả phí)
4. Bỏ tick "Add a README", "Add .gitignore", "Choose a license" (để repo rỗng)
5. Bấm **Create repository**

#### A.2 Upload file lên repo

Cách dễ nhất: **dùng giao diện web GitHub** (không cần git terminal):

1. Trong repo vừa tạo, click link **"uploading an existing file"** (hoặc vào tab Add file → Upload files)
2. Kéo thả file `experiment_jspsych.html` từ máy vào trang web
3. Cuộn xuống, ô **Commit changes**: gõ message như `Initial upload`
4. Bấm **Commit changes**

Bây giờ repo đã có file. URL của repo dạng: `https://github.com/[username]/grammar-survey`

### Bước B: Deploy lên Vercel

#### B.1 Đăng ký Vercel (Sign in với GitHub)

1. Vào https://vercel.com → bấm **Sign Up**
2. Chọn **Continue with GitHub** → cho phép Vercel access GitHub
3. Hoàn tất profile (chọn Hobby/Free plan)

#### B.2 Import repo

1. Trong dashboard Vercel, bấm **Add New...** → **Project**
2. Tìm repo `grammar-survey` trong danh sách → bấm **Import**
3. Trang config hiện ra, **để default tất cả** (không cần đổi gì)
4. Bấm **Deploy**
5. Đợi ~30 giây → "Congratulations!" → bạn được URL dạng `https://grammar-survey-xxx.vercel.app`
6. **Bookmark URL này** — đây là link gửi cho participants

> 💡 Vercel tự deploy lại mỗi khi bạn sửa file trên GitHub. Không cần làm gì thêm.

### Bước C: Setup DataPipe (để collect data)

#### C.1 Đăng ký OSF (tài khoản cha của DataPipe)

1. Vào https://osf.io/register → đăng ký bằng email (free)
2. Xác nhận email

#### C.2 Tạo OSF project mới (làm container chứa data)

1. Login OSF → bấm **Create new project** ở dashboard
2. Đặt tên (vd `Grammar Survey Data`)
3. Bấm **Create**
4. Vào project vừa tạo → tab **Files** → chọn folder **OSF Storage** → bấm **Create folder** → tạo folder tên `data` (hoặc gì cũng được)
5. **Make project public**: cần để DataPipe ghi file vào. Vào Settings → tích "Make project public" (hoặc bạn có thể giữ private nhưng cần config sâu hơn)

#### C.3 Đăng ký DataPipe + tạo experiment

1. Vào https://pipe.jspsych.org → bấm **Login** → sign in với OSF account (cùng acc vừa tạo)
2. Sau khi login, bấm **New experiment**
3. Điền:
   - **Name**: `Grammar Survey` (hoặc tên gì cũng được)
   - **OSF Project**: chọn project vừa tạo ở bước C.2
   - **Path**: chọn folder `data` vừa tạo
4. Bấm **Create** → bạn được **Experiment ID** (chuỗi 10-20 ký tự, ví dụ: `aBcDeFgHiJ`)
5. **Copy Experiment ID này** — bước tiếp theo cần dùng

### Bước D: Paste DataPipe ID vào code

1. Vào GitHub repo `grammar-survey` → click file `experiment_jspsych.html`
2. Click icon **bút chì** ✏️ (Edit this file) — góc trên phải
3. Dùng **Ctrl+F** (hoặc Cmd+F) → tìm `DATAPIPE_EXPERIMENT_ID`
4. Tìm dòng:
   ```javascript
   const DATAPIPE_EXPERIMENT_ID = "";
   ```
5. Paste ID vào giữa 2 dấu nháy, ví dụ:
   ```javascript
   const DATAPIPE_EXPERIMENT_ID = "aBcDeFgHiJ";
   ```
6. Cuộn xuống cuối trang → **Commit changes** → gõ message `Add DataPipe ID` → **Commit**
7. Vercel sẽ tự deploy lại trong ~30 giây

### Bước E: Test full workflow

1. Mở URL Vercel (vd `https://grammar-survey-xxx.vercel.app`) trên cả desktop và điện thoại
2. Làm thử survey từ đầu đến cuối
3. Sau khi xong, vào https://pipe.jspsych.org → mở experiment → tab **Data** → kiểm tra có file CSV mới không
4. Hoặc vào OSF project → folder data → có file CSV mới
5. Nếu thấy data ✅ → setup xong!

---

## 4. Hướng dẫn sửa nội dung

### 4.1 Cách mở để sửa (qua GitHub web — không cần cài gì)

1. Vào https://github.com/[username]/grammar-survey
2. Click file `experiment_jspsych.html`
3. Click icon **bút chì** ✏️ (Edit this file)
4. Sửa code trong editor web
5. Cuộn xuống cuối → ô **Commit changes**
6. Gõ message ngắn mô tả thay đổi (vd `Update target sentences`)
7. Bấm **Commit changes**
8. **Vercel sẽ tự deploy lại trong ~30 giây** — URL không đổi, code mới live ngay
9. Refresh URL trên browser để test thay đổi

### 4.2 Quy tắc cần nhớ

| Quy tắc | Ví dụ ĐÚNG | Ví dụ SAI |
|---|---|---|
| Text trong cặp `"..."` | `"The boy eats cookies."` | `The boy eats cookies.` |
| Mỗi item trong list cách nhau bằng `,` | `"câu 1",`<br>`"câu 2"` | `"câu 1"`<br>`"câu 2"` |
| Không đặt `,` sau item cuối | xem code mẫu | thêm `,` thừa |
| Nếu trong câu có dấu `"`, viết `\"` | `"He said \"hi\"."` | `"He said "hi"."` |
| HTML tags dùng được | `<b>bold</b>`, `<br>`, `<p>` | (tất cả) |

### 4.3 Ví dụ sửa thực tế

#### Đổi thời gian timer từ 10s thành 15s

Tìm dòng:
```javascript
const TIMER_SECONDS = 10;
```

Đổi thành:
```javascript
const TIMER_SECONDS = 15;
```

Commit → 30s sau live.

#### Đổi ngưỡng IELTS reject

Hiện tại reject IELTS 6.0 và 6.5. Muốn cho IELTS 6.5 tham gia (chỉ reject 6.0):

Tìm:
```javascript
const IELTS_REJECT_SCORES = ["6.0", "6.5"];
```

Đổi thành:
```javascript
const IELTS_REJECT_SCORES = ["6.0"];
```

#### Sửa câu target (giữ nguyên cấu trúc)

> ⚠️ KHÔNG nên thêm/xóa số câu trong target sets — phải khớp với số CONDITIONS (8). Chỉ sửa nội dung câu.

Tìm câu cần đổi trong `TARGET_SETS`, ví dụ:
```javascript
"The boy eats cookies every afternoon.",
```

Đổi thành:
```javascript
"The student reads books every evening.",
```

#### Thêm câu filler mới

Tìm `FILLERS`, thêm item mới (nhớ dấu `,` sau item áp chót):
```javascript
const FILLERS = [
  { id: "filler_01", sentence: "..." },
  ...
  { id: "filler_16", sentence: "The lady had better not..." },
  { id: "filler_17", sentence: "Câu mới của bạn ở đây." }
];
```

#### Sửa text consent

Tìm `CONSENT_HTML`. Đây là HTML — sửa text giữa các tag `<p>`, `<b>`, `<li>` thoải mái, đừng đụng vào `<` và `>`.

#### Thêm câu background question

Tìm `BACKGROUND_QUESTIONS`, thêm item:
```javascript
{
  id: "q10",
  question: "10. Câu hỏi mới?",
  hint: "(Gợi ý nếu cần)"
}
```

> 💡 `id` phải duy nhất.

---

## 5. Test sau khi sửa

### Test trên desktop

1. Sau khi commit trên GitHub → đợi ~30 giây cho Vercel deploy xong
2. Mở URL Vercel trên browser (Ctrl+Shift+R để hard refresh tránh cache)
3. Bấm qua từng màn xem có lỗi không

### Test trên điện thoại

Mở URL Vercel trên điện thoại — đảm bảo UI mobile ổn.

### Test full flow với DataPipe

1. Làm survey đến cuối
2. Vào https://pipe.jspsych.org → experiment → Data → check có row mới
3. Nếu có → OK

> ⚠️ **Lưu ý**: Mỗi lần test bạn cũng tạo 1 row data. Vào DataPipe xóa row test khi cần thu data thật.

---

## 6. Lấy dữ liệu participants

### Cách 1: Từ DataPipe dashboard

1. Login https://pipe.jspsych.org
2. Mở experiment
3. Tab **Data** → thấy danh sách CSV files (mỗi participant = 1 file)
4. Bấm **Download all** để tải zip toàn bộ

### Cách 2: Từ OSF project

1. Login https://osf.io
2. Mở project → folder `data`
3. Tải từng file, hoặc dùng OSF API/CLI để batch download

### Cột data quan trọng

| Cột | Ý nghĩa |
|---|---|
| `task` | Tên trial (consent, judgement, filler, etc.) |
| `item_id` | ID câu (target_xxx hoặc filler_xx) |
| `condition` | 1 trong 8 conditions |
| `grammaticality` | grammatical / ungrammatical |
| `rating_first_value` | Rating đầu tiên user click (1-7) |
| `rating_final_value` | Rating cuối cùng khi submit |
| `rating_rt_ms` | Thời gian phản ứng (ms) — đến click đầu tiên |
| `submit_rt_ms` | Thời gian đến lúc bấm Next |
| `response_status` | submitted / timed_out_after_rating / timed_out_no_rating |
| `participant_set` | Set người này được phân (1-8) |
| `ielts_score` | Điểm IELTS user khai |

---

## 7. Các lỗi thường gặp

### ❌ "Survey không hiển thị gì sau khi commit"

**Nguyên nhân**: Sai cú pháp (thiếu `"`, `,`, `}` etc.)

**Cách sửa**:
1. Mở **DevTools Console** (F12 → tab Console)
2. Đọc message màu đỏ — báo dòng nào lỗi
3. Quay lại GitHub editor → tới dòng đó → kiểm tra `"`, `,`, `}`, `]`

### ❌ "Vercel báo build failed"

**Nguyên nhân**: HTML không hợp lệ

**Cách sửa**:
1. Vercel dashboard → Project → tab Deployments → bấm deployment failed → xem log
2. Thường log chỉ ra dòng nào sai
3. Quay GitHub sửa → commit lại → Vercel tự deploy lại

### ❌ "Sửa rồi mà không thấy đổi"

**Nguyên nhân**: Cache browser hoặc Vercel chưa deploy xong

**Cách sửa**:
1. Đợi 1 phút (Vercel build có thể chậm)
2. Hard refresh: `Ctrl+Shift+R` (Cmd+Shift+R trên Mac)
3. Check Vercel dashboard → tab Deployments → chắc deployment mới nhất status "Ready"

### ❌ "Data không lưu vào DataPipe"

**Nguyên nhân**:
1. DATAPIPE_EXPERIMENT_ID sai
2. OSF project chưa public
3. Network error participant

**Cách sửa**:
1. Mở `experiment_jspsych.html` → kiểm tra `DATAPIPE_EXPERIMENT_ID` đúng (copy lại từ DataPipe)
2. Vào OSF project → Settings → tick "Make public"
3. Mở DevTools Console khi test → xem có error đỏ liên quan đến `pipe.jspsych.org`

### ❌ "Trang trắng khi mở trên điện thoại"

**Nguyên nhân**: Có thể network điện thoại lỗi

**Cách sửa**:
1. Thử URL trên trình duyệt máy tính trước
2. Reload trên điện thoại (kéo xuống refresh)

### ❌ "Timer không countdown"

**Nguyên nhân**: Sửa nhầm `TIMER_SECONDS` thành chuỗi

**Cách sửa**: Kiểm tra:
```javascript
const TIMER_SECONDS = 10;     // ĐÚNG (số, không nháy)
const TIMER_SECONDS = "10";   // SAI (chuỗi, có nháy)
```

---

## 📞 Liên hệ

Nếu gặp lỗi không tự sửa được:
1. Chụp màn hình lỗi (cả màn hình + Console DevTools nếu có)
2. Ghi rõ: bạn vừa sửa gì, ở section nào
3. Gửi cho developer hỗ trợ

---

## 📚 Links nhanh

- GitHub repo: `https://github.com/[username]/grammar-survey`
- Vercel dashboard: https://vercel.com/dashboard
- DataPipe dashboard: https://pipe.jspsych.org
- OSF project: https://osf.io/myprojects

**Survey URL** (gửi cho participants): `https://grammar-survey-xxx.vercel.app`

---

## 📚 Tài liệu thêm (nếu muốn tìm hiểu sâu)

- jsPsych docs: https://www.jspsych.org
- DataPipe docs: https://pipe.jspsych.org/getting-started
- Vercel docs: https://vercel.com/docs
- GitHub docs: https://docs.github.com

Không cần đọc các docs trên trừ khi muốn customize sâu hơn.
