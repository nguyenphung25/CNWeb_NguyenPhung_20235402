# Prompt phát hiện & sửa lỗi HTML cho `blog_wrong.html` (công thức CRAFT)

## Prompt

```text
[C – CONTEXT / BỐI CẢNH]
Tôi đang làm bài tập môn Công nghệ Web. Tôi có file blog_wrong.html – trang "Blog" của một
website template tĩnh (Blakletterpress), chỉ dùng HTML + file CSS ngoài (css/style.css),
không dùng framework. File này bị cố tình cài nhiều lỗi HTML, nhưng cũng có một số đoạn
trông bất thường mà vẫn hoàn toàn hợp lệ; đó là các "bẫy" kiểm tra khả năng phân biệt lỗi
chuẩn với sở thích viết mã. Phần lớn các lỗi thật vẫn hiển thị
gần như bình thường vì trình duyệt tự "đoán và sửa" (error recovery), nên KHÔNG thể phát hiện
bằng cách nhìn giao diện. Tôi cần phát hiện chúng dựa trên chuẩn HTML5 (WHATWG HTML Living
Standard) và kết quả của W3C Markup Validator (validator.w3.org).
Ràng buộc: chỉ sửa lỗi có thể chứng minh bằng quy tắc chuẩn cụ thể. Giữ nguyên nội dung,
cấu trúc bố cục, URL, hành vi JavaScript và class/id đang được CSS sử dụng; không thêm thư
viện, không đổi giao diện. Không được tự áp dụng các khuyến nghị hoặc refactor vào file sửa.

[R – ROLE / VAI TRÒ]
Hãy đóng vai một Front-end Developer kỳ cựu kiêm chuyên gia kiểm định chuẩn W3C và khả năng
truy cập (WCAG 2.1), có kinh nghiệm review code HTML cho sinh viên.

[A – ACTION / NHIỆM VỤ]
1. Đọc kỹ TỪNG DÒNG mã nguồn bên dưới (không bỏ qua phần header, sidebar, footer).
2. Phát hiện toàn bộ lỗi, tối thiểu rà soát các nhóm sau:
   a. Khai báo tài liệu: DOCTYPE, <html lang>, <meta charset> (giá trị hợp lệ), số lượng <title>.
      Lưu ý: thiếu lang chỉ là cảnh báo/khuyến nghị trong bài này, không tự động là lỗi cú pháp.
   b. Cấu trúc & lồng thẻ: thẻ không đóng, thẻ đóng không khớp thẻ mở (vd mở <ul> đóng <ol>),
      thẻ lồng sai mô hình nội dung (vd phần tử không phải <li> nằm trực tiếp trong <ul>/<ol>),
      thẻ <a> lồng nhau hoặc chưa đóng.
   c. Thuộc tính: thuộc tính bị lặp trên cùng một phần tử, giá trị sai kiểu
      (vd width/height có đơn vị "px"), id bị trùng trong cùng trang.
   d. Liên kết & URL: URL không hợp lệ và thẻ liên kết chưa đóng. Không suy đoán một URL là
      "sai đích" chỉ vì nó khác các link bên cạnh; href="" là URL tham chiếu tài liệu hiện tại;
      dấu & thô chỉ sai khi tạo thành ambiguous ampersand/character reference không hợp lệ.
   e. Khả năng truy cập & ngữ nghĩa: <img> thiếu alt, liên kết không có accessible name và
      thứ bậc heading. Phân biệt rõ lỗi HTML với khuyến nghị WCAG; <i>, <b>, <h1>–<h6> đều là
      phần tử HTML hợp lệ và không được đổi chỉ vì có lựa chọn ngữ nghĩa khác tốt hơn.
   f. Các lỗi khác mà W3C Validator sẽ báo (error) hoặc cảnh báo (warning).
3. Với mỗi lỗi: giải thích vì sao sai, vì sao trình duyệt vẫn hiển thị "bình thường"
   và hậu quả tiềm ẩn (SEO, accessibility, CSS/JS chọn nhầm phần tử, validator...).
4. Sửa toàn bộ lỗi thật bằng thay đổi nhỏ nhất và xuất ra file HTML hoàn chỉnh đã sửa.
5. Tự kiểm tra lại: đảm bảo bản sửa sẽ qua W3C Validator với 0 error, và không thay đổi
   giao diện hiện tại.
Không tự bịa lỗi; nếu một điểm chỉ là khuyến nghị (không phải lỗi chuẩn) thì ghi rõ
"Khuyến nghị" thay vì "Lỗi" và TUYỆT ĐỐI KHÔNG triển khai khuyến nghị đó vào mã đã sửa.

[DANH SÁCH BẤT BIẾN – PHẢI BẢO VỆ]
Các đoạn sau trong blog_wrong.html là hợp lệ hoặc nằm ngoài phạm vi sửa lỗi. Phải giữ nguyên
từng đoạn trong file đầu ra; chỉ được nêu ở mục khuyến nghị nếu thật sự cần:
1. Giữ nguyên thẻ mở <html> không có lang; không tự thêm lang="en".
2. Giữ nguyên <i>free</i>. <i> là phần tử HTML hợp lệ, không phải thẻ obsolete.
3. Giữ nguyên URL href="blog.html?page=2&sort=new". Chuỗi &sort= không phải ambiguous
   ampersand vì không kết thúc bằng dấu chấm phẩy; không được suy đoán link "First" sai đích.
4. Giữ nguyên href="" của nút "View More". Đây là empty relative URL tham chiếu chính tài liệu,
   không phải lỗi cú pháp và không có đủ dữ kiện để đổi thành news.html.
5. Giữ nguyên onBlur/onFocus cùng tiền tố javascript:. Trong event-handler attribute,
   javascript: được phân tích như một JavaScript label hợp lệ; có thể thừa nhưng không sai.
6. Giữ nguyên các thẻ <h5> trong #posts. Không đổi heading chỉ để "đẹp" outline.
7. Giữ nguyên các <a> icon rỗng và target="_blank" không có rel/aria-label. Có thể báo khuyến
   nghị accessibility, nhưng đây không phải lỗi cú pháp HTML và không được sửa trong đầu ra.
8. Khi xử lý class bị lặp ở class="sitename" class="brand", phải giữ class đầu tiên mà trình
   duyệt đang dùng và xoá thuộc tính lặp: class="sitename". Không gộp thành class="sitename brand"
   vì thao tác đó làm class brand bắt đầu có hiệu lực và có thể đổi CSS/JS.
9. Không thêm aria-label, rel, placeholder; không sửa nội dung event handler; không đổi URL,
   heading hay văn bản nếu thay đổi đó không bắt buộc để khắc phục một lỗi chuẩn đã chứng minh.

Trước khi xuất kết quả, tạo diff trong suy luận giữa đầu vào và đầu ra. Mỗi dòng thay đổi phải
ánh xạ được tới đúng một lỗi thật trong bảng; hoàn tác mọi thay đổi chỉ phục vụ khuyến nghị.

[F – FORMAT / ĐỊNH DẠNG ĐẦU RA]
Trả lời bằng tiếng Việt, theo đúng 4 phần:
Phần 1 – Bảng tổng hợp lỗi (Markdown) gồm các cột:
  | STT | Dòng | Đoạn mã sai | Nhóm lỗi | Mức độ (Lỗi/Cảnh báo/Khuyến nghị) | Giải thích | Cách sửa |
Phần 2 – Giải thích chi tiết các lỗi "ẩn" (hiển thị vẫn đúng nhưng sai chuẩn), mỗi lỗi 2–3 câu.
Phần 3 – Mã nguồn HTML đầy đủ sau khi sửa, trong một khối ```html```, có comment
  <!-- FIX: ... --> ngay tại mỗi vị trí đã sửa.
Phần 4 – Checklist tự kiểm tra (tổng số lỗi đã sửa, kết quả dự kiến khi chạy W3C Validator).

[T – TARGET AUDIENCE / ĐỐI TƯỢNG & GIỌNG VĂN]
Người đọc là sinh viên năm 2–3 ngành CNTT, đã biết HTML/CSS cơ bản nhưng chưa quen đọc báo
cáo validator. Giọng văn rõ ràng, sư phạm, ngắn gọn; thuật ngữ tiếng Anh giữ nguyên kèm
giải thích tiếng Việt khi xuất hiện lần đầu.

Mã nguồn blog_wrong.html:
D:\20261_CN_WEB\assignment_02\blog_wrong.html
"""
<dán toàn bộ nội dung file blog_wrong.html vào đây>
"""
```

## Đáp án tham khảo (để đối chiếu kết quả AI trả về)

| # | Dòng | Lỗi trong `blog_wrong.html` | Sửa |
|---|------|------------------------------|-----|
| 1 | 5 | `charset="utf8"` không dùng nhãn chuẩn dành cho tác giả | `charset="UTF-8"` |
| 2 | 6–7 | Hai thẻ `<title>` trong `<head>` | Giữ một `<title>` |
| 3 | 14 | Thuộc tính `class` bị lặp (`class="sitename" class="brand"`) | Giữ duy nhất `class="sitename"`; không gộp `brand` |
| 4 | 14 | `width="142px"` — thuộc tính width/height chỉ nhận số nguyên không đơn vị | `width="142"` |
| 5 | 16 | `<img>` thiếu `alt` | Thêm `alt="Text"` |
| 6 | 73 | `<div class="ad">` nằm trực tiếp trong `<ul>` (con trực tiếp phải là `<li>` hoặc phần tử hỗ trợ script) | Chuyển `<div>` ra ngay sau `</ul>` |
| 7 | 76 | `<a href="blog.html">1` không có `</a>` → liên kết sau bị lồng sai | Đóng `</a>` ngay sau `1` |
| 8 | 32 & 83 | `id="list"` bị trùng (id phải duy nhất) | Bỏ `id` ở `<ul>` của sidebar |
| 9 | 123 | Mở `<ul>` nhưng đóng bằng `</ol>` | `</ul>` |

## Các bẫy hợp lệ không được sửa

| Dòng | Đoạn mã hợp lệ/cần bảo toàn | Kết luận |
|---|---|---|
| 3 | `<html>` không có `lang` | Có thể cảnh báo accessibility, nhưng không phải lỗi cú pháp; giữ nguyên |
| 37 | `<i>free</i>` | `<i>` vẫn là phần tử HTML hợp lệ; giữ nguyên |
| 76 | `href="blog.html?page=2&sort=new"` | URL có query hợp lệ; `&sort=` không phải ambiguous ampersand; không đổi đích |
| 24 | `onBlur="javascript:..." onFocus="javascript:..."` | JavaScript hợp lệ dù tiền tố là label không cần thiết; giữ nguyên hành vi |
| 102, 133–151 | Các liên kết icon không có chữ/ARIA | HTML hợp lệ; chỉ nêu khuyến nghị accessibility, không sửa |
| 110, 117 | `<h5>` sau `<h2>` | Không phải thẻ sai/không tồn tại; chỉ nêu khuyến nghị về outline nếu cần, không sửa |
| 124 | `href=""` | Empty relative URL hợp lệ, trỏ về tài liệu hiện tại; giữ nguyên |

Các điểm có trong cả bản gốc `blog.html` chỉ được nêu như **khuyến nghị**, không đưa vào mã
đã sửa: thêm `lang`, accessible name cho icon-link, cải thiện thứ bậc heading, thay JavaScript
inline bằng `placeholder`, hoặc sửa chữ "© Copyright ©" bị lặp.
