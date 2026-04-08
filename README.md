# CARe - 블록체인 기반 외국인 차량 렌탈 플랫폼

<div align="center">

![CARe Logo](https://img.shields.io/badge/CARe-Blockchain%20Car%20Rental-blue?style=for-the-badge)

**AI 신원 인증 + 블록체인 스마트 계약 기반 해외 렌트 서비스**

[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.0-6DB33F?style=flat-square&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.28-363636?style=flat-square&logo=solidity&logoColor=white)](https://soliditylang.org)
[![Polygon](https://img.shields.io/badge/Polygon-Amoy-8247E5?style=flat-square&logo=polygon&logoColor=white)](https://polygon.technology)

</div>

---

## 목차

- [프로젝트 소개](#-프로젝트-소개)
- [주요 기능](#-주요-기능)
- [시스템 아키텍처](#-시스템-아키텍처)
- [기술 스택](#-기술-스택)
- [블록체인 구성](#-블록체인-구성)
- [팀원 소개](#-팀원-소개)
- [프로젝트 구조](#-프로젝트-구조)
- [시작하기](#-시작하기)

---

## 프로젝트 소개

**CARe**는 해외 렌트 시 여권과 국제운전면허증만으로 간편하게 차량을 렌탈할 수 있는 서비스입니다.

기존 렌탈 과정의 문제점을 해결합니다.

| 문제 | CARe의 해결책 |
|------|--------------|
| 신원 확인의 어려움 | AI OCR + 안면 인식으로 자동 신원 인증 |
| 분쟁 발생 시 증거 불투명 | 렌탈 전·후 차량 손상 AI 비교 + 블록체인 기록 |
| 계약 신뢰성 부족 | 스마트 컨트랙트로 양측 동의 기반 분쟁 해결 |
| 복잡한 결제/보증금 처리 | CARE 토큰 (ERC-20) 기반 디지털 결제 |

---

## 주요 기능

### 신원 인증 (DID + VC)
- 여권 및 국제운전면허증 **Claude Vision OCR** 자동 추출
- **DeepFace(VGG-Face)** 기반 셀피 ↔ 면허증 사진 안면 대조
- W3C 표준 Verifiable Credential 발급 → IPFS 업로드 → 온체인 DID 등록

### AI 차량 손상 검사
- 렌탈 전·후 차량 이미지 **ResNet50** 특징 벡터 추출
- 코사인 유사도 + L1 차이 점수로 손상 정량화
- **YOLO** 기반 차량/번호판 탐지

### 블록체인 분쟁 해결
- 렌터(고객)와 렌탈 업체 양측 서명이 모두 필요한 온체인 분쟁 합의
- 불변한 분쟁 기록 → 투명한 정산
- **Polygon Amoy** 테스트넷 배포

### 스마트 차량 접근
- QR 코드 기반 디지털 스마트키
- WebSocket 실시간 차량 상태 업데이트

### 다국어 지원
- i18next 기반 한국어 / 영어 UI 전환

---

## 시스템 아키텍처

```
┌─────────────────┐    ┌─────────────────┐
│  Renter App     │    │  Company Admin  │
│  (React PWA)    │    │  (React Web)    │
│  + Privy Wallet │    │  + Three.js 3D  │
└────────┬────────┘    └────────┬────────┘
         │                     │
         └──────────┬──────────┘
                    │ HTTPS
         ┌──────────▼──────────┐
         │   Nginx (Infra)     │
         └──────────┬──────────┘
                    │
         ┌──────────▼──────────┐
         │  Spring Boot API    │
         │  + WebSocket        │
         │  + Web3j (Polygon)  │
         └──────┬───────┬──────┘
                │       │
    ┌───────────▼──┐  ┌─▼──────────────┐
    │  FastAPI AI  │  │  Polygon Amoy  │
    │  - ResNet50  │  │  - CarNFT      │
    │  - DeepFace  │  │  - CareToken   │
    │  - OCR       │  │  - DIDRegistry │
    └──────────────┘  │  - Dispute     │
                      └────────────────┘
         ┌────────────────────────────┐
         │  MySQL │ Redis │ AWS S3    │
         │  IPFS (Pinata)            │
         └────────────────────────────┘
```

---

## 기술 스택

### Frontend

| 구분 | 기술 |
|------|------|
| **Renter App** | React 19, Vite 7, react-router-dom v7 |
| **Company Admin** | React 18, Vite 5, Three.js |
| **지갑 연동** | Privy (`@privy-io/react-auth`), Ethers.js v6 |
| **PWA** | vite-plugin-pwa |
| **번호판 스캔** | HuggingFace Transformers (ONNX/WebAssembly) |
| **다국어** | i18next |
| **통신** | Axios, SSE (fetch-event-source) |

### Backend

| 구분 | 기술 |
|------|------|
| **프레임워크** | Spring Boot 3.5.0, Java 17 |
| **보안** | Spring Security, JWT (jjwt 0.11.5) |
| **DB** | Spring Data JPA, MySQL 8, Redis 7 |
| **블록체인** | Web3j 4.12.2 (Polygon Amoy) |
| **스토리지** | AWS S3 SDK v2, Pinata (IPFS) |
| **실시간** | WebSocket |
| **문서화** | SpringDoc OpenAPI (Swagger) |

### AI

| 구분 | 기술 |
|------|------|
| **프레임워크** | FastAPI, PyTorch 2.6 (CUDA 12.4) |
| **손상 감지** | ResNet50 (cosine similarity + L1 diff) |
| **안면 인증** | DeepFace 0.0.93, VGG-Face |
| **OCR** | Claude Vision (Anthropic API) |
| **객체 탐지** | Ultralytics YOLO |
| **이미지 처리** | OpenCV, Pillow |

### Blockchain

| 구분 | 기술 |
|------|------|
| **개발 환경** | Hardhat |
| **언어** | Solidity ^0.8.24 |
| **네트워크** | Polygon Amoy Testnet |
| **라이브러리** | OpenZeppelin Contracts v5 |

### Infra / DevOps

| 구분 | 기술 |
|------|------|
| **CI/CD** | Jenkins (release 브랜치 선택적 빌드) |
| **컨테이너** | Docker, Docker Compose |
| **리버스 프록시** | Nginx |

---

## 블록체인 구성

스마트 컨트랙트 4종 (Polygon Amoy 배포)

| 컨트랙트 | 표준 | 설명 |
|----------|------|------|
| `CarNFT.sol` | ERC-721 | 차량을 NFT로 등록 및 관리 |
| `CareToken.sol` | ERC-20 | CARE 토큰 (1억 발행, faucet + burn) |
| `DIDRegistry.sol` | - | 사용자 DID 문서 온체인 해시 등록 |
| `DisputeSettlement.sol` | - | 양측 동의 기반 분쟁 합의 기록 |

---

## 팀원 소개

| 이름 | 역할 | 담당 영역 |
|------|------|----------|
| **정현우** | 팀장 | Backend |
| **조하원** | 팀원 | AI · Frontend |
| **손효지** | 팀원 | Frontend |
| **강희정** | 팀원 | Backend · AI |
| **진혜린** | 팀원 | Backend · 블록체인 |
| **김정훈** | 팀원 | 인프라 · Backend · 블록체인 |

---

## 프로젝트 구조

```
CARe/
├── renter/          # 렌터 React PWA
├── company/         # 업체 관리자 React Web
├── backend/         # Spring Boot REST API
│   └── src/main/java/
│       └── com/care/backend/
│           ├── domain/      # JPA 엔티티
│           ├── service/     # 비즈니스 로직
│           └── controller/  # REST 컨트롤러
├── ai/              # FastAPI AI 서비스
│   └── app/
│       ├── models/  # ResNet50, DeepFace, OCR
│       ├── services/
│       └── api/routes/
├── ai/verify/       # 검증 전용 FastAPI 컨테이너
├── blockchain/      # Hardhat + Solidity 컨트랙트
├── infra/           # Nginx 설정
├── docker-compose.yml
└── Jenkinsfile
```

---

## 시작하기

### 사전 요구사항

- Docker & Docker Compose
- Java 17+
- Node.js 20+
- Python 3.11+
- CUDA 12.4 (AI 서비스, GPU 사용 시)

### 환경 변수 설정

각 서비스 루트에 `.env` 파일을 설정합니다.

**Backend** (`backend/src/main/resources/application.yml`)
```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/care
  redis:
    host: localhost

aws:
  s3:
    bucket: your-bucket-name

web3:
  polygon:
    rpc-url: https://rpc-amoy.polygon.technology
```

**AI** (`ai/.env`)
```env
ANTHROPIC_API_KEY=your-key
AWS_ACCESS_KEY_ID=your-key
AWS_SECRET_ACCESS_KEY=your-key
PINATA_API_KEY=your-key
```

### 실행

```bash
# 인프라 (MySQL, Redis) 실행
docker-compose up -d

# Backend
cd backend && ./gradlew bootRun

# AI 서비스
cd ai && uvicorn app.main:app --reload --port 8000

# Renter Frontend
cd renter && npm install && npm run dev

# Company Frontend
cd company && npm install && npm run dev
```

### 스마트 컨트랙트 배포

```bash
cd blockchain
npm install
npx hardhat compile
npx hardhat run scripts/deploy.js --network amoy
```

---

<div align="center">

SSAFY 14기 특화 프로젝트 | Team CARe

</div>
