# TaskAndResolution.md

# AI-Based Resume Keyword Extractor using OpenAI API

---

# Project Overview

The Enterprise AI Innovation Engineering team initiated a smart Resume Analyzer project designed to automate resume screening and keyword extraction using Artificial Intelligence.

The objective was to develop a Python-based AI utility capable of extracting exactly five job-relevant keywords from a resume paragraph using the OpenAI Chat Completion API.

This automation can significantly improve HR screening efficiency, ATS optimization, and intelligent candidate matching.

---

# Task Objective

Develop a Python application named:

```text
resume_extractor.py
```

The application should:

1. Initialize an OpenAI client
2. Load API credentials securely
3. Accept resume text dynamically
4. Generate an AI prompt for keyword extraction
5. Extract exactly five comma-separated keywords
6. Print the extracted keywords

---

# Environment Details

| Component | Value |
|---|---|
| Project Directory | `/root/openaiproject` |
| Python Version | Python 3.12 |
| Virtual Environment | `venv` |
| SDK Used | OpenAI Python SDK |
| AI Model | `openai/gpt-4.1-mini` |

---

# Step 1 — Navigate to Project Directory

## Command

```bash
cd /root/openaiproject
```

---

# Explanation

Changed the current working directory to the project workspace where the AI keyword extraction module would be developed.

---

# Step 2 — Create Virtual Environment

## Command

```bash
python3 -m venv venv
```

---

# Explanation

Created a Python virtual environment named:

```text
venv
```

---

# Why Virtual Environments Are Important

Advantages:

- Dependency isolation
- Prevent package conflicts
- Cleaner deployments
- Easier troubleshooting

---

# Step 3 — Activate Virtual Environment

## Command

```bash
source venv/bin/activate
```

---

# Expected Output

```bash
(venv) automation-engineer@workspace:~/openaiproject$
```

---

# Explanation

Activated the Python virtual environment for isolated package management.

---

# Step 4 — Install OpenAI SDK

## Command

```bash
pip install openai
```

---

# Output

```bash
Successfully installed openai-2.38.0
```

---

# Explanation

Installed the OpenAI Python SDK and all required dependencies.

Installed libraries included:

- openai
- httpx
- pydantic
- tqdm
- anyio

---

# Step 5 — Load Environment Variables

## Command

```bash
source /root/.bash_profile
```

---

# Explanation

Loaded OpenAI API credentials into the current shell session.

Environment variables used:

```bash
OPENAI_API_KEY
OPENAI_API_BASE
```

---

# Initial Mistakes Encountered

Several task instructions were accidentally pasted directly into the shell.

---

# Example Incorrect Inputs

```bash
The datacenter AI Innovation Team...
```

---

# Resulting Errors

```text
bash: The: command not found
bash: You: command not found
bash: syntax error near unexpected token `text:'
```

---

# Root Cause

Task instructions were executed as shell commands instead of being followed manually.

---

# Resolution

Returned to the correct workflow:

1. Navigate to project directory
2. Create virtual environment
3. Install dependencies
4. Create Python file
5. Execute script properly

---

# Step 6 — Create resume_extractor.py

## Command

```bash
vi /root/openaiproject/resume_extractor.py
```

---

# Final Working Python Code

```python
import os
from openai import OpenAI

# Initialize OpenAI client
client = OpenAI(
    api_key=os.environ.get("OPENAI_API_KEY"),
    base_url=os.environ.get("OPENAI_API_BASE")
)

def extract_keywords(text: str) -> str:
    prompt = f"""
Extract exactly 5 job-relevant keywords from the following resume text.

Return ONLY 5 comma-separated keywords.

Resume:
{text}
"""

    response = client.chat.completions.create(
        model="openai/gpt-4.1-mini",
        messages=[
            {
                "role": "user",
                "content": prompt
            }
        ],
        max_tokens=40,
        temperature=0
    )

    return response.choices[0].message.content.strip()

# Resume text
text = """
Experienced DevOps engineer skilled in Python, Kubernetes, Docker, CI/CD pipelines, and cloud automation.
"""

# Store response
response = extract_keywords(text)

# Print extracted keywords
print(response)
```

---

# Code Explanation

---

# Import Required Modules

```python
import os
from openai import OpenAI
```

---

# Explanation

## os

Used to access environment variables.

## OpenAI

Imports the OpenAI Python SDK client.

---

# Initialize OpenAI Client

```python
client = OpenAI(
    api_key=os.environ.get("OPENAI_API_KEY"),
    base_url=os.environ.get("OPENAI_API_BASE")
)
```

---

# Explanation

Creates an authenticated OpenAI API client using environment variables.

---

# Why Environment Variables Are Important

Advantages:

- Secure credential handling
- Avoid hardcoded secrets
- Simplified CI/CD integration
- Easier key rotation

---

# Define extract_keywords Function

```python
def extract_keywords(text: str) -> str:
```

---

# Explanation

Defines a reusable function that dynamically accepts resume text.

---

# Prompt Engineering

```python
prompt = f"""
Extract exactly 5 job-relevant keywords...
"""
```

---

# Explanation

Uses prompt engineering to precisely instruct the AI model.

The prompt explicitly requests:

- Exactly 5 keywords
- Comma-separated values
- Job-relevant technical skills

---

# Send Request to OpenAI

```python
response = client.chat.completions.create(
```

---

# Explanation

Calls the OpenAI Chat Completion API.

---

# Model Used

```python
model="openai/gpt-4.1-mini"
```

---

# Explanation

Uses GPT-4.1-mini for lightweight keyword extraction tasks.

---

# messages Parameter

```python
messages=[
    {
        "role": "user",
        "content": prompt
    }
]
```

---

# Explanation

Defines the AI conversation request.

| Field | Purpose |
|---|---|
| role | Identifies message sender |
| content | Contains generated prompt |

---

# max_tokens

```python
max_tokens=40
```

---

# Explanation

Restricts maximum response size.

Benefits:

- Cost optimization
- Faster execution
- Prevents verbose responses

---

# temperature

```python
temperature=0
```

---

# Explanation

Controls AI randomness.

| Value | Behavior |
|---|---|
| 0 | Fully deterministic |
| 0.5 | Balanced |
| 1 | Highly creative |

Using `0` ensures consistent keyword extraction.

---

# Extract Response

```python
return response.choices[0].message.content.strip()
```

---

# Explanation

Extracts and cleans the AI-generated keyword response.

---

# Define Resume Text

```python
text = """
Experienced DevOps engineer...
"""
```

---

# Explanation

Stores the resume paragraph used for AI keyword extraction.

---

# Store Response

```python
response = extract_keywords(text)
```

---

# Explanation

Executes the keyword extraction function and stores the result.

---

# Print Final Output

```python
print(response)
```

---

# Explanation

Displays the extracted keywords on the terminal.

---

# Step 7 — Execute resume_extractor.py

## Command

```bash
python3 /root/openaiproject/resume_extractor.py
```

---

# Final Successful Output

```text
DevOps, Python, Kubernetes, Docker, CI/CD
```

---

# AI Workflow Architecture

```text
Python Application
        ↓
Prompt Construction
        ↓
OpenAI Chat Completion API
        ↓
GPT-4.1-mini
        ↓
Keyword Extraction
        ↓
Console Output
```

---

# Enterprise Use Cases

## ATS Optimization

- Resume scoring
- Candidate filtering
- Keyword analysis

## HR Automation

- Skill extraction
- Resume classification
- Automated ranking

## AI Talent Intelligence

- Technical skill mapping
- Workforce analytics
- Hiring recommendations

---

# Security Best Practices

| Practice | Purpose |
|---|---|
| Environment Variables | Secure API credentials |
| Virtual Environments | Dependency isolation |
| Token Limits | Cost optimization |
| Prompt Constraints | Controlled AI output |

---

# Production Enhancement Ideas

## Suggested Improvements

- Web dashboard
- Resume upload support
- PDF parsing
- Multi-language extraction
- Batch resume analysis
- Database integration
- Async processing

---

# Scenario Based Interview Questions & Answers

# L1 — Junior Engineer Level

---

## Q1. Why use virtual environments in Python?

### Answer

Virtual environments isolate dependencies and prevent conflicts between multiple Python projects.

---

## Q2. Why use environment variables for API keys?

### Answer

Environment variables protect secrets by avoiding hardcoded credentials inside source code.

---

## Q3. Why did the shell show “command not found” errors?

### Answer

Task instructions were accidentally pasted directly into the terminal instead of being followed manually.

Example:

```bash
The datacenter AI Innovation Team...
```

Bash interpreted it as a shell command.

---

# L2 — Mid-Level Engineer

---

## Q4. Why was temperature set to 0?

### Answer

Temperature `0` ensures deterministic and consistent AI responses, which is important for structured keyword extraction.

---

## Q5. Why explicitly request exactly five keywords?

### Answer

AI models may otherwise return inconsistent numbers of keywords. Prompt constraints improve output reliability.

---

## Q6. Why use prompt engineering?

### Answer

Prompt engineering helps guide the AI model toward structured, predictable outputs.

---

# L3 — Senior Engineer Level

---

## Q7. How would you productionize this resume analyzer?

### Answer

Production improvements:

- FastAPI backend
- Docker deployment
- Kubernetes orchestration
- PDF parsing integration
- Resume database indexing
- Async request handling

---

## Q8. How would you improve reliability?

### Answer

Add:

- Retry mechanisms
- Exception handling
- Timeouts
- Structured logging
- Output validation

---

## Q9. How would you optimize OpenAI API costs?

### Answer

Optimization strategies:

- Token reduction
- Response caching
- Smaller AI models
- Batch processing

---

# L4 — Architect Level

---

## Q10. Design an enterprise AI resume screening platform.

### Answer

## High-Level Architecture

```text
Resume Upload Portal
         ↓
API Gateway
         ↓
AI Orchestration Layer
         ↓
Prompt Management Service
         ↓
OpenAI Integration Layer
         ↓
Resume Analytics Engine
         ↓
HR Dashboard
```

---

# Core Components

## API Gateway

- Authentication
- Rate limiting
- Traffic control

## Prompt Layer

- Prompt templates
- Validation
- Version management

## AI Layer

- Multi-model routing
- Response normalization
- Retry handling

## Analytics Layer

- Skill scoring
- Resume ranking
- Candidate insights

---

## Q11. How would you secure enterprise AI integrations?

### Answer

Security controls:

- Vault-based secret management
- TLS encryption
- RBAC policies
- Audit logging
- API gateway security

---

## Q12. How would you support multiple AI providers?

### Answer

Use abstraction architecture:

```text
Application
     ↓
AI Adapter Layer
 ├── OpenAI
 ├── Claude
 ├── Gemini
 └── Internal Models
```

Benefits:

- Vendor flexibility
- Failover capability
- Cost optimization
- Easier migrations

---

# Key Learnings

- Prompt engineering strongly affects AI output
- Environment variables improve operational security
- Virtual environments isolate dependencies
- Temperature settings affect response consistency
- Structured prompts improve deterministic outputs

---

# Final Result

Successfully developed and executed a Python-based AI Resume Keyword Extractor that:

- Uses OpenAI GPT-4.1-mini
- Dynamically extracts exactly five job-relevant keywords
- Uses secure environment variables
- Demonstrates enterprise AI integration best practices
- Produces structured, deterministic AI-generated outputs

---
