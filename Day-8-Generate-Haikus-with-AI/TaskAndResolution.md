# TaskAndResolution.md

# AI-Based Haiku Generator using OpenAI API

---

# Project Overview

The Enterprise AI Creativity Engineering team initiated an innovation project to explore how Artificial Intelligence can generate creative literary content automatically.

The objective was to develop a Python-based AI Haiku Generator capable of creating three-line haikus following the traditional 5-7-5 syllable pattern using the OpenAI Chat Completion API.

This solution demonstrates how Generative AI can be used for creative writing, content generation, education, and digital storytelling.

---

# Task Objective

Develop a Python application named:

```text
haiku_generator.py
```

The application should:

1. Initialize an OpenAI client
2. Load API credentials securely
3. Accept a topic dynamically
4. Generate a parameterized haiku prompt
5. Request a 5-7-5 syllable haiku from the AI model
6. Print the generated three-line haiku

---

# Environment Details

| Component | Value |
|------------|---------|
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

Changed the working directory to the project workspace where the AI Haiku Generator would be created.

---

# Step 2 — Create Virtual Environment

## Command

```bash
python3 -m venv venv
```

---

# Explanation

Created an isolated Python virtual environment.

Benefits:

- Dependency isolation
- Clean package management
- Environment consistency
- Simplified troubleshooting

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

Activates the Python virtual environment.

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

Installs the OpenAI SDK and required dependencies.

Installed packages included:

- openai
- httpx
- pydantic
- anyio
- tqdm

---

# Step 5 — Load Environment Variables

## Command

```bash
source /root/.bash_profile
```

---

# Explanation

Loads OpenAI credentials into the shell environment.

Variables used:

```bash
OPENAI_API_KEY
OPENAI_API_BASE
```

---

# Step 6 — Create haiku_generator.py

## Command

```bash
vi /root/openaiproject/haiku_generator.py
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

def generate_haiku(topic: str) -> str:
    prompt = f"""
Generate a haiku about '{topic}'.

Requirements:
- Exactly 3 lines
- Follow a 5-7-5 syllable structure
- Output only the haiku
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
        temperature=0.0
    )

    return response.choices[0].message.content.strip()

# Topic
topic = "sky"

# Store response
response = generate_haiku(topic)

# Print haiku
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

Used to access Linux environment variables.

## OpenAI

Imports the OpenAI client library.

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

Creates a secure OpenAI API client using environment variables.

---

# Why Environment Variables Are Important

Advantages:

- Secure secret management
- No hardcoded credentials
- Easier CI/CD integration
- Simplified credential rotation

---

# Define generate_haiku Function

```python
def generate_haiku(topic: str) -> str:
```

---

# Explanation

Creates a reusable function that accepts a topic dynamically.

---

# Prompt Engineering

```python
prompt = f"""
Generate a haiku about '{topic}'.
"""
```

---

# Explanation

Uses prompt engineering to instruct the model to:

- Generate a haiku
- Follow 5-7-5 structure
- Produce exactly three lines

---

# Send Request to OpenAI

```python
response = client.chat.completions.create(
```

---

# Explanation

Sends the generated prompt to OpenAI Chat Completion API.

---

# Model Used

```python
model="openai/gpt-4.1-mini"
```

---

# Explanation

Uses GPT-4.1-mini for lightweight creative text generation.

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

Defines the user message sent to the AI model.

---

# max_tokens

```python
max_tokens=60
```

---

# Explanation

Limits the maximum size of generated output.

Benefits:

- Faster responses
- Cost optimization
- Output control

---

# temperature

```python
temperature=0.0
```

---

# Explanation

Controls randomness.

| Value | Behavior |
|---------|-----------|
| 0.0 | Deterministic |
| 0.5 | Balanced |
| 1.0 | Creative |

A value of 0.0 ensures consistent haiku generation.

---

# Extract Response

```python
return response.choices[0].message.content.strip()
```

---

# Explanation

Retrieves and cleans the generated haiku.

---

# Define Topic

```python
topic = "sky"
```

---

# Explanation

Stores the haiku topic.

---

# Store Response

```python
response = generate_haiku(topic)
```

---

# Explanation

Calls the AI function and stores the generated haiku.

---

# Print Output

```python
print(response)
```

---

# Explanation

Displays the generated haiku in the terminal.

---

# Step 7 — Execute Script

## Command

```bash
python3 /root/openaiproject/haiku_generator.py
```

---

# Final Successful Output

```text
Endless blue canvas,
Whispers of clouds drift softly,
Dreams float with the breeze.
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
Haiku Generation
        ↓
Terminal Output
```

---

# Enterprise Use Cases

## Creative Content Automation

- Poetry generation
- Creative writing assistance
- Storytelling tools

## Education Platforms

- Literature learning
- Language practice
- Creative writing exercises

## Marketing & Branding

- Creative campaigns
- Social content creation
- AI-assisted copywriting

---

# Security Best Practices

| Practice | Purpose |
|------------|-----------|
| Environment Variables | Secure credentials |
| Virtual Environment | Dependency isolation |
| Token Limits | Cost optimization |
| Prompt Constraints | Output control |

---

# Production Enhancement Ideas

## Suggested Improvements

- Web UI
- REST API
- Multiple poetry styles
- Language selection
- Theme libraries
- Prompt templates
- AI content moderation

---

# Scenario Based Interview Questions & Answers

# L1 — Junior Engineer Level

---

## Q1. Why use a Python virtual environment?

### Answer

A virtual environment isolates project dependencies and prevents conflicts between packages used by different projects.

---

## Q2. Why use environment variables for API keys?

### Answer

Environment variables prevent sensitive credentials from being hardcoded in source code.

---

## Q3. What is prompt engineering?

### Answer

Prompt engineering is the process of designing instructions that guide AI models toward desired outputs.

Example:

```text
Generate a haiku about sky.
Follow a 5-7-5 syllable pattern.
```

---

# L2 — Mid-Level Engineer

---

## Q4. Why use temperature=0.0?

### Answer

Temperature 0.0 minimizes randomness and produces consistent outputs.

---

## Q5. Why limit max_tokens?

### Answer

max_tokens helps:

- Reduce costs
- Improve performance
- Control output length

---

## Q6. Why use a parameterized function?

### Answer

Parameterized functions increase code reusability and support dynamic input values.

---

# L3 — Senior Engineer Level

---

## Q7. How would you productionize this solution?

### Answer

Production enhancements:

- FastAPI backend
- Docker deployment
- Kubernetes orchestration
- Monitoring
- Logging
- Retry mechanisms

---

## Q8. How would you improve reliability?

### Answer

Add:

- Exception handling
- Timeout controls
- API retries
- Response validation
- Structured logging

---

## Q9. How would you optimize OpenAI costs?

### Answer

Optimization strategies:

- Prompt reduction
- Response caching
- Smaller models
- Batch processing

---

# L4 — Architect Level

---

## Q10. Design an enterprise AI Creative Content Platform.

### Answer

### Architecture

```text
Web Application
       ↓
API Gateway
       ↓
AI Orchestration Layer
       ↓
Prompt Management Service
       ↓
OpenAI Integration Layer
       ↓
Content Repository
       ↓
Analytics Dashboard
```

---

# Core Components

## API Gateway

- Authentication
- Rate limiting
- Request validation

## Prompt Layer

- Template management
- Version control
- Content validation

## AI Layer

- Multi-model routing
- Failover support
- Output normalization

## Analytics Layer

- Usage tracking
- Content insights
- Cost monitoring

---

## Q11. How would you secure AI-generated content systems?

### Answer

Security controls:

- Secret management
- TLS encryption
- RBAC
- Audit logging
- API gateway protection

---

## Q12. How would you support multiple AI vendors?

### Answer

Use an abstraction layer:

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
- Failover capability
- Cost optimization

---

# Key Learnings

- Prompt engineering strongly affects AI output
- Environment variables improve security
- Virtual environments isolate dependencies
- Temperature controls AI creativity
- Structured prompts improve consistency

---

# Final Result

Successfully developed and executed a Python-based AI Haiku Generator that:

- Uses OpenAI GPT-4.1-mini
- Generates topic-based haikus
- Follows the traditional 5-7-5 structure
- Uses secure environment variables
- Demonstrates enterprise AI integration best practices
- Produces structured creative content automatically

---
