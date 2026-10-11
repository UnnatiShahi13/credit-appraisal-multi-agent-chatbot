# credit-appraisal-multi-agent-chatbot
Multi-agent RAG chatbot built in n8n that answers Car Loan and Home Loan eligibility questions from a Credit Appraisal Policy document, using local Ollama models.
# Credit Appraisal Policy – Multi-Agent Chatbot

A multi-agent chatbot built with **n8n** that answers questions about loan
eligibility (Car Loan and Home Loan) using a Credit Appraisal Policy document
as its knowledge base.

## Overview
The workflow uses Retrieval-Augmented Generation (RAG) with an orchestrator
that delegates work to specialised agents, so answers come from the policy
document rather than from the model's imagination.

## Architecture

**1. Ingestion pipeline**
Manual Trigger → Read Policy File (.docx) → Default Data Loader →
Embeddings (Ollama) → Simple Vector Store

**2. Chat pipeline**
Chat Trigger → Orchestrator Agent (with Simple Memory), which calls:
- **policy_researcher**: searches the Policy Knowledge Base (vector store)
  and retrieves relevant policy rules
- **support_agent**: turns the findings into a clear, customer-friendly answer

## Tech Stack
- n8n (workflow automation)
- Ollama (local LLM and embedding models)
- n8n Simple Vector Store
- n8n Simple Memory (conversation context)

## Features
- Multi-agent orchestration (orchestrator + researcher + support agent)
- Answers grounded in the policy document
- Conversation memory across turns
- Says "not specified in the policy" when the information isn't available
- Runs locally, so no data leaves your machine

## Example Queries
- "What is the maximum LTV for a new battery electric car loan?"
- "Is a customer with a FOIR of 55% eligible for a Home Loan?"
- "What is the processing fee for a car loan?" → *Not specified in the policy*

## How to Run
1. Install n8n and Ollama, and pull your chat and embedding models.
2. Import `workflow/credit-appraisal-multi-agent.json` into n8n.
3. Configure the Ollama credentials in the model and embedding nodes.
4. Place the policy document in the path used by the *Read Policy File* node.
5. Run the **ingestion** flow once to build the vector store.
6. Open the chat and start asking questions.

## Screenshots
See the `/screenshots` folder.

## Future Improvements
- Persistent vector DB (Qdrant / Pinecone / Supabase)
- More loan products (personal, education)
- Eligibility calculator tool for LTV / FOIR
- Source citations in answers

## License
MIT
