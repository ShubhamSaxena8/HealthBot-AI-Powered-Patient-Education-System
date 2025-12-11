# HealthBot – AI-Powered Patient Education System

An AI-powered chatbot prototype that helps patients understand medical conditions and treatments through personalized explanations and interactive quizzes.

## Overview

HealthBot is an agentic AI prototype designed to improve patient education and engagement. It guides patients through self-directed learning on specific health topics, using retrieval-augmented generation to provide concise explanations and then checking understanding through a short quiz.

The goal is to simulate how AI could support healthcare providers by handling basic patient education while keeping clinicians in control of medical decisions.

## Problem

Many patients struggle to understand their diagnosis, treatment options, and post-care instructions. This can lead to poor adherence, unnecessary readmissions, and worse outcomes. HealthBot explores how an AI assistant could:

- Provide clear, patient-friendly explanations on demand  
- Offer 24/7 access to reliable health information (from external sources)  
- Reinforce understanding through simple comprehension checks  

> This project is for educational and prototyping purposes only and is **not** a medical device or a source of clinical advice.

## Architecture & Flow

HealthBot uses a LangGraph-based workflow with a structured, multi-step conversation:

1. Ask the patient what health topic or condition they want to learn about.  
2. Use the Tavily search tool (via LangChain community integration) to fetch relevant, up-to-date information.  
3. Summarize search results into a patient-friendly explanation.  
4. Present the summary and wait until the patient indicates they are ready for a comprehension check.  
5. Generate a single, relevant quiz question based on the summary.  
6. Collect the patient’s answer.  
7. Evaluate the answer, assign a grade, and generate an explanation that references parts of the original summary.  
8. Show the grade and explanation to the patient.  
9. Ask if the patient wants to learn about another topic or end the session.  
10. When a new topic is selected, reset the internal state to avoid leaking information between topics.

### Logical Components

- **Conversation Orchestrator**  
  Controls the overall flow, tracks state, and decides which step to execute next.

- **Retrieval Component (Tavily via LangChain)**  
  Takes the patient’s topic and queries external sources for reliable information.

- **Summarization Component**  
  Converts raw search results into a concise, patient-friendly explanation.

- **Quiz Generation Component**  
  Creates a single, context-aware question based on the summary.

- **Evaluation Component**  
  Compares the patient’s answer with the expected answer and returns a grade plus explanation with citations.

- **Session Manager**  
  Manages topic-level state and ensures a clean reset when starting a new topic.

## Key Features

- Topic-driven patient education with natural language queries.  
- Retrieval-augmented responses using Tavily search via LangChain tools.  
- Single-question quiz per topic to check understanding.  
- Graded feedback with explanations referencing earlier content.  
- Session reset for privacy and accurate context handling.  

## Tech Stack

- Language: Python  
- Orchestration: LangGraph  
- LLM Framework: LangChain  
- Retrieval: Tavily Search (LangChain community tool)  
- LLM Provider: Azure OpenAI / OpenAI (configurable)  

