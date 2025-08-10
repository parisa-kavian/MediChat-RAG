# MediChat-RAG
This project is an AI-powered Question & Answering (Q&A) system that leverages the Retrieval-Augmented Generation (RAG) technique to provide accurate answers to medical questions. The system's knowledge base is sourced from authoritative articles on the Mayo Clinic website.

The repository includes two primary Python scripts:

A stateless bot: Processes each question independently without any memory of past interactions.

A stateful bot: Maintains conversational context, allowing it to understand and answer follow-up questions.

# Key Features
Authoritative Data Source: Scrapes and processes data from trusted Mayo Clinic articles to ensure high-quality, reliable information.

Automated Data Processing: Features a complete pipeline for web scraping, HTML cleaning, and text chunking.

Semantic Search: Utilizes OpenAIEmbeddings and FAISS to find the most relevant text chunks based on the semantic meaning of a user's query.

LLM-Powered Response Generation: Employs the gpt-4o-mini model to generate coherent, context-aware answers based on the retrieved information.

RAG Architecture with LangChain: Implemented with an efficient LangChain Expression Language (LCEL) chain to orchestrate the retrieval and generation workflow.

Conversational Memory: The stateful version can understand context and pronouns (e.g., "it," "its") in follow-up questions.
