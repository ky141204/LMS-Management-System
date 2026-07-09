---
title: "Event 2"
date: 2026-05-23
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

# BÀI THU HOẠCH: HỘI THẢO CÔNG NGHỆ AWS COMMUNITY DAY VIETNAM

---
> [!IMPORTANT]
> ### 📅 Tổng quan sự kiện & Mục tiêu
> **AWS Community Day Vietnam 2026** là sự kiện công nghệ cộng đồng lớn nhất trong năm về hệ sinh thái Điện toán đám mây Amazon Web Services. Nội dung bài thu hoạch này đúc kết và phân tích chuyên sâu từ **6 chuyên đề thực chiến** xoay quanh các xu hướng nóng hổi nhất hiện nay: Hệ sinh thái AWS, Trí tuệ nhân tạo tạo sinh (Generative AI), Kiến trúc Multi-Agent doanh nghiệp và các chiến lược tối ưu hóa chi phí lẫn hiệu năng đám mây.

## 1. NỘI DUNG CHI TIẾT CỦA BÀI THU HOẠCH

### Thông tin tham dự sự kiện
* **Hình thức:** Offline.
* **Địa điểm tham dự:** Tầng 26.
* **Thời gian tham dự:** 9 giờ.

### Chuyên đề 1: Making AI Actually Work for You — Context Is Everything
* **Diễn giả:** Trịnh Trường (Tinh Truong) – Platform Engineer tại GoTymeX.
* **Chủ đề chính:** Tầm quan trọng của bối cảnh (Context) trong việc tối ưu hóa hiệu quả của AI và xây dựng "Bộ não AI thứ hai" (Second AI Brain).
#### Nội dung cốt lõi:
1. **Nút thắt cổ chai trong ứng dụng AI:** 
   * Nhiều kết quả AI không đạt kỳ vọng không phải do mô hình yếu, mà do thiếu bối cảnh đầu vào (prompt mơ hồ, thiếu thông tin đích, thiếu ràng buộc).
   * AI không thể đọc được suy nghĩ của người dùng; nó chỉ hoạt động dựa trên những gì được cung cấp.
2. **Định nghĩa về bối cảnh (Context):** Bao gồm: Mục tiêu (Goal), Tình huống thực tế (Situation), Ràng buộc kỹ thuật/ngân sách/định dạng (Constraints), và Dữ liệu minh chứng liên quan (Evidence).
3. **Các sai lầm phổ biến khi cung cấp Context:**
   * *Nhồi nhét thông tin (Internet Puller):* Copy toàn bộ tài liệu dài hoặc nhiều ảnh chụp màn hình vào chatbot làm mô hình bị nhiễu và tăng chi phí token.
   * *Nói lại những gì AI đã biết:* Ví dụ cung cấp code Express.js rồi lại yêu cầu AI viết bằng Express.js thay vì chỉ ra yêu cầu refactor cụ thể (phân trang, validation...).
   * *Thiếu mục tiêu và ràng buộc.*
4. **Sự tiến hóa của ứng dụng AI:** Đi từ **Prompt (Câu hỏi đơn lẻ)** $\rightarrow$ **Context (Hệ thống có bối cảnh)** $\rightarrow$ **Memory (Hệ thống ghi nhớ cá nhân hóa)**.
5. **Mô hình "Second AI Brain" (Bộ não thứ hai):**
   * Hoạt động theo chu kỳ: **Store (Lưu trữ ghi chú/code)** $\rightarrow$ **Retrieve (Truy xuất phần liên quan)** $\rightarrow$ **Generate (Tạo câu trả lời)** $\rightarrow$ **Learn (Ghi nhớ bài học)**.
   * Ánh xạ lên dịch vụ AWS: Amazon S3, Vector DB, Amazon Bedrock và các công cụ giám sát (Observability).
---
### Chuyên đề 2: Friendly AI Assistant with Amazon Q (Quick)
* **Diễn giả:** Phạm Ngô Hải Anh – AWS Community Builder tại G-AsiaPacific Vietnam.
* **Chủ đề chính:** Xây dựng trợ lý AI thân thiện trong doanh nghiệp bằng cách sử dụng bộ giải pháp Amazon Quick (Amazon Q).
#### Nội dung cốt lõi:
1. **Nỗi đau của người dùng doanh nghiệp:** Mất nhiều thời gian thu thập/phân tích thông tin từ nhiều nguồn khác nhau, thực hiện các tác vụ lặp đi lặp lại và phụ thuộc vào các chuyên gia để phân tích dữ liệu chuyên sâu.
2. **Giải pháp AI Agentic của AWS:** 
   * Giới thiệu **Amazon Quick Suite** – một trải nghiệm thống nhất, tích hợp an toàn dữ liệu doanh nghiệp để rút ngắn thời gian từ dữ liệu đến hành động.
   * Khả năng kết nối mạnh mẽ: Hơn 40 cổng kết nối dữ liệu (Data connectors), khả năng tích hợp dữ liệu tải lên từ người dùng, cơ sở dữ liệu và kho dữ liệu lớn.
3. **Khung quản trị và bảo mật (Responsible AI):** Đảm bảo an toàn thông qua kiểm soát truy cập (Access controls), thiết lập rào chắn bảo mật (Guardrails) và tuân thủ pháp lý.
4. **Trường hợp sử dụng thực tế (Use Case):** Trợ lý Quản lý dự án (PM Assistant) giúp tự động hóa việc ghi biên bản cuộc họp (MoM - Minutes of Meeting), gửi email cho các bên liên quan và tự động lên lịch họp tiếp theo.
---
### Chuyên đề 3: From Edge to Origin — CloudFront as Your Foundation
* **Diễn giả:** Nguyễn Tuấn Thịnh – DevOps Engineer tại First Cloud AI Journey.
* **Chủ đề chính:** Tối ưu chi phí, nâng cao tính bảo mật, độ tin cậy và hiệu năng hạ tầng web thông qua Amazon CloudFront.
#### Nội dung cốt lõi:
1. **Thử thách của khách hàng về chi phí CDN truyền thống:**
   * Cách tính phí theo lưu lượng (Pay-as-you-go) dễ dẫn đến rủi ro "bùng nổ hóa đơn" (bill spike) lên tới hàng trăm ngàn USD khi có lượng truy cập đột biến hoặc bị tấn công DDoS.
2. **Giải pháp mới từ AWS (Ra mắt tháng 11/2025):** 
   * Gói giá cố định (Fixed-Price CDN & Security Pricing Plans) bao gồm cả CDN (CloudFront), WAF, DDoS protection, DNS (Route 53), Logging (CloudWatch), và S3 storage. Giúp doanh nghiệp chủ động dự báo chi phí tháng.
3. **Phòng chống tấn công phân tán (DDoS):** Tận dụng kiến trúc mạng phân tán toàn cầu của CloudFront (700+ PoPs tại 50+ quốc gia) phối hợp với AWS Shield và AWS WAF để chặn đứng lưu lượng độc hại ngay tại vùng biên gần nguồn tấn công nhất.
4. **Tối ưu hóa chi phí & Hiệu năng:**
   * Miễn phí truyền dữ liệu (Data Transfer Out - DTO) từ các dịch vụ gốc của AWS về CloudFront.
   * Giảm tải CPU cho máy chủ gốc (EC2/ALB) bằng cách đẩy việc xử lý bắt tay TLS (HTTPS), nén dữ liệu (Gzip/Brotli) và phân phối tĩnh lên CloudFront.
   * Nâng cao hiệu năng nhờ kiến trúc bộ đệm nhiều tầng (Multi-layer caching: Edge $\rightarrow$ Regional Edge Caches $\rightarrow$ Origin Shield) và giao thức HTTP/3 (QUIC/UDP) hỗ trợ tải song song vượt trội so với HTTP/1.1.
5. **Cơ chế bảo mật nâng cao:** 
   * Hỗ trợ Mutual TLS (mTLS), Origin Access Control (OAC) để che giấu máy chủ gốc (S3, API Gateway, Lambda), và Signed URL/Signed Cookies để bảo vệ nội dung số có bản quyền.
---
### Chuyên đề 4: 36 Hours with LotusHacks — Building UTMorpho from Idea to Reality
* **Diễn giả/Đội ngũ:** Team VIB.
* **Chủ đề chính:** Kinh nghiệm thực chiến tại Hackathon lớn nhất Việt Nam (LotusHacks) và hành trình xây dựng sản phẩm UTMorpho trong 36 giờ.
#### Nội dung cốt lõi:
1. **Hành trình từ con số 0:** Bắt đầu từ trạng thái chưa có ý tưởng cụ thể (Hour 0), đội ngũ đã tìm kiếm cảm hứng từ những khó khăn trực tiếp trong công việc hàng ngày để kiến tạo nên **UTMorpho** – một công cụ tập trung vào trải nghiệm chỉnh sửa nội dung tối ưu.
2. **Quy trình phát triển dưới áp lực thời gian (36 giờ):**
   * Thiết lập và đồng bộ hóa đội ngũ (Setup & alignment).
   * Phát triển tính năng cốt lõi trước tiên (Core slice).
   * Vượt qua giai đoạn khó khăn ở giữa dự án (The hard middle).
   * Tích hợp, trau chuốt và chuẩn bị bài thuyết trình (Pitching).
3. **Thử thách và thất bại kỹ thuật:**
   * Hiện tượng AI tạo ra quá nhiều nội dung không cần thiết (AI Overgeneration).
   * Giới hạn lượng token (Token Limits) của mô hình.
   * Sự mệt mỏi và kiệt sức (Burnout) cận kề giờ thuyết trình.
4. **Bài học xương máu:**
   * "Ý tưởng thực tế nhất đến từ những ức chế/khó khăn thực tế" (Real Frustration Creates Real Ideas).
   * Nhiều ý tưởng không bằng ý tưởng chất lượng và tập trung.
   * Sự đồng bộ trong giao tiếp và phối hợp nhóm (Team Sync) quyết định sự thành bại dưới áp lực thời gian.
---
### Chuyên đề 5: Non-Determinism of "Deterministic" LLM Settings
* **Diễn giả:** Đức Đào (Duc Dao) – Solution Architect tại Cloud Kinetics.
* **Chủ đề chính:** Bản chất không xác định (Non-Determinism) của LLM ngay cả khi thiết lập Temperature = 0 và các giải pháp giảm thiểu.
#### Nội dung cốt lõi:
1. **Lý thuyết vs. Thực tế:** 
   * *Lý thuyết:* Khi đặt `Temperature = 0`, mô hình sẽ kích hoạt cơ chế giải mã tham lam (greedy decoding) – luôn chọn token có xác suất cao nhất tại mỗi bước, nhằm đảm bảo tính tái lập (deterministic) của kết quả.
   * *Thực tế:* Nghiên cứu thực nghiệm trên 5 mô hình lớn (GPT-3.5, GPT-4o, Llama-3, Mixtral) cho thấy **không có mô hình nào đạt độ ổn định tuyệt đối**. Độ chính xác của câu trả lời có thể lệch tới 15% giữa các lượt chạy giống hệt nhau, và tỷ lệ trùng khớp chuỗi ký tự (exact string match - TARr@10) gần như bằng 0% đối với các tác vụ khó.
2. **Nguyên nhân cốt lõi:**
   * *Nguyên nhân kỹ thuật (GPU):* Các phép tính dấu phẩy động (Floating-point arithmetic) trên GPU không có tính chất kết hợp (`(a + b) + c` không phải lúc nào cũng bằng `a + (b + c)` theo chuẩn IEEE 754). Sự không xác định trong thứ tự thực thi song song của GPU dẫn đến các lỗi làm tròn cực nhỏ ở logits, từ đó làm thay đổi kết quả chọn token xác suất lớn nhất (flip argmax).
   * *Nguyên nhân thương mại (Batching):* Các nhà cung cấp API gộp nhiều yêu cầu của các người dùng khác nhau vào một lượt xử lý (Inference Batching) để tối ưu chi phí phần cứng. Phép tính cho yêu cầu của bạn sẽ bị ảnh hưởng bởi các yêu cầu chạy song song khác trong batch.
3. **Chiến lược giảm thiểu (Mitigation):**
   * *Đa lượt chạy & Biểu quyết (Majority Voting):* Chạy prompt nhiều lần và lấy kết quả xuất hiện nhiều nhất.
   * *Ràng buộc cấu trúc đầu ra:* Sử dụng JSON mode hoặc function calling để thu hẹp không gian từ vựng có thể sinh ra.
   * *Tự host mô hình:* Cho phép kiểm soát toàn bộ tham số hạ tầng suy luận.
   * *Mẹo thực chiến:* Đặt `Temperature = 0.1` thay vì `0` để tránh lỗi lặp từ (repetitive loops), đồng thời thiết kế hệ thống downstream có khả năng xử lý độ lệch thông tin.
---
### Chuyên đề 6: Enterprise-Grade Multi-Agent System — The Case of Startup Credit Scoring
* **Diễn giả:** Vy Lâm (Vy Lam) – Senior Business Systems Analyst tại VPBank.
* **Chủ đề chính:** Thiết kế hệ thống Multi-Agent đạt chuẩn doanh nghiệp lớn để giải quyết bài toán chấm điểm tín dụng startup.
#### Nội dung cốt lõi:
1. **Sự bất tương thích dữ liệu (Structural Mismatch):** Hệ thống ngân hàng truyền thống chấm điểm tín dụng dựa trên tài sản thế chấp, báo cáo tài chính 3 năm, lịch sử tín dụng dài hạn. Trong khi đó, startup chỉ có 6-18 tháng hoạt động, tài sản chủ yếu là sở hữu trí tuệ (IP), đội ngũ và chỉ số tăng trưởng (traction), dữ liệu chủ yếu phi cấu trúc.
2. **Hạn chế của Single Agent (Đơn tác tử):** Dễ bị loãng chuyên môn do bối cảnh quá rộng (Context Limits), không có cơ chế đối trọng giám sát (Checks & Balances), dễ tạo ra đầu ra không đáng tin cậy.
3. **Mô hình Ủy ban tín dụng ảo (Virtual Credit Committee - Multi-Agent):**
   * Các tác tử chuyên biệt hóa phối hợp chặt chẽ: **Financial Analyst** (phân tích dòng tiền, burn rate), **Market Analyst** (TAM/SAM/SOM, đối thủ), **Team Evaluator** (năng lực nhà sáng lập), **Risk Assessor** (đánh giá rủi ro), **Compliance Agent** (tuân thủ chính sách ngân hàng).
   * Các tác tử được điều phối bởi một **Manager Agent** để đưa ra điểm tín dụng đồng thuận cùng vết kiểm toán rõ ràng (Audit Trail).
4. **6 trụ cột của Enterprise-Grade AI:** Security (Bảo mật), Data Governance (Quản trị dữ liệu), Network (Mạng cô lập VPC), Operations (Giám sát vận hành), Human Factors (Yếu tố con người), và Compliance (Tuân thủ pháp lý).
5. **Hiệu quả đầu tư (ROI thực tế):**
   * Giảm thời gian xử lý hồ sơ từ **2-3 tuần xuống còn 2-4 giờ** (nhanh hơn 95%).
   * Giảm số giờ làm việc của chuyên viên từ **40-60 giờ xuống 2-4 giờ**.
   * Nâng tỷ lệ phê duyệt từ **15-20% lên 35-45%** nhờ hiểu đúng dữ liệu startup.
   * Giảm thiểu 95% chi phí đưa ra quyết định.
6. **Lộ trình triển khai:** Trải qua 4 giai đoạn: **Foundation (Xây dựng gốc)** $\rightarrow$ **Integration (Tích hợp hệ thống)** $\rightarrow$ **Pilot (Thử nghiệm)** $\rightarrow$ **Scale (Mở rộng toàn diện)**.
---

## 2. PHÂN TÍCH CHUYÊN SÂU CÁC XU HƯỚNG CÔNG NGHỆ

### 2.1. Context Engineering trở thành kỹ năng cốt lõi khi làm việc với AI

Một điểm nổi bật xuyên suốt các chuyên đề là AI không còn được nhìn nhận như một công cụ chỉ cần đặt câu hỏi rồi nhận câu trả lời. Để AI tạo ra kết quả có giá trị, người dùng cần biết cách cung cấp bối cảnh đầy đủ, rõ ràng và đúng trọng tâm.

Trong thực tế, nhiều sinh viên hoặc lập trình viên mới sử dụng AI thường chỉ viết prompt ngắn, ví dụ "viết giúp tôi API đăng nhập" hoặc "sửa lỗi đoạn code này". Cách làm này có thể cho kết quả nhanh nhưng thiếu ổn định, vì mô hình không hiểu rõ hệ thống đang dùng framework gì, yêu cầu bảo mật ra sao, dữ liệu đầu vào thế nào và tiêu chí hoàn thành là gì.

Từ chuyên đề về **Context Is Everything**, em rút ra rằng một prompt tốt nên có:

* **Mục tiêu rõ ràng:** muốn AI tạo ra kết quả gì.
* **Bối cảnh hệ thống:** dự án đang dùng công nghệ nào, kiến trúc ra sao.
* **Ràng buộc:** giới hạn thời gian, ngân sách, coding style, format đầu ra.
* **Dữ liệu minh chứng:** log lỗi, đoạn code, ảnh chụp màn hình, tài liệu liên quan.
* **Tiêu chí đánh giá:** thế nào là kết quả đúng hoặc có thể sử dụng được.

Kỹ năng này rất gần với cách kỹ sư phần mềm làm việc trong doanh nghiệp: trước khi triển khai, cần hiểu yêu cầu, bối cảnh nghiệp vụ và ràng buộc kỹ thuật. AI chỉ khuếch đại năng lực của người dùng khi người dùng biết đặt vấn đề đúng.

### 2.2. Hạ tầng Cloud là nền tảng cho ứng dụng AI hiện đại

Các chuyên đề cho thấy AI không thể tách rời khỏi hạ tầng cloud. Một ứng dụng AI thực tế cần nhiều thành phần hơn là một mô hình ngôn ngữ lớn. Nó cần nơi lưu trữ dữ liệu, cơ chế truy xuất tri thức, lớp bảo mật, hệ thống giám sát, API, CDN, cơ sở dữ liệu và pipeline vận hành.

Ví dụ, để xây dựng một hệ thống trợ lý AI nội bộ, doanh nghiệp cần:

* Lưu tài liệu trên S3 hoặc hệ thống lưu trữ tương đương.
* Tạo vector index để truy xuất thông tin liên quan.
* Dùng Bedrock hoặc nền tảng model để sinh phản hồi.
* Kiểm soát quyền truy cập theo vai trò.
* Ghi log, theo dõi chi phí và phát hiện lỗi.
* Bảo vệ endpoint bằng WAF, CDN hoặc cơ chế xác thực.

Điều này giúp em nhận ra rằng học AI không chỉ là học prompt hoặc model. Muốn đưa AI vào sản phẩm thật, cần hiểu cloud architecture, security, networking và observability.

### 2.3. Tối ưu chi phí là bài toán kỹ thuật, không chỉ là bài toán tài chính

Chuyên đề CloudFront cho thấy chi phí cloud có thể tăng rất nhanh nếu hệ thống không được thiết kế tốt. Với các ứng dụng web hoặc AI có nhiều người dùng, lưu lượng truy cập, request API và data transfer đều có thể trở thành chi phí lớn.

Tối ưu chi phí không có nghĩa là luôn chọn dịch vụ rẻ nhất. Điều quan trọng là chọn kiến trúc phù hợp:

* Dùng CDN để giảm tải origin.
* Cache nội dung tĩnh và nội dung thường truy cập.
* Đặt cảnh báo billing sớm.
* Theo dõi request bất thường.
* Chọn đúng loại compute cho workload.
* Tắt hoặc cleanup tài nguyên không sử dụng.

Với sinh viên, bài học này rất thực tế. Khi làm project trên AWS, nếu không hiểu billing, có thể để quên EC2, NAT Gateway, database hoặc load balancer và phát sinh chi phí. Vì vậy, kỹ năng đọc pricing, đặt budget và cleanup là một phần quan trọng của việc học cloud.

### 2.4. Multi-Agent mở ra hướng thiết kế hệ thống AI phức tạp hơn

Chuyên đề về hệ thống Multi-Agent cho thấy một agent đơn lẻ khó xử lý các nghiệp vụ lớn, đặc biệt là các bài toán cần nhiều góc nhìn như tài chính, tín dụng, quản trị dự án hoặc chăm sóc khách hàng.

Mô hình Multi-Agent chia hệ thống thành nhiều tác tử chuyên trách:

* Agent phân tích dữ liệu tài chính.
* Agent đánh giá rủi ro.
* Agent kiểm tra tuân thủ.
* Agent tổng hợp kết quả.
* Agent điều phối luồng xử lý.

Điểm hay của cách tiếp cận này là mỗi agent có phạm vi rõ hơn, từ đó giảm tình trạng context quá rộng và tăng khả năng kiểm chứng. Tuy nhiên, Multi-Agent cũng tạo ra thách thức mới: làm sao đồng bộ trạng thái, tránh agent trả lời mâu thuẫn, kiểm soát quyền truy cập và ghi lại audit trail.

---

## 3. LIÊN HỆ VỚI VIỆC HỌC TẬP VÀ LÀM PROJECT CỦA SINH VIÊN

### 3.1. Áp dụng vào project cá nhân

Sau sự kiện, em có thể áp dụng các bài học vào project cá nhân theo hướng thực tế hơn. Ví dụ, nếu xây dựng một website quản lý sự kiện sinh viên, em có thể:

* Dùng CloudFront để phân phối frontend tĩnh.
* Dùng API Gateway và Lambda cho backend.
* Dùng DynamoDB để lưu thông tin đăng ký.
* Dùng IAM role để cấp quyền tối thiểu.
* Dùng CloudWatch để ghi log và theo dõi lỗi.
* Dùng AI assistant để hỗ trợ tra cứu thông tin sự kiện, nhưng phải thiết kế context và dữ liệu nguồn rõ ràng.

Như vậy, bài học từ AWS Community Day không chỉ nằm ở lý thuyết mà có thể chuyển thành cách thiết kế project cụ thể.

### 3.2. Thay đổi cách dùng AI trong học tập

Trước đây, nhiều người dùng AI như một công cụ trả lời nhanh. Sau sự kiện, em nhận thấy nên dùng AI như một cộng sự học tập có cấu trúc hơn:

* Nhờ AI giải thích khái niệm nhưng phải kiểm chứng lại bằng tài liệu chính thức.
* Dùng AI để review code nhưng vẫn tự hiểu lỗi.
* Dùng AI để tạo checklist triển khai.
* Dùng AI để so sánh các phương án kiến trúc.
* Không copy kết quả AI vào project khi chưa kiểm tra.

Đặc biệt, khi dùng AI cho code, cần cung cấp đầy đủ context: stack công nghệ, file liên quan, lỗi cụ thể, yêu cầu đầu ra và giới hạn được phép thay đổi.

### 3.3. Xây dựng tư duy vận hành

Một điểm em thấy quan trọng là các chuyên đề không chỉ nói về xây dựng ứng dụng, mà còn nói về vận hành ứng dụng. Trong môi trường thực tế, một hệ thống tốt không chỉ "chạy được" mà còn phải:

* Theo dõi được.
* Bảo mật được.
* Mở rộng được.
* Dự báo được chi phí.
* Có log để debug.
* Có quy trình rollback khi lỗi.

Đây là sự khác biệt giữa project demo và sản phẩm thật. Với sinh viên, nếu rèn luyện tư duy vận hành từ sớm, khi đi thực tập hoặc làm việc sẽ dễ thích nghi hơn.

---

## 4. KẾ HOẠCH HÀNH ĐỘNG SAU SỰ KIỆN

Sau khi tham gia AWS Community Day Vietnam, em đặt ra một số hướng hành động cụ thể:

1. **Ôn lại nền tảng AWS:** IAM, S3, EC2, VPC, Lambda, CloudWatch và CloudFront.
2. **Thực hành một mini project cloud:** triển khai frontend, backend, database và monitoring.
3. **Rèn luyện context engineering:** viết prompt có mục tiêu, bối cảnh, ràng buộc và tiêu chí đánh giá.
4. **Tìm hiểu thêm về RAG:** học cách lưu tài liệu, tạo embedding và truy xuất thông tin liên quan.
5. **Theo dõi chi phí cloud:** đặt budget alarm và cleanup tài nguyên sau khi thực hành.
6. **Tìm hiểu Multi-Agent:** thử thiết kế một hệ thống nhiều agent đơn giản, ví dụ agent phân tích yêu cầu, agent kiểm tra lỗi và agent tổng hợp kết quả.
7. **Ghi chép lại bài học:** tạo tài liệu cá nhân để lưu lại lỗi gặp phải, cách sửa và kinh nghiệm triển khai.

Kế hoạch này giúp biến kiến thức từ hội thảo thành hành động cụ thể, tránh việc chỉ nghe xong rồi quên. Em nhận thấy giá trị lớn nhất của sự kiện là mở rộng góc nhìn: công nghệ hiện đại không chỉ là một công cụ riêng lẻ, mà là sự kết hợp giữa AI, cloud, bảo mật, vận hành và tư duy sản phẩm.

---

> [!TIP]
> ### 💡 Bài học & Nhận thức chung (Synthesis)
> 
> Từ các bài thuyết trình trên, có thể rút ra 3 bài học mang tính xu hướng lớn trong việc ứng dụng công nghệ hiện nay:
> 
> 1. **Sự dịch chuyển từ "AI đơn giản" sang "Hệ thống AI phức hợp và chuyên biệt hóa"**:
>    * Việc chỉ dùng Prompt cơ bản đã chạm tới giới hạn. Kỹ nghệ bối cảnh (Context Engineering), việc xây dựng hệ thống bộ nhớ (Memory), kết hợp kiến trúc Multi-Agent (nhiều tác tử cộng tác, phản biện nhau) là chìa khóa để đưa AI vào các nghiệp vụ có độ phức tạp cao, yêu cầu tính chính xác như tài chính (VPBank), quản trị dự án (Amazon Q).
> 2. **Kỹ thuật thực chiến luôn đi kèm với sự thấu hiểu giới hạn của công nghệ**:
>    * Cần chấp nhận thực tế rằng LLM có tính chất không xác định (Non-Determinism) từ cấp độ phần cứng GPU và cơ chế API batching. Thay vì tin tưởng tuyệt đối vào thiết lập `temp=0`, kỹ sư cần thiết kế hệ thống chấp nhận sự sai lệch và có cơ chế kiểm chứng (majority voting, guardrails).
> 3. **Hạ tầng đám mây vững chắc là bệ đỡ cho sự tối ưu**:
>    * Dù phát triển AI hay ứng dụng truyền thống, các yếu tố nền tảng về hạ tầng như CDN (CloudFront), WAF, VPC cô lập, và kiểm soát quyền hạn tối giản (Least Privilege IAM) luôn quyết định tính khả thi khi đưa sản phẩm từ môi trường thử nghiệm (PoC/Hackathon) lên quy mô doanh nghiệp lớn (Enterprise-Grade).

## Ảnh minh chứng

![Ảnh minh chứng tham gia AWS Community Day Vietnam](images/aws-community-day-evidence.jpg)

