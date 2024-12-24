# Plagiarism Check API with Flask and Docker

A REST API built with Flask that checks text similarity between two pieces of text. The API uses MongoDB for data storage, includes user authentication, and a token-based system for API usage.

## Features

- User Registration
- Text Similarity Check
- Token-based API Usage
- Admin Token Refill System
- Secure Password Hashing
- Dockerized Application
- MongoDB Integration

## Prerequisites

- Python 3.11 or higher
- Docker and Docker Compose
- MongoDB
- Git

## Project Structure
flask-api-docker-plagiarism-check/
├── web/
│ ├── app.py
│ ├── requirements.txt
│ └── Dockerfile
├── docker-compose.yml
└── README.md


## Installation & Setup

1. Clone the repository:
git clone <repository-url>
cd flask-api-docker-plagiarism-check

Create a virtual environment (optional but recommended):

python -m venv myenv
# For Windows
myenv\Scripts\activate
# For Unix or MacOS
source myenv/bin/activate

Install required packages:

pip install Flask
pip install flask_restful
pip install pymongo
pip install bcrypt
pip install spacy

Download spaCy English language model:

python -m spacy download en_core_web_sm

Docker Setup
Build and run the containers:

docker compose up --build

To stop the containers:

docker compose down

Insert at cursor
bash
API Endpoints
1. Register User
Endpoint: /register

Method: POST

Body:

{
    "username": "your_username",
    "password": "your_password"
}

json
Response:

{
    "status": 200,
    "msg": "You successfully signed up for the API"
}

json
2. Check Text Similarity
Endpoint: /similarity

Method: POST

Body:

{
    "username": "your_username",
    "password": "your_password",
    "text1": "First text to compare",
    "text2": "Second text to compare"
}

json
Response:

{
    "status": 200,
    "similarity": 0.8,
    "msg": "Similarity successfully checked"
}

json
3. Refill Tokens
Endpoint: /refill

Method: POST

Body:

{
    "username": "your_username",
    "admin_pw": "abc123",
    "refill": 10
}

json
Response:

{
    "status": 200,
    "msg": "Refilled successfully"
}

json
Testing the API
You can test the API using curl or Postman:

Register a new user:

curl -X POST http://localhost:5000/register \
-H "Content-Type: application/json" \
-d '{"username":"testuser", "password":"testpass"}'

Check text similarity:

curl -X POST http://localhost:5000/similarity \
-H "Content-Type: application/json" \
-d '{
    "username": "testuser",
    "password": "testpass",
    "text1": "The quick brown fox",
    "text2": "The fast brown fox"
}'

Refill tokens:

curl -X POST http://localhost:5000/refill \
-H "Content-Type: application/json" \
-d '{
    "username": "testuser",
    "admin_pw": "abc123",
    "refill": 10
}'

Important Notes
Each new user starts with 6 tokens

Each similarity check costs 1 token

Only admin can refill tokens (admin password: abc123)

Passwords are securely hashed using bcrypt

The API uses spaCy's language model for text similarity comparison

Error Codes
200: Success

301: Invalid Username

302: Incorrect Password

303: Out of Tokens

304: Invalid Admin Password

Security Considerations
Admin password should be changed in production

Use environment variables for sensitive data

Implement rate limiting in production

Use HTTPS in production

Consider implementing JWT for better authentication

Development
To run the application in development mode:

Without Docker:

python app.py

With Docker:

docker compose up --build

Troubleshooting
If you encounter MongoDB connection issues:

Ensure MongoDB service is running

Check if the MongoDB container is up

Verify the connection string in app.py

For spaCy model issues:

Ensure the model is downloaded

Try reinstalling spaCy and the model
