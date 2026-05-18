# Role-Based Interview Introductions

> Pick the version that matches the company/role. Speak for 60–75 seconds max.
> All versions are true — just different angles on the same resume.

---

## How to Know Which Version to Use

| Signal | Use Version |
|--------|------------|
| JD says "Backend Engineer / Node / Python / API" | → Backend Version |
| JD says "Frontend / Angular / React / UI" | → Frontend Version |
| Company is an AI startup / AI product | → AI Company Version |
| Normal product company, JD mentions AI as bonus | → AI Skills (Non-AI Company) |
| JD says "Full Stack" | → Mix Backend + 1 AI line |

---

## Version 1 — Backend-Focused

> Use when: role is Node.js, Python, API design, microservices, or backend engineer.

**Introduction:**
I'm Abhishek Dubey, a backend developer with 3+ years of experience at Boson Technology in Mumbai.

On the backend, I've built and owned production systems end-to-end — RESTful APIs on Node.js handling 10,000+ daily requests with 99.9% uptime, Python automation pipelines that reduced operational costs by $75,000 annually, and an invoice processing system that cut processing time by 70% using Gemini AI and AWS Lambda.

I work regularly with PostgreSQL, MongoDB, Redis, and I've deployed on AWS and GCP with Nginx load balancing across multiple instances. I've also integrated JWT authentication and RBAC across 8 enterprise applications securing 5,000+ user accounts.

I'm now looking for a backend role where I can work on larger-scale distributed systems and grow into a senior engineer.

---

### Backend — Common Follow-Up Questions

**Q: What's your experience with databases?**
> PostgreSQL is my primary — I've done query optimization, indexing, and written complex aggregation queries. Also used MongoDB (with aggregation pipelines in the Mgaf HR project) and MySQL. I understand the tradeoffs: PostgreSQL for relational consistency, MongoDB for flexible schemas at scale.

**Q: Have you worked with microservices?**
> Yes — I've built and maintained microservices on Node.js, deployed on AWS EC2 behind Nginx with load balancing across 4 instances. I've also used Redis for caching and session management between services, and WebSockets for real-time communication.

**Q: What's your experience with Python on the backend?**
> Heavy usage — Python is my go-to for data pipelines and automation. I've built a scraper that extracts 50,000+ product records daily, an invoice OCR pipeline using Gemini AI, and an ML translation system (HuggingFace MBart-50) that generates $200–400/day in revenue. I use Flask for APIs when Python is the right tool.

**Q: How do you handle API performance?**
> I've dealt with this at 10K+ requests/day. Key techniques I use: connection pooling, Redis caching for hot data, pagination, query indexing, and async processing for heavy jobs. I've also used AWS Lambda for scheduled/background tasks to offload the main server.

---

## Version 2 — Frontend-Focused

> Use when: role is Angular, React, UI Engineer, or frontend developer.

**Introduction:**
I'm Abhishek Dubey, a frontend developer with 3+ years of experience, primarily in Angular, at Boson Technology in Mumbai.

I've built multiple enterprise Angular applications — a multi-brand sales dashboard handling 10,000+ daily API requests, an AI-powered HR platform serving 250+ employees, and a real-time communication dashboard with WebSocket integration. I've done deep Angular work — NgRx state management, RxJS, lazy loading, and Angular Auth Guards for role-based access.

One of my biggest wins was optimizing an Angular app from 4.2s to 2.9s load time by implementing code splitting, lazy loading, and reducing bundle size from 3.2MB to 1.8MB — which improved user retention by 25%.

I also built and deployed my own full app — Umang Emails — solo, live at umang-emails.web.app.

I'm looking for a frontend or full-stack role where I can own UI architecture and performance.

---

### Frontend — Common Follow-Up Questions

**Q: How do you manage state in Angular?**
> I use NgRx for complex state — actions, reducers, selectors, effects. For simpler state I use services with BehaviorSubject. I choose based on complexity: NgRx adds boilerplate, but it's worth it when multiple components share the same async state.

**Q: How have you handled performance in Angular?**
> On the Extreme App dashboard: reduced bundle from 3.2MB → 1.8MB via lazy loading modules, tree shaking, and code splitting. Load time went from 4.2s → 2.9s. I also use OnPush change detection, trackBy in ngFor, and avoid unnecessary subscriptions by using async pipe + takeUntil patterns.

**Q: Have you worked with React?**
> Yes — I built the AI Product Listing Enhancement Tool in ReactJS. I'm comfortable with hooks, component architecture, and Context API. My primary is Angular, but I can pick up React projects without issue.

**Q: How do you handle API integration on the frontend?**
> I use Angular HttpClient with interceptors for auth headers and error handling. For loading states I use RxJS operators — switchMap for cancellable requests, combineLatest when multiple streams need to sync. I always handle error states in UI explicitly — not just console.log.

---

## Version 3 — AI Company (They Are an AI Product/Startup)

> Use when: company's core product is AI — AI agent, LLM product, ML platform, AI SaaS.

**Introduction:**
I'm Abhishek Dubey, a full stack developer with 3+ years of experience, with a strong focus on AI integration in production systems.

At Boson Technology I've built real AI-powered products — not just demos. A translation system using HuggingFace MBart-50 that processes 500+ files weekly and generates $200–400 in daily revenue. An invoice pipeline using Gemini AI that reduced processing time by 70%. An HR platform integrating ChatGPT API serving 250+ employees. And I run Ollama with Llama 3 locally for offline LLM workflows.

I work across the full AI integration stack — prompt engineering, API integration (OpenAI, Gemini, Claude), LangChain for orchestration, and I'm actively learning RAG and fine-tuning. I'm also comfortable building the frontend and backend around AI features — Angular for UI, Node.js/Python for APIs, AWS/GCP for deployment.

I'm excited about this role because I want to go deeper — building products where AI is the core, not just a feature.

---

### AI Company — Common Follow-Up Questions

**Q: Have you worked with LLM orchestration frameworks?**
> Yes — I've used LangChain for chaining LLM calls and managing context. I've integrated Ollama for local Llama 3 inference to avoid cloud dependency for privacy-sensitive data. I'm currently exploring LangGraph for multi-agent workflows and RAG patterns with vector databases.

**Q: What's your experience with prompt engineering?**
> Practical, production-tested. For the invoice extraction system, I designed prompts for Gemini to extract structured data (vendor, amount, date) from unstructured PDFs with 94% accuracy. For the HR system, I engineered prompts for goal generation and report summarization. I've learned that structured output prompts (JSON schema in the prompt) are far more reliable than free-form.

**Q: How do you handle LLM failures or hallucinations in production?**
> Validation layer — I always parse and validate LLM output before using it. For structured data I check required fields exist, types match, values are in expected range. For critical flows I have fallback paths (manual review queue). I also log all LLM inputs/outputs to catch patterns where the model fails.

**Q: Have you worked with vector databases or RAG?**
> I've studied RAG architecture — embed documents, store in vector DB (Pinecone/pgvector), retrieve relevant chunks, augment prompt. I haven't shipped a RAG system to production yet, but I built a prototype using LangChain + pgvector. It's the area I'm most actively learning right now.

**Q: Local LLMs — Ollama experience?**
> Yes, production use. I integrated Ollama with Llama 3 in the product data scraper pipeline for offline AI-assisted data parsing. The reason: privacy-sensitive manufacturer data couldn't go to OpenAI. I served the model locally, called it via REST, and it handled normalization tasks well. Latency is higher than cloud but predictable.

---

## Version 4 — AI Skills at a Non-AI Company

> Use when: company isn't an AI product but you want to highlight AI as a differentiator.

**Introduction:**
I'm Abhishek Dubey, a full stack developer with 3+ years at Boson Technology in Mumbai.

My core stack is Angular, Node.js, and Python — I've built enterprise applications, REST API infrastructure at 10,000+ daily requests, and handled cloud deployments on AWS and GCP. What I've also brought to my current role is AI integration — I identified where AI could cut real costs and built those solutions. A Gmail-to-S3 invoice pipeline using Gemini AI reduced processing time by 70%. An HuggingFace-based translation system now generates $200–400/day in revenue. An n8n CRM automation reduced support response time by 70%.

I'm not just someone who can call AI APIs — I understand where AI actually adds value and where it doesn't. I'm looking for a role where strong engineering fundamentals matter, and where I can bring that AI integration lens to the team.

---

### Non-AI Company — If They Ask About AI

**Q: "We don't really use AI — is that okay?"**
> Absolutely — I'm primarily a software engineer. AI is a tool I've used where it solved real problems, not something I need in every project. What I'm looking for is good engineering challenges — scale, reliability, clean architecture. The AI work is just part of my experience.

**Q: "What AI tools do you use day to day?"**
> For coding: Claude Code and GitHub Copilot — they speed up boilerplate. For anything going into production, I review every line. For automation ideas: I think in terms of n8n workflows when I see repetitive processes. But I don't over-engineer — if a simple script works, I write that.

---

## Quick Cheat Sheet

```
Backend role      → Start with APIs, databases, Python automation
Frontend role     → Start with Angular, performance wins, Umang Emails
AI company        → Start with AI products in production, then full stack
Non-AI company    → Start with full stack fundamentals, mention AI briefly at end
```

---

## Links
- [[Interview/Self Interview/HR Questions]] — full HR Q&A (salary, why leaving, etc.)
- [[Study Plan/Interview Answers/README]] — STAR stories and answer bank
- [[About Me/Profile]] — numbers to back up every claim
- [[Comm Improvemts/Communication Tips]] — STAR method, speaking pace
