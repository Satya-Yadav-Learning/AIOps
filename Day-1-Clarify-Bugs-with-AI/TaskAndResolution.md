# TaskAndResolution.md

# AI Bug Description Clarifier using OpenAI API

## Project Overview

The AI Engineering team required a Python-based utility that converts informal developer-reported bugs into professional and structured issue summaries using the OpenAI Chat Completion API.

The goal of this implementation was to:

- Improve bug clarity
- Standardize issue descriptions
- Enhance reproducibility of bugs
- Reduce ambiguity in developer communication

---

# Objective

Develop a Python application named `bug_clarifier.py` that:

1. Initializes the OpenAI client using environment variables
2. Dynamically accepts raw bug descriptions
3. Sends prompts to the OpenAI Chat Completion API
4. Returns a professional bug summary
5. Prints the AI-generated clarification to the console

---

# Environment Details

| Component | Value |
|---|---|
| Workspace Directory | `/root/ai_project` |
| Python Version | Python 3.12 |
| Virtual Environment | `venv` |
| OpenAI SDK | openai-2.36.0 |
| Model Used | `openai/gpt-4.1-mini` |

---

# Step 1: Navigate to Project Directory

## Command

```bash
cd /root/ai_project
```

## Explanation

Changed the working directory to the project workspace where the Python application would be created.

---

# Step 2: Create Python Virtual Environment

## Command

```bash
python3 -m venv venv
```

## Explanation

A dedicated Python virtual environment was created to isolate project dependencies from the system-wide Python installation.

This helps in:

- Dependency management
- Version consistency
- Environment isolation
- Clean deployments

---

# Step 3: Activate Virtual Environment

## Command

```bash
source venv/bin/activate
```

## Expected Output

```bash
(ai-env) user@workspace:~/ai_project$
```

## Explanation

Activated the virtual environment so that all Python packages install locally within the project.

---

# Step 4: Install OpenAI Python SDK

## Command

```bash
pip install openai
```

## Output

```bash
Successfully installed openai-2.36.0
```

## Explanation

Installed the official OpenAI Python SDK required for interacting with the Chat Completion API.

Installed dependencies included:

- httpx
- pydantic
- anyio
- tqdm
- typing-extensions

---

# Step 5: Verify Environment Variables

## Command

```bash
cat /root/.bash_profile
```

## Output

```bash
export OPENAI_API_BASE=https://api-gateway.internal/v1
export OPENAI_API_KEY=***************
```

## Explanation

Verified that API credentials were already available as environment variables.

Important observation:

The available variables were:

- `OPENAI_API_KEY`
- `OPENAI_API_BASE`

Initial failures occurred because incorrect variable names were used in the script.

---

# Step 6: Create Python Application

## Command

```bash
vi bug_clarifier.py
```

---

# Final Python Code

```python
import os
from openai import OpenAI

# Initialize OpenAI client using environment variables
client = OpenAI(
    api_key=os.environ.get("OPENAI_API_KEY"),
    base_url=os.environ.get("OPENAI_API_BASE")
)

def clarify_bug(description: str) -> str:
    prompt = f"""
Rewrite the following informal bug report into a clear, structured, and professional issue summary.

Bug Report:
{description}

Return only the clarified bug summary.
"""

    completion = client.chat.completions.create(
        model="openai/gpt-4.1-mini",
        messages=[
            {
                "role": "user",
                "content": prompt
            }
        ],
        max_tokens=100,
        temperature=0.0
    )

    return completion.choices[0].message.content.strip()

# Input bug report
bug_description = "App keeps crashing when I click save."

# Store AI response
response = clarify_bug(bug_description)

# Print clarified bug summary
print(response)
```

---

# Step 7: Source Environment Variables

## Command

```bash
source /root/.bash_profile
```

## Explanation

Loaded environment variables into the active shell session so Python could access:

- `OPENAI_API_KEY`
- `OPENAI_API_BASE`

---

# Step 8: Execute the Python Script

## Command

```bash
python3 /root/ai_project/bug_clarifier.py
```

## Final Output

```text
The application crashes consistently whenever the "Save" button is clicked.
```

---

# Issue Encountered During Implementation

## Problem 1: Syntax Error

### Error

```python
print(response)from openai import OpenAI
```

### Root Cause

An accidental string append caused invalid Python syntax.

### Resolution

Removed the unintended text and corrected the final print statement.

Correct line:

```python
print(response)
```

---

# Problem 2: Authentication Failure

## Error

```text
openai.AuthenticationError: Error code: 401
Incorrect API key provided
```

---

# Root Cause Analysis

The application attempted to load incorrect environment variables:

Incorrect:

```python
os.environ.get("API_KEY")
os.environ.get("BASE_URL")
```

Available variables:

```bash
OPENAI_API_KEY
OPENAI_API_BASE
```

---

# Final Resolution

Updated the code to:

```python
api_key=os.environ.get("OPENAI_API_KEY")
base_url=os.environ.get("OPENAI_API_BASE")
```

After correction, the API call executed successfully.

---

# OpenAI API Parameters Used

| Parameter | Value |
|---|---|
| model | openai/gpt-4.1-mini |
| max_tokens | 100 |
| temperature | 0.0 |
| messages | user prompt |

---

# Why temperature=0.0 Was Used

Using `temperature=0.0` ensures:

- Deterministic responses
- Consistent bug summaries
- Reduced randomness
- Stable enterprise outputs

Ideal for operational tooling and ticket generation systems.

---

# Architecture Flow

```text
Developer Bug Report
        ↓
Prompt Construction
        ↓
OpenAI Chat Completion API
        ↓
AI Clarified Summary
        ↓
Console Output
```

---

# Real-World Enterprise Use Cases

## DevOps

- Incident normalization
- Alert enrichment
- Ticket quality improvement

## QA Automation

- Structured bug generation
- Reproducible issue formatting

## AI Operations

- Automated ticket enhancement
- AI-assisted triaging

## Platform Engineering

- Intelligent observability workflows
- AI-powered incident management

---

# Security Best Practices

## Recommended Practices

- Never hardcode API keys
- Use environment variables
- Restrict model access
- Rotate credentials regularly
- Use isolated virtual environments

---

# Performance Considerations

| Area | Optimization |
|---|---|
| API Calls | Reuse client object |
| Token Usage | Keep prompts concise |
| Reliability | Add retry logic |
| Scalability | Async API execution |
| Security | Secrets management |

---

# Scenario Based Interview Questions & Answers

# L1 — Junior Engineer Level

---

## Q1. Why do we use virtual environments in Python?

### Answer

Virtual environments isolate project dependencies from the system Python installation.

Benefits include:

- Preventing package conflicts
- Maintaining version consistency
- Safer dependency upgrades
- Easier deployments

Example:

```bash
python3 -m venv venv
source venv/bin/activate
```

---

## Q2. Why were environment variables used for API credentials?

### Answer

Environment variables improve security by avoiding hardcoded secrets inside source code.

Advantages:

- Secure credential management
- Easier CI/CD integration
- Simplified secret rotation
- Better compliance

---

## Q3. What caused the 401 Authentication Error?

### Answer

The script used incorrect environment variable names.

Incorrect:

```python
API_KEY
BASE_URL
```

Correct:

```python
OPENAI_API_KEY
OPENAI_API_BASE
```

---

# L2 — Mid-Level Engineer

---

## Q4. Why was temperature set to 0.0?

### Answer

Temperature controls randomness in AI responses.

Using `0.0` ensures:

- Consistent responses
- Deterministic outputs
- Stable ticket formatting

This is important for operational tooling.

---

## Q5. How would you improve this application?

### Answer

Potential improvements:

- Add logging
- Add retry handling
- Add timeout controls
- Validate input descriptions
- Add async processing
- Store results in databases

---

## Q6. Why use a reusable OpenAI client object?

### Answer

Benefits:

- Better connection reuse
- Lower overhead
- Cleaner code structure
- Easier scalability

---

# L3 — Senior Engineer

---

## Q7. How would you productionize this solution?

### Answer

Production improvements:

- REST API wrapper using FastAPI
- Centralized logging
- Rate-limit handling
- Authentication middleware
- Monitoring integration
- Containerization with Docker
- CI/CD pipelines

---

## Q8. How would you reduce API cost?

### Answer

Strategies:

- Prompt optimization
- Response caching
- Batch processing
- Token minimization
- Use smaller models when possible

---

## Q9. How would you implement observability?

### Answer

Integrations:

- Metrics via Prometheus
- Logs via Loki
- Tracing via OpenTelemetry
- Dashboards via Grafana

Track:

- API latency
- Token consumption
- Failure rates
- Retry counts

---

# L4 — Architect Level

---

## Q10. Design an enterprise AI bug clarification platform.

### Answer

## Proposed Architecture

```text
Developer Portal
       ↓
API Gateway
       ↓
AI Clarification Service
       ↓
Prompt Orchestration Layer
       ↓
LLM Provider
       ↓
Incident/Ticketing Systems
```

---

## Key Components

### API Gateway

- Authentication
- Rate limiting
- Traffic control

### Prompt Layer

- Dynamic prompt templates
- Context enrichment
- Validation

### AI Service

- Multi-model support
- Retry mechanisms
- Cost optimization

### Storage Layer

- Prompt history
- Response caching
- Audit trails

### Observability

- Metrics
- Logging
- Tracing

---

## Q11. How would you secure enterprise AI integrations?

### Answer

Security controls:

- Vault-based secret management
- TLS encryption
- Role-based access
- Request auditing
- Token rotation
- API throttling

---

## Q12. How would you support multiple AI providers?

### Answer

Use an abstraction layer:

```text
Application
     ↓
AI Provider Adapter
 ├── OpenAI
 ├── Gemini
 ├── Claude
 └── Internal Models
```

Benefits:

- Vendor flexibility
- Failover support
- Cost optimization
- Dynamic model routing

---

# Key Learnings

- Environment variables must match actual exported names
- Virtual environments improve dependency isolation
- Prompt engineering significantly affects AI quality
- Deterministic AI responses are critical for enterprise tooling
- API authentication errors are commonly caused by configuration mismatches

---

# Final Result

Successfully developed and executed a Python-based AI Bug Description Clarifier that:

- Dynamically rewrites informal bug reports
- Uses OpenAI Chat Completion API
- Generates professional issue summaries
- Implements secure credential handling
- Produces deterministic outputs suitable for enterprise environments

---
