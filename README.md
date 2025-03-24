# Sentiment Analysis Web Application

A full-stack web application that performs real-time sentiment analysis on text using a fine-tuned DistilBERT model. The application provides instant feedback on whether input text has a positive, negative, or neutral sentiment.

FOR NOW USE VIEWING IN RAW TO SEE DIAGRAM MEANINGFULLY

## Technical Stack & Skills Demonstrated

### Frontend
- React.js for dynamic UI
- Modern React Hooks and State Management
- Responsive Design
- Real-time API Integration

### Backend
- Flask REST API
- JWT Authentication System
- Rate Limiting Implementation
- RESTful Architecture

### Machine Learning
- HuggingFace Transformers
- DistilBERT Model Fine-tuning
- Real-time Inference
- Confidence Thresholding

### DevOps
- Docker Containerization
- Docker Compose for Multi-container Management
- Environment Configuration
- Network Security

                             
```
                           APPLICATION FLOW & COMPONENTS
    ┌─────────┐     ┌─────────────┐     ╔════════════════════════════════════╗       
    │  USER   │◀───│   REACT     │◀────║           FLASK BACKEND            ║       
    │ INPUT ⏎ │===▶│  FRONTEND   │====▶║ ┌─────────────────────────────┐   ║       
    └─────────┘     └─────────────┘     ║ │      JWT Auth (auth.py)     │   ║       
    [RESULT ✓]                          ║ │   - Access & Refresh Tokens  │  ║       
                                        ║ │   - Protected Routes         │  ║       
                                        ║ └─────────────────────────────┘   ║       
                                        ║ ┌─────────────────────────────┐   ║       
                                        ║ │        Rate Limiter         │   ║       
                                        ║ │  - 200/day, 50/hour limit   │   ║       
                                        ║ └─────────────────────────────┘   ║       
                                        ║ ┌─────────────────────────────┐   ║       
                                        ║ │    Sentiment Analysis       │   ║       
                                        ║ │  (fineTunedSentimentModel)  │   ║       
                                        ║ │   - DistilBERT Transformer  │   ║       
                                        ║ └─────────────────────────────┘   ║       
                                        ╚═══════════════════════════════════╝       
    Input Flow:  ====▶  (Text input for analysis)
    Output Flow: ----▶  (Sentiment analysis result)
```

```
                              DEPLOYMENT & CONTAINER ARCHITECTURE

    ┌─────────────────────────────  Docker Compose  ────────────────────────────┐
    │                                                                           │
    │    ┌────────────────────┐                   ┌────────────────────┐       │
    │    │ Frontend Container │                   │ Backend Container  │       │
    │    │    (frontend)      │                   │    (backend)       │       │
    │    │ ┌──────────────┐   │                   │ ┌──────────────┐   │       │
    │    │ │   React App  │   │◀─── app_network ─▶│ │  Flask API   │   │       │
    │    │ │  Port 5173   │   │                   │ │  Port 5000   │   │       │
    │    │ └──────────────┘   │                   │ └──────────────┘   │       │
    │    │                    │                   │     (.env)         │       │
    │    │ Build: ./frontend  │                   │ Build: . (dev)     │       │
    │    │ Depends on:        │                   │                    │       │
    │    │   - backend        │                   │                    │       │
    │    └────────────────────┘                   └────────────────────┘       │
    │                                                                          │
    │    Networks:                                                            │
    │    └─ app_network (bridge driver)                                       │
    └──────────────────────────────────────────────────────────────────────────┘

    Container Communication: ◀─────────▶  (via app_network bridge network)

```

## Key Features

1. **Secure Authentication**
   - JWT-based authentication system
   - Access and refresh token mechanism
   - Protected API endpoints

2. **Rate Limiting**
   - Prevents API abuse
   - Configurable limits per endpoint
   - IP-based tracking

3. **Sentiment Analysis**
   - Real-time text analysis
   - Three-way classification (Positive/Negative/Neutral)
   - Confidence scoring
   - Configurable thresholds for better accuracy

4. **Containerized Deployment**
   - Isolated frontend and backend containers
   - Secure network configuration
   - Environment-based configuration
   - Easy deployment with Docker Compose

## Local Development Setup

1. Clone the repository:
   ```bash
   git clone [repository-url]
   cd sentimentanalysisproject
   ```

2. Set up environment variables:
   ```bash
   # Create .env file with required variables:
   JWT_SECRET=yourSecret
   TOKEN_EXP=3600
   REFRESH_EXP=86400
   ADMIN_USERNAME=admin
   ADMIN_PASSWORD=yourPassword
   MODEL_PATH=yourModelPath
   NEUTRAL_THRESHOLD=0.30
   CERTAINTY_THRESHOLD=0.65
   ```

3. Build and run with Docker:
   ```bash
   docker-compose up --build
   ```

4. Access the application:
   - Frontend: http://localhost:5173
   - Backend API: http://localhost:5000

## API Documentation

### Authentication Endpoints
- POST `/api/auth/login`: Login with username/password
- POST `/api/auth/logout`: Logout and invalidate tokens
- POST `/api/auth/refresh`: Refresh access token

### Sentiment Analysis Endpoint
- POST `/api/analyze`: Analyze text sentiment
  - Request Body: `{"text": "your text here"}`
  - Response: `{"sentiment": "positive/negative/neutral", "scores": [0.1, 0.2, 0.7]}`

## Future Improvements

Potential areas for enhancement:
- Enhanced detection of neutral sentiment 
- Multi-language support
- Enhanced error handling
- User feedback collection

## Detailed Setup Instructions

### Environment Setup

1. Copy the environment template:
   ```bash
   cp .env.example .env
   ```

2. Update the `.env` file with your secure values:
   - Generate a secure `JWT_SECRET` (you can use `openssl rand -hex 32`)
   - Set your admin credentials
   - Adjust thresholds if needed
   - Set appropriate CORS origins for your deployment

### Model Setup

The sentiment analysis model files are not included in the repository due to size. To set up the model:

1. Download the fine-tuned model files from Hugging Face.
2. Place the model files in the `fineTunedSentimentModel` directory (or whatever you want to call it).
3. Ensure the `MODEL_PATH` in your `.env` points to this directory
