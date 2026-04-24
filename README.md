# ERICA — AI Tutoring Agent

A GraphRAG-powered AI tutor that answers natural language questions grounded 
in course lecture content, built with LangChain, FAISS, and an LLM backbone.

## Architecture

**Ingestion:** Scrapes course websites (BeautifulSoup) + fetches YouTube transcripts → 
chunked with RecursiveCharacterTextSplitter

**Knowledge Graph Construction:** An LLM extracts concepts, relationships (prereq_of, 
part_of, is_a, near_transfer), and resource nodes → stored as a directed graph (NetworkX)

**Retrieval:** Keyword-matched subgraph traversal retrieves relevant concept nodes + 
their linked source documents as context

**Generation:** Qwen-2.5-72B answers queries using the retrieved subgraph as grounded context

## Stack
`Python` `LangChain` `FAISS` `NetworkX` `BeautifulSoup` `YouTube Transcript API` 
`sentence-transformers` `OpenRouter API`

## Key Design Decisions
- GraphRAG over flat vector search: concept relationships (prerequisites, part-of) 
  enable structured reasoning paths, not just semantic similarity
- Multi-source ingestion: web + video transcripts unified into one knowledge graph
- JSON-structured LLM extraction: forces structured concept/edge output for reliable graph construction
