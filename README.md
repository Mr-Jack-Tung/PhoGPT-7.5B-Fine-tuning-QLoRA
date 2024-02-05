- PhoGPT-7.5B-Fine-tuning-QLoRA
- Author: Mr.Jack _ Công ty www.BICweb.vn
- Date: 05 Feb-2024

# Sự kiện:
- Ngày 06 Nov-2023: PhoGPT: Generative Pre-training for Vietnamese (https://arxiv.org/abs/2311.02945)
- Ngày 05 Dec-2023: Thế giới có ChatGPT, Việt Nam có PhởGPT (https://tuoitre.vn/the-gioi-co-chatgpt-viet-nam-co-phogpt-20231205164736363.htm)

# Fine-tuning model PhoGPT-7.5B
- Cấu hình Colab T4 (15GB) trở lên
- Source code … không phải làm gì nhiều vì bộ thư viện Transformers và Peft nó làm gần hết việc rồi, chỉ mỗi cấu hình Trainer  😂
- Dataset cá nhân siêu nhỏ, tuỳ nhu cầu sử dụng
- Thời gian train ~1s/item
- File LoRA khá nhỏ gọn, tổng cộng khoảng dưới 800MB
- 
