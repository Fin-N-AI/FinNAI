1️⃣ Spring Server (Main Backend)

**기술 스택**

`Spring Boot 3`, `Spring Data JPA`, `PostgreSQL + PostgresML`, `QueryDSL`, `Swagger`, `Validation`, `Lombok`, `Web`

### ✅ 핵심 기능

1. **회원 관리 (Auth)** 🅱
    - [ ]  회원가입:
        - 회원가입하고 후순위로 OAuth추가할지말지
    - [ ]  로그인
        - JWT 인증 기반으로만 할지 세션 로그인 병행 가능 여부 논의
    - [ ]  로그아웃
    - [ ]  회원탈퇴
2. **유저 서비스**
    - [ ]  파일 업로드 (프로필/리포트 업로드) 🅲
    - [ ]  개인 페이지 조회 (마이페이지) 🅲
    - [ ]  북마크 등록 / 조회 / 삭제 🅳
    - [ ]  관심기업 구독하기 🅳
    - [ ]  구독 알림받기 (WebSocket + Event 기반) 🅳
    - [ ]  기업 검색 (Full-text search + pgvector + PostgresML) 🅱
3. **건의/피드백 게시판** 🅳
    - [ ]  CRUD 기능
    - [ ]  게시글 공개/비공개 설정
    - [ ]  댓글은 관리자만 작성 가능하게 할지 여부 결정 필요
4. **관리자(Admin)**
    - [ ]  사용자 관리 (정지, 삭제, 권한 변경 등) 🅳
    - [ ]  API 사용량 및 상태 관리
    - [ ]  ai 매트릭 조회 (agent가 몇초걸렸는지? )
        - langgraph에서 루프 몇번돌았는지 추적가능하면?

---

### 2️⃣ Python Server (AI Agent & RAG Backend)

> 필요 시 FastAPI 기반으로 확장
> 

## 성능지표 설정 (엄청 중요!)

Ragas + LLM as Judge 🅰+

### ✅ 주요 Agent 기능

1. **기업 최신 뉴스 요약/분석 Agent**  🅱
    - 외부 뉴스 수집 + LLM 요약
2. **기업 상세 지표 조회 Agent**  🅱
    - 재무 지표 비교 분석 (ROE, PER, PSR 등)
3. **기업 공시 정보 분석 Agent**  🅱
    - DART 보고서 분석 및 키포인트 요약
4. **개인 업로드 보고서 분석 Agent**  🅱
    - 사용자가 업로드한 보고서의 LLM 기반 요약 및 인사이트 생성

---

### 3️⃣ 시스템 자동화

1. **Polling** 
    - [ ]  DART 분기보고서 주기적 체크 🅲  ——-
    - [ ]  새로운 보고서 탐지 시 구독자에게 알림 전송 (RabbitMQ 이벤트) 🅳
2. **알림 전송 시스템**
    - WebSocket 기반 알림 스트림 🅳
    - Redis Pub/Sub 또는 RabbitMQ 선택 필요 🅳
    - FCM 🅳

---

### 4️⃣ 모니터링 시스템

1. **LLM API 사용량 모니터링 (업스테이 안된다고함, openai는 가능)** 🅲
2. **API 상태 조회 (Health Check / Latency)** 🅲
3. **AI Agent 매트릭 조회 (성공률, 응답시간 등)** 🅲
4. **대시보드 제작 (Grafana + Prometheus + Loki)** 🅲
5. Loki + Promtail  적용 고려  ****🅲

---

### 5️⃣ 인프라 & CI/CD

1. 도커파일 만들어주기 (환경세팅) 🅰

1. **인프라 구성** 🅲
    - Docker Compose
        - Spring / Python
        - PostgreSQL
    - Prometheus / Grafana
    - RabbitMQ 통합
2. **CI/CD (프론트가 없어서** 🅳라고 생각함)
    - GitHub Actions 기반 배포 자동화
    - Test → Build → Deploy 파이프라인 설계

---

## 🧱 브랜치 전략 / 협업 룰 (요약)

| 구분 | 브랜치 | 머지조건 |
| --- | --- | --- |
| 배포 | `main` | 4명 승인 |
| 개발 | `dev` | 1명 이상 승인 |
| 기능 | `feat/{티켓번호}` | 이슈 연결 필수 |

---

## 🧾 커밋 컨벤션

| 타입 | 설명 |
| --- | --- |
| feat | 새로운 기능 추가 |
| fix | 버그 수정 |
| docs | 문서 수정 |
| ref | 리팩토링 |
| test | 테스트 관련 |
| cicd | CI/CD 관련 |
| style | 포맷/주석 등 스타일 변경 |
| ai | LLM, Agent, Embedding 등 AI 관련 기능 |
| exp | AI 관련 학습, 테스트, 추론등 실험한 기능 - 프로덕션 포함 X |
| chore | 기타 변경사항 |

---

## ✨ 우선순위 제안

| 우선순위 | 태그 |  |
| --- | --- | --- |
| 🅰 | A |  |
| 🅱 | B |  |
| 🅲 | C |  |
| 🅳 | D |  |
|  |  |  |
