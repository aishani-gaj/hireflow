HireFlow AI: Multi-Agent HR Automation
Problem: Problem 2 (Multi-Agent HR Automation)

System Overview: HireFlow AI is a secure, three-agent system designed for automated HR tasks. It features robust safety layers including PII redaction, prompt hardening, and schema validation.

Architecture (The Three Agents)
TalentScout: Screens resumes against a Job Description (JD), calculates an explainable Role Fit Score (using a deterministic formula), and generates a confidence level.

Onboarder: Generates a personalized 30/60/90-day onboarding plan based on the candidate's structured profile.

PolicyAnswerer: Answers HR-related questions by performing a keyword search against the Policy Knowledge Store (policies.json) and grounding the LLM response only on the provided snippet.

Security and Defenses (The Winning Edge)
PII Redaction: Emails and phone numbers are removed from all user input before calling the LLM.

Prompt Hardening: All user input is contained within a dedicated user_data JSON field, and the system prompt forbids embedded instructions.

Schema Validation: All LLM outputs are validated against a required JSON schema. Invalid outputs are rejected, and the system falls back to a deterministic, rule-based explanation.

Audit Logging: Every transaction is logged to audit.log with a timestamp, redacted input, and the active prompt_template_version for full traceability.

Setup and Running
Clone the Repo and create the virtual environment:

python -m venv venv
source venv/bin/activate
pip install -r requirements.txt

Set Environment Variables: Get your key and choose your model.

export OPENAI_API_KEY="sk-..."
export OPENAI_MODEL="gpt-4o-mini"

Start the App:

python app.py

(The app runs on http://127.0.0.1:5050)

Run Break Tests (Attack Phase): While the server is running, open a new terminal and run the attack script to demonstrate defenses:

python break_tests.py
