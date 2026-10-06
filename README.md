# 📚 Chat With Your PDFs (n8n + Supabase + Gemini)

> Stop scrolling through 80-page PDFs. Just ask them a question. 🧠

Upload a PDF, ask anything in plain English, and get an answer pulled from the document itself. No hallucinated nonsense, no "as an AI I cannot..." Just your document, answering back.

Built with **n8n** (the workflow brain), **Supabase** (the memory), and **Google Gemini** (the language skills). No backend code needed. 🚀



![Workflow screenshot](./Workflow2.png)



---

## ✨ What it does

- 📄 **Ingests PDFs**: reads them, chops them into chunks, and stores them as vectors
- 🔎 **Searches by meaning**, not just keywords
- 💬 **Answers questions** using only what's inside your documents
- 🛟 **Has a fallback**, so if nothing relevant is found it says so instead of making things up

---

## 🧩 How it works

There are two flows living in one n8n workflow:

**1️⃣ Ingest flow (feeding the brain)**

```
Webhook → PDF Loader → Text Splitter → Gemini Embeddings → Supabase Vector Store → Done ✅
```

**2️⃣ Question flow (asking the brain)**

```
Webhook → Validate Question → Retriever (top-k) → Gemini Chat Model → Answer 🎯
```

In plain words: the PDF is split into small pieces, each piece becomes a list of numbers (an embedding), and Supabase stores them. When you ask a question, it finds the pieces closest in meaning and hands them to Gemini to write the answer.

---

## 🛠️ Tech stack

| Tool | Job |
|---|---|
| **n8n** | Runs the whole workflow |
| **Supabase (pgvector)** | Stores and searches the embeddings |
| **Google Gemini** | Embeddings + answer generation |
| **Webhooks** | Lets any app or page talk to it |

---

## 🚀 Run it yourself

**You'll need:** n8n (local or cloud), a free Supabase project, and a Gemini API key from [Google AI Studio](https://aistudio.google.com).

1. **Clone this repo**
   ```bash
   git clone https://github.com/YOUR-USERNAME/rag-knowledge-base-supabase-pdf-retriever.git
   ```
2. **Set up Supabase.** Enable the `vector` extension, create a documents table, and a match function. Make sure the vector size matches your embedding model. (Mismatched sizes = angry errors. Ask me how I know. 😅)
3. **Import the workflow.** In n8n: `⋯ menu → Import from file → RAG Knowledge Base using Supabase (PDF Retriever).json`
4. **Add your credentials.** Supabase and Gemini, in each node that needs them.
5. **Activate the workflow** and copy the Production URLs from both Webhook nodes.
6. **Send a PDF** to the ingest webhook, then **ask a question** to the question webhook. Done! 🎉

---

## 🧪 Try it

Ask your PDF things like:

- *"What is this document about?"*
- *"Summarize the key points."*
- *"What does it say about pricing?"*

---

## 😤 Things that broke along the way (so they don't break for you)

- **Vector size mismatch.** The embedding model's output size must match your table's `vector(N)` column.
- **Model overload (503).** Turn on *Retry On Fail* in the HTTP node settings.
- **Model names change.** If you get a 404, check Google's current model list.

---

## 🔐 Heads up

Never commit API keys. Keep them in n8n credentials or a `.env` file, and double-check the workflow JSON before you push.

---

## 🗺️ What's next

- [ ] Image support (ask questions about pictures too 🖼️)
- [ ] Simple web page to upload and chat
- [ ] Show source pages with each answer

---

## 🤝 Let's connect

Built by **YOUR NAME** while learning AI automation.

- 💼 LinkedIn: [your-link](https://linkedin.com/in/your-profile)
- 🐙 GitHub: [@your-username](https://github.com/your-username)

If this helped you, drop a ⭐. It makes my day.
