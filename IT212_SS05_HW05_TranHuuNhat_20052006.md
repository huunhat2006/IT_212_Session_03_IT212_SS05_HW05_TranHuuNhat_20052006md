1. Phân tích & Thiết kế nghiệp vụ
Yêu cầu thô từ khách hàng

"Tôi muốn hệ thống tự động gợi ý các sản phẩm liên quan khi người dùng đang xem một món đồ, dựa trên lịch sử mua hàng của họ."

Giả định nghiệp vụ

Hệ thống Shop AI có:

Người dùng đã đăng nhập.
Lưu lịch sử mua hàng.
Có danh mục sản phẩm.
Có dữ liệu các sản phẩm thường được mua cùng nhau.
Input
Tên	Kiểu dữ liệu	Mô tả
userId	Long	ID người dùng
productId	Long	Sản phẩm đang xem
limit	Integer	Số lượng gợi ý tối đa
Output
Tên	Kiểu dữ liệu	Mô tả
recommendedProducts	List<Product>	Danh sách sản phẩm đề xuất
Luồng xử lý
User xem Product A
        |
        v
Lấy lịch sử mua hàng của User
        |
        v
Tìm nhóm sản phẩm User quan tâm
        |
        v
So sánh với Product A hiện tại
        |
        v
Xếp hạng sản phẩm liên quan
        |
        v
Loại bỏ sản phẩm đã mua gần đây
        |
        v
Trả về Top N gợi ý
Sơ đồ ASCII
+----------------+
| User View Item |
+----------------+
         |
         v
+---------------------+
| Current Product ID  |
+---------------------+
         |
         v
+---------------------+
| Purchase History    |
+---------------------+
         |
         v
+---------------------+
| Recommendation Rule |
+---------------------+
         |
         v
+---------------------+
| Ranking Engine      |
+---------------------+
         |
         v
+---------------------+
| Top N Suggestions   |
+---------------------+

ROLE:

Bạn là Senior Business Analyst và System Analyst.

GOAL:

Chuyển yêu cầu nghiệp vụ thô thành tài liệu Use Case chuyên nghiệp.

CONTEXT:

Khách hàng yêu cầu:

"Tôi muốn hệ thống tự động gợi ý các sản phẩm liên quan khi người dùng đang xem một món đồ, dựa trên lịch sử mua hàng của họ."

TASK:



Xác định:

Actors

Preconditions

Triggers

Main Flow

Alternative Flow

Exception Flow

Postconditions

Không được giả định mơ hồ.

Nếu thiếu thông tin hãy đưa ra giả định nghiệp vụ hợp lý.

OUTPUT FORMAT:



Use Case Name

Goal

Actors

Preconditions

Trigger

Main Flow

Alternative Flow

Exception Flow

Postconditions 

Chào bạn, với tư cách là một Senior Business Analyst và System Analyst, tôi xin phép chuyển đổi yêu cầu nghiệp vụ thô của khách hàng thành một tài liệu đặc tả Use Case hoàn chỉnh và chuyên nghiệp.

Để tài liệu đạt tiêu chuẩn bàn giao cho đội ngũ Phát triển (Developers) và Kiểm thử (QA), tôi sẽ đưa ra một số giả định nghiệp vụ hợp lý dựa trên các hệ thống E-Commerce hiện đại:

Hệ thống gợi ý được đặt tên là Recommendation Engine (AI Service).

Gợi ý phân làm 2 trường hợp: Người dùng đã đăng nhập (Gợi ý cá nhân hóa cao dựa theo lịch sử) và Khách vãng lai chưa đăng nhập (Gợi ý dựa trên độ phổ biến của sản phẩm hoặc hành vi xem trong phiên).

TÀI LIỆU ĐẶC TẢ USE CASE: TỰ ĐỘNG GỢI Ý SẢN PHẨM LIÊN QUAN
1. Use Case Name
Mã định danh: UC-REC-01

Tên Use Case: Tự động hiển thị gợi ý sản phẩm liên quan (Automated Product Recommendation)

2. Goal
Mục tiêu: Hiển thị danh sách các sản phẩm liên quan và phù hợp với sở thích của người dùng ngay trên trang Chi tiết sản phẩm (Product Detail Page - PDP), nhằm kích thích nhu cầu mua sắm, tăng tỷ lệ chuyển đổi (CR) và giá trị trung bình trên mỗi đơn hàng (AOV).

3. Actors
Primary Actor: Người dùng (User) - bao gồm Khách hàng đã đăng nhập (Authenticated Customer) và Khách vãng lai (Guest).

Supporting Actor: Hệ thống Gợi ý (Recommendation Engine / AI Service).

4. Preconditions
Người dùng đang truy cập hệ thống Shop AI bằng Web hoặc Mobile App.

Danh mục sản phẩm (Product Catalog) trên hệ thống đang hoạt động ổn định.

Khối dữ liệu lịch sử mua hàng (Purchase History) đã được index và sẵn sàng truy vấn (đối với người dùng đã đăng nhập).

5. Trigger
Người dùng nhấn chọn xem một sản phẩm bất kỳ và hệ thống bắt đầu tải trang Chi tiết sản phẩm (Product Detail Page).

6. Main Flow (Luồng xử lý chính - Áp dụng cho Người dùng đã đăng nhập)
Người dùng truy cập vào trang Chi tiết sản phẩm (ID: P-001).

Hệ thống (Backend API) ghi nhận sự kiện xem sản phẩm và kiểm tra trạng thái đăng nhập của Người dùng.

Hệ thống xác định Người dùng đã đăng nhập và lấy mã định danh định danh (User_ID).

Hệ thống gửi yêu cầu (gồm User_ID và Product_ID) sang Recommendation Engine.

Recommendation Engine phân tích:

Danh mục, thương hiệu, phân khúc giá của sản phẩm hiện tại (Product_ID).

Lịch sử các đơn hàng đã hoàn thành của User_ID trong vòng 180 ngày gần nhất.

Recommendation Engine tính toán và trả về danh sách tối đa 10 sản phẩm có điểm số liên quan cao nhất.

Hệ thống tải trang Chi tiết sản phẩm đồng thời hiển thị khối "Sản phẩm gợi ý cho bạn" (Recommended for you) ở phía dưới thông tin sản phẩm chính.

7. Alternative Flow (Luồng rẽ nhánh)
AF-01: Người dùng là Khách vãng lai (Chưa đăng nhập)

Tại bước 3 của Main Flow: Hệ thống phát hiện người dùng chưa đăng nhập (User_ID = Null).

Bước 4: Hệ thống gửi yêu cầu chỉ chứa Product_ID sang Recommendation Engine.

Bước 5: Recommendation Engine chuyển đổi thuật toán: Tìm kiếm các sản phẩm thường được mua kèm với sản phẩm hiện tại (Frequently Bought Together) dựa trên dữ liệu tổng thể của toàn sàn, hoặc sản phẩm cùng danh mục có lượt mua cao nhất (Top Sellers).

Hệ thống tiếp tục quy trình từ bước 6 của Main Flow.

AF-02: Người dùng mới đăng nhập chưa có lịch sử mua hàng

Tại bước 5 của Main Flow: Recommendation Engine kiểm tra thấy lịch sử mua hàng của User_ID trống (Tài khoản mới).

Bước 6: Hệ thống áp dụng thuật toán gợi ý theo hành vi xem gần đây (Clickstream trong phiên) kết hợp với các sản phẩm đang có xu hướng (Trending Products) thuộc cùng danh mục của sản phẩm hiện tại.

Hệ thống tiếp tục quy trình từ bước 7 của Main Flow.

8. Exception Flow (Luồng xử lý ngoại lệ)
EF-01: Hệ thống Gợi ý (Recommendation Engine) bị mất kết nối hoặc phản hồi chậm (> 500ms)

Tại bước 4 hoặc 5 của Main Flow: Kết nối tới Recommendation Engine bị timeout hoặc trả về mã lỗi 5xx.

Hệ thống xử lý bảo vệ (Fallback Mechanism): Để tránh làm treo hoặc chậm tiến trình tải trang chính của khách hàng, hệ thống Backend sẽ tự động lấy danh sách 10 sản phẩm ngẫu nhiên cùng danh mục (Category) từ cơ sở dữ liệu core làm dữ liệu thay thế.

Hệ thống ghi nhận log lỗi hệ thống (System Error Log) để gửi cảnh báo cho DevOps Team.

EF-02: Sản phẩm gợi ý bị hết hàng (Out of Stock) đột ngột

Tại bước 6 của Main Flow: Danh sách sản phẩm trả về từ AI có chứa sản phẩm đã hết hàng trong kho vật lý.

Hệ thống xử lý: Tầng Backend API thực hiện bộ lọc (Filter), tự động loại bỏ các sản phẩm có trạng thái Stock = 0 hoặc Status = Inactive trước khi trả dữ liệu về giao diện Client.

9. Postconditions
Khối gợi ý sản phẩm được hiển thị đầy đủ thông tin (Hình ảnh, Tên, Giá, Đánh giá sao) trong vòng dưới 300ms kể từ khi trang chính tải xong.

Mọi hành vi Click/Xem của người dùng trên khối gợi ý này phải được ghi nhận lại (Tracking Event) vào hệ thống dữ liệu để tiếp tục tối ưu hóa thuật toán AI cho các phiên làm việc sau.

ROLE:

Bạn là Senior System Analyst.

CONTEXT:

Dựa trên Use Case đã sinh ở bước trước.

TASK:

Sinh Functional Requirements cho module AI Product Recommendation.

Yêu cầu:



Đánh số FR-001 trở đi.

Mỗi FR phải có:

Requirement ID

Description

Trigger

Input

Processing

Output

Acceptance Criteria

Bắt buộc bao phủ:



Người dùng đã đăng nhập.

Người dùng chưa có lịch sử mua hàng.

Không tìm thấy sản phẩm liên quan.

Giới hạn số lượng gợi ý.

Hiệu suất phản hồi.

Trường hợp dữ liệu recommendation bị lỗi. 

Chào bạn, dựa trên tài liệu Đặc tả Use Case UC-REC-01 đã xây dựng, dưới đây là danh sách các Yêu cầu chức năng (Functional Requirements - FR) được chi tiết hóa cho module AI Product Recommendation.

Tài liệu này được thiết kế theo cấu trúc chuẩn hóa, sẵn sàng chuyển giao cho đội ngũ Phát triển Hệ thống (Backend/AI Engineer) và Kiểm thử (QA Team).

ĐẶC TẢ YÊU CẦU CHỨC NĂNG (FUNCTIONAL REQUIREMENTS)
MODULE: AI PRODUCT RECOMMENDATION
FR-001: Gợi ý cá nhân hóa cho Người dùng đã đăng nhập
Requirement ID: FR-001

Description: Hệ thống tự động phân tích lịch sử mua hàng để hiển thị danh sách sản phẩm gợi ý cá nhân hóa khi người dùng đã đăng nhập truy cập trang Chi tiết sản phẩm (PDP).

Trigger: Người dùng đã đăng nhập nhấn xem một sản phẩm bất kỳ.

Input: User_ID, Product_ID (Sản phẩm đang xem).

Processing: 1. Bộ lọc API xác thực User_ID hợp lệ từ Security Context.
2. Gửi request đồng thời chứa User_ID và Product_ID sang Recommendation Engine.
3. AI Service truy vấn lịch sử mua hàng của User_ID trong 180 ngày gần nhất và tính toán điểm tương quan (Correlation Score) với Product_ID.
4. Sắp xếp danh sách giảm dần theo điểm số tương quan.

Output: Mảng JSON danh sách các đối tượng sản phẩm liên quan.

Acceptance Criteria: * Danh sách hiển thị phải mang tính cá nhân hóa (khác nhau giữa các tài khoản khác nhau khi cùng xem một sản phẩm).

Các sản phẩm gợi ý phải thuộc trạng thái đang kinh doanh (Active) và còn hàng (Stock > 0).

FR-002: Gợi ý cho Người dùng mới / Chưa có lịch sử mua hàng
Requirement ID: FR-002

Description: Hệ thống cung cấp cơ chế gợi ý thay thế dựa trên hành vi clickstream trong phiên hoặc sản phẩm xu hướng khi tài khoản người dùng chưa phát sinh lịch sử mua sắm (Xử lý bài toán Cold Start).

Trigger: Người dùng đã đăng nhập nhưng lịch sử mua hàng trống, hoặc Khách vãng lai truy cập xem sản phẩm.

Input: Product_ID, User_ID (có thể null hoặc có thông tin nhưng lịch sử đơn hàng bằng 0).

Processing: 1. Recommendation Engine phát hiện lịch sử mua sắm của User_ID trống hoặc không có User_ID.
2. Hệ thống chuyển đổi thuật toán sang: "Sản phẩm thường được xem/mua kèm" (Collaborative Filtering) hoặc "Sản phẩm bán chạy nhất/Thịnh hành nhất" (Top Trending) trong cùng danh mục (Category) của Product_ID hiện tại.

Output: Mảng JSON danh sách sản phẩm xu hướng/liên quan tổng thể.

Acceptance Criteria: Giao diện khối gợi ý vẫn hiển thị đầy đủ và mượt mà, không để lại khoảng trắng hoặc thông báo trống trải trên màn hình người dùng.

FR-003: Giới hạn số lượng sản phẩm gợi ý hiển thị
Requirement ID: FR-003

Description: Hệ thống áp dụng quy tắc cấu hình cứng (Hard Limit) về số lượng bản ghi trả về giao diện nhằm tối ưu hóa bố cục UI/UX và băng thông đường truyền.

Trigger: Kích hoạt tự động khi Recommendation Engine tổng hợp kết quả trả về.

Input: Danh sách thô các sản phẩm gợi ý do AI Service tính toán (có thể lên tới hàng trăm sản phẩm).

Processing: 1. Tầng Backend Service nhận danh sách sản phẩm từ AI.
2. Áp dụng hàm cắt mảng (Slice/Limit) để chỉ lấy tối đa 10 sản phẩm có điểm số cao nhất.

Output: Mảng JSON chứa từ 0 đến tối đa 10 sản phẩm.

Acceptance Criteria: Số lượng phần tử hiển thị trong khối gợi ý trên giao diện Web/Mobile tuyệt đối không được vượt quá 10 sản phẩm dưới mọi tình huống.

FR-004: Xử lý tình huống không tìm thấy sản phẩm liên quan phù hợp
Requirement ID: FR-004

Description: Định nghĩa kịch bản dự phòng khi thuật toán AI không tìm thấy bất kỳ sản phẩm nào đạt ngưỡng điểm tương quan tối thiểu với sản phẩm đang xem.

Trigger: Recommendation Engine trả về danh sách rỗng (Empty List hoặc điểm số < ngưỡng quy định).

Input: Product_ID.

Processing: 1. Tầng Backend nhận kết quả rỗng từ AI Engine.
2. Hệ thống tự động kích hoạt truy vấn trực tiếp vào Database Core: Lấy ra tối đa 10 sản phẩm ngẫu nhiên có cùng Category_ID hoặc cùng Brand_ID với sản phẩm hiện tại để lấp đầy khối gợi ý.

Output: Mảng JSON chứa danh sách sản phẩm cùng danh mục thay thế.

Acceptance Criteria: Khối gợi ý vẫn phải có dữ liệu hiển thị cho người dùng; không hiển thị màn hình trống hoặc thông báo lỗi nghiệp vụ ra ngoài Front-end.

FR-005: Kiểm soát hiệu suất phản hồi dữ liệu (Performance SLA)
Requirement ID: FR-005

Description: Đảm bảo thời gian xử lý và phản hồi dữ liệu gợi ý nằm trong ngưỡng cho phép để không ảnh hưởng tới tốc độ tải (Loading time) của trang chính.

Trigger: Khởi chạy đồng thời khi API của trang Chi tiết sản phẩm được gọi.

Input: Lời gọi hàm API yêu cầu lấy dữ liệu gợi ý.

Processing: 1. Thiết lập cấu hình thời gian chờ tối đa (HTTP Timeout) cho kết nối giữa Backend API và Recommendation Engine là 500ms.
2. Sử dụng cơ chế gọi bất đồng bộ (Asynchronous Call / Non-blocking) hoặc kỹ thuật xử lý luồng song song để việc tải khối gợi ý không chặn tiến trình render thông tin cơ bản của sản phẩm chính.

Output: Dữ liệu trả về hoặc kích hoạt ngắt kết nối (Timeout) nếu vượt ngưỡng.

Acceptance Criteria: * Thời gian phản hồi (Response Time) của API gợi ý phải ≤300ms trong điều kiện tải bình thường và tối đa không quá 500ms.

Thông tin sản phẩm chính bắt buộc phải hiển thị trước, khối gợi ý có thể hiển thị sau dưới dạng Lazy Loading (Skeleton effect).

FR-006: Cơ chế Fallback an toàn khi dữ liệu Recommendation bị lỗi hệ thống
Requirement ID: FR-006

Description: Bảo vệ hệ thống tổng thể (Fault Tolerance) khi phân hệ AI Product Recommendation gặp sự cố phần cứng, sập dịch vụ (Downtime), hoặc trả về dữ liệu lỗi cấu trúc (Malformed JSON).

Trigger: Hệ thống ghi nhận HTTP Status Code 5xx, kết nối bị Timeout (>500ms), hoặc xảy ra ngoại lệ parse dữ liệu từ AI Service.

Input: Ngoại lệ hệ thống (Exception), mã lỗi HTTP.

Processing: 1. Bộ ngắt mạch (Circuit Breaker) kích hoạt trạng thái mở (Open).
2. Hệ thống cô lập phân hệ AI bị lỗi để tránh gây hiệu ứng sụp đổ dây chuyền (Cascading Failure).
3. Tự động chuyển luồng xử lý về hàm Fallback: Đọc dữ liệu từ bộ nhớ đệm Cache (Redis) của danh mục sản phẩm bán chạy nhất trong tuần (Top Weekly Sellers).
4. Ghi nhận thông tin lỗi chi tiết (StackTrace) vào hệ thống Log tập trung.

Output: Trả về danh sách sản phẩm bán chạy nhất làm dữ liệu thay thế tạm thời.

Acceptance Criteria: * Ứng dụng không bị sập (Crash) hoặc báo lỗi "Internal Server Error" (500) lên màn hình khách hàng.

Ghi log bảo mật/vận hành chính xác với mức độ CRITICAL để cảnh báo hệ thống giám sát.

ROLE:

Bạn là Data Architect.

CONTEXT:

Dựa trên Functional Requirements của module AI Product Recommendation.

TASK:

Xây dựng Data Dictionary sơ bộ.

Yêu cầu:

Liệt kê:



User

Product

PurchaseHistory

RecommendationResult

Với mỗi thực thể:



Field Name

Data Type

Description

Constraint

Example Value

OUTPUT:

Bảng Markdown chuẩn SRS. 

Chào bạn, với tư cách là một Data Architect, tôi xin phép chuyển đổi các thực thể nghiệp vụ từ tài liệu Functional Requirements của module AI Product Recommendation thành cấu trúc dữ liệu vật lý sơ bộ (Data Dictionary).

Bảng từ điển dữ liệu này tuân thủ các nguyên tắc thiết kế hệ thống có hiệu năng cao, tối ưu hóa các câu lệnh truy vấn cho cả hệ thống Core DB (RDBMS) lẫn hệ thống Recommendation Engine (NoSQL/Vector DB).

DATA DICTIONARY: MODULE AI PRODUCT RECOMMENDATION
1. Thực thể: User (Thông tin người dùng)
Bảng này lưu trữ thông tin định danh cơ bản của người dùng để phục vụ ánh xạ hành vi và cá nhân hóa.

Field Name	Data Type	Description	Constraint	Example Value
user_id	BIGINT	Khóa chính, định danh duy nhất của người dùng.	PRIMARY KEY, AUTO_INCREMENT	1054329
email	VARCHAR(100)	Địa chỉ email của người dùng (dùng làm username).	UNIQUE, NOT NULL	nguyenvan@gmail.com
status	VARCHAR(20)	Trạng thái hoạt động của tài khoản trong hệ thống.	NOT NULL (ACTIVE, INACTIVE, BANNED)	ACTIVE
created_at	TIMESTAMP	Thời điểm tài khoản được khởi tạo thành công.	NOT NULL, DEFAULT CURRENT_TIMESTAMP	2026-01-15 08:30:00
2. Thực thể: Product (Thông tin sản phẩm)
Lưu trữ thông tin cấu hình và trạng thái thương mại của sản phẩm phục vụ bộ lọc hiển thị.

Field Name	Data Type	Description	Constraint	Example Value
product_id	BIGINT	Khóa chính, định danh duy nhất của sản phẩm.	PRIMARY KEY, AUTO_INCREMENT	88432
category_id	INT	Định danh danh mục cấp cao của sản phẩm.	FOREIGN KEY, NOT NULL	12 (Điện tử)
brand_id	INT	Định danh thương hiệu của sản phẩm.	FOREIGN KEY, NULLABLE	55 (Sony)
product_name	VARCHAR(255)	Tên hiển thị của sản phẩm.	NOT NULL	Tai nghe không dây Sony WH-1000XM4
price	DECIMAL(12,2)	Giá bán hiện tại của sản phẩm.	NOT NULL, ≥0	6500000.00
stock_quantity	INT	Số lượng hàng vật lý còn lại trong kho khả dụng.	NOT NULL, ≥0	45
is_active	BOOLEAN	Trạng thái kinh doanh (Cho phép hiển thị/Bán).	NOT NULL, DEFAULT TRUE	true
3. Thực thể: PurchaseHistory (Lịch sử mua hàng)
Phân hệ dữ liệu lịch sử đơn hàng làm đầu vào (Input Features) quan trọng cho thuật toán gợi ý của AI.

Field Name	Data Type	Description	Constraint	Example Value
purchase_id	BIGINT	Khóa chính, định danh bản ghi lịch sử mua hàng.	PRIMARY KEY, AUTO_INCREMENT	9928311
user_id	BIGINT	Định danh người dùng thực hiện mua hàng.	FOREIGN KEY, INDEXED, NOT NULL	1054329
product_id	BIGINT	Định danh sản phẩm đã được mua thành công.	FOREIGN KEY, NOT NULL	88432
order_id	BIGINT	Mã đơn hàng chứa sản phẩm này.	FOREIGN KEY, NOT NULL	550122
purchased_at	TIMESTAMP	Thời điểm đơn hàng chuyển sang trạng thái HOÀN THÀNH.	NOT NULL, INDEXED	2026-05-20 14:15:22
4. Thực thể: RecommendationResult (Kết quả gợi ý từ AI)
Bảng lưu trữ hoặc bộ nhớ đệm (Cache) kết quả tính toán từ Recommendation Engine để tối ưu hóa SLA phản hồi.

Field Name	Data Type	Description	Constraint	Example Value
rec_id	VARCHAR(64)	Khóa chính, định danh chuỗi kết quả băm (MD5/UUID).	PRIMARY KEY	rec_hash_99a8b7c6
user_id	BIGINT	Định danh người dùng nhận gợi ý (Null nếu là khách).	INDEXED, NULLABLE	1054329
source_product_id	BIGINT	Sản phẩm gốc mà người dùng đang xem tại trang PDP.	INDEXED, NOT NULL	88432
recommended_products	JSON / TEXT	Mảng danh sách các product_id gợi ý sắp xếp theo thứ tự ưu tiên (Tối đa 10 IDs).	NOT NULL	[88433, 91200, 77412]
correlation_scores	JSON / TEXT	Mảng điểm số tương quan tương ứng với các sản phẩm gợi ý (Do AI chấm).	NOT NULL	[0.98, 0.85, 0.72]
algorithm_type	VARCHAR(50)	Tên thuật toán được dùng để sinh ra kết quả này.	NOT NULL (PERSONALIZED, TRENDING, FALLBACK)	PERSONALIZED
updated_at	TIMESTAMP	Thời điểm cập nhật kết quả (Dùng để tính thời gian hết hạn Cache TTL).	NOT NULL	2026-06-18 20:00:00
