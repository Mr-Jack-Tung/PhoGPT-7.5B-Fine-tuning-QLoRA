# PhoGPT-7.5B-Fine-tuning-QLoRA
- Author: Mr.Jack _ Công ty www.BICweb.vn
- Start Date: 23 Dec-2023
- End Date: 05 Feb-2024
- If you like what I do, give me a star ^^ ~> ⭐

## Fundamental:
- Github: https://github.com/VinAIResearch/PhoGPT
- Huggingface: https://huggingface.co/vinai/PhoGPT-7B5-Instruct
- PhoGPT: Generative Pre-training for Vietnamese (https://arxiv.org/abs/2311.02945)
- MPT model: https://huggingface.co/docs/transformers/model_doc/mpt ; https://www.mosaicml.com/mpt
- Introducing MPT-7B: A New Standard for Open-Source, Commercially Usable LLMs (https://www.databricks.com/blog/mpt-7b)
- PEFT: https://huggingface.co/docs/peft/en/index ; https://arxiv.org/abs/2205.05638
- LoRA: https://huggingface.co/docs/diffusers/en/training/lora ; https://arxiv.org/abs/2106.09685
- Quantization: https://huggingface.co/docs/accelerate/en/usage_guides/quantization ; https://arxiv.org/abs/2208.07339
- Flash attention: https://huggingface.co/docs/text-generation-inference/conceptual/flash_attention ; https://arxiv.org/abs/2205.14135
- ALiBi: Train Short, Test Long: Attention with Linear Biases Enables Input Length Extrapolation (https://arxiv.org/abs/2108.12409)

## Sự kiện:
- Ngày 21 Aug-2023: "Vào ngày 21/08/2023, Công ty Cổ phần VinBigdata công bố xây dựng thành công mô hình ngôn ngữ lớn tiếng Việt, đặt nền móng cho việc xây dựng các giải pháp tích hợp AI tạo sinh..." (https://genk.vn/vinbigdata-phat-trien-cong-nghe-ai-tao-sinh-se-som-cho-ra-mat-chatgpt-phien-ban-viet-20230821140700664.chn)
- Ngày 06 Nov-2023: PhoGPT: Generative Pre-training for Vietnamese (https://arxiv.org/abs/2311.02945)
- Ngày 05 Dec-2023: Thế giới có ChatGPT, Việt Nam có PhởGPT (https://tuoitre.vn/the-gioi-co-chatgpt-viet-nam-co-phogpt-20231205164736363.htm)
- Ngày 06 Dec-2023: VinAI bất ngờ giới thiệu PhởGPT: Cạnh tranh với ChatGPT, hiểu văn phong tiếng Việt vượt bậc (https://cafef.vn/vinai-bat-ngo-gioi-thieu-phogpt-canh-tranh-voi-chatgpt-hieu-van-phong-tieng-viet-vuot-bac-188231206132611864.chn)
- Ngày 06 Dec-2023: Được mệnh danh là "ChatGPT phiên bản Việt", PhởGPT có gì khác biệt? (https://doisongphapluat.nguoiduatin.vn/uoc-menh-danh-la-chat-gpt-phien-ban-viet-pho-gpt-co-gi-khac-biet-a395419.html)

## Lý do:
- Khi mà trên thế giới tràn ngập các model English only với quy mô từ nhỏ (1M-33M-124M), vừa (355M-774M-1.5B) đến lớn (3B-7B-13B-34B) và khổng lồ (70B-180B) với độ trả lời câu hỏi chính xác khá cao, nhưng ở Việt Nam thì chưa thấy có model chat nào quy mô khoảng 7B dùng được :( thì việc fine-tuning được một em ChatGPT biết "ăn nói nhẹ nhàng" ở nhà để vọc vạch là "ước mơ" của bao đời lập trình viên chứ không của riêng ai. Vì vậy khi VinAi công bố model PhoGPT-7.5B là mình cũng thấy rất hào hứng và muốn bắt tay vào fine-tuning em nó để phục vụ mục đích nghiên cứu và học tập.
- Mình chia sẻ kết quả này là để động viên anh em "ngành" hãy cứ mạnh dạn Fine-tuning PhoGPT-7.5B (hoặc các Model-7B nói chung) bằng bộ thư viện PEFT-QLoRA thì khá nhẹ và nhanh chứ không bị nặng và lâu đâu nhé. Mỗi item chỉ train khoảng 1s trên Colab T4 là quá ổn nhé vì train bằng QLoRA nên số lượng params train rất ít mà kết quả vẫn Ok ^^

## Fine-tuning model PhoGPT-7.5B
- Model architecture: MPT-7B (https://www.databricks.com/blog/mpt-7b)
- Cấu hình tối thiểu: GPU 15GB ~ Colab T4
- Source code thì … copy-paste … không phải làm gì nhiều vì bộ thư viện Transformers và Peft nó làm gần hết việc rồi, chỉ mỗi cấu hình Trainer 😂
- Dataset cá nhân siêu nhỏ, tuỳ nhu cầu sử dụng
- Thời gian train ~1s/item
- File LoRA khá nhỏ gọn ~256MB, tổng cộng tất cả các files của 1 checkpoint khoảng dưới 800MB
- Training loss xuống cũng khá nhanh, nhưng lại không bị Overfit sớm
- Khi dùng Peft Fine-tuning với QLoRA-4bit thì giảm được bộ nhớ GPU rất nhiều nên chỉ cần dùng em T4-15GB colab, nhưng Inference 16bfloat thì lại phải gọi đến em V100-16GB colab
- Ví dụ: nếu doanh nghiệp bạn có khoảng 1000 câu hỏi đáp, thì dataset sẽ là 1000 items, Fine-tuning khoảng 30 epoch (ChatGPT-3 fine-tuning khoảng 16 epochs ?! để overfit dữ liệu; còn GPT2 thì "We then fine-tuned a model on each of the datasets, with 500 training epochs per model 😂, a threshold chosen to prevent overfitting."_page4 of https://arxiv.org/pdf/1908.09203.pdf) để cho em nó overfit thì 1000 items x 30 epochs = 30.000 iterations / 3600s = 8.33h Nvidia Tesla T4 colab x $0.42/h = $3.58 ~> một chi phí quá ổn cho một em lễ tân "của nhà trồng được" nhé 😂

![alt text](https://github.com/Mr-Jack-Tung/PhoGPT-7.5B-Fine-tuning-QLoRA/blob/main/Training%20loss.jpg)

![alt text](https://github.com/Mr-Jack-Tung/PhoGPT-7.5B-Fine-tuning-QLoRA/blob/main/LoRA%20checkpoin%20files.jpg)

## Update 05/02/2024 - 01PM:
- khi các bạn train thì nhớ update cái prompt instruction theo sample_prompt_response_pairs (https://github.com/VinAIResearch/PhoGPT/blob/main/sample_instruction_following_dataset/sample_prompt_response_pairs.jsonl) thay cho cái prompt instruction mình đang dùng (version cũ) thì sẽ chuẩn hơn nhé:
- '### Instruction:{question}### Response:' ~> '### Câu hỏi:{question}\n\n### Trả lời:'
- Ví dụ: "### Câu hỏi:\nTìm từ trái nghĩa với từ sau\nỒn ào\n\n### Trả lời:Yên tĩnh."

### bnb_config = BitsAndBytesConfig(
- load_in_4bit=True,
- bnb_4bit_use_double_quant=True,
- bnb_4bit_quant_type="nf4",
- bnb_4bit_compute_dtype="float16")

### model = AutoModelForCausalLM.from_pretrained(
- mode_id,
- quantization_config=bnb_config,
- device_map="cua",
- trust_remote_code=True)

![alt text](https://github.com/Mr-Jack-Tung/PhoGPT-7.5B-Fine-tuning-QLoRA/blob/main/PhoGPT-7B5-Instruct%20model.jpg)

### peft_config = LoraConfig(
- r=32,
- lora_alpha=32,
- target_modules=["attn.Wqkv", "attn.out_proj", "ffn.up_proj", "ffn.down_proj"],
- lora_dropout=0.05,
- bias="none",
- task_type="CAUSAL_LM")

### training_arguments = TrainingArguments(
- output_dir=output_model,
- per_device_train_batch_size=1,
- gradient_accumulation_steps=1,
- optim="paged_adamw_32bit",
- learning_rate=1e-4,
- lr_scheduler_type="cosine",
- save_strategy="steps",
- save_steps=50,
- logging_steps=10,
- num_train_epochs=100,
- max_steps=100,
- fp16=True)

### trainer = SFTTrainer(
- model=model,
- train_dataset=data,
- peft_config=peft_config,
- dataset_text_field="text",
- args=training_arguments,
- tokenizer=tokenizer,
- packing=False,
- max_seq_length=1024)

## Sử dụng model mặc định, chưa qua fine-tuning:

![alt text](https://github.com/Mr-Jack-Tung/PhoGPT-7.5B-Fine-tuning-QLoRA/blob/main/10-cau-hoi-ve-kinh-doanh.jpg)

![alt text](https://github.com/Mr-Jack-Tung/PhoGPT-7.5B-Fine-tuning-QLoRA/blob/main/10-cau-hoi-ve-ban-hang.jpg)

![alt text](https://github.com/Mr-Jack-Tung/PhoGPT-7.5B-Fine-tuning-QLoRA/blob/main/chuyen-gia-tu-van-khoi-nghiep.jpg)![alt text](https://github.com/Mr-Jack-Tung/PhoGPT-7.5B-Fine-tuning-QLoRA/blob/main/chuyen-gia-tu-van-tinh-truong.jpg)

## Update 23Feb2024 - 08PM
Test thử em vinai/PhoGPT-4B-Chat-v0.1 thấy cũng hay phết ^.^ Cấu hình chạy cũng nhẹ nhàng, chỉ cần dùng Colab-T5 là dùng được, mà chỉ cần chạy có 50% là khoảng 7GB GPU thôi nhé.

- Model: vinai/PhoGPT-4B-Chat-v0.1
- Type: Instruction following & Chat
- Model Size: 3.7B
- Context length: 8192
- Vocab size: 20K
- Training data size: 70K instructional prompt and response pairs & 290K conversations
- Note: PROMPT_TEMPLATE = "### Câu hỏi: {instruction}\n### Trả lời:"

![alt text](https://github.com/Mr-Jack-Tung/PhoGPT-7.5B-Fine-tuning-QLoRA/blob/main/test_PhoGPT-4B-Chat-v01.jpg)

