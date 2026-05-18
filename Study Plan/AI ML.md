# AI / ML Learning Path

> For someone who already uses OpenAI/Gemini/Claude APIs and wants to go deeper.
> Goal: Go from "I call AI APIs" → "I understand and fine-tune models"

---

## Where You Are Now (From Resume)
- OpenAI, Gemini, Claude API — proficient
- HuggingFace Transformers — used MBart-50 in production
- LangChain — familiar
- Ollama + Llama 3 — used for local inference
- n8n automation — proficient
- Prompt Engineering — working knowledge

---

## Phase 1 — Foundations (2–4 weeks)

### Python for ML (if rusty)
- NumPy, Pandas, Matplotlib basics
- Resource: [Python for Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/) (free)

### ML Fundamentals
- Linear regression, classification, overfitting, train/test split
- Resource: [fast.ai — Practical Deep Learning](https://course.fast.ai/) (free, hands-on)
- Resource: [Google ML Crash Course](https://developers.google.com/machine-learning/crash-course) (free)

### Key Concepts to Know
- [ ] Supervised vs unsupervised learning
- [ ] Loss functions, gradient descent
- [ ] Overfitting, regularization, cross-validation
- [ ] Feature engineering basics

---

## Phase 2 — Deep Learning & NLP (4–6 weeks)

### Deep Learning
- Neural networks, CNNs, RNNs
- Resource: [deeplearning.ai — Deep Learning Specialization](https://www.coursera.org/specializations/deep-learning) (Coursera, audit free)

### NLP (Most Relevant for You)
- Tokenization, embeddings, attention mechanism
- Transformers architecture (the "T" in GPT/BERT)
- Resource: [HuggingFace NLP Course](https://huggingface.co/learn/nlp-course) (free)

### Key Skills to Build
- [ ] Fine-tune a pre-trained model on HuggingFace
- [ ] Build a text classifier with BERT
- [ ] Use sentence-transformers for semantic search

---

## Phase 3 — LLM Engineering (Practical, 4–6 weeks)

This is where your current skills connect to deeper knowledge.

### RAG (Retrieval-Augmented Generation)
- Vector databases: Pinecone, Weaviate, pgvector
- Embed documents → store → retrieve → augment prompt
- Resource: [LangChain RAG Tutorial](https://python.langchain.com/docs/tutorials/rag/)

### Fine-Tuning LLMs
- LoRA / QLoRA — fine-tune large models with less compute
- Use HuggingFace PEFT library
- Resource: [HuggingFace Fine-tuning Guide](https://huggingface.co/docs/transformers/training)

### LLM Agents
- Tool calling, function calling
- Multi-agent systems (LangGraph, AutoGen)
- Resource: [LangGraph Docs](https://langchain-ai.github.io/langgraph/)

### Key Projects to Build
- [ ] RAG chatbot over your own documents
- [ ] Fine-tune Llama 3 on custom dataset (via Ollama)
- [ ] Multi-tool agent (search + code execution + memory)

---

## Phase 4 — MLOps (Optional but Valuable)

- Model deployment: FastAPI + Docker + AWS Lambda
- Model monitoring: track drift, accuracy over time
- Tools: MLflow, Weights & Biases, HuggingFace Hub

---

## Tools Reference

| Tool | Use Case | Link |
|------|----------|------|
| HuggingFace | Models, datasets, fine-tuning | [huggingface.co](https://huggingface.co) |
| Ollama | Run LLMs locally | [ollama.com](https://ollama.com) |
| LangChain | LLM app framework | [langchain.com](https://langchain.com) |
| LangGraph | Multi-agent workflows | [langchain-ai.github.io/langgraph](https://langchain-ai.github.io/langgraph) |
| Pinecone | Vector database | [pinecone.io](https://www.pinecone.io) |
| fast.ai | Practical DL course | [fast.ai](https://fast.ai) |
| Weights & Biases | Experiment tracking | [wandb.ai](https://wandb.ai) |

---

## Links
- [[Study Plan/AI Tools]] — using AI tools to build apps faster
- [[Project Ideas/Ideas]] — project ideas that use AI/ML
- [[Study Plan.md]] — back to main study plan
