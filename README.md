# vector-embeddings-store
Sample python code to Connect Amazon Bedrock with Postgres on EC2 with LangChain. This is useful when you are running a Postgres database on an AWS EC2 instance.

# Here's a breakdown of the code:

1. Import the necessary modules and classes from boto3, langchain.embeddings, and langchain.vectorstores.pgvector.
2. Load the required environment variables for the PostgreSQL database connection (PGVECTOR_HOST, PGVECTOR_PORT, PGVECTOR_DATABASE, PGVECTOR_USER, PGVECTOR_PASSWORD).
3. Initialize the Amazon Bedrock client using boto3.client('bedrock').
4. Initialize the text embedding model using BedrockEmbeddings from LangChain, passing the Bedrock client.
5. Create a connection string for the PostgreSQL database using the environment variables.
6. Create an instance of PGVector from LangChain, passing the connection string, embedding function, distance strategy, and the collection name for storing vector embeddings.
7. Add a sample text to the vector store using vector_store.add_texts([text]).
8. Perform a similarity search on the vector store using vector_store.similarity_search(query, k=3), which returns the top 3 most similar texts to the given query. 

# Note:

- Make sure to replace the environment variable names ( PGVECTOR_HOST, PGVECTOR_PORT, PGVECTOR_DATABASE, PGVECTOR_USER, PGVECTOR_PASSWORD) with the appropriate values for your PostgreSQL database running on the EC2 instance.
- The EC2 instance and the Amazon Bedrock service should be in the same VPC to allow communication between them.
- Ensure that the necessary security group rules are in place to allow inbound and outbound traffic between the EC2 instance and the Amazon Bedrock service.
- This code assumes that you have already set up the PostgreSQL database with the pgvector extension enabled and created the necessary tables or collections for storing vector embeddings.

By following this example, you can connect from Amazon Bedrock to a PostgreSQL database running on an EC2 instance in the same VPC, generate vector embeddings using Bedrock, and store and search those embeddings in the PostgreSQL database using the PGVector class from LangChain.
