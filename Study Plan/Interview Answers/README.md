# Interview Answer Bank

> Master index. All answers in one place. No repeats — questions live in [[Interview/Self Interview/HR Questions]].

---

## Quick Navigation

| Question | Short Answer (Read Before Interview) |
|----------|-------------------------------------|
| Tell me about yourself | 3+ yrs Full Stack, Angular/Node/Python, AI automation, $200-400/day revenue project |
| Why leaving? | Growth ceiling after 3 years; want senior/lead role and bigger challenges |
| Salary expectation | ₹18–25 LPA (Mumbai), negotiate, always ask their budget first |
| Notice period | 2 months, can negotiate early relieving |
| Strength | Full-stack + AI, end-to-end ownership, ships to production |
| Weakness | Goes too deep on problems; timebox to 30 min now |
| 5-year goal | Senior/Lead Engineer, owning AI-integration decisions |
| Questions to ask | Team pain points, tech debt balance, 90-day success, growth path |

---

## Behavioral Answer Bank (STAR Format)

### Challenge Story — Translation System
- **S:** 500+ CSV files needed weekly translation; done manually
- **T:** Build automated, accurate pipeline
- **A:** HuggingFace MBart-50, batch processing, Flask API, GCP
- **R:** 95% accuracy, $200–400/day revenue, 500+ files/week

### Impact Story — Automation Savings
- **S:** 20+ hrs/week of manual data entry across workflows
- **T:** Reduce operational cost through automation
- **A:** Node.js + Python automation pipelines
- **R:** $75K/year cost reduction, 50% operational cost cut

### Technical Leadership — Auth System
- **S:** 8 enterprise apps with no consistent auth
- **T:** Standardize auth across applications
- **A:** JWT + Angular Auth Guards with RBAC
- **R:** 5,000+ users secured, security incidents: 12 → 0/month

### Conflict/Collaboration Story
- **S:** API format mismatch blocking frontend-backend integration
- **T:** Ship feature without delay
- **A:** Contract-first API spec, aligned both teams in one meeting
- **R:** On-time delivery, spec became team standard

### End-to-End Ownership — Umang Emails
- **S:** Wanted to prove solo full-stack deployment capability
- **T:** Build, deploy, maintain production app alone
- **A:** Angular + Node.js + Firebase + Gmail API, deployed on GCP
- **R:** Live at umang-emails.web.app; fully solo

---

## System Design Answers

### Design a File Translation Pipeline
1. Upload endpoint (Node.js / Flask)
2. Queue (Redis / SQS) for batch jobs
3. Worker: HuggingFace MBart-50 model (batch processing)
4. Result storage: S3 / GCP Storage
5. Status polling or webhook to notify completion

### Design a Scraping System at Scale
1. Scheduler (Cron / Airflow) triggers jobs
2. Proxy rotation (ScraperAPI / Bright Data)
3. Worker pool (Python + Selenium/BS4)
4. Dedup + storage (PostgreSQL + Redis cache)
5. Monitoring: error rate, extraction accuracy dashboards

---

## Salary Negotiation Quick Reference

| Scenario | Target | Floor (walk away) |
|----------|--------|-------------------|
| Mumbai, product company | ₹20–25 LPA | ₹16 LPA |
| Mumbai, startup | ₹18–22 LPA + ESOPs | ₹15 LPA |
| Remote (Indian company) | ₹22–28 LPA | ₹18 LPA |
| Remote (US/EU company) | $30–50/hr | $20/hr |

---

## Links
- [[Interview/Self Interview/HR Questions]] — full question + answer scripts
- [[Interview/Mock Interview WebPage/Resources]] — where to practice
- [[What To Say/Scenarios]] — negotiation scripts
- [[About Me/Profile]] — numbers and proof points
