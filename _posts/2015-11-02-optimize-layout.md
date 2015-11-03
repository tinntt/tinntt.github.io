---
layout: post
title: View Hierarchy, Optimize Layout và Custom View (Phần 1)!
---

<p align="justify">Bắt đầu với chủ đề custom layout để đẩy nhanh tốc độ vẽ màn hình của ứng dụng. Mình dự định chia chủ đề này ra làm 2-3 bài viết, với bài đầu tiên là bàn lại về kiến thức View của android cũng như view hierarchy, còn 1-2 bài sau để viết về phần optimize layout và custom view. Qua đó giúp cho các bạn tiện theo dõi về chủ đề này hơn. Vì vậy, toàn bộ bài này mình sẽ viết về kiến thức View cũng như View Hierarchy, làm sao android có thẻ vẽ lên giao diện người dùng được, vẽ như thế nào,... Nên nếu có kiến thức tốt về view và view hierarchy thì bạn có thể BỎ QUA BÀI NÀY.</p>

<h2>View là gì?</h2>
<p align="justify">Tạm định nghĩa là 1 class dùng để thế hiện các thành phần giao diện lên màn hình của thiết bị, mỗi view sẽ chiếm 1 ô hình chữ nhật trên màn hình, view chịu trách nhiệm đo kích thước, tìm vị trí, vẽ chính nó lên màn hình thiết bị nếu có lệnh gọi từ người dùng và nhận các sự kiện từ người dùng. View dùng để tạo các thành phần tương tác được với người dùng (Button, TextView, EditText,..) - Widgets. Ngoài ra ViewGroup là 1 lớp con của view dùng để đóng vai trò là các container chứa các view khác, thường thì viewgroup sẽ không hiển thị lên màn hình (RelativeLayout, LinearLayout,...) - Layouts.</p>

<h4>IDs</h4>
<p align="justify">Để có thể thao tác, chỉnh sữa, cài đặt cho 1 view nào đó thì developer sẽ truy cập tới view đó thông qua ID, vì vậy mỗi ID trong 1 layout sẽ phải là duy nhất, không được trùng với ID của các view khác. NẾU CÁC VIEW ĐÓ CÙNG NẰM TRONG 1 LAYOUT.</p>
<p align="justify">Định nghĩa ID:</p>
				<Button
				     android:id="@+id/my_button"
				     android:layout_width="wrap_content"
				     android:layout_height="wrap_content"
				     android:text="@string/my_button_text"/>
<p align="justify">Truy cập tới view thông qua ID:</p>
				Button myButton = (Button) findViewById(R.id.my_button);
<h4>Vị trí:</h4>
<p align="justify">Vì hình dạng của 1 view là hình chữ nhật, nên sẽ có 2 cặp giá trị biểu diễn vị trí đặt trên màn hình của 1 view. 1 cặp biểu diễn vị trí đặt gồm 2 giá trị left (bên trái) và top (bên trên) và cặp còn lại thể hiện kích thước của 1 view gồm width (chiều rộng) và height (chiều cao). Từ 2 cặp giá trị này chúng ta sẽ biết được ví trí mà view chiếm trên 1 màn hình.</p>

<p align="justify">CẦN CHÚ Ý: cặp tọa độ left và top sẽ được tính theo vị trí của view cha của chính view đó, chứ không phải tính từ góc trái trên của màn hình thiết bị. Chúng ta có thể lấy các giá trị này ra thông qua các hàm getLeft(), getTop(), getWidth() và getHeight(). Ví dụ nếu getLeft() trả về là 50 thì view này sẽ được đặc cách mép trái của VIEW CHA 1 đoạn 50 pixels.</p>

<h4>Kích thước:</h4>
<p align="justify">Về kích thước của 1 view, sẽ có 2 cặp giá trị để biểu diễn chiều rộng và chiều cao của View. 1 cặp là Measuared Width và Measured Height, cặp còn lại mà Witdh và Height.</p>
<p align="justify">+ Measured Width và Measured Height: cặp giá trị này thể hiện chiều rộng và chiều cao mà view muốn được chiếm trên view cha của mình, cặp giá trị này dùng để đo lường kích thước thật của View sau khi được vẽ lên. Có thể lấy cặp giá trị này qua hàm getMeasuredWidth() và getMeasuredHeight().</p>
<p align="justify">+ Width và Height: cặp giá trị còn lại thể hiện độ dài và độ rộng thật sự của View trên màn hình sau khi được vẽ lên. Cặp giá trị này có thể khác giá trị với cặp measured width và measured height. Có thể lấy cặp giá trị này qua hàm getWidth() và getHeight().</p>
<h2>View Hierarchy - cây giao diện?</h2>
<p align="justify">Android sẽ tổ chức giao diện màn hình dưới dạng cây. Thường thì các layout sẽ là các nốt cha và các widget sẽ là các nốt con. Vả thông thường các lá sẽ là phần được thể hiện lên giao diện người dùng. Với cách tổ chức như vậy thì việc giao diện có cây quá sâu thì lúc duyệt sẽ rất tốn thời gian.</p>

![alt tag](https://raw.githubusercontent.com/tinntt/tinntt.github.io/master/images/view-tree.png)

<h2>Làm sao để view có thể được vẽ lên màn hình?</h2>
<p align="justify">Để vẽ được 1 view lên màn hình thì android sẽ thực hiện 2 bước layout và draw. Đầu tiên View phải biết được vị trí và kích thước thật sự của nó trên màn hình để được vẽ, đây gọi là bước layout. Sau đó view sẽ được vẽ lên màn hình của thiết bị - bước draw.</p>
<h4>Layout:</h4>
<p align="justify">Để thực hiện được việc layout này android cần làm 2 việc, có thể tạm gọi là: đo (measure) và đặt (layout). </p>
<p align="justify">+ Đo (Measure): Bước này sẽ tính được kích thước thật sự của 1 view trên màn hình thiết bị bằng cách gọi hàm measure(int,int). Và được duyệt theo cây giao diện từ cao xuống thấp. Sau khi xong bước measure, mỗi view của cây sẽ biết được kích thước thật sự của mình. </p>
<p align="justify">+ Đặt (Layout): Việc này sẽ diễn ra sau khi hàm layout(int, int, int, int) được gọi, cũng bằng cách duyệt cây giao diện từ cao xuống thấp và sử dụng các kích thước đã được đo trong bước measure ở trên để đặt các view vào các vị trí cụ thể trên màn hình.</p>
<p align="justify">Để yêu cầu lại bước Layout này chúng ta có thể gọi hàm requestLayout() để android tính toán lại kích thước và vị trí của các view trên màn hình</p>
<h4>Draw:</h4>
<p align="justify">Sau khi đã có kích thước và vị trí của từng view trong cây, android sẽ tiến hành duyệt cây để xem view nào cần vẽ lại và tiến hành vẽ. Việc vẽ phải được vẽ theo thứ tự từ cha xuống con. Nếu 1 view bạn có set background cho nó thì background sẽ được vẽ trước và view vẽ sau, với các view ngang hàng thì view nào được đặt trước thì vẽ trước.</p>
<p align="justify">Để gọi lại 1 view vẽ lại chính nó thì có thể gọi hàm invalidate().</p>

<p align="justify">Tạm kết thúc phần 1 về View và cách 1 view được vẽ lên màn hình. Bài tiếp theo mình sẽ đi đến optimize layout.</p>