# BÀI LÀM PHA 1 

- **Họ tên:** Nguyễn Ngọc Duy Anh
- **Lớp:** HCM-KS26-CNTT1
- **Link repository Pha1:**

> Pha 1 (70 phút đầu, KHÔNG dùng AI). Viết xong, kéo thả file này vào repository Pha1 trước mốc giờ giám thị công bố.

## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khán giả [TEN_KHACH], số điện thoại [SO_DIEN_THOAI], số CCCD [SO_CCCD], email [EMAIL], đặt 3 vé gói SVT trận bán kết Cúp Sao Vàng ngày 18/12/2026 cho 2 người lớn và 1 trẻ em 9 tuổi. Khán giả đã chuyển khoản đặt cọc 1.500.000 đồng. Khán giả yêu cầu 3 ghế ngồi cạnh nhau gần lối đi.
```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
Câu 1: Chỉ sử dụng thông tin có trong file chính sách hoàn/huỷ vé để trả lời, không tự suy luận hoặc bổ sung thông tin bên ngoài. Nếu trong file không có thôn tin thì phải hỏi hoặc báo cho tôi, không được nói những thông tin mà không có trong file.

Câu 2: Khi trả lời, phải ghi rõ nguồn thông tin được trích dẫn, điều khoản hoặc số trang ở trong file để cho người đọc dễ dàng kiểm tra đối chiếu.
```

## 4.2. Trích xuất tin nhắn đặt vé ra JSON

### PROMPT

#### C - Context
Hãy đóng vai trò là một người chuyên xử lý và chuyển hoá thông tin đặt vé sự kiện.

BẢNG MÃ GÓI
|SVT|FZ|FZ|
|---|---|---|
|Sân Vận Động: vé trận đấu|Fan Zone: khu cổ vũ|Khán đài VIP|

#### R - Request
Nhiệm vụ của bạn là:
- Nhiệm vụ của bạn là đọc tin nhắn khách hàng, trích xuất thông tin và chuyển đổi thành dữ liệu JSON theo cấu trúc thống nhất.
- Xử lý 3 tin nhắn TN1, TN2, TN3 và chuyển thành một mảng JSON 3 đối tượng, đúng thứ tự, đúng 6 trường.

Mã đối tượng phải có đúng 6 trường:
- ma_goi:
- ngay_su_kien:
- nguoi_lon:
- tre_em:
- loai_ve:
- ghi_chu:

#### E - Explanation
Tuân thủ 5 quy tắc chuẩn hoá sau:
1. ma_goi lấy theo bảng mã gói.
2. ngay_su_kien dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
4. loai_ve chỉ nhận "thuong", "vip" hoặc null.
5. ghi_chu chỉ ghi yêu cầu đặc biệt về chỗ ngồi, hỗ trợ di chuyển hoặc ăn uống; không có thì null.

#### A - Action
**ví dụ 1:**

Tin nhắn đầu vào: Đặt giúp mình 2 vé VIP trận chung kết ngày 15/11/2026, 2 người lớn và 1 bé. Cần chỗ ngồi cạnh lối đi.

Kết quả:
```JSON
{
    "ma_goi": "VIP",
  "ngay_su_kien": "2026-11-15",
  "nguoi_lon": 2,
  "tre_em": 1,
  "loai_ve": "vip",
  "ghi_chu": "chỗ ngồi cạnh lối đi"
}
```
**ví dụ 2:**

Tin nhắn đầu vào: Cho mình một vé Fan Zone, ngày nào cũng được, mình đi một mình.

Kết quả:
```JSON
{
    "ma_goi": "FZ"
    "ngay_su_kien": null
    "nguoi_lon": 1
    "tre_em": 0
    "loai_ve": "thuong"
    "ghi_chu": null
}
```
**Dữ liệu cần xử lý**
<tin_nhan>
TN1: Mình muốn đặt gói Sân Vận Động trận tứ kết ngày 20/12 nha, 2 người lớn với 1 bé 8 tuổi, vé thường.

TN2: Cho 3 người đi Fan Zone trận ngày 05/01/2027 ạ. Một người cần hỗ trợ xe lăn.

TN3: Trận chung kết Cúp Sao Vàng tháng 12 còn vé không ạ? Nhà em 4 người lớn, có một người khiếm thị cần hỗ trợ tìm chỗ, lấy vé VIP.
</tin_nhan>

Hãy xử lý từng tin nhắn độc lập, không bỏ sót thông tin và không tự suy diễn dữ liệu không được đề cập.
#### T - Tone
- Sử dụng giọng điệu nhẹ nhàng, tiếng Việt.
- Chính xác, khách quan và nhất quán.
- Không tự suy luận hoặc bịa thêm thông tin.
- Ưu tiên dữ liệu được khách hàng cung cấp.
- Không thay đổi tên hoặc kiểu dữ liệu của 6 trường đã quy định.

#### E - Extras
- Số lượng khách phải là kiểu số nguyên.
- Không thêm trường ngoài 6 trường đã quy định.
- Đảm bảo JSON hợp lệ, có thể sử dụng trực tiếp trong chương trình Python hoặc JavaScript.
- Tuyệt đối không chào hỏi, không giải thích, không viết nhận xét và không sử dụng Markdown bên ngoài JSON.
- Sử dụng `null` khi không có thông tin phù hợp.

## 4.3. Báo giá vé bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
1. ROLE (Vai trò)
Bạn là AI chuyên xử lý yêu cầu đặt vé và tính toán chi phí vé sự kiện. Nhiệm vụ của bạn là đọc bảng giá, áp dụng đúng các quy tắc tính giá và đưa ra tổng số tiền khách hàng cần thanh toán.
2. CONTEXT (Bối cảnh)
Khách hàng cung cấp thông tin về loại vé, số lượng người lớn, trẻ em và yêu cầu sử dụng khu ghế ưu tiên. Bạn phải tính toán dựa hoàn toàn vào dữ liệu được cung cấp bên dưới.
3. INPUT DATA (Dữ liệu đầu vào)

<du_lieu>
BẢNG GIÁ VÉ (đồng/người lớn)
- SVT – Sân Vận Động: 1.200.000 đồng.
- FZ – Fan Zone: 800.000 đồng.
- VIP – Khán đài VIP: 2.500.000 đồng.

QUY TẮC TÍNH GIÁ
1. Trẻ em từ 5 đến 11 tuổi tính 70% giá người lớn. Trẻ dưới 5 tuổi miễn phí.
2. Nhóm từ 5 người lớn trở lên được giảm 5% trên tiền vé (tiền người lớn + tiền trẻ em).
3. Phụ thu khu ghế ưu tiên: 300.000 đồng/người. Phụ thu không được giảm giá.
4. Tổng tiền = tiền vé sau giảm + phụ thu.

YÊU CẦU BÁO GIÁ
Nhóm cổ động viên đi xem trận bán kết, mua gói SVT, gồm 5 người lớn, 2 trẻ em (8 tuổi và 10 tuổi) và 1 bé 3 tuổi. Có 1 người lớn chọn khu ghế ưu tiên.
</du_lieu>
4. TASK (Nhiệm vụ)
Hãy tính tổng tiền khách hàng phải thanh toán theo đúng 6 bước sau:

Bước 1: Tính tiền người lớn
- Xác định giá vé người lớn theo gói đã chọn.
- Ghi rõ phép tính: số người lớn × giá vé.

Bước 2: Tính tiền trẻ em
- Tính riêng giá vé từng trẻ theo độ tuổi.
- Trẻ từ 5 đến 11 tuổi tính 70% giá người lớn.
- Trẻ dưới 5 tuổi được miễn phí.
- Ghi rõ phép tính của từng trẻ và tổng tiền trẻ em.

Bước 3: Tính tiền vé
- Cộng tiền người lớn và tiền trẻ em.
- Ghi rõ phép tính và kết quả.

Bước 4: Tính giảm giá nhóm
- Kiểm tra điều kiện nhóm có từ 5 người lớn trở lên.
- Nếu đủ điều kiện, giảm 5% trên tổng tiền vé (người lớn + trẻ em).
- Nếu không đủ điều kiện, mức giảm bằng 0 đồng.
- Ghi rõ phép tính số tiền được giảm.

Bước 5: Tính phụ thu
- Xác định số người chọn khu ghế ưu tiên.
- Tính phụ thu 300.000 đồng/người.
- Ghi rõ phép tính.
- Không áp dụng giảm giá đối với khoản phụ thu.

Bước 6: Tính tổng tiền
- Lấy tiền vé trừ tiền giảm giá, sau đó cộng phụ thu.
- Ghi rõ công thức và kết quả cuối cùng.
5. CONSTRAINTS (Ràng buộc)
- Chỉ sử dụng bảng giá và quy tắc trong dữ liệu đầu vào.
- Không tự ý thay đổi giá vé hoặc tỷ lệ giảm giá.
- Không tính trẻ dưới 5 tuổi vào tiền vé.
- Điều kiện giảm giá được xét theo số người lớn, không phải tổng số khách.
- Không áp dụng giảm giá cho phụ thu.
- Không bỏ qua bất kỳ bước tính toán nào.
- Tất cả phép tính phải chính xác và sử dụng đơn vị đồng.
- Nếu dữ liệu thiếu hoặc mâu thuẫn, phải nêu rõ thay vì tự bịa thông tin.
6. OUTPUT FORMAT (Định dạng đầu ra)

Trình bày kết quả theo mẫu:

BƯỚC 1: TIỀN NGƯỜI LỚN
[Phép tính]
Kết quả: ... đồng.

BƯỚC 2: TIỀN TRẺ EM
[Phép tính từng trẻ]
Kết quả: ... đồng.

BƯỚC 3: TIỀN VÉ
[Phép tính]
Kết quả: ... đồng.

BƯỚC 4: GIẢM GIÁ NHÓM
[Điều kiện và phép tính]
Kết quả: ... đồng.

BƯỚC 5: PHỤ THU
[Phép tính]
Kết quả: ... đồng.

BƯỚC 6: TỔNG TIỀN
[Phép tính cuối cùng]
Kết quả: ... đồng.

Dòng cuối cùng bắt buộc có định dạng:

[RESULT: <tổng tiền> đồng]

Chỉ sử dụng dữ liệu đã cung cấp, không thêm thông tin ngoài yêu cầu.
```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. (Viết câu trả lời vào đây – xoá dòng này)

2.

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
(Viết câu lệnh vào đây – xoá dòng này)
```

## 4.5. Prompt chấm bài theo Rubric

**PROMPT**

```text
(Viết prompt vào đây – xoá dòng này)
```

## 4.6. Hoàn thiện System Prompt

> Phần Vai trò và Chuẩn đầu ra đã cho sẵn. Viết tiếp phần Quy tắc ràng buộc và Xử lý ngoại lệ.

```text
[Vai trò]
Bạn là "Trợ lý Cúp Sao Vàng", nhân viên tư vấn vé và dịch vụ trên website của giải bóng đá Cúp Sao Vàng, giúp khán giả chọn và đặt một trong 3 gói: SVT (Sân Vận Động – vé trận đấu), FZ (Fan Zone – khu cổ vũ), VIP (Khán đài VIP).

[Quy tắc ràng buộc]
1. (Viết quy tắc 1 – xoá dòng này)
2.
3.

[Chuẩn đầu ra]
Trả lời bằng tiếng Việt, lịch sự, tối đa 120 từ. Giá vé trình bày dạng gạch đầu dòng. Kết thúc bằng một câu hỏi về nhu cầu tiếp theo của khách.

[Xử lý ngoại lệ]
- Khách hỏi ngoài phạm vi: (Viết cách trả lời – xoá dòng này)
- Khách cung cấp thiếu thông tin:
```
