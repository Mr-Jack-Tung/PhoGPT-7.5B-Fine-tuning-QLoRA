- PhoGPT-7.5B-Fine-tuning-QLoRA
- Author: Mr.Jack _ Công ty www.BICweb.vn
- Start Date: 23 Dec-2023
- End Date: 05 Feb-2024

# Sự kiện:
- Ngày 06 Nov-2023: PhoGPT: Generative Pre-training for Vietnamese (https://arxiv.org/abs/2311.02945)
- Ngày 05 Dec-2023: Thế giới có ChatGPT, Việt Nam có PhởGPT (https://tuoitre.vn/the-gioi-co-chatgpt-viet-nam-co-phogpt-20231205164736363.htm)

# Lý do:
- Khi mà trên thế giới tràn lan các model English only với quy mô từ nhỏ (1M-33M-124M) đến lớn (7B-13B-33B) và khổng lồ (70B-180B), nhưng ở Việt Nam thì chưa thấy có model nào quy mô khoảng 7B dùng được cả thì việc fine-tuning được một em ChatGPT biết "ăn nói nhẹ hàng" ở nhà để vọc vạch là "ước mơ" của bao đời Lập trình viên chứ không của riêng ai. Vì vậy khi VinAi công bố model PhoGPT-7.5B là mình cũng thấy rất hào hứng và muốn bắt tay vào fine-tuning em nó để phục vụ mục đích nghiên cứu và học tập.

# Fine-tuning model PhoGPT-7.5B
- Cấu hình Colab T4 (15GB) trở lên
- Source code … không phải làm gì nhiều vì bộ thư viện Transformers và Peft nó làm gần hết việc rồi, chỉ mỗi cấu hình Trainer  😂
- Dataset cá nhân siêu nhỏ, tuỳ nhu cầu sử dụng
- Thời gian train ~1s/item
- File LoRA khá nhỏ gọn, tổng cộng khoảng dưới 800MB
