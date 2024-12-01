# RAG Based Medical ChatBot

This project uses Retrieval-Augmented Generation using ChromaDB as the knowledge store and Llama2 as the llm with a custom data set of medical books, to make a chatbot that can help you with quick diagonsis and/or first aid instructions and how to proceed further with medical advice
## Project architecture
![Project architecture](model_architecture.jpg)
### Front end Chat client
The chat client uses a simple web socket architecture, with a basic client 
using html, css and js along with an express.js server to handle the communication between the user and the model. When the server recieves a message from the user, the server checks if the backend is online and if yes sends a request to the backend and sends the response back to the client.
### Backend Model
The backend model consists of an api designed in flask that has the endpoint `/ask` which expects a json body in the following format
```json
{
"question":"I am having high fever and runny nose"
}
```
The flask server sends the querry to ChromaDB which will provide us with information from our datasets that matches with the querry. The flask server then formats the querry and sends it to Llama2 with the appropriate information from ChromaDB. Then it formats the response given by Llama2 and sends it to the express.js server in the format given below
```json
{
"response":"Having high fever and runny nose is a ......"
}
```