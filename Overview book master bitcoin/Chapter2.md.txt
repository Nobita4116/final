# Bitcoin làm việc như thế nào ?

## 1. Transactions, Blocks Mining và Blockchain.
* Hệ thống bitcoin hoạt động hoàn toàn dựa vào sự tin tưởng phân tán ( phi tập trung) : thay vì sử dụng một cơ quan đáng tin cậy trung ương hoặc một máy chủ trung tâm thì nó đươc thực hiện như một tài sản từ các tương tác của những người tham gia trong hệ thông Bitcoin.
* Hệ thống bitcoin bao gồm: 
	* Người dùng với ví chứa khóa riêng.
	* Các giao dịch được sinh ra trong mạng lưới.
	* Miner là những người tạo ra sự thỏa thuận trong blockchain.
	* Số cái (blockchain) là nơi chứa tất cả các giao dịch.
	![Bitcoin Overview](/image/bitcoinOverview.png)

## Giao dịch Bitcoin.
* Một giao dịch Bitcoin nói đơn giản là sẽ cho mạng Bitcoin biết rằng chủ sở hữu của một số giá trị Bitcoin đã cho phép chuyển giao giá trị đó cho một chủ sở hữu khác. Chủ sở hữu mới hiện có thể chi tiêu Bitcoin này bằng cách tạo một giao dịch khác cho phép chuyển giao nó cho một chủ sở hữu khác.
* Một giao dịch cũng chứa bằng chứng quyền sở hữu cho mỗi số bitcoin ( đầu vào ) có giá trị đang và đã được chi tiêu dưới dạng chữ ký số từ chủ sở hữu.
	* Ví dụ về giao dịch Bitcoin biểu diễn dưới dạng sổ toán kép: 
	![Transaction as double-entry bookkeeping](/image/double_entry.png)

	* Biểu diễn chúng dưới dang chuỗi giao dich: 
	![Transaction Chains](/image/transactionChains.png)
* Một vài loại giao dịch phổ biến
Gồm 3 loại chính:
	* Giao dịch thông dụng ( 1 input và 2 output): là thanh toán đơn giản từ địa chỉ này sang địa chỉ khác, thường bảo gồm số dư được trả lại cho chủ sở hữu ban đầu.
	![Common Transaction](/image/form1.png)
	* Giao dịch tổng hợp ( nhiều input và 1 output): là giao dịch tổng hợp một số đầu vào thành đầu ra đơn lẻ. Các giao dịch như thế thường được tạo ra bởi các ứng dụng ví để biến mất các số tiền nhỏ đã đươc nhận để thành một số tiền dùng cho các khoản thanh toán sau.
	![Aggregating Transaction](/image/form2.png)
	* Giao dịch phân phối ( 1 input và nhiều output): là một hình thức giao thức thường thấy trên các sổ kế toán bitcoin là một giao dịch phân phối 1 đầu vào cho nhiều đầu ra đại diện cho các người nhận. Nó thường được sử dụng khi các tổ chức thương mại muốn phân phối tiền.
	![Distributing Transation](/image/form3.png)

* Xây dựng một giao dịch.
	* Điều kiện cần: địa chỉ đích, số tiền, số tiền còn lại trong ví.
	* Ứng dụng ví có thể xây dựng giao dịch ngay cả khi nó ngoại tuyến.
	* Quy trình thực hiện sẽ trải qua các bước: 
		* Lấy ra các đầu vào phù hơp:
			* Các ví đều có một cơ sở dữ liệu nhỏ lưu trữ bản copy của output từ mọi giao dịch trong blockchain (unspent output).
			* Tính toán ra tất cả các output thuộc sở hữu của những địa chỉ trong ví mà có thể dùng được.
			* Nếu ứng dụng ví không duy trì một bản sao thì nó có thể truy vẫn mạng bitcoin để lấy được thông tin bằng cách sử dụng nhiều API đến full-node có sãn bởi các nhà cung cấp.
			* Việc tra cứu sẽ sử dụng 1 request API ( 1 lệnh HTTP GET tới 1 URL chỉ định), URL sẽ trả về tất cả output chưa được thanh toán cho một địa chỉ.
			![Unspent Ouput](/image/tranction1.png)

		* Tạo đầu ra: 
			Đầu ra của 1 giao dịch được tạo ra dưới dạng script với một sự ràng buộc về giá trị và chỉ có thể được sử dụng nếu đưa ra một lời giải đúng cho script đó. Những ai đưa ra được key từ khóa tương đương với địa chỉ public ( nói cách khác là người sở hữu ví có địa chỉ như thế ) thì mới sử dụng được .
			![View Transaction](/image/contructing2.png)

		* Thêm giao dịch vào số cái (Blockchain)
			* Sau khi giao dịch được ví cửa người gửi tạo ra chứa tất cả mọi thứ cần thiết để xác nhận quyền sở hữu số tiền và chỉ định chủ sở hữu mới thì giao dịch sẽ được truyền tới mạng bitcoin. Nó sẽ trở thành một phần của số cái (blockchain).
			* Vì mạng bitcoinn là một mạng ngang hàng nên với mỗi giao dịch đầy đủ thông tin thì sẽ không quan trọng về việc nó được truyền như thế nào và đến đâu. Giao dịch sẽ được truyền tới tất cả các người tham gia vào mạng Blockchain.
			* Cách thức truyền đi: **flooding** bất ký 1 node nào trên mạng nhận được 1 giao dịch hợp lệ mà nó chưa từng  thấy trước đó sẽ ngay lập tức truyền đến tất cả các node khác mà nó đã được kết nối.

		* Khai thác Bitcoin ( Bitcoin mining).
			* Một giao dịch được phổ biến ( phán tán ) lên mạng Bitcoin . Nó sẽ trở thành một phần của Blockchain sau khi nó đươc xác nhận và  bao gồm trong một block sau một quá trình Mining (khai thác).
			* Sự tin tưởng của hệ thống bitcoin dựa trên sự tính toán của các máy tính. Các giao dịch sẽ được đóng gói thành các khối (block ) và đòi hỏi một lượng tính toán lớn để xác minh.
			* Quá trình Mining có 2 mục đích: 
				* Mining node xác nhận tất cả các giao dịch bằng các tham chiếu tới những *quy tắc đồng thuận* của bitcoin. Do đó Mining cũng cấp độ bảo mật cho giao dịch bitcoin và đồng thời loại bỏ những giao dịch bị lỗi hoặc không hợp lệ.
				* Mining sẽ tạo ra bitcoin mới trong mỗi khối.
			* Mining sử dụng tài nguyên tính toán để giải quyết vấn toán học mà ở đấy là một Hash mật mã, nó không đối xứng nghĩa là nó khó có thể giải được nhưng dễ để xác nhận và độ khó có thể điều chính ( thuật toán Proof-of-Work).

		* Khai thác giao dịch trong khối.
			* Khi quá trình Mining xây dựng một khối mới ( chi phí giao dịch), họ sẽ thêm những giao dịch chưa được xác minh tới 1 block mới và sau đó sẽ cố gắng giải quyết xác nhận cho block đó. Với thuật toán Mining (PoW) , Mining tìm được kết quả chính xác đầu tiên sẽ nhận được phân thưởng và phí của các giao dịch trong block đó.

		* Chi tiêu cho giao dich (Spending the transaction).
			* Với mỗi 1 bitcoin client đều có thể xác thực giao dịch 1 các độc lập.
				Với Full-client ể theo dấu vết nguồn từ số tiền từ thời điểm bitcoin được tạo ra tăng dần theo giao dịch cho tới khi đat được địa chỉ cuối cùng.
				Với Light-node


