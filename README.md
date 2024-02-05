- PhoGPT-7.5B-Fine-tuning-QLoRA
- Author: Mr.Jack _ Công ty www.BICweb.vn
- Start Date: 23 Dec-2023
- End Date: 05 Feb-2024

# Foundation:
- github: https://github.com/VinAIResearch/PhoGPT
- huggingface: https://huggingface.co/vinai/PhoGPT-7B5-Instruct
- PhoGPT: Generative Pre-training for Vietnamese (https://arxiv.org/abs/2311.02945)
- MPT model: https://huggingface.co/docs/transformers/model_doc/mpt ; https://www.mosaicml.com/mpt
- Introducing MPT-7B: A New Standard for Open-Source, Commercially Usable LLMs (https://www.databricks.com/blog/mpt-7b)
- PEFT: https://huggingface.co/docs/peft/en/index ; https://arxiv.org/abs/2205.05638
- LoRA: https://huggingface.co/docs/diffusers/en/training/lora ; https://arxiv.org/abs/2106.09685
- Quantization: https://huggingface.co/docs/accelerate/en/usage_guides/quantization
- Flash attention: https://huggingface.co/docs/text-generation-inference/conceptual/flash_attention ; https://arxiv.org/abs/2205.14135
- ALiBi: Train Short, Test Long: Attention with Linear Biases Enables Input Length Extrapolation (https://arxiv.org/abs/2108.12409)

# Sự kiện:
- Ngày 21 Aug-2023: "Vào ngày 21/08/2023, Công ty Cổ phần VinBigdata công bố xây dựng thành công mô hình ngôn ngữ lớn tiếng Việt, đặt nền móng cho việc xây dựng các giải pháp tích hợp AI tạo sinh..." (https://genk.vn/vinbigdata-phat-trien-cong-nghe-ai-tao-sinh-se-som-cho-ra-mat-chatgpt-phien-ban-viet-20230821140700664.chn)
- Ngày 06 Nov-2023: PhoGPT: Generative Pre-training for Vietnamese (https://arxiv.org/abs/2311.02945)
- Ngày 05 Dec-2023: Thế giới có ChatGPT, Việt Nam có PhởGPT (https://tuoitre.vn/the-gioi-co-chatgpt-viet-nam-co-phogpt-20231205164736363.htm)
- Ngày 06 Dec-2023: VinAI bất ngờ giới thiệu PhởGPT: Cạnh tranh với ChatGPT, hiểu văn phong tiếng Việt vượt bậc (https://cafef.vn/vinai-bat-ngo-gioi-thieu-phogpt-canh-tranh-voi-chatgpt-hieu-van-phong-tieng-viet-vuot-bac-188231206132611864.chn)
- Ngày 06 Dec-2023: Được mệnh danh là "ChatGPT phiên bản Việt", PhởGPT có gì khác biệt? (https://doisongphapluat.nguoiduatin.vn/uoc-menh-danh-la-chat-gpt-phien-ban-viet-pho-gpt-co-gi-khac-biet-a395419.html)

# Lý do:
- Khi mà trên thế giới tràn ngập các model English only với quy mô từ nhỏ (1M-33M-124M) đến lớn (7B-13B-33B) và khổng lồ (70B-180B), nhưng ở Việt Nam thì chưa thấy có model nào quy mô khoảng 7B dùng được cả thì việc fine-tuning được một em ChatGPT biết "ăn nói nhẹ hàng" ở nhà để vọc vạch là "ước mơ" của bao đời Lập trình viên chứ không của riêng ai. Vì vậy khi VinAi công bố model PhoGPT-7.5B là mình cũng thấy rất hào hứng và muốn bắt tay vào fine-tuning em nó để phục vụ mục đích nghiên cứu và học tập.
- Mình chia sẻ kết quả này để động viên anh em "ngành" là anh em cứ mạnh dạn Fine-tuning PhoGPT-7.5B hoặc các Model-7B nói chung bằng bộ thư viện PEFT-QLoRA thì khá nhẹ và nhanh chứ không bị nặng và lâu đâu nhé. Mỗi item chỉ train khoảng 1s trên Colab T4 là quá ổn nhé vì train bằng QLoRA nên số lượng params train rất ít mà kết quả vẫn Ok ^^

# Fine-tuning model PhoGPT-7.5B
- Cấu hình Colab T4 (15GB) trở lên
- Source code … không phải làm gì nhiều vì bộ thư viện Transformers và Peft nó làm gần hết việc rồi, chỉ mỗi cấu hình Trainer 😂
- Dataset cá nhân siêu nhỏ, tuỳ nhu cầu sử dụng
- Thời gian train ~1s/item
- File LoRA khá nhỏ gọn, tổng cộng khoảng dưới 800MB
- Training loss xuống cũng khá nhanh, nhưng lại không bị Overfit sớm
- Khi dùng Peft hay ở chỗ là Fine-tuning thì chỉ cần dùng em T4-15GB colab (vì dùng QLoRA nên giảm được bộ nhớ GPU), nhưng Inference lại phải gọi đến em V100-16GB colab 😂
