# Lab 21 — Phân tích rủi ro AI qua case study thực tế

- Họ và tên: Nguyễn Văn Biển
- Mã học viên: 2A202602416
- Lớp: AI Thực Chiến — Track 1
- Ngành đã chọn: **HR / tuyển dụng** (AI sàng lọc CV, chấm điểm và lọc ứng viên)

> Quy ước trong bài: **[Sự kiện]** = điều nguồn xác nhận; **[Nhận định]** = suy luận/đánh giá của tôi. Các mức Thấp/Trung bình/Cao là đánh giá định tính cho bài tập, không phải kết luận phân loại pháp lý.

### 1. Industry Risk Snapshot

| Nội dung | Đánh giá của tôi và lý do |
| --- | --- |
| Những tác hại chính có thể xảy ra | (1) **Mất cơ hội việc làm** do AI lọc bỏ ứng viên đủ năng lực — ứng viên chịu thiệt trực tiếp. (2) **Phân biệt đối xử có hệ thống** theo giới, tuổi, chủng tộc, khuyết tật vì mô hình học lại thiên lệch từ dữ liệu tuyển dụng quá khứ — ảnh hưởng nhóm yếu thế. (3) **Thiếu minh bạch / không thể khiếu nại**: ứng viên bị từ chối tự động, không biết lý do. (4) **Mất riêng tư** do thu thập và suy luận dữ liệu cá nhân từ CV, video phỏng vấn. (5) Rủi ro pháp lý và uy tín cho doanh nghiệp tuyển dụng và nhà cung cấp phần mềm. |
| Mức độ high-stakes | **Cao.** Quyết định tuyển dụng ảnh hưởng trực tiếp đến thu nhập, sinh kế và lộ trình nghề nghiệp. Một công cụ được nhiều nhà tuyển dụng dùng chung có thể lặp lại cùng một lỗi trên hàng triệu hồ sơ, nên lỗi mang tính hệ thống chứ không đơn lẻ. EU AI Act cũng xếp AI dùng trong tuyển dụng/sàng lọc ứng viên vào nhóm high-risk (Annex III), điều này khớp với đánh giá của tôi. |
| Dữ liệu nhạy cảm có thể được sử dụng | Họ tên, ngày sinh/tuổi, giới tính, ảnh, địa chỉ; trường học, lịch sử công việc (có thể là *proxy* cho giới, tuổi, chủng tộc — ví dụ tên trường nữ sinh, năm tốt nghiệp); tình trạng sức khỏe/khuyết tật; video/giọng nói phỏng vấn; kết quả bài test tâm lý. *(Bài không chứa dữ liệu thật của bất kỳ ứng viên nào.)* |
| Nhu cầu human review | **Cao.** (a) **Trước triển khai**: đội HR + pháp chế + data scientist kiểm tra bias audit (tỷ lệ chọn theo nhóm, quy tắc 4/5) trên dữ liệu thử. (b) **Khi vận hành**: recruiter phải xem xét thủ công các hồ sơ bị AI loại, không để AI tự động từ chối ở bước cuối; lấy mẫu ngẫu nhiên hồ sơ bị loại để soát lỗi. (c) **Sau quyết định**: có kênh để ứng viên yêu cầu người thật xem lại. Lý do: lỗi thiên lệch thường không nhìn thấy ở từng hồ sơ riêng lẻ, chỉ phát hiện được khi có người kiểm tra số liệu tổng hợp. |

### 2. Case study 1 — Amazon: công cụ AI chấm điểm CV thiên lệch chống lại phụ nữ

#### Brief Case

- Tổ chức / sản phẩm AI: Amazon — công cụ tuyển dụng thử nghiệm (nội bộ, không có tên thương mại) chấm điểm CV bằng machine learning.
- Thời gian, địa điểm / bối cảnh: Phát triển từ 2014 bởi đội machine learning của Amazon; phát hiện thiên lệch khoảng 2015; nhóm dự án bị giải tán đầu năm 2017; Reuters công bố ngày 10/10/2018.
- AI được dùng để làm gì: Chấm điểm ứng viên từ 1 đến 5 sao dựa trên CV, nhằm tự động chọn ra các ứng viên tốt nhất cho vị trí kỹ thuật (software developer và các vị trí kỹ thuật khác).
- Vấn đề hoặc sự kiện đáng chú ý: **[Sự kiện]** Mô hình được huấn luyện trên CV nộp cho Amazon trong 10 năm, phần lớn của nam giới; kết quả là hệ thống **hạ điểm CV có chữ "women's"** (vd. "women's chess club captain") và **hạ điểm ứng viên tốt nghiệp hai trường đại học chỉ dành cho nữ**. Amazon chỉnh sửa để trung lập với các từ này nhưng không đảm bảo mô hình không tìm cách phân biệt khác, nên dừng dự án. Ngoài ra dữ liệu có vấn đề khiến hệ thống còn gợi ý ứng viên không đủ năng lực cho nhiều vị trí.
- Số liệu có nguồn:
  - **500** mô hình theo từng chức năng công việc và địa điểm, mỗi mô hình học nhận diện khoảng **50.000** thuật ngữ từ CV cũ (Reuters, 10/10/2018).
  - Dữ liệu huấn luyện: CV nộp trong **10 năm** (Reuters).
  - Thang điểm **1–5 sao** (Reuters).
  - Bối cảnh ngành: khoảng **55%** quản lý nhân sự Mỹ cho rằng AI sẽ là phần thường xuyên trong công việc trong 5 năm tới (khảo sát CareerBuilder 2017, Reuters trích dẫn).
- Nguồn:
  - Jeffrey Dastin — *Amazon scraps secret AI recruiting tool that showed bias against women* — Reuters — 10/10/2018 — https://www.reuters.com/article/us-amazon-com-jobs-automation-insight-idUSKCN1MK08G
  - Bản đăng lại cùng nội dung (dự phòng nếu Reuters chặn): https://www.cnbc.com/2018/10/10/amazon-scraps-a-secret-ai-recruiting-tool-that-showed-bias-against-women.html
- Phân biệt bằng chứng và nhận định:
  - **[Sự kiện]** Mô hình hạ điểm dấu hiệu liên quan đến phụ nữ; dự án bị dừng. Theo Reuters, recruiter có xem gợi ý của công cụ nhưng **không chỉ dựa vào** xếp hạng đó; Amazon nói công cụ không được dùng để đánh giá ứng viên.
  - **[Nhận định]** Không có số liệu công khai về số ứng viên nữ bị loại thực tế. Vì vậy tác hại cho cá nhân cụ thể là **chưa được xác nhận**; tôi phân tích ở mức *nguy cơ* nếu công cụ được dùng tự động hóa hoàn toàn.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Bước sàng lọc CV đầu vào cho vị trí kỹ thuật: AI chấm 1–5 sao, recruiter dựa vào điểm này để chọn ai được vào vòng tiếp theo. |
| Stakeholder bị ảnh hưởng | Trực tiếp: ứng viên nữ (và ứng viên học trường nữ, tham gia hoạt động dành cho nữ). Gián tiếp: recruiter/hiring manager (ra quyết định dựa trên điểm sai), Amazon (pháp lý, uy tín, mất nhân tài), ngành công nghệ (mất cân bằng giới càng sâu). |
| Failure mode | **Bias / fairness** (chính): học lại sự mất cân bằng giới trong dữ liệu lịch sử, kể cả qua *proxy* (từ "women's", tên trường). Phụ: **Over-reliance** — nguy cơ recruiter tin điểm sao như một đánh giá khách quan. |
| Layer bắt đầu lỗi | **Model** (kèm dữ liệu huấn luyện): mô hình được huấn luyện để bắt chước quyết định tuyển dụng quá khứ, vốn do nam giới chiếm đa số → mục tiêu học đã chứa thiên lệch. **UX** là lớp phụ (giả thuyết): hiển thị dạng "5 sao" dễ tạo cảm giác chắc chắn, khó cho recruiter nhận ra lỗi. Nguồn không công bố kiến trúc chi tiết. |
| Harm xảy ra là gì? | **Nguy cơ (chưa xác nhận đã xảy ra với cá nhân cụ thể):** ứng viên nữ đủ năng lực bị xếp hạng thấp hơn và mất cơ hội vào vòng phỏng vấn khi CV có dấu hiệu liên quan đến phụ nữ. **Đã xảy ra:** lỗi thiên lệch của mô hình (được chính đội Amazon phát hiện) và dự án nhiều năm bị hủy — tổn thất cho tổ chức. |
| Harm lens | **Opportunity loss** (mất cơ hội việc làm); **Dignity loss** (bị đánh giá thấp vì giới tính). |
| Severity | **High** — mất cơ hội việc làm ảnh hưởng thu nhập và sự nghiệp, và là hành vi phân biệt bị pháp luật cấm. Không phải Critical vì không gây tổn hại thể chất. |
| Scale | **Tiềm năng: High; thực tế: chưa đủ dữ liệu.** 500 mô hình phủ nhiều chức năng/địa điểm của một nhà tuyển dụng rất lớn → nếu áp dụng tự động thì phạm vi ảnh hưởng rộng. Không có số ứng viên bị ảnh hưởng được công bố. |
| Probability | **High (nhận định của tôi)** với ứng viên có dấu hiệu "nữ" trong CV, vì đây là hành vi có hệ thống của mô hình (Reuters xác nhận mô hình hạ điểm), không phải lỗi ngẫu nhiên. Không có tỷ lệ đo được công khai. |
| Frequency | **High nếu triển khai** — lỗi lặp lại ở mọi CV có đặc điểm tương tự. Thực tế bị chặn vì dự án dừng và recruiter không chỉ dựa vào điểm. |
| Vì sao? | Căn cứ chính là Reuters (nguồn ẩn danh nội bộ, Amazon không phủ nhận việc dừng dự án). Giới hạn: không có số liệu ứng viên bị loại, không có kiến trúc mô hình; các đánh giá Scale/Probability/Frequency là nhận định. Bài học: "xóa từ khóa nhạy cảm" không đủ, vì mô hình vẫn tìm được proxy → cần bias audit theo kết quả đầu ra và human review. |

### 3. Case study 2 — iTutorGroup: phần mềm tuyển dụng tự động loại ứng viên lớn tuổi (EEOC)

#### Brief Case

- Tổ chức / sản phẩm AI: iTutorGroup (gồm 3 công ty liên kết, cung cấp dạy tiếng Anh trực tuyến cho học viên ở Trung Quốc) — phần mềm xử lý đơn ứng tuyển gia sư.
- Thời gian, địa điểm / bối cảnh: Năm 2020, tuyển gia sư làm việc từ xa tại Mỹ. EEOC (Ủy ban Cơ hội Việc làm Bình đẳng Mỹ) khởi kiện năm 2022 (EEOC v. iTutorGroup, Inc., et al., Tòa Liên bang Quận Đông New York); thỏa thuận hòa giải công bố 13/9/2023. Báo chí chuyên ngành mô tả đây là một trong những vụ dàn xếp đầu tiên của EEOC liên quan đến phần mềm tuyển dụng tự động (nhận định của báo chí, không phải của EEOC).
- AI được dùng để làm gì: Tự động sàng lọc đơn ứng tuyển gia sư.
- Vấn đề hoặc sự kiện đáng chú ý: **[Sự kiện]** Phần mềm được lập trình để **tự động loại ứng viên nữ từ 55 tuổi trở lên và ứng viên nam từ 60 tuổi trở lên**, vi phạm Luật chống phân biệt tuổi tác trong việc làm (ADEA). Theo các báo cáo về vụ kiện, vụ việc bị phát hiện khi một ứng viên nộp hai hồ sơ giống nhau, chỉ khác ngày sinh — hồ sơ trẻ hơn được mời phỏng vấn.
- Số liệu có nguồn:
  - **Hơn 200** ứng viên đủ điều kiện ở Mỹ bị loại vì tuổi (EEOC, 2023).
  - Ngưỡng loại tự động: **nữ ≥ 55 tuổi, nam ≥ 60 tuổi** (EEOC).
  - Tiền dàn xếp: **365.000 USD** chia cho các ứng viên bị loại tự động; EEOC giám sát tuân thủ **ít nhất 5 năm** (EEOC, 13/9/2023).
- Nguồn:
  - U.S. EEOC — *iTutorGroup to Pay $365,000 to Settle EEOC Discriminatory Hiring Suit* — 13/9/2023 — https://www.eeoc.gov/newsroom/itutorgroup-pay-365000-settle-eeoc-discriminatory-hiring-suit
  - Bản tin email chính thức của EEOC (dự phòng): https://content.govdelivery.com/accounts/USEEOC/bulletins/370170c
- Phân biệt bằng chứng và nhận định:
  - **[Sự kiện]** Quy tắc loại theo tuổi, số >200 ứng viên, 365.000 USD, cam kết đào tạo, chính sách mới và giám sát 5 năm — do EEOC công bố. iTutorGroup dàn xếp và không thừa nhận sai phạm.
  - **[Nhận định]** Hệ thống ở đây là **quy tắc tự động đơn giản** (rule-based), chưa chắc là machine learning. Tôi vẫn chọn case vì nó là "automated decision-making" trong tuyển dụng và minh họa rõ rủi ro khi không có human review. Số 200 là con số được xác định trong vụ kiện, số thực tế có thể khác.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Thời điểm ứng viên nộp đơn: phần mềm đọc ngày sinh và **tự động từ chối** trước khi có bất kỳ người nào xem hồ sơ. |
| Stakeholder bị ảnh hưởng | Trực tiếp: ứng viên nữ ≥55, nam ≥60 ở Mỹ. Gián tiếp: học viên (mất gia sư có kinh nghiệm), iTutorGroup (bồi thường, bị giám sát, mất uy tín), cơ quan quản lý (EEOC). |
| Failure mode | **Bias / fairness** — phân biệt trực tiếp theo tuổi (và theo giới, vì ngưỡng khác nhau cho nam/nữ). Kèm **Escalation failure**: hệ thống ra quyết định từ chối cuối cùng mà không chuyển cho người kiểm tra. |
| Layer bắt đầu lỗi | **Grounding** (quy tắc/cấu hình hệ thống): lỗi nằm ở logic do con người cài đặt — tiêu chí sàng lọc trái luật được viết thẳng vào hệ thống, không phải mô hình "tự học" sai. **Safety** là lớp thứ hai: không có cơ chế chặn tiêu chí bị cấm (tuổi) và không có bước human review trước khi từ chối. |
| Harm xảy ra là gì? | **Đã xảy ra (EEOC xác nhận):** hơn 200 ứng viên đủ năng lực ở Mỹ bị từ chối tự động vì tuổi và mất cơ hội làm gia sư trong năm 2020. |
| Harm lens | **Opportunity loss**; **Dignity loss** (bị loại chỉ vì tuổi và giới). |
| Severity | **High** — mất cơ hội thu nhập, phân biệt đối xử trái luật, có hậu quả pháp lý thật. |
| Scale | **Medium** — >200 người theo EEOC; giới hạn ở một công ty và một nhóm vị trí (gia sư). |
| Probability | **Rất cao (≈100%) với nhóm thuộc ngưỡng tuổi** — vì là quy tắc cứng: mọi ứng viên đạt ngưỡng tuổi đều bị loại. Đây là suy luận từ mô tả của EEOC. |
| Frequency | **High** — lặp lại với mỗi đơn của nhóm tuổi đó cho đến khi bị phát hiện và kiện. |
| Vì sao? | Nguồn chính là thông cáo cơ quan nhà nước (độ tin cậy cao). Case cho thấy rủi ro không chỉ đến từ mô hình phức tạp: một quy tắc tự động sai + không có người xem lại cũng gây hại hàng loạt. Giới hạn: EEOC không công bố chi tiết kỹ thuật phần mềm. |

### 4. Case study 3 — Mobley v. Workday: vụ kiện tập thể về AI sàng lọc ứng viên

#### Brief Case

- Tổ chức / sản phẩm AI: Workday, Inc. — nền tảng tuyển dụng (applicant tracking) có tính năng AI đề xuất/xếp hạng ứng viên, được nhiều doanh nghiệp sử dụng; sau này bao gồm cả các tính năng HiredScore AI (Workday mua lại 4/2024).
- Thời gian, địa điểm / bối cảnh: Đơn kiện nộp 21/2/2023 tại Tòa Liên bang Quận Bắc California (Case No. 23-cv-00770-RFL, thẩm phán Rita Lin). 7/2024: tòa bác yêu cầu hủy vụ kiện của Workday. 16/5/2025: tòa chấp thuận chứng nhận sơ bộ vụ kiện tập thể (collective action) theo ADEA cho ứng viên từ 40 tuổi trở lên. 7/2025: tòa yêu cầu mở rộng phạm vi sang ứng viên được xử lý qua HiredScore.
- AI được dùng để làm gì: Sàng lọc, chấm điểm và đề xuất ứng viên cho các nhà tuyển dụng dùng Workday.
- Vấn đề hoặc sự kiện đáng chú ý: **[Cáo buộc, chưa có phán quyết cuối cùng]** Nguyên đơn Derek Mobley — người Mỹ gốc Phi, trên 40 tuổi, có tình trạng lo âu và trầm cảm — cho biết từ 2017 đã nộp **hơn 100** đơn vào các công ty dùng Workday và **bị từ chối tất cả**. Ông cáo buộc AI của Workday tạo tác động bất lợi (disparate impact) theo chủng tộc, tuổi và khuyết tật. **[Sự kiện tố tụng]** Tòa cho phép vụ kiện tiếp tục và chứng nhận sơ bộ nhóm tập thể; tòa xác định thiệt hại chung là bị "denied the right to compete on equal footing with other candidates".
- Số liệu có nguồn:
  - Workday cho biết **1,1 tỷ đơn ứng tuyển bị từ chối** thông qua công cụ phần mềm của họ trong giai đoạn liên quan → nhóm tập thể có thể gồm **"hàng trăm triệu"** thành viên (Proskauer, tóm tắt lệnh ngày 16/5/2025).
  - Nguyên đơn: **>100** đơn bị từ chối kể từ **2017** (theo đơn kiện, được các nguồn tóm tắt).
- Nguồn:
  - Proskauer Rose LLP (blog Law and the Workplace) — *AI Bias Lawsuit Against Workday Reaches Next Stage as Court Grants Conditional Certification of ADEA Claim* — 6/2025 — https://www.proskauer.com/blog/ai-bias-lawsuit-against-workday-reaches-next-stage-as-court-grants-conditional-certification-of-adea-claim
  - CSD / REFRAIME — *Case 9: Mobley v. Workday* (tóm tắt sự kiện vụ án) — https://refraime.csd.eu/wp-content/uploads/case-9-en.pdf
  - Hồ sơ vụ án: *Mobley v. Workday, Inc.*, N.D. Cal., No. 3:23-cv-00770 — https://www.courtlistener.com/?q=Mobley+v.+Workday
- Phân biệt bằng chứng và nhận định:
  - **[Sự kiện]** Có vụ kiện, các mốc tố tụng, con số 1,1 tỷ đơn bị từ chối do chính Workday đưa ra trong hồ sơ.
  - **[Cáo buộc]** AI của Workday gây phân biệt — **chưa được tòa kết luận**. Workday phản bác rằng quyết định tuyển dụng là của doanh nghiệp khách hàng và tác động khác nhau tùy khách hàng.
  - **[Nhận định]** 1,1 tỷ là tổng số đơn bị từ chối, **không phải** số đơn bị từ chối sai/do thiên lệch. Tôi chỉ dùng nó để ước lượng *quy mô tiềm năng*.

#### Harm Map Worksheet

| Trường | Phân tích của tôi |
| --- | --- |
| High-risk moment | Ứng viên nộp đơn qua cổng Workday của doanh nghiệp; AI chấm điểm/đề xuất và đơn có thể bị từ chối trước khi recruiter đọc (chi tiết vận hành cụ thể chưa được công bố). |
| Stakeholder bị ảnh hưởng | Trực tiếp: ứng viên ≥40 tuổi, ứng viên da màu, ứng viên khuyết tật (theo cáo buộc). Gián tiếp: hàng nghìn doanh nghiệp khách hàng của Workday (rủi ro pháp lý, mất ứng viên tốt), Workday (nhà cung cấp — tòa coi có thể chịu trách nhiệm như "agent" của nhà tuyển dụng), thị trường lao động nói chung. |
| Failure mode | **Bias / fairness** (cáo buộc disparate impact). **Over-reliance**: doanh nghiệp tin điểm/đề xuất của AI để loại hồ sơ hàng loạt. **Escalation failure** (giả thuyết): thiếu bước người thật xem lại trước khi từ chối. |
| Layer bắt đầu lỗi | **Chưa đủ bằng chứng** — Workday không công bố chi tiết mô hình và vụ án chưa kết thúc. Giả thuyết của tôi: (1) **Model** — học từ dữ liệu quyết định tuyển dụng quá khứ của khách hàng, có thể chứa proxy về tuổi (năm tốt nghiệp, số năm kinh nghiệm); (2) **Safety/UX** — cấu hình cho phép tự động từ chối hoặc ẩn ứng viên điểm thấp khiến recruiter không bao giờ thấy họ. |
| Harm xảy ra là gì? | **Nguy cơ (đang được tòa xem xét, chưa xác nhận):** ứng viên lớn tuổi/da màu/khuyết tật bị loại một cách có hệ thống trên nhiều công ty cùng lúc → mất cơ hội việc làm lặp lại, không biết lý do và không có ai để khiếu nại. **Đã xảy ra:** nguyên đơn bị từ chối >100 lần (nguyên nhân do AI hay không là vấn đề còn tranh chấp). |
| Harm lens | **Opportunity loss** (chính); **Dignity loss**; **Privacy loss** (tiềm năng — suy luận tuổi/khuyết tật từ dữ liệu CV). |
| Severity | **High** — mất sinh kế, phân biệt nhiều đặc điểm được bảo vệ; tác động cộng dồn vì một người bị chặn ở rất nhiều công ty cùng dùng một nền tảng. |
| Scale | **Rất cao (tiềm năng)** — 1,1 tỷ đơn bị từ chối qua công cụ Workday; tòa nói nhóm tập thể có thể lên tới hàng trăm triệu người. Đây là quy mô hệ thống, khác biệt lớn với case 1 và 2 (một công ty). |
| Probability | **Chưa đủ dữ liệu để đánh giá.** Không có số liệu công khai về tỷ lệ chọn theo nhóm tuổi/chủng tộc. Việc tòa cho vụ kiện đi tiếp chỉ có nghĩa cáo buộc đủ hợp lý để xem xét, chưa chứng minh xác suất. |
| Frequency | **High nếu cáo buộc đúng** — mỗi đơn nộp qua hệ thống đều đi qua cùng một logic chấm điểm. Hiện là nhận định. |
| Vì sao? | Case này cho thấy rủi ro **"monoculture"**: khi nhiều nhà tuyển dụng dùng chung một AI, thiên lệch không còn là lỗi của một công ty mà thành rào cản cho cả thị trường lao động. Giới hạn bằng chứng: vụ án đang diễn ra, tôi dựa vào tóm tắt của hãng luật và tổ chức nghiên cứu, không phải phán quyết cuối cùng. |

### 5. Tổng hợp và bài học cho ngành HR

| | Case 1 — Amazon | Case 2 — iTutorGroup | Case 3 — Workday |
| --- | --- | --- | --- |
| Loại hệ thống | ML tự học từ CV cũ | Quy tắc tự động cứng | Nền tảng AI dùng chung |
| Layer chính | Model (dữ liệu) | Grounding/cấu hình + Safety | Chưa đủ bằng chứng |
| Tình trạng harm | Nguy cơ (dự án dừng) | Đã xảy ra (EEOC xác nhận) | Đang tranh chấp tại tòa |
| Scale | Một công ty lớn | >200 người | Tiềm năng hàng trăm triệu |

**Đề xuất (nhận định của tôi):**
1. **Bias audit định kỳ** theo kết quả đầu ra (tỷ lệ chọn theo giới, tuổi, nhóm), không chỉ xóa trường nhạy cảm — vì mô hình học được proxy (case 1).
2. **Chặn cứng tiêu chí bị cấm** (tuổi, giới…) ở lớp cấu hình và review quy tắc sàng lọc bởi pháp chế trước khi triển khai (case 2).
3. **Không để AI ra quyết định từ chối cuối cùng**: AI chỉ xếp hạng/gợi ý; người thật phải xem xét hồ sơ bị loại, ít nhất bằng lấy mẫu (case 2, 3).
4. **Minh bạch với ứng viên**: thông báo có dùng AI, cung cấp kênh yêu cầu người xem lại.
5. **Phân định trách nhiệm nhà cung cấp – doanh nghiệp** trong hợp đồng, vì nhà cung cấp AI cũng có thể bị coi là chịu trách nhiệm (case 3).
