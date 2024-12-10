# RAG PDF Chatbot Application :robot: :page_facing_up:

## Table of Contents :bookmark_tabs:
1. [Overview](#overview)
2. [Features](#features)
3. [Setup](#setup)
    - [Prerequisites](#prerequisites)
    - [Environment Variables](#environment-variables)
    - [Vector Search Index](#vector-search-index)
    - [Build and Run](#build-and-run)
4. [API Endpoints](#api-endpoints)
    - [Chat Request](#chat-request)
    - [Chat Stream](#chat-stream)
    - [Load Documents](#load-documents)
    - [Clear Data](#clear-data)
5. [Error Handling](#error-handling)
6. [Logging](#logging)
7. [Contributing](#contributing)
8. [License](#license)

## Overview :rocket:

Welcome to the **RAG PDF Chatbot Application**! Imagine having a smart assistant that knows everything inside your PDFs and can chat with you about it. Whether you're exploring a complex manual, diving into research papers, or just curious about a document, this app brings your PDFs to life. It's all done in a secure, isolated environment, so your data stays private and safe.

## Features :sparkles:

- **Chat with Your PDFs**: Have a question about what's in your PDFs? Just ask! Our chatbot is here to provide answers based on the content of your documents.
- **Live Response Streaming**: Get instant answers as you chat. It's like having a conversation with your documents in real-time!
- **Easy Document Loading**: Add your PDF files effortlessly—whether from a default folder or any URL. It’s a breeze to get your content into the chat.
- **Clear Your Data**: Need a fresh start? Clear out all your old documents with a single click and start with a clean slate.

## Setup :wrench:

### Prerequisites :memo:

Make sure you have the following installed:

- **Java 17 or higher** :coffee:
- **Maven or Gradle** :hammer:
- **MongoDB** (for storing and managing documents) :file_cabinet:

### Environment Variables :earth_americas:

Ensure the following environment variables are set:

- `COLLECTION_NAME`: The name of the MongoDB collection used for storing documents.
- `DATABASE_NAME`: The name of the MongoDB database.
- `PATH_NAME`: Path name for the vector store in MongoDB.
- `INDEX_NAME`: Name of the vector store index.
- `OPENAI_KEY`: Your OpenAI API key for chat model access.
- `CONNECTION_STRING`: MongoDB connection URI.

### Vector Search Index :mag_right:

To run the application, you must create a vector search index for the MongoDB collection. Follow the instructions provided in the [Spring AI Documentation](https://docs.spring.io/spring-ai/reference/api/vectordbs/mongodb.html) to set up the index.

### Build and Run :rocket:

1. **Clone the repository**:
    ```bash
    git clone https://github.com/zarkk01/chatbot.git
    cd chatbot
    ```

2. **Add PDF files** (optional):
    - If you want to load your own PDF files during initialization, place them in the `src/main/resources/docs` folder before running it.

    > **IMPORTANT**  
    > The application will automatically load these PDFs when it starts and will delete them from this folder after the load for security reasons.

3. **Build the application**:
    ```bash
    ./mvnw clean install
    ```

4. **Run the application**:
    ```bash
    ./mvnw spring-boot:run
    ```

## API Endpoints :globe_with_meridians:

### Chat Request :speech_balloon:

- **Endpoint**: `/chat`
- **Method**: `GET`
- **Query Parameter**: `query` - The query to be processed by the chatbot.
- **Description**: Handles a chat request and returns a response based on the provided query.
- **Example Request**:
    ```http
    GET http://localhost:8080/chat?query=What is the phone number of a person in the PDFs?
    ```

### Chat Stream :ocean:

- **Endpoint**: `/chat/stream`
- **Method**: `GET`
- **Query Parameter**: `query` - The query to be processed by the chatbot.
- **Produces**: `text/event-stream`
- **Description**: Streams responses in real-time based on the provided query.
- **Example Request**:
    ```http
    GET http://localhost:8080/chat/stream?query=What is the phone number of a person in the PDFs?
    ```

### Load Documents :page_with_curl:

- **Endpoint**: `/load`
- **Method**: `POST`
- **Query Parameter**: `file` (optional) - URL of the PDF to load. If not provided, loads PDFs from the default location.
- **Description**: Loads documents into the database from a specified URL or the default folder.
- **Example Request**:
    ```http
    POST http://localhost:8080/load?file=https://example.com/sample.pdf
    ```
    Or without the `file` parameter to load from the default folder:
    ```http
    POST http://localhost:8080/load
    ```

### Clear Data :broom:

- **Endpoint**: `/clear`
- **Method**: `POST`
- **Description**: Clears all documents from the database.
- **Example Request**:
    ```http
    POST http://localhost:8080/clear
    ```

## Error Handling :warning:

- **Malformed URL**: Returns a `400 Bad Request` response with an error message if a malformed URL is provided during the load operation.
- **General Errors**: Logs errors and provides appropriate status codes in response.

## Logging :scroll:

The application uses SLF4J with `logback` for logging. Key events are logged at `INFO` and `DEBUG` levels to provide insights into the application's operations.

## Contributing :handshake:

Contributions are welcome! Please fork the repository and submit a pull request with your changes.

## License :memo:

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
