# vector-embeddings-store
Connect Amazon Bedrock to Postgres on EC2 with LangChain

import os
import boto3
from langchain.embeddings import BedrockEmbeddings
from langchain.vectorstores.pgvector import PGVector, DistanceStrategy

# Load environment variables
PGVECTOR_HOST = os.environ.get('PGVECTOR_HOST')
PGVECTOR_PORT = os.environ.get('PGVECTOR_PORT')
PGVECTOR_DATABASE = os.environ.get('PGVECTOR_DATABASE')
PGVECTOR_USER = os.environ.get('PGVECTOR_USER')
PGVECTOR_PASSWORD = os.environ.get('PGVECTOR_PASSWORD')

# Initialize the Bedrock client
bedrock_client = boto3.client('bedrock')

# Initialize the text embedding model
embeddings = BedrockEmbeddings(bedrock_client=bedrock_client)

# Create a connection string for the PostgreSQL database
connection_string = f"postgresql://{PGVECTOR_USER}:{PGVECTOR_PASSWORD}@{PGVECTOR_HOST}:{PGVECTOR_PORT}/{PGVECTOR_DATABASE}"

# Create a PGVector instance for the vector database
vector_store = PGVector(
    connection_string=connection_string,
    embedding_function=embeddings,
    distance_strategy=DistanceStrategy.EUCLIDEAN,
    collection_name="vector_embeddings"
)

# Example usage: Add a vector embedding to the database
text = "This is a sample text for vector embedding."
vector_store.add_texts([text])

# Example usage: Search for similar texts
query = "What is a vector embedding?"
results = vector_store.similarity_search(query, k=3)
print(results)
