---
layout: post
title: Bài toán sinh nhật, cách về bờ cho các đê thủ mùa WC.
---

<p align="justify">Sẵn tiện đang có mùa WC cũng như đọc được mấy bài toán hay về xác suất (trong lúc ôn lại algorithm and data structure). Nên ngồi viết xàm về 1 bài toán mà mình nghĩ có thể giúp anh em gỡ lại điện thoại, xe máy, tivi đã ra đi cùng đội tuyển yêu thích của mình.</p>

<h1>Bài toán sinh nhật (Birthday problem).</h1>

<p align="justify">Nếu muốn đọc tiếng anh thì anh em có thể search keywork bên trên, còn không thì đợi 20 năm nữa con mình viết ver tiếng anh (my engrisk is suck !@#!@#!@$). Còn ai biết bài toán này rồi thì stop tại đây cho đỡ phí thời gian cuối tuần.</p>

<p align="justify"><b>Đề bài</b>: Trong 1 lớp cần có ít nhất bao nhiêu học sinh để có 2 học sinh trùng ngày sinh với nhau. 
Bỏ qua chuyện làm giấy khai sinh giả hay bị lưu bang, tất cả học sinh đều sinh cùng năm. Và 1 năm có 365 ngày.
Ok, tới đây bạn hãy nghĩ trong đầu 1 con số mà bạn cho là thỏa đề bài trên.</p>

<p align="justify">Mình sẽ có 2 cách làm: </br>Cách 1 dựa vào các công thức xác suất, tính toán các kiểu. </br>Cách 2 thì đơn giản mà hiệu quả hơn, tính từ từ với số học sinh tăng dần từ 1. Và cuối cùng mình sẽ đưa ra cách anh em gỡ vốn bằng bài toán này. Nếu ai nào đang đau đầu vì tiền, tình, công việc thì xuống thẳng cách 2 cho khỏe.</p>

<h2>Cách 1:</h2>

<p align="justify">
	đặt n = 365, (số ngày trong năm).</br>
		k là số học sinh cần phải có.</br>
		b<sub>i</sub> là ngày sinh của học sinh i.</br>
		Với từng cặp học sinh (i,j) ta đặt 1 biến X<sub>ij</sub> với 1 &le; i < j &le; k: </br>
		X<sub>ij</sub> = I{xác suất để học sinh i và j trùng ngày sinh} = 1 (nếu trùng) = 0 (nếu không trùng).</br>
	Đầu tiên, xác suất để 1 học sinh rơi vào 1 ngày a nào đó là 1/n.</br>
	Pr{b<sub>i</sub> = a} = 1/n.</br>
	=> Pr{b<sub>i</sub> = a và b<sub>j</sub> = a}</br> = Pr{b<sub>i</sub> = a}Pr{b<sub>j</sub> = a}</br> = 1/n<sup>2</sup> (2 xác suất độc lập).</br>

	1 năm có n ngày, vậy xác suất để 2 học sinh trùng ngày sinh vào 1 ngày bất kì là:</br>
	&sum;<sub>a=1</sub><sup>n</sup> (1/n<sup>2</sup>) = n(1/n<sup>2</sup>) = 1/n.</br>

	Vậy sự kiện để 2 học sinh có cùng ngày sinh là E[X<sub>ij</sub>] = Pr{2 học sinh có cùng ngày sinh} = 1/n.</br>

	Đặt X là tổng số các cặp học sinh có cùng ngày sinh với nhau:</br>

	X = &sum;<sub>i=1</sub><sup>k</sup>&sum;<sub>j=i+1</sub><sup>k</sup>X<sub>ij</sub>.</br>

	vậy ta có E[X] = E[&sum;<sub>i=1</sub><sup>k</sup>&sum;<sub>j=i+1</sub><sup>k</sup>X<sub>ij</sub>]</br>
				   = &sum;<sub>i=1</sub><sup>k</sup>&sum;<sub>j=i+1</sub><sup>k</sup>E[X<sub>ij</sub>]</br>
				   = C(k,2)1/n ( C(k,2) = chọn 2 trong k học sinh).</br>
				   = k(k-1)/2n.

	Vậy để có ít nhất 1 cặp học sinh trùng ngày sinh thì k(k-1) &ge; 2n => k = 28. Có vẻ hơi nhỏ, nhưng thử với cách 2 và so sánh xem mình chứng mình đúng hay sai.
</p>

<h2>Cách 2 (from wiki):</h2>

<p align="justify">
	Kết quả ở cách 1 ta có là 28 học sinh. Với cách này mình sẽ chứng minh ngược lại, bằng cách tìm xác suất để số k học sinh có khác ngày sinh với nhau. Bắt đầu từ học sinh 1, số cách chọn ngày sinh sẽ là 365/365, vậy học sinh 2 chỉ còn 364/365 cách chọn ngày sinh. cứ thế học sinh thứ i sẽ có (365 - i + 1)/365 cách chọn.</br>
	Mình sẽ lấy số học sinh ở cách 1 và tìm xem xác suất để 28 học sinh này khác ngày sinh với nhau là bao nhiêu:</br>
	gọi P(A') là xác suất 28 học sinh khác ngày sinh.</br>
	P(A') = 365/365 * 364/365 * 363/365 * ..... * 338/365</br>
		  = (1/365)<sup>28</sup> * (365 * 364 * 363 * .... * 338)</br>
		  ~ 0.3655385.</br>
	Vậy P(A) (xác suất 28 học sinh có ít nhất 1 cặp trùng ngày sinh) = 1 - 0.3655385 = 0.6344 = 63,44%.</br>
	Vậy chỉ với 28 học sinh, thì xác suất để có 1 cặp trùng ngày sinh là trên > 50%.</br>
	Tính tương tự vậy đến 50 học sinh, ta sẽ có xác suất là 97%. 1 xác suất gần như chắc chăn sẽ có học sinh trùng ngày sinh trong 1 lớp có 50 người. 
</p>

<p align="justify">Bây giờ bạn đem con số đã chứng mình so sánh với số lúc đầu bạn nghĩ xem chênh lệch như thế nào. Sẽ không ít người nghĩ là cần ít nhất 366 học sinh để thỏa đề bài toán. Vậy cách kiếm tiền đây là gì?</br>
Nếu nhà có em nhỏ chưa đi học đại học (tức là chưa học qua môn xác chết thống kê). Thì anh em cứ mạnh dạn mà đưa ra kèo "tao chỉ cần 50 người cùng năm sinh để có thể có 1 cặp cùng ngày sinh, nếu không có cặp nào thì mày thắng, còn lại thì tao ăn nữa tiền thôi. Chọn ngẫu nhiên theo lớp học hay gì đấy cũng được.". Đương nhiên những đứa nghĩ cần 366 người thì sẽ nhận lời liền, vì 50 chỉ bằng 1/7 con số 366, dại gì mà không chơi. </br>
Chúc anh em mau giàu, còn nếu không giàu thì do bạn xui, vì 3% cũng rơi vào được thì tốt nhất đừng chơi gì hết, để tiền uống trà sửa cho bổ.
</p>

<h2>Comments</h2>
<div
  class="fb-like"
  data-share="true"
  data-width="450"
  data-show-faces="true">
</div>
<div class="fb-comments" data-href="http://developers.facebook.com/docs/plugins/comment?post=20151103" data-numposts="5"></div>