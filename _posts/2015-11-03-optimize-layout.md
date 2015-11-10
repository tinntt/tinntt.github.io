---
layout: post
title: View Hierarchy, Optimize Layout và Custom View (Phần 2)!
---

<p align="justify">Tiếp tục với bài viết ở phần 1, sau khi đã hiểu được View là gì, cách android vẽ giao diện lên màn hình, cách tổ chức màn hình. Thì chúng ta sẽ đi đến phần kế tiếp, làm sao để tổ chức layout được tốt, ít tốt thời gian vẽ, 1 số mẹo để cái thiện tốc độ vẽ giao diện của ứng dụng.</p>

<h2>Optimize layout.</h2>
<p align="justify">Nhắc lại tí nội dung của bài trước thì layout trên màn hình sẽ được tổ chức theo dạng cây, và việc đo kích thước cũng như vẽ các view lên màn hình đều là các phép duyệt cây từ cao xuống thấp. Nên tốc độ vẽ 1 màn hình có thể được xem là tổng tốc độ các lần duyệt cây layout. Nên trong phần này mình sẽ nói về cách làm PHẴN 1 cây giao diện, tổ chức 1 cây giao diện theo cách RỘNG và CẠN, thay vì HẸP mà SÂU.</p>

<h4>Relative Layout hay Linear Layout??</h4>
<p align="justify">Chắc hẵn một android developer không thể không biết tới 2 loại ViewGroup - Layout này. Nói sơ qua thì LinearLayout tổ chức và sắp xếp các view con theo 1 CHIỀU CỐ ĐỊNH và có thể căn chỉnh theo tỉ lệ từng thành phần. Còn RelativeLayout thì tổ chức và sắp xếp các view con theo vị trí của view cha hoặc các view con trước đó.</p>
(Bổ sung hình)
<p align="justify">Vậy nếu một người mới lập trình android sẽ dễ dàng chọn LinearLayout làm layout chính cho các màn hình của ứng dụng, vì nó rất dễ căn chỉnh các view theo tỉ lệ, dễ dàng sắp xếp các thành phần theo từng thành phần riêng lẽ và dễ quản lí lẫn cài đặt. Còn Relative layout rất khó cho việc căn tỉ lệ, ví trị của từng view, phải xác định vị trí của từng view đối với các view còn lại, nên sẽ rất khó trong việc cài đặt. Thử xét ví dụ với màn hình sau:</p>

<p align="justify">Đang viết...</p>



<h2>Comments</h2>
<div
  class="fb-like"
  data-share="true"
  data-width="450"
  data-show-faces="true">
</div>
<div class="fb-comments" data-href="http://developers.facebook.com/docs/plugins/comment?post=20151103" data-numposts="5"></div>