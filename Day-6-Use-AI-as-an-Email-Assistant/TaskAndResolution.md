# TaskAndResolution.md

# AI-Based Professional Email Rewriter using OpenAI API

---

# Project Overview

The Enterprise AI Automation Engineering division launched an initiative to automate written communication workflows using Artificial Intelligence.

The objective was to build a Python-based AI Email Assistant capable of transforming informal messages into polite, professional email communication using the OpenAI Chat Completion API.

---

# Task Objective

Develop a Python application named:

```text
email_assistant.py
```

The application should:

1. Initialize an OpenAI client
2. Read API credentials securely
3. Accept email text dynamically
4. Generate a professional rewrite prompt
5. Send the prompt to OpenAI Chat Completion API
6. Print the rewritten professional email

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

Changed the working directory to the project workspace where the AI email assistant application would be created and executed.

---

# Step 2 — Create Virtual Environment

## Command

```bash
python3 -m venv venv
```

---

# Explanation

Created an isolated Python virtual environment named:

```text
venv
```

---

# Why Virtual Environments Are Important

Benefits:

- Prevent dependency conflicts
- Isolate project packages
- Improve portability
- Avoid modifying system Python libraries

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

Activated the virtual environment so all Python packages install locally inside the project.

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

Installed the official OpenAI Python SDK along with all required dependencies.

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

Loaded API credentials into the terminal session.

Environment variables used:

```bash
OPENAI_API_KEY
OPENAI_API_BASE
```

---

# Common Mistake Encountered

## Incorrect Command

```bash
source /root/.bash_profilecd /root/openaiproject
```

---

# Error Produced

```text
bash: /root/.bash_profilecd: No such file or directory
```

---

# Root Cause

Two commands were accidentally combined into one line.

---

# Resolution

Executed commands separately:

```bash
source /root/.bash_profile
```

---

# Step 6 — Create email_assistant.py

## Command

```bash
vi /root/openaiproject/email_assistant.py
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

def rewrite_email(text: str) -> str:
    prompt = f"""
Rewrite the following email politely and professionally.

Email:
{text}

Return only the rewritten email.
"""

    response = client.chat.completions.create(
        model="openai/gpt-4.1-mini",
        messages=[
            {
                "role": "user",
                "content": prompt
            }
        ],
        max_tokens=60,
        temperature=0.1
    )

    return response.choices[0].message.content.strip()

# Input email text
text = "hey send me that report asap"

# Store response
response = rewrite_email(text)

# Print output
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

Used for accessing Linux environment variables.

## OpenAI

Imports the OpenAI client SDK.

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

# Why Environment Variables Matter

Advantages:

- Avoid hardcoded credentials
- Improve security posture
- Simplify CI/CD integration
- Enable easier secret rotation

---

# Define rewrite_email Function

```python
def rewrite_email(text: str) -> str:
```

---

# Explanation

Defines a reusable function that accepts raw email text dynamically.

---

# Prompt Engineering

```python
prompt = f"""
Rewrite the following email politely and professionally.
"""
```

---

# Explanation

Uses prompt engineering to instruct the AI model to rewrite informal communication professionally.

Benefits:

- Consistent formatting
- Better AI guidance
- Reusable architecture

---

# Send Request to OpenAI

```python
response = client.chat.completions.create(
```

---

# Explanation

Sends the generated prompt to the OpenAI Chat Completion API.

---

# Model Used

```python
model="openai/gpt-4.1-mini"
```

---

# Explanation

Uses the lightweight GPT-4.1-mini model optimized for structured text rewriting tasks.

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

Defines the AI conversation input.

| Field | Purpose |
|---|---|
| role | Defines sender role |
| content | Contains generated prompt |

---

# max_tokens

```python
max_tokens=60
```

---

# Explanation

Limits maximum response size.

Benefits:

- Cost optimization
- Faster response generation
- Prevents excessively long emails

---

# temperature

```python
temperature=0.1
```

---

# Explanation

Controls AI randomness.

| Value | Behavior |
|---|---|
| 0.0 | Deterministic |
| 0.1 | Stable professional output |
| 1.0 | Creative/random |

---

# Extract Response

```python
return response.choices[0].message.content.strip()
```

---

# Explanation

Extracts generated email text from the API response.

---

# Define Input Text

```python
text = "hey send me that report asap"
```

---

# Explanation

Stores the informal email text that will be rewritten professionally.

---

# Store AI Response

```python
response = rewrite_email(text)
```

---

# Explanation

Executes the email rewriting function and stores the generated response.

---

# Print Final Output

```python
print(response)
```

---

# Explanation

Displays the professional email on the terminal.

---

# Step 7 — Execute email_assistant.py

## Command

```bash
python3 /root/openaiproject/email_assistant.py
```

---

# Final Successful Output

```text
Dear [Recipient's Name],

Could you please send me the report at your earliest convenience?

Thank you very much.

Best regards,
[Your Name]
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
GPT-4.1-mini Model
        ↓
Professional Email Rewrite
        ↓
Terminal Output
```

---

# Enterprise Use Cases

## AI Communication Automation

- Professional email rewriting
- Executive communication enhancement
- Customer support automation

## AI Productivity Solutions

- Automated messaging
- Tone correction
- Internal communication optimization

## AI Writing Assistants

- HR communication
- Corporate messaging
- Helpdesk interactions

---

# Security Best Practices

| Practice | Purpose |
|---|---|
| Environment Variables | Secure credentials |
| Virtual Environments | Dependency isolation |
| Token Limits | Cost optimization |
| Prompt Constraints | Controlled output |

---

# Production Enhancement Ideas

## Suggested Improvements

- Web UI integration
- FastAPI REST service
- Multi-language rewriting
- Email templates
- Async processing
- Logging and monitoring
- Email sentiment analysis

---

# Scenario Based Interview Questions & Answers

# L1 — Junior Engineer Level

---

## Q1. Why use virtual environments in Python?

### Answer

Virtual environments isolate project dependencies and prevent conflicts between packages installed for different projects.

---

## Q2. Why store API keys in environment variables?

### Answer

Environment variables improve security by avoiding hardcoded credentials in source code repositories.

---

## Q3. What caused the .bash_profile error?

### Answer

Two shell commands were merged accidentally:

```bash
source /root/.bash_profilecd /root/openaiproject
```

which caused Bash to interpret it as a non-existent file path.

---

# L2 — Mid-Level Engineer

---

## Q4. Why use prompt engineering?

### Answer

Prompt engineering improves AI response quality by clearly defining expected behavior and formatting.

---

## Q5. Why use temperature=0.1?

### Answer

Low temperature reduces randomness and ensures stable, professional email formatting.

---

## Q6. Why limit max_tokens?

### Answer

max_tokens controls response size and helps optimize API costs and response latency.

---

# L3 — Senior Engineer Level

---

## Q7. How would you productionize this email assistant?

### Answer

Production improvements:

- FastAPI backend
- Docker containers
- Kubernetes deployment
- Retry mechanisms
- Monitoring integration
- Rate limiting

---

## Q8. How would you improve reliability?

### Answer

Add:

- Exception handling
- Timeout controls
- Retries
- Response validation
- Structured logging

---

## Q9. How would you optimize OpenAI API costs?

### Answer

Optimization techniques:

- Prompt minimization
- Smaller models
- Response caching
- Batch processing

---

# L4 — Architect Level

---

## Q10. Design an enterprise AI communication platform.

### Answer

## High-Level Architecture

```text
Frontend Portal
      ↓
API Gateway
      ↓
AI Orchestration Layer
      ↓
Prompt Management Service
      ↓
OpenAI Integration Layer
      ↓
Monitoring & Analytics
```

---

# Core Components

## API Gateway

- Authentication
- Rate limiting
- Request validation

## Prompt Service

- Template management
- Prompt versioning
- Validation

## AI Service Layer

- Multi-model routing
- Failover handling
- Response normalization

## Observability Layer

- Metrics
- Logs
- Distributed tracing

---

## Q11. How would you secure enterprise AI systems?

### Answer

Security controls:

- Secret vault integration
- TLS encryption
- RBAC policies
- Audit logging
- API gateway security

---

## Q12. How would you support multiple AI vendors?

### Answer

Use provider abstraction:

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

- Vendor independence
- Easier migration
- Failover support
- Cost optimization

---

# Key Learnings

- Prompt engineering significantly affects AI responses
- Environment variables improve operational security
- Virtual environments isolate dependencies
- Temperature tuning improves output consistency
- Token limits help optimize API usage

---

# Final Result

Successfully developed and executed a Python-based AI Email Assistant that:

- Uses OpenAI GPT-4.1-mini
- Rewrites informal text professionally
- Uses secure environment variables
- Demonstrates enterprise-grade AI integration practices
- Produces structured, polite, professional email responses

---
