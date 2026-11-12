# Ghi chú phân tích · Day 04

Họ và tên: Trần Quang Hưng
MSSV: 2A202603767

## 1. Case được chọn

- ID case: H1
- Câu trả lời của agent: "### Incident GitHub - **h02n9572mx9y**\n- **Tên:** Incident with Actions\n- **Trạng thái:** Đã được giải quyết\n- **Thời gian bắt đầu:** 2026-11-04T17:40:33Z\n- **Thời gian cập nhật:** 2026-11-07T01:10:18Z\n- **Thành phần liên quan:** Actions\n- **Cập nhật:**\n  1. **Đã giải quyết:** 2026-11-04T18:16:08Z - \"Vui lòng tham khảo tóm tắt kết hợp trong sự cố liên quan: [tại đây](https://www.githubstatus.com/incidents/xr3myzj7ms51)\"\n  2. **Đang giám sát:** 2026-11-04T18:07:51Z - \"Sự suy giảm ảnh hưởng đến Actions đã được giảm thiểu. Chúng tôi đang giám sát để đảm bảo tính ổn định.\"\n  3. **Đang điều tra:** 2026-11-04T17:40:33Z - \"Chúng tôi đang điều tra các báo cáo về việc giảm khả năng sử dụng cho Actions.\"\n\n### Incident Cloudflare - **yaa0witbl2me**\n- **Tên:** Workers Builds Issues\n- **Trạng thái:** Đã được giải quyết\n- **Thời gian bắt đầu:** 2026-11-05T19:51:39Z\n- **Thời gian cập nhật:** 2026-11-05T20:20:10Z\n- **Thành phần liên quan:** Workers Builds\n- **Cập nhật:**\n  1. **Đã giải quyết:** 2026-11-05T20:20:10Z - \"Thời gian hàng đợi đã trở lại bình thường.\"\n  2. **Đang giám sát:** 2026-11-05T19:55:51Z - \"Các bản xây dựng đang được xử lý và chúng tôi đang làm việc để giải quyết tồn đọng.\"\n  3. **Đã nhận diện:** 2026-11-05T19:51:39Z - \"Cloudflare nhận thức được và đang điều tra một vấn đề với Cloudflare Workers Builds có thể ảnh hưởng đến nhiều khách hàng.\"\n\n### So sánh giữa hai incident:\n- **Thời gian:**\n  - GitHub: 2026-11-04\n  - Cloudflare: 2026-11-05\n- **Trạng thái:** Cả hai đều đã được giải quyết.\n- **Thành phần:** Không có sự chồng chéo rõ ràng trong thành phần giữa cả hai sự cố; GitHub tập trung vào Actions trong khi Cloudflare tập trung vào Workers Builds.\n  \n### Kết luận:\nHiện tại không có bằng chứng rõ ràng cho thấy một sự cố cụ thể của GitHub và Cloudflare có quan hệ nhân quả với nhau hay không. Các incident riêng biệt với các thành phần khác nhau diễn ra gần nhau trong thời gian nhưng thiếu thông tin liên kết trực tiếp giữa chúng.\n\n### Nguồn:\n- [GitHub Incident Details](https://stspg.io/7pwv28hvkmz8)\n- [Cloudflare Incident Details](https://www.cloudflarestatus.com/incidents/yaa0witbl2me)",
- Điểm ở lần chạy 1: 60

## 2. Bằng chứng trong trace

Dán đoạn trace chứng minh lỗi và nêu nguyên nhân có thể xảy ra.

```text
    {
      "status": "resolved",
      "created_at": "2026-11-04T18:16:08.361Z",
      "body": "Please refer to the combined summary in this related incident: https://www.githubstatus.com/incidents/xr3myzj7ms51",
      "truncated": false
    },

```
Nguyên nhấn vấn đề có thể do agent chưa đi theo hết mọi link liên quan đến incident để đưa ra một kết luận chính xác nhất.

## 3. Thay đổi đã thực hiện

- Sửa gì, ở đâu: Thêm chỉ dẫn follow đường link nếu gặp phải trong quá trình tra cứu. Sửa ở system prompt
- Vì sao chọn thay đổi này: Thay đổi này sẽ (hi vọng) cải thiện điểm của H1 và H6 khi gặp phải trường hợp này.

## 4. So sánh hai lần chạy

| Chỉ số | `eval_before.json` | `eval_after.json` |
|---|---|---|
| Điểm tổng | 80.95 | 80.0 |
| Điểm case đã chọn | 60 | 60 |
| Số model calls | 2 | 2 |
| Token, chi phí nếu có | 2200 token, cost 0.00039255 | 2316 token, 0.00044235|

- Lỗi đã giải quyết: Tăng được điểm test H6, và H8, giải quyết được vấn đề không tiếp tục tra cứu đường link đồng thời agent đưa ra được lời giải thích phù hợp hơn
- Lỗi còn lại hoặc mới xuất hiện: Điểm nhìn chung của các test khác phần lớn giảm và chưa giải quyết trực tiếp được vấn đề của test H1

## 5. Giới hạn

Điểm judge gây giới hạn về mặt trình bày, vì mỗi lần prompt AI có thể trình bày một cách hoàn toàn khác và bị đánh giá điểm thấp hơn. Với snapshot từ ngày 9/11 trở về trước, có nhiều thông tin chưa đủ mới làm ảnh hưởng đến khả năng tra cứu thông tin chính xác của agent. Mỗi phiên bản chỉ chạy một lần làm cho đánh giá không được khách quan vì khả năng dự đoán của AI là khác nhau mỗi lần làm cho kết quả chạy có thể dao động rất mạnh nếu chạy được nhiều lần khác nhau.
