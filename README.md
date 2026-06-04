# CARe - 블록체인 기반 외국인 차량 렌탈 플랫폼

<div align="center">

![CARe Logo](https://img.shields.io/badge/CARe-Blockchain%20Car%20Rental-blue?style=for-the-badge)

**AI 신원 인증 + 블록체인 스마트 계약 기반 해외 렌트 서비스**

[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=black)](https://react.dev)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.0-6DB33F?style=flat-square&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.24-363636?style=flat-square&logo=solidity&logoColor=white)](https://soliditylang.org)
[![Polygon](https://img.shields.io/badge/Polygon-Amoy-8247E5?style=flat-square&logo=polygon&logoColor=white)](https://polygon.technology)

> **삼성 청년 SW·AI 아카데미 14기 특화 프로젝트** · **Team CARe**<br>
> **플랫폼**: React PWA (Renter) / React Web (Company Admin)<br>
> **개발 인원**: 6명
>
> **여권과 국제운전면허증**만으로 간편하게 차량을 렌탈하고,<br>
> **AI 차량 손상 검사**와 **스마트 컨트랙트 기반 분쟁 해결**로 신뢰를 더하는 해외 차량 렌탈 서비스

</div>

---

## 목차

- [📌 서비스 소개](#service)
- [👥 팀원](#team)
- [✨ 주요 기능](#features)
- [🛠️ 기술 스택](#tech-stack)
- [🏗️ 시스템 아키텍처](#architecture)
- [🔬 핵심 기술 상세](#tech-detail)

---

<a name="service"></a>

## 📌 서비스 소개

**CARe**는 외국인이 해외에서 차량을 렌트할 때 겪는 신원 확인의 어려움과 반납 시 발생하는 차량 손상 분쟁을 혁신적으로 해결하는 플랫폼입니다.

- **타깃**: 해외에서 안전하고 간편하게 차량을 렌트하고자 하는 모든 외국인 여행객 및 렌탈 업체
- **핵심 가치**
    1. 여권 및 면허증 **AI OCR 및 안면 대조 신원 인증**
    2. W3C 표준 기반 **DID + VC(Verifiable Credential) 온체인 관리**
    3. ResNet50 및 코사인 유사도 기반 **차량 손상 정량화 분석**
    4. **Polygon Amoy 온체인 합의**를 통한 투명한 분쟁 해결
- **차별점**: 계약부터 반납, 분쟁 조정까지 모든 이력이 블록체인에 기록되어 위변조가 불가능하며, QR 코드 기반 스마트키 시스템으로 대면 단계를 최소화합니다.

---

<a name="team"></a>

## 👥 팀원

<table>
  <tr>
    <td align="center" width="33%">
      <b>정현우</b><br/>
      <sub>팀장 · BE</sub><br/>
      <sub>@jhw_dev</sub>
    </td>
    <td align="center" width="33%">
      <b>조하원</b><br/>
      <sub>FE · AI</sub><br/>
      <sub>@godhw1018</sub>
    </td>
    <td align="center" width="33%">
      <b>손효지</b><br/>
      <sub>FE</sub><br/>
      <sub>@hyoji0284</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <b>강희정</b><br/>
      <sub>BE · AI</sub><br/>
      <sub>@hj_kang</sub>
    </td>
    <td align="center">
      <b>진혜린</b><br/>
      <sub>BE · Blockchain</sub><br/>
      <sub>@hr_jin</sub>
    </td>
    <td align="center">
      <b>김정훈</b><br/>
      <sub>Infra · BE · BC</sub><br/>
      <sub>@kik1232198</sub>
    </td>
  </tr>
</table>

---

<a name="features"></a>

## ✨ 주요 기능

| 기능 분류 | 핵심 기능 요약 | 상세 구현 및 기술 스택 설명 |
| :--- | :--- | :--- |
| **🪪 신원 인증 (DID + VC)** | 비대면 글로벌 신원 검증 | 여권 및 국제운전면허증을 **Claude Vision OCR**로 자동 추출하고, **DeepFace(VGG-Face)** 기반 셀피 사진 안면 대조를 거쳐 W3C 표준 규격의 VC를 발급합니다. 생성된 문서는 IPFS에 업로드 후 온체인 DID 레지스트리에 등록됩니다. |
| **🚗 AI 차량 손상 검사** | 차량 파손 정량화 분석 | 렌탈 전·후 촬영된 차량 이미지를 **ResNet50** 기반 특징 벡터로 추출하여 코사인 유사도 및 L1 차이 점수로 손상을 정량 분석합니다. 또한 **YOLO**를 활용해 차량 바디 및 번호판 구역을 정밀 탐지합니다. |
| **⚖️ 블록체인 분쟁 합의** | 스마트 계약 기반 분쟁 해결 | 차량 반납 프로세스 중 손상 등으로 발생한 분쟁에 대해 렌터와 대여 업체 양측의 디지털 서명이 결합된 멀티시그 스마트 계약을 발동합니다. 조작 불가능한 온체인 이력으로 투명한 정산을 보장합니다. |
| **🔑 스마트 접근 제어** | QR 기반 디지털 키 관리 | 분산 신원 인증이 완료된 계정을 대상으로 차량 도어를 제어할 수 있는 QR 코드 스마트키를 활성화합니다. **WebSocket** 실시간 통신 파이프라인을 구축하여 차량 개폐 및 상태 변동을 실시간 제어합니다. |
| **🔀 글로벌 인프라** | 다국어 UI 및 디지털 결제 | **i18next** 기반의 다국어 전환 시스템(한국어/영어)을 제공합니다. 보증금 예치 및 결제 시스템은 ERC-20 표준 기반의 **CARE 토큰**을 발행하여 Faucet 및 Burn 메커니즘을 통해 정산 구조를 자동화했습니다. |
| **📦 자산 관리 및 관제** | 차량 NFT 및 3D 웹 관제 | 플랫폼에 등록되는 모든 렌탈 차량을 ERC-721 기반 **NFT 자산**으로 민팅하여 고유 이력을 관리합니다. 대여 업체 대시보드에는 **Three.js** 3D 그래픽 엔진을 탑재하여 차량 현황을 시각적으로 관제합니다. |

---

<a name="tech-stack"></a>

## 🛠️ 기술 스택

| 분류 | 기술 Stack |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Frontend** | ![React](https://img.shields.io/badge/React-19-61DAFB?style=plastic&logo=react&logoColor=black) ![Vite](https://img.shields.io/badge/Vite-7-646CFF?style=plastic&logo=vite&logoColor=white) ![Privy](https://img.shields.io/badge/Privy_Auth-black?style=plastic&logo=web3&logoColor=white) ![Ethers.js](https://img.shields.io/badge/Ethers.js-v6-2B3B95?style=plastic&logo=ethereum&logoColor=white) ![Three.js](https://img.shields.io/badge/Three.js-black?style=plastic&logo=three.js&logoColor=white) ![PWA](https://img.shields.io/badge/PWA-5A0FC8?style=plastic&logo=progressivewebapps&logoColor=white) ![HuggingFace](https://img.shields.io/badge/HuggingFace_ONNX-FFD21E?style=plastic&logo=huggingface&logoColor=black) |
| **Backend** | ![Java](https://img.shields.io/badge/Java-17-ED8B00?style=plastic&logo=openjdk&logoColor=white) ![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5.0-6DB33F?style=plastic&logo=springboot&logoColor=white) ![Spring Data JPA](https://img.shields.io/badge/Spring_Data_JPA-6DB33F?style=plastic&logo=spring&logoColor=white) ![Web3j](https://img.shields.io/badge/Web3j-4.12.2-2F3542?style=plastic&logo=web3&logoColor=white) ![MySQL](https://img.shields.io/badge/MySQL-8-4479A1?style=plastic&logo=mysql&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-7-FF4438?style=plastic&logo=redis&logoColor=white) ![AWS S3](https://img.shields.io/badge/AWS_S3-FF9900?style=plastic&logo=amazonaws&logoColor=white) |
| **AI** | ![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=plastic&logo=python&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=plastic&logo=fastapi&logoColor=white) ![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=plastic&logo=pytorch&logoColor=white) ![DeepFace](https://img.shields.io/badge/DeepFace-0.0.93-FF6B6B?style=plastic) ![YOLO](https://img.shields.io/badge/YOLO_v8-111F68?style=plastic&logo=ultralytics&logoColor=white) ![Claude](https://img.shields.io/badge/Claude_Vision-D97757?style=plastic&logo=anthropic&logoColor=white) |
| **Blockchain** | ![Solidity](https://img.shields.io/badge/Solidity-0.8.24-363636?style=plastic&logo=solidity&logoColor=white) ![Hardhat](https://img.shields.io/badge/Hardhat-FBEE20?style=plastic&logo=hardhat&logoColor=black) ![Polygon](https://img.shields.io/badge/Polygon_Amoy-8247E5?style=plastic&logo=polygon&logoColor=white) ![OpenZeppelin](https://img.shields.io/badge/OpenZeppelin-4E5EE4?style=plastic&logo=openzeppelin&logoColor=white) ![IPFS](https://img.shields.io/badge/IPFS_Pinata-65C2CB?style=plastic&logo=ipfs&logoColor=white) |
| **Infra** | ![Docker Compose](https://img.shields.io/badge/Docker_Compose-2496ED?style=plastic&logo=docker&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=plastic&logo=nginx&logoColor=white) ![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=plastic&logo=jenkins&logoColor=white) |

---

<a name="architecture"></a>

## 🏗️ 시스템 아키텍처

```text
┌────────────────────────────────────────────────────────┐
│                 Web Client Application                 │
│  ┌─────────────────────────┐ ┌──────────────────────┐  │
│  │ Renter App (PWA)        │ │  Company Admin (Web) │  │
│  │  + React 19 / Vite 7    │ │  + React 18 / Vite 5 │  │
│  │  + Privy Wallet         │ │  + Three.js 3D View  │  │
│  └────────────┬────────────┘ └──────────┬───────────┘  │
└───────────────┼─────────────────────────┴──────────────┘
                │ HTTPS (JWT Auth)
         ┌──────▼──────────────┐
         │     Nginx Proxy     │
         └──────┬──────────────┘
                │
         ┌──────▼────────────────────────────────┐
         │         Spring Boot API Server        │
         │   - Spring Data JPA │ Spring Security │
         │   - Web3j Connector │ WebSocket       │
         └──────┬──────────────────────▲─────────┘
                │                      │
                │ HTTP / JSON          │ RPC / Transact.
                │                      │
         ┌──────▼──────────────────────┴─────────┐   ┌───────────────────────────────┐
         │              FastAPI AI Server        │   │     Polygon Amoy Testnet      │
         │   - ResNet50 Feat.  │ DeepFace Match  │   │   - CarNFT      │ CareToken   │
         │   - Claude OCR      │ Ultralytics YOLO│   │   - DIDRegistry │ DisputeSettl.│
         └───────────────────────────────────────┘   └───────────────────────────────┘
         ┌──────────────────────────────────────────────────────────────────────────┐
         │ MySQL 8 │ Redis 7 │ AWS S3 │ IPFS (Pinata 분산 저장소)                     │
         └──────────────────────────────────────────────────────────────────────────┘
```

- 클라이언트 ↔ BE: React PWA(렌터용) 및 React Web(업체 관리자용)이 Nginx 프록시를 통해 Spring Boot API 서버와 HTTPS 통신을 수행하며, Web3 지갑 연동에는 Privy가 활용됩니다.

- BE ↔ AI / Blockchain: Spring Boot가 코어 비즈니스 처리 중 비전/OCR 모델 제어를 위해 FastAPI를 호출하며, 온체인 스마트 계약 연동 및 DID 검증은 Web3j 라이브러리를 통해 Polygon Amoy Testnet과 연결됩니다.

- 데이터 저장소: 메타데이터는 MySQL과 Redis에 저장되며, DID 자격증명 문서(VC)와 원본 손상 이미지는 분산 파일 시스템인 IPFS(Pinata) 및 AWS S3에 물리적으로 격리 분할 저장됩니다.


## 🔬 핵심 기술 상세
### 🪪 분산 신원 인증 및 자격증명 (DID & VC)
외국인 신원 식별의 불투명성을 제거하기 위해 W3C 글로벌 표준 규격의 분산 신원인증 아키텍처를 도입했습니다.

사용자가 여권 및 국제면허증을 업로드하면 고성능 비전 LLM인 Claude Vision API가 다국어 텍스트 레이아웃을 바이어스 없이 클렌징하여 OCR 매핑을 처리합니다.

추출된 데이터 정보는 DeepFace(VGG-Face) 코어의 특징점 비교 모델을 통해 실시간 라이브 셀피 이미지와 일치 여부를 판단하며, 성공 시 암호학적으로 서명된 Verifiable Credential(VC)을 생성해 IPFS에 바인딩하고 해시값을 온체인 DIDRegistry.sol에 등록합니다.

### 🚗 컴퓨터 비전 기반 차량 손상 정량화 (ResNet50 & YOLO)
차량의 사후 렌탈 분쟁을 원천 방지하기 위해 정밀 비교 알고리즘 파이프라인을 구축했습니다.

차량 인계 시점과 반납 시점에 촬영된 교차 검증 타깃 이미지는 YOLO(Ultralytics) 엔진이 번호판 및 차량 바디 오브젝트 영역을 관심 구역(ROI)으로 타이트하게 검출합니다.

바운딩 박싱 처리된 가공 이미지는 ResNet50 딥러닝 백본 네트워크를 거쳐 고차원 특징 벡터(Feature Vector)로 변환됩니다. 이후 벡터 간의 코사인 유사도(Cosine Similarity) 연산 및 L1-Norm 픽셀 오차 분석 계수를 연계해 미세 스크래치 및 찌그러짐을 수치적으로 정량화합니다.

### 📜 스마트 컨트랙트 기반 온체인 합의 (Solidity)
중앙 집중형 렌탈 서버의 데이터 변조 우려를 해소하기 위해 독립된 컨트랙트 아키텍처를 설계했습니다.

총 4종의 코어 컨트랙트(CarNFT, CareToken, DIDRegistry, DisputeSettlement)를 유기적으로 오케스트레이션합니다.

특히 반납 시 발생하는 수리비 정산 및 분쟁 발생 시, 중앙 관리자 개입 없이 오직 스마트 계약상에 기록된 렌터와 업체 양측의 Multi-Sig 기반 합의 트랜잭션이 블록체인 네트워크에 마이그레이션 및 컨펌되어야 보증금 락업 해제 및 토큰 정산이 최종 발동되도록 탈중앙화 거버넌스를 보장합니다.

## 🚀 시작하기

### 1. 인프라 환경 구축

```
# 인프라 핵심 컨테이너(MySQL, Redis) 백그라운드 구동
cd infra
docker-compose up -d
```

### 2. Backend (Spring Boot)
`backend/src/main/resources/application.yml` 파일에 데이터베이스, S3, Web3 rpc 주소를 알맞게 주입합니다.

```
cd backend
./gradlew bootRun
```

### 3. AI 서비스 (FastAPI)
ai/.env 파일 내에 ANTHROPIC_API_KEY 및 AWS, Pinata 자격 증명을 입력합니다.

```
cd ai
uvicorn app.main:app --reload --port 8000
```

### 4. Frontend (Renter & Company)

```
# Renter PWA 실행
cd renter
npm install && npm run dev

# Company Web Admin 실행
cd company
npm install && npm run dev
```

### 5. Smart Contract 배포

```
cd blockchain
npm install
npx hardhat compile
npx hardhat run scripts/deploy.js --network amoy
```

## 📁 프로젝트 구조

```
CARe/
├── renter/          # 렌터 전용 모바일 최적화 React PWA
├── company/         # 대여 업체 관리자용 대시보드 React Web (Three.js 내장)
├── backend/         # Spring Boot 핵심 비즈니스 로직 및 Web3j 통신 서버
│   └── src/main/java/com/care/backend/
│       ├── domain/      # JPA 엔티티 레이어
│       ├── service/     # 트랜잭션 서비스 비즈니스 레이어
│       └── controller/  # RESTful 엔드포인트 제어 레이어
├── ai/              # FastAPI 코어 AI 마이크로서비스 (DeepFace, ResNet50, OCR 통합)
├── ai/verify/       # 신원 및 손상 이미지 교차 검증 전용 경량 모듈 컨테이너
├── blockchain/      # Hardhat 환경 기반 Solidity 스마트 컨트랙트 자산 코드
├── infra/           # Nginx 역방향 프록시 및 배포용 오케스트레이션 구성 파일
├── docker-compose.yml
└── Jenkinsfile      # 자동화 통합 파이프라인 스크립트
```

## 🌿 개발 프로세스 및 규칙

### 브랜치 전략
```
master   ← 최종 배포 (릴리스 버전 태그 관리)
  ▲
release  ← 통합 QA 테스트 및 프로덕션 검증 단계
  ▲
develop  ← 전체 기능 피처 피드 통합 브랜치
피처 브랜치 명명 구조: {fe / be / ai / infra}/feature-{기능 요약}-{이슈번호}
```

- 이슈 예시: be/feature-did-integration-S14P31S309-402

- 커밋 메시지 규칙

```
[#이슈번호] {유형}: {변경 사항 기술}
```

- feature: 새로운 기능 모듈의 빌드 및 도입

- fix: 코드 논리 예외 및 버그 트래킹 수정

- docs: 마크다운 가이드라인 및 프로젝트 위키 수정

- refactor: 가독성 중심의 코드 리팩토링 및 청소

- design: UI 레이아웃, CSS, 마크업 아키텍처 보완

SSAFY 14기 특화 프로젝트 | Team CARe
