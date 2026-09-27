# Prompt refactor `index.html` sang semantic HTML5 (công thức CRAFT)

## Prompt

```text
[C – CONTEXT / BỐI CẢNH]
Tôi đang làm bài tập môn Công nghệ Web. File index.html là trang chủ của website template tĩnh
Blakletterpress. Trang này chỉ dùng HTML và một file CSS ngoài (css/style.css), không dùng
framework hay JavaScript ngoài. Bố cục hiện tại dựng hoàn toàn bằng <div> (div#header,
div#main, div#sidebar, div#navigation, div#footer...), nên trình duyệt, công cụ tìm kiếm và
trình đọc màn hình không biết đâu là phần đầu trang, nội dung chính, menu, thanh bên hay chân trang.
Tôi cần refactor (tái cấu trúc mã mà không đổi kết quả hiển thị) sang các thẻ semantic HTML5
để cải thiện SEO cơ bản, rồi lưu kết quả thành index_new.html.

Ràng buộc bắt buộc:
- Giữ nguyên bố cục và giao diện: hiển thị index_new.html phải giống index.html đến từng pixel
  trên trình duyệt desktop hiện đại (Chrome/Edge/Firefox).
- Giữ nguyên toàn bộ nội dung: văn bản, thứ tự phần tử, href, src, alt, width/height, <title>,
  cấp heading (h1/h2/h5), event handler của ô tìm kiếm.
- Giữ nguyên mọi id và class. KHÔNG sửa css/style.css, không thêm CSS inline hay thẻ <style>,
  không thêm thư viện, không thêm JavaScript.

[R – ROLE / VAI TRÒ]
Hãy đóng vai một Front-end Developer kỳ cựu chuyên về semantic HTML, SEO on-page (tối ưu SEO
ngay trong mã trang) và khả năng truy cập (WCAG 2.1), có kinh nghiệm hướng dẫn sinh viên.

[A – ACTION / NHIỆM VỤ]
1. Đọc kỹ TỪNG DÒNG của index.html VÀ css/style.css. Lập danh sách mọi selector CSS phụ thuộc
   vào TÊN THẺ, không chỉ vào id/class. Ví dụ: "#main div.body", "#sidebar div.section",
   "#navigation > div", "#footer > div", "#gallery > div", "#connect > a", "#contents h1",
   "#posts h5". Đổi tên thẻ mà các selector này đang bám vào sẽ làm vỡ giao diện.
2. Xác định vai trò ngữ nghĩa của từng vùng và thay <div> bằng thẻ HTML5 phù hợp:
   <header>, <nav>, <main>, <aside>, <section>, <article>, <footer>.
   Quy tắc khi thay:
   a. Chỉ đổi tên thẻ của một phần tử khi mọi selector trỏ tới nó chỉ dùng id/class. Giữ nguyên
      id/class trên thẻ mới (vd <header id="header">).
   b. Nếu selector có kèm tên thẻ (vd "#main div.body", "#sidebar div.section") thì GIỮ <div>.
      Khi cần thêm ngữ nghĩa, bọc thêm một thẻ semantic BÊN TRONG sao cho không selector nào
      đổi phần tử mà nó khớp. Không thêm lớp bọc nào làm hỏng quan hệ ">" (con trực tiếp).
   c. <main> chỉ xuất hiện một lần. Mỗi <section> phải có heading riêng; vùng không có heading
      thì giữ <div> (không tạo <section> rỗng tiêu đề).
   d. Không dùng thẻ mà trình duyệt cũ có thể hiển thị khác, như <search> hay <small> (vì
      <small> làm chữ nhỏ đi so với cỡ chữ của #footnote). Ô tìm kiếm dùng <form role="search">.
   e. Kiểm tra style mặc định của trình duyệt (UA stylesheet) cho từng thẻ mới (display, margin,
      font-size của h1 khi nằm trong section/article...). Chỉ dùng thẻ mới khi CSS hiện có đã
      ghi đè hết các khác biệt đó.
3. Bổ sung SEO cơ bản trong <head> và <html>, không làm thay đổi phần hiển thị:
   - <html lang="en"> (nội dung trang là tiếng Anh).
   - <meta name="description" content="..."> dài khoảng 120–160 ký tự, tóm tắt đúng nội dung trang.
   - Giữ nguyên <meta charset="UTF-8"> và <title>.
   Những điểm SEO/accessibility khác cần sửa nội dung, như alt="Img" chưa mô tả, h2 nhảy xuống h5,
   liên kết icon không có chữ hay thiếu rel="noopener", thì chỉ ghi là "Khuyến nghị", không đưa
   vào mã.
4. Tự kiểm tra lại:
   - Với mỗi thay đổi, chỉ ra các selector CSS liên quan và giải thích vì sao giao diện không đổi.
   - Đối chiếu văn bản hiển thị của index.html và index_new.html: phải giống hệt nhau.
   - Dự kiến kết quả W3C Markup Validator (validator.w3.org): không được phát sinh lỗi mới so với
     index.html. Nêu rõ các lỗi, cảnh báo sẵn có từ bản gốc (nếu có) mà bạn giữ nguyên vì ràng buộc.
Không tự bịa lợi ích SEO. Nếu thẻ semantic chủ yếu giúp accessibility hoặc cấu trúc tài liệu hơn là
xếp hạng tìm kiếm thì nói rõ điều đó.

[F – FORMAT / ĐỊNH DẠNG ĐẦU RA]
Trả lời bằng tiếng Việt, theo đúng 4 phần:
Phần 1 – Bảng ánh xạ (Markdown):
  | STT | Dòng (index.html) | Thẻ cũ | Thẻ mới | Vai trò ngữ nghĩa | Selector CSS liên quan | Vì sao giao diện không đổi |
  Kèm theo danh sách các <div> được GIỮ NGUYÊN và lý do cho từng cái.
Phần 2 – Giải thích ngắn (2–3 câu/mục) lợi ích của từng thẻ semantic đối với SEO,
  accessibility và khả năng bảo trì mã.
Phần 3 – Mã nguồn đầy đủ của index_new.html trong một khối ```html```, có comment
  <!-- SEMANTIC: ... --> tại mỗi vị trí đã thay đổi.
Phần 4 – Checklist tự kiểm tra: bố cục không đổi, nội dung không đổi, id/class không đổi,
  CSS không bị sửa, kết quả dự kiến của W3C Validator, và danh sách "Khuyến nghị" chưa áp dụng.

[T – TARGET AUDIENCE / ĐỐI TƯỢNG & GIỌNG VĂN]
Người đọc là sinh viên năm 2–3 ngành CNTT, đã biết HTML/CSS cơ bản nhưng chưa quen với semantic
HTML5 và SEO. Giọng văn rõ ràng, sư phạm, ngắn gọn. Khi thuật ngữ tiếng Anh xuất hiện lần đầu,
giữ nguyên và giải thích bằng tiếng Việt.

Mã nguồn index.html:
"""
<dán toàn bộ nội dung file index.html vào đây>
"""

Mã nguồn css/style.css:
"""
<dán toàn bộ nội dung file css/style.css vào đây>
"""
```

## Đáp án tham khảo (để đối chiếu kết quả AI trả về)

| # | Dòng | Thẻ cũ | Thẻ mới | Lý do an toàn với CSS |
|---|------|--------|---------|------------------------|
| 1 | 3 | `<html>` | `<html lang="en">` | Thuộc tính, không ảnh hưởng hiển thị |
| 2 | 5–6 | – | `<meta name="description" …>` | Nằm trong `<head>`, không hiển thị |
| 3 | 11, 27 | `<div id="header">` | `<header id="header">` | Mọi selector chỉ dùng `#header` |
| 4 | 22 | `<form>` | `<form role="search">` | Thuộc tính ARIA, không đổi hiển thị |
| 5 | 29, 64 | `<div id="main">` | `<main id="main">` | `#main`, `#main div.body` vẫn khớp |
| 6 | 56–62 | (nội dung trong `div.body`) | bọc bằng `<article>` | Giữ `div.body` vì có `#main div.body`; `#contents h1/p` là selector hậu duệ nên vẫn khớp |
| 7 | 65, 112 | `<div id="sidebar">` | `<aside id="sidebar">` | `#sidebar div.section` là selector hậu duệ, `div.section` vẫn được giữ |
| 8 | 66, 83 | `<div id="navigation">` | `<nav id="navigation" aria-label="Main">` | Giữ `<div>` bên trong vì có `#navigation > div` |
| 9 | 85, 88 | `<div id="connect">` | `<section id="connect">` | Có sẵn `<h2>`; `#connect > a` vẫn là con trực tiếp |
| 10 | 91, 110 | `<div id="posts">` | `<section id="posts">` | Có sẵn `<h2>`; `#posts …` là selector hậu duệ |
| 11 | 94–107 | nội dung mỗi `<li>` trong `#posts` | bọc bằng `<article>` | `#posts h5/p/a.more` là selector hậu duệ, vẫn khớp |
| 12 | 114, 146 | `<div id="footer">` | `<footer id="footer">` | Giữ `<div>` bên trong vì có `#footer > div` |

## Các `<div>` phải giữ nguyên

| Phần tử | Lý do |
|---|---|
| `div#page`, `div#contents` | Chỉ là khung bố cục, không mang nghĩa |
| `div#motto`, `div#logo`, `div#searchbar` | Không có vai trò landmark (vùng mốc điều hướng) riêng; không dùng `<search>` vì trình duyệt cũ coi là thẻ inline |
| `div#gallery` | Không có heading nên không dùng `<section>` được; thẻ semantic không mang lại lợi ích SEO đáng kể ở đây |
| `div.body` | Selector `#main div.body` phụ thuộc tên thẻ |
| `div.section` (×2) | Selector `#sidebar div.section` phụ thuộc tên thẻ |
| `<div>` trong `#navigation` và `#footer` | Selector `#navigation > div`, `#footer > div` |

## Khuyến nghị (không áp dụng vì phải giữ nguyên nội dung)

- `alt="Img"` và `alt="Text"` chưa mô tả được ảnh. Nên đổi thành mô tả thật để có SEO hình ảnh.
- `<h2>` nhảy xuống `<h5>` trong `#posts`. W3C Validator báo lỗi này ở cả bản gốc.
- Liên kết icon (mạng xã hội, footer) không có chữ: nên thêm `aria-label`. Link có `target="_blank"` nên thêm `rel="noopener"`.
- `<title>` nên mô tả cụ thể hơn, ví dụ "Home – Blakletterpress".

## Kết quả kiểm tra thực tế

- W3C Validator:
  - `index.html`: 1 error (h2 → h5) và 1 info (thiếu `lang`).
  - `index_new.html`: vẫn 1 error h2 → h5 có sẵn từ bản gốc, không phát sinh lỗi mới. Có thêm 1 info báo trang "có vẻ là tiếng Catalan"; đây là báo nhầm do đoạn chữ mẫu Lorem ipsum, nên giữ `lang="en"`.
- Chụp màn hình Chrome headless ở kích thước 1280×1800 rồi so sánh từng pixel: hai trang **giống hệt nhau** (không có vùng khác biệt nào).
