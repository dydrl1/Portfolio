# [백엔드 개발자] 이용기
# 🌟 갓생로그 (GodLife Project)
> 일상을 더 의미 있게! 루틴 공유형 챌린지 플랫폼  
> React + Spring Boot 기반의 **루틴·챌린지 관리 서비스**

---

## 🧾 소개

**갓생로그(GodLife Project)** 는 사용자가 자신의 루틴과 챌린지를 기록하고,  
다른 사람들과 공유하며 함께 성장할 수 있도록 돕는 웹 서비스입니다.

일상 목표를 설정하고 인증하며,  
공개/비공개 설정을 통해 자신만의 루틴을 관리할 수 있습니다.

**백엔드 개발을 담당**했으며,  
프론트엔드 팀원과 협업하여 **기획 → 개발 → 배포** 전 과정을 진행했습니다.

---

## 🗓️ 개발 기간

> 2025.01.15 ~ 2025.05.30 (약 4개월)

---

## 👥 개발 인원

> 총 4명 (프론트엔드 2명, 백엔드 2명)

---

## 💼 담당 주요 업무

- Spring Boot + MyBatis + MariaDB 기반 **REST API 개발**
- **ERD 설계**, API 명세서 작성
- **챌린지, 계획(Plan), 인증(Verification), 유저(User), 신고(Report)** 등 주요 도메인 설계 및 개발
- **Redis 캐시**를 활용한 조회 성능 개선
- **스케줄러 기반 상태 자동 업데이트 로직** 구현 (챌린지 종료 처리)
- **AWS EC2 + Docker + Nginx + GitHub Actions** 기반 CI/CD 구축 및 배포 자동화

---

## ⚙️ 주요 개발 내용

- **JWT 인증 및 토큰 갱신 로직** 구현  
  → Access / Refresh Token 구조 및 Redis 기반 로그아웃 관리

- **챌린지 공개(PUBLIC) / 비공개(PRIVATE) 설정 기능**  
  → 관리자는 모든 챌린지 접근 가능, 일반 유저는 공개 챌린지만 조회 가능

- **이벤트성 챌린지(SPECIAL) / 일반 챌린지(NORMAL)** 타입 구분  
  → 관리자가 SPECIAL 챌린지를 등록하여 기간 한정 이벤트 운영 가능

- **Redis 캐시 구조 설계**  
  → 챌린지 목록 / 카테고리 목록 / FAQ 목록 캐싱 → 조회 속도 약 40% 개선

- **MyBatis + 동적 SQL** 기반 필터링 검색  
  → 카테고리, 상태, 공개 여부, 챌린지 타입 등 복합 조건 검색 지원

- **Spring Scheduler** 기반 종료 상태 자동 변경 로직  
  → 매일 자정, 종료 조건에 맞는 챌린지를 자동으로 `END` 상태로 변경

- **관리자 페이지 API**  
  → FAQ, QnA, 신고 관리, 유저 정지/해제 기능 구현

- **CI/CD 구축**
  - GitHub Actions → Docker 이미지 빌드 → Nginx Reverse Proxy를 통한 Blue-Green 배포  
  - Branch Protection + Pull Request 기반 협업 적용

---

## 🚨 트러블슈팅

- **Redis 연결 오류 (`RedisConnectionFailureException`)**  
  → `bind 127.0.0.1` 설정 해제 및 `protected-mode no` 적용으로 해결  
  → 복구 후 캐시 무효화 처리로 데이터 일관성 유지

- **스케줄러가 종료된 챌린지를 갱신하지 않던 문제**  
  → SQL 조건문(`chall_end_time < NOW()`) 누락 확인 및 수정

- **CORS 문제 해결**  
  → Nginx Reverse Proxy 설정으로 `Access-Control-Allow-Origin` 헤더 일괄 관리

- **MariaDB → Redis 동시 갱신 시 데이터 불일치**  
  → 캐시 무효화 전략(Cache Evict) 패턴 적용으로 해결

- **배포 중 Docker 네트워크 충돌 이슈**  
  → 각 컨테이너별 명시적 네트워크 설정 및 `depends_on`으로 해결

---

## 🧠 사용 기술

| 분야 | 기술 스택 |
|------|------------|
| **Framework** | Spring Boot 3.x, MyBatis, Spring Security, Spring Scheduler |
| **Database** | MariaDB, Redis |
| **Infra** | AWS EC2, Docker, Nginx, GitHub Actions |
| **Frontend 협업** | React, Axios, TailwindCSS |
| **Testing & Docs** | JUnit5, Swagger, Postman |
| **Monitoring** | Spring Actuator, EC2 Metrics |
| **Tools** | IntelliJ, Notion, Git, Figma |

---

## 🧩 시스템 아키텍처

```plaintext
[React Frontend]
       ↓ Axios
[Spring Boot API Server]
       ↓ MyBatis
[MariaDB] ←→ [Redis]
       ↑
[Docker + Nginx + GitHub Actions (CI/CD)]
