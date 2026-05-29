# 🧑‍💼 AI CV Screener & HR Automation

> Monitors your Gmail for job applications, uses GPT-4o to score and evaluate each CV, automatically sends personalized responses (interview invite / under review / rejection), and logs everything to a candidates tracker in Google Sheets.

## What It Does

1. Monitors Gmail inbox for incoming job application emails
2. GPT-4o evaluates the candidate against job requirements
3. Scores them across 4 dimensions (0–100 total)
4. Routes to one of 3 decisions: **Advance / Hold / Reject**
5. Sends the appropriate personalized email automatically
6. Logs full candidate profile to Google Sheets tracker

## Scoring Dimensions

| Dimension | Weight | What It Measures |
|---|---|---|
| Technical Skills | 40pts | Relevant tools, languages, frameworks |
| Experience Relevance | 30pts | Years + domain match |
| Education Fit | 20pts | Degree level and field |
| Communication | 10pts | Email quality and clarity |

## Decision Routing

```
Score 80-100 → ✅ ADVANCE → Sends interview invitation email
Score 60-79  → ⏳ HOLD    → Sends "under review" email
Score < 60   → ❌ REJECT  → Sends polite rejection email
```

## Workflow Architecture

```
Gmail Trigger (monitors for application emails)
      │
      ▼
Fetch Full Email Content
      │
      ▼
GPT-4o: Evaluate CV
      │  Returns: name, skills, score, recommendation,
      │           strengths, concerns, interview questions
      ▼
Switch: Route by Decision
  ├── Advance → Send Interview Invitation Email
  ├── Hold    → Send Under Review Email
  └── Reject  → Send Polite Rejection Email
      │
      ▼
Google Sheets: Log Candidate Profile
```

## Google Sheets Output

| Field | Example |
|---|---|
| candidate_name | Riham Tarabay |
| years_experience | 2 |
| key_skills | Python, TensorFlow, RAG, FastAPI |
| overall_score | 87 |
| recommendation | Advance |
| interview_questions | "Walk me through your RAG pipeline..." |

## Setup Instructions

1. Import `cv_screener_hr_automation.json` into n8n
2. Connect **Gmail** via OAuth2 (use company email)
3. Connect **Google Sheets** via OAuth2
4. Update your job requirements in the GPT-4o system prompt
5. Update the Google Sheet ID in the "Log to Candidates Tracker" node
6. Activate — it now screens candidates 24/7 automatically

## What I Learned
- Building end-to-end HR automation with conditional routing
- Multi-dimensional scoring prompt design for consistent LLM output
- Switch nodes for decision-based workflow branching
- Automating professional email communication at scale

## Tech Stack
`n8n` · `OpenAI GPT-4o` · `Gmail API` · `Google Sheets API`
