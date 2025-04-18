# Sentiment Analysis Web Application
<h3>Demo Video Link</h3>
<p align="center">
  <iframe src="https://www.loom.com/share/5b385316680a4e8c98a73ae045c05473?sid=4724d554-e51c-462c-ad09-036f0c80f34d" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen width="100%" height="400"></iframe>
</p>

**This is a public showcase only. No code or implementation details are included.** 

A full-stack web application that performs real-time sentiment analysis on text using a fine-tuned DistilBERT model. The application provides instant feedback on whether input text has a positive, negative, or neutral sentiment. Link to private repo available upon request.

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
    │    │ │   React App  │   │◀── app_network ─▶│ │  Flask API   │   │       │
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

## License

This project is a public showcase only.  
No code, model, or proprietary business logic is included.  
All rights reserved. See LICENSE for details.
