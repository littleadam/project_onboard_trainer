# project_onboard_trainer
This is an Aws based genAI application to train new members to a project with secured documents and processes.

Components:

User Interface (UI): This is where users interact with the system and submit their queries.
Amazon SageMaker Endpoint (Optional): If your Foundation Model (FM) is deployed on SageMaker, the UI sends the query there for initial processing.
Foundation Model (FM): This is a large language model (LLM) pre-trained on a massive dataset of text and code. It provides a baseline understanding of the user's query. (Optional for Bedrock Integration)
Amazon S3 Bucket: Stores the documents used for knowledge retrieval. These documents can be in various formats like text files, PDFs, etc.
Amazon Comprehend (Optional): If your documents require pre-processing for better understanding, Comprehend can be used for tasks like entity recognition, key phrase extraction, and sentiment analysis.
Amazon Kendra (Optional): This is an optional component that can be used for indexing and searching the documents in the S3 bucket. It can improve retrieval performance.
Bedrock Knowledge Base: This component stores the processed document representations (embeddings) and metadata extracted from the documents in the S3 bucket. The Bedrock Agent automatically generates these embeddings.
Bedrock Retrieve API: This API takes the user query as input and retrieves the most relevant documents from the Bedrock Knowledge Base based on the document embeddings and the query embedding.
Bedrock Generate API (Optional): This API takes the user query and the retrieved documents as input and utilizes the FM (if deployed on SageMaker) to generate a response that incorporates information from both the query and the relevant documents.
Guardrails (Optional): This component can be used to filter out undesirable or harmful content from the user query or the model response based on pre-defined policies.
Response: The final response is presented to the user through the UI.
Data Flow:

User submits a query: The user enters a query through the UI.
(Optional) Preprocess Query (SageMaker): If an FM is deployed on SageMaker, the query might be sent there for initial processing.
Query Embedding: The user query is converted into a numerical representation (embedding) for efficient retrieval.
Document Retrieval: The Bedrock Retrieve API searches the Bedrock Knowledge Base for documents with embeddings most similar to the query embedding.
(Optional) Document Preprocessing (Comprehend): If Comprehend is used, it can further process the retrieved documents for tasks like entity recognition.
(Optional) Document Enrichment (Kendra): If Kendra is used, it can provide additional information about the retrieved documents.
(Optional) Generate Response: If an FM is used, the Bedrock Generate API takes the user query and the retrieved documents as input and generates a response using the FM.
(Optional) Apply Guardrails: Guardrails can be used to filter inappropriate content from the user query or the model response.
Present Response: The final response is displayed to the user through the UI.
Benefits:

Improves the accuracy and relevance of responses by incorporating information from relevant documents.
Reduces the need to constantly retrain the FM as new knowledge can be added to the knowledge base.
Provides a more flexible and scalable approach to knowledge-based applications.
Note:

This is a high-level diagram. The specific components and data flow may vary depending on your specific requirements.
The use of SageMaker, Comprehend, and Kendra is optional and depends on your specific use case.
