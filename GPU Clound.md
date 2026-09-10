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
  --model Qwen/Qwen2.5-7B-Instruct \
  --host 0.0.0.0 \
  --port 8000 \
  --api-key my-secret-api-key-12345

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