# 🤖 Multi-Agent System với LangGraph

Dự án này triển khai các hệ thống multi-agent thông minh sử dụng LangGraph và LangChain, cho phép nhiều AI agent chuyên biệt cộng tác với nhau để giải quyết các tác vụ phức tạp.

## 📋 Mục lục

- [Cài đặt](#-cài-đặt)
- [1. Simple Multi-Agent](#1️⃣-simple-multi-agent)
- [2. Visual Agentic AI](#2️⃣-visual-agentic-ai)
- [Dependencies](#-dependencies)
- [Lưu ý kỹ thuật](#-lưu-ý-kỹ-thuật)

## 🚀 Cài đặt

### Yêu cầu hệ thống
- Python >= 3.12
- UV package manager

### Các bước cài đặt

**Bước 1:** Clone repository
```bash
git clone <repository-url>
cd Multi-agent
```

**Bước 2:** Cài đặt dependencies
```bash
uv sync
```

**Bước 3:** Cấu hình biến môi trường

Tạo file `.env` trong thư mục gốc:
```bash
OPENAI_API_KEY=your_openai_api_key
TAVILY_API_KEY=your_tavily_api_key
```

---

## 1️⃣ Simple Multi-Agent

> **File:** [Multi-agent.ipynb](Multi-agent.ipynb)

### 📖 Tổng quan
Hệ thống multi-agent đơn giản với supervisor quản lý hai agent chuyên biệt để xử lý các tác vụ tìm kiếm thông tin và tính toán.

### ✨ Tính năng
- ✅ **Tìm kiếm web real-time** với Tavily Search
- ✅ **Tính toán toán học** (cộng, nhân, chia)
- ✅ **Supervisor thông minh** tự động phân bổ công việc
- ✅ **Hỗ trợ tiếng Việt** đầy đủ

### 🏗️ Kiến trúc

```
        Supervisor (GPT-4o)
              │
    ┌─────────┴─────────┐
    ▼                   ▼
Research Agent      Math Agent
(Web Search)        (Calculator)
```

### 🤖 Các Agent

#### 1. Research Agent
- **Tools:** `TavilySearch` (tìm kiếm web real-time)
- **Chức năng:** Tìm kiếm và tổng hợp thông tin từ internet
- **Model:** GPT-4o-mini

#### 2. Math Agent  
- **Tools:** `add()`, `multiply()`, `divide()`
- **Chức năng:** Thực hiện các phép tính toán học
- **Model:** GPT-4o-mini

#### 3. Supervisor
- **Model:** GPT-4o
- **Chức năng:** 
  - Phân tích yêu cầu người dùng
  - Giao việc cho agent phù hợp
  - Tổng hợp kết quả cuối cùng

### 🚀 Cách chạy
1. Mở file [Multi-agent.ipynb](Multi-agent.ipynb)
2. Chạy lần lượt từng cell bằng cách nhấn nút ▶️ Run

### 💡 Ví dụ sử dụng

**Example 1:** Tìm kiếm thông tin
```python
"Ai là thị trưởng của thành phố New York?"
```
→ Research Agent tìm kiếm trên web

**Example 2:** Tính toán
```python
"Kết quả của phép tính (3 + 5) x 7 là bao nhiêu?"
```
→ Math Agent thực hiện tính toán

**Example 3:** Kết hợp cả hai
```python
"Hãy tìm GDP của Việt Nam năm 2023 và 2024, 
sau đó tính toán tỷ lệ tăng/giảm phần trăm giữa hai năm này?"
```
→ Research Agent tìm GDP → Math Agent tính tỷ lệ

---

## 2️⃣ Visual Agentic AI

> **File:** [Visual-Agentic-AI.ipynb](Visual-Agentic-AI.ipynb)

### 📖 Tổng quan
Hệ thống multi-agent nâng cao kết hợp khả năng nghiên cứu học thuật và xử lý hình ảnh với computer vision.

### ✨ Tính năng
- 🔍 **Tìm kiếm bài báo khoa học** trên Arxiv
- 📚 **Tra cứu thông tin** trên Wikipedia  
- 🖼️ **Mô tả chi tiết hình ảnh** với GPT-4o-mini
- 🎯 **Phát hiện và đếm đối tượng** với YOLOv11x
- 🤝 **Kết hợp nhiều agent** để xử lý tác vụ phức tạp
- 🌐 **Hỗ trợ ảnh local và URL**

### 🏗️ Kiến trúc

```
        Supervisor (GPT-4o)
              │
    ┌─────────┴─────────┐
    ▼                   ▼
Research Agent      Visual Agent
(Arxiv, Wiki)     (Vision AI)
                       │
                  ┌────┴────┐
                  ▼         ▼
            Image       Object
          Describer    Detection
          (GPT-4o)     (YOLOv11)
```

### 🤖 Các Agent

#### 1. Research Agent
- **Tools:** 
  - `ArxivQueryRun`: Tìm bài báo khoa học
  - `WikipediaQueryRun`: Tra cứu Wikipedia
- **Chức năng:** Tìm kiếm và tổng hợp thông tin học thuật
- **Model:** GPT-4o-mini
- **Đặc biệt:** Tự động dịch kết quả sang tiếng Việt

#### 2. Visual Agent
- **Tools:**
  - `image_describer`: Mô tả nội dung ảnh chi tiết
  - `detect_and_count_objects`: Phát hiện đối tượng với YOLO
- **Chức năng:** 
  - Phân tích và mô tả hình ảnh
  - Phát hiện, đếm và định vị đối tượng
  - Trích xuất văn bản trong ảnh (OCR)
- **Model:** GPT-4o-mini + YOLOv11x
- **Output:** Mô tả chi tiết, số lượng đối tượng, tọa độ bounding box, confidence score

#### 3. Supervisor  
- **Model:** GPT-4o
- **Chức năng:**
  - Điều phối Research Agent và Visual Agent
  - Kết hợp kết quả từ nhiều agent
  - Trả lời cuối cùng cho người dùng

### 🚀 Cách chạy
1. Mở file [Visual-Agentic-AI.ipynb](Visual-Agentic-AI.ipynb)
2. Chạy lần lượt từng cell bằng cách nhấn nút ▶️ Run
3. **Lưu ý:** Cell đầu tiên sẽ tự động tải YOLO model (~200MB)

### 💡 Ví dụ sử dụng

**Example 1:** Nghiên cứu đơn giản
```python
"Nghiên cứu mới nhất về positional embeddings là gì?"
```
→ Research Agent tìm trên Arxiv và Wikipedia

**Example 2:** Phân tích ảnh
```python
"Có bao nhiêu con chó trong bức ảnh này? 
Bức ảnh: https://example.com/dog.jpg"
```
→ Visual Agent phát hiện và đếm đối tượng

**Example 3:** Kết hợp Visual + Research
```python
"Khái niệm được thể hiện trong bức ảnh này là gì? 
Bức ảnh: https://huggingface.co/datasets/tmnam20/Storage/resolve/main/rope.png
Hãy cung cấp thông tin chi tiết và các bài nghiên cứu liên quan."
```
→ Visual Agent mô tả ảnh → Research Agent tìm thông tin chi tiết

**Example 4:** Phân tích chi tiết
```python
"Con chó trong hình có bộ lông màu gì? 
Và hãy cung cấp cho tôi thêm thông tin về giống chó này.
Bức ảnh: https://example.com/terrier.jpg"
```
→ Visual Agent mô tả → Research Agent tìm thông tin về giống chó

---

## 📦 Dependencies

### Core Frameworks
- `langchain==0.3.24` - Framework chính cho LLM applications
- `langchain-openai==0.3.14` - Integration với OpenAI models
- `langgraph>=0.6.11` - State machine và workflow cho multi-agent
- `langgraph-supervisor>=0.0.29` - Supervisor pattern implementation

### Search & Research Tools
- `langchain-tavily==0.1.6` - Web search real-time
- `langchain-community>=0.3.23` - Community tools (Arxiv, Wikipedia, DuckDuckGo)
- `arxiv>=2.4.0` - Arxiv API client
- `wikipedia>=1.4.0` - Wikipedia API client
- `duckduckgo-search>=8.1.1` - DuckDuckGo search engine

### Computer Vision (chỉ cho Visual Agentic AI)
- `ultralytics>=8.3.252` - YOLOv11 object detection framework
- `torch>=2.9.1` - PyTorch deep learning backend
- `torchvision>=0.24.1` - Computer vision utilities
- `opencv-python>=4.11.0.86` - Image processing library

### Utilities
- `python-dotenv>=1.2.1` - Environment variables management
- `python-magic>=0.4.27` - File type detection
- `ipykernel>=7.1.0` - Jupyter notebook kernel support

📄 Xem [pyproject.toml](pyproject.toml) để biết danh sách đầy đủ các dependencies.

---

## 🔧 Lưu ý kỹ thuật

### Simple Multi-Agent
- ✅ Nhẹ, không yêu cầu GPU
- ✅ Chỉ cần ~500MB RAM
- ✅ Chạy nhanh trên mọi máy

### Visual Agentic AI  
- ⚠️ **YOLO Model**: Lần đầu chạy sẽ tự động tải `yolo11x.pt` (~200MB)
- ⚠️ **RAM**: Yêu cầu tối thiểu ~2GB RAM
- ⚠️ **GPU**: Tự động sử dụng CUDA nếu có GPU NVIDIA (tăng tốc 10-20x)
- ⚠️ **CPU**: Vẫn chạy được nhưng chậm hơn (~2-3s/ảnh)

### API Keys
- `OPENAI_API_KEY` - **Bắt buộc** cho cả hai hệ thống
- `TAVILY_API_KEY` - Chỉ cần cho Simple Multi-Agent

---

## 📄 License

MIT License

## 👥 Đóng góp

Mọi đóng góp đều được chào đón! Vui lòng tạo issue hoặc pull request.

---

**Phiên bản:** 0.1.0  
**Cập nhật:** January 2026