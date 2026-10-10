# Home Credit Loan Against Property (LAP) — Voice AI Qualification Agent

[![Retell AI](https://img.shields.io/badge/Platform-Retell%20AI-blue.svg)](https://www.retellai.com/)
[![Language](https://img.shields.io/badge/Language-English%20%7C%20Hindi-green.svg)](#multilingual-support)
[![Status](https://img.shields.io/badge/Evaluation-8%20Scenarios%20Tested-brightgreen.svg)](#test-scenarios-recordings--transcripts)

An enterprise-grade, conversational voice AI agent designed for **Home Credit** to conduct outbound preliminary qualification calls for pre-approved **Loan Against Property (LAP)** offers up to **₹75,00,000 (75 Lakhs)**.

The agent handles complex real-world voice conversational dynamics: multi-slot out-of-order extraction, natural interruption handling, balance transfer detection, polite rejection exits, callback scheduling, and full English / Hindi bilingual fluency with grammatically accurate gender alignment.

---

## 🚀 Live Interactive Demo

Test the live voice agent directly in your browser:

🔗 **[Try the Voice Agent on Retell AI](https://agent.retellai.com/orb/agent_3f3d73ccb081b0bb72de85b57a?token=7cb225cbbafc4380f36e54a94abc967b)**

*(Microphone permission required. Also documented in [`AGENT_URL.txt`](AGENT_URL.txt))*

---

## 📌 Table of Contents

- [Live Interactive Demo](#-live-interactive-demo)
- [Project Overview](#project-overview)
- [Qualification & Policy Rules](#qualification--policy-rules)
- [Key Conversational Capabilities](#key-conversational-capabilities)
- [Repository Structure](#repository-structure)
- [Test Scenarios, Recordings & Transcripts](#test-scenarios-recordings--transcripts)
- [System Prompt Design](#system-prompt-design)
- [How to Test the Agent](#how-to-test-the-agent)

---

## Project Overview

Home Credit provides pre-approved Loan Against Property (LAP) offers to existing valued customers. This conversational AI agent serves as the first line of engagement:

1. **Identity & Availability Verification:** Confirms customer identity and checks availability before pitching.
2. **Preliminary Value Pitch:** Explains the pre-approved offer clearly with transparent disclaimers that it is a preliminary check, not a final credit decision.
3. **Structured Information Gathering:** Collects all 7 mandatory qualification fields naturally through conversation.
4. **Deterministic Policy Enforcement:** Immediately and politely rejects or reroutes callers who do not meet credit criteria, saving underwriter time.
5. **Specialized Routing & Handoff:** Identifies balance transfer / refinance intent or transfers eligible applicants directly to a Senior Loan Expert.

---

## Qualification & Policy Rules

The voice agent is strictly configured with Home Credit's preliminary eligibility guardrails:

| Qualification Parameter | Permitted / Pass Criteria | Disqualification / Alternate Path |
| :--- | :--- | :--- |
| **Property Type** | Residential, Commercial, or Industrial property | **Agricultural land** or vacant plots are ineligible (politely terminate) |
| **Ownership Status** | Sole ownership or Joint ownership | Third-party / Disputed properties disqualified |
| **Original Documents** | Original title deeds / documents available at home | Missing / unavailable originals cannot proceed |
| **Requested Loan Amount** | Up to ₹75,00,000 (₹75 Lakhs) | Requests > ₹75L offered maximum cap of ₹75L; if declined, exit politely |
| **Income Mode** | Salaried or Self-Employed via **Bank Transfer / Cheque** | **Pure cash income** is ineligible without formal banking paper trail |
| **Preferred Tenure** | **3 to 15 Years** | Tenures < 3 years or > 15 years are outside policy limits |
| **Existing Loan / BT** | Balance transfer / EMI consolidation requested | Route to dedicated **Loan Transfer Specialist** |

---

## Key Conversational Capabilities

- **Out-of-Order Slot Extraction:** If a customer answers multiple questions in a single breath (e.g., *"It's my residential house, worth 1.1 crore, and I want 50 lakhs"*), the agent captures all 3 slots simultaneously and never redundantly asks for them again.
- **Interruption & Tangent Management:** Answers mid-call customer questions (such as interest rate ranges or turnaround times) with appropriate regulatory disclaimers before smoothly guiding the conversation back to the next pending qualification step.
- **Existing Loan Transfer Intent:** Detects keywords like *"already have a loan"*, *"transfer my loan"*, *"lower my EMI"*, and transfers the lead to the balance transfer team.
- **Respectful Exit on Ineligibility:** Once hard disqualification criteria are met (e.g., cash income, agricultural land), the agent does not interrogate the user further. It politely explains the policy constraint and closes the call gracefully.
- **Busy / Call-Later Scheduling:** Respects customer availability immediately if they are driving, in a meeting, or occupied, capturing preferred callback times without aggressive sales pressure.
- **Bilingual & Gender Concordance:** Seamlessly conducts conversations in professional English or native conversational Hindi, utilizing proper feminine grammatical verb conjugations and self-references (`जाँच करनी होगी`, `बता देती हूँ`) aligned with the agent persona (*Ananya*).

---

## Repository Structure

```plaintext
ShiftAI/assignment/
├── AGENT_URL.txt           # Live agent web orb URL on Retell AI
├── SYSTEM_PROMPT.md        # Complete production system prompt with state logic & guardrails
├── README.md               # Documentation & test summary
├── recordings/             # 8 full audio call recordings (.wav)
│   ├── Call 1 — Successful qualification.wav
│   ├── Call 2 — Agricultural property.wav
│   ├── Call 3 — Cash income.wav
│   ├── Call 4 — Above-limit request, then acceptance.wav
│   ├── Call 5 — Existing loan  EMI transfer.wav
│   ├── Call 6 — Out-of-order facts, interruption, and rate question.wav
│   ├── Call 7 — Busy customer.wav
│   └── Call 8 — Hindi language and gender check.wav
└── transcripts/            # Markdown transcripts with checklist evaluations
    ├── call1.md
    ├── call2.md
    ├── call3.md
    ├── call4.md
    ├── call5.md
    ├── call6.md
    ├── call7.md
    └── call8.md
```

---

## Test Scenarios, Recordings & Transcripts

The agent has been rigorously benchmarked across 8 comprehensive call scenarios covering happy paths, edge cases, hard disqualifications, and conversational pivots:

| # | Scenario | Audio Recording | Transcript | Key Behavior Validated | Call Outcome |
| :-: | :--- | :--- | :--- | :--- | :--- |
| **1** | **Successful Qualification** | [Audio](recordings/Call%201%20%E2%80%94%20Successful%20qualification.wav) | [`call1.md`](transcripts/call1.md) | Standard end-to-end happy path; all 7 parameters collected cleanly | **Qualified** (Handoff to Senior Expert) |
| **2** | **Agricultural Property** | [Audio](recordings/Call%202%20%E2%80%94%20Agricultural%20property.wav) | [`call2.md`](transcripts/call2.md) | Customer offers agricultural farmland; early exit without unnecessary questions | **Ineligible** (Policy rejection) |
| **3** | **Cash Income Mode** | [Audio](recordings/Call%203%20%E2%80%94%20Cash%20income.wav) | [`call3.md`](transcripts/call3.md) | Self-employed customer with pure cash earnings; flags banking proof requirement | **Ineligible** (Policy rejection) |
| **4** | **Above-Limit Request** | [Audio](recordings/Call%204%20%E2%80%94%20Above-limit%20request%2C%20then%20acceptance.wav) | [`call4.md`](transcripts/call4.md) | Customer requests ₹90L; agent offers ₹75L cap; customer accepts ₹75L and proceeds | **Qualified** (Approved at ₹75L limit) |
| **5** | **Existing Loan / EMI Transfer** | [Audio](recordings/Call%205%20%E2%80%94%20Existing%20loan%20%20EMI%20transfer.wav) | [`call5.md`](transcripts/call5.md) | Customer mentions existing loan balance and interest reduction goal | **Rerouted** (Transfer Specialist handoff) |
| **6** | **Interruption & Rate Query** | [Audio](recordings/Call%206%20%E2%80%94%20Out-of-order%20facts%2C%20interruption%2C%20and%20rate%20question.wav) | [`call6.md`](transcripts/call6.md) | Multiple slots in one utterance + mid-call interest rate query answered transparently | **Qualified** (Handoff to Senior Expert) |
| **7** | **Busy Customer** | [Audio](recordings/Call%207%20%E2%80%94%20Busy%20customer.wav) | [`call7.md`](transcripts/call7.md) | Customer driving; agent acknowledges promptly and schedules callback time | **Callback Scheduled** |
| **8** | **Hindi Language & Tenure Check** | [Audio](recordings/Call%208%20%E2%80%94%20Hindi%20language%20and%20gender%20check.wav) | [`call8.md`](transcripts/call8.md) | Fluent Hindi conversation, female gender agreement, handles invalid 2-year tenure | **Ineligible** (Tenure below 3-year minimum) |

---

## System Prompt Design

The system instructions in [`SYSTEM_PROMPT.md`](SYSTEM_PROMPT.md) are engineered to prevent common voice AI failure modes:

1. **State Tracking & Missing-Slot Logic:** The agent tracks which of the 7 fields are satisfied, prioritizing unasked questions rather than following a rigid script.
2. **Context Guardrails:** Explicitly distinguishes preliminary pre-qualification from final underwriting to maintain regulatory compliance (RBI guidelines for financial disclosures).
3. **No Redundant Questioning:** If a field was disclosed casually during greeting or property description, the agent absorbs it silently.
4. **Tone & Empathy:** Warm, consultative, and concise — keeping voice turns below 25 words where possible to minimize latency and cognitive fatigue.

---

## How to Test the Agent

1. Visit the [Retell Agent Web Interface](https://agent.retellai.com/orb/agent_3f3d73ccb081b0bb72de85b57a?token=7cb225cbbafc4380f36e54a94abc967b).
2. Allow microphone access in your browser.
3. Try testing the scenarios outlined above:
   - *Test natural interruptions:* Say *"Wait, what is your interest rate?"* mid-conversation.
   - *Test bulk info:* Say *"I have a commercial shop in Delhi worth 80 lakhs, owned by me, and I need 40 lakhs."*
   - *Test in Hindi:* Respond in Hindi (*"हाँ, मैं राहुल बोल रहा हूँ..."*) to experience bilingual voice generation.
