# AI chatbot Backend

## Overview
This backend powers a real-time chat application that supports:
- User authentication with JWT
- Real-time messaging using WebSockets (STOMP)
- AI-generated responses using OpenAI API
- Persistent conversation & message storage in PostgreSQL
- Input filtering, sanitization, and rate limiting
- Async processing for AI replies

It exposes secure REST endpoints and STOMP WebSocket channels.

## Features
- Register & Login (email + username + password)
- JWT-based authentication
- Create & list conversations
- Paginated message history
- Send/receive real-time messages
- AI responds asynchronously
- WebSocket reconnect support (frontend)
- Filters for unsafe or abusive content
- Prompt injection protection

## Tech Stack
- Java 17
- Spring Boot 3.x
- Spring Web / Security / WebSocket / Data JPA
- PostgreSQL
- Lombok
- OpenAI Java SDK
- JWT (custom utility)
- Maven

## Project Structure

src/main/java/com/example/chat/
│
├── config/                  # security, websockets, async, cors, ai
├── controller/              # REST + WebSocket controllers
├── dto/                     # transfer objects
├── entity/                  # JPA entities
├── repository/              # Spring Data repositories
├── service/                 # Auth, AI logic
├── util/                    # JWT, sanitizers, filters, rate limiter
└── exception/               # Global exception handler

## WebSocket Endpoints
Server WebSocket URL:

ws://localhost:8080/ws

### Client → Server (send messages)

/app/chat

### Server → Client (AI & user responses)

/topic/conversations/{conversationId}

## REST API Endpoints

### Authentication

POST /auth/register
POST /auth/login

### User
GET /user/me

### Conversations
POST /conversations/create?title=NewChat
GET /conversations

### Messages (with pagination)
GET /messages/{conversationId}?page=0&size=15

## Database Configuration
Set in `application.properties`:

spring.datasource.url=jdbc:postgresql://localhost:5432/chatdb
spring.datasource.username=chatuser
spring.datasource.password=chatpassword
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

## Running the Backend

### 1. Start PostgreSQL using Docker
docker-compose up -d

### 2. Run Spring Boot
mvn spring-boot:run

Backend runs on:
http://localhost:8080

## Environment Variables
Set OpenAI key:

OPENAI_API_KEY=your_key_here

## Build Commands
mvn clean install
mvn spring-boot:run


