# 🤖 AI Chatbot Service

OpenAI GPT를 활용한 실시간 대화형 챗봇 서비스

[![Railway Deploy](https://img.shields.io/badge/Deploy-Railway-blueviolet)](https://your-app.railway.app)
[![Swagger API Docs](https://img.shields.io/badge/API-Swagger-green)](https://your-app.railway.app/swagger-ui.html)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.10-brightgreen)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16.13-blue)](https://www.postgresql.org/)

## 📋 목차

- [프로젝트 소개](#-프로젝트-소개)
- [주요 기능](#-주요-기능)
- [기술 스택](#-기술-스택)
- [시스템 아키텍처](#-시스템-아키텍처)
- [프로젝트 구조](#-프로젝트-구조)
- [API 문서](#-api-문서)

---

## 🎯 프로젝트 소개

**AI Chatbot Service**는 OpenAI의 GPT-3.5 Turbo 모델을 기반으로 한 실시간 대화형 챗봇 서비스입니다.

### 개발 기간
- **2026.02.02 ~ 2026.02.27**

### 개발 인원
- **백엔드 개발자 1명** (오승훈)

### 프로젝트 목표
- Spring Boot 기반 RESTful API 서버 구축
- OpenAI API 연동 및 실시간 스트리밍 응답 구현
- JWT 기반 사용자 인증 시스템 구현
- PostgreSQL을 활용한 대화 이력 관리
- Railway를 통한 클라우드 배포

---

## ✨ 주요 기능

### 1. 사용자 인증
- JWT 기반 회원가입 및 로그인
- 토큰 기반 인증 시스템
- API Key 인증을 통한 보안 강화

### 2. AI 채팅
- OpenAI GPT-3.5 Turbo 모델 활용
- 실시간 SSE(Server-Sent Events) 스트리밍 응답
- 대화 컨텍스트 관리 (최근 10개 메시지)

### 3. 대화 관리
- 대화 이력 저장 및 조회
- 대화 검색 기능
- 대화 삭제 기능
- 사용자별 대화 격리

### 4. API 문서화
- Swagger UI를 통한 인터랙티브 API 문서
- 실시간 API 테스트 지원

---

## 🛠 기술 스택

### Backend
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.10-brightgreen?logo=springboot)
![Java](https://img.shields.io/badge/Java-17-orange?logo=java)
![Spring Security](https://img.shields.io/badge/Spring%20Security-6.2.15-green?logo=springsecurity)
![Spring Data JPA](https://img.shields.io/badge/Spring%20Data%20JPA-3.5.8-green?logo=spring)

### Database
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16.13-blue?logo=postgresql)

### AI
![OpenAI](https://img.shields.io/badge/OpenAI-GPT--3.5%20Turbo-black?logo=openai)

### Authentication
![JWT](https://img.shields.io/badge/JWT-0.12.3-purple?logo=jsonwebtokens)
![BCrypt](https://img.shields.io/badge/BCrypt-Password%20Encryption-red)

### API Documentation
![Swagger](https://img.shields.io/badge/Swagger-SpringDoc%202.3.0-green?logo=swagger)

### Build Tool
![Gradle](https://img.shields.io/badge/Gradle-8.x-blue?logo=gradle)

### Deployment
![Railway](https://img.shields.io/badge/Railway-Cloud%20Deploy-blueviolet?logo=railway)

### Version Control
![Git](https://img.shields.io/badge/Git-Version%20Control-orange?logo=git)
![GitHub](https://img.shields.io/badge/GitHub-Repository-black?logo=github)

---

## 🏗 시스템 아키텍처
```
┌─────────────┐
│   Client    │
│  (Swagger)  │
└──────┬──────┘
       │ HTTPS
       ▼
┌─────────────────────────────────┐
│     Railway (Cloud Platform)     │
│  ┌────────────────────────────┐ │
│  │   Spring Boot Application  │ │
│  │  ┌──────────────────────┐  │ │
│  │  │  Security Layer      │  │ │
│  │  │  - JWT Auth Filter   │  │ │
│  │  │  - API Key Filter    │  │ │
│  │  └──────────────────────┘  │ │
│  │  ┌──────────────────────┐  │ │
│  │  │  Business Layer      │  │ │
│  │  │  - ChatService       │  │ │
│  │  │  - AuthService       │  │ │
│  │  │  - MessageService    │  │ │
│  │  └──────────────────────┘  │ │
│  │  ┌──────────────────────┐  │ │
│  │  │  Data Layer          │  │ │
│  │  │  - JPA Repositories  │  │ │
│  │  └──────────────────────┘  │ │
│  └────────────────────────────┘ │
└─────────────────────────────────┘
       │                    │
       │                    │
       ▼                    ▼
┌─────────────┐      ┌─────────────┐
│ PostgreSQL  │      │  OpenAI API │
│  (Railway)  │      │ GPT-3.5 T.  │
└─────────────┘      └─────────────┘
```

---

## 📁 프로젝트 구조
```
chatbot/
├── src/main/java/com/example/chatbot/
│   ├── chat/                      # 채팅 관련
│   │   ├── controller/
│   │   │   └── ChatController.java
│   │   ├── service/
│   │   │   └── ChatService.java
│   │   ├── repository/
│   │   │   └── ConversationRepository.java
│   │   ├── entity/
│   │   │   └── Conversation.java
│   │   └── dto/
│   │       ├── ChatRequest.java
│   │       ├── ChatResponse.java
│   │       ├── ConversationListResponse.java
│   │       ├── ConversationDetailResponse.java
│   │       └── ConversationDeleteResponse.java
│   │
│   ├── message/                   # 메시지 관련
│   │   ├── service/
│   │   │   └── MessageService.java
│   │   ├── repository/
│   │   │   └── MessageRepository.java
│   │   ├── entity/
│   │   │   ├── Message.java
│   │   │   └── MessageRole.java
│   │   └── dto/
│   │       └── MessageResponse.java
│   │
│   ├── user/                      # 사용자 관련
│   │   ├── controller/
│   │   │   └── AuthController.java
│   │   ├── service/
│   │   │   └── AuthService.java
│   │   ├── repository/
│   │   │   └── UserRepository.java
│   │   ├── entity/
│   │   │   └── User.java
│   │   └── dto/
│   │       ├── SignupRequest.java
│   │       ├── SignupResponse.java
│   │       ├── LoginRequest.java
│   │       └── LoginResponse.java
│   │
│   ├── openAI/                    # OpenAI 연동
│   │   ├── service/
│   │   │   └── OpenAiService.java
│   │   ├── config/
│   │   │   └── OpenAIConfig.java
│   │   └── dto/
│   │       ├── AiMessage.java
│   │       ├── AiRequest.java
│   │       └── AiResponse.java
│   │
│   └── common/                    # 공통 모듈
│       ├── config/
│       │   ├── SecurityConfig.java
│       │   ├── SwaggerConfig.java
│       │   └── WebConfig.java
│       ├── filter/
│       │   └── JwtAuthenticationFilter.java
│       ├── interceptor/
│       │   └── ApiKeyInterceptor.java
│       ├── handler/
│       │   └── GlobalExceptionHandler.java
│       ├── util/
│       │   └── JwtUtil.java
│       ├── entity/
│       │   └── BaseTime.java
│       ├── exception/
│       │   ├── ErrorCode.java
│       │   ├── ConversationAccessDeniedException.java
│       │   ├── BusinessException.java
│       │   ├── ForbiddenException.java
│       │   ├── ConversationNotFoundException.java
│       │   ├── DuplicateLoginIdException.java
│       │   ├── InvalidRequestException.java
│       │   ├── UnauthorizedEx.java
│       │   └── InvalidCredentialsException.java
│       └── dto/
│           └── ErrorResponse.java
│
└── src/main/resources/
    ├── application.yaml
    ├── application-dev.yaml
    └── application-prod.yaml
```

---

## 📚 API 문서

### 배포 서버
- **Base URL**: `https://chatbot-production-0a8c.up.railway.app`
- **Swagger UI**: `https://chatbot-production-0a8c.up.railway.app/swagger-ui/index.html`

### 주요 API 엔드포인트

#### 인증
- `POST /api/auth/signup` - 회원가입
- `POST /api/auth/login` - 로그인

#### 채팅
- `POST /api/chat` - 채팅 (일반)
- `POST /api/chat/stream` - 채팅 (스트리밍)

#### 대화 관리
- `GET /api/chat/conversations` - 내 대화 목록 조회
- `GET /api/chat/conversations/{id}` - 대화 상세 조회
- `DELETE /api/chat/conversations/{id}` - 대화 삭제
- `GET /api/chat/conversations/search?keyword={keyword}` - 대화 검색

### 인증 방법
모든 API 요청 시 다음 헤더 필요:
- `Authorization: Bearer {JWT_TOKEN}`
- `X-API-Key: {API_KEY}`

**📖 자세한 API 사용법**: [Notion 문서](https://www.notion.so/swagger-API-314f2d6d103c8008b09cd2a07ddc4a59)

---


