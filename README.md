RAG System with Pinecone Vector Database
A Retrieval-Augmented Generation (RAG) system that extracts text from documents (PDF, DOCX, TXT), stores embeddings in Pinecone vector database, and answers questions using semantic search and question-answering models.
Features

Multi-format Support: Process PDF, DOCX, and TXT files
Semantic Search: Uses sentence transformers for embedding generation
Vector Storage: Pinecone serverless vector database integration
Question Answering: Transformer-based QA pipeline for accurate answers
Efficient Retrieval: Fast similarity search with cosine metric

Overview
This RAG system enables you to upload documents, extract their content, convert text into vector embeddings, store them in Pinecone's vector database, and then ask questions about the content. The system retrieves relevant information and generates accurate answers using state-of-the-art NLP models.
Prerequisites

Python 3.7 or higher
Pinecone API key (obtainable from Pinecone Console)
Google Colab environment (optional but recommended for easy setup)
Stable internet connection

Required Packages
The system requires the following Python packages:

pymupdf: For PDF text extraction
python-docx: For DOCX file processing
pinecone-client: Official Pinecone vector database client
sentence-transformers: For generating text embeddings
transformers: For the question-answering pipeline

How It Works
Document Processing Pipeline

Upload Document: Upload a PDF, DOCX, or TXT file to the system
Text Extraction: The system extracts raw text from the uploaded document
Text Chunking: Content is split into manageable chunks (default: 100 words per chunk)
Embedding Generation: Each chunk is converted into a 384-dimensional vector using the all-MiniLM-L6-v2 model
Storage: Embeddings are stored in Pinecone with metadata containing the original text

Question Answering Pipeline

User Query: You ask a question about the uploaded document
Query Embedding: Your question is converted into a vector embedding
Similarity Search: Pinecone finds the most relevant text chunks using cosine similarity
Context Retrieval: Top matching chunks are retrieved and combined
Answer Generation: A transformer-based QA model generates an answer from the context

Configuration
Embedding Model
The system uses all-MiniLM-L6-v2 by default, which produces 384-dimensional embeddings. This model offers a good balance between speed and accuracy for semantic search tasks.
Pinecone Index

Index Name: rag-demo (customizable)
Dimension: 384 (matches the embedding model output)
Metric: Cosine similarity
Cloud Provider: AWS
Region: us-east-1 (Serverless)

Text Chunking
Documents are split into chunks of 100 words by default. This size can be adjusted based on your specific use case and requirements.
Key Functionalities
Text Extraction
Supports multiple document formats and automatically detects the file type based on extension, then applies the appropriate extraction method.
Embedding and Storage
Each text chunk is converted into a numerical vector representation and stored in Pinecone with a unique identifier and metadata containing the original text.
Context Retrieval
When you ask a question, the system retrieves the top 3 most relevant text chunks from the vector database based on semantic similarity.
Answer Generation
A pre-trained question-answering model processes your question along with the retrieved context to generate a precise answer.
Use Cases

Document Question Answering: Ask specific questions about uploaded documents
Resume Parsing: Extract and query information from resumes
Knowledge Base Search: Build searchable knowledge bases from documents
Research Paper Analysis: Query scientific papers and technical documents
Legal Document Review: Search through contracts and legal texts
Technical Documentation: Quick lookup in user manuals and guides

System Architecture
The system follows a clear pipeline:
Indexing Phase: Document → Text Extraction → Chunking → Embedding → Pinecone Storage
Query Phase: User Query → Query Embedding → Similarity Search → Context Retrieval → Answer Generation
Advantages

Scalability: Pinecone serverless handles growing document collections
Speed: Fast similarity search even with large datasets
Accuracy: State-of-the-art NLP models for embedding and QA
Flexibility: Works with multiple document formats
Cost-Effective: Free tier available for development and testing

Limitations

Maximum file size depends on available memory
Best performance with English language content
Pinecone free tier has usage limits (check their pricing page)
Answer quality depends on the relevance of retrieved context
Complex queries spanning multiple topics may need refinement

Performance Optimization Tips

Batch Processing: Process multiple documents simultaneously for efficiency
Chunk Size Tuning: Experiment with different chunk sizes for your specific content
Model Selection: Choose embedding models appropriate for your domain
Index Management: Regularly clean up unused indexes to optimize performance
Query Refinement: Formulate clear, specific questions for better results

Troubleshooting Guide
Connection Issues
Verify your Pinecone API key is correct and you have an active internet connection.
No Results Found
Ensure documents are properly indexed and try adjusting the number of results retrieved (top_k parameter).
Embedding Errors
Confirm the embedding dimension matches your model's output (384 for all-MiniLM-L6-v2).
