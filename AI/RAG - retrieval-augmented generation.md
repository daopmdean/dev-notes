
your prompt -> divide your prompt into chunk -> query in vector db data related to your chunk data -> append to your prompt -> post LLM -> response

this is to avoid fine-tuning a model to train again the data (which cost time and effort), 
RAG help users to feed the latest data from the knowledge base into the prompt 

steps apply RAG
1. feed data into vector database (knowledge base)
2. retrieve relevant data from your vector database
3. inject retrieved data into your original prompt
4. send prompt to LLM

