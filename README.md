# 🏷️ msa-project

이 프로젝트는 **Spring Cloud 기반 MSA 구조**와 **Kafka 이벤트 기반 서비스 간 통신**을 학습하기 위해 구현한 실습 프로젝트입니다.  
API Gateway를 통해 단일 진입점을 구성하고 User, Board, Point 서비스를 분리하여 이벤트 기반으로 연동했습니다.

---

# 📌 Project Overview

이 프로젝트는 마이크로서비스 환경에서

- 서비스 간 **책임 분리**
- **이벤트 기반 비동기 통신**
- **API Gateway 기반 단일 진입점**

구조를 학습하기 위해 구현되었습니다.

---

# 🏗 System Architecture

### Architecture Diagram

<img width="1536" height="1024" alt="msa-architecture" src="https://github.com/user-attachments/assets/35a7c33e-40ab-4753-9680-8b02a132c646" />

Client  
↓  
API Gateway  
↓  
Board Service  
↓ (Publish Event)  
Kafka  
↓ (Consume Event)  
User Service / Point Service  

게시글 작성 이벤트 발생 시 Kafka를 통해 다른 서비스가 이벤트를 수신하여 처리합니다.  
또한 게시글 작성 요청 시 Board Service는 Point Service API를 호출하여 포인트 차감을 수행합니다.

---

# 🔧 Services

| Service | Description |
|-------|-------------|
| api-gateway-service | 클라이언트 요청 라우팅 및 JWT 인증 처리 |
| user-service | 사용자 계정 관리 및 게시글 이벤트 기반 활동 점수 처리 |
| board-service | 게시글 CRUD 및 Kafka 이벤트 발행 |
| point-service | 포인트 차감 API 및 Kafka 이벤트 기반 포인트 적립 |

### Service Repository

- https://github.com/k724k/api-gateway-service
- https://github.com/k724k/user-service
- https://github.com/k724k/board-service
- https://github.com/k724k/point-serivce

---

# 🔄 Event Flow

게시글 작성 시 서비스 간 흐름

1️⃣ Client → API Gateway 요청  
2️⃣ Board Service → Point Service API 호출 (포인트 차감)  
3️⃣ 게시글 저장  
4️⃣ Kafka 이벤트 발행  
5️⃣ User Service 이벤트 수신 → 활동 점수 증가  
6️⃣ Point Service 이벤트 수신 → 포인트 적립  

Kafka를 통해 서비스 간 직접적인 의존성을 제거하고  
비동기 이벤트 기반으로 서비스가 동작하도록 설계했습니다.

---

# ⚙️ Tech Stack

<div align="left">

<img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" />
<img src="https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white" />
<img src="https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white" />

<img src="https://img.shields.io/badge/Spring_Cloud_Gateway-6DB33F?style=for-the-badge&logo=spring&logoColor=white" />
<img src="https://img.shields.io/badge/Apache_Kafka-231F20?style=for-the-badge&logo=apachekafka&logoColor=white" />

<img src="https://img.shields.io/badge/MySQL-00000F?style=for-the-badge&logo=mysql&logoColor=white" />
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
<img src="https://img.shields.io/badge/Amazon_AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white" />

</div>

---

# 💡 What I Learned

- MSA 환경에서 **서비스 책임 분리**의 중요성  
- **Kafka 기반 이벤트 아키텍처 설계** 경험  
- 동기 통신(API)과 비동기 통신(Event)의 역할과 차이 이해  
- 서비스 간 **결합도를 낮추는 설계 방법** 습득  
