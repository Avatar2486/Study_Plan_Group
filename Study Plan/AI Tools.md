# Using AI Tools to Build Apps

> How to use AI coding tools effectively as a Full Stack Developer.
> Goal: Ship faster, write better code, stay in control.

---

## Tools You Already Use (From Resume)
- **Claude Code** — CLI AI coding assistant
- **GitHub Copilot** — in-editor autocomplete
- **n8n** — automation workflows

---

## The AI Coding Toolkit

| Tool | Best For | Free? |
|------|----------|-------|
| **Claude Code** (Anthropic) | Full codebase tasks, multi-file edits, terminal | Paid |
| **GitHub Copilot** | In-editor autocomplete, chat | Paid (free for students) |
| **Cursor** | AI-native IDE, codebase chat | Free tier |
| **Windsurf** | Agentic coding, cascade mode | Free tier |
| **ChatGPT** | Quick code gen, debugging | Free/Paid |
| **v0.dev** (Vercel) | Generate React/Next.js UI components | Free |
| **Bolt.new** | Full-stack app scaffolding (Node + React) | Free tier |
| **Lovable** | UI/frontend generation | Free tier |
| **Replit AI** | Quick prototypes, deploy instantly | Free tier |

---

## Effective Prompting for Code

### Be Specific
**Bad:** "Write a Node.js server"
**Good:** "Write a Node.js Express server with JWT auth middleware, PostgreSQL connection pool using pg, and a `/api/users` GET route with role-based access (admin/user). Use ES modules."

### Provide Context
- Paste your existing code structure
- Mention your stack versions
- State what already exists vs what you need

### Iterative Approach
1. Generate scaffold → review → ask for changes
2. Don't accept first output blindly — test it
3. "What are the edge cases here?" after generation

---

## Building Apps with AI — Workflow

### Frontend (Angular/React)
1. **v0.dev** → generate component UI (React/Tailwind)
2. Copy to project → adapt to Angular if needed
3. Copilot for logic, event binding, services

### Backend (Node.js/Python)
1. **Claude Code** → "Add an endpoint that does X with these schemas"
2. Copilot for boilerplate (controllers, middleware)
3. Always review generated SQL queries — never trust blindly

### Database
1. Ask Claude/ChatGPT for schema design → review
2. "What indexes should I add for this query?" → validate with EXPLAIN ANALYZE
3. Generate migration files via Copilot

### Deployment
1. Ask Claude Code for Nginx config, Dockerfile
2. Use GitHub Copilot to write CI/CD pipeline YAML
3. Always review before applying to production

---

## n8n Automation — AI Integration Patterns

### Common Patterns You Can Build
| Pattern | Use Case |
|---------|----------|
| Webhook → OpenAI → Email | Auto-respond to form submissions |
| Gmail trigger → Gemini → Sheets | Invoice data extraction |
| Cron → Scraper → Slack | Daily job alert digest |
| HTTP Request → Claude API → DB | Batch content generation |

### n8n + LLM Tips
- Use "AI Agent" node for multi-step reasoning
- Store API keys in n8n credentials (never hardcode)
- Use "Split in Batches" for large datasets
- Add error handling node for LLM timeouts

---

## When NOT to Use AI for Code

- Security-critical code (auth, encryption) — review line by line
- Database migrations — test on staging first, never auto-run
- Infrastructure changes (Nginx, DNS, SSL) — manual review required
- Anything touching user data/PII

---

## Staying Sharp (Don't Lose Core Skills)

- Still write first drafts of algorithms yourself
- Understand every line AI generates before merging
- Use AI for boilerplate, not for architecture decisions
- Code review AI output like you'd review a junior dev's PR

---

## Links
- [[Study Plan/AI ML]] — go deeper into how models work
- [[Project Ideas/Ideas]] — ideas to build using these tools
- [[Study Plan.md]] — back to main study plan
