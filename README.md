# CS5588_DS_Capstone
# Week 1 Hands-On Lab
Data Science Capstone Project
Name: Prathyu Adari
Major: Data Science Analytics - Graduate Program

Research / Project Interest: 
Dynamic "Challenge" & Identity Verification Agent 
 Objective & Impact: 
o Problem: Static security questions ("What is your mother's maiden name?") are 
easy to hack. When a high-risk transaction happens, banks need a better way to 
verify identity without blocking the user entirely. 
o Impact: A "Smart Challenge" agent that generates context-aware verification 
questions based on the user's recent real spending history (which a hacker 
wouldn't know). 
 Models & GenAI Methods: 
o Knowledge Graph + LLM: Construct a temporary Knowledge Graph of the 
user's genuine past 30 days of transactions. 
o GenAI Agent: The LLM generates a unique, one-time question based on that 
graph (e.g., "You spent approximately $40 at a coffee shop last Tuesday. Was 
it Starbucks or Dunkin?"). 
 Planned Deliverable: 
o Demo: A simulated mobile app interface where the AI agent asks a dynamic 
security question to "unblock" a flagged credit card transaction. 

# Week 2 Hands-On Lab
# SentinelAuth: Dynamic Identity Verification Agent 🛡️

## 1. Product Overview
**Venture:** SentinelAuth
**Problem:** Static security questions (e.g., "Mother's maiden name") are vulnerable to social engineering.
**Solution:** A RAG-based agent that dynamically retrieves verification protocols based on real-time risk scores (Context-Aware Auth).
**Target User:** FinTech compliance teams and automated banking portals.

## 2. System Architecture
* **Retrieval:** Hybrid Pipeline (BM25 for exact rule matching + FAISS for semantic context).
* **Generation:** Google Flan-T5-Large (Local Execution).
* **Governance:** "Safety Gateway" function that intercepts `MANUAL_REVIEW` signals and locks accounts.

## 3. Risk & Trust Analysis
| Risk Scenario | System Behavior | Safeguard Implemented |
| :--- | :--- | :--- |
| **Hallucination** | Agent invents a fake security rule. | **Grounding:** Agent strictly constrained to retrieved chunks. |
| **High Stakes** | Critical risk score (150+). | **Governance Layer:** Auto-detects "MANUAL_REVIEW" and locks account. |
| **Missing Data** | New threat (Deepfake) not in policy. | **Failure Loop:** System detects low confidence/generic answer -> Triggers Policy Update. |

## 4. Evaluation Results
| Metric | Score | Description |
| :--- | :--- | :--- |
| **Precision@1** | 0.67 (67%) | retrieved the correct policy for 3/3 test cases. |
| **Trust Score** | 3.7/5.0 | Agent consistently followed "Human Handoff" protocols. |

## 5. Failure & Fix Demo
* **The Failure:** Initially, the system had no protocol for "Deepfake" threats, resulting in generic responses.
* **The Fix:** We implemented a dynamic document loader that injected a "Deepfake Protocol".
* **Result:** The agent now correctly identifies deepfake attempts and issues an immediate auto-ban.
