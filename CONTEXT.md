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


# AWS Spring 초기설정
```
# 1. 시스템 업데이트 & 타임존 한국 설정 (로그 시간 맞추기 위해 필수)
sudo apt-get update && sudo apt-get upgrade -y
sudo timedatectl set-timezone Asia/Seoul

# 2. 필수 유틸리티 & JDK 17 설치 (Spring Boot 3 필수)
sudo apt-get install -y openjdk-17-jdk htop net-tools unzip curl git

# 3. Docker & Docker Compose 설치 (배포의 핵심)
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu  # sudo 없이 도커 쓰게 권한 부여
sudo apt-get install -y docker-compose-plugin

# 4. 스왑 메모리 2GB 설정 (서버 다운 방지용 생명보험)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab



# 설치 확인
java -version
# (결과: openjdk version "17.0..." 뜨면 OK)

docker -v
# (결과: Docker version 24... 뜨면 OK)

free -h
# (결과: Swap 행에 2.0Gi 라고 잡혀있으면 OK)
```


# FastApi Server 초기 설정
```
# 1. 시스템 업데이트 & 타임존 한국 설정
sudo apt-get update && sudo apt-get upgrade -y
sudo timedatectl set-timezone Asia/Seoul

# 2. 필수 유틸리티 & Python 빌드 라이브러리 설치 (FastAPI/uv 구동용)
sudo apt-get install -y git make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev htop net-tools unzip

# 3. Docker 설치 (agent_test.py 등 MCP 서버 실행에 필수)
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker ubuntu  # sudo 없이 도커 쓰게 권한 부여

# 4. uv (Python 패키지 매니저) & Python 3.11 설치
curl -LsSf https://astral.sh/uv/install.sh | sh
source $HOME/.cargo/env
uv python install 3.11

# 5. 스왑 메모리 2GB 설정 (EC2 멈춤 방지용 필수)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab


# 잘 깔렸는지 확인
# Python & uv 버전 확인 (uv x.x.x 뜨면 OK)
uv --version
uv python list

# Docker 확인 (Docker version 24... 뜨면 OK)
docker -v

# 스왑 메모리 확인 (Swap 행에 2.0Gi 잡혀있으면 OK)
free -h



# 이후 직접 해당 디렉터리 들어가서 가상환경 설치
# 1. Python 3.11 기반 가상환경(.venv) 생성
uv venv .venv --python 3.11

# 2. 가상환경 활성화 (터미널 앞에 (.venv)가 생김)
source .venv/bin/activate

# 3. 필수 패키지 설치 (엄청 빠릅니다)
uv pip install -r requirements.in
```

