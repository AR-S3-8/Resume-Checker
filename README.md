#Resume Checker

An end-to-end AI-powered recruitment automation pipeline built with n8n.

Resume Checker automatically collects candidate data, processes resumes (PDF, DOCX, Image), performs AI-based screening, separates applicants into structured hiring stages, and supports multi-phase recruitment including interview scheduling and final acceptance.

🚀 Overview

Resume Checker is a multi-stage hiring automation system that enables companies to:

Collect candidate information via form

Store and organize all applicants

Extract and analyze resume content using AI

Automatically filter candidates based on defined criteria

Maintain separate applicant and accepted lists

Generate professional rejection messages

Prepare interview scheduling infrastructure

Support final human approval and acceptance

This system ensures structured, scalable, and auditable recruitment.

🏗 System Architecture

The workflow is built entirely in n8n and integrates with:

Google Drive

Google Sheets

Gmail

Google Calendar

OpenRouter

ConvertAPI (PDF/DOCX → TXT)

OCR.space (Image → Text)

🔁 End-to-End Hiring Flow
🟢 Stage 1 – Applicant Submission & Data Collection

When a candidate submits the form:

Data Collected

Full Name

Email

Age

Job Position

Phone Number

Resume File (PDF / DOCX / Image)

Automated Actions

Resume uploaded to Google Drive

Candidate data appended to Sheet #1 – All Applicants

Confirmation email sent

Resume file downloaded for processing

Text extracted from file

📌 Result:
The company maintains a complete database of all applicants.

📄 Resume Processing Engine

The workflow dynamically detects file type:

DOCX

→ Converted to text using ConvertAPI

PDF

→ Converted to text using ConvertAPI

Image (JPG/PNG)

→ Processed using OCR.space API

The extracted text is passed to the AI screening agent.

🧠 Stage 2 – AI Screening & Smart Filtering

An AI Agent (via OpenRouter) evaluates the resume.

Acceptance Criteria

A candidate must:

Mention experience with Python

Mention experience working with APIs

Be 30 years old or younger

All criteria must be satisfied.

The AI returns structured JSON:

{
  "accept": true
}


The workflow then merges:

Applicant info

AI result

And applies final conditional logic.

✅ Accepted Candidates (Round 1)

If:

AI result = true

Age ≤ 30

Then:

Candidate added to Sheet #2 – Accepted Candidates

Interview invitation email sent

Telegram notification (optional, enabled in workflow)

Infrastructure prepared for calendar scheduling

📌 The company now has two structured datasets:

All Applicants

Accepted Candidates (Round 1)

This ensures:

No data loss

Clear hiring stages

Auditability

HR analytics capability

❌ Rejected Candidates

If criteria are not met:

A second AI Agent generates:

A respectful rejection message

In Persian

Maximum 3 lines

Personalized with candidate name

Clearly stating missing qualifications

The message is automatically emailed to the candidate.

🔵 Stage 3 – Interview & Final Approval (Human-in-the-Loop)

The workflow includes prepared (currently disabled) nodes for:

Checking availability via Google Calendar

Finding free 15-minute slots

Creating interview events

Sending scheduling notifications

After in-person interviews:

The manager selects final candidates

Only remaining candidates receive final acceptance email

This ensures:

AI-assisted screening

Human final decision authority

🗂 Data Structure
Sheet 1 – All Applicants

Contains every submission:

Accepted

Rejected

Pending

Sheet 2 – Accepted (Round 1)

Contains only candidates who passed AI + age filter.

This separation provides structured hiring stages and reporting capability.

⚙️ Technical Workflow Breakdown
Core Nodes Used

Form Trigger

Switch (MIME type routing)

HTTP Request (ConvertAPI & OCR)

Extract From File

AI Agent (LLM Screening)

Code (JSON Parsing & Merging)

IF Condition Nodes

Google Sheets (Append operations)

Gmail (Notifications)

Google Drive (File storage)

AI Design

Two AI Agents:

Screening Agent
→ Returns strict JSON { "accept": boolean }

Rejection Generator
→ Produces human-like Persian rejection reason

Structured output parsing ensures reliability and prevents malformed responses.

🛡 Error Handling

Retry enabled on HTTP nodes

Fallback parsing for invalid JSON

Continue-on-error logic for safe merging

Structured response enforcement in AI node

📦 Deployment

The workflow can run on:

Self-hosted n8n (Docker recommended)

n8n Cloud

VPS

Local instance

Recommended production setup:

Dockerized n8n

Secured credentials storage

Environment variable management for API keys

🔐 Security Considerations

API keys stored in n8n credentials

No hardcoded secrets in workflow

File storage centralized in Drive

Structured output prevents AI injection artifacts

Email sender identity controlled via Gmail OAuth

📈 Business Value

Resume Checker transforms recruitment by:

Reducing manual screening time

Standardizing evaluation criteria

Providing scalable filtering

Maintaining structured hiring stages

Combining AI automation with human oversight

Supporting multilingual resume analysis (Persian supported)

🔮 Future Improvements

Automated interview scheduling activation

Scoring-based candidate ranking

Admin dashboard

ATS integration

Candidate feedback analytics

Bias monitoring layer

Resume skill extraction scoring model

📌 Why This Project Matters

Resume Checker is not just a resume filter.

It is a:

Multi-Stage Hiring Automation System

AI-Powered Screening Engine

Structured Recruitment Pipeline

Human-in-the-Loop Decision System

It demonstrates workflow orchestration, LLM integration, structured output enforcement, file processing automation, and real-world business logic implementation.

👨‍💻 Built With

n8n

OpenRouter LLM API

Google Workspace APIs

ConvertAPI

OCR.space

JavaScript (n8n Code nodes)

Python (OCR parsing)

📄 License

This project is intended for educational and portfolio purposes.
Commercial usage requires proper API licensing.