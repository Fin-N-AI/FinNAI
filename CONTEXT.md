다음 회의 떄 해야할 것들

# 이슈 템플릿 만들기

[우선순위] 간단한 설명
  
예시:
[A] 임베딩 대용량 처리 기능 추가
[B] 아이콘 클릭 시 활성화 표시
[C] API 문서 작성
[D] 성능 최적화 검토

## 우선순위
- [ ] A - 당장 해야 할 일 (긴급)
- [ ] B - 오늘 안에
- [ ] C - 이번 주 안에 (평일)
- [ ] D - 이번 달 안에

## 담당자
- Assignee: @username (1명만 지정)

## 이슈 설명
### 왜 이 이슈가 필요한가?
(이유 작성)

### 작업 내용
- [ ] 할 일 1
- [ ] 할 일 2

## 예상 일정
- 시작일: YYYY-MM-DD
- 완료 예정일: YYYY-MM-DD
  - A: 당일
  - B: 오늘 안(24시간 이내)
  - C: 이번 주 금요일까지
  - D: 이번 달 말일까지

## 추가 정보 (선택)
- 고객 시나리오: 
- 참고 자료: 
- 관련 이슈: #이슈번호
```

---

## GitHub Labels 설정
```
우선순위 라벨:
🔴 priority-A (당장, 긴급)      - 색상: #d73a4a (빨강)
🟠 priority-B (오늘 안)         - 색상: #ff9800 (주황)
🟡 priority-C (이번 주)         - 색상: #fbca04 (노랑)
🟢 priority-D (이번 달)         - 색상: #0e8a16 (초록)

PR 템플릿
markdown## 관련 이슈 (필수)
Closes #이슈번호

## 담당자 (필수)
- Author: @작성자
- Reviewer: @리뷰어

## 변경 사항
무엇을 변경했나요?

## 테스트 (필수)
### 실행 방법
```bash
실행 명령어 또는 테스트 방법
```

### 실행 결과
```
예상 결과:
실제 결과:
```

## 작업 기간
- 시작: YYYY-MM-DD
- 종료: YYYY-MM-DD
```

---

# 브랜치 전략
```
main (prod)
  ↑ 
  ├─ 머지 조건: 4명 전원 Approve 필요
  │
dev
  ↑
  ├─ 머지 조건: 1명 이상 Approve
  │
feature/#이슈번호-설명
hotfix/#이슈번호-설명


# 기능 개발
feature/#23-login
feature/#45-icon-active

# 버그 수정
hotfix/#67-api-error
hotfix/#89-timeout
```

## 작업 흐름
```
1. 이슈 생성 → GitHub가 #번호 자동 부여

2. 브랜치 생성
   git checkout -b feature/#23-login

3. 작업 & 커밋
   git commit -m "feat(#23): 로그인 기능 추가"

4. PR 생성 (dev 브랜치로)
   - 1명 이상 Approve → dev 머지

5. dev → prod PR
   - 4명 전원 Approve → prod 머지
```

## 머지 규칙
```
feature/#번호 → dev
- 1명 이상 Approve 필요
- 담당자가 머지 버튼 클릭

dev → prod
- 4명 전원 Approve 필요
- 마지막 승인자가 머지

긴급 수정 (hotfix):
- prod에서 직접 브랜치 생성
- hotfix/#번호-설명
- 2명 이상 Approve → prod 직접 머지
- 이후 dev로 체리픽
```

## 이슈-담당자 규칙
```
✅ 이슈 담당:
- 1개 이슈 = 1명 담당자
- Assignee로 지정

✅ PR 리뷰:
- 담당자가 PR 생성
- 다른 팀원이 리뷰
- 문제 발견 시:
  - 리뷰어가 코멘트
  - 담당자가 수정
  - 재리뷰 요청

❌ 금지 사항:
- 담당자 외 다른 사람이 해당 브랜치에 커밋 금지
- 본인 PR 본인 Approve 금지
```

## Conflict 발생 시
```
1. dev와 충돌 시:
   git checkout feature/#23-login
   git pull origin dev
   충돌 해결
   git push

2. 담당자가 해결 원칙
   - 담당자가 자기 브랜치 충돌 해결
   - 도움 필요 시 팀원에게 요청 가능

Commit Convention (수정)
형식
<type>: <내용>

예시:
feat: 로그인 기능 추가
fix: 아이콘 활성화 오류 수정
Type 정의
feat:     기능 추가/변경
fix:      버그 수정
docs:     문서 작업
refactor: 기능 동일, 내부 처리 변경
test:     테스트 관련
ci:       CI/CD yaml 수정
style:    코드 포맷, 주석, 공백 등
chore:    기타 작업 (빌드, 패키지 등)
예시
bash✅ 좋은 예시:
feat: 사용자 로그인 API 연동
fix: 아이콘 클릭 시 활성화 표시 버그 수정
docs: README 설치 가이드 추가
refactor: 임베딩 처리 로직 최적화
test: 로그인 기능 단위 테스트 추가
ci: GitHub Actions 워크플로우 수정
style: 코드 포맷팅 및 주석 정리
chore: 의존성 패키지 업데이트

❌ 나쁜 예시:
수정
로그인 만듦
기능 추가함
```

## 규칙
```
- 소문자로 시작
- 마침표 없이 끝내기
- 명령형으로 작성 ("추가한다" ❌, "추가" ✅)
- 한 커밋은 한 가지 작업만
- 50자 이내로 간결하게
```

---

## 이슈 번호는 어디에?
```
❌ 커밋: feat: 로그인 추가 (이슈번호 없음)
✅ PR 제목: [#23] 로그인 기능 구현
✅ PR 본문: Closes #23

장점:
- 커밋은 자유롭게 작은 단위로
- PR에서 이슈와 연결
- 커밋 메시지 심플

디렉션파일

# 아키텍처 (2025.11.03 확정)

## 전체 아키텍처

```
Client (Web/Mobile)
    ↓
Spring Boot Server (Auth, API Gateway, Business Logic)
    ↓
RabbitMQ (Message Queue - 비동기 처리)
    ↓
FastAPI Server (AI 처리, Embedding, RAG)
    ↓
PostgreSQL 17 + pgvector (데이터 저장 + 벡터 검색)
    ↓
External APIs (DART, Upstage, News API)

[모니터링]
Prometheus + Grafana + Loki + Promtail
```

## 아키텍처 결정 사항

### ✅ 확정된 사항
1. **메시지큐 도입**: RabbitMQ를 통한 Spring ↔ FastAPI 비동기 처리
   - 대용량 트래픽 대응
   - Spring과 FastAPI 간 결합도 낮춤
   - 재시도 및 DLQ로 안정성 확보

2. **비동기 아키텍처**: 3계층 비동기 처리
   - Layer 1: Spring Boot (사용자 요청 수신)
   - Layer 2: RabbitMQ (메시지 큐잉)
   - Layer 3: FastAPI (AI 처리 및 응답)

3. **데이터 흐름**:
   - 클라이언트 → Spring (인증, 검증)
   - Spring → RabbitMQ (작업 큐잉)
   - RabbitMQ → FastAPI (AI 처리)
   - FastAPI → PostgreSQL (벡터 검색, 데이터 저장)
   - FastAPI → External APIs (DART, Upstage 등)

### 🔄 검토 필요 사항 (다음 회의)
1. **에이전트 위치**: AI Agent를 어느 계층에서 실행할지 결정
   - 옵션 1: FastAPI 내부에서 Agent 실행
   - 옵션 2: 별도 Agent 서비스 분리

2. **실행 순서 검증**:
   - 클라이언트 요청 시 바로 DART로 가는지?
   - 아니면 Spring → Cache 확인 → DART 순서인지?

3. **상세 Use Case 다이어그램 작성 필요**

---

# 개발 프로세스

## 코드 품질 관리
1. 코드래빗 기반 PR 자동 AI 리뷰 고려 중
2. 커밋 컨벤션은 확정됨 (위 섹션 참조)

## 다음 회의 안건 (TODO)
1. 상세 Use Case 다이어그램 작성
2. AI Agent 아키텍처 위치 결정
3. 데이터 흐름 실행 순서 최종 확정

# 기술스택 (확정 - 2025.11.03 회의)

## Backend - Spring Boot

### Spring Boot
- **버전**: Spring Boot 3
- **Java 버전**: Spring Boot 3 호환 버전 (Java 17+)
- **참고**: https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Release-Notes

### ORM 및 Database 접근
- **JPA**: 기본 의존성 사용 (디폴트 설정)
- **QueryDSL**: 타입 세이프 쿼리 작성

### API 명세
- **도구**: Spring Doc (Swagger)
- **선정 이유**:
  - FastAPI가 기본 지원하므로 호환성 확보
  - 잦은 수정 예상으로 개발 생산성 우선
  - RestDocs 대비 실시간 수정 용이
- **Swagger 문제점 및 해결책**:
  - ❌ 문제: 프로덕션 코드에 문서화 어노테이션 침투로 가독성 저하
  - ✅ 해결: Controller에서 docs 명세를 interface로 분리
  - ⚠️ 한계: DTO 어노테이션은 분리 불가능
- **RestDocs 미선택 이유**:
  - TDD 기반 테스트 작성 예정이지만, 문서화를 위한 추가 테스트는 생산성 저해

---

## Backend - FastAPI

### Python & FastAPI
- **Python 버전**: 3.11.9
- **FastAPI 버전**: 0.115.0
- **선정 이유**:
  - 개발 생산 속도가 빠름
  - 레퍼런스 풍부 및 학습 곡선 낮음
  - 메인 DB 관리는 Spring에서 담당하므로 AI 처리에 집중

---

## Database

### PostgreSQL + pgvector
- **버전**: PostgreSQL 17
- **확장**: pgvector 0.9
- **선정 배경**:
  - Auth/회원 DB와 벡터 DB 분리 검토했으나, 규모 대비 비용/관리 포인트 증가로 통합 결정
  - 팀원 모두 SQL 경험 보유
- **버전 선정 이유**:
  - PostgreSQL 15 (2022년, 5년 지원 보장) 고려했으나
  - 최신 pgvector 0.9 + LangChain 1.0 호환성을 위해 17 선택

---

## Message Queue

### RabbitMQ
- **필요성**: Spring - FastAPI - Database 3계층 비동기 아키텍처로 대용량 트래픽 대응
- **선정 이유**: Redis / RabbitMQ / Kafka 비교

| 평가 항목 | 우리 요구사항 | Redis | RabbitMQ | Kafka |
|---------|------------|-------|----------|-------|
| 요청-응답 비동기 처리 | ✅ 필요 | ⚠️ 유실 위험 | ✅ 안정적 | ✅ 가능하지만 복잡 |
| 재시도 및 DLQ | ✅ 필요 | ❌ 불가능 | ✅ 내장 기능 | ⚠️ 직접 구현 |
| 메시지 순서 및 보존 | ✅ 필요 | ❌ 없음 | ✅ 큐 단위 보존 | ✅ 로그 단위 보존 |
| 운영비용 | 💰 저렴해야 함 | ✅ 매우 저렴 | ✅ 저렴 | ❌ 비쌈 |
| 모니터링 | ✅ Prometheus 통합 | ⚠️ 기본 수준 | ✅ 강력한 Exporter 내장 | ✅ 가능 (설정 복잡) |
| 향후 확장성 | ✅ AI 파이프라인 확장 예정 | ⚠️ 제한적 | ✅ 수평확장 용이 | ✅ 고성능 확장 |
| 학습 곡선 / 관리 편의성 | ✅ 낮을수록 좋음 | ✅ 쉬움 | ✅ 쉬움 | ❌ 어려움 |
| **종합 평가** | — | ❌ 유실형 알림 수준 | 🏆 ✅ 균형 잡힌 실무형 선택 | ⚠️ 대규모 로그용, 과도함 |

**RabbitMQ 선정 종합 이유**:
- ✅ 기술적: 비동기 메시지 보장 (ACK 기반, DLQ), 메시지 라우팅 및 우선순위 제어 가능
- ✅ 운영/비용: Kafka 대비 인프라 1/5 수준, 단일 브로커로 10만 msg/s 처리 가능
- ✅ 확장: AI Job Worker 수평 확장 시 Consumer Pool만 확장, Prometheus + Grafana 실시간 모니터링

---

## 모니터링

### Prometheus + Grafana + Loki + Promtail

**도입 필요성**:
- Spring Boot – FastAPI – RabbitMQ – PostgreSQL 비동기 아키텍처
- 요청 흐름 추적 어려움, 장애 구간 파악 어려움
- RabbitMQ 큐 적체, FastAPI 워커 지연 시 Spring은 정상처럼 보이는 문제
- 메트릭 기반 모니터링 + 로그 기반 진단 시스템 필수

| 구성요소 | 역할 | 비고 |
|---------|------|------|
| **Prometheus** | 메트릭 수집 (CPU, Memory, Queue backlog, 처리율 등) | RabbitMQ / Spring / FastAPI 공식 exporter 풍부 |
| **Grafana** | 대시보드 및 알람 시각화 | Prometheus, Loki 모두 통합 관리 |
| **Loki** | 로그 저장소 (라벨 기반 저장) | Elasticsearch 대비 1/10 수준 리소스 |
| **Promtail** | 로그 수집기 (Loki로 push) | 도커 컨테이너 로그 자동 라벨링 |

**선정 이유**:
1. **비용 및 운영 효율성**
   - ELK 대비 리소스 사용량 10~20% 수준 (모두 Go 기반)
   - 오픈소스, 라이선스 제약 없음
   - Docker 기반 `docker-compose up`으로 구축 가능

2. **확장성 및 실무 적합성**
   - Prometheus exporter 방식으로 RabbitMQ, DB 등 메트릭 수집
   - Promtail은 Docker 로그 경로 자동 수집
   - Loki는 인덱싱 없이 라벨 기반 쿼리로 빠른 검색

3. **시각화 및 운영 편의성**
   - Grafana에서 메트릭과 로그 한 화면 Cross-Filter
   - 지연 발생 시 동일 타임라인 로그 즉시 확인
   - Alertmanager 연동으로 Slack, Email 실시간 알림

4. **아키텍처 호환성**
   - Spring Boot Actuator + Micrometer → Prometheus 연동 용이
   - RabbitMQ → `rabbitmq_prometheus` 플러그인으로 큐 상태 추적
   - FastAPI → uvicorn 로그, 응답 시간 등 Promtail 자동 수집

**모니터링 아키텍처**:
```
┌─────────────────────────┐
│     Dockerized App      │
│  (Spring, FastAPI 등)   │
│  writes /var/log/*.log  │
└────────────┬────────────┘
             │
      [Promtail Container]
             │ push logs
             ▼
        [Loki Container]
             │ query API
             ▼
      [Grafana Container]
             ▲
             │ scrape metrics
    [Prometheus Container]
```

**RabbitMQ vs Redis Exporter 비교**:

| 항목 | Redis Exporter | RabbitMQ Exporter |
|------|---------------|-------------------|
| **공식 제공 여부** | ✅ Prometheus community 제공 | ✅ RabbitMQ 공식 제공 (plugin 내장) |
| **설치 위치** | Redis와 별도 실행 (sidecar) | RabbitMQ 내부 플러그인 활성화만 하면 됨 |
| **메트릭 종류** | 메모리, 커넥션, 캐시 히트율, 처리량, 레이턴시 → **리소스 상태 중심** | 큐별 메시지 수, 소비자 수, Ack율, DLQ 적체량, 처리속도, 재시도율 → **메시지 흐름 중심** |
| **메트릭 초점** | 서버 성능 모니터링 | 메시지 흐름 모니터링 |
| **Alert 예시** | Redis down, Memory > 90%, Latency ↑ | Queue backlog ↑, Consumer fail ↑, DLQ 증가 |
| **운영 관점** | 서버가 죽는지, 느려졌는지 감지 | 작업량/적체 상태 직접 추적 |

---

## CI/CD

### GitHub Actions
- **선정 이유**:
  - GitHub 기반 이슈/PR/브랜치 관리 중이므로 즉시 적용 가능
  - Jenkins 대비: 별도 서버 불필요, 플러그인 관리 부담 없음, HA 고려 불필요
  - 배포 자동화까지 지원으로 인프라 부담 경감
- **자동화 대상**: 시간이 많이 걸리거나 사람이 추적 관리해야 하는 부분

---

## 인프라

### AWS 프리티어
- **배포 위치**: 단일 서버 (비용 절감 + 관리 포인트 축소)
- **구성 요소**:
  - Spring Boot 서버
  - FastAPI 서버
  - PostgreSQL
  - RabbitMQ
  - 모니터링 스택 (Prometheus, Grafana, Loki, Promtail)
- **선정 이유**:
  - 외부 독립 환경으로 안정성 확보
  - Docker 사용 용이
  - 가격 경쟁력

### AI 추론 서버
- **Upstage API**: 임베딩 및 생성 API 외부 사용

---

## 기타

### 코드 품질 관리
- **코드 리뷰**: 코드래빗 기반 PR 자동 AI 리뷰 고려 중

---

# 개발 목표

## 단기 목표 (토요일)
- 각 개인이 작업한 것 병합
- **최소 페이지 1개 완성**
