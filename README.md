
# 📊 AI Statistics Tutor using Phi-3-mini and vLLM
## 🚀 Project Overview


This project is an AI-powered Statistics Tutor developed for a Deep Learning course project using Large Language Models (LLMs). The system is designed to answer statistics-related questions in a simple and educational manner.

The tutor can:
- Explain statistical concepts
- Provide simple explanations
- Give real-life examples
- Answer conceptual questions
- Guide users about statistical tests

Example Questions:
- What is probability?
- When should we use a t-test?
- Difference between correlation and regression
- What is the probability of getting two tails?

## 🎯 Project Objective
The main objective of this project was to design and deploy an AI-powered educational assistant using Large Language Models (LLMs), prompt engineering, and vLLM-based cloud GPU deployment on RunPod.

## 🧠 Initial Approach: RAG (Retrieval-Augmented Generation)
Initially, this project was implemented using the RAG approach.

The following steps were performed:
- Statistical PDF books were uploaded
- Text extraction was performed
- Embeddings were generated
- Vector database was created
- Relevant chunks were retrieved during question answering

### ⚠️ Problem Faced
The extracted text from PDFs contained:
- OCR noise
- Broken sentences
- Formatting issues
- Unclear statistical definitions
Because of this:
- Retrieved chunks became noisy
- The model generated messy responses
- Answers were not reliable enough for educational 

Example of noisy extracted text:
```text
Probability and statistics an fundamentally interrelated...
degree of oelief.in.A.particulautaCment...
```

Therefore, the RAG-based pipeline was not suitable for producing high-quality educational responses due to noisy OCR extraction, broken PDF formatting, and unreliable retrieved context.

## ✅ Final Solution
The final system uses:
- Prompt-engineered LLM improvements
- Phi-3-mini-4k-instruct model
- vLLM deployment on RunPod GPU

Instead of depending on noisy PDF retrieval, the AI tutor was redesigned to generate clean and human-like educational explanations using carefully engineered prompts.

The model was instructed to:
- Answer only the asked question
- Avoid generating unrelated topics
- Give simple explanations
- Provide real-life examples
- Respond like a statistics teacher
## ☁️ Cloud Deployment using vLLM
The model was deployed using:
- RunPod cloud GPU server
- Ubuntu environment
- vLLM API server

This converted the model into a production-style API system.

### Architecture:
- RunPod acts as the server  
- Python client sends requests via API URL  
- vLLM generates real-time responses  
- Chatbot receives and displays answers  

 ## ⚡ Technologies Used

- Python  
- PyTorch (for local inference)  
- Hugging Face Transformers (for loading Phi-3-mini model)  
- microsoft/Phi-3-mini-4k-instruct (Large Language Model)  
- Prompt Engineering (to control AI behavior as a Statistics tutor)  
- vLLM (for high-performance inference server deployment)  
- RunPod (cloud GPU hosting for API deployment)

## 💡 Features

✅ Simple and clear explanations  
✅ Real-life examples  
✅ Educational AI tutor behavior  
✅ Fast inference using vLLM  
✅ Cloud-based deployment  
✅ API-based chatbot system  

# 📂 Project Structure

```bash
project/
│
├── RAG.py
├── LLM.py
├── client.py
├── README.md
├── project_report/
└── screenshots/
```
## ▶️ How to Run
### 1️⃣ Clone the GitHub Repository
```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO.git
cd YOUR_REPO
```
### 2️⃣ Install Dependencies
```bash
pip install -U vllm
```
### 3️⃣ Run vLLM Server on RunPod
```bash
python -m vllm.entrypoints.openai.api_server \
  --model microsoft/Phi-3-mini-4k-instruct \
  --host 0.0.0.0 \
  --port 8000
```
### 4️⃣ Wait for Server to Start
When the server is successfully running, you will see:
```bash
Application startup complete
```
### 5️⃣ Get API URL (RunPod)

RunPod will provide a public URL like:
```bash
https://xxxxx-8000.proxy.runpod.net
```
This URL is your LLM API endpoint.

### 6️⃣ Run Python Client (Chatbot)
Now use this URL inside your Python client:
```python
import requests
API_URL = "https://xxxxx-8000.proxy.runpod.net/v1/chat/completions"
messages = [
    {
        "role": "system",
        "content": "You are a helpful statistics tutor. Give only final answers clearly."
    }
]

while True:
    user_input = input("You: ")

    if user_input.lower() in ["exit", "quit"]:
        break

    messages.append({"role": "user", "content": user_input})

    response = requests.post(
        API_URL,
        json={
            "model": "microsoft/Phi-3-mini-4k-instruct",
            "messages": messages
        }
    )

    result = response.json()
    answer = result["choices"][0]["message"]["content"]

    print("AI:", answer)

    messages.append({"role": "assistant", "content": answer})
```

## 📈 Results

The final system successfully:
- Generated accurate and clean statistical explanations  
- Improved response quality compared to the initial RAG-based approach  
- Reduced noise caused by PDF extraction issues  
- Enabled real-time AI responses through a cloud API  
- Demonstrated stable chatbot behavior using vLLM deployment  

## 🎓 Academic Purpose

This project was developed as part of a Deep Learning and Large Language Model course.

The main objective was to understand:
- How large language models work in real applications  
- How prompt engineering can control model behavior  
- How to deploy LLMs using cloud GPU infrastructure  
- How client-server architecture works for AI systems  

## 🧠 System Classification
| Layer         | Role                      |
| ------------- | ------------------------- |
| Phi-3-mini    | Brain (LLM)               |
| vLLM          | Server (inference engine) |
| RunPod        | Cloud GPU hosting         |
| Python script | Client (chat interface)   |
| requests      | HTTP communication        |

## 👩‍💻 Author

- Maryam Tahir  
- MS Data Science Student 
- https://github.com/maryam27-byte/stats-AI-tutor-project