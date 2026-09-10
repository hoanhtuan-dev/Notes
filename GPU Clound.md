Dựa trên thông tin màn hình GPU của bạn, server đang chạy template `vllm-openai:latest-cu129`. Đối với vLLM, **API Key chính là mã do bạn tự thiết lập** khi khởi chạy server vLLM, hoặc nếu container khởi chạy sẵn thì bạn có thể truy cập vào Terminal (SSH hoặc TTYD) để kiểm tra/đặt API Key.

---

### Bước 1: Mở Terminal điều khiển

Bạn có 2 cách rất tiện lợi ngay trên giao diện ảnh:

1. **Cách 1 (Dễ nhất - Trực tiếp trên web):**
* Nhấp vào đường link ở mục **TTYD**: `[http://n3.ckey.vn:1364](http://n3.ckey.vn:1364)`
* Màn hình Terminal dòng lệnh Ubuntu sẽ mở ra ngay trên trình duyệt.


2. **Cách 2 (Qua SSH):**
* Mở Terminal/PowerShell trên máy tính của bạn và dán lệnh trong mục **SSH**:
```bash
ssh root@n3.ckey.vn -p 1363

```





---

### Bước 2: Khởi chạy vLLM và đặt API Key riêng của bạn

Trong màn hình Terminal (TTYD hoặc SSH), bạn thực hiện chạy lệnh vLLM. Bạn có thể tự đặt chuỗi API Key bất kỳ ở tham số `--api-key`:

```bash
python3 -m vllm.entrypoints.openai.api_server \
  --model Qwen/qwen3.8:27b \
  --host 0.0.0.0 \
  --port 8000 \
  --api-key atd-api-276813

```

> **Ghi chú:**
> * **API Key của bạn:** `my-secret-api-key-12345` *(bạn có thể đổi thành chuỗi tùy ý)*.
> * **Base URL API:** `[http://n3.ckey.vn:1365/v1](http://n3.ckey.vn:1365/v1)` *(nhìn từ mục `vLLM API` trên ảnh của bạn: `[http://n3.ckey.vn:1365](http://n3.ckey.vn:1365)`)*.
> 
> 

---

### Bước 3: Kiểm tra & Sử dụng API Key trong Python

Sau khi vLLM chạy xong, bạn dùng thông tin vừa tạo để gọi API:

```python
import openai

client = openai.OpenAI(
    base_url="http://n3.ckey.vn:1365/v1",       # URL lấy từ mục vLLM API trên ảnh
    api_key="my-secret-api-key-12345"          # API Key bạn đã đặt ở bước 2
)

response = client.chat.completions.create(
    model="Qwen/Qwen2.5-7B-Instruct",
    messages=[
        {"role": "user", "content": "Xin chào, hãy giới thiệu ngắn gọn về bạn!"}
    ]
)

print(response.choices[0].message.content)

```

*(Lưu ý: Nếu container tự chạy sẵn service vLLM ở ngầm mà không yêu cầu `--api-key`, bạn có thể dùng bất kỳ chuỗi text nào cho tham số `api_key` trong Python code).*


**Không thể** chạy cùng lúc nhiều model LLM lớn đầy đủ trên 1 GPU RTX 5060 Ti (16GB VRAM) với vLLM thông thường, vì mỗi model 7B-8B đã chiếm từ 12GB–14GB VRAM để chứa weight và KV Cache.

Tuy nhiên, bạn hoàn toàn có thể phục vụ nhiều nhu cầu/model trên cùng kết nối SSH qua các giải pháp kỹ thuật sau:

---

### Giải pháp 1: Dùng LoRA Adapter (Khuyên dùng - Chạy 1 Model nền, tải nhiều LoRA)

Nếu bạn có nhiều phiên bản model fine-tune khác nhau (như 1 LoRA cho viết code, 1 LoRA cho chat tiếng Việt) từ cùng một model gốc (ví dụ Qwen 2.5 7B):

vLLM cho phép bạn load **1 Model nền + nhiều LoRA Adapter cùng lúc** mà tốn rất ít VRAM:

```bash
python3 -m vllm.entrypoints.openai.api_server \
  --model Qwen/Qwen2.5-7B-Instruct \
  --enable-lora \
  --lora-modules task-writer=/path/to/lora1 task-coder=/path/to/lora2 \
  --host 0.0.0.0 \
  --port 8000 \
  --api-key my-secret-key

```

*Khi gọi API, bạn chỉ cần đổi tên `model` thành `"task-writer"` hoặc `"task-coder"`.*

---

### Giải pháp 2: Dùng Ollama (Tự động swap/chuyển đổi Model)

Nếu bạn muốn dùng các model hoàn toàn khác nhau (ví dụ vừa dùng `llama3.1:8b`, vừa dùng `qwen2.5:7b`, vừa dùng `gemma2:9b`):

1. **Khởi chạy Ollama Server:**
```bash
ollama serve

```


2. **Tải các model về sẵn:**
```bash
ollama pull llama3.1
ollama pull qwen2.5

```



Ollama sẽ tự động **load/unload VRAM linh hoạt**: khi bạn gọi API model A, nó nạp model A vào GPU; khi bạn gọi API model B, nó sẽ xả model A khỏi VRAM và nạp model B vào.

---

### Bảng so sánh giải pháp

| Phương pháp | Số Model chạy song song | Tốc độ chuyển Model | Tối ưu VRAM 16GB |
| --- | --- | --- | --- |
| **vLLM Standard** | 1 Model duy nhất | Phải tắt process chạy lại | Rất cao |
| **vLLM + LoRA** | 1 Base Model + Nhiều LoRA | Tức thì (Concurrent) | Rất cao |
| **Ollama** | Nhiều Model (Lần lượt) | Mất vài giây để swap VRAM | Tự động quản lý |