# Đồ án cuối kì Khoa học dữ liệu và Ứng dụng

## Giáo viên: Lê Ngọc Thành, Hoàng Xuân Trường

### Sinh viên: 
- Huỳnh Minh Châu 1712298
- Đào Duy Tuấn 1712869

# 1. Câu hỏi được đặt ra là gì?
Cho dữ liệu lịch sử giá cổ phiểu của một công ty, dự đoán giá cố phiếu của công ty đó những ngày tiếp theo?

# 2. Nếu trả lời được câu hỏi thì có ý nghĩa gì?
Người tham gia vào thị trường chứng khoán có thể tham khảo và kết hợp với hiểu biết thị trường để đưa quyết định mua/bán sao cho tạo được lợi nhuận.

# 3. Cách thức thu nhập dữ liệu như thế nào? (từ đâu, parse HTML hay API, tham khảo từ đâu,...)
Thu thập dữ liệu bằng 2 cách:
- Parse HTML (với Selenium) https://finance.yahoo.com/ thu thập dữ liệu daily (trong tối đa 20 năm trở lại).
- API https://www.alphavantage.co/ thu thập dữ liệu intraday (trong 2 năm trở lại).

Về phần thu thập dữ liệu nhóm em tham khảo các slide trên lớp, [document của Selenium](https://selenium-python.readthedocs.io/), [document của Alphavantage](https://www.alphavantage.co/documentation/), [trang blog này](https://beenje.github.io/blog/posts/parsing-html-tables-in-python-with-pandas/) cách dùng Pandas parse HTML table.

Tham khảm cho các phần khác cho ghi trong mục `VI. Tham khảo` trong file notebook `QuyTrinhKHDL.ipynb`.

# 4. Tổng quan dữ liệu thu nhập được có bao nhiêu dòng, cột và cột cần dự đoán là gì.
Loại dữ liệu:
- daily (hằng ngày): dữ liệu có mỗi record (dòng) là thông tin giá cổ phiếu tổng quan cho một ngày.
- intraday (trong ngày): dữ liệu có nhiều record cho một ngày, mỗi record (dòng) là thông tin cổ phiểu ở nhiều thời điểm trong ngày cách nhau một số phút nhất định (có thể chỉ định).

Dữ liệu daily thu thập được một số công ty có số dòng, cột như sau:
| | APPLE | AMAZON | FACEBOOK | GOOGLE | IBM | MICROSOFT | NETFLIX | TESLA |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| row | 5535 | 5571 | 2167 | 4120 | 5624 | 5603 | 4685 | 2645 |
| col | 7 |	7 |	7 |	7 |	7 |	7 |	7 |	7 |

Dữ liệu intraday chỉ thu thập của công ty Amazon, có số dòng là 7453, số cột là 6.

Cột cần dự đoán:
- Dữ liệu daily: `adj_close`
- Dữ liệu intraday: `close`

# 5. Với mỗi cột dữ liệu thu nhập có ý nghĩa gì, kiểu dữ liệu và ví dụ.
| Tên cột | Ý nghĩa ở dữ liệu daily | Ý nghĩa ở dữ liệu intraday | Kiểu dữ liệu | Ví dụ |
| :--- | :--- | :--- | :--- | :--- |
|**date** hoặc **time**|Ngày của mỗi dòng dữ liệu, có định dạng `mmm dd, yyyy`. Ví dụ: Dec 24, 2020 | Ngày và giờ của mốc thời điểm đang xét, có định dạng `yyyy-mm-dd hh:mm:ss`. Ví dụ: 2020-12-30 20:00:00 | `datetime` | |
|**open**|Giá cổ phiếu ở phiên giao dịch đầu tiên trong ngày| Giá cổ phiếu ở phiên giao dịch đầu tiên tại thời điểm | `float` | 3193.90 |
|**high**|Giá cổ phiếu cao nhất trong ngày| Giá cổ phiếu cao nhất giữa 2 mốc thời gian | `float` | 3202.00 |
|**low**|Giá cổ phiếu thấp trong ngày| Giá cổ phiếu thấp nhất giữa 2 mốc thời gian | `float` | 3169.00 |
|**close**|Giá cổ phiếu ở phiên giao dịch cuối cùng trong ngày và điều chỉnh Giá nếu có tách cổ phiếu|  Giá cổ phiếu ở phiên giao dịch cuối cùng trước mốc thời gian tiếp theo và đã được điều chỉnh tách cổ phiếu, chia cổ tức | `float` | 3172.69 |
|**adj_close**|Tương tự như **close** và tính thêm sự điều chỉnh sau khi chia cổ tức| (không có) |  `float` | 3172.69 |
|**volume**|Số lượng giao dịch trong ngày| Số lượng giao dịch giữa hai mốc thời gian |  `int` | 54930100 |

Tất cả các cột giá có đơn vị là USD.

# 6. Tự đánh giá đồ án (kết quả, thiếu sót, cần làm gì phát triển thêm,..).

# 7. Phân công công việc.
| Tên sinh viên | Công việc |
| :--- | :--- |
| - Thu thập dữ liệu<br> - Tiền xử lý dữ liệu<br> - Phân tích dữ liệu<br> - Tìm hiểu và triển khai mô hình ARIMA<br> - Biên tập, trình bày notebook, readme | - Khám phá dữ liệu<br> - Phân tích dữ liệu<br>  - Tìm hiểu và triển khai mô hình ARIMA<br> - Feature engineer cho mô hình LSTM<br>- Tìm hiểu và triển khai mô hình LSTM |

# 8. Hướng dẫn chạy các file notebook (tất cả các quy trình, cả code thu nhập dữ liệu)
Để chạy thầy cần clone cả repo này về máy. Cấu trúc đầy đủ các thư mục như sau:
- data
	- daily
		- daily_AAPL.csv
		- daily_AMZN.csv
		- daily_FB.csv
		- daily_IBM.csv
		- daily_MSFT.csv
		- daily_NFLX.csv
		- daily_TSLA.csv
	- daily_NFLX_api.csv
	- intraday_60min
		- intraday_AMZN_60min.csv
- driver
	- geckodriver-v0.28.0-linux64.tar.gz
	- geckodriver-v0.28.0-win64.zip
- notebook
	- ThuThapDuLieu.ipynb
	- QuyTrinhKHDL.ipynb

Tổng cộng khoảng 12MB.

Có 2 file notebook:
- `ThuThapDuLieu.ipynb` chứa toàn bộ code thu thập dữ liệu cần thiết.
	- Để chạy chọn `Kernel` - `Restart & Run All`. 
	- Khi chạy đến phần parse HTML, notebook sẽ dừng lại prompt input, cần nhập tên của hệ điều hành để code chạy đúng file thực thi browser driver (nhóm em có tải sẵn 2 file thực thi cho linux và windows đã được nén nên cũng nhẹ).
	- Nếu thầy dùng Linux thì thu nhỏ cửa sổ driver lại giúp em vì bên Linux nó focus cửa sổ driver còn hàm `minimize_window` của Selenium khiến driver bị đơ.
- `QuyTrinhKHDL.ipynb` chứa toàn bộ code và báo cáo.
	- Để chạy chọn `Kernel` - `Restart & Run All`. 

Cần chạy 2 file notebook tuần tự theo thứ tự liệt kê như trên.
