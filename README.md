# FinSolve RAG Chatbot

## Objective

Built an internal AI chatbot for FinSolve Technologies (a fictional fintech company) that lets employees ask questions about company data in plain English. The key challenge was making sure each department only sees their own data — finance can't see HR salaries, employees can't see revenue numbers, but the CEO sees everything.

## What it does

- Employees log in, and the system figures out their role (finance, marketing, HR, engineering, c-level, or general employee)
- They type a question like "what was our Q3 revenue?" or "how many sick days do I get?"
- The system searches through company documents, but only the ones that person is allowed to access
- It generates an answer using an LLM and cites exactly which document it pulled the information from
- If the documents don't have the answer, it says so instead of making something up

## How I built it

I started by taking all the company documents (financial reports, marketing data, HR records, engineering docs, employee handbook) and breaking them into small searchable chunks. Each chunk gets tagged with which department it belongs to and stored in a vector database.

When a user asks a question, the system first checks their role, then filters the database to only search through documents they're authorized to see. The matching chunks get passed to Claude (Anthropic's LLM) along with strict instructions to only answer from the provided context and always cite sources.

The access control happens at the retrieval layer — unauthorized documents never even reach the LLM, so there's no chance of data leaking through.

## Tools used

Python, FastAPI, LangChain, ChromaDB, Streamlit, Claude API (Anthropic), HuggingFace Embeddings, Pandas
