<h1 align="center"> Retrieval-Augmented Generation with Gradio and Groq API Key</h1>
<p align="center"> Natural Language Processing Project</p>

<div align="center">

<img src="https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54">

</div>

### Name : Arifian Saputra
### Tech Stack : Python, Gradio, LangChain, HuggingFace Embedding, FAISS vector store

---

### 1. Analysis about how the project works
- TODO

Proyek ini merupakan implementasi dari Retrieval-Augmented Generation (RAG) menggunakan pipeline:
- Upload dokumen PDF
- Dokumen di-split menjadi chunk teks
- Setiap chunk dikonversi menjadi vector embeddings menggunakan HuggingFaceEmbeddings (all-MiniLM-L6-v2)
- Embeddings disimpan dalam FAISS Vector Store
- Saat pengguna bertanya, sistem menggunakan vector store untuk melakukan semantic search
- Top-N dokumen hasil pencarian diberikan ke LLM (Groq model) sebagai context untuk menjawab pertanyaan



### 2. Analysis about how different every model works on Retrieval-Augmented Generation

```python
def get_llm():
    return ChatGroq(
        groq_api_key=GROQ_API_KEY,
        model_name="llama-3.3-70b-versatile", # Change the model in the code
        temperature=0.2
    )
```
- Model used : ```[llama-3.3-70b-versatile, deepseek-r1-distill-llama-70b, gemma2-9b-it]```

2.1 Analysis on ```llama-3.3-70b-versatile``` : 
- Akurat dan lengkap dalam memahami konteks dokumen.
- Respons cukup cepat.
- Bahasa formal dan koheren.
- Kadang memberi jawaban terlalu panjang (verbose).
- Lebih berat dibanding model kecil.

2.2 Analysis on ```deepseek-r1-distill-llama-70b``` : 
- Distilled model, lebih cepat dibanding LLaMA-3 full.
- Respons masih cukup akurat dan padat.
- Lebih efisien untuk real-time use.
- Kurang detail pada konteks yang panjang.
- Sering menjawab dengan ringkasan yang terlalu pendek.


2.3 Analysis on ```gemma2-9b-it``` : 
- Ringan dan cepat, ideal untuk sistem dengan resource terbatas.
- Gaya penulisan instruktif (karena fine-tuned untuk instruction).
- Cenderung kurang akurat pada dokumen panjang atau kompleks.
- Terbatas dalam reasoning atau jawaban multi-paragraf.



### 3. Analysis about how temperature works

```python
def get_llm():
    return ChatGroq(
        groq_api_key=GROQ_API_KEY,
        model_name="llama-3.3-70b-versatile",
        temperature=0.2 # Change the temperature value here and analzye
    )
```

3.1 Analysis on higher temperature 
- temperature tinggi → lebih banyak randomness dalam output → model lebih eksploratif dan kreatif.
- Jawaban bisa lebih bervariasi, namun kadang tidak konsisten dengan sumber dokumen.
- Meningkatkan kemungkinan halusinasi (model menjawab dengan informasi yang tidak ada di PDF).
- Cocok untuk pertanyaan yang terbuka atau interpretatif, bukan faktual.
- Kurang dapat dipercaya untuk use-case faktual.
- Tidak ideal untuk use-case legal, akademik, atau medis berbasis sumber.



3.2 Analysis on lower temperature
- temperature rendah → output lebih deterministik dan fokus pada jawaban paling mungkin.
- Cocok untuk sistem dokumen QA berbasis fakta seperti ini.
- Jawaban lebih konsisten, dan lebih mungkin berasal dari isi dokumen.
- Mengurangi risiko halusinasi.
- Tidak terlalu kreatif, tidak cocok untuk brainstorming.

### 4. How to run the project

- Clone this repository with : 

```git
git clone https://github.com/arifian853/RAG_with_GroqAPI.git
```

- Copy the ```.env.example``` file and rename it to ```.env```

```
GROQ_API_KEY=your-groq-api-key
```

- Fill the ```GROQ_API_KEY``` with your Groq API Key, find it here : https://console.groq.com/keys

- TODO
- TODO
- TODO
- TODO
- TODO
- TODO
- TODO
