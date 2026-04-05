# Week 7: RAG Security Knowledge Assistant — Evaluation Report

## 1. Setup Summary
- **LLM:**
  - llama-3.3-70b-versatile via Groq
- **Embeddings:**
  - sentence-transformers/all-MiniLM-L6-v2 via HuggingFace
- **Vector Store:**
  - In-Memory Vector Store
- **Documents loaded:**
  - mitre-initial-access.txt (~1-2 pages)
  - mitre-lateral-movement.txt (~1-2 pages)
  - mitre-credential-access.txt (~1-2 pages)

## 2. Test Results

| # | Question | Used Documents? | Quality | Notes |
|---|----------|----------------|---------|-------|
| 1 | How can valid cloud accounts be used by adversaries to achieve persistence or lateral movement? | Yes | Good | It makes references to the Additional Cloud Credentials document. It is accurate, but it is more general than the information in the actual documents. |
| 2 | What are different ways attackers can gain initial access through Wi-Fi networks, and what risks does this create? | Yes | Good | It makes references such as the Evil Twin attacks and their different risks. It is very accurate, and it matches the information from the document. |
| 3 | How does brute force password guessing work, and what systems or services are commonly targeted? | Yes | Good | It references specific services and ports like SSH and RDP. It is using a lot of detailed information from the documents. |
| 4 | How can attackers use Remote Desktop Protocol (RDP) for lateral movement after obtaining valid credentials? | Yes | Good | It explains how RDP is used for lateral movement and mentions real attacker groups. |
| 5 | What is a trusted relationship attack, and how can compromising a third-party provider lead to access in a target organization? | No | Partial | The answer is correct, but it sounds more like general information about the topic. |

## 3. Edge Case Observations
- **Unrelated question:**
  - When I asked “What is the weather like today?”, the chatbot responded with “Hmm, I’m not sure”, instead of making up an answer. As it is only able to give an answer using the documents it has available. 
- **Topic not in documents:**
  - When I asked about trusted relationship attacks or CVEs, the chatbot still generated an answer instead of saying that it doesn't know. This was partial hallucination, as the chatbot gave an answer based on more general knowledge instead of using information strictly in the documents it was given. 

## 4. Settings Experiments 
- **Temperature change:**
  - Increasing the temperature from 0.3 to 0.7, it made the responses more detailed and natural, but it also caused the chatbot to give more information that was not in the documents. 
- **Chunk size change:**
  - Reducing the chunk size from 1000 to 500, it improved the retrieval accuracy. The chatbot gave an answer that was more focused and relevant because it was pulling from smaller sections of the documents. 
- **Top K change:**
  - Increasing the Top K from 4 to 6, it made the answer more detailed because it was retrieving more document chunks. However, there was a bit of unnecessary and repeated information in the answer.

## 5. Reflection
- What surprised you about how RAG works? 
  - What surprised me most about how RAG works was how the quality of the answer depends on how the model retrieves the information, rather than just the model itself. 
- How could you improve this chatbot for real-world use?
  - I would improve the chatbot by adding more documents that cover more techniques and I would add more features that would prevent the chatbot from hallucinating when it is asked a question that is not within its documents.
- How might you use RAG in your capstone project?
  - I could use RAG to build a cybersecurity assistant that analyzes threat intelligence feeds and maps them. It could help automate the threat analysis by retrieving relevant attack patterns and explaining them.

## 6. Flowise Chatbot Share Link
- https://cloud.flowiseai.com/chatbot/7f436a8e-24f9-473a-8f23-1adfcf8c4187 
